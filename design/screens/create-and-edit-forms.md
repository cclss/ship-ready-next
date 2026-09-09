# Create and edit forms

## Read this when

The card adds or changes a form: create/edit dialogs, multi-step creation, or an
input-heavy wizard step.

## Anatomy

**Container.** A harmless creation — no side effect beyond creating or editing the
object: no credential, no charge, no message sent — fits a modal at 5 fields or
fewer. More fields, a file upload, a credential, or money means a full page.

**Layout.** Single column. Modals: 560 px wide. Pages: up to 640 px wide. Label
above each field, helper text below, required marker on the label. Group fields
under a small heading every 4–6 fields.

**Footer.** Cancel (secondary) left of the primary action; primary at the right,
sticky on pages. Primary label is verb plus object, for example "Create project."

**Multi-step.** Progress indicator ("Step 2 of 4", named steps), Back/Next, review
step last.

## Required states

| State | What shows |
|---|---|
| Pristine | Empty or default values; primary action enabled |
| Dirty | Unsaved-changes guard fires on close or navigate |
| Submitting | Primary action disabled with a spinner; fields locked |
| Field error | Inline message under the field; field outline in `--color-danger`; focus moves to the first error |
| Form-level error | Banner above the footer with a retry action |
| Success | Dialog closes (or the page redirects) and a toast names the object, with an "Open" link |

## Interactions

Validate a field on blur; re-validate on every change once that field has shown an
error. Never validate before the user first leaves the field. `⌘/Ctrl+Enter`
submits; `Esc` cancels, running the dirty-form guard first. Autofocus the first
field on open. Selects with more than 7 options get a search box. Dates use a
picker with a typed-input fallback. File inputs show name, size, and a remove
control.

## Copy rules

Title follows "New `<object>`" / "Edit `<object>`", for example "New project" and
"Edit project." Primary button: "Create `<object>`" on create, "Save changes" on
edit. Error messages say what to do — "Enter a name shorter than 80 characters" —
never "Invalid input." No exclamation marks in form copy.

## Per-profile differences

`design/profiles/saas-workspace.md` — creation with 3 or more fields uses a 560 px
modal, title field first, `⌘/Ctrl+Enter` to submit; 1–2 fields (a new label, a new
team) stay inline or in a small popover instead.

`design/profiles/admin-dashboard.md` — anything creating a credential, a charge, or
another side effect uses a full page regardless of field count; a modal is only for
3 or fewer fields with none of those effects. Edit pages carry a Danger zone for
delete, separate from Save.

`design/profiles/marketplace.md` — listing creation is a multi-step full-page flow:
photos, then details, then pricing, with a persistent progress bar throughout.

## Checklist

- [ ] Modal for ≤ 5 harmless fields, full page otherwise; single column with labels above fields
- [ ] Footer has Cancel then the primary button at the right; primary label is verb + object
- [ ] Validation runs on blur, errors show inline under the field, and focus moves to the first error on submit
- [ ] Submitting disables the primary button and locks fields; a form-level error shows a banner with retry
- [ ] Leaving a dirty form asks for confirmation
- [ ] Success closes or redirects and shows a toast naming the object
- [ ] ⌘/Ctrl+Enter submits and Esc cancels; the first field is focused on open
- [ ] Deleting the object (edit pages) sits in a Danger zone with confirmation, not next to Save
