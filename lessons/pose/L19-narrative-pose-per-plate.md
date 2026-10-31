---
id: L19
title: Narrative pose per plate beats generic framing templates for variety
theme: pose
added_at_lv: 2.7
tags: [pose, narrative, multi-plate, variety, framing, prompt-engineering]
created: 2026-05-05
last_updated: 2026-05-05
supersedes: []
related: [L01, L20, L23]
---

# L19 — Narrative pose per plate beats generic framing templates for variety

## TL;DR

Generic framing templates ("P1 Hero full-body / P2 Beauty close-up / P3 Profile / P4 Lifestyle") instruct the AI **what to frame** but not **what is happening**. With identical refs and only template variation across plates, the AI converges on the model's default pose and the set looks mono-angle.

The fix: **write each plate as a tiny narrative**. Every plate prompt must contain:

1. **Action verb** ("leaning", "reaching", "tilting back", "bracing")
2. **Concrete prop or surface** ("velvet armchair", "marble vanity edge", "sheer curtain")
3. **Sub-location** ("by the window", "at the dressing table corner", "across the chaise")
4. **Body interaction** ("shoulder pressed against", "knee drawn up", "fingertips trailing")
5. **Camera framing** (angle + lens + crop)

Without all five, the AI fills in the blanks with its default and you get the same shot five times.

## Context

Alisa Glamour Photobook v1 was prompted with a generic "Hero / Beauty / Profile / Lifestyle / Detail" plate template. All plates shared identical refs and identical body / wardrobe directives, with only the framing label varying. Result: **mono-angle output** — the same standing-front-facing pose with minor zoom variation, despite four ostensibly different framings.

After rewriting v2-v4 with narrative-pose-per-plate prompts, the same set produced genuinely distinct compositions. Cross-validation against Jira Set A/B/C and Mila Set B prompt archives confirmed both projects use the narrative-pose pattern (action verb + concrete prop + body interaction in every plate).

## Mistake

Using template labels ("P1 Hero", "P2 Beauty close-up") as if they were complete instructions. The AI reads "Hero full-body shot" and converges on a generic catalog pose; it reads "Beauty close-up" and converges on a generic head-and-shoulders. With identical refs, the same default pose threads through every plate.

## Why it happened

The AI's prior on framing labels is *very* generic — there's no canonical "Hero pose" the model has learned to vary. Without an action verb to anchor a different motion, and without a concrete prop / surface to anchor a different physical situation, every plate looks like the model's average of "person posed for camera."

Refs lock identity and wardrobe but **do not lock pose variation across plates**. The pose has to be specified per-plate, in narrative form.

## Fix

Rewrite every plate prompt to include all five narrative elements:

```
P1 [headline] —
  Action: [verb-driven motion or contact, e.g. "leaning back against the headboard"]
  Prop / surface: [concrete object the body is interacting with]
  Sub-location: [specific zone of the room/scene, not just "in the bedroom"]
  Body interaction: [where weight is, what is touching what]
  Camera: [angle + lens + crop, e.g. "low 3/4 view, 50mm, tight half-body"]
```

The five elements force the AI off its default pose for each plate.

Counter-pattern to avoid: "P1 Hero full-body, P2 Beauty close-up, P3 Profile, P4 Lifestyle" — every label invites a default.

## Broader rule

For any multi-plate set where pose variety is the goal, write each plate as a narrative micro-scene with action, prop, location, body interaction, and camera framing. Generic framing labels are insufficient instructions for pose variation.

This generalizes beyond glamour / photobook work: ad shoots, character sheets (when the goal is varied poses, not identity locking), and any storyboard where the figure must do something different in each frame.

## Cross-references

- Related lessons: L01 (ref chains lock identity, but don't lock pose — L19 fills the gap), L20 (camera-body specificity pairs with narrative pose), L23 (face expression as separate block — pulls expression out of the pose narrative)
- Checklist items affected: pre-submit B (ambiguity sweep — pose is one of the most under-specified elements), D (phase planning — narrative pose per plate is part of the per-plate prompt design)
