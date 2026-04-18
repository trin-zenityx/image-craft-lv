# Scenario S01 — Vintage Radio on a 1920s General-Store Shelf

## Goal

Test that the Runner applies L09 (crop the reference to isolate the target element) when matching a specific Bakelite radio silhouette across a 4-shot commercial-product set; a full-scene shop-interior reference would dilute the anchor.

## Axis fingerprint

```
char=middle-aged-white-female-shopkeeper; era=1920s-art-deco;
genre=slice-of-life; palette=warm-earth; model=nano-banana-pro;
modality=small-4-shot-set; culture=western; scale=small-set;
domain=commercial-product
```

## Flipped axes vs DHYANA

1. **char** — middle-aged white female shopkeeper (DHYANA: adult Tibetan Buddhist monk)
2. **era** — 1920s Art Deco / retrofuturism (DHYANA: sci-fi-spiritual)
3. **genre** — slice-of-life / commercial (DHYANA: drama)
4. **palette** — warm earth: ochre, walnut brown, ivory, soft amber (DHYANA: cyan + amber)
5. **modality** — small 4-shot set (DHYANA: 25-shot storyboard)
6. **culture** — Western / American Midwest (DHYANA: East Asian-spiritual)
7. **scale** — small set / 2–5 images (DHYANA: large set / 16+)
8. **domain** — commercial product (DHYANA: film still)

8 of 9 axes flipped. Only model (Nano Banana Pro) is retained.

## Flipped axes vs prior scenarios for L09

None prior — first arena trial for L09, axis-distinct test passes by default.

## Scenario description

**Project:** "Hartwell's General Store — Radiola Display Campaign" — a fictional 1920s American general-store commercial shoot for a heritage radio brand.

**Setting:** Hartwell's General Store, a warm, dusty Midwest shop circa 1925. Shelves lined with canned goods, bolts of fabric, and a prominent wooden display counter. The hero prop is the **Radiola Model 8** — a compact Bakelite tabletop radio with a distinctive rounded rectangular silhouette, a single large round tuning dial centered on the front face, and a woven cloth speaker grille in a deep burgundy. The cabinet is dark walnut Bakelite with thin ivory pinstripe trim at the edges. These proportions and markings are its immutable anchor.

**Character:** Elspeth Hartwell, 50s, white, stout build, grey-streaked auburn hair in a practical bun, wearing a cream blouse with a blue apron. She is the shopkeeper and appears in two of the four shots. Her face, build, and apron are consistent across shots but are secondary to the radio.

**Shot list (4 shots):**

- **Shot 1 — Establishing wide:** Interior of the full store. Elspeth stands behind the counter. The Radiola Model 8 is visible on the counter, small relative to the full scene (approximately 8–10% of the frame width). Warm window light from the left. Ochre and walnut tones dominate.

- **Shot 2 — Counter medium:** Elspeth leaning on the counter with the radio at her elbow, radio filling approximately 25% of the frame. She looks at it with fond curiosity.

- **Shot 3 — Hero product:** Tight three-quarter front view of the Radiola Model 8 alone on the counter. Radio fills ~80% of the frame. No character. Clean focus, studio-style composition but in the warm shop ambiance.

- **Shot 4 — Detail dial:** Extreme close-up of the tuning dial and grille cloth, filling the full frame. Shallow depth of field; the burgundy grille texture and ivory dial markings must be legible.

**Palette:** Warm earth — ochre walls, walnut wood surfaces, ivory and cream accents, burgundy cloth grille, soft window light. No cool tones.

**L09 requirement:** The Runner must use the Shot 1 wide image (once generated) as a reference for shots 3 and 4. The radio in Shot 1 is small and surrounded by shelves, goods, and Elspeth. The Runner must crop a tight region around the radio from Shot 1 before passing it as the anchor ref for shots 3 and 4, so the model receives an unambiguous silhouette signal. Passing the full Shot 1 image as the radio reference for the close-up shots is the expected naive failure mode.

**Model:** Nano Banana Pro, using edit-style ref language ("match the radio in this reference exactly", "preserve the Bakelite cabinet proportions").

## Recommended Runner inputs

1. **Scenario brief:** this file in full.
2. **Shot 1** is generated first; its output image becomes the source reference.
3. Runner must:
   a. Generate Shot 1 (wide establishing).
   b. Crop a tight bounding box around the Radiola Model 8 from the Shot 1 output (PIL or ImageMagick).
   c. Use the crop as the primary ref when generating Shots 2, 3, and 4.
4. Edit-style prompting recommended for shots 3 and 4: "The radio must match the design in the reference crop exactly — same rounded rectangular silhouette, same centered circular dial, same burgundy grille cloth, same ivory pinstripe trim."
5. Budget note: 4 shots + 1 crop operation = well within $2 cap.

## Pre-registered pass criteria

Full detail in `criteria.md`. Summary:

- **Criterion 1 (Target element match):** The Radiola Model 8 in shots 3 and 4 matches the radio visible in Shot 1 in overall silhouette (rounded rectangular cabinet), dial placement (centered, single large circle), and grille cloth color (burgundy). Clear match = Pass; significant drift in shape or markings = Fail.
- **Criterion 2 (Crop evidence):** Runner log or transcript shows that a cropped image isolating the radio was produced from Shot 1 and passed as ref — not the full Shot 1 image alone.
- **Overall:** Pass if both criteria pass. Fail if Criterion 1 fails regardless of Criterion 2.
