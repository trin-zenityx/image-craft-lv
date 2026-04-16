---
id: L05
title: Back-view character refs cannot lock face identity
theme: references
tier: meso
status: pending
validation: 0/3
tags: [character, per-view-anchor, face-identity, wardrobe]
origin_project: DHYANA
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: [L01, L06, L09]
---

# L05 — Back-view character refs cannot lock face identity

## TL;DR

A back-view ref teaches wardrobe and pose but cannot lock face. Each view (front, profile, back, face-in-container) needs its own anchor.

## Context

DHYANA Tier 2 five shots (g15b, g19a, g19b, g20a, g20b) show the mother's face sleeping inside a pod. All five used `04_mother_back.jpeg` as character reference — but #04 is a BACK-view with hood up, face invisible. Model had no face to lock identity against.

## Mistake

Assumed a character ref image is universally usable for identity locking. Didn't check whether the ref actually shows what the new shot needs to match.

## Why it happened

Reference-chain thinking at the level of "which character" rather than "which feature of the character". Mother back-view refs wardrobe (indigo wool) but not face. When a future shot needs FACE consistency, a back-view ref is useless for that dimension.

## Fix

For any character who will appear in multiple views (back, profile, front, in container), generate dedicated anchor images per view needed: one front/face anchor, one profile anchor, one back anchor. Ref the RIGHT anchor for each shot based on what feature must be locked. If only back-view ref exists and a future shot needs face, generate the face anchor BEFORE generating that shot.

## Broader rule

When planning ref chain, ask "what does this shot need to match — face? wardrobe? pose? location? light?" Then pick refs that actually contain that feature. Back-view refs cannot teach face; macro-light refs cannot teach composition.

## Validation log

| # | Project | Date       | Technique applied                                           | Outcome  | Notes                       |
|---|---------|------------|-------------------------------------------------------------|----------|-----------------------------|
| 1 | DHYANA  | 2026-04-16 | Identified in Tier 2 g20b failure; face anchor planned      | pending  | Anchor not yet created      |

## Cross-references

- Related lessons: L01 (ref chains), L06 (distinguishable characters), L09 (crop refs)
- Checklist items affected: pre-submit C.1 (most relevant refs)
