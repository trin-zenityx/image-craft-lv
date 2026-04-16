---
id: L02
title: Face orientation inside containers must be explicit
theme: orientation
tier: meso
status: pending
validation: 1/3
tags: [face-orientation, containers, window-mirror, explicit-direction]
origin_project: DHYANA
created: 2026-04-15
last_updated: 2026-04-15
supersedes: []
related: [L03]
---

# L02 — Face orientation inside containers must be explicit

## TL;DR

Any time a face/body is seen through a window/mirror/transparent surface, state (a) subject orientation, (b) camera position relative to subject, (c) what viewer sees through the glass. Otherwise the model defaults to "face the window", which is often wrong.

## Context

DHYANA #7 pod detail — full-body pod, sleeping face visible through face-window.

## Mistake

Wrote "the calm sleeping face of an adult human, visible through the frosted face-window". Did not specify which way the face was oriented.

## Why it happened

Human logic says "if face is visible through window, face is probably turned to window" — but that's the model's assumption, not your intent. Your intent was "supine body, face up to ceiling, visible through top-mounted porthole".

## Fix

Always state face direction explicitly: "face turned UPWARD to the ceiling, body supine, face visible through the window from above" or "face turned forward to camera at three-quarters" — never leave it unstated.

## Broader rule

Any time a face/body is seen through a window/mirror/transparent surface, specify (a) subject orientation, (b) camera position relative to subject, (c) what viewer sees through the glass.

## Validation log

| # | Project | Date       | Technique applied                             | Outcome | Notes |
|---|---------|------------|-----------------------------------------------|---------|-------|
| 1 | DHYANA  | 2026-04-15 | Explicit face-UP orientation in #7 v5         | pass    | —     |

## Cross-references

- Related lessons: L03 (opaque/transparent vocabulary)
- Checklist items affected: pre-submit B.1 (orientation of hidden/partial subjects)
