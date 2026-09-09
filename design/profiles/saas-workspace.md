# SaaS workspace

## Identity

Use this profile for internal or team products where a team, inside one workspace,
works on objects organised as lists: issues, docs, tasks, messages. Reference products: Linear
(issue tracker), Notion (docs/database), Slack (channels), Asana (tasks), Height.

Belongs here: project trackers, wikis, CRMs used by a team, chat, planning tools.

Does not belong here: a console for a deployed system (use
`design/profiles/admin-dashboard.md`) or a public catalog with buyers and sellers
(use `design/profiles/marketplace.md`).

## Shell

- Left sidebar, fixed. 240 px wide on viewports ≥ 1024 px. Collapses to a 64 px icon
  rail between 768–1023 px. Below 768 px it hides behind a hamburger at the top-left
  of the top bar and opens as a full-height drawer.
- Sidebar, top to bottom: workspace switcher (workspace name + chevron),
  search trigger (also bound to `⌘/Ctrl+K`), primary "New" button.
- Primary navigation holds at most 7 items, each with icon and label, grouped top to
  bottom into three blocks: an Inbox (or Notifications) entry first, then My items,
  then workspace sections such as Projects, Teams, or Docs. The active item gets a
  filled `--color-surface` background.
- Sidebar bottom: user avatar and name. Clicking it opens the account menu with
  Profile, Preferences, Workspace settings, and Sign out. Settings lives only in this
  menu, never in primary navigation.
- Top bar is 48 px tall: breadcrumb or page title on the left, view controls and page
  actions on the right. There is no global top navigation.
- An optional right panel, 320–400 px wide, shows a detail peek and closes with `Esc`.

## Density and tone

Keep the interface compact and keyboard-first.

- Base grid: 4 px. Spacing steps: 4, 8, 12, 16, 24, 32.
- Type steps: 12, 13, 14, 16, 20, 24 px, with 14 px as the body size.
- Dividers: 1 px, `--color-border`.
- Shadows: none, except on popovers.
- Corner radius: 6 px. Icon size: 16 px.
- Every list supports `j`/`k` or arrow-key navigation, and every menu shows a visible
  shortcut hint next to its label.

## Common rules

- Place the primary action of a region at that region's top-right: a page's primary
  action sits in the top bar, right side; a card's primary action sits in the card
  header, right side. Show exactly one primary button per view.
- Put destructive actions in an overflow (`…`) menu. Require a confirmation dialog
  whose confirm button uses `--color-danger` and states the target object's name.
- Prefer inline editing to modals: edit titles, statuses, and assignees in place.
  Reserve modals for creation flows with 3 or more fields.
- Collapse responsively in this order as width shrinks: right panel first, then
  sidebar to icon rail, then sidebar to drawer, then top-bar actions into an overflow
  menu.
- Never hardcode colours; use role tokens (`--color-bg`, `--color-surface`,
  `--color-border`, `--color-text`, `--color-text-muted`, `--color-primary`,
  `--color-danger`) only. Never hide the workspace switcher.

## Screen variations

- `design/screens/app-shell-and-navigation.md`: follow the Shell section above as-is.
- `design/screens/list-and-detail.md`: default to a dense table or board with a
  right-panel peek; open a full detail page only through an explicit open action.
- `design/screens/create-and-edit-forms.md`: creation with 3 or more fields uses a
  560 px modal, title field first, submit on `⌘/Ctrl+Enter`; creation with 1–2 fields
  (a new label, a new team) stays inline or in a small popover, per Common rules.
- `design/screens/settings-page.md`: opens from the account menu; uses a left
  sub-nav to divide sections.
- `design/screens/onboarding-flow.md`: workspace name, then invite members, then
  create the first object; skipping the invite step is allowed.
- `design/screens/empty-loading-error-states.md`: an empty list offers a
  "New" action naming the object type ("New task", "New doc") plus a keyboard hint.

## Checklist

- [ ] Left sidebar is 240 px on ≥ 1024 px, an icon rail at 768–1023 px, and a drawer behind a top-left hamburger below 768 px
- [ ] Sidebar top holds workspace switcher, search (⌘/Ctrl+K), and the New button, in that order
- [ ] Primary navigation has at most 7 items, each with icon and label
- [ ] Settings and Sign out open from the avatar menu at the bottom of the sidebar, not from primary navigation
- [ ] Top bar is 48 px with breadcrumb/title left and page actions right; there is no global top navigation
- [ ] Exactly one primary button per view, placed top-right of the region it acts on
- [ ] Destructive actions are in an overflow menu and confirm with a danger-coloured button naming the object
- [ ] Spacing uses the 4/8/12/16/24/32 scale; body text is 14 px
- [ ] Colours come from role tokens only; no literal colour values in new code (checked in the diff, not the screenshot)
- [ ] Lists support keyboard navigation and menus show shortcut hints
- [ ] Workspace switcher stays visible in every sidebar state; nothing hides or collapses it away
- [ ] Right panel, when used, is 320–400 px wide and closes with Esc
