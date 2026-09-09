# List and detail

## Read this when

The card shows a collection (table, board, grid, feed, search results) and/or a
single item's page or panel.

## Anatomy

**List header** — title with a count ("Issues · 42"), search input, filter
controls, a view switcher (only with more than one view), sort, and
the primary "New" action at the right.

**List body** — rows or cards showing only the fields that decide a click (title,
status, owner, updated); one visual density per list; selection checkboxes appear
on hover or once selected.

**Bulk action bar** — replaces the header when items are selected: count,
actions, clear.

**Detail** — a page, or a right-panel peek / drawer per the profile. Header (title, status,
primary action, overflow menu), metadata block (owner, dates, ids), body, then
activity or comments last.

**Pagination or infinite scroll** with a visible total.

## Required states

- **Loading** — a skeleton matching the row or card height.
- **Empty** — first-use empty and filtered-empty are different screens; see
  `design/screens/empty-loading-error-states.md`.
- **Error** — a partial-load error with a retry action.
- **Detail not found** — "This item no longer exists" plus a link back to the list.
- **Optimistic update** — applies immediately and rolls back on failure.

## Interactions

- Rows are real links: click opens the detail, modifier-click opens a new tab.
- Inline edit for status or assignee where the profile allows.
- Filters reflect in the URL (`?status=open`); views are shareable.
- Sort persists per list: returning without a sort param shows the last-chosen
  order.
- Where the profile is keyboard-first: `j`/`k` or arrow keys move focus, `Enter`
  opens the focused row, `x` selects it.

## Copy rules

Header title is the plural noun with a middle-dot count ("Issues · 42").
Filtered-empty says "No issues match these filters" with a "Clear filters" action.
The detail title is the item's own name, never "Detail".

## Per-profile differences

`design/profiles/saas-workspace.md` — dense table or board with a right-panel peek; a
full detail page only via an explicit open action; inline edits in the row or the
peek.

`design/profiles/admin-dashboard.md` — a data table; small records open in a
right-side drawer, large records on a full detail page with a metadata sidebar;
ids in the table and the sidebar render in monospace; the list offers an export
action.

`design/profiles/marketplace.md` — a card grid paired with a full-page detail that
has a sticky action panel; filters open in a modal ("Filters" button with an active
count) instead of inline controls, at every viewport size.

## Checklist

- [ ] List header shows title with count, search, filters, and the New action at the right
- [ ] Rows/cards show only fields that decide a click (title, status, owner, updated); one density per list
- [ ] Selecting items shows a bulk action bar with count and a clear control
- [ ] Filters and sort are reflected in the URL and survive reload
- [ ] Rows are real links (modifier-click opens a new tab)
- [ ] Loading shows a skeleton matching the row/card shape; total count is visible with pagination or infinite scroll
- [ ] Filtered-empty and first-use-empty are different screens
- [ ] Load errors offer Retry; a missing item shows "This item no longer exists" with a link back; optimistic edits roll back visibly on failure
- [ ] Title is the plural noun with a middle-dot count; filtered-empty offers Clear filters; the detail title is never "Detail"
- [ ] Detail view has header (title, status, primary action, overflow), metadata, body, activity — in that order
