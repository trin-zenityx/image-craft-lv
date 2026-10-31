---
id: L03
title: Opaque vs transparent container surfaces must match across the set
theme: consistency
added_at_lv: 1.0
tags: [design-language, containers, cross-shot, vocabulary]
created: 2026-04-15
last_updated: 2026-04-15
supersedes: []
related: [L01, L08]
---

# L03 — Opaque vs transparent container surfaces must match across the set

## TL;DR

Pick one unambiguous phrase per surface treatment (opaque vs transparent) and reuse it identically across every prompt in the set.

## Context

DHYANA pods — #6 corridor and #7 detail.

## Mistake

Said "transparent/frosted panels" in the detail prompt, same subject but different word choice than corridor prompt. Model rendered #6 with entirely opaque bodies (only face-window) and #7 with transparent-torso panels.

## Why it happened

Vague wording + no cross-shot design-language statement. Each prompt re-decides the design.

## Fix

In any multi-shot prompt set, pick one unambiguous phrase for each surface treatment and use it identically: "completely OPAQUE white ceramic shell along entire body, with face-window as the only transparent surface". Then mirror it exactly in every prompt that features that object.

## Broader rule

Design-language facts established in one shot must be stated the same way in every related shot. Vague wording = model re-decides per gen.

## Cross-references

- Related lessons: L01 (ref chains), L08 (palette consistency)
- Checklist items affected: pre-submit A.4 (design-language match)
