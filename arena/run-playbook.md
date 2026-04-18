# Arena Run Playbook (MVP)

> Copy-paste workflow to execute one trial end-to-end. Treat each
> numbered step as a discrete command or subagent dispatch. Commit
> after every step that produces an artifact.

## Prerequisites per trial

- A pending lesson ID (e.g. `L09`).
- A trial ID of the form `<date>-<lessonID>-<scenarioID>`, e.g.
  `2026-04-20-L09-S01`.
- A fresh trial folder: `arena/trial-records/<trialID>/`.

## The 8 steps

### Step 1 — Create trial folder

```
cd ~/.claude/skills/image-craft-lv
mkdir -p arena/trial-records/<trialID>
```

### Step 2 — Dispatch Generator subagent

Use `arena/prompts/generator-prompt.md` as the prompt. Inputs to include
in the dispatch:
- Lesson body: the full `lessons/<theme>/L##-*.md` file.
- DHYANA baseline: section "DHYANA fingerprint" from `arena/axes.md`.
- Scenario-bank index: the entirety of `arena/scenario-bank/README.md`.
- Axes rules: `arena/axes.md`.
- Criteria template: `arena/criteria/L##-criteria.md`.

Expected outputs (saved into trial folder):
- `scenario.md` with "Axis fingerprint" section.
- `criteria.md` — pre-registered pass criteria, concrete.

Commit immediately:
```
git add arena/trial-records/<trialID>/
git commit -m "Arena <trialID>: generator output (scenario + criteria)"
```

### Step 3 — Human checkpoint (REQUIRED)

Open the scenario and criteria. Ask yourself:
- Does it actually test the claim of L##?
- Does the axis fingerprint pass the ≥3-flip rule?
- Are the criteria measurable with the tools on hand?

If yes: proceed to Step 4. If no: re-dispatch Generator with your
feedback (max 3 reworks), or abort.

### Step 4 — Dispatch Runner subagent (blinded)

Use `arena/prompts/runner-prompt.md`. Inputs:
- `scenario.md` (ONLY). Do NOT pass the lesson body.
- Instruction to invoke `image-craft-lv` normally.
- Budget cap: $2 hard. Target 10–15 images.

Expected outputs in trial folder:
- `runner-log.md` — prompts used + Post-generate Self-review notes.
- `images/` — filenames or URLs of generated images (keep actual bytes
  or references depending on kie-nano-banana output).

Commit:
```
git add arena/trial-records/<trialID>/
git commit -m "Arena <trialID>: runner output (images + log)"
```

### Step 5 — Dispatch Judge subagent

Use `arena/prompts/judge-prompt.md`. Inputs:
- `criteria.md` (LOCKED — Judge cannot edit).
- `runner-log.md` + images.

Expected output:
- `judgment.md` with per-criterion verdict + overall
  `pass | partial | fail | criteria-broken`.

Commit:
```
git add arena/trial-records/<trialID>/judgment.md
git commit -m "Arena <trialID>: judgment"
```

### Step 6 — Dispatch Skeptic subagent

Use `arena/prompts/skeptic-prompt.md`. Inputs:
- Full trial record so far.

Expected output:
- `skeptic.md` with verdict: `adversarial-valid` |
  `void-too-easy` | `void-criteria-weak` | `void-lesson-unnecessary`.

Commit:
```
git add arena/trial-records/<trialID>/skeptic.md
git commit -m "Arena <trialID>: skeptic verdict"
```

### Step 7 — Update ledger OR void

If `skeptic.md` says `adversarial-valid` AND `judgment.md` says
`pass` or `partial`:

1. Append a row to `VALIDATION_LEDGER.md`:
   - Project = `arena:SXX` (new scenario ID from scenario-bank)
   - Reviewer = `AI-jury`
   - Notes = axis fingerprint summary
2. Mirror into the lesson's own Validation log table.
3. Increment the lesson's `validation:` counter in frontmatter.
4. Append to `arena/scenario-bank/README.md` with fingerprint.

Otherwise (any void or fail):
1. Append to `arena/void-log.md` with trial ID, verdict, reason.
2. If the SAME lesson has voided 3 times consecutively, add
   `flags: [arena-unresolvable]` to its frontmatter — surface
   to user for rewrite/retire decision.

Commit:
```
git add VALIDATION_LEDGER.md arena/ lessons/
git commit -m "Arena <trialID>: ledger update [pass|void]"
```

### Step 8 — Archive + review artifact

Generate an HTML summary of the trial at
`arena/trial-records/<trialID>/summary.html` — following L07
(reviewable-artifact). It should embed (or reference) images side by
side with criteria, judgment, and skeptic output.

Open it:
```
open arena/trial-records/<trialID>/summary.html
```

Commit:
```
git add arena/trial-records/<trialID>/summary.html
git commit -m "Arena <trialID>: review artifact"
```

Push all arena work at session end:
```
git push origin main
```

## Cost ledger per trial

- Generator + Judge + Skeptic: ~$0.15 total (Claude subagent runs).
- Runner: 10–15 Nano Banana calls × $0.04 ≈ $0.4–0.6.
- **Per-trial budget: ~$0.7. Hard cap $2.**

## When to promote the lesson

After Step 7, inspect the lesson's frontmatter:
- Meso (`validation: X/3`) with ≥2 passes across ≥2 axis-distinct
  projects → promote `status: validated`.
- Macro (`validation: X/5`) with ≥3 passes across ≥3 axis-distinct
  projects → promote `status: validated`.

Promotion steps:
1. Flip `status:` in lesson frontmatter to `validated`.
2. Update `lessons/README.md` status badge.
3. Update `SKILL.md` lessons-library table row.
4. Append CHANGELOG entry (LV bump).
5. Git tag the promotion (e.g. `lv2.3-L09-validated`).
6. Push.
