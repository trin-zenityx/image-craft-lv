# L09 — Crop refs to isolate target criteria template

## What this lesson claims
When a ref must lock ONE specific element (object, pose, color),
cropping the ref so that element fills the frame gives the model an
unambiguous anchor; full-scene refs dilute the target.

## Scenario requirements
- Runner needs to replicate ONE specific element (a particular object
  silhouette, a specific pose, a specific palette accent) from a
  reference.
- The reference image is available but depicts a larger scene — Runner
  must choose to crop to isolate the target.

## Judge rubric

### Criterion 1: Target element match
The target element in the generated image matches the reference's
target element in silhouette / shape / proportion — naive comparison
at similar zoom levels.

Pass: clear match.
Partial: recognizable match but some drift.
Fail: element differs significantly.

### Criterion 2: Crop evidence in Runner log
Runner log shows that a cropped version of the reference was created
or used as primary ref.

### Overall
Pass if both. Fail if Criterion 1 fails.

## Generator: tune for your scenario
- Specify which single element is the target.
- Provide or designate the reference image.
