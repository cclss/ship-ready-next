# Admin dashboard

## Identity

Use this profile for consoles that operate or observe a system: payments,
deployments, databases, analytics. Users are operators who read numbers and
tables, then act. Reference products: Stripe Dashboard, Vercel, Supabase,
PostHog.

Belongs here: ops consoles, analytics products, developer dashboards,
back-office admin.

Does not belong here: collaborative object editing by a team (use
`design/profiles/saas-workspace.md`) or consumer browsing (use
`design/profiles/marketplace.md`).

## Shell

- Left sidebar, fixed. 224 px wide on viewports ≥ 1024 px, grouped into
  labelled sections: Overview, then product-area sections, then Developers,
  then Settings as its own item at the bottom. No icon rail at any width —
  labels matter here.
- Below 1024 px the sidebar hides behind a hamburger at the top-left of the
  top bar and opens as a full-height drawer.
- Top bar is 56 px tall. Left: organisation/project switcher. Immediately
  right of it: an environment toggle (for example Test/Live) when the
  product has environments. Centre-left: global search. Right: help,
  notifications, avatar.
- Overview page order, top to bottom: a KPI row of 4–6 stat tiles, then a
  chart, then recent-activity tables. Every stat tile shows a value, a
  delta versus the previous period, and the period label.
- Record detail opens in a right-side drawer when the record is small (a
  single payment) and on a full page when the record is large.

## Density and tone

Keep the interface data-dense.

- Base grid: 8 px. Spacing steps: 8, 16, 24, 32, 48.
- Type steps: 12, 13, 14, 16, 20, 28 px. 13 px is the table body size; 28 px
  is the KPI value size, set in tabular figures.
- Tables: full-width, sticky header, zebra striping off, row hover on.
- Ids, keys, and code render in monospace.
- Charts use `--color-primary` plus one muted tone from `--color-text-muted`,
  at most 4 series.
- Shadows: none. Dividers: 1 px, `--color-border`. Corner radius: 8 px on
  cards.

## Common rules

- Page header holds a title, a one-line description, and the primary action
  at the right (for example "Create payment link"). Secondary actions are
  outline buttons placed to its left.
- Every table has: search, filter chips, column visibility, pagination or
  infinite scroll with a visible row count, and export when the data is
  tabular.
- Put destructive or irreversible operations (rotate key, delete project) in
  a Danger zone at the bottom of the relevant settings page; require typing
  the resource name to confirm.
- Keep environment/tenant context visible in the top bar at all times; it
  never changes as a side effect of navigation.
- An empty table explains how data arrives (an install snippet, a connect
  integration step) rather than offering a "Create" action.
- Never hardcode colours; use role tokens (`--color-bg`, `--color-surface`,
  `--color-border`, `--color-text`, `--color-text-muted`, `--color-primary`,
  `--color-danger`) only.

## Screen variations

- `design/screens/app-shell-and-navigation.md`: sidebar section groups and
  the environment toggle follow the Shell section above.
- `design/screens/list-and-detail.md`: a data table paired with a full
  detail page that has a metadata sidebar (id, created, status).
- `design/screens/create-and-edit-forms.md`: a full page for anything with
  credentials or side effects; a modal only for 3 or fewer harmless fields.
- `design/screens/settings-page.md`: Settings is a sidebar item; inside it,
  a left sub-nav divides sections, with Danger zone last.
- `design/screens/onboarding-flow.md`: create org/project, then connect
  data (API key or install snippet), then verify the first event; the
  verify step shows a live "waiting for data" state.
- `design/screens/empty-loading-error-states.md`: skeletons for KPI tiles
  and table rows; errors surface a request id.

## Checklist

- [ ] Left sidebar is 224 px with labelled section groups and Settings as the last item; it becomes a drawer below 1024 px
- [ ] Top bar shows the organisation/project switcher and (if applicable) the environment toggle at the left, avatar at the right
- [ ] Overview page order is KPI tiles → chart → tables; each tile shows value, delta, and period
- [ ] Tables have sticky headers, search, filter chips, and pagination or a visible row count
- [ ] Ids, keys, and code render in monospace
- [ ] Page header has title, one-line description, and the primary action at the right
- [ ] Irreversible operations sit in a Danger zone and require typing the resource name
- [ ] Environment/tenant context is visible on every page and never changes implicitly
- [ ] Spacing uses the 8/16/24/32/48 scale; table body text is 13 px
- [ ] Colours come from role tokens only; charts use at most 4 series
