# Skeptic review — 2026-04-17-L09-S02

## Q1: Was the scenario hard enough?

The tsuba in Shot 1 is actually larger than specified — the runner notes it landed at ~15–20% of frame width, not the 6–9% targeted. Even so, the crop isolates a detail-rich object (dragon silhouette, hitsu-ana openings, circular rim) from a busy scene containing Kenji, tools, cloth, and multiple other fittings. The full Shot 1 reference genuinely contains competing visual signals: at least 5 other metal objects are visible on the table, and Kenji's figure dominates the mid-ground. A naive prompt with only the text "iron tsuba with a dragon cutout" and the full-scene ref would plausibly produce a plausible dragon tsuba, but the specific silhouette layout — arc directionality, head position, diagonal body lean — is not textually constrained. The scenario is not trivial: getting the arc direction right required the visual anchor to be unambiguous. The scenario was meaningfully hard for the dimension that matters.

## Q2: Was the lesson actually necessary?

Looking at 3A and 3B directly: 3B shows a top-leading symmetric dragon wrap, not a left-leading diagonal. 3A shows a left-leading diagonal matching the crop reference. This difference is visually unambiguous — not a measurement-dependent judgment call. The crop's unique contribution was making the dragon's specific diagonal orientation the loudest signal in the reference. In the full-scene ref, the tsuba occupies a corner of a wide shot and appears as a near-silhouette against a light table surface; the model's attention was distributed across the entire scene and produced a plausible-but-different dragon layout. The two tied dimensions (void count, guard shape) are both "easy" features: any dragon tsuba will be circular and have hitsu-ana openings — the model gets these right regardless of ref strategy, which is expected and does not undermine the causal claim. The two winning dimensions (arc directionality, overall fidelity) are the design-specific features that require a loud visual anchor to reproduce. This is exactly the causal structure L09 predicts. The lesson was necessary for the dimensions that are actually hard.

## Q3: Were the criteria decisive?

The 2/4 scoring rule was pre-registered and applied cleanly — no post-hoc interpretation was needed. "Arc directionality" could in principle be disputed (is a diagonal sweep "the same arc direction" as a top-leading wrap?), but the visual difference here is stark enough that a different judge would almost certainly land on the same call: 3A head-at-left diagonal vs 3B head-at-top symmetric are not borderline. "Overall silhouette fidelity" is deliberately subjective by design (naive viewer test), but it aligns with the arc result — no ambiguity introduced. The tied dimensions are also unambiguous: both images are circular, both have hitsu-ana openings. The only realistic alternate verdict is Pass (if a judge counted arc directionality as a stronger standalone win and argued for 3/4) — not Fail. The PARTIAL verdict is a confident, rules-consistent application of the scoring table, not hedging. The criteria held up.

## Overall verdict

adversarial-valid

## Rationale

The scenario created a genuine causal test: the only variable between 3A and 3B was the reference, and the difference in arc directionality is visually unambiguous — exactly what L09 predicts would differ. The 2/4 win is not a weak signal; the 2 tied dimensions (void count, guard shape) are structural features any dragon tsuba would have regardless of ref quality, so a tie there is expected and neutral. The 2 winning dimensions (arc directionality, overall fidelity) are the design-specific features L09 exists to protect. The PARTIAL verdict is a clean, honest application of a pre-registered scoring rule — the lesson is causally supported at partial strength, which is what the ledger should record.
