# Onboarding flow

## Read this when

The card builds the first-run experience after sign-up or after creating a
workspace: welcome, setup steps, invites, or a getting-started checklist.

## Anatomy

A full-screen flow outside the app shell (no sidebar, no top bar). Logo at
top-left; step progress at top-centre or top-right; "Skip for now" at
top-right where the step allows it.

At most 4 steps, each asking one thing:

1. **Identity** — your name/avatar, or the workspace name.
2. **Context** — role, team size, or intent.
3. **Invite** — teammate emails or a share link.
4. **First object** — create the first project, listing, or data
   connection, pre-filled with an example (a project named "Welcome board").

After the last step, land in the app on that first object. A dismissible
getting-started checklist (3–5 items, with progress) sits inside the shell —
not another modal.

## Required states

| State | What shows |
|---|---|
| Progress | Persists per user; reloading returns to the same step |
| Step validation | Continue stays disabled until the step's required input is valid |
| Invite | Accepts zero, one, or many emails; partial input still advances |
| Waiting for data | Connection steps (admin-dashboard) show a live "waiting for data" state that updates without a reload once an event arrives |
| Checklist complete | Auto-dismisses once every item is done |

## Interactions

Back is available on every step after the first; Continue is the primary
button, right-aligned. `Enter` advances the current step. Skipping a step
never blocks later use — the getting-started checklist offers the skipped
action again. The first object from step 4 is real, not a placeholder: it
is visible in lists immediately. Returning users never see the flow again;
the flag is per user, not per device.

## Copy rules

One sentence of purpose per step, second person, no marketing language. Step
titles are questions or imperatives — "Name your workspace," "Who's on your
team?" Buttons read "Continue," "Skip for now," and "Finish" on the last
step. No exclamation marks.

## Per-profile differences

`design/profiles/saas-workspace.md` — workspace name, then invite members,
then create the first object; the invite step is skippable.

`design/profiles/admin-dashboard.md` — organisation/project, then connect
data via an API key or an install snippet with a copy control, then verify
the first event, shown as a live "waiting for data" state until one lands.

`design/profiles/marketplace.md` — role choice (browse vs. supply), then
location/interests, then a first save or a first listing draft; browsers can
skip every remaining step.

## Checklist

- [ ] At most 4 steps, each asking one thing, with visible step progress
- [ ] The flow is full-screen without the app shell and has Back on every step after the first
- [ ] Progress persists across reload and the flow never shows again once finished
- [ ] Every non-essential step has "Skip for now"; skipped items reappear in the getting-started checklist
- [ ] The last step creates a real first object and lands the user on it
- [ ] A dismissible 3–5 item getting-started checklist appears in the shell after the flow
- [ ] Buttons are Continue / Skip for now / Finish; step titles are questions or imperatives
- [ ] Profile-specific step set is followed (workspace→invite→object; org→connect→verify; role→interests→first action)
- [ ] Continue is right-aligned and disabled until the step is valid; Enter advances; the invite step accepts partial input
- [ ] The never-show-again flag is per user (a second device skips the flow); the getting-started checklist auto-dismisses when complete
