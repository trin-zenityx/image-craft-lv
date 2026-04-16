# Session Kickoff — image-craft-lv

> Claude: run these 5 steps before touching the first prompt of a still-image session.

## Step 1 — Identify project context

Ask (or infer) and note:
- Project name. Is it already in `VALIDATION_LEDGER.md`?
- Approximate shot count. Single gen or batch?
- Reused characters / locations / props — which ones?
- Target model (Nano Banana Pro, Nano Banana 2, Midjourney, Flux, etc.)?

## Step 2 — Retrieve relevant lesson themes

Load only the lesson subsets that match the task:

| Task signal | Load these themes |
|-------------|-------------------|
| Multi-shot character or location | `lessons/consistency/` + `lessons/character/` |
| Using reference images | `lessons/references/` |
| Batch ≥3 shots, final delivery | `lessons/delivery/` |
| First-time gen / baseline | `lessons/workflow/` |
| Known hard-to-render element | `lessons/model-limits/` |
| Face/body through container/window | `lessons/orientation/` |

Always load: `workflow/L04-self-review-protocol.md`.

## Step 3 — Warn about pending lessons in play

For every lesson loaded in Step 2 with `status: pending`:
- Tell the user: "This session will exercise L## (status pending X/Y). Outcome will be logged."
- Record the intent in the session so outcomes get back to the ledger.

## Step 4 — Convert Pre-submit Checklist into TodoWrite

Open `SKILL.md`. For every checklist item under "PRE-SUBMIT CHECKLIST" (sections A/B/C/D), create one TodoWrite entry. Mark each as `pending` at start.

## Step 5 — Confirm Batch Gate

If the session will batch more than 3 shots:
- Report cost estimate.
- Insist on a single test gen first, reviewed and approved, before batching.
- If user overrides, note the override explicitly in the validation log entry.
