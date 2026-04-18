# L11 — Video-continuity refs criteria template

## What this lesson claims
Tier-1 reference images that will feed a video generation must be
designed for compatibility (pose, angle, bg) — not just standalone
beauty. Per-pose refs, compatibility matrix required.

## Scenario requirements
- The scenario simulates preparing Tier-1 refs for a downstream video
  pipeline (even if the video itself is not generated in arena).
- Runner must produce ≥3 refs that will be used TOGETHER in a
  hypothetical video gen (stated in scenario).
- Scenario specifies the implied video motion (e.g. "character raises
  hand, butterfly forms").

## Judge rubric

### Criterion 1: Per-pose refs present
Runner produced distinct refs for each pose the character appears in
during the implied motion.

### Criterion 2: Pair compatibility
For every pair of refs that will be used together: pose/angle/bg are
compatible enough that smooth interpolation is plausible.
Pass: all pairs compatible.
Partial: one borderline pair, rest clear.
Fail: any pair incompatible.

### Criterion 3: Compatibility matrix documented
Runner log explicitly lists which refs pair with which and notes
compatibility.

### Overall
Pass if all three. Fail if Criterion 2 fails.

## Generator: tune for your scenario
- Specify the implied video motion and the minimum refs needed.
