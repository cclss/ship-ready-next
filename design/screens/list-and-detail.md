# List and detail

## Read this when

The card shows a collection (table, board, grid, feed, search results) and/or a
single item's page or panel.

## Anatomy

**List header** — title with a count ("Issues · 42"), search input, filter
controls, a view switcher (only if the list offers more than one view), sort, and
the primary "New" action at the right.

**List body** — rows or cards showing only the fields that decide a click (title,
status, owner, updated); one visual density per list; selection checkboxes appear
on hover or once an item is selected.

**Bulk action bar** — replaces the header when one or more items are selected:
count, actions, a clear control.

**Detail** — a page or a side panel, per the profile. Header (title, status,
primary action, overflow menu), metadata block (owner, dates, ids), body, then
activity or comments last.

**Pagination or infinite scroll**, with a visible total.

## Required states

- **Loading** — a skeleton matching the row or card height.
- **Empty** — first-use empty and filtered-empty are different screens; see
  `design/screens/empty-loading-error-states.md`.
- **Error** — a partial-load error with a retry action.
- **Detail not found** — "This item no longer exists" plus a link back to the list.
- **Optimistic update** — applies immediately and rolls back on failure.

## Interactions

- A row click opens the detail; a modifier-click opens a new tab, because rows are
  real links.
- Inline edit for status or assignee where the profile allows it.
- Filters reflect in the URL (`?status=open`) so a view is shareable.
- Sort persists per list.
- Where the profile is keyboard-first: arrow keys move focus, `Enter` opens the
  focused row, `x` selects it.

## Copy rules

The header title is the plural noun ("Issues", not "Issue"); the count uses a
middle dot ("Issues · 42"). Filtered-empty says "No `<items>` match these filters"
— for example, "No issues match these filters" — with a "Clear filters" action.
The detail title is the item's own name, never "Detail".

## Per-profile differences

`design/profiles/saas-workspace.md` — default to a dense table or board with a
right-panel peek; open a full detail page only through an explicit open action;
inline edits are available directly in the row or the peek panel.

`design/profiles/admin-dashboard.md` — a data table paired with a full detail page
that carries a metadata sidebar; ids in the table and the sidebar render in
monospace; the list offers an export action.

`design/profiles/marketplace.md` — a card grid paired with a full-page detail that
has a sticky action panel; filters open in a modal ("Filters" button with an active
count) instead of inline controls.

## Checklist

- [ ] List header shows title with count, search, filters, and the New action at the right
- [ ] Rows/cards show only the fields needed to decide a click; one density per list
- [ ] Selecting items shows a bulk action bar with count and a clear control
- [ ] Filters and sort are reflected in the URL and survive reload
- [ ] Rows are real links (modifier-click opens a new tab)
- [ ] Loading shows a skeleton matching the row/card shape; total count is visible with pagination or infinite scroll
- [ ] Filtered-empty and first-use-empty are different screens
- [ ] Detail view has header (title, status, primary action, overflow), metadata, body, activity — in that order
