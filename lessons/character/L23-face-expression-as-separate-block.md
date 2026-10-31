---
id: L23
title: Face EXPRESSION as separate prompt block, with explicit "NOT hard, NOT stiff" anti-pattern
theme: character
added_at_lv: 2.7
tags: [face, expression, prompt-engineering, naturalness, emotion]
created: 2026-05-05
last_updated: 2026-05-05
supersedes: []
related: [L19, L20, L22]
---

# L23 — Face EXPRESSION as separate prompt block, with explicit "NOT hard, NOT stiff" anti-pattern

## TL;DR

Burying expression inside a pose / framing block ("standing confidently with a sultry expression") loses prioritization — the AI optimizes for pose first and treats expression as decorative, defaulting to its house "fashion-model resting face" (jaw clenched, eyes hard, lips tight).

**Pull face EXPRESSION into its own dedicated prompt block** with explicit positive descriptors and explicit "NOT hard, NOT stiff" anti-pattern. The visual separation in the prompt structure raises the priority weight on expression and forces the model to treat it as a first-class spec.

## Context

Alisa Glamour Photobook v2 buried expression in the pose ("leaning back with a sensual look"). Output faces read as "AI fashion-model default" — hard, stiff, jaw-clenched, eyes too direct. v3-v4 broke expression into its own block:

```
EXPRESSION: relaxed warmth, soft eyes with slight smile-line at corners,
lips natural and slightly parted (not pressed). Genuine ease.
NOT: hard glamour stare, NOT clenched jaw, NOT stiff doll pose.
```

Output faces became natural, expressive, on-brief.

## Mistake

Treating expression as a sub-attribute of pose. The model reads pose as a structural directive (where the body goes) and expression as a flavor word — loses the priority weight needed to override the AI's hard-stare default.

## Why it happened

The AI's default for "fashion-model" / "editorial" / "glamour" prompts is a tightly clustered face expression — what Trin labels "hard glamour stare." This default is so strong that any expression word buried in a longer block fails to overcome it. Pulling expression into a dedicated block with explicit positives + negatives raises the local prompt-attention weight on those tokens.

## Fix

Restructure prompts to give expression its own block:

```
EXPRESSION:
  Positive: [relaxed warmth | quiet confidence | playful softness | etc.]
  Eyes: [soft / direct / averted, with specific physical descriptor]
  Mouth: [lips relaxed / slight smile / parted / etc.]
  NOT: hard glamour stare, NOT clenched jaw, NOT stiff doll pose,
       NOT vacant eyes
```

Place the block adjacent to (but separate from) the pose block. The visual separation in the prompt mirrors the structural separation in the model's attention.

## Broader rule

For any prompt where face / expression rendering matters, isolate the expression spec into its own prompt block, with both positive descriptors and explicit anti-pattern. Don't bury expression inside pose, mood, or framing — it loses priority weight.

This is a specific instance of a more general prompt-craft rule: **first-class concerns deserve first-class prompt blocks**. Burying a concern inside an unrelated block downgrades its attention weight.

## Cross-references

- Related lessons: L19 (narrative pose per plate — pull expression OUT of the pose narrative), L20 (camera body + film stock — Portra signature pairs with soft expression), L22 (anti-overproduction calibration — "NOT hard, NOT stiff" is a calibrated anti-directive paired with positive replacements)
- Checklist items affected: pre-submit B (ambiguity sweep — expression is one of the most under-specified elements, especially when buried in pose)
