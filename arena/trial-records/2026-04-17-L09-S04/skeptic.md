# Skeptic review — 2026-04-17-L09-S04

## Q1: Was the scenario/methodology rigorous enough?

Controls held on the critical axis: all 5 hero shots used verbatim identical sparse text, identical model, identical aspect ratio and resolution, and differed only in `ref_images`. This is a clean isolation. The text prompt ("Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory") contains no directional or structural adjectives for the orrery, so the model's text prior would generate a generic symmetric orrery — the asymmetric features must come from the ref. This is genuinely hard.

One methodological impurity: the `crop-small.png` (353×512px) contains a substantial swathe of the mahogany bookshelf and the brass barometer in its upper portion — it was not a tight orrery-only crop as specified in the scenario ("Orrery body should fill at least 80% of the crop frame"). Visual inspection confirms the barometer is visible in the upper ~25% of the crop-small frame. This contaminates the "crop-only sacrifices scene context" signal slightly: SE1 was technically present in the small-crop input, yet 3A-small still scored 0 on SE1. The experiment survived its own impurity (the model ignored the scene debris in the crop), but it means the crop-small was not a clean isolated-element ref. The scenario's crop preparation instructions and the Runner's execution diverged at this point.

The three scene elements (SE1 barometer, SE2 sconce, SE3 arched windows) are visually distinctive, spatially specific, and unambiguously present or absent in each hero shot. Judge could score these reliably — confirmed by image inspection. Axis fingerprint shows 8/9 flips from DHYANA and 4–5 flips from each prior L09 scenario. Scenario diversity is strong.

**Minor concern, does not void**: the crop-small impurity strengthens H1 (scene sacrifice is even more real, since the model had a barometer in the small crop and still failed SE1), so the impurity actually cuts against favorable-to-the-hypothesis bias. It does not invalidate H1, H2, or H3.

## Q2: Are the findings robust or artifactual?

**H1 PASS (scene sacrifice)**: Robust. The visual evidence is unambiguous. 3A-small scores 0/3 on all scene elements — confirmed by inspection, the image shows a warm-toned interior with no windows, no sconce, no barometer, completely wrong palette. 3A-large recovers partially (barometer yes, sconce no, window partial) but still far below 3B's 3.0. The crop-small impurity (barometer in frame) makes H1 even more impressive, not less. This finding would likely replicate.

**H2 PASS (dual-ref wins composite)**: Partially robust, partially fragile. 3D-small at D3=2.000 vs 3B at 1.875 is a margin of 0.125 — meaningful, but not large. The margin exists because 3B drops F4 to partial (sun off-center). Visually, 3B's sun placement is genuinely ambiguous — it is hard to confirm clear right-of-center displacement in the hero shot framing. If 3B is re-scored as F4=yes, 3B D1 becomes 4.0 and D3 becomes 2.000, tying 3D-small. H2 would drop from PASS to PARTIAL. The Judge flagged this ambiguity explicitly. The claim "dual-ref clearly wins" is therefore fragile at the margin — it rests on a single half-point call that a different Judge could resolve differently. The directional finding (dual-ref competitive with or better than best single-ref) is sound; the claim that 3D-small is the clear winner is not ironclad.

**H3 PASS (crop resolution affects D1)**: Highly robust. The gap is 4.0 vs 1.0 — a 3-point difference. Visually confirmed: 3A-small shows no Saturn arm, no off-center sun, ambiguous tilt and curve. 3A-large shows all four features clearly. This finding would replicate with near certainty. The 353×512px crop demonstrably failed to convey radially-positioned directional features.

**H4 PARTIAL (dual-ref robustness)**: Weakly supported. The entire H4 partial verdict rests on a single element dropout: SE2 (sconce) in 3D-large. Visually confirmed — 3D-large has no clear wall-mounted amber sconce, while 3D-small has one. But this is n=1 per variant. The Judge explicitly flagged that a repeat generation of 3D-large might restore the sconce. The proposed mechanism (large crop consuming "attention capacity" that leaves less room for the full-scene ref to populate the background) is speculative and untested. A repeat run that produces SE2 in 3D-large would convert H4 to PASS. A single-generation trial cannot meaningfully distinguish a systematic large-crop attention effect from ordinary stochastic dropout. H4 partial is not robust.

