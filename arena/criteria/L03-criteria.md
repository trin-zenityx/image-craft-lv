# L03 — Opaque vs transparent vocabulary criteria template

## What this lesson claims
Design-language facts (e.g. opaque vs transparent surfaces) established
in one shot of a set must be stated the same way in every related shot;
vague wording = model re-decides per gen.

## Scenario requirements
- Multi-shot set with at least one object/surface that has two possible
  interpretations (opaque/transparent, rough/smooth, matte/glossy, etc.)
- ≥3 shots feature the same object across them.

## Judge rubric

### Criterion 1: Surface consistency across shots
Pass if: in ALL shots featuring the object, the surface treatment
matches (e.g. opaque body looks opaque in every shot; translucent
material looks translucent in every shot).
Fail if: any shot shows a different surface treatment.

### Criterion 2: Vocabulary locked in Runner log
Runner log shows consistent phrasing for the surface across all
prompts that reference the object.

### Overall
Pass if both. Fail if either fails.

## Generator: tune for your scenario
- Specify which object, which two interpretations, and which shots
  feature it.
