# Design templates for ship-ready

- **Status**: accepted (2026-09-09)
- **Repo**: `cclss/ship-ready-next` (staging copy of `cclss/ship-ready`; verified commits are promoted 1:1 to `ship-ready` `main`)
- **Consumer**: coding agents (Charlie) working on devkanban issue cards inside a product repo created from this template

## Problem

Products created from ship-ready get run/deploy conventions but no design guidance, so every UI card
reinvents the shell: where the navigation lives, where the primary button goes, what an empty list
looks like. We want a library of Markdown "design briefs" — distilled from well-known SaaS products
(public companies, Product Hunt all-time leaders) — that an agent follows **without reading all of it**.
Only the documents relevant to the card at hand are opened.

## Decisions

1. **Two layers.** A *profile* (product type) is fixed once per product; *screen* documents are read
   per card. The profile answers product-wide questions (nav model, hamburger placement, where
   settings live); a screen document answers card-level questions (what a settings page contains).
2. **Profiles are product types, not brands.** `saas-workspace`, `admin-dashboard`, `marketplace`, …
   Each profile cites 3–5 reference products and records their *common* conventions. A product picks
   the type it belongs to; nobody "copies Linear".
3. **Screen documents are per screen, not per component.** One card ≈ one screen ≈ one file
   (`settings-page.md`, `onboarding-flow.md`). Component rules shared across screens live in the
   profile's "Common rules" section; a separate component layer is deferred until three or more
   screen documents visibly overlap.
4. **Verification is a checklist in the document.** Every profile and screen document ends with a
   checklist. The agent reproduces it in the card's proof, ticking each item ✓ / ✗ (with a reason) /
   n/a, and lists the design documents it read. This rides the existing proof review in devkanban;
   no automation.
5. **Profile selection is a pointer file.** `design/PROFILE.md` names the profile. If it is missing,
   the first agent that touches UI chooses a profile from the product description and board contents,
   writes the file (profile id, one-line reason, date), and continues. If it exists, it is
   authoritative; humans edit it to override. A devkanban wizard step can write the same file later.
6. **On-demand loading is structural, not a request.** `AGENTS.md` (always read) routes UI work to
   `design/INDEX.md`; the index routes to exactly one profile and one or two screen documents via a
   keyword table. Non-UI cards never reach `design/`.
7. **Environment split is by repository, not branch.** devkanban copies a template's default branch
   through GitHub's generate API, which cannot pick a branch. `ship-ready-next` is registered as a
   ready-made seed on dev/frontier; production keeps `ship-ready`.

## Layout

```
AGENTS.md                      + one routing row: "Building or changing a screen / UI → design/INDEX.md"
design/
  INDEX.md                     entry point (≤ 300 words): pick profile, pick screens, proof rule
  PROFILE.md                   pointer; absent in the template, written by the first UI card
  profiles/
    saas-workspace.md          Linear, Notion, Slack, Asana, Height
    admin-dashboard.md         Stripe, Vercel, Supabase, PostHog
    marketplace.md             Airbnb, Etsy, Product Hunt
  screens/
    app-shell-and-navigation.md
    list-and-detail.md
    create-and-edit-forms.md
    settings-page.md
    onboarding-flow.md
    empty-loading-error-states.md
```

v2 candidates (not in this iteration): profiles `consumer-social`, `dev-console`,
`ecommerce-storefront`, `creator-tool`, `content-publishing`; screens `auth-screens`,
`billing-and-plans`, `search-and-filters`, `notifications-and-activity`, `landing-page`.

## Reading budget

| Document | Limit |
|---|---|
| `design/INDEX.md` | 300 words |
| one profile | 900 words |
| one screen document | 600 words |
| per UI card, total | ≤ 4 files, ≤ 2,500 words |

Limits are enforced by a word-count check in the promotion checklist (see Testing), not by tooling.

## Document formats

**`design/INDEX.md`**
1. When to read this (UI trigger) and when not to.
2. Step 1 — profile: read `PROFILE.md`; if missing, choose from `profiles/` using the product
   description and board, write `PROFILE.md`, say so in the proof.
3. Step 2 — screens: keyword → file table (e.g. "settings, preferences, account, workspace admin →
   `screens/settings-page.md`"). Read one, at most two.
4. Proof rule: the two mandatory blocks (documents read; checklist with ✓ / ✗ reason / n/a).
5. Precedence: `PROFILE.md` > profile document > screen document > agent judgement. Existing code in
   the product wins over all of these when they conflict; note the conflict in the proof.

**Profile document** (identical skeleton in every profile)
1. Identity — what this type is, reference products, which products belong here / do not.
2. Shell — navigation model (sidebar / top bar / both), hamburger placement and the breakpoint at
   which it appears, primary nav item cap, where search, notifications, "new", settings and the
   account menu sit.
3. Density and tone — spacing and type scale steps, colour by **role token only** (never literals;
   matches the product's design-token rule), border/shadow policy.
4. Common rules — primary action top-right of the region it acts on, destructive actions behind an
   overflow menu plus confirmation, responsive collapse order, keyboard/focus basics.
5. Screen variations — how each `screens/*.md` default changes under this profile.
6. Checklist — 8–12 verifiable statements.

**Screen document**
1. Read this when — trigger keywords (mirrors the INDEX table).
2. Anatomy — regions in order, what each contains.
3. Required states — empty, loading, error, success/confirmation.
4. Interactions — what happens on primary/secondary/destructive actions, inline vs page vs modal.
5. Copy rules — titles, button labels, empty-state wording pattern.
6. Per-profile differences — one short paragraph per profile.
7. Checklist — 6–10 verifiable statements.

Checklist items are written so an outsider can tick them from a screenshot or a short click-through
("Sidebar is 240 px wide and collapses to icons below 1024 px", "Every list has an empty state with
one primary action").

## Proof contract

A UI card's proof must contain:

```
Design documents read: design/INDEX.md, design/PROFILE.md, design/profiles/saas-workspace.md, design/screens/settings-page.md
Design checklist:
- [✓] Settings opens from the account menu, bottom-left of the sidebar
- [✗] Sections are a left sub-nav — product already uses tabs; kept tabs
- [n/a] Billing section — no billing in this product
```

Missing blocks mean the card did not follow the design system; the reviewer treats it like a
missing preview-prep proof.

## Testing (dev environment)

1. Merge this branch to `ship-ready-next` `main`; register `cclss/ship-ready-next` as a ready-made
   seed in the dev admin.
2. Create a product from that seed (a team to-do app is a good fit for `saas-workspace`).
3. Run three UI cards written **without any design wording**: app shell + main list; settings page;
   onboarding. Then one non-UI card (an API endpoint or migration).
4. Pass criteria:
   - `design/PROFILE.md` exists after card 1, names a sensible profile, gives a reason.
   - Each UI card's proof has both mandatory blocks; the documents listed match the card.
   - The preview matches the profile's shell rules (nav model, hamburger, settings placement).
   - The non-UI card's proof mentions no design documents and the run log shows none were read.
   - Word counts: every document within its budget.
5. Promotion: once the four cards pass, push the same commits to `cclss/ship-ready` `main`.

## Out of scope

Component-level documents, automated screenshot/DOM checks, a profile picker in the devkanban
product wizard, and per-brand ("make it look like Linear") profiles.
