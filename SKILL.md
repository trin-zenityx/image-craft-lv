---
name: image-craft-lv
description: >-
  Discipline layer for STILL-IMAGE prompt engineering (Nano Banana, Midjourney,
  DALL·E, Stable Diffusion, Flux). Enforces a Pre-submit Checklist, Batch Gate,
  and Post-generate Self-review before/after any still-image generation.
  Maintains a lessons library; Claude proposes new lessons + LV bumps with
  reasoning, user decides. Auto-invoke whenever about to write/submit/refine a
  still-image prompt, plan a multi-shot image project, or debug drift between
  related images. DO NOT use for video prompting or raw API
  calls (see kie-craft-lv).
level: 2.15
updated: 2026-08-12
sister_skills: [kie-craft-lv, internal-board-builder]
---

# image-craft-lv

> Living skill. Lessons accumulate in `lessons/`. Claude proposes; user decides. Single source of truth for the level is the `level:` field above.

## THE RULE

**Before submitting ANY still-image prompt, run the Batch Gate, then the Pre-submit Checklist. Before showing generated output to the user, run the Post-generate Self-review.**

## BATCH DISCIPLINE GATE

Still-image gens are cheaper than video but batching 20 shots with a systemic error is still painful.

- **First gen in this project/session?** Render a single test first. Never batch without a baseline.
- **First time using a technique (new ref strategy, new model, new prompt structure)?** Test 1–3 gens before batching.
- **Batch >3 shots?** Report a cost estimate to the user before submitting.
- **User approved batching after seeing tests?** If not, stop. Ask.

Anti-pattern: submitting 20 gens before confirming the first 1–3 work.

## PRE-SUBMIT CHECKLIST

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
- [ ] Under the model's ref limit (Nano Banana 2.1: 10; Nano Banana Pro: 8; Nano Banana 2: 14; Seedance Omni: 9).
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

1. **Mismatch between shots beats beauty per shot.** Two adequate matched shots > a perfect #1 and a perfect #2 that don't match.
2. **Ambiguity = model's choice, not yours.** Every unstated detail is a coin-flip. State everything that matters; accept the rest as generative surprise.
3. **Reference images are not optional polish — they are foundational.** For any multi-shot project, ref chains are designed BEFORE the first generation.
4. **Numbers > adjectives.** "2.1 meter" not "long". "85 mm" not "telephoto". "40 rack columns" not "many racks".
5. **Negative-state the common failures.** "No age markers, no text, no watermark, no [specific failure you have seen]".
6. **Self-review is not optional.** It is the last step of generation.
7. **Face identity is HIGHER priority than pose / action fidelity.** If face renders well but pose is simpler than described, that is the PREFERRED outcome. State this explicitly at the bottom of every multi-plate prompt — e.g. `"FACE IDENTITY HAS HIGHER PRIORITY THAN POSE / ACTION DETAILS — preserve face above all else."`
8. **Filter problems are diagnosed by layer (word / combo / structural) and fixed by tier.** The full system — classify-first, R1→R5 playbook, vocab tier registry, error taxonomy — now lives in the standalone **`filter-craft-lv`** skill (migrated from L13/L17/L18). Invoke it whenever a generation fails or edgy wardrobe is going out. Never silently rewrite wardrobe to "filter-safe vocab" — propose a tier assignment for any new triggering word per `filter-craft-lv/VOCAB.md`.

## LESSONS LIBRARY

Index + headlines: [lessons/README.md](lessons/README.md). One lesson per file under themed folders.

Loading rule: at task start, glance at the README cheatsheet and load only the themes relevant to the current task — not every lesson every time.

## LEVELING (simple version)

No point system, no thresholds, no "session-end review". The flow:

- **New lesson** — when Claude observes a pattern, failure, or insight worth keeping: propose to the user with reasoning. User says yes (add to library), edit (revise then add), or no (drop).
- **LV bump** — when active lessons have accumulated enough that they meaningfully change behavior: Claude proposes a bump with reasoning. User says yes/no.
- **Archive** — when a lesson is no longer useful (superseded, model changed, false): move file to `lessons/archive/` and note in `lessons/README.md`. The lesson file is kept for reference, just not loaded.

The `level:` in the frontmatter is the single source of truth. Body text doesn't repeat it. Level history lives in [CHANGELOG.md](CHANGELOG.md). Notable outcomes worth narrating live in [OUTCOMES_HISTORY.md](OUTCOMES_HISTORY.md) (audit only — not used for promotion).

## TEMPLATES

- [`templates/lesson-template.md`](templates/lesson-template.md) — skeleton for new lessons.
- [`templates/batch-plan-template.md`](templates/batch-plan-template.md) — dependency-graph planner for multi-shot projects.

## SISTER SKILLS

- **`kie-craft-lv`** — raw KIE API calls (image AND video incl. Seedance submission). This skill is the strategy layer above it; that one is the execution layer. (The former `seedance-craft-lv` video-prompting sister was retired 2026-06-12, rebuild planned — archived at `~/.claude/skills/_backups/seedance-craft-lv-removed-*/`.)
- **`internal-board-builder`** — for building local HTML review boards (L16's home).
