# Marketplace

## Identity

Use this profile for two-sided products where visitors browse a catalog of listings
made by other users and act on one: book, buy, upvote, or contact. Reference
products: Airbnb, Etsy, Product Hunt.

Belongs here: rentals, goods marketplaces, directories, launch/upvote sites, job
boards.

Does not belong here: a single seller's store with a cart (a future
`ecommerce-storefront` profile), team tools (use
`design/profiles/saas-workspace.md`), or system consoles (use
`design/profiles/admin-dashboard.md`).

## Shell

- No sidebar. Top bar 64–80 px tall: logo on the left; a prominent, rounded search
  bar at centre with 2–3 facets (for example where/when/who); right side holds the
  supply-side call to action as text (for example "Become a host", "Sell on…",
  "Submit"), notifications, and the avatar menu.
- Avatar menu holds, in order: Messages, Trips/Orders/My listings, Wishlist,
  Account settings, Help, Log out. Settings lives only in this menu, never in the
  top bar.
- Below 768 px the search bar collapses to a single pill. A bottom tab bar with
  4–5 tabs (Explore, Wishlist, Orders/Trips, Messages, Profile) replaces the avatar
  menu; a hamburger is not used at any width.
- A category chips row sits under the top bar on browse pages and stays sticky on
  scroll.
- A footer with grouped links appears on every public page; hide it inside
  checkout or booking flows.

## Density and tone

Keep the interface airy and photo-led.

- Base grid: 8 px. Spacing steps: 16, 24, 32, 48, 64.
- Type steps: 14, 16, 18, 22, 32 px, with 16 px as the body size.
- Cards use a 12 px corner radius and a 4:3 image aspect ratio (1:1 for goods).
- Text sits on `--color-bg`.
- Shadows appear only on hover and on the sticky action panel.
- Reserve `--color-primary` for the single conversion button per page.

## Common rules

- Browse pages are card grids: 1 column below 640 px, 2 columns at 640–1023 px,
  3–4 columns at 1024 px and above. Each card shows an image, a title, one line of
  meta, a price or score, and a save/upvote affordance at the image's top-right.
- Listing detail: gallery first, then title and meta, then a two-column body with
  the description on the left and a sticky action panel on the right (price,
  date/quantity pickers, the one primary button). Below 1024 px the panel becomes
  a sticky bottom bar.
- Trust elements — ratings, review count, verified badge, host/seller card —
  appear above the fold on detail pages.
- Supply-side screens (create listing, seller dashboard) switch to the
  `design/profiles/saas-workspace.md` shell rules for that area only; state this
  switch in the proof.
- Destructive actions (cancel booking, delete listing) confirm in a modal that
  restates the consequences (fees, dates).
- Never hardcode colours; use role tokens (`--color-bg`, `--color-surface`,
  `--color-border`, `--color-text`, `--color-text-muted`, `--color-primary`,
  `--color-danger`) only.

## Screen variations

- `design/screens/app-shell-and-navigation.md`: follow the Shell section above;
  the mobile bottom tab bar replaces both the hamburger and the sidebar.
- `design/screens/list-and-detail.md`: card grid plus a full-page detail with a
  sticky action panel; filters open in a modal ("Filters" button with an active
  count) at every size.
- `design/screens/create-and-edit-forms.md`: listing creation is a multi-step
  full-page flow with one topic per step (photos, details, pricing) and a
  persistent progress bar.
- `design/screens/settings-page.md`: the account page, reached from the avatar,
  lays out sections as stacked cards rather than a sub-nav, unless there are more
  than 6 sections.
- `design/screens/onboarding-flow.md`: role choice (browse vs. supply), then
  location/interests, then a first save or a first listing draft; browsers can
  skip everything.
- `design/screens/empty-loading-error-states.md`: empty search results show
  "Clear filters" first; wishlist and orders empty states point back to Explore.

## Checklist

- [ ] No sidebar; top bar has logo left, prominent search centre, supply-side CTA + notifications + avatar right
- [ ] Settings, orders/trips, and messages open from the avatar menu
- [ ] Below 768 px a bottom tab bar (4–5 tabs) replaces the avatar menu and search collapses to a pill
- [ ] Browse pages are responsive card grids (1 / 2 / 3–4 columns) with a save or upvote control on each card
- [ ] Listing detail shows gallery, title/meta, and trust elements above the fold
- [ ] Listing detail has one sticky action panel (right on desktop, bottom bar below 1024 px) with the single primary button
- [ ] Filters open in a modal from a button that shows the active-filter count
- [ ] Footer appears on public pages and is hidden inside booking/checkout
- [ ] Spacing uses the 16/24/32/48/64 scale; body text is 16 px; cards use 12 px radius
- [ ] Colours come from role tokens only; the primary colour is used for one conversion button per page
