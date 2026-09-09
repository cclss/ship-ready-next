# Empty, loading, and error states

## Read this when

The card adds or changes what users see when there is nothing, when data is
arriving, or when something failed: empty lists, skeletons, error pages,
toasts, retry.

## Anatomy

**Empty — first-use.** Centred block: an icon (24–48 px), a title naming the
object ("No projects yet"), one line on what it is for, one primary action
("New project"), an optional secondary link (docs, import, sample data).

**Empty — filtered (or search).** Compact inline message ("No issues match these
filters") with a "Clear filters" action; never the first-use icon.

**Empty — permission.** Says who can add items; no primary action.

**Loading.** Skeletons matching the final layout (row height, card shape,
KPI tile), shown immediately for lists; a spinner only past 300 ms
of waiting; never a full-page spinner after the shell has rendered.

**Error — field.** Inline under the field, per
`design/screens/create-and-edit-forms.md`.

**Error — region.** Replaces the region with a title, a one-line cause, a
Retry button, and a request id when available.

**Error — transient.** A toast (bottom-left or bottom-centre), auto-dismiss
in 5 s, with Undo or Retry when meaningful.

**404 / 403.** Inside the shell: title, one line, a link back to the nearest
list.

## Required states

Every list has both empty variants (first-use and filtered). Every async
region has a skeleton. Every mutation has a failure toast. A missing or
forbidden object renders the 404/403 page inside the shell.

## Interactions

Retry re-runs only the failed request. Toasts stack at most 3 and are
individually dismissible. Skeleton animation runs no faster than one cycle per
1.5 s. The empty-state CTA opens the header's New action: same modal, same
defaults.

## Copy rules

Titles are short and factual ("No results", "Couldn't load payments"). The
body line says the next action, not the cause. No blame ("You entered…") and
no jargon: no HTTP codes in titles (`404`, `500` stay out of headlines); ids
go in a muted line below the message.

## Per-profile differences

`design/profiles/saas-workspace.md` — the empty-state CTA names the object
("New task", not "Create") and pairs it with a keyboard hint ("Press C to
create").

`design/profiles/admin-dashboard.md` — empty tables explain how data arrives
(an install snippet, a connect step) instead of offering a Create button;
skeletons cover both KPI tiles and table rows; region errors show a request
id.

`design/profiles/marketplace.md` — empty search results show "Clear filters"
first, then nearby or related suggestions; wishlist and orders empty states
link back to Explore instead of offering a creation action.

## Checklist

- [ ] First-use-empty state has icon, object-named title, one-line purpose, and one primary action
- [ ] Filtered-empty state is compact and offers Clear filters; it never reuses the first-use icon
- [ ] Loading uses skeletons that match the final layout; no full-page spinner after the shell renders
- [ ] Region errors show title, cause, Retry, and a request id when available; Retry re-runs only that request
- [ ] Transient errors use toasts that auto-dismiss in 5 s, stack ≤ 3, and offer Undo/Retry when meaningful
- [ ] 404 and 403 render inside the shell with a link back to the nearest list
- [ ] Empty-state CTA opens the header's New action (see Per-profile differences for exceptions)
- [ ] Copy has no HTTP codes in titles, no blame, and names the next action
- [ ] Permission empty state says who can add items and shows no primary action
- [ ] Every mutation has a failure toast; skeleton animation cycles no faster than every 1.5 s
