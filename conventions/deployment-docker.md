# Deployment: Docker

A minimal **deploy** contract for shipping your project as a single container image. This is a floor, not a ceiling — it does not constrain your code design, stack, architecture, patterns, or testing. It only describes what an image must respect to run behind a reverse proxy (TLS terminator) as a single-container target.

## How this relates to local preview (read this first)

Local preview runs your app **from source** — it detects the framework by inspecting source markers (`package.json`, `mix.exs`, `requirements.txt` + `Procfile`, a root `index.html`, or a prebuilt output dir). It does **not** build your Dockerfile to preview.

So keep both paths intact:

- **Source markers** drive the local preview path. Keep `package.json` / `mix.exs` / `requirements.txt` + `Procfile` / `index.html` in place.
- **The Dockerfile** is the deploy path. Add it for shipping; it does not change preview.

⚠️ **If the repo has only a `Dockerfile` (or `docker-compose.yml`) and no source markers, local preview is blocked** — it gets classified as container-only and cannot be previewed from source. The fix is to keep your real source files in the repo alongside the Dockerfile, not to remove the Dockerfile.

## Image contract

- **Single port, monolithic.** One container exposes one port. If you have a static frontend, serve it from the same backend on that one port. (Single port is the recommended shape, not a forced architecture.)
- **Respect `PORT`.** Bind to the `PORT` environment variable at runtime; never
  hardcode a port. Local preview supplies a loopback `HOST`; Hestia injects
  `PORT` but not `HOST`, so a deployed container must bind `0.0.0.0:$PORT`.
- **Plain HTTP.** Listen in plaintext HTTP. TLS is terminated upstream by the proxy/orchestrator. Do **not** force `https://` or self-redirect to HTTPS.
- **Config via env.** Read all config and secrets from environment variables. Never bake secrets into the image or commit them.
- **Multi-stage build.** Build in one stage, copy artifacts into a slim runtime stage — smaller, faster, fewer attack surfaces.
- **Non-root.** Run the process as a non-root user.
- **Small base image.** Use a slim/alpine or distroless runtime base where practical.

## Skeletons per stack

These are minimal starting points. Adapt freely.

### Static site
Serve the **built** files with a small static server. Make it honor `PORT` and add SPA fallback if you have client-side routing.

```dockerfile
FROM node:lts-slim AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:lts-slim
WORKDIR /app
# Bake the static server at BUILD time — the deploy runtime rootfs is read-only
# (only /tmp is writable), so nothing can be installed or written at boot.
RUN npm i -g serve
COPY --from=build /app/dist ./dist
USER node
CMD ["sh", "-c", "serve -s dist -l tcp://0.0.0.0:${PORT:-3000}"]
```

**Never use dev tooling as the deploy CMD** — `vite preview`, `next dev`, `npm run dev`.
`vite preview` bundles `vite.config.*` to a temp file **next to the config** at boot;
under the read-only rootfs it dies with EACCES before it ever listens (the router then
shows "no available server"). This is Vite-internal behavior — moving `HOME`/npm cache
to `/tmp` does not avoid it. An `nginx` base needs the same care (it writes cache/pid
paths at boot); the `serve` shape above matches the platform's own static recipe.


### Node backend (build → slim runtime)
```dockerfile
FROM node:lts-slim AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build   # if you have a build step

FROM node:lts-slim
WORKDIR /app
ENV NODE_ENV=production
COPY --from=build /app ./
USER node
# Bind to process.env.PORT inside your start command.
CMD ["npm", "start"]
```

### React Router v8 Framework Mode (stable successor to Remix v1/v2)

React Router v8 has two different image shapes: an SSR/BFF Node process and a
static `build/client` image. Do not treat both as a generic Vite `dist/` build.
Use the pinned, non-root reference images and matching `.dockerignore` in
`stack-react-router-v8.md`.

### Phoenix / Elixir (build → release)
```dockerfile
FROM hexpm/elixir:1.16-otp-26-alpine AS build
WORKDIR /app
ENV MIX_ENV=prod
RUN mix local.hex --force && mix local.rebar --force
COPY mix.exs mix.lock ./
RUN mix deps.get --only prod && mix deps.compile
COPY . .
RUN mix assets.deploy && mix release

FROM alpine:3.19
RUN adduser -D app
WORKDIR /app
COPY --from=build /app/_build/prod/rel/my_app ./
USER app
# The release reads PORT, PHX_HOST, SECRET_KEY_BASE, DATABASE_URL from the env.
CMD ["bin/my_app", "start"]
```

### Python backend (deps → slim runtime)
```dockerfile
FROM python:3.12-slim AS build
WORKDIR /app
COPY requirements.txt ./
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

FROM python:3.12-slim
WORKDIR /app
RUN useradd --create-home app
COPY --from=build /install /usr/local
COPY . .
USER app
# Same production server as the Procfile web: line — never flask run /
# manage.py runserver / --reload (dev tooling; read-only rootfs at deploy).
CMD ["sh", "-c", "uvicorn main:app --host 0.0.0.0 --port ${PORT:-8000}"]
```

## Landmines seen in production (each of these broke a real publish)

- **Pin base images to tags that exist.** `FROM ${VAR}` fails preflight, and a
  pinned tag that isn't on the registry fails before the build with a clear
  message — verify the exact tag on Docker Hub before pinning.
- **Prisma (or any engine-downloading ORM): install `openssl ca-certificates`
  in the BUILD stage too**, not just runtime. Without it `prisma generate`
  detects the wrong openssl and bakes mismatched engines; the runtime re-download
  then dies on the read-only rootfs (surfaces as a migrate-job timeout).
- **Monorepo: the Dockerfile must copy everything the build references.**
  `assets`/CSS/esbuild imports of `../../packages/*` mean those packages must be
  copied into the image (copy the whole `packages/` dir, not files one by one).
- **Workspace packages consumed by a compiled CJS runtime must ship built JS.**
  An `exports` map pointing only at `./src/index.ts` crashes the runtime with
  `Cannot use import statement outside a module` — build `dist/` and split
  exports (`require` → `./dist/index.js`, `import`/`types` → source).
- **Elixir releases: never put `:code.priv_dir` in a module attribute.** It
  freezes the compile-time `_build/...` path, so the release can't find the file
  at runtime (works in dev, always broken in the release). Evaluate at runtime.
- **Verify before you commit:** run `docker build` on every Dockerfile at least
  once, and boot the app in its deploy form (the release / the built image), not
  just `npm run dev` — several of the failures above are invisible in dev mode.

## Checklist

- [ ] Multi-stage build (build stage → slim runtime stage).
- [ ] Every Dockerfile passed at least one real `docker build`; the app booted in its deploy form.
- [ ] Deploy CMD is a production server, **never** dev tooling (`vite preview` / `next dev` / `npm run dev`); static apps serve the built output.
- [ ] Binds to `PORT`; no hardcoded port.
- [ ] Plain HTTP only; no forced HTTPS / self-redirect.
- [ ] Single port; static frontend served by the same process.
- [ ] Runs as non-root, slim base image.
- [ ] Secrets read from env; nothing secret baked into the image.
- [ ] **Source markers (`package.json` / `mix.exs` / `requirements.txt` + `Procfile` / `index.html`) kept in the repo** so local preview still works.
