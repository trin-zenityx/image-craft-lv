---
id: L12
title: Dual-ref (crop + full-scene) locks target AND scene context; crop-ref alone loses context
theme: references
tier: meso
status: pending
validation: 0/3
tags: [reference-image, dual-ref, cropping, scene-context, complement-to-L09]
origin_project: arena:S04
created: 2026-04-17
last_updated: 2026-04-17
supersedes: []
related: [L01, L09]
---

# L12 — Dual-ref (crop + full-scene) locks target AND scene context

## TL;DR

L09 (crop refs) locks the target element but **unanchors** everything else in the frame — the model re-imagines background, lighting, character clothing, palette from text prior. When the new shot is wider than the crop, **pass BOTH the crop AND the full-scene image** as references. The crop anchors the target; the full-scene ref anchors the rest.

## Context

Discovered during arena methodology investigation `2026-04-17-L09-S04` (Victorian laboratory orrery). After L09 was validated in S03, human review found that S03's crop-ref shot (3A) reproduced the target headdress correctly but **completely re-imagined the surrounding plaza** — different buildings, different crowd, missing pyramid from Shot 1. S04 was designed as a multi-factor experiment (ref-strategy × crop-size) to test whether dual-ref could resolve this.

## Mistake

Treating L09 ("crop the reference to isolate the target") as a universal solution. For close-up shots where the frame equals the crop, L09 works. For wider shots that include surrounding context, crop-only sacrifices the entire scene to gain one target lock — a trade, not a win.

Runner's self-review of S04 showed this explicitly in 3A-small: the outfit changed from steel-blue lab coat to tweed jacket and the palette shifted warm, even though the prompt and model were identical to other variants — because the small crop contained only the orrery with no character/scene context, so the model filled the rest from its text prior.

## Why it happened

A single reference image anchors what is VISIBLE in that reference. A tight crop of the target removes the scene from what the model can see, so the model falls back on text prior for everything not in the crop. This is how refs work mechanically — they teach, in proportion to how much of the frame each element occupies.

Models like Nano Banana Pro accept multiple references (up to 8). Using only 1 when 2 are needed is leaving capacity on the table.

## Fix

For shots where the new frame is wider than the target-isolating crop:

1. **Prepare TWO references:**
   - Ref A: tight crop of the target element (per L09)
   - Ref B: the full-scene source image (for context anchor)

2. **Pass both in the same API call:**
   - Pass the crop first (primary — signals target priority)
   - Pass the full-scene second (context — signals scene preservation)

3. **Use edit-style prompting that names what each ref does:**
   - "Match the [target] EXACTLY from reference 1; preserve the [scene/character/palette] from reference 2."

4. **Crop resolution matters** (see also L09 sub-rule): the crop should be ≥ 1024px on its longer side if the model output is ≥ 2K. Low-res crops lose edge detail and force the model to reconstruct the target fuzzily.

## Broader rule

Match the reference to what you want it to anchor. If you want one thing locked, use one ref; if you want target + scene BOTH locked, use two. Crop isolation (L09) and scene preservation are not in conflict — they are complementary, and the model supports both simultaneously through multi-ref input.

## Validation log

| # | Project | Date | Technique applied | Outcome | Notes |
|---|---------|------|-------------------|---------|-------|
| 1 | arena:S04 | 2026-04-17 | Dual-ref (small crop + full Shot 1) in Victorian-lab hero shot | pending (origin-experiment) | 3D-small ranked #1 at D3=2.000 vs best single-ref at D3=1.875. Skeptic flagged margin as fragile and S04 as methodology origin, NOT counted as arena validation pass. Requires S05 (different scenario) for first real validation entry. |

## Cross-references

- **Sibling:** [L09](L09-crop-refs.md) — L12 complements, not replaces. Use L09 when new shot ≈ crop bounds (target-only close-up). Use L12 when new shot is wider (hero shot, portrait with bg, scene-continuation).
- **Upstream:** [L01](../consistency/L01-ref-chains.md) — L12 is L01's ref-chain discipline applied to a single shot (2 refs for 1 output) rather than across multiple shots.
- **Checklist items:** pre-submit C.1 (most-relevant refs), C.3 (chain order).

## Known limitations (from S04 findings)

- **H4 was only partial** — one of two dual-ref variants (3D-large) dropped a scene element that the twin variant (3D-small) preserved. The Skeptic called this possibly stochastic (N=1 single gen per condition). Until replicated, recommend **dual-ref with small-to-medium crop** (not the largest possible crop) to reduce any competition between the crop and full-scene for the model's reconstruction capacity.
- **Findings from 1 scenario only.** Arena validation requires ≥2 axis-distinct projects showing Pass. L12 is currently pending 0/3.
