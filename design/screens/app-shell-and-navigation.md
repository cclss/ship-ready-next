# App shell and navigation

## Read this when

The card builds or changes the app frame, sidebar, top bar, menus, route layout, or
how pages are reached.

## Anatomy

1. **Navigation container** — sidebar, top bar, or bottom tab bar, per the profile.
2. **Context switcher** — the workspace or organisation/project switcher, where
   the profile defines one (marketplace has none); when present it comes first.
3. **Global search trigger.**
4. **Primary navigation** — up to the profile's item cap; each item has a route, an
   icon only where the profile uses icons, and a label. The active item is
   distinguishable without relying on colour alone.
5. **Utility area** — notifications, help, and the account (avatar) menu with the
   items the profile lists.
6. **Content region** — a `<main>` element with a page header: title, optional
   one-line description, and actions at the right.
7. **Optional detail panel.**

## Required states

- **Loading** — a navigation skeleton while workspace data loads; never render a
  blank frame.
- **Active** — the current route's nav item is marked as active.
- **Collapsed / rail / drawer** — per the profile's breakpoints. An open drawer
  traps focus and closes on `Esc` and on backdrop click.
- **Badged** — items that can carry unread items show a badge count.

## Interactions

- Navigation uses real URLs; the browser back button returns to the prior view.
- The current route survives a full page reload.
- Drawer or rail collapse state persists per user (local storage is sufficient).
- `⌘/Ctrl+K` opens global search from any page.
- The account or avatar menu opens on click, not on hover.
- The context switcher lists the user's other contexts plus a "Create" entry.

## Copy rules

Navigation labels are one or two words, nouns, sentence case ("Projects", not "My
Projects list"). Every icon carries a label, except inside an icon rail, where the
label is a tooltip on hover or focus.

## Per-profile differences

`design/profiles/saas-workspace.md` — sidebar with workspace switcher, search, and
New at the top; the avatar menu at the bottom is the only place Settings and Sign
out appear.

`design/profiles/admin-dashboard.md` — sidebar grouped under labelled sections with
Settings last; the organisation/project switcher and environment toggle sit in the
top bar.

`design/profiles/marketplace.md` — top bar only, no sidebar; on mobile the top bar
stays (search becomes a pill) and a bottom tab bar replaces the avatar menu.
Supply-side areas may switch to a sidebar for that area only; record it in the
proof.

## Checklist

- [ ] The frame renders a skeleton, never a blank region, while workspace data loads
- [ ] Every navigation item maps to a real URL; browser back/forward and reload restore the same view
- [ ] The active item is distinguishable without colour alone (weight, background, or indicator)
- [ ] Context switcher (if the profile has one) comes first in the navigation and lists other contexts plus "Create"
- [ ] ⌘/Ctrl+K opens global search from any page
- [ ] The mobile drawer or tab bar behaves as the profile prescribes; the drawer traps focus and closes on Esc
- [ ] Account/avatar menu opens on click and holds the items the profile lists
- [ ] Content region has a page header with title (and actions at the right) on every page this card touches
- [ ] Nav labels are one or two sentence-case nouns; no nav icon appears without a label (icon rail excepted, tooltip on hover)
- [ ] Collapsed/rail/drawer state survives a reload; items that can carry unread items show a badge count
