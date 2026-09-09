# Design briefs

Read this only when a card touches something a user sees: page, panel, form,
nav, or state (empty/loading/error). API-only, migration, infra, and test
cards skip `design/`.

## Step 1 — the product profile

Read `design/PROFILE.md`.

- **Present:** authoritative. Read only the profile it names.
- **Absent:** pick the profile whose *Identity* matches the product, then
  create `design/PROFILE.md`:

  ```
  profile: saas-workspace
  reason: internal tool with a workspace, members, and list objects
  chosen: 2026-09-09 by <agent/run id>
  ```

  Say so in the proof; humans may override.

Profiles: `design/profiles/saas-workspace.md` (team tools, trackers) ·
`design/profiles/admin-dashboard.md` (consoles, dashboards) ·
`design/profiles/marketplace.md` (listings, catalogs, directories).

## Step 2 — the screen brief

Match one row, two at most.

| Card is about… | Read |
|---|---|
| app frame, sidebar, top bar, menu, navigation, layout, routing shell | `design/screens/app-shell-and-navigation.md` |
| list, table, board, index page, detail page, item view, search results | `design/screens/list-and-detail.md` |
| create, edit, new item, form, modal, wizard step with inputs | `design/screens/create-and-edit-forms.md` |
| settings, preferences, account, profile, workspace admin, members, billing | `design/screens/settings-page.md` |
| onboarding, first run, welcome, setup, invite flow, getting started | `design/screens/onboarding-flow.md` |
| empty state, loading, skeleton, error page, 404, retry, toast | `design/screens/empty-loading-error-states.md` |

Also follow the profile's *Common rules*. Budget: one profile, one or two
screens.

## Proof rule

Every proof includes both blocks, verbatim headings:

```
Design documents read: design/INDEX.md, design/PROFILE.md, design/profiles/<id>.md, design/screens/<name>.md
Design checklist:
- [✓] <item copied from the brief>
- [✗] <item> — <one-line reason>
- [n/a] <item> — <why it does not apply>
```

Copy each checklist item from the documents read; missing blocks make the
proof incomplete.

## Precedence

`PROFILE.md` › profile › screen brief › your judgement. Existing product code
wins over all; on conflict, stay consistent and record it as a `[✗]`.
