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
- Avatar menu holds, in order: Messages; the transaction record (Trips,
  Orders, Applications, or My listings, as the product calls it);
  Saves/Wishlist (omit if the product has none); Account settings; Help; Log out.
  Settings lives only in this menu, never in the top bar.
- Below 768 px the search bar collapses to a single pill. A bottom tab bar with
  4–5 tabs (Explore, Orders/Trips, Saves, Messages, Profile) replaces the avatar
  menu. Buyer-side pages never use a hamburger; supply-side areas follow the
  saas-workspace drawer rule instead (see Common rules).
- A category chips row sits under the top bar on browse pages and stays sticky on
  scroll.
- A footer with grouped links appears on every public page; hide it inside
  checkout or booking flows.

## Density and tone

Keep it airy. Rentals and goods are photo-led; launch sites and job boards are
rank-led (vote count or timestamp dominates).

- Base grid: 8 px. Spacing steps: 8, 16, 24, 32, 48, 64.
- Type steps: 14, 16, 18, 22, 32 px, with 16 px as the body size.
- Cards use a 12 px corner radius; lead images are 4:3 (1:1 for goods).
- Page background is `--color-bg`; only cards and the sticky action panel use
  `--color-surface`.
- Shadows appear only on hover and on the sticky action panel.
- Reserve filled `--color-primary` for the one conversion button per page (Book,
  Buy, Submit). Save/upvote controls are outline or `--color-text-muted` at rest
  and fill only when active.

## Common rules

- Browse pages are card grids: 1 column below 640 px, 2 columns at 640–1023 px,
  3–4 columns at 1024 px and above. Each card shows a title, one meta line, a
  price/score/vote count, and a save/upvote control top-right. Photo-led
  products add a lead image; rank-led ones a small logo, or none.
- Listing detail: gallery first, then title and meta, then a two-column body with
  the description on the left and a sticky action panel on the right (for
  example price, date/quantity pickers, and the one primary button). Below 1024 px the panel becomes
  a sticky bottom bar.
- Trust elements — ratings, review count, verified badge, host/seller/maker
  card — appear above the fold on detail pages.
- Supply-side screens (create listing, seller dashboard) use the
  `design/profiles/saas-workspace.md` Shell rules (sidebar, hamburger, drawer)
  for that area only; density and tone stay marketplace; state this in the proof.
- Destructive actions (cancel booking, delete listing) confirm in a modal that
  restates the consequences (fees, dates) and uses `--color-danger` on the
  confirm button.
- Never hardcode colours; use role tokens (`--color-bg`, `--color-surface`,
  `--color-border`, `--color-text`, `--color-text-muted`, `--color-primary`,
  `--color-danger`) only.

## Screen variations

- `design/screens/app-shell-and-navigation.md`: follow the Shell section;
  buyer-side pages have no sidebar or hamburger; on mobile the tab bar replaces
  the avatar menu.
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
- `design/screens/empty-loading-error-states.md`: empty search shows "Clear
  filters" first, then related suggestions; wishlist/orders empties link to Explore.

## Checklist

- [ ] No sidebar; top bar has logo left, prominent search centre, supply-side CTA + notifications + avatar right
- [ ] Settings, orders/trips, and messages open from the avatar menu (desktop; on mobile they live behind the Profile tab)
- [ ] Below 768 px a bottom tab bar (4–5 tabs) replaces the avatar menu and search collapses to a pill
- [ ] Browse pages are responsive card grids (1 / 2 / 3–4 columns) with a save or upvote control on each card
- [ ] Listing detail shows gallery, title/meta, and trust elements above the fold
- [ ] Listing detail has one sticky action panel (right on desktop, bottom bar below 1024 px) with the single primary button
- [ ] Filters open in a modal from a button that shows the active-filter count
- [ ] Footer appears on public pages and is hidden inside booking/checkout
- [ ] Spacing uses the 8/16/24/32/48/64 scale; body text is 16 px; cards use 12 px radius
- [ ] Colours come from role tokens only (checked in the diff); the filled primary colour appears on one conversion button per page, save/upvote controls only when active
