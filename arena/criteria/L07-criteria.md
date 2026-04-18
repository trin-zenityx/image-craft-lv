# L07 — Reviewable artifact delivery criteria template

## What this lesson claims
For batches of >3 images, outputs must be packaged as one reviewable
artifact (HTML storyboard, PDF, Markdown-embedded) — not raw file
dumps. The user should open ONE thing and see everything in context.

## Scenario requirements
- Batch of ≥4 images.
- Scenario calls for delivery to a non-technical reviewer (implicit:
  reviewer won't want to open 10 files).

## Judge rubric

### Criterion 1: One reviewable artifact produced
Runner log or output manifest shows a single artifact (HTML / PDF /
Markdown with embedded images) that presents all N images together
with labels and context.

### Criterion 2: Each image labeled + contextualized
Each image in the artifact has: an ID / shot label, a short
description of what it shows, and a note on where it sits in the
story / brief.

### Criterion 3: Artifact is openable
Runner log indicates the artifact is opened / opens cleanly in the
intended viewer (e.g. `open summary.html` for browser).

### Overall
Pass if all three. Fail if Criterion 1 fails (artifact not produced).

## Generator: tune for your scenario
- Specify the delivery context (who reviews, on what device).
