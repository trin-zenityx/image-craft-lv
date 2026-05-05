---
id: L22
title: Anti-overproduction directives are calibration tools, not blanket switches
theme: prompt-craft
tier: meso
status: pending
validation: 1/3
tags: [anti-prompt, calibration, overproduction, sensuality, glamour, natural]
origin_project: alisa-glamour-photobook
created: 2026-05-05
last_updated: 2026-05-05
supersedes: []
related: [L20, L21, L23]
---

# L22 — Anti-overproduction directives are calibration tools, not blanket switches

## TL;DR

Negative directives like `"NOT magazine glamour"`, `"NOT boudoir"`, `"NOT lingerie"` are **calibration tools**, not safety switches. Used surgically, they pull back specific over-polish tendencies the AI defaults to. Used as a blanket, they over-correct and kill the sensuality / mood the brief actually needs.

**Always pair an anti-directive with a positive descriptor of what you DO want.** A negative directive without a positive replacement leaves the AI in default-fill mode — and the default usually overshoots in the opposite direction.

## Context

Alisa Glamour Photobook v3 attempted a "natural" recipe by stacking anti-directives: `"NOT magazine glamour, NOT boudoir, NOT lingerie, NOT over-retouched"`. Output went too far the other way — modest, unsensual, missed the photobook brief entirely. v4 kept only `"NOT magazine glamour"` (the actual problem to solve) and added positive replacement: `"natural sensuality, relaxed editorial posture, soft daylight"` — recipe locked.

## Mistake

Using anti-directives as a global mood switch ("turn off the glamour"). This treats the AI as if anti-directives were independent levers, when in fact each anti-directive shifts the joint distribution — and stacking several can over-shift it past where you wanted.

Specifically: telling the model "not boudoir, not lingerie" while the brief is glamour-natural pushes the model away from any sensual register at all, because the model's interior representation of "sensual" overlaps with both removed clusters.

## Why it happened

The AI does not parse negative directives compositionally ("remove only the glamour part"). It downweights everything it associates with the negated cluster — and clusters overlap. Over-stacking negatives subtracts from the very signal you wanted to keep.

## Fix

Calibration recipe for anti-directives:

1. **Diagnose first.** What specifically over-fires when you don't use anti-directives? "Plastic skin"? "Hard glamour light"? "Over-retouched face"? Name it.
2. **One anti-directive per identified over-fire.** `"NOT magazine glamour retouch"` is precise; `"NOT magazine glamour"` is broader; `"NOT glamour"` is too broad.
3. **Always pair with positive replacement.** `"Skin: matte, soft pores, K-beauty polished, zero plastic shine"` — the positive descriptor tells the AI what to do INSTEAD.
4. **Test by removing anti-directives one at a time.** If output stays on-brief without the directive, the directive was unnecessary and was costing you signal.

Default to fewer, more surgical anti-directives. When in doubt, use a positive descriptor instead of a negative one.

## Broader rule

Negative prompts down-weight clusters in the model's prior. Stacking many of them shrinks the available distribution of outputs and can push past the target. Use anti-directives surgically, paired with positive replacements, and audit which ones are actually load-bearing.

This generalizes: any specification-by-negation system (negative regex, exclusion filters, blocklists) has the same failure mode — over-broad rules subtract from the target along with the noise.

## Validation log

| # | Project | Date       | Technique applied                                          | Outcome | Notes                   |
|---|---------|------------|------------------------------------------------------------|---------|-------------------------|
| 1 | Alisa Glamour Photobook v3 → v4 | 2026-05-05 | v3 stacked 4 anti-directives → over-corrected output (modest, unsensual). v4 reduced to 1 anti-directive + positive replacements → on-brief glamour-natural. | pass | Validated by direct A/B comparison. Anti-directive count reduced 4→1 and mood landed correctly. |

## Cross-references

- Related lessons: L20 (positive skin description = the positive replacement for "not plastic"), L21 (designer aesthetic anchors — when paired with anti-directives, the calibration question is which one is doing the work), L23 (face expression as separate block — common positive replacement for "not hard" anti-directives)
- Checklist items affected: pre-submit B (ambiguity sweep — count anti-directives, audit each for necessity)