**Portability concern**: All four findings rest on one Victorian laboratory scenario with one model (nano-banana-pro). The dual-ref advantage is real within this trial. Whether it holds across other scene types, other instrument types, or other models is unknown. This is a genuine limitation given the proposed system changes.

## Q3: Are the findings decisive enough to act on?

**Narrowing L09's scope (add sub-rule: crop must be high-res enough)**: Yes, act. H3's 4.0 vs 1.0 gap is so large it would be irresponsible not to document the crop resolution constraint. This is a clear, strong, single-trial finding that fills an obvious gap in L09's current guidance. The lesson currently says "crop it so that element fills the frame" but says nothing about minimum resolution for complex multi-arm instruments. Adding a note that 512px is insufficient for complex directional instruments is well-supported.

**Creating new L12 lesson (dual-ref) as pending**: Borderline. H2 passes, but the winning margin is fragile (one F4 half-point call). The directional finding is sound — dual-ref is at minimum competitive with the best single-ref strategy, and appears to resolve scene sacrifice while maintaining element lock. However, spawning a new pending lesson on N=1, with the winner's margin fragile, with H4 inconclusive about crop size guidance in dual-ref context, means L12 would be drafted with significant uncertainty baked in. "Pending" status is the appropriate label precisely for this situation — it signals the technique is promising but not validated. Creating L12 as pending is acceptable if its lesson body is carefully qualified.

**Modifying arena prompts (Skeptic Q4 side-effect check)**: Not yet. The proposed Skeptic Q4 addition (side-effect check) responds to the observation that the large crop may have suppressed the sconce. This effect is speculative and single-instance. Modifying arena infrastructure on the basis of a one-shot mechanism hypothesis is premature. Hold until a follow-up trial can confirm or deny the attention-competition mechanism.

**Overall judgment on action vs hold**: H1 and H3 findings justify immediate L09 annotation. H2 finding justifies creating L12 as pending, with the lesson body carefully noting the winning margin is narrow and the finding is N=1. H4 partial and the proposed arena prompt change should hold pending an S04b follow-up that re-runs 3D-large (and possibly 3D-small) to test replicability of the sconce dropout.

## Overall verdict

**adversarial-valid**

## Rationale

The core experimental controls held cleanly (identical text, model, parameters; only ref_images varied), the target element is genuinely hard (four unambiguous directional asymmetries that a generic text prior cannot reproduce), and the three key findings (H1, H2, H3) are visually confirmed and directionally strong. The trial is not too easy — 3A-small's complete failure and 3A-large's partial recovery are real experimental signals. The scenario is adversarially valid.

The verdict is adversarial-valid rather than void because no systemic flaw undermines the trial's validity: the crop-small impurity actually strengthens H1, the scoring criteria were interpretable (with one acknowledged ambiguity on F4/3B that the Judge flagged), and the methodology was rigorously controlled. H4 partial is weakly supported, but that is a finding about the evidence, not about the trial design.

## Recommendation

**Act on H1 and H3 now. Create L12 as pending. Hold on H4-driven changes and arena prompt modification.**

Specifically:
- **Act**: Annotate L09 with the scene-sacrifice caveat (H1) and the crop resolution sub-rule (H3 — 512px insufficient for complex instruments; 2048px recommended).
- **Act**: Create L12 (dual-ref) as `status: pending` using S04 as origin. Lesson body must note: (a) winning margin over 3B is narrow and rests on N=1, (b) crop size interaction with scene reconstruction is uncertain, (c) small crop in dual-ref context outperformed large crop on D2 in this trial but the mechanism is not confirmed.
- **Hold**: Do not modify arena Skeptic prompts yet. The SE2 dropout in 3D-large is a single-generation artifact that may be stochastic. An S04b follow-up (re-run 3D-large 2–3 times to test sconce reproducibility) should precede any infrastructure change.
- **Hold**: The H2 win margin depends on F4/3B scoring. Before treating 3D-small as decisively superior to 3B, a repeat trial should confirm the D3 gap is real and not a one-point ambiguity artifact.

## Suggestions (if void)

N/A — verdict is adversarial-valid. No generator changes required.

---

*Skeptic: claude-sonnet-4-6 | Trial: 2026-04-17-L09-S04 | Date: 2026-04-17*
