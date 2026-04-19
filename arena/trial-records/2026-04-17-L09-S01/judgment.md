# Judgment — 2026-04-17-L09-S01

## Per-criterion verdicts

### Criterion 1: Target element match

- **Relevant images:** shot01-wide-establishing.jpeg (reference baseline), shot01-radio-crop-final.png (crop anchor), shot03-hero-product.jpeg (Shot 3), shot04-detail-dial.jpeg (Shot 4)
- **Verdict:** pass
- **Evidence:**

  **Shot 1 baseline:** The radio in Shot 1 is clearly visible on the counter at approximately 8–10% of frame width. Zooming in confirms: rounded-rectangular cabinet (not oval, not square), single large circular dial on the right portion of the front face, dark reddish/burgundy woven cloth grille on the left, and visible light-colored pinstripe trim lines along cabinet edges.

  **Shot 3 (hero product, radio ~80% frame):** The cabinet is unambiguously rounded-rectangular — same proportions as Shot 1, with softly curved corners. The single large circular tuning dial is centered-right on the front face, consistent with Shot 1. The woven cloth grille occupies the left portion of the front face in a deep burgundy/dark red — consistent with Shot 1. Ivory/gold pinstripe trim lines run along the cabinet edges and are clearly visible. No extra dials introduced; grille shape and proportion match Shot 1. Near-exact match to the crop reference.

  **Shot 4 (dial close-up, extreme CU):** Evaluating on dial placement and grille cloth color only (per Judge notes). The circular tuning dial occupies the right half of the frame — consistent with Shot 1 and Shot 3. The grille cloth fills the left half and reads as deep burgundy with clearly legible woven textile texture. Ivory/aged frequency markings are legible on the dial face. No contradictions with Shot 1. Consistent.

  All pass checks satisfied for both Shot 3 and Shot 4. No major new features introduced. Silhouette, dial, and grille are consistent across shots.

---

### Criterion 2: Crop evidence in Runner log

- **Relevant images / files:** runner-log.md, images/shot01-radio-crop.png, images/shot01-radio-crop-v2.png, images/shot01-radio-crop-final.png
- **Verdict:** pass
- **Evidence:**

  The runner-log.md explicitly documents a dedicated crop operation under the heading "[CROP OPERATION — L09]". The log records three distinct crop iterations with pixel coordinates:
  - `shot01-radio-crop.png` (850×900 px) — first attempt, radio clipped, discarded
  - `shot01-radio-crop-v2.png` (1200×1200 px) — second attempt, adjusted, discarded
  - `shot01-radio-crop-final.png` (1000×970 px) — **final tight crop, radio fills ~85% of crop frame**

  All three crop image files are present in the `images/` directory and confirmed to exist (glob listing). The crop-final file visually confirms the radio fills the frame tightly with all design elements unambiguous.

  The log explicitly states the crop was passed as PRIMARY ref for Shots 2, 3, and 4, and the L09 Crop Evidence table confirms the full Shot 1 was NOT passed as the primary radio ref for close-up shots. The runner distinguishes between the crop (radio prop anchor) and the full Shot 1 (location/character/ambiance anchor) throughout.

  This is a clean pass of Criterion 2: a distinct cropped image file was produced AND that file is explicitly documented as the reference input for shots 3 and 4.

---

## Overall verdict

pass

**Reasoning:** Criterion 1 passes cleanly — the Radiola Model 8 in Shots 3 and 4 shows a consistent rounded-rectangular cabinet silhouette, a single large centered circular dial, and a deep burgundy woven grille cloth matching the radio visible in Shot 1. No silhouette drift, no multiplied dials, no absent grille. Criterion 2 passes cleanly — the Runner produced three distinct crop file iterations, retained the final crop as a named file, and explicitly documented passing it as the primary prop anchor ref for Shots 2, 3, and 4 (not the full Shot 1 image). Per the Overall verdict table, Pass + Pass = PASS.

## Confidence

high

The images are unambiguous: the radio design is consistent across all shots, the crop file exists and is visually confirmed, and the runner log leaves no doubt about the mechanical steps taken. No borderline calls were required.
