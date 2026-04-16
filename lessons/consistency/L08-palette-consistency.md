---
id: L08
title: Palette consistency within same world/time must be explicit
theme: consistency
tier: meso
status: pending
validation: 1/3
tags: [palette, color, world-time, cross-shot, cinematography]
origin_project: DHYANA
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: [L01, L03]
---

# L08 — Palette consistency within same world/time must be explicit

## TL;DR

All shots in the same world/time must share one named palette. Refs lock composition/geometry — not palette.

## Context

DHYANA flashback scenes — #04 (mother walking into upload center) and #08 (upload exterior) both supposed to be the same location at the same pre-dawn moment. User caught that #04 had warm pink-amber memory palette while #08 had cool clinical blue palette — two very different moods for what should be the same scene.

## Mistake

When regenerating #04 with #08 as architecture ref, assumed palette would inherit from the ref image. It didn't — model used ref for composition/geometry only, re-decided palette from prompt. Prompt said "pre-dawn" but gave Nano too much latitude.

## Why it happened

Confused "reference locks visual identity" with "reference locks EVERY visual attribute". Palette is a separate axis that needs its own anchor or explicit instruction. Vague terms like "pre-dawn" or "dusk" interpret wildly across generations.

## Fix

Explicit palette statement in prompt: name the exact color gradient ("warm pink fading to pale amber, warm ground fog, NO cold blue") + state what palette should be matched from ref image + negative-state the wrong palette. When using multiple refs, tell the model which ref dictates palette vs. which dictates architecture vs. which dictates character.

## Broader rule

A single world-time has a palette. All shots in that world-time must share it explicitly. Cross-world-time deliberately differs (cinematography). Group shots by world-time and check each group's palette consistency separately.

## Validation log

| # | Project | Date       | Technique applied                                         | Outcome | Notes                        |
|---|---------|------------|-----------------------------------------------------------|---------|------------------------------|
| 1 | DHYANA  | 2026-04-16 | Regenerated #08 v2 warm-amber palette matching #04        | pass    | Memory flashback cohesion    |

## Cross-references

- Related lessons: L01, L03
- Checklist items affected: pre-submit A.4
