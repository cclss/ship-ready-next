# Settings page

## Read this when

The card builds preferences, account, profile, workspace/organisation
administration, members, billing, integrations, notifications, or API keys.

## Anatomy

1. **Entry point** — per profile: an account-menu item or a sidebar item; see
   Per-profile differences.
2. **Two scopes, visibly separated** — Personal (Profile, Preferences,
   Notifications, Security) and Workspace/Organisation (General, Members,
   Billing, Integrations, API, Danger zone). A heading or grouped block marks
   each scope without interleaving sections.
3. **Section navigation** — a left sub-nav at 4 or more sections, tabs at 2–3,
   stacked cards on one page at exactly 1 section.
4. **Section body** — each section is a titled card with a one-line
   description; related fields group inside it. Each card has its own Save,
   or autosaves with an inline "Saved" confirmation for toggles.
5. **Danger zone** — always the last section, visually separated with a
   `--color-danger` border.

## Required states

| State | What shows |
|---|---|
| Loading | A skeleton per card, matching that card's field count |
| Unsaved changes | The card's Save is enabled only once a field in that card is dirty |
| Saved | Inline "Saved" text next to the field, or a toast, on success |
| Permission-limited | Fields render read-only with "Only owners can change this" beside them |
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
example "Deleting the workspace removes all projects for every member."

## Per-profile differences

`design/profiles/saas-workspace.md` — Settings opens only from the avatar
menu at the sidebar bottom, never from primary navigation. Personal and
Workspace sit as two labelled groups inside the settings sub-nav.

`design/profiles/admin-dashboard.md` — Settings is the last item in the main
sidebar, not an avatar-menu entry. The organisation/project switcher and
environment toggle from the top bar still apply while settings is open. The
Danger zone requires typing the resource's name to confirm each action.

`design/profiles/marketplace.md` — reached as an "Account" page from the
avatar menu. Sections render as stacked cards unless there are more than 6
of them, at which point a left sub-nav replaces the stack. Payouts and
listings render as a separate "Seller" group, not mixed into
Workspace/Organisation.

## Checklist

- [ ] Settings entry point matches the profile (avatar menu or sidebar item) and lands on the first section
- [ ] Personal and workspace/organisation scopes are visibly separated
- [ ] Section navigation is a left sub-nav (≥ 4 sections), tabs (2–3), or stacked cards (1)
- [ ] Each section is a titled card with a description and its own Save, or immediate-apply toggles with confirmation
- [ ] Save is disabled until the card is dirty; leaving a dirty card asks for confirmation
- [ ] Read-only settings explain who can change them
- [ ] Secrets/API keys show once with a copy control, then are masked
- [ ] Danger zone is the last section, danger-bordered, and each action states its consequences before confirming
