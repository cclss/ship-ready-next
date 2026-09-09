# Create and edit forms

## Read this when

The card adds or changes a form: create/edit dialogs, multi-step creation, wizard
steps with inputs.

## Anatomy

**Container.** A harmless creation — no credential, no charge, no message sent —
fits a modal at 5 fields or fewer. More fields, a file upload, a credential, or
money means a full page. Profile caps differ: admin-dashboard modals stop at 3;
saas-workspace keeps 1–2-field creation inline.

**Layout.** Single column; modals 560 px, pages up to 640 px. Label above each
field, helper text below, required marker on the label. A small heading every
4–6 fields.

**Footer.** Cancel (secondary) left of the primary button; primary at the right,
sticky on pages. Primary label is verb plus object: "Create project."

**Multi-step.** Progress ("Step 2 of 4", named steps), Back/Next, review step last.

## Required states

| State | What shows |
|---|---|
| Pristine | Defaults shown; primary enabled |
| Dirty | Unsaved-changes guard on close or navigate |
| Submitting | Primary button disabled with spinner; fields locked |
| Field error | Inline message under the field, outline `--color-danger`, focus to first error |
| Form-level error | Banner above the footer with retry |
| Success | Dialog closes (or the page redirects) and a toast names the object, with an "Open" link |

## Interactions

Validate on blur; re-validate on change once a field has shown an error; never
before the user leaves the field. `⌘/Ctrl+Enter` submits; `Esc` cancels after
the dirty guard. Autofocus the first field. Selects with more than 7 options get
a search box. Dates: picker with typed fallback. File inputs show name, size,
and a remove control.

## Copy rules

Title: "New project" / "Edit project". Primary button: "Create project" /
"Save changes". Errors say what to do — "Enter a name shorter than 80
characters" — never "Invalid input." No exclamation marks.

## Per-profile differences

`design/profiles/saas-workspace.md` — 3 or more fields use a modal, title first,
`⌘/Ctrl+Enter` submits; 1–2 fields (a new label) stay inline or in a popover.

`design/profiles/admin-dashboard.md` — a credential, a charge, or another side
effect means a full page whatever the field count; a modal only for 3 or fewer
fields with none of those. Edit pages carry a Danger zone for delete, apart from
Save.

`design/profiles/marketplace.md` — listing creation is a multi-step full-page
flow: photos, details, pricing, with a persistent progress bar.

## Checklist

- [ ] Modal only within the profile's cap (5 harmless fields; admin-dashboard 3; saas-workspace 1–2 inline), else full page; single column, labels above fields
- [ ] Footer has Cancel then the primary button at the right; primary label is verb + object
- [ ] Validation runs on blur, errors show inline under the field, and focus moves to the first error on submit
- [ ] Submitting disables the primary button and locks fields; separately, a form-level error shows a banner above the footer with retry
- [ ] Leaving a dirty form asks for confirmation
- [ ] Success closes or redirects and shows a toast naming the object
- [ ] ⌘/Ctrl+Enter submits and Esc cancels; the first field is focused on open
- [ ] Deleting (edit pages) follows the profile's destructive rule — admin-dashboard: Danger zone; others: overflow menu or confirm modal — never next to Save
- [ ] Selects with > 7 options are searchable; dates have a typed-input fallback; file inputs show name, size, and remove; no exclamation marks in copy
- [ ] Multi-step forms show step progress, Back/Next, and a review step last
