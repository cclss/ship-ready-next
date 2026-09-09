# Design briefs

Read this only when a card touches what users see: page, panel, form, nav,
or state. API-only, migration, infra, and test cards skip `design/`.

## Step 1 — the product profile (once per product)

Read `design/PROFILE.md`.

- **Present:** authoritative — open only the profile it names.
- **Absent:** compare only each profile's *Identity* section against the
  product description, README, and board; then create `design/PROFILE.md`:

  ```
  profile: saas-workspace
  reason: team tool with workspace, members, list objects
  chosen: 2026-09-09
  ```

  Say so in the proof; humans may edit it.

Profiles: `design/profiles/saas-workspace.md` ·
`design/profiles/admin-dashboard.md` ·
`design/profiles/marketplace.md`.

## Step 2 — the screen brief (per card)

Match one row, at most two.

| Card is about… | Read |
|---|---|
| app frame, sidebar, top bar, menu, navigation, layout, routing shell | `design/screens/app-shell-and-navigation.md` |
| list, table, board, index page, detail page, item view, search results | `design/screens/list-and-detail.md` |
| create, edit, new item, form, modal, wizard step with inputs | `design/screens/create-and-edit-forms.md` |
| settings, preferences, account, workspace admin, members, billing | `design/screens/settings-page.md` |
| onboarding, first run, welcome, setup, first-run invites, getting started | `design/screens/onboarding-flow.md` |
| empty state, loading, skeleton, error page, 404, retry, toast | `design/screens/empty-loading-error-states.md` |

Also follow the profile's *Common rules*. Never read other briefs "for
context".

## Proof rule

Every UI proof includes these two lines verbatim, as shown:

```
Design documents read: design/INDEX.md, design/PROFILE.md, design/profiles/<id>.md, design/screens/<name>.md[, design/screens/<name2>.md]
Design checklist:
- [✓] <item copied from the brief>
- [✗] <item> — <one-line reason>
- [n/a] <item> — <why it does not apply>
```

Copy every item read. Put both blocks in the card's **final** report, not only
where you read the briefs.

## Precedence

Profile › screen brief › agent judgement. Existing product code wins; on
conflict, record a `[✗]`.
