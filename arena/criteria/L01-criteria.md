# L01 — Reference chains criteria template

## What this lesson claims
For multi-shot sets, a ref-chain dependency graph (master anchors
first, secondary ref master, tertiary ref both) produces visual
consistency that text-only prompting cannot.

## Scenario requirements (Generator enforces)
- Multi-shot set (≥3 shots) with ≥1 recurring element (character,
  location, or prop).
- At least one pair of shots where the recurring element appears from
  different angles / moods / distances.
- The Runner's blinded instruction should not mention "use refs" —
  Runner must choose to use refs because the skill tells them to.

## Judge rubric

### Criterion 1: Recurring-element consistency
For each pair of shots featuring the same recurring element:
- Pass if the element reads as clearly the same character/location/prop
  to a naive viewer.
- Fail if the element drifts (face looks different, architecture looks
  different, prop changes design).
- Partial if 1 pair drifts but ≥75% of pairs are consistent.

### Criterion 2: Ref-chain evidence in Runner log
Runner log shows:
- Master anchor generated first, without refs.
- Secondary shots reference the master.
- Pass / fail clear.

### Overall
Pass if both criteria pass. Fail if either fails. Partial if 1 partial.

## Generator: tune for your scenario
- Fill in specific shot-pair expectations (e.g. "shots 1 & 3 must show
  character A; shots 2 & 4 must show location B").
- Decide the specific recurring element(s).
- Adjust partial threshold if shot count is small.
