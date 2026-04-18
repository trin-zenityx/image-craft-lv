# L10 — Prominence floor / diminishing returns criteria template

## What this lesson claims
When a regen improves a metric less than the previous attempt did,
Runner is approaching the model's floor. Stop prompt-tuning; accept
or switch tools.

## Scenario requirements
- Scenario includes a requirement that the model will STRUGGLE with
  (tiny element prominence, unusual proportion, anti-default detail)
  so diminishing returns are likely.
- Scenario should have a concrete target (e.g. "face window = 15% of
  pod length") and a model-plausible floor (e.g. ~17–20%).

## Judge rubric

### Criterion 1: Runner tracked the metric across regens
Runner log shows numeric tracking of the target metric across regen
attempts.

### Criterion 2: Runner stopped at diminishing returns
Runner attempted ≤ 5 regens and stopped when the improvement curve
flattened (explicitly noted in log).

### Criterion 3: Runner honestly reported the final gap
If Runner did not hit the target exactly, the final report clearly
states the achieved value and how it compares to target (no silent
acceptance of miss).

### Overall
Pass if all three. Fail if Criterion 2 fails (Runner burned >5 regens
without acknowledging the floor).

## Generator: tune for your scenario
- Design the hard target and the expected floor.
- Make the request specific enough that a numeric metric exists.
