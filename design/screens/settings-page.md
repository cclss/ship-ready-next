# Settings page

## Read this when

The card builds or changes preferences, account, profile, workspace/organisation
administration, members, billing, integrations, notification settings, or API keys.

## Anatomy

1. **Entry point** — per profile: an avatar-menu item or a sidebar item; see
   Per-profile differences.
2. **Two scopes, visibly separated** — Personal (Profile, Preferences,
   Notifications, Security) and Workspace/Organisation (General, Members,
   Billing, Integrations, API, Danger zone), never interleaved.
3. **Section navigation** — left sub-nav at 4 or more sections, tabs at 2–3,
   stacked cards at 1; profiles override (see below).
4. **Section body** — a titled card with a one-line description and grouped
   fields; its own Save, or autosave with an inline "Saved" for toggles.
5. **Danger zone** — always the last section, visually separated with a
   `--color-danger` border.

## Required states

| State | What shows |
|---|---|
| Loading | A skeleton per card |
| Unsaved changes | The card's Save enables only once a field in it is dirty |
| Saved | Inline "Saved" beside the field, or a toast |
| Permission-limited | Read-only fields with "Only owners can change this" beside them |
| Members empty | Empty member list with Invite as the primary action |

## Interactions

Toggles apply immediately and offer Undo in the confirming toast. Text fields
save only when the card's Save is pressed. Leaving a dirty card (route change
or close) asks for confirmation. An API key shows once, at creation, with a
copy control; later views show it masked. Demoting your own role asks for
confirmation before it applies. Changing the billing plan confirms with the
new price and effective date.

## Copy rules

Section titles are nouns — "Members," not "Manage members." Each
description states what the setting affects, in one line, below the title.
Danger-zone actions state the consequence before the confirmation step, for
example "Deleting this workspace removes all projects for every member."

## Per-profile differences

`design/profiles/saas-workspace.md` — Settings opens only from the avatar menu
at the sidebar bottom; Personal and Workspace are two labelled groups in the
sub-nav.

`design/profiles/admin-dashboard.md` — Settings is the last sidebar item, always
with a left sub-nav; the top bar's organisation/project switcher and environment
toggle still apply. The Danger zone requires typing the resource's name.

`design/profiles/marketplace.md` — an "Account" page from the avatar menu;
stacked cards up to 6 sections, a left sub-nav beyond that. Payouts and listings
form a separate "Seller" group.

## Checklist

- [ ] Settings entry point matches the profile (avatar menu or sidebar item) and lands on the first section; an empty Members list shows Invite as the primary action
- [ ] Personal and workspace/organisation scopes are visibly separated
- [ ] Section navigation follows the profile: left sub-nav (≥ 4 sections, or admin-dashboard always), tabs (2–3), stacked cards (1, or marketplace ≤ 6)
- [ ] Each section is a titled card with a description and its own Save; toggles instead apply immediately with Undo in the toast
- [ ] Save is disabled until the card is dirty; leaving a dirty card asks for confirmation
- [ ] Read-only settings explain who can change them
- [ ] Secrets/API keys show once with a copy control, then are masked
- [ ] Danger zone is the last section, danger-bordered, states each action's consequence, and (admin-dashboard) requires typing the resource name
- [ ] Demoting your own role and changing the billing plan confirm before applying; billing states the new price and effective date
