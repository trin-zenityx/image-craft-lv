# Arena Void Log

> Trials that did NOT count toward the ledger (Skeptic void, Judge
> criteria-broken, Runner abort, human-abort, etc.).

Append-only. Each entry:

## <trial-id>

- **Date:** YYYY-MM-DD
- **Lesson tested:** L##
- **Verdict:** void-too-easy | void-criteria-weak | void-lesson-unnecessary | criteria-broken | human-abort | runner-abort
- **Reason (1-2 lines):** ...
- **Trial folder:** `arena/trial-records/<trial-id>/`

---

<!-- First void will be appended below -->

## 2026-04-17-L09-S01

- **Date:** 2026-04-17
- **Lesson tested:** L09 (crop refs to isolate target element)
- **Verdict:** `void-lesson-unnecessary`
- **Reason:** Scenario over-specified the target element (Radiola Model 8) in the text prompts across every shot, creating a confound. Without a counterfactual "full-ref + same text" condition, we cannot attribute the clean prop-match in Shots 3–4 to the crop operation rather than to rich text anchoring. The Runner did apply L09 correctly (Judge: PASS), but the trial does not prove L09 was the decisive factor.
- **Trial folder:** `arena/trial-records/2026-04-17-L09-S01/`
- **Skeptic's suggestions for next L09 scenario:**
  1. Include a paired "control" shot: same scene, full Shot 1 as sole ref, same text prompt — so Judge can compare crop-ref vs full-ref outputs directly.
  2. Strip the radio's text description down to name + 1-2 traits, forcing the model to rely on the visual reference for design details.
  3. Raise Criterion 2 to a causal check (crop-ref shot vs full-ref shot must show meaningfully better element lock), not merely a process check ("crop file exists").

**L09 arena void count:** 1 (threshold for `arena-unresolvable` flag: 3)
