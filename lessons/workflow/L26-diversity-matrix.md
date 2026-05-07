---
id: L26
title: For multi-plate sets, build an explicit diversity matrix BEFORE generating to prevent visual repetition
theme: workflow
tier: meso
status: pending
validation: 1/3
tags: [photobook, multi-plate, diversity, narrative-arc, planning]
origin_project: jira-wanderlust-vol06
created: 2026-05-07
last_updated: 2026-05-07
supersedes: []
related: [L19, L24]
---

# L26 — Diversity matrix per plate BEFORE generation

## TL;DR

When designing a photobook set with multiple plates of the same look (e.g., 7-plate sets, 8-plate sets), build an **explicit diversity matrix** as the very first step — BEFORE writing prompts. The matrix forces each plate to differ from every other plate across at least 2 of 4 axes:

| Axis | Example values |
|---|---|
| **Camera distance** | very wide / wide / medium 3/4 / chest-up close / detail |
| **Camera angle** | eye-level / low-angle (looking up) / high-angle (looking down) / behind / over-shoulder |
| **Body pose** | standing / sitting / leaning / walking / lying / kneeling / reclined |
| **Action / state** | static / in motion / interacting with object / candid moment / contemplative |

If two plates share 3+ axis values, they will look like duplicates of each other in the final review — **regardless of how varied the prompt text reads**.

## When this lesson applies

- Multi-plate sets per look (typically 7-8 plates)
- Same character + same wardrobe + same setting across plates
- Goal: visual variety across the set, not narrative-equivalent repetition

## Mistake (canonical case)

**Mila Studio Photobook (Vol 05) M03 White Bustier Angel** — first attempt produced 7 plates where P1, P4, P6, P7 were all "standing 3/4 turn with hand at hair" — the prompts described slightly different intents (hero / 3/4 turn / wide environmental / look-back closing) but the AI rendered all four as essentially the same standing-3/4 pose. User feedback: *"P1 P4 P6 P7 แทบจะเหมือนกันเลยครับ ออกแบบใหม่ ให้มีท่าทางที่แตกต่างกัน หรือมีสตอรี่ ไม่ใช่ใช้ท่าทางซ้ำๆ"*

Root cause: The prompt vocabulary varied ("confident," "elegant," "graceful," "look back"), but the underlying pose specification did NOT vary on the 4 axes — all four were `standing × eye-level × 3/4 turn × static`. AI honored the structural specification (same) over the adjective variation (different).

## Fix protocol

Before writing any plate prompts for a set, build the matrix as a table:

```
M03 White Bustier · 7 plates · diversity matrix:
  P1: standing × eye-level × power stance × static                    (commanding)
  P2: chest-up × eye-level × close framing × candid                   (luxe close)
  P3: seated × eye-level × on white cube × static                     (composed)
  P4: standing × eye-level × walking forward × in motion              (dynamic)
  P5: chest-up × eye-level × detail close × interacting (necklace)    (intimate detail)
  P6: kneeling × eye-level × wide environmental × contemplative       (vast space)
  P7: walking × behind / over-shoulder × walking AWAY × in motion     (narrative end)
```

Each row differs from every other row on 2+ axes. Then translate each row into a prompt with explicit pose vocabulary (mermaid sit / power stance / kneeling on floor / walking AWAY look-back).

## Validation log

| # | Project | Date | Technique | Outcome | Notes |
|---|---------|------|-----------|---------|-------|
| 1 | Jira Wanderlust Vol 06 (J02 cafe + J05 drive) | 2026-05-07 | Built diversity matrix as first design step before any prompt writing. 14 plates across 2 looks: each plate distinct on 2+ axes. | pass | Trin feedback after Mila session: *"รอบครอบหน่อยระวังอย่าให้ภาพมีท่าทางมุมถ่ายซ้ำกันเกินไป หลากหลายหน่อย"* — direct instruction codified as L26. Result: zero "looks the same" complaints in J02+J05 review. Original 14/14 R1 PASS, narrative variety preserved. |

## Anti-patterns

- ❌ Writing 7 prompts in a row, varying only adjectives ("confident", "elegant", "graceful")
- ❌ Assuming "different camera distance" alone is enough variety
- ❌ Building all plates around the same body pose with different framings
- ❌ Skipping the matrix and reviewing only after generation (expensive iteration)

## Cross-references

- Related lessons: L19 (narrative pose per plate beats generic framing), L24 if introduced (pose redesign for structural triggers)
- Checklist items affected: pre-submit D (phase planning) — add explicit matrix step
