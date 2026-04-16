---
id: L09
title: Crop reference images to isolate the target element
theme: references
tier: meso
status: pending
validation: 1/3
tags: [reference-image, cropping, edit-mode, target-anchor]
origin_project: DHYANA
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: [L01, L05]
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

## Cross-references

- Related lessons: L01 (ref chains), L05 (back-view refs)
- Checklist items affected: pre-submit C.1, C.3

## Related technique

Per research, Nano Banana Pro treats reference images with edit-style prompting ("match THIS exactly", "preserve the pod in the reference") more restrictively than generation-style prompting ("in the style of..."). Combine cropped refs with edit-style language when you need exact matching.
