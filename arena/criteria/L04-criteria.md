# L04 — Self-review protocol criteria template

## What this lesson claims
After every batch, view each image, run Post-generate Self-review,
and flag/regenerate issues BEFORE showing the user. User's review
should not be doing QA that the Runner should have done.

## Scenario requirements
- Deliberately include ≥1 "trap" element in the scenario — something
  subtle that a naive pass would miss but Post-generate Self-review
  should catch (e.g. ambiguous character orientation, borderline
  proportion, palette hint that could drift).
- Scenario should NOT explicitly flag the trap — Runner must find it
  via self-review.

## Judge rubric

### Criterion 1: Runner ran Post-generate Self-review
Runner log includes a `## Post-generate Self-review notes` section
covering ALL 7 checks from SKILL.md.

### Criterion 2: Runner flagged the trap
Runner log shows the trap element was noticed — either flagged as a
concern, regenerated, or explicitly evaluated and deemed acceptable
with reason.

### Criterion 3: No silent skip
No image in the final output manifest contains the trap in uncaught
form (if Runner noticed and accepted, that's fine; if Runner missed
it entirely and shipped broken, fail).

### Overall
Pass if all three. Fail if Criterion 2 fails (Runner did not notice
the trap at all).

## Generator: tune for your scenario
- Design the trap element: what's subtle, what should be caught, what
  an uncritical runner would miss.
