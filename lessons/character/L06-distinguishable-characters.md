---
id: L06
title: Different characters in similar contexts must be made visibly distinct
theme: character
tier: meso
status: pending
validation: 1/3
tags: [characters, distinguishable-features, plot-integrity, generic-vs-specific]
origin_project: DHYANA
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: [L05]
---

# L06 — Different characters in similar contexts must be made visibly distinct

## TL;DR

When a "generic" background character shares context with a "specific" important character, specify immutable distinguishing features (gender, ethnicity, hair, facial structure) for BOTH. Otherwise the model renders both as generic variants of the same face.

## Context

DHYANA g10a (generic pod sleeper in Act 3) and g15b (specifically the mother's pod in Act 4). Both rendered as "neutral adult face sleeping in pod" — model gave both roughly-similar-looking adult women. User could not distinguish them, which would destroy the Act 4 reveal ("he finds his mother among thousands") because viewers would think he already saw her in Act 3.

## Mistake

Assumed "generic neutral adult" description was sufficient for the background character (g10a). Did not specify immutable features to distinguish from the specific character (g15b mother).

## Why it happened

When one character is "generic" and another is "specific", prompting only the specific one forces the model to invent features for the generic one — often landing on a similar default, especially when both share context (same pod, same pose, same lighting).

## Fix

Even for "generic" background characters, specify immutable distinguishing features (gender, ethnicity, hair color/length, facial structure) that guarantee a viewer can't confuse them with the specific/important character in the same set. Phrase in negative as well: "this is NOT the [other character] — specifically a man with grey hair, not a woman with dark hair".

## Broader rule

The self-review checklist must cross-check pairs of shots featuring different-but-similar-context characters. Not just "does character A stay consistent across A's shots" but "does character A look different from character B".

## Validation log

| # | Project | Date       | Technique applied                                         | Outcome | Notes                   |
|---|---------|------------|-----------------------------------------------------------|---------|-------------------------|
| 1 | DHYANA  | 2026-04-16 | g10a v2: adult male grey hair, distinct from g15b mother  | pass    | Reveal integrity preserved |

## Cross-references

- Related lessons: L05 (back-view refs — which views to anchor)
- Checklist items affected: pre-submit B.5 (character distinguishability)
