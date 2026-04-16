---
id: L04
title: Self-review before showing output prevents obvious failures from reaching the user
theme: workflow
tier: macro
status: pending
validation: 0/5
tags: [self-review, qa, delivery-cadence, full-frame-scan, proportion]
origin_project: DHYANA
created: 2026-04-15
last_updated: 2026-04-15
supersedes: []
related: [L07]
---

# L04 — Self-review before showing output prevents obvious failures from reaching the user

## TL;DR

After every batch, view each image and run the Post-generate Self-review checklist. Never ship without. User QA is not a substitute for self-review.

## Context

DHYANA Tier 1 delivery.

## Mistake

Rendered 12 images, renamed, and showed them to user without scanning for issues myself. User caught the face-orientation problem on #7 that I should have caught first.

## Why it happened

Treated "generate succeeds, file downloads" as completion. Skipped the step of actually LOOKING at each image with a critical eye.

## Fix

After every batch, view each image, scan against the Post-generate Self-review checklist. Flag issues, regen, THEN show user.

## Broader rule

Self-review is the last step of generation, not a nice-to-have. User reviewing your output is their check, not yours.

## Validation log

| # | Project | Date       | Technique applied                           | Outcome | Notes               |
|---|---------|------------|---------------------------------------------|---------|---------------------|
| 1 | DHYANA  | 2026-04-15 | Codified; no gen since then                 | pending | Awaits next batch   |

## Cross-references

- Related lessons: L07 (reviewable artifacts)
- Checklist items affected: entire Post-generate Self-review block (items #1–7)

## Reinforcements

**CRITICAL — Proportion comparison rule:** When checking "does X match ref Y" for proportions, compare to the **ORIGINAL full-scale ref image**, NOT a zoomed/cropped version. A crop enlarges the target in your field of view, which tricks you into thinking the proportions in the new image are fine when they may be 2-3x too large. Do the comparison at equal zoom levels.

**CRITICAL — Full-frame scan rule (anti-tunnel-vision):** When regenerating to fix issue A, DO NOT only verify A. Scan the ENTIRE frame against ref image for unrelated drifts introduced by the regen: environment (ceiling, walls, floor), background elements (other objects, fog density, light sources), lighting direction, color temperature, depth cues. Regens often fix the target but introduce new drifts elsewhere because the model re-decides unspecified details. List every environmental element of the ref image and confirm each is preserved before shipping.
