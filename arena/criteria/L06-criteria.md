# L06 — Distinguishable characters criteria template

## What this lesson claims
When two characters share context (same shot, similar roles), immutable
distinguishing features must be specified for both; otherwise the
model renders them as generic near-duplicates.

## Scenario requirements
- ≥2 named characters who appear together or in similar shots.
- Characters should be in visually-similar contexts (same lighting,
  clothing genre, setting) — so distinguishability depends on
  features specified by Runner, not context.

### Judge rubric

### Criterion 1: Cross-character distinguishability
In every shot featuring ≥2 of the named characters, a naive viewer can
identify which is which based on visible immutable features alone
(hair, facial structure, age, ethnicity).

Pass: all shots distinguishable.
Partial: 1 shot borderline, rest clear (and shot count ≥ 4).
Fail: any shot where characters could be mistaken for each other.

### Criterion 2: Feature specification in Runner log
Runner log shows explicit feature differentiation per character in
prompts (not "two people" but "man A with grey hair vs woman B with
dark hair"-style specifics).

### Overall
Pass if both. Fail if Criterion 1 fails.

## Generator: tune for your scenario
- Specify character names and 2-3 axes on which they must read different.
