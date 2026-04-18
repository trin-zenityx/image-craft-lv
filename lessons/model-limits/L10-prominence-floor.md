---
id: L10
title: Recognize subject-prominence floor; stop diminishing-return regens
theme: model-limits
tier: macro
status: pending
validation: 1/5
tags: [model-prior, diminishing-returns, stop-iterating, post-processing, subject-prominence]
origin_project: DHYANA
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: []
---

# L10 — Recognize subject-prominence floor; stop diminishing-return regens

## TL;DR

When a regen improves the metric less than the previous attempt did, you are approaching the model's floor. Stop prompt-tuning. Either accept the floor honestly or switch tools (inpainting, post-process, different model).

## Context

DHYANA #07 pod detail — attempted to shrink the face-window from 31% of pod length to target 13%. Iterated through 7 versions with increasingly explicit prompts (numeric ratios, real-world size metaphors, edit-style instructions, Nano Banana 2 model). Ratio improved 31% → 20% → 19% → 17%, then plateaued. Could not get below 17%.

## Mistake

Kept iterating assuming the next prompt tweak would close the gap. Each subsequent regen gave diminishing returns (first attempt -11 points, fifth attempt -0 points).
Result: Wasted several cycles trying to hit exact target. User had to spend review energy on diminishing-return regens.

## Why it happened

Image models have semantic priors that bias toward making subjects "readable" — faces in particular render prominently because that's what the model was trained to prioritize. No amount of prompt engineering overrides a learned prior completely. The model will interpret "small face" within a reasonable floor that keeps the face visible.

## Fix

When a regen improves the metric but less than the previous attempt did, you are approaching the model's floor. Compare the improvement curve: 11 points → 1 point → 2 points → 0 points = diminishing returns = stop. Either (a) accept the floor as "good enough" with honest measurement and user consent, or (b) move to post-processing / different tool, not more prompt tuning.

## Broader rule

Prompt tuning is effective within the model's prior envelope. Beyond the envelope, you need different tools (inpainting, PIL post-process, image-to-image with different model). Recognize diminishing returns quickly (by attempt 3 usually), don't burn 7 rounds chasing 2 percentage points.

## Validation log

| # | Project | Date       | Technique applied                                            | Outcome | Notes                                   |
|---|---------|------------|--------------------------------------------------------------|---------|-----------------------------------------|
| 1 | DHYANA  | 2026-04-16 | Stopped at 17% face-window ratio (target 13%) for #07 v10    | pass    | 7-regen diminishing curve observed      |

## Cross-references

- Related lessons: none direct; this lesson modifies the regen-decision flow across ALL other lessons
- Checklist items affected: decision to re-enter Post-generate Self-review loop vs accept output
