# Judgment — 2026-04-17-L09-S03

## Per-criterion verdicts

### Criterion 1: Target element silhouette match (3A)

- Relevant images: `shot1-crop-headdress.png` (ground truth), `shot3a-hero-crop-ref.jpeg`
- Verdict: **pass**
- Evidence: Shot 3A matches the crop reference on all 4 observable dimensions. D1: the dark feather fan fans clearly higher and wider on the left — strongly asymmetric, matching the crop. D2: the crown/apex leans rightward (viewer's right), matching the crop's specific tilt direction. D3: long emerald quetzal feathers cascade dramatically to the left and upward-left from the apex, matching the crop. D4: a naive viewer would immediately identify the 3A headdress as the same specific asymmetric penacho — left-dominant dark fan, rightward crown lean, leftward green cascade — matching the crop's overall silhouette. 3A scores 4/4 against ground truth.

---

### Criterion 2: Causal control validity

- Relevant images: runner-log.md (A/B integrity section)
- Verdict: **pass**
- Evidence: Runner log confirms all four required conditions. (a) Shot 3A used `shot1-crop-headdress.png` (2036×1966 px PIL crop of headdress+face) as primary reference. (b) Shot 3B used `shot1-plaza-full.jpeg` (full uncropped 5504×3072 px scene) as primary reference. (c) Prompt text for 3A and 3B is verbatim identical: `"Ixtli, elderly Aztec high priest, wearing penacho headdress. Game concept art, jade and terracotta palette, dusk lighting."` (d) Same model (nano-banana-pro), same aspect ratio (3:4), same resolution (4K), no negative prompts or seed differences noted. The only variable between 3A and 3B is the reference image. Control is clean.

---

### Criterion 3: Comparative advantage — the PASS gate

- Relevant images: `shot1-crop-headdress.png` (ground truth), `shot3a-hero-crop-ref.jpeg`, `shot3b-hero-full-ref.jpeg`
- Verdict: **pass**
- Evidence — dimension-by-dimension independent scoring:

**D1 — Left-fan dominance (left side visibly taller/wider than right?):**
- 3A: YES. The dark feather fan masses strongly to the left; the left side rises noticeably higher and spreads wider than the right — matching the crop's pronounced asymmetry.
- 3B: NO. The dark fan in 3B extends leftward but the asymmetry is significantly weaker; the right side retains substantial feather mass and the difference between sides is mild compared to the crop reference.
- Result: **3A wins D1.**

**D2 — Crown lean direction (apex leans rightward from vertical?):**
- 3A: YES. The headdress apex leans toward viewer's right, consistent with the crop reference's specific rightward tilt.
- 3B: NO. The apex leans toward viewer's left — opposite to the reference direction. The model defaulted to a different crown orientation when given the full busy scene as reference.
- Result: **3A wins D2.**

**D3 — Quetzal feather cascade (long tail feathers curve leftward from apex?):**
- 3A: YES. Long emerald feathers sweep leftward and upward-left from the apex in a dramatic cascade, matching the crop.
- 3B: YES. Long emerald feathers also cascade leftward from the apex. This feature survived even in the full-ref control condition.
- Result: **Tie (both match).**

**D4 — Overall silhouette fidelity (naive viewer test: same specific headdress as the crop?):**
- 3A: YES. The combined left-dominant fan, rightward crown lean, and leftward quetzal cascade produce a silhouette a naive viewer would immediately recognize as the same specific penacho from the crop.
- 3B: NO. The milder left asymmetry and reversed crown lean (leftward instead of rightward) produce a different silhouette overall. A naive viewer would register this as a generic Aztec headdress, not the distinctive specific penacho shown in the crop.
- Result: **3A wins D4.**

**Summary table:**

| Dim | 3A vs crop | 3B vs crop | Winner |
|-----|-----------|-----------|--------|
| D1  | YES       | NO        | 3A     |
| D2  | YES       | NO        | 3A     |
| D3  | YES       | YES       | Tie    |
| D4  | YES       | NO        | 3A     |

3A wins 3 of 4 dimensions (D1, D2, D4), including D4 (overall silhouette fidelity). D3 is a tie.

Per the scoring table in criteria.md: 3A wins ≥3 dimensions AND includes D4 → **PASS**.

---

## Overall verdict

**pass**

Reasoning: Criterion 2 is clean — the A/B control was properly executed with identical prompts and the only variable being the reference image type. Criterion 1 passes with 3A matching the crop on all 4 dimensions. Criterion 3 meets the PASS gate: 3A beats 3B on exactly 3 of 4 dimensions (D1, D2, D4), with D3 a tie (both outputs reproduced the leftward quetzal cascade). Crucially, D4 (overall silhouette fidelity) is among the 3A wins. The lesson's causal claim is robustly supported: the crop reference locked in the directional asymmetry (left-fan dominance and rightward crown lean) that the full-scene reference failed to anchor, causing 3B to default to a weaker, differently-oriented headdress. This trial promotes L09 from pending to validated.

## Confidence

**high**

All four dimension calls are unambiguous from visual inspection. The directional features (left vs right fan dominance, crown lean direction, feather cascade direction) are clearly readable in each image. The D2 reversal in 3B (leftward lean instead of rightward) is the most decisive single observation and is not a borderline call. D3 tie is straightforward — both outputs show leftward quetzal cascade. No dimension required a close call.
