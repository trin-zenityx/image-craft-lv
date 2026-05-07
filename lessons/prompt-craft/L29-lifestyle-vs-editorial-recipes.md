---
id: L29
title: Lifestyle vs Editorial recipes — choose ONE entire vocabulary set; never mix
theme: prompt-craft
tier: meso
status: pending
validation: 1/3
tags: [recipe-discipline, lifestyle, editorial, vocabulary-coherence, vibe]
origin_project: jira-wanderlust-vol06
created: 2026-05-07
last_updated: 2026-05-07
supersedes: []
related: [L20, L21]
---

# L29 — Lifestyle vs Editorial recipes — don't mix

## TL;DR

There are two distinct prompt vocabulary recipes for portrait work, and they should NEVER be mixed:

| Element | **Editorial recipe** (drama) | **Lifestyle recipe** (charm) |
|---|---|---|
| **Lens** | 85-100mm telephoto | 35-50mm normal |
| **Lighting** | Dramatic spotlight, low-key, smoke, deep shadow | Natural sunlight, dappled, golden hour |
| **Face expression** | "smoldering", "magnetic", "dominant", "knowing seductive" | "charming", "warm", "gentle smile", "candid" |
| **Wardrobe vocab** | "DEEP V plunge", "fitted body-skimming", "voluminous décolletage" | "soft scoop neckline", "naturally drapes" |
| **Camera body** | Hasselblad H6D / X2D medium-format | Sony A7R IV mirrorless / Fujifilm |
| **Film stock** | Cinestill 800T tungsten / Portra dramatic | Portra 400 / Cinestill 800 dusty warm |
| **Mood vocabulary** | "cinematic dramatic", "fashion magazine cover", "editorial power" | "candid lifestyle", "Sunday morning", "sun-kissed afternoon" |
| **Aesthetic refs** | Vogue Italia · Helmut Newton · Tom Ford · Dior haute couture | Travel diary · sun-flared lifestyle · Sunday brunch · vintage road trip |

Mixing recipes (e.g., editorial lens + lifestyle expression, or dramatic spotlight + casual wardrobe) produces uncanny output that "doesn't quite work" — the visual signals contradict each other.

## When this lesson applies

- Choosing recipe at the start of a new look or photobook
- Reviewing a prompt that's been edited piecemeal — check coherence
- Differentiating models / brands that have different positioning (e.g., Mila = editorial, Jira = lifestyle)

## Mistake (avoided in practice — protective lesson)

When designing Jira's J02 Bangkok cafe + J05 coastal drive (Vol 06), the temptation was to copy the Mila/Tara editorial recipe (Hasselblad 100mm, smoldering gaze, dramatic spotlight) since that recipe had been validated. Doing so would have produced overly intense magazine-cover output that contradicted the user's "เสน่ห์ + sexy นิดๆ" intent.

Catching this BEFORE generation, swapping to the lifestyle recipe (Sony 35mm, charming gentle smile, natural dappled sunlight, Cinestill 800), produced 14/14 R1 PASS plates that matched the intended vibe.

## Fix protocol

Before writing prompts, classify the project:

```
Is this:
  (a) EDITORIAL — magazine cover, dramatic, sexy, fashion power
      → Hasselblad medium-format · 85-100mm · smoldering · DEEP V vocab · dramatic spotlight
      
  (b) LIFESTYLE — candid, sun-kissed, charming, relaxed
      → Sony A7R / Fuji · 35-50mm · gentle charming smile · soft scoop · natural sunlight
      
  (c) HYBRID — DON'T. Pick one. If hybrid feels needed, the project is two looks not one.
```

Then commit to ALL ELEMENTS of that recipe. Never mix lens from editorial with expression from lifestyle (or vice versa).

## Vocabulary swap cheatsheet

| Editorial → drop | Lifestyle → use |
|---|---|
| smoldering | charming |
| magnetic | warm |
| dominant | gentle |
| knowing seductive | gentle knowing |
| DEEP V plunge | soft scoop neckline |
| body-skimming fitted | naturally drapes |
| FULL voluminous décolletage | elegant feminine silhouette |
| cinematic dramatic | candid lifestyle |
| fashion magazine cover | Sunday morning charm |
| Vogue Italia × Helmut Newton | travel diary × afternoon walk |

| Lifestyle → drop | Editorial → use |
|---|---|
| candid | dramatic |
| Sunday morning | golden hour editorial |
| Sony 35mm | Hasselblad 100mm |
| dappled natural light | dramatic spotlight from above-left |
| charming smile | smoldering gaze |
| relaxed | confident |

## Anti-patterns

- ❌ Sony 35mm + "smoldering magnetic gaze" + "DEEP V latex" — uncanny mix
- ❌ Hasselblad 100mm + "Sunday morning charming smile" + "casual cafe" — overshoots the vibe
- ❌ Copying Mila/Tara editorial recipe to a Jira lifestyle project (or vice versa)
- ❌ Editing prompts piecemeal until they're a Frankenstein of both recipes

## Validation log

| # | Project | Date | Technique | Outcome | Notes |
|---|---------|------|-----------|---------|-------|
| 1 | Jira Wanderlust Vol 06 (J01-J05 anchor + J02+J05 photobook) | 2026-05-07 | Caught the temptation to use editorial recipe; swapped to full lifestyle recipe at design time. 5/5 anchors R1 PASS, 14/14 photobook plates R1 PASS (1 R2). Lifestyle vibe preserved. | pass | First explicit codification — the recipe contrast with prior Mila/Tara editorial sessions made the distinction visible. Trin's "เสน่ห์ + sexy นิดๆ" instruction was the design constraint. |

## Cross-references

- Related lessons: L20 (camera body + film stock specificity); L21 (designer / aesthetic reference choice)
- Checklist items affected: pre-submit (entire) — add recipe-classification step before any vocabulary writing
