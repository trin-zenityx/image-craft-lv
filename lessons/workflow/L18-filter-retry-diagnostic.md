---
id: L18
title: Filter blocks don't cost credits — retry 3-5× as diagnostic before modifying prompt
theme: workflow
tier: meso
status: pending
validation: 1/3
tags: [google-filter, retry, diagnostic, cost, input-vs-output-filter]
origin_project: alisa-glamour-photobook
created: 2026-05-05
last_updated: 2026-05-05
supersedes: []
related: [L13, L17]
---

# L18 — Filter blocks don't cost credits — retry 3-5× as diagnostic before modifying prompt

## TL;DR

Filter-blocked generations on Google / Imagen do **not** consume credits. Before editing the prompt or ref strategy, **retry the same prompt 3-5×**. The retry pattern itself diagnoses which filter fired:

- **Always blocks (3-5/5):** input-side prompt filter (deterministic). Vocabulary needs to change.
- **Sometimes blocks (1-2/5):** output-side image filter (stochastic, sees the rendered candidate). Same prompt + same refs can pass; just retry until it does.

Skipping this diagnostic = changing the prompt unnecessarily and degrading the output for free.

## Context

During Alisa Glamour Photobook G01 v3-v4 generation, several plates returned filter blocks intermittently. Initial reflex was to immediately rewrite vocabulary, which caused unnecessary drift in the recipe. Switching to a retry-first protocol revealed that ~half of the blocks were stochastic output-filter rejections — the same prompt passed cleanly on the next attempt.

## Mistake

Treating every filter block as a signal to modify the prompt. This:

1. Wastes time on rewrites that were never needed (the output filter would have passed on retry).
2. Erodes a prompt that was working — each rewrite is a chance to introduce a bug.
3. Conflates two distinct filter mechanisms with very different remedies.

## Why it happened

The two filter layers (input prompt filter, output image filter) return identical-looking error responses. Without a diagnostic step, a stochastic output rejection is indistinguishable from a deterministic prompt block.

The economic asymmetry isn't intuitive either: most paid APIs charge for any attempt. Imagen / Google does not charge for filter rejections, which makes retry essentially free.

## Fix

When a filter block fires:

1. **Check it's not a network / quota error first** (different error class — those DO consume credits).
2. **Retry the exact same prompt + refs 3-5 times**, no edits.
3. **Read the pattern:**
   - 0/5 blocks → wasn't actually a filter issue, ignore.
   - 1-2/5 blocks → output-filter stochastic. Keep retrying for that plate; do not rewrite the prompt.
   - 3-5/5 blocks → input-filter deterministic. NOW edit prompt vocabulary (per L13 sweet spot).
4. Log the retry pattern in your generation notes so future plates with the same prompt skeleton can route the right way faster.

## Broader rule

For any model whose filter rejections are non-billable, **build retry-as-diagnostic into the workflow** before any prompt modification. The retry is a free experiment that distinguishes deterministic vs stochastic failure modes — and the remedies for each are completely different.

This is also a general debugging principle: when a system has multiple failure modes that look the same on the surface, design a cheap signal that splits them before applying a fix.

## Validation log

| # | Project | Date       | Technique applied                                          | Outcome | Notes                   |
|---|---------|------------|------------------------------------------------------------|---------|-------------------------|
| 1 | Alisa Glamour Photobook G01 v4 batch | 2026-05-05 | Retry-first protocol on all filter-blocked plates. Logged 3-5× retry pattern per plate before any prompt edit. | pass | ~half of blocks resolved on retry without prompt change. Other half showed deterministic block pattern → vocab swap (per L13) fixed those cleanly. Net: less prompt churn, cleaner recipe. |

## Cross-references

- Related lessons: L13 (sweet-spot vocab — the fix when retry fails), L17 (filter triggers on prompt text — explains why deterministic blocks happen)
- Checklist items affected: workflow / generation loop — add "retry 3-5× before edit" step
