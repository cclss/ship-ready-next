# App shell and navigation

## Read this when

The card builds or changes the app frame, sidebar, top bar, menus, route layout, or
how pages are reached.

## Anatomy

1. **Navigation container** — sidebar, top bar, or bottom tab bar, per the profile.
2. **Context switcher** — workspace, organisation, or environment; always the first
   element of the navigation.
3. **Global search trigger.**
4. **Primary navigation** — up to the profile's item cap; each item has a route, an
   icon only where the profile uses icons, and a label. The active item is
   distinguishable without relying on colour alone.
5. **Utility area** — notifications, help, account menu.
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

- Navigation changes the route: use real URLs, and the browser back button returns
  to the prior view.
- The current route survives a full page reload.
- Drawer or rail collapse state persists per user (local storage is sufficient).
- `⌘/Ctrl+K` opens global search from any page.
- The account menu opens on click, not on hover.
- The context switcher lists the user's other contexts plus a "Create" entry.

## Copy rules

Navigation labels are one or two words, nouns, sentence case ("Projects", not "My
Projects list"). Never pair an icon with no label, except inside an icon rail, where
the label appears as a tooltip on hover or focus.

## Per-profile differences

`design/profiles/saas-workspace.md` — the sidebar carries the workspace switcher,
search, and the "New" button at the top; the avatar menu sits at the bottom and is
the only place Settings and Sign out appear.

`design/profiles/admin-dashboard.md` — the sidebar groups items under labelled
sections, with Settings as its own item last; the organisation/project switcher and
the environment toggle (when the product has environments) sit in the top bar.

`design/profiles/marketplace.md` — there is no sidebar; navigation is a top bar,
with a bottom tab bar replacing it below the profile's mobile breakpoint. Supply-side
areas (create listing, seller dashboard) may switch to a sidebar for that area only;
record the switch in the proof.

## Checklist

- [ ] The frame renders a skeleton, never a blank region, while workspace data loads
- [ ] Every navigation item maps to a real URL; browser back/forward and reload restore the same view
- [ ] The active item is distinguishable without colour alone (weight, background, or indicator)
- [ ] Context switcher (workspace/org/env) is the first element of the navigation and lists other contexts plus "Create"
- [ ] ⌘/Ctrl+K opens global search from any page
- [ ] The mobile drawer or tab bar behaves as the profile prescribes; the drawer traps focus and closes on Esc
- [ ] Account menu opens on click and contains Settings and Sign out
- [ ] Content region has a page header with title (and actions at the right) on every page
