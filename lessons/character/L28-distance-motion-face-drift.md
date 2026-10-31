---
id: L28
title: Distance + motion = face drift risk — when face occupies <15% of frame OR is in motion, expect identity loss
theme: character
added_at_lv: 2.12
tags: [face-drift, identity, wide-shot, motion, framing-budget]
created: 2026-05-07
last_updated: 2026-05-07
supersedes: []
related: [L26, L27]
---

# L28 — Distance + motion = face drift risk

## TL;DR

AI face identity matching weakens as the face's pixel area in the rendered frame decreases. **When the face occupies less than ~15% of frame area, OR when the face is captured during motion (driving, running, dancing), expect identity drift** — even with strong FACE_LOCK directives. The fix is structural (composition / pose), not vocabulary.

## When this lesson applies

- Wide environmental shots where the model is small in the frame
- Motion shots (driving, running, dancing, action)
- Any combination of distance + motion (worst case)

## The mechanism

Face identity preservation depends on the model's face having sufficient pixel resolution to anchor against the reference image. When the face is:

- **Small** (wide shot, distant subject): few pixels = weak identity signal = AI fills in plausible face = drift to "generic similar Asian/Western model"
- **In motion** (motion blur, action): blurred edges = unclear feature boundaries = AI cannot match precisely = drift
- **Both** (wide + moving): catastrophic identity loss is near-certain

FACE_LOCK directives in the prompt do NOT compensate for this — they are linguistic, not pixel-budget controls.

## Mistake (canonical case)

**Jira Wanderlust Vol 06**:

- **J05-P6 (wide vista v1)**: model was ~30% of frame in a "very wide vista" composition. Face was tiny. Trin: *"หน้าเปลียนเป็นคนละคน"*.
- **J05-P7 (driving away v1)**: car was driving away from camera at distance + motion blur. Face was small AND moving. Trin: *"หน้าเปลียนเป็นคนละคน"*.

Both plates had FACE_LOCK at the top of prompt and explicit "TACK-SHARP face" guidance. The directives could not save the composition.

## Fix protocol

When a plate calls for wide framing OR motion:

### Option A — Bring the face closer (preferred for wide shots)
- Specify "model in foreground 45-50% of frame height" instead of "model small in distance"
- Still cinematic, but face has enough pixels to anchor identity
- Use 35-50mm lens, not 24mm extreme wide

### Option B — Stop the motion (preferred for action shots)
- Convert "driving away" → "car parked at viewpoint"
- Convert "walking briskly" → "paused mid-stride"
- Convert "in motion blur" → "static moment of movement"
- Face becomes capturable; the implied narrative still reads (just-arrived, just-stopped)

### Option C — Both (preferred for wide + motion)
- Stop motion AND bring closer (gives both cinematic vibe AND identity)

### Option D — Accept the loss (last resort)
- If wide vista is non-negotiable, expect identity drift and either accept it or downgrade the plate's importance
- Useful for environmental/atmospheric plates where identity is secondary to mood

## Anti-patterns

- ❌ Adding more "TACK-SHARP face" directives to wide/motion shots and expecting different results
- ❌ Wide vista with 30% model framing for any plate that needs identity preservation
- ❌ "Driving away" / "running away" / "fading into distance" closing-hero compositions
- ❌ Treating FACE_LOCK as a compensator for low pixel budget

## Quick reference

| Composition | Face % of frame | Identity risk |
|---|---|---|
| Tight chest-up close | 30-40% | very low |
| Medium 3/4 portrait | 15-25% | low |
| Full body | 10-15% | medium |
| Wide environmental (model 50%) | 8-12% | medium-high |
| Very wide (model 30%) | <5% | **high** |
| Motion + wide | <5% + blur | **catastrophic** |

## Cross-references

- Related lessons: L26 (diversity matrix — wide environmental is one valid axis but must respect face budget); L27 (disembodied details — different framing problem)
- Checklist items affected: pre-submit B (ambiguity sweep) — add face-pixel-budget check; post-generate self-review #2 (orientation / face) — verify identity at planned framing
