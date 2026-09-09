# Design briefs

Read this only when a card touches what users see: page, panel, form, nav,
or state (empty/loading/error). API, migration, infra, and test cards
skip `design/`.

## Step 1 — the product profile (once per product)

Read `design/PROFILE.md`.

- **Present:** authoritative; read only that profile.
- **Absent:** pick the profile whose *Identity* fits the product
  description, README, and board; then create `design/PROFILE.md`:

  ```
  profile: saas-workspace
  reason: team tool with workspace, members, list objects
  chosen: 2026-09-09 <run id>
  ```

  Say so in the proof; humans may edit it.

Profiles: `design/profiles/saas-workspace.md` (team tools) ·
`design/profiles/admin-dashboard.md` (consoles) ·
`design/profiles/marketplace.md` (listings).

## Step 2 — the screen brief (per card)

Match one row, at most two.

| Card is about… | Read |
|---|---|
| app frame, sidebar, top bar, menu, navigation, layout, routing shell | `design/screens/app-shell-and-navigation.md` |
| list, table, board, index page, detail page, item view, search results | `design/screens/list-and-detail.md` |
| create, edit, new item, form, modal, wizard step with inputs | `design/screens/create-and-edit-forms.md` |
| settings, preferences, account, profile, workspace admin, members, billing | `design/screens/settings-page.md` |
| onboarding, first run, welcome, setup, invite flow, getting started | `design/screens/onboarding-flow.md` |
| empty state, loading, skeleton, error page, 404, retry, toast | `design/screens/empty-loading-error-states.md` |

Also follow the profile's *Common rules*. Never read other briefs "for
context": one profile, one or two screens.

## Proof rule

Every UI proof includes, with verbatim headings:

```
Design documents read: design/INDEX.md, design/PROFILE.md, design/profiles/<id>.md, design/screens/<name>.md
Design checklist:
- [✓] <item copied from the brief>
- [✗] <item> — <one-line reason>
- [n/a] <item> — <why it does not apply>
```

Copy every checklist item you read; without both blocks the proof is
incomplete.

## Precedence

`PROFILE.md` › profile › screen brief › judgement. Existing product code
wins; on conflict, record a `[✗]` and stay consistent.
