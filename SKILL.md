---
name: image-craft-lv
description: >-
  Self-improving discipline layer for STILL-IMAGE prompt engineering
  (Nano Banana, Midjourney, DALL·E, Stable Diffusion, Flux). Enforces
  a Pre-submit Checklist, Batch Gate, and Post-generate Self-review
  before/after any still-image generation. Maintains a lessons library
  that levels up with validated outcomes. Auto-invoke whenever about
  to write/submit/refine a still-image prompt, plan a multi-shot image
  project, or debug drift between related images. DO NOT use for video
  (see seedance-craft-lv) or raw API calls (see kie-nano-banana).
level: 2
updated: 2026-04-16
sister_skills: [seedance-craft-lv, kie-nano-banana]
---

# image-craft-lv

> A living skill. Every generation teaches something; validated lessons level this skill up. Future-you reads this before writing any still-image prompt.

## Current Level: **LV 2** (redesign LV 2.1)

Full history: [CHANGELOG.md](CHANGELOG.md)

## THE RULE (non-negotiable)

**Before submitting ANY still-image prompt, run the Batch Gate, then the Pre-submit Checklist. Before showing generated output to the user, run the Post-generate Self-review. No exceptions. Skipping = LV regression.**

## ENTRY PROTOCOL (Claude reads first)

Run `templates/session-kickoff.md` at the start of any session that will touch still-image generation. In short:

1. Identify project context (name, shot count, reused assets, model).
2. Retrieve relevant lesson themes from `lessons/` per the cheatsheet in `lessons/README.md`.
3. Warn about any `pending` lessons that will be exercised.
4. Convert the Pre-submit Checklist into TodoWrite items.
5. Confirm the Batch Gate before any multi-shot submission.

## BATCH DISCIPLINE GATE

Still-image gens are cheaper than video but batching 20 shots with a systemic error is still painful.

- **First gen in this project/session?** Render a single test first. Never batch without a baseline.
- **First time using a technique (new ref strategy, new model, new prompt structure)?** Test 1–3 gens before batching.
- **Batch >3 shots?** Report a cost estimate to the user before submitting.
- **User approved batching after seeing tests?** If not, stop. Ask.

Anti-pattern: submitting 20 gens before confirming the first 1–3 work.

## PRE-SUBMIT CHECKLIST

Convert every item below into a TodoWrite entry at session start. Tick each before submitting.

### A. Consistency audit
- [ ] Recurring character? Ref image attached, or master anchor generated first?
- [ ] Recurring location? Same.
- [ ] Recurring prop/motif? Same.
- [ ] Design-language match? Opaque stays opaque; red stays red; never let the model re-decide established visual facts.

### B. Ambiguity sweep
- [ ] Orientation of hidden/partial subjects (face inside a window/container/mirror, body relative to camera) stated explicitly.
- [ ] Dimensions stated as numbers, not adjectives ("2.1 m pod", not "long pod").
- [ ] Camera angle and lens named ("telephoto 85 mm low-angle 3/4 view", not "a shot of X").
- [ ] Negative prompts for common drift ("no text, no watermark, no age markers, …").
- [ ] Distinguishability of characters in similar contexts — immutable features stated for each (gender, ethnicity, hair, facial structure).

### C. Reference strategy
- [ ] Refs chosen are the MOST relevant to what this shot must lock (not just "related").
- [ ] Under the model's ref limit (Nano Banana Pro: 8; Nano Banana 2: 14; Seedance Omni: 9).
- [ ] Chain order correct: master anchors first, secondary with master refs, tertiary with both.

### D. Phase planning (multi-shot projects)
- [ ] Dependency graph drawn.
- [ ] Phases arranged: parallel within phase, sequential between phases.

## POST-GENERATE SELF-REVIEW

Run every image through these seven checks before showing the user.

1. **Anatomical plausibility.** Pod proportions, body in pose, scale of figure vs environment. Quantify ratios; do not eyeball.
2. **Orientation.** Does the face point where you intended? Hand pose match ref?
3. **Design-language drift.** Does the opaque-body pod in shot A still look opaque in shot B? Did the robe color change?
4. **Within-image internal consistency.** Light direction matches shadows. Rim light from the window side.
5. **Intent fulfillment.** Re-read your own prompt's key phrases. Does the image show those exact phrases, or a generic version?
6. **Proportion comparison against ORIGINAL refs, not crops.** (L04 + L09 reinforcement.) Cropping a target enlarges it in your field of view and tricks you into thinking proportions are fine. Always compare at equal zoom.
7. **Full-frame scan after every regen.** (L04 reinforcement.) When regen fixes issue A, do not only verify A. Scan the entire frame against the ref for unrelated drifts — environment, background, lighting direction, color temperature, depth cues. List every environmental element of the ref and confirm each is preserved before shipping.

