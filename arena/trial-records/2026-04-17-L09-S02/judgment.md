# Judgment — 2026-04-17-L09-S02

## Per-criterion verdicts

---

### Criterion 1 — Element match (Shot 3A vs reference crop)

**Criterion verbatim:** Shot 3A (crop-ref close-up) must match `images/shot1-tsuba-crop.png` across four observable dimensions: Cutout Silhouette, Negative-space count, Tsuba body shape, and Material read.

**Relevant images:** `images/shot3a.jpeg`, `images/shot1-tsuba-crop.png`, `images/shot1.jpeg`

#### Dimension scoring

| Dimension | Score | Evidence |
|-----------|-------|----------|
| **Cutout silhouette** | Pass | Shot 3A shows a dragon body with head at upper-left, serpentine body arcing diagonally toward lower-right — matching the crop reference's directionality. The general arc and left-to-right lean of the dragon in 3A corresponds to the crop. The reference crop shows the tsuba at a side/tilted angle which makes direct silhouette comparison approximate, but the fundamental arc direction (head left, tail right, body curving clockwise through the guard interior) is preserved in 3A. |
| **Negative-space count** | Pass | The crop reference shows two prominent central hitsu-ana openings plus surrounding void spaces from the dragon cutout. Shot 3A shows two central hitsu-ana (the elongated oval pair near center) plus multiple secondary voids tracing the dragon body — void count is within ±1 of major voids in the reference. |
| **Tsuba body shape** | Pass | Shot 3A shows a clearly circular guard with correct diameter proportional to frame. The circular rim is complete and round. Matches the crop reference's circular guard shape. |
| **Material read** | Pass | Shot 3A shows aged iron — very dark, near-black, with visible iron-oxide texture and slightly matte surface. Correct iron-family appearance. No bright color, no gold or brass tones. |

**Criterion 1 Verdict: PASS**

All 4 dimensions at Pass level. Cutout Silhouette passes (no Fail). Passes by "3 or 4 dimensions at Pass level; no Fail on Cutout Silhouette" rule.

---

### Criterion 2 — Causal comparison (Shot 3A vs Shot 3B)

**Criterion verbatim:** Shot 3A (crop-ref) must show measurably better dragon-cutout silhouette fidelity than Shot 3B (full-ref), evaluated against the ground-truth crop across four dimensions. Both shots used identical text prompts and identical reference-lock language; the only variable is the reference image.

**Relevant images:** `images/shot3a.jpeg`, `images/shot3b.jpeg`, `images/shot1-tsuba-crop.png`

#### Reference ground truth orientation (crop)

The crop (`shot1-tsuba-crop.png`) shows: dragon head at LEFT side of the guard, body sweeping rightward in a single flowing arc that curves down and to the right (clockwise diagonal), tail at lower-right. Two central hitsu-ana openings. Circular guard. The dragon body traces a left-leaning diagonal — not a symmetric wrap.

#### 4-Dimension A/B Table

| Dimension | 3A | 3B | Winner |
|-----------|----|----|--------|
| **Dragon arc directionality** | Head at upper-left, body arcs diagonally toward lower-right — matches the crop's left-to-right diagonal lean and clockwise sweep direction | Head at upper-center/top, body wraps more symmetrically around the central openings in a near-horizontal arrangement — arc direction departs from the crop's strong diagonal lean | **3A wins** |
| **Negative-space void count** | Two clear central hitsu-ana openings plus multiple secondary voids from the dragon cutout body — count within ±1 of reference | Two central hitsu-ana openings plus surrounding cutout voids — also within ±1 of reference | **Tie** — both within ±1 of major void count |
| **Guard body shape** | Clearly circular, complete rim, correct proportions relative to frame | Clearly circular, complete rim, correct proportions — equally reads as circular guard | **Tie** — both correctly circular |
| **Overall silhouette fidelity** | A naive viewer shown the crop alongside 3A and 3B would identify 3A as the closer match: the diagonal arc placement of the dragon (head left, diagonal body sweep toward lower-right) directly echoes the crop's most distinctive compositional feature — the asymmetric single-arc layout. 3B's more symmetric top-to-bottom wrap around the hitsu-ana is a plausible dragon tsuba but does not reproduce the crop's specific silhouette layout. | 3B shows a coherent dragon tsuba but the head-top / symmetric-body configuration diverges from the crop's pronounced left-leading diagonal arc. | **3A wins** |

