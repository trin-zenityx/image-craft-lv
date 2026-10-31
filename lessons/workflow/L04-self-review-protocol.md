---
id: L04
title: Self-review before showing output prevents obvious failures from reaching the user
theme: workflow
added_at_lv: 1.0
tags: [self-review, qa, delivery-cadence, full-frame-scan, proportion]
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

## Cross-references

- Related lessons: L07 (reviewable artifacts)
- Checklist items affected: entire Post-generate Self-review block (items #1–7)

## Reinforcements

**CRITICAL — Proportion comparison rule:** When checking "does X match ref Y" for proportions, compare to the **ORIGINAL full-scale ref image**, NOT a zoomed/cropped version. A crop enlarges the target in your field of view, which tricks you into thinking the proportions in the new image are fine when they may be 2-3x too large. Do the comparison at equal zoom levels.

**CRITICAL — Full-frame scan rule (anti-tunnel-vision):** When regenerating to fix issue A, DO NOT only verify A. Scan the ENTIRE frame against ref image for unrelated drifts introduced by the regen: environment (ceiling, walls, floor), background elements (other objects, fog density, light sources), lighting direction, color temperature, depth cues. Regens often fix the target but introduce new drifts elsewhere because the model re-decides unspecified details. List every environmental element of the ref image and confirm each is preserved before shipping.

## Audit checklist expansion (added 2026-05-01 from Alisa Future Mecha session)

Three failure modes that can sneak past a casual review — user caught them when self-audit missed them. Run these 3 checks explicitly on every multi-panel sheet:

**1. Edge artifact scan (duplicate / ghost figures):**
- Multi-panel sheets with dynamic poses + dense ref imagery + complex wardrobe can produce **ghost duplicate subjects** in a single plate (second body partially visible behind primary subject, doubled limbs, ghost overlapping torso).
- Don't just look at the central subject — **scan the FOUR EDGES of every plate** for unintended figures, doubled hair masses, ghost shoulders peeking out from behind primary subject.
- High-risk plates: tight close-ups with hair flowing across multiple directions, full-body shots with held props, refs that include duplicate elements.
- Validated on Alisa L3-Crimson-Pilot P3: ghost duplicate body visible on left edge that auditor missed initially.

**2. Back-view face identity check:**
- P4 plates (full-body back view with face turned over shoulder) are easy to skip during identity audit because face is small in frame.
- But **identity drift can absolutely happen** on small back-view faces — the AI generalizes when face occupies < 10% of frame.
- For every P4 plate: zoom to the face region and verify against master/hero identity (sculptural V-line jaw, eye shape, skin tone, etc.)
- Validated on Alisa L3-Crimson-Pilot P4: face turned over shoulder drifted to a generic softer face that wasn't the master subject. Auditor passed it because "back view, face is small". User caught it.

**3. Angle differentiation rule (P2 vs P3):**
- The whole point of having both P2 (frontal beauty close-up) and P3 (3/4 beauty close-up) in a sheet is to show two distinct angles of the same identity.
- A **slight head turn** is NOT a 3/4 angle. P3 must show **profile contour (jawline silhouette against background)** clearly visible, with one ear hidden, hair flowing to one side.
- Don't accept "well, P3 is slightly turned" — verify that P3 actually delivers the angle differentiation the sheet requires.
- Validated on Alisa L2-White-Goddess P3: P3 was essentially the same frontal angle as P2, just zoomed out wider. Auditor accepted because "wardrobe consistent, identity ok". User caught it.

**Rule of thumb:** When auditing a sheet, run all 3 checks on every plate explicitly. Don't pre-optimize ("this one looks ok overall") — the failure modes above all sneak past holistic review.
