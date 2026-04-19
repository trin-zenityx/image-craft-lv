# Criteria — 2026-04-17-L09-S03 (The Penacho Trial)

## What this scenario tests

L09 claims: cropping a reference image to isolate a single target element gives the model an unambiguous anchor; full-scene references dilute the target and cause the model to default to a generic version.

In this scenario, the target element is the **Penacho** — an asymmetric ceremonial feathered headdress with a left-dominant fan and rightward crown lean. The model's text prior defaults to a symmetric centered fan. Only the visual anchor can communicate the asymmetry.

## Observable dimensions

Four dimensions are pre-registered. Each is scored independently for 3A and 3B by comparing against the crop reference (`shot1-crop-headdress.png`).

| Dim | Feature | Measured how |
|-----|---------|--------------|
| D1 | Left-fan dominance | Is the left side of the fan visibly taller / wider than the right? Yes/No |
| D2 | Crown lean direction | Does the headdress apex lean rightward from vertical? Yes/No |
| D3 | Quetzal feather cascade | Do the long tail feathers curve leftward from apex? Yes/No |
| D4 | Overall silhouette fidelity | Naive viewer test: does the headdress read as the same specific headdress as the crop? Yes/No/Partial |

For D4, "Partial" counts as a half-win for neither side (tie).

---

## Criterion 1: Target element silhouette match (3A)

**What is judged:** Does Shot 3A (crop-ref variant) reproduce the headdress silhouette from the crop reference?

- **Pass:** 3A matches on ≥3 of 4 dimensions (D1–D4).
- **Partial:** 3A matches on exactly 2 of 4 dimensions.
- **Fail:** 3A matches on ≤1 of 4 dimensions.

**Threshold reasoning:** The headdress has 4 observable asymmetric features. If crop-ref usage works, the model should land 3 or 4 of these correctly. If only 1–2 are correct, the crop did not effectively anchor the silhouette.

---

## Criterion 2: Causal control validity

**What is judged:** Was the A/B control clean? Was Criterion 2 the ONLY variable?

- **Pass:** Runner log confirms (a) Shot 3A used the cropped headdress image as primary reference, (b) Shot 3B used the full Shot 1 image as primary reference, (c) the text prompt was character-for-character identical for both, (d) no other generation parameters differed (same seed range, same model, same resolution, same step count if applicable).
- **Fail:** Any of the above conditions were violated. A Fail here invalidates the entire trial regardless of visual results.

**What counts as a violation:** Giving 3A a more descriptive prompt than 3B; using different models; generating at different resolutions; adding negative prompts to only one side.

---

## Criterion 3: Comparative advantage — the PASS gate

**What is judged:** Does 3A beat 3B on ≥3 of 4 dimensions, including D4 (overall fidelity)?

For each dimension, compare 3A vs 3B against the crop reference:
- 3A wins a dimension if it matches the reference and 3B does not.
- 3B wins a dimension if it matches the reference and 3A does not.
- Tie: both match, both fail, or D4 is Partial for either.

**Scoring table:**

| 3A wins | Includes D4 | Verdict |
|---------|-------------|---------|
| ≥3 | Yes | **PASS** |
| ≥3 | No | **PARTIAL** (causal claim holds but overall fidelity not demonstrated) |
| 2 | — | **PARTIAL** |
| ≤1 | — | **FAIL** |

**Threshold reasoning:** The scenario was designed so that D1, D2, and D3 are all mechanically caused by the same underlying silhouette asymmetry — if the crop works, the model should capture all three directional features simultaneously. D4 should follow automatically if D1–D3 are met. Getting ≥3 therefore tests whether the crop advantage is robust and not a lucky partial match. A 2/4 result (matching S02's Partial) would indicate the asymmetric headdress was not distinctive enough in the crop, or that competing text priors were too strong on some dimensions.

---

## Overall verdict logic

1. **Criterion 2 fails** → void or invalid (escalate, do not score as Pass/Partial/Fail).
2. **Criterion 3: 3A wins ≥3/4 incl. D4** → **PASS** (promotes L09 from pending to validated).
3. **Criterion 3: 3A wins ≥3/4 excl. D4, or 3A wins exactly 2/4** → **PARTIAL** (causal structure confirmed, full pass not achieved).
4. **Criterion 3: 3A wins ≤1/4** → **FAIL** (lesson not supported by this evidence).
5. Criterion 1 is informative but not the gate — what matters for lesson validation is Criterion 3 (3A beats 3B), not merely that 3A was good in absolute terms.

---

## Why this scenario should achieve a PASS (not just Partial)

S02 got Partial (2/4) because two dimensions — guard shape (circular) and void count (hitsu-ana openings) — are structural features that any dragon tsuba would have regardless of reference quality. Those were ties by design, not losses. The S02 lesson: tie dimensions inflated the denominator without helping 3A win.

S03 is structured to avoid this:

- **All 4 dimensions are asymmetric / direction-specific** (left vs right, lean vs straight, curve direction). None of them are features that "any headdress would have" — a symmetric headdress would lose D1, D2, and D3 simultaneously. There is no equivalent of "both are circular."
- **The model's text prior is specifically wrong**: "Aztec headdress" defaults to symmetric. This means 3B (full-ref) is more likely to produce the wrong version than 3A (crop-ref), giving 3A a genuine advantage across multiple dimensions.
- **The target element (penacho) is maximally distinctive in silhouette**: the left-lean is not subtle. It is an absolute directional asymmetry a naive viewer would flag immediately.

Expected outcome: 3A wins D1, D2, D3 (all three directional features) and D4 (overall fidelity follows). 3B, using the full busy scene as ref and the model's symmetric text prior, defaults to a centered fan and loses D1–D4. Result: 3A wins 4/4, including D4 → PASS.
