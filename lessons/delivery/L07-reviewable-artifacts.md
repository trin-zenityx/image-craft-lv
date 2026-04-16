---
id: L07
title: Deliverables must be packaged as reviewable artifacts, not raw file dumps
theme: delivery
tier: macro
status: pending
validation: 1/3
tags: [delivery, storyboard, html, reviewable-artifact, packaging]
origin_project: DHYANA
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: [L04]
---

# L07 — Deliverables must be packaged as reviewable artifacts, not raw file dumps

## TL;DR

For any batch >3 images, produce ONE reviewable artifact (HTML storyboard, PDF, Markdown with embedded images) that labels each image and maps it to the story. Never deliver as a raw file dump.

## Context

DHYANA Tier 2 — 22 images generated with file names like `g15b.jpeg`, `g19a.jpeg`. User was expected to open each file individually in a folder, match it mentally to which shot it represents in the story, and decide if it was correct.

## Mistake

Delivered the batch as "22 files in a folder, here are the paths". No visual summary. No Thai labels. No shot→story mapping. Placed 100% of the review-assembly cost on the user.

## Why it happened

Treated "generated and organized" as "delivered". Assumed filenames were self-explanatory. Did not consider the user's actual workflow for reviewing a batch.

## Fix

For any batch of >3 images/artifacts, package deliverables as a *reviewable artifact* — an HTML storyboard, PDF, Markdown with embedded images, or similar — that presents each image INLINE with: (a) clear label (Act/Scene/Shot), (b) short Thai/user-language description of what it shows, (c) narrative context (where in the story this shot falls), (d) pair grouping for related shots. User opens ONE file, sees everything in order, can review efficiently.

## Broader rule

"Delivered" means "user can review without extra assembly work on their part". Raw file dumps are not deliverables. If you generate N images, produce the reviewable artifact that shows all N at once, labeled and contextualized.

## Validation log

| # | Project | Date       | Technique applied                                       | Outcome | Notes                             |
|---|---------|------------|---------------------------------------------------------|---------|-----------------------------------|
| 1 | DHYANA  | 2026-04-16 | Tier 1+2 HTML storyboard delivered via browser open     | pass    | Confirmed CC preview mismatch     |

## Cross-references

- Related lessons: L04 (self-review)
- Checklist items affected: none (delivery phase, post-checklist)

## Additional rule

When producing HTML for user review, default to `open <path>` after write — don't rely on Claude Code preview panel.
