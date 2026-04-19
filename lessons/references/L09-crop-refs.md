---
id: L09
title: Crop reference images to isolate the target element
theme: references
tier: meso
status: validated
validation: 2.5/3
tags: [reference-image, cropping, edit-mode, target-anchor]
origin_project: DHYANA
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: [L01, L05, L12]
---

# L09 — Crop reference images to isolate the target element

## TL;DR

When a ref must lock ONE specific element (object, pose, color), crop it so that element fills the frame. Full-scene refs dilute the anchor.

## Context

DHYANA #07 pod detail — multiple regen attempts (v3, v4, v5, v6) all used the full pod corridor image (#06) as reference. Each regen produced pods with different shapes — a bulgy egg, a compact head-only capsule, a disproportioned hybrid — none matched the sleek elongated capsule shape visible in #06.

## Mistake

Passed the entire corridor image as ref when only ONE specific object needed to be matched exactly. The model had too much visual information (corridor, water, multiple pods at various angles, background racks) and couldn't decide which element was the "target". It reinterpreted pod shape each generation.

## Why it happened

Treated "use reference" as "pass the related image". Did not consider that the ref's job is to anchor a specific visual element, and including unrelated elements dilutes that anchor.

## Fix

When a ref needs to lock ONE element (specific object, specific pose, specific color), crop the source image to contain ONLY that element. Use PIL/ImageMagick to extract the tight region. Pass the crop as the primary ref. This gives the model an unambiguous visual target.

## Broader rule

A reference image teaches the model what it shows, in proportion to how much of the frame that thing occupies. If the pod is 10% of a scene ref, the pod design is 10% "loud" to the model. If the pod fills the frame of a cropped ref, it is 100% loud.

## Validation log

| # | Project | Date       | Technique applied                                          | Outcome | Notes                   |
|---|---------|------------|------------------------------------------------------------|---------|-------------------------|
| 1 | DHYANA  | 2026-04-16 | Cropped pod front (1885×1280 of 4096×2286) used for #07 v7 | pass    | Silhouette finally matched |
| 2 | arena:S02 | 2026-04-17 | Iron tsuba A/B control (3A crop-ref vs 3B full-ref, identical sparse text) | partial | 3A beat 3B on 2/4 dimensions (arc + overall); Skeptic adversarial-valid. 7-axis flip from DHYANA |
| 3 | arena:S03 | 2026-04-17 | Aztec penacho A/B control (all 4 dims directional/asymmetric) | **pass** | 3A beat 3B on 3/4 dimensions (left-fan + crown lean + overall); Skeptic adversarial-valid. 6-axis flip vs DHYANA/S01/S02. **PROMOTION to validated** |

## Scope limits (added from arena:S04 findings)

**L09 alone is NOT sufficient when the new shot is wider than the crop.** A crop-only ref anchors the target element but unanchors everything else in the frame — model re-imagines bg/character/palette from text prior. For shots that include surrounding context, **combine L09 with L12 (dual-ref)**: pass both the crop and the full-scene source.

**Crop resolution matters.** Arena:S04 found that small crops (< output resolution, e.g. 353×512px feeding a 4K hero shot) can fail to convey fine target detail even when the crop correctly isolates the element. Rule of thumb: **the crop's long side should be ≥ ½ of the output's long side**. Use the native-resolution crop of Shot 1 when possible; downscale the crop only when the generated shot is similarly small.

## Cross-references

- Related lessons: L01 (ref chains), L05 (back-view refs), **L12 (dual-ref — use together when new shot wider than crop)**
- Checklist items affected: pre-submit C.1, C.3

## Related technique

Per research, Nano Banana Pro treats reference images with edit-style prompting ("match THIS exactly", "preserve the pod in the reference") more restrictively than generation-style prompting ("in the style of..."). Combine cropped refs with edit-style language when you need exact matching.
