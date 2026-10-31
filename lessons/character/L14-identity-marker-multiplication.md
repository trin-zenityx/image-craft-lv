---
id: L14
title: Mentioning a singular identity marker (mole, beauty mark, scar, tattoo) in prompt causes AI to multiply it across the face
theme: character
added_at_lv: 2.5
tags: [identity, beauty-mark, mole, prompt-engineering, real-person, drift]
created: 2026-05-01
last_updated: 2026-05-01
supersedes: []
related: [L01, L13]
---

# L14 — Mentioning a singular identity marker in prompt causes AI to multiply it

## TL;DR

When the subject has a distinctive identity marker (mole, beauty mark, scar, freckle, tattoo, birthmark) and you mention it in the prompt to "lock identity", the AI tends to interpret it as a **feature category** rather than a single instance, and multiplies it across the face/body. **Drop the marker mention entirely** — let the reference image carry it naturally.

## Context

Pupae's master photo shows a single small natural beauty mark on her left cheek (near jawline) — a clear identity marker.

## Mistake

Built a structural face anchor for character sheet plates that explicitly stated: `"naturally medium-fuller lips with subtle Cupid's bow, small natural beauty mark on left cheek"` — to lock the marker in place across plates.

## What happened

Rather than placing a single beauty mark on the left cheek as instructed, the AI interpreted "natural beauty mark" as a category of feature and rendered **multiple visible moles/beauty marks scattered across the face** — on cheeks, forehead, chin, neck. This made the close-up plates look like a different person with skin condition variation, not the master subject who has exactly one small mark.

Affected plates: Pupae L1-cafe-sweetie P2 + P3 (cute close-ups had multiple visible moles).

## Why it happened

The AI's understanding of "natural beauty mark" appears to be: this person's face HAS beauty marks → render some. It does not consistently render exactly one in exactly the position described. Once the category is invoked, the model expresses it generously.

The reference image, on the other hand, shows exactly one mark in exactly one position. The AI is much better at copying what's IN the reference visually than at executing positional descriptions.

## Fix

**Drop the marker mention from the prompt entirely.** Trust the reference image to carry the marker. The AI will render the marker because it sees it in the reference, but won't multiply it because no prompt directive says "this person has beauty marks."

For Pupae fix: removed `"small natural beauty mark on left cheek"` from face anchor. Result: regen showed exactly one beauty mark in correct position (matching ref) — no multiplication.

## Broader rule

For singular identity markers (mole, scar, birthmark, tattoo, etc.):
- **DON'T**: describe them in prompt as "single small X on left cheek"
- **DO**: ensure the reference image clearly shows the marker, and let the AI copy it visually
- The exception: very prominent markers that are key to the brand/character (e.g., a famous singer's defining facial mark) — for these, you may need to describe AND use ref, but accept some multiplication risk and audit carefully.

This is counter-intuitive: more specification → worse output. The pattern aligns with how the AI handles features it categorizes (skin tone, hair color, eye shape) vs what it copies from refs (specific arrangements, exact placements).

## Cross-references

- Related lessons: L01 (reference chains beat text-only); filter vocab → skill `filter-craft-lv` (migrated from L13)
- Memory file: `feedback_realperson_identity_drift.md` (separate angle on identity preservation for real-person AI portraits)
- Checklist items affected: pre-submit C (reference strategy)

## Edge cases

- **Multiple markers naturally**: if subject has multiple moles/freckles naturally, then mentioning "freckles across cheeks and nose bridge as in references" is fine — the multiplication is desired.
- **Very faint marker**: if marker barely visible in ref, AI may miss it entirely. Solution: use a tighter crop ref (per L09) showing the marker clearly, NOT prompt description.
- **Tattoo with specific design**: prompt vocabulary may help with placement BUT the design itself must come from ref — text descriptions of tattoo art always drift to generic.
