# Skeptic review — 2026-04-17-L09-S01

## Q1: Was the scenario hard enough?

The 8% frame-width radio constraint is real: Shot 1 visually confirms the radio is small relative to a busy scene — shelves, Elspeth, window light, and period goods all compete for visual weight. A naive user passing the full Shot 1 as ref for a hero product shot would plausibly get silhouette drift. However, the scenario also front-loads an extremely detailed text description of the radio (rounded rectangular, single circular dial, burgundy woven grille, ivory pinstripe trim) in the scenario brief, which Runner faithfully translated into every shot prompt. A naive but text-competent prompt engineer could anchor the design through verbose text alone, making the crop a reinforcement rather than a necessity. The scenario does not include a "text-only control" condition to distinguish these two mechanisms. This is a meaningful gap: the scenario asks whether crop is needed, but the text description is so rich that the radio's distinctiveness in the generated output could be wholly attributable to text anchoring, not crop anchoring.

## Q2: Was the lesson actually necessary?

Runner simultaneously applied L09, L01, L04, and L08 — four lessons working together. There is no counterfactual run: we do not know what Shots 3 and 4 would look like if Runner had passed the full Shot 1 with the same detailed text prompts. The L09 lesson posits that at ~8-10% frame width the crop signal is "10% loud" — but the text description in every prompt was 100% explicit about silhouette, dial position, grille layout, and trim. The crop may have been decisive, or it may have been redundant alongside the text. The runner-log's self-reported "near-perfect silhouette match" does not distinguish between these causes. The DHYANA validation in L09 itself (where the lesson was proven necessary) involved a case where text description alone failed across v3–v6 regens; this trial has no equivalent evidence of text-alone failure, making the lesson's contribution here unproven rather than demonstrated.

## Q3: Were the criteria decisive?

Criterion 1 is generally clear, but "burgundy" introduces interpretive slack: the actual grille in Shot 3 and the crop reads as dark maroon/oxblood — a color a strict Judge could classify as "shifted toward brown" and invoke the partial/fail threshold. The Judge called it burgundy (pass) without documenting the color boundary, meaning a different Judge reading the same criteria could have landed partial. Shot 3's dial is described in criteria as "centered" but the scenario describes it as "centered on the front face" while the brief's own description says "centered on the right portion of the front face" — the images show it right-of-center, which is consistent, but a Judge unfamiliar with the scenario description could flag dial placement as drifted. Criterion 2 is process-verifiable (file exists in images/ directory) and unambiguous — that part is decisive. Overall: one of the two criteria carries real interpretive risk.

## Overall verdict

void-lesson-unnecessary

## Rationale

The scenario cannot establish that L09 was the decisive factor because the radio's design was over-specified in text across every shot prompt, creating a confound. Without a counterfactual run (full Shot 1 ref + same text, no crop), we cannot attribute the clean match in Shots 3 and 4 to the crop operation rather than to rich text anchoring — exactly the causal claim L09 validation requires. A trial that passes because of detailed text description alongside a crop does not prove the crop was necessary; it only proves the Runner followed the lesson.

## Suggestions

1. **Control condition required.** The scenario should mandate that Runner also generate one "naive" version of Shot 3 or Shot 4 using the full Shot 1 as the sole ref with the same text prompt, so the Judge can compare prop consistency directly. Without this A/B pair, Criterion 1 cannot distinguish text-anchoring from crop-anchoring.

2. **Reduce text description of the target element.** Strip the scenario brief's radio description down to a name ("Radiola Model 8") and one or two traits, forcing the model to rely on the visual reference to fill in design details. If the crop-ref trial passes and a text-only run fails, L09's necessity is demonstrated.

3. **Raise the bar on Criterion 2.** "A crop file exists" is a process check, not a causal check. Add a requirement that the Judge compare a crop-ref shot to a full-ref shot of the same scene to verify that the crop produced meaningfully better element lock. The current Criterion 2 can be satisfied by a Runner who crops but whose text prompt would have passed anyway.
