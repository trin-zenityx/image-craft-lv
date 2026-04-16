---
id: L01
title: Reference chains beat text-only for multi-shot sets
theme: consistency
tier: macro
status: pending
validation: 1/5
tags: [multi-shot, reference-chain, dependency-graph, character, location]
origin_project: DHYANA
created: 2026-04-15
last_updated: 2026-04-15
supersedes: []
related: [L05, L09, L11]
---

# L01 — Reference chains beat text-only for multi-shot sets

## TL;DR

For multi-shot sets, build a ref-chain dependency graph before the first gen. Text-only prose drifts.

## Context

DHYANA project Tier 1 round 1 — 12 anchor images for a 25-shot short film.

## Mistake

Generated all 12 with text-only prompts. Relied on verbal repetition ("saffron robe, shaved scalp, weathered olive-tan skin") to keep Tenzin's face consistent across #1 frontal and #2 profile.

## Why it happened

Assumed prose repetition was sufficient. Didn't think about model's stochastic interpretation per call.

## Fix

Build dependency graph. Generate master anchors first (no refs). Generate secondary with master refs. Generate tertiary with master + secondary refs. Per the Nano Banana skill, pass `--reference path/to/anchor.png` as many times as needed.

## Broader rule

Build dependency graph before the first generation. Generate master anchors with no refs; secondary shots use master as ref; tertiary uses master + secondary. This applies to any project reusing a character, location, or prop across more than one image.

## Validation log

| # | Project | Date       | Technique applied                                | Outcome | Notes                |
|---|---------|------------|--------------------------------------------------|---------|----------------------|
| 1 | DHYANA  | 2026-04-15 | Ref chain for Tier 1 v2 (12 regenerated images)  | pass    | Face + arch locked   |

## Cross-references

- Related lessons: L05 (back-view refs), L09 (crop refs), L11 (video-continuity refs)
- Checklist items affected: pre-submit A (all), C.3 (chain order), D.1 (dependency graph)
