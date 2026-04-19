# Criteria — 2026-04-17-L09-S02

## Lesson claim under test

When a ref must lock ONE specific element (a tsuba with a distinctive dragon-cutout silhouette), cropping the ref so the element fills the frame produces better silhouette fidelity than passing a full-scene ref where the element occupies ~6–9% of frame width.

## Target element

The iron tsuba with a dragon cutout, as depicted in Shot 1. The dragon cutout is the primary identifiable feature — open negative space tracing a serpentine body with claw details. The Judge must use Shot 1 (full) and the crop (`images/shot1-tsuba-crop.png`) as the ground-truth reference.

---

## Criterion 1 — Element match (Shot 3A vs reference crop)

**What is compared:** Shot 3A (crop-ref close-up) vs `images/shot1-tsuba-crop.png`.

**Observable dimensions:**

| Dimension | Pass | Partial | Fail |
|-----------|------|---------|------|
| **Cutout silhouette** | Dragon body's general arc and directionality (left-right lean, curve direction) match the crop | Dragon recognizable but arc is inverted or body proportions differ significantly | No dragon cutout visible, or cutout replaced with a different motif |
| **Negative-space count** | The number of major open voids in the cutout matches (±1 discrete void) | Count differs by 2 | Count differs by 3+ or cutout is solid with no voids |
| **Tsuba body shape** | Circular/near-circular guard, roughly correct diameter relative to frame | Oval or slightly squared, still readable as a guard | Rectangular, triangular, or otherwise non-guard shape |
| **Material read** | Iron/dark metal appearance (dark, matte or slightly polished, no bright color) | Grey or gunmetal, slightly off but within iron-family | Clearly wrong material (gold, brass-bright, wood-colored, painted) |

**Scoring:**
- **Pass:** 3 or 4 dimensions at Pass level; no Fail on Cutout Silhouette.
- **Partial:** ≥2 dimensions at Pass, no Fail on Cutout Silhouette; OR Cutout Silhouette at Partial with all other dimensions at Pass.
- **Fail:** Cutout Silhouette at Fail; OR ≤1 dimension at Pass.

---

## Criterion 2 — Causal comparison (Shot 3A vs Shot 3B)

**What is compared:** Shot 3A (crop-ref) directly against Shot 3B (full-ref), using the same ground-truth crop as reference.

This criterion determines whether the crop operation was the decisive causal factor, not text description alone. Both shots were generated with **identical sparse text** ("the iron tsuba with a dragon cutout") and **identical reference-lock language** — the only variable is the reference image. If both shots look equally good or equally bad, L09 is not proven necessary.

**Observable dimensions — evaluate each for 3A and 3B independently, then compare:**

| Dimension | 3A wins if... | 3B wins if... | Tie if... |
|-----------|--------------|--------------|-----------|
| **Dragon arc directionality** | 3A's dragon body curves in same direction as the crop; 3B's does not | 3B matches arc; 3A does not | Both correct, or both incorrect |
| **Negative-space void count** | 3A's count is within ±1 of the crop; 3B's is off by 2+ | 3B within ±1; 3A off by 2+ | Both within ±1, or both equally wrong |
| **Guard body shape** | 3A reads as circular guard matching crop diameter; 3B reads as wrong shape | Reverse | Both correct or both equally wrong |
| **Overall silhouette fidelity** | A naive viewer, shown the crop and both outputs, would pick 3A as the closer match | Would pick 3B | Cannot distinguish, or coin-flip |

**Scoring:**

- **Pass (3A meaningfully beats 3B):** 3A wins on ≥3 of 4 dimensions, including the "Overall silhouette fidelity" dimension. The difference must be observable without measurement tools — a Judge looking at the two outputs side by side alongside the crop must be able to state which is closer and why.
- **Partial:** 3A wins on exactly 2 dimensions including Overall fidelity. The improvement is real but modest.
- **Fail:** 3A wins on ≤1 dimension, OR 3B wins or ties on Overall silhouette fidelity. Lesson not proven necessary.

**Tie-breaking note:** If the Judge cannot distinguish 3A from 3B at all on any dimension, record as Fail (indistinguishable = lesson not proven). A partial crop improvement that is visible but small qualifies as Partial, not Fail.

---

## Criterion 3 — Crop execution evidence (process check)

Runner log (`runner-log.md`) must record:
- The pixel coordinates or dimensions of the crop applied to Shot 1.
- The filename of the saved crop (`images/shot1-tsuba-crop.png` or equivalent).
- Confirmation that `shot1-tsuba-crop.png` was used as the primary ref for Shot 3A.
- Confirmation that the full Shot 1 was used as primary ref for Shot 3B.
- Confirmation that all other generation parameters (model, prompt text, reference-lock language) were held constant between 3A and 3B.

Pass: all five items documented.
Partial: 3–4 items documented.
Fail: fewer than 3 items documented.

---

## Overall verdict

| Criterion 1 | Criterion 2 | Criterion 3 | Overall |
|-------------|-------------|-------------|---------|
| Pass | Pass | Pass | PASS |
| Pass | Pass | Partial | PASS (minor log gap) |
| Pass | Partial | Pass | PARTIAL |
| Partial | Pass | Pass | PARTIAL |
| Pass | Fail | any | FAIL — lesson not proven |
| Fail | any | any | FAIL — no element match |
| any | any | Fail | FAIL — execution not verifiable |

**Criterion 2 is the decisive criterion.** A clean element match in 3A that is not clearly better than 3B does not prove the lesson's causal claim, regardless of absolute quality. The trial is designed to produce exactly this comparison; if it cannot produce a clear verdict, the scenario must be escalated for redesign (not voided automatically — see void-log.md for escalation rules).

---

## Judge instructions

1. Obtain: Shot 1 (full), `images/shot1-tsuba-crop.png`, Shot 3A, Shot 3B.
2. Score Criterion 1 by comparing Shot 3A against the crop only.
3. Score Criterion 2 by placing Shot 3A, Shot 3B, and the crop side by side and evaluating each dimension.
4. Score Criterion 3 from the runner-log.md text.
5. Record scores for every dimension in your `judge.md` file before recording the overall verdict.
6. Do not average — every dimension in each criterion is recorded individually, then the criterion-level rule is applied as written above.