**Summary: 3A wins on 2 dimensions (Arc Directionality, Overall Silhouette Fidelity); Tie on 2 dimensions (Void Count, Guard Shape); 3B wins on 0 dimensions.**

**Criterion 2 Verdict: PARTIAL**

Applying the scoring rule: "Partial: 3A wins on exactly 2 dimensions including Overall fidelity." 3A wins Arc Directionality and Overall Silhouette Fidelity. 3A does not win ≥3 dimensions, so this does not meet the Pass threshold. 3A wins Overall fidelity (not a tie or 3B win), so this is not a Fail. The improvement is real and observable — the arc directionality difference is clear without measurement tools — but it is not dominant enough (3A does not win ≥3 of 4).

---

### Criterion 3 — Crop execution evidence (process check)

**Criterion verbatim:** Runner log must record: (1) pixel coordinates/dimensions of the crop, (2) filename of saved crop, (3) confirmation that crop was used as primary ref for 3A, (4) confirmation that full Shot 1 was used for 3B, (5) confirmation that all other generation parameters were held constant between 3A and 3B.

**Relevant file:** `runner-log.md`

#### Item checklist

| Item | Present? | Evidence |
|------|----------|----------|
| Crop pixel coordinates/dimensions | Yes | "x1: 4017, y1: 1167, x2: 5504, y2: 3072 — Crop size: 1487 × 1905 px" |
| Filename of saved crop | Yes | "images/shot1-tsuba-crop.png" explicitly named |
| Confirmation crop used as primary ref for 3A | Yes | "Ref images: images/shot1-tsuba-crop.png (crop isolating the tsuba from Shot 1)" in img03 section |
| Confirmation full Shot 1 used for 3B | Yes | "Ref images: images/shot1.jpeg (FULL Shot 1, unmodified)" in img04 section |
| All other parameters held constant | Yes | A/B Control section documents identical: prompt text (verbatim), model, aspect ratio, resolution, edit-style reference-lock language, framing intent |

All 5 items documented.

**Criterion 3 Verdict: PASS**

---

## Overall verdict

**PARTIAL**

Applying the overall verdict table:

| Criterion 1 | Criterion 2 | Criterion 3 | Maps to |
|-------------|-------------|-------------|---------|
| Pass | Partial | Pass | PARTIAL |

Reasoning: The trial demonstrates a real, observable improvement from the crop technique — Shot 3A reproduces the ground-truth tsuba's distinctive diagonal dragon arc more faithfully than Shot 3B. The arc directionality dimension and the overall fidelity dimension both clearly favor 3A. However, the improvement is not dominant: 3A wins only 2 of 4 dimensions (ties on void count and guard shape, both of which both images produce correctly). The lesson's causal claim is supported but not conclusively proven at the Pass threshold — the crop technique improves the most diagnostic dimension (arc directionality) but does not produce a broader advantage across the silhouette's other measurable dimensions.

The process was clean and fully documented: blinded runner, correct A/B isolation, crop coordinates logged, all parameters held constant.

---

## Confidence

**High**

The difference between 3A and 3B on arc directionality is visually unambiguous — in 3A the dragon head is at left and the body sweeps diagonally toward lower-right, directly matching the crop reference; in 3B the head is at top-center and the body wraps symmetrically. This is a clear, no-tools-required observation. The tie on void count and guard shape is equally clear — both images produce two central hitsu-ana and circular guards. The 2-win / 2-tie score is not a borderline call. The PARTIAL verdict is a confident application of the written scoring rule, not a hedge.
