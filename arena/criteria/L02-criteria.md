# L02 — Face orientation explicitness criteria template

## What this lesson claims
For faces/bodies seen through windows/containers/mirrors, orientation
must be stated explicitly (subject orientation, camera angle, what
viewer sees through glass). Models default to "face the glass"
otherwise.

## Scenario requirements
- At least 3 shots showing a face/body through some barrier (window,
  pod, mirror, one-way glass, etc.).
- Each shot has a specified orientation that is NOT the default
  "looking toward camera through glass".

## Judge rubric

### Criterion 1: Orientation compliance per shot
For each shot: the face/body orientation in the rendered image
matches what was specified (e.g. "face upward to ceiling" means the
face points up, not at the camera).

Pass: ≥ 4 of 5 shots comply (or 100% if fewer than 5 shots).
Fail: ≤ 3 of 5 comply.

### Criterion 2: Orientation stated in prompts
Runner log shows explicit orientation language per shot, not just
"face visible through the window".

### Overall
Pass if both. Fail if Criterion 1 fails.

## Generator: tune for your scenario
- Specify the barrier type(s), the shots, and the non-default
  orientation for each.