**If anything fails: regenerate with a fix, do not ship broken and hope.**

## CORE PRINCIPLES

These do not change between LVs. They are the spine.

1. **Mismatch between shots beats beauty per shot.** Two adequate matched shots > a perfect #1 and a perfect #2 that don't match.
2. **Ambiguity = model's choice, not yours.** Every unstated detail is a coin-flip. State everything that matters; accept the rest as generative surprise.
3. **Reference images are not optional polish — they are foundational.** For any multi-shot project, ref chains are designed BEFORE the first generation.
4. **Numbers > adjectives.** "2.1 meter" not "long". "85 mm" not "telephoto". "40 rack columns" not "many racks".
5. **Negative-state the common failures.** "No age markers, no text, no watermark, no [specific failure you have seen]".
6. **Self-review is not optional.** It is the last step of generation.

## LEVELING PROTOCOL (summary)

- **Status** per lesson: `pending (X/Y)` → `validated` → `retired`.
- **Tier thresholds:** Micro 1/1 · Meso 2/3 · Macro 3/5.
- **Project spread (LV 2.1):** Meso requires passes across ≥2 projects; Macro requires ≥3.
- **Promotion:** flips status, bumps LV, adds CHANGELOG entry, commits.
- **Full protocol + rollback procedure:** [CHANGELOG.md](CHANGELOG.md#leveling-protocol).
- **Validation log of record:** [VALIDATION_LEDGER.md](VALIDATION_LEDGER.md).

## LESSONS LIBRARY

Themed index: [lessons/README.md](lessons/README.md). One lesson per file.

| ID  | Theme         | Status                 | Headline                                                         |
|-----|---------------|------------------------|------------------------------------------------------------------|
| L01 | consistency   | pending 1/5 · macro    | Reference chains beat text-only for multi-shot sets              |
| L02 | orientation   | pending 1/3 · meso     | Face orientation inside containers must be explicit              |
| L03 | consistency   | pending 1/3 · meso     | Opaque vs transparent surface vocabulary must match across set   |
| L04 | workflow      | pending 0/5 · macro    | Self-review before showing output                                |
| L05 | references    | pending 0/3 · meso     | Back-view refs cannot lock face identity                         |
| L06 | character     | pending 1/3 · meso     | Distinguish lookalike characters with immutable features         |
| L07 | delivery      | pending 1/5 · macro    | Deliverables as reviewable artifacts, not file dumps             |
| L08 | consistency   | pending 1/3 · meso     | Palette consistency within same world/time                       |
| L09 | references    | pending 1/3 · meso     | Crop refs to isolate target element                              |
| L10 | model-limits  | pending 1/5 · macro    | Recognize prominence floor; stop diminishing-return regens       |
| L11 | references    | pending 0/5 · macro    | Tier-1 refs designed for video-pipeline continuity               |

## TEMPLATES

- [`templates/session-kickoff.md`](templates/session-kickoff.md) — 5-step intro Claude runs at session start.
- [`templates/lesson-template.md`](templates/lesson-template.md) — skeleton for new lessons.
- [`templates/batch-plan-template.md`](templates/batch-plan-template.md) — dependency-graph planner for multi-shot projects.

## ARENA (synthetic validation)

Auto-leveling via adversarial scenarios. See [`arena/README.md`](arena/README.md).

- Run a trial via [`arena/run-playbook.md`](arena/run-playbook.md) — full
  8-step workflow with a single human checkpoint after Generator.
- Ledger rows from arena use `Project = arena:SXX`, `Reviewer = AI-jury`.
- **Distinct-project rule:** a scenario counts toward validation only if
  it flips ≥3 of 9 axes from DHYANA AND ≥2 axes from any prior arena
  scenario for the same lesson (see [`arena/axes.md`](arena/axes.md)).
- Four AI roles: 🎲 Generator → 🖌️ Runner (blinded) → ⚖️ Judge → 🕵️ Skeptic.
- Lessons that void 3+ trials consecutively get flagged
  `arena-unresolvable` and must be rewritten or retired.

## SISTER SKILLS

- **`seedance-craft-lv`** — same leveling pattern, but for video (ByteDance Seedance). If the task involves video, route there.
- **`kie-nano-banana`** — raw KIE API calls. This skill is the strategy layer above it; that one is the execution layer.
