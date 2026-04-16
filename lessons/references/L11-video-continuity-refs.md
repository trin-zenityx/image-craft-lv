---
id: L11
title: Tier 1 refs must be designed for video continuity, not just standalone beauty
theme: references
tier: macro
status: pending
validation: 0/5
tags: [tier-1, video-pipeline, compatibility-matrix, per-pose]
origin_project: DHYANA
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: [L01, L05]
---

# L11 — Tier 1 refs must be designed for video continuity, not just standalone beauty

## TL;DR

Still-image refs optimized individually can conflict in video-interpolation. Design Tier 1 refs with pose/angle/bg compatibility in mind — if a video gen will use refs A and B together, A and B must be compatible.

## Context

DHYANA Tier 1 designed 13 standalone "beauty shots" — each optimized to look great individually (#01 Tenzin sitting front, #10 butterfly on extended hand from side). When used together as video refs in Seedance, pose/angle/bg conflicts caused anatomy breaks.

## Mistake

Still-image thinking applied to video-pipeline assets. Refs designed without considering how they'd interact IN MOTION within a single video gen.

## Why it happened

Still-image thinking does not account for video interpolation. Each ref was designed to stand alone and look beautiful, not to co-exist with other refs in a single motion gen.

## Fix

Tier 1 Design Rules for Video Projects:
1. **Per-pose refs:** Don't create just ONE character ref. Create refs for each pose the character will appear in (sitting, standing, walking, hand detail). Label clearly.
2. **Compatibility matrix:** Before finalizing Tier 1, draw a table: which refs will be used TOGETHER in each gen? Check pose/angle/bg compatibility for every pair.
3. **Prop refs must match character refs:** If butterfly forms from monk's hands, the butterfly ref must show hands IN THE SAME POSE as the character ref (mudra, not extended). Same camera angle. Same background depth.
4. **Ask: "Can Seedance smoothly interpolate from ref A to ref B?"** If no → redesign one or both.

## Broader rule

Tier 1 refs for video projects must pass a compatibility matrix: for every pair of refs that will be used together in a gen, verify pose/angle/bg match. Ask: "Can the video model smoothly interpolate from ref A to ref B?" If no, redesign one or both.

## Validation log

| # | Project | Date       | Technique applied                                          | Outcome | Notes                            |
|---|---------|------------|------------------------------------------------------------|---------|----------------------------------|
| 1 | DHYANA  | 2026-04-16 | Planned #14 Tenzin-standing + #15 butterfly-on-mudra       | pending | Gen 1 video anatomy break observed |

## Cross-references

- Related lessons: L01 (ref chains), L05 (back-view refs)
- Sister skill: seedance-craft-lv (video-specific discipline that uses these refs downstream)
