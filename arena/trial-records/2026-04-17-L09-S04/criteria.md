# Criteria — 2026-04-17-L09-S04 (Multi-Factor: Ref Strategy × Crop Size)

> This trial does NOT use the standard L09 asymmetry rubric. It is a multi-factor investigation with four hypotheses. Judge and Skeptic produce **findings**, not a pass/partial/fail verdict.

## Scoring setup

Judge receives all 6 images: Shot 1 (ground-truth), and the 5 hero variants (3A-small, 3A-large, 3D-small, 3D-large, 3B).

Judge scores each hero variant on D1 and D2 independently. D3 is derived.

---

## D1 — Target element fidelity

**Definition**: How accurately does the hero variant reproduce the specific asymmetric features of the orrery as shown in Shot 1?

**Reference**: Shot 1 (the orrery as generated — whatever specific form it took)

**Four scoring sub-elements (each: yes / partial / no):**

| ID | Feature | Yes | Partial | No |
|----|---------|-----|---------|-----|
| F1 | **Ecliptic ring tilt**: main ring tilts left (viewer's left higher, right lower) | Tilt clearly present and directionally correct | Tilt present but direction ambiguous | Ring is level or tilts wrong direction |
| F2 | **Saturn arm direction**: one arm extends to viewer's right and terminates lower than all other arms | Right-side low arm with ring/disk model clearly present | Arm present but direction or height relationship unclear | No right-side low arm, or arm points left |
| F3 | **Earth arm curve**: one arm curves leftward before its terminal sphere | Leftward curve clearly present | Curve present but direction ambiguous | No curve, or curves right |
| F4 | **Sun off-center right**: central sphere sits right-of-center on base platform | Off-center position clearly right | Slightly off-center, direction uncertain | Central or off-center to left |

**D1 score**: count of `yes` answers (0–4). Partial = 0.5.

**Per-variant D1 scores** (Judge fills in):

| Variant | F1 | F2 | F3 | F4 | D1 score |
|---------|----|----|----|----|----------|
| 3A-small | | | | | |
| 3A-large | | | | | |
| 3D-small | | | | | |
| 3D-large | | | | | |
| 3B | | | | | |

---

## D2 — Scene context preservation

**Definition**: How well does the hero variant preserve the specific background scene elements established in Shot 1?

**Reference**: Shot 1 (wide establishing scene)

**Note**: The hero shot is a medium close-up. Scene elements may be partially visible, cropped, or reduced in prominence — the question is whether their essential identity is preserved where they appear, NOT whether they fill the same frame area as in Shot 1.

**Three scene elements (each: yes / partial / no):**

| ID | Scene element | Yes | Partial | No |
|----|--------------|-----|---------|-----|
| SE1 | **Brass barometer on mahogany shelving** (far wall, center-right behind scientist) | Barometer or equivalent distinctive instrument on shelving clearly identifiable | Something is on shelving but not clearly a barometer; shelving present but sparse | No shelving, or generic lab equipment replaces shelving entirely |
| SE2 | **Gas-jet wall sconces with amber glow** (right wall; warm amber light pools against cool grey stone) | Warm amber lighting source visible on right side, clearly wall-mounted, contrasting with cooler ambient light | Some warm light source present but position, mounting, or color ambiguous | No amber wall lighting; overhead or cool lighting only; right wall absent |
| SE3 | **Arched frosted-glass windows** (left wall; grey daylight quality) | At least one arched or Gothic window partially in frame with cool grey daylight quality | Window or light source visible but arch form unclear or light is not grey/cool | No windows, or windows are rectangular and bright/warm, or left wall absent |

**D2 score**: count of `yes` answers (0–3). Partial = 0.5.

**Per-variant D2 scores** (Judge fills in):

| Variant | SE1 | SE2 | SE3 | D2 score |
|---------|-----|-----|-----|----------|
| 3A-small | | | | |
| 3A-large | | | | |
| 3D-small | | | | |
| 3D-large | | | | |
| 3B | | | | |

---

## D3 — Composite score

**Definition**: D1 + D2 combined, equally weighted. Captures overall fidelity across both target element AND scene context.

**Formula**: D3 = D1 (normalized to 0–1 by dividing by 4) + D2 (normalized to 0–1 by dividing by 3), then ranked.

Or equivalently, rank variants by `(D1/4 + D2/3)` descending.

**D3 composite table** (Judge/Skeptic fills in):

| Variant | D1 (0–4) | D1 norm | D2 (0–3) | D2 norm | D3 composite | Rank |
|---------|----------|---------|----------|---------|-------------|------|
| 3A-small | | | | | | |
| 3A-large | | | | | | |
| 3D-small | | | | | | |
| 3D-large | | | | | | |
| 3B | | | | | | |

---

## Hypothesis tests

### H1 — Crop-only sacrifices scene context

**Claim**: Crop-only refs (3A-small, 3A-large) produce worse scene preservation than full-scene ref (3B).

**Pass condition**: BOTH 3A-small AND 3A-large score strictly lower than 3B on D2.
**Partial condition**: ONE of the two 3A variants scores lower than 3B on D2, the other ties or exceeds.
**Fail condition**: Neither 3A variant scores lower than 3B on D2 (both tie or beat 3B).
**Inconclusive**: D2 scores are identical across all three variants (all tied at 0 or all tied at 3).

**H1 result** (fill in): ___________

**H1 implication if pass**: L09 scope should explicitly note that crop-only refs sacrifice scene context when the hero shot extends beyond the crop bounds. Dual-ref becomes more important.
**H1 implication if fail**: Scene sacrifice is not inherent to crop-only — may be prompt-dependent or this scenario may not exhibit the effect. L09 scope update deferred.

---

### H2 — Dual-ref wins on composite

**Claim**: Dual-ref variants (3D-small, 3D-large) outperform the best single-ref variant on D3.

**Pass condition**: At least one of {3D-small, 3D-large} has the highest D3 composite score among all 5 variants.
**Partial condition**: One 3D variant ties for highest D3 with a single-ref variant.
**Fail condition**: Both 3D variants score below MAX(3A-small, 3A-large, 3B) on D3.
**Inconclusive**: All 5 variants have identical D3 scores (unlikely given 7 sub-elements).

**H2 result** (fill in): ___________

**H2 implication if pass**: Dual-ref is a strong candidate for L12. Runner should draft L12 lesson body.
**H2 implication if fail**: Dual-ref does not reliably improve on either single-ref strategy. L12 deprioritized.

---

### H3 — Larger crop = better target fidelity

**Claim**: The large crop (more pixels, more detail of the orrery) produces better target element reproduction than the small crop.

**Pass condition**: 3A-large D1 score strictly exceeds 3A-small D1 score.
**Partial condition**: 3A-large and 3A-small tie on D1 but 3D-large > 3D-small on D1 (pattern holds in dual-ref context).
**Fail condition**: 3A-small D1 ≥ 3A-large D1 AND 3D-small D1 ≥ 3D-large D1.
**Inconclusive**: Both 3A variants score 0 on D1 (model completely ignores crop ref in both cases).

**H3 result** (fill in): ___________

**H3 implication if pass**: Crop resolution is a material variable; warrants documentation in L09 as a sub-rule, and possibly L13 (crop resolution guidance).
**H3 implication if fail**: Crop resolution below ~512px may already be sufficient for anchor; or model is insensitive to ref resolution. No new lesson warranted on this finding alone.

---

### H4 — Dual-ref is robust to crop size

**Claim**: Dual-ref performance is relatively insensitive to whether the crop is small or large, because the full-scene ref compensates for any lost detail.

**Pass condition**: |D1(3D-large) − D1(3D-small)| ≤ 1 AND |D2(3D-large) − D2(3D-small)| ≤ 0.5 (scores within 1 sub-element of each other on both dimensions).
**Partial condition**: One dimension satisfies the threshold, the other does not.
**Fail condition**: Both dimensions show gap > threshold (dual-ref strongly sensitive to crop size).
**Inconclusive**: Both 3D variants score identically on all sub-elements (possible if model treats both refs uniformly).

**H4 result** (fill in): ___________

**H4 implication if pass**: Dual-ref is more robust than single-ref; L12 guidance can recommend small crop as sufficient when full ref is also provided. Lower overhead for practitioners.
**H4 implication if fail**: Dual-ref also benefits from larger crops; L12 guidance must specify minimum crop size. H3 and H4 together constrain the L12 recipe.

---

## Overall outcome (findings format)

This trial produces findings, not a pass/fail verdict on L09.

**Finding F-A (scene sacrifice)**: [H1 result + supporting D2 data]
**Finding F-B (dual-ref advantage)**: [H2 result + supporting D3 data]
**Finding F-C (crop resolution)**: [H3 result + supporting D1 data]
**Finding F-D (dual-ref robustness)**: [H4 result + H4 partial data]

### Downstream actions triggered by findings

| Condition | Action |
|-----------|--------|
| H1 pass | Add note to L09 body: "Crop-only refs sacrifice scene context when hero shot is wider than crop bounds" |
| H2 pass | Runner drafts L12 lesson body (dual-ref technique) |
| H3 pass | Add sub-rule to L09: "Larger crops produce better element lock; minimum ~512px recommended; ~2048px preferred for complex instruments" |
| H4 pass | L12 lesson body can specify: "small crop sufficient when paired with full-scene ref" |
| H1+H2 both pass | L12 scope confirmed: solves scene-sacrifice while maintaining target lock |
| H2 fail | Dual-ref deprioritized; note inconclusive in L09 validation log |

---

## Judge notes section

*Judge and Skeptic: use this space for observations beyond the structured scoring that may inform the findings.*

### Observations on D1:

### Observations on D2:

### Observations on D3:

### Edge cases or ambiguities encountered:

### Skeptic adversarial notes:
