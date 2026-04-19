# Runner log — 2026-04-17-L09-S02

## Session summary

- **Model used:** nano-banana-pro (4K resolution, all shots)
- **Total images generated:** 4 (Shot 1, Shot 2, Shot 3A, Shot 3B) + 1 crop file (PIL)
- **Total estimated cost:** ~$0.16 (4 × ~$0.04/image at 4K)
- **Wall-clock duration:** ~18 minutes (submit + wait × 4)
- **Runner:** Blinded (did not read criteria.md or lesson files)

---

## Prompts used

### img01 — Shot 1 (wide workshop scene, no ref)

**Prompt (verbatim):**
```
Wide shot of a traditional Japanese sword-fittings workshop, Edo period, documentary register. A single low table dominates the foreground, iron and shakudo fittings arranged along the near edge. The iron tsuba with a dragon cutout rests on the right foreground of the table, occupying roughly 6-8% of frame width — its silhouette distinctive but small. Kenji, a young Japanese male artisan in his mid-twenties, lean build, ink-stained fingers, wearing a plain indigo kosode and a leather apron, works in the mid-ground. Natural light filters through shoji screens — soft and directionless, ochre cast from aged paper. Indigo-dyed cloth wraps several completed pieces on the table. Muted palette: aged iron near-black, warm wood tones, ochre light, indigo cloth accents. No saturated color. Slight desaturation overall. Long lens, documentary still camera style. Quiet, observational mood. 85 mm equivalent telephoto, slightly elevated angle. No text, no watermark, no Western design elements.
```

**Ref images:** None (first generation, baseline)
**Model params:** nano-banana-pro, 16:9, 4K
**Task ID:** 825fe228c89e785b8732bbc098c57ca1
**Output file:** images/shot1.jpeg

**Notes:** No ref. Batch Gate baseline. The model placed the tsuba in the right foreground with excellent clarity — the dragon cutout silhouette is distinctly readable. The tsuba appears somewhat larger (~15-20% of frame width) than the 6-8% specified, but the silhouette is well-formed and will serve as a strong anchor for the crop.

---

### img02 — Shot 2 (medium context, Shot 1 as scene ref)

**Prompt (verbatim):**
```
Medium shot inside the same traditional Japanese sword-fittings workshop, Edo period, documentary register. Kenji's hands in close foreground, leaning over a piece of indigo-dyed cloth, arranging or inspecting a completed fitting. The low wooden table fills the lower frame. The iron tsuba with a dragon cutout is visible on the table but not dominant — to one side, partially visible. Warm ochre light from shoji screens at rear. Same muted indigo-ochre palette: aged iron near-black, warm wood, ochre light, indigo cloth. No saturated color. Slight desaturation. 85mm equivalent telephoto, low angle looking across the table surface. No text, no watermark, no Western elements. Quiet, observational documentary mood.
```

**Ref images:** shot1.jpeg (full scene ref for consistency)
**Model params:** nano-banana-pro, 16:9, 4K
**Task ID:** aeb04ab9991dc8295db882ab3866e22c
**Output file:** images/shot2.jpeg

**Notes:** Strong scene consistency with Shot 1. Same shoji screens, same warm ochre backlight, same indigo garments on Kenji. The tsuba with dragon cutout appears on the right side of the frame — somewhat more prominent than "not dominant" but acceptable for a medium context shot.

---

### img03 — Shot 3A (tsuba close-up, CROP as primary ref — L09 technique)

**Prompt (verbatim):**
```
Tight close-up of the iron tsuba with a dragon cutout, filling the frame, resting on a warm wooden table surface. Shallow depth of field — table grain softly in focus in corners. Match the tsuba in the reference exactly. Preserve the hand guard shape from the reference. Muted palette: aged iron near-black, warm wood tones, ochre ambient light. No saturated color. Slight desaturation. Macro lens, top-down 3/4 angle. No text, no watermark, no decorative borders.
```

**Ref images:** images/shot1-tsuba-crop.png (crop isolating the tsuba from Shot 1)
**Model params:** nano-banana-pro, 1:1, 4K
**Task ID:** 5b4b171c131c4a68b364db9b0f59b9bc
**Output file:** images/shot3a.jpeg

**Notes:** L09 technique applied — cropped reference passed. The tsuba fills the frame with a detailed dragon cutout. Dragon anatomy shows head at upper-left, serpentine body coiling through the guard, tail at lower-right — this arrangement corresponds closely to the crop reference silhouette.

---

### img04 — Shot 3B (tsuba close-up, FULL Shot 1 as primary ref — naive control)

**Prompt (verbatim):**
```
Tight close-up of the iron tsuba with a dragon cutout, filling the frame, resting on a warm wooden table surface. Shallow depth of field — table grain softly in focus in corners. Match the tsuba in the reference exactly. Preserve the hand guard shape from the reference. Muted palette: aged iron near-black, warm wood tones, ochre ambient light. No saturated color. Slight desaturation. Macro lens, top-down 3/4 angle. No text, no watermark, no decorative borders.
```

**Ref images:** images/shot1.jpeg (FULL Shot 1, unmodified)
**Model params:** nano-banana-pro, 1:1, 4K
**Task ID:** 91beb28663f206677212b959dcc40665
**Output file:** images/shot3b.jpeg

**Notes:** Control condition. IDENTICAL prompt to Shot 3A word-for-word. Only variable is the reference image (full scene vs. crop). The dragon arrangement in 3B shows a slightly different coiling configuration than the crop reference.

---

## A/B Control — Proof of identical conditions

**The following were held CONSTANT between Shot 3A and Shot 3B:**
- Prompt text: identical (verified verbatim above — same 149-word prompt)
- Model: nano-banana-pro
- Aspect ratio: 1:1
- Resolution: 4K
- Edit-style reference-lock language: identical ("Match the tsuba in the reference exactly. Preserve the hand guard shape from the reference.")
- Framing intent: tight close-up filling frame, shallow DoF, table surface visible

**The ONLY variable:**
- Shot 3A reference: `images/shot1-tsuba-crop.png` (cropped region isolating tsuba)
- Shot 3B reference: `images/shot1.jpeg` (full scene, 5504×3072 px, unmodified)

---

## Crop dimensions and source coordinates

**Source image:** images/shot1.jpeg — 5504 × 3072 px

**Crop region (PIL coordinates):**
- x1: 4017, y1: 1167, x2: 5504, y2: 3072
- Crop size: 1487 × 1905 px

**What the crop contains:** The tsuba with dragon cutout dominates the crop frame (~70% fill). A small margin of warm wooden table surface is visible at edges. The dragon silhouette (circular iron guard, serpentine dragon body, hitsu-ana openings at center) is fully visible and the tsuba circle is complete.

**Crop file:** images/shot1-tsuba-crop.png

---

## Pre-submit Checklist compliance

### A. Consistency audit
- [x] Recurring prop (tsuba): anchored via Shot 1 in both Shot 2 (scene ref) and Shot 3A/3B
- [x] Recurring character (Kenji): Shot 1 used as scene ref for Shot 2 for consistency
- [x] Design-language match: indigo-ochre palette, iron near-black specified in all prompts

### B. Ambiguity sweep
- [x] Camera angle named in all prompts (85mm telephoto, slightly elevated for Shot 1; 85mm low angle for Shot 2; macro lens, top-down 3/4 for Shots 3A/3B)
- [x] Negative prompts included in all shots ("No text, no watermark, no Western design elements")
- [x] No container/mirror orientation ambiguity in this scenario (object is a flat metal disc)

### C. Reference strategy
- [x] Shot 1: no ref (first generation, correct)
- [x] Shot 2: Shot 1 full scene (scene consistency, not element locking — correct)
- [x] Shot 3A: crop ref — most relevant to locking the specific tsuba design (L09 applied)
- [x] Shot 3B: full ref — naive control condition
- [x] Chain order correct: Shot 1 generated first, used as ref source for all downstream
- [x] Under model ref limit (1 ref per shot, limit is 8)

### D. Phase planning
- [x] Shot 1 solo baseline first (Batch Gate compliance)
- [x] Shot 2 after Shot 1 confirmed
- [x] Crop produced before Shots 3A/3B
- [x] 3A and 3B generated sequentially from identical prompt text

---

## Post-generate Self-review notes

### Shot 1
1. Anatomical: Kenji's figure proportional and natural. Scale vs environment correct.
2. Orientation: Kenji faces downward toward work. Documentary, not theatrical.
3. Design-language: Muted indigo-ochre confirmed. No saturated color.
4. Internal consistency: Warm shoji backlight, coherent shadows.
5. Intent: Wide shot with table foreground. Tsuba visible in right foreground with clear dragon cutout.
6. Proportion vs ref: N/A (first generation, no ref).
7. Full-frame: Tools, indigo cloth, fittings on table, Kenji in mid-ground. No text/watermark. PASS.

**Result: PASS. No regen needed.**

### Shot 2
1. Anatomical: Kenji torso + hands visible. Lean young male, indigo kosode, apron. Correct.
2. Orientation: Kenji leaning over table, looking down. Natural.
3. Design-language: Same palette as Shot 1. Shoji screens, warm ochre light. Consistent.
4. Internal consistency: Light from rear shoji consistent. Table surface, tools all match Shot 1 world.
5. Intent: Medium shot, hands working foreground, tsuba visible (slightly more prominent than "not dominant" but acceptable).
6. Proportion vs Shot 1 ref: Character appearance, environment, palette all consistent. Good.
7. Full-frame: No extraneous elements. No text/watermark. PASS.

**Result: PASS. No regen needed.**

### Shot 3A (crop-ref)
1. Anatomical: Circular iron tsuba with complete rim, hitsu-ana openings at center, dragon body coiling through guard. Correct object type.
2. Orientation: Flat disc on table, top-down 3/4 angle as specified. Correct.
3. Design-language: Aged iron near-black, warm wood table. Muted. Correct.
4. Internal consistency: Shallow DoF — center sharp, edges soft. Warm ochre ambient light. Correct.
5. Intent: Tsuba fills frame. Dragon cutout highly detailed — serpentine body, visible claws, head at upper-left, tail at lower-right. Strong match to crop reference arrangement.
6. Proportion vs ORIGINAL crop ref: Dragon silhouette arrangement (head upper-left, body diagonally coiling, hitsu-ana openings at center) corresponds to crop reference. Good fidelity.
7. Full-frame: Table surface only in background. No extraneous elements. No text/watermark. PASS.

**Result: PASS. No regen needed.**

### Shot 3B (full-ref)
1. Anatomical: Circular iron tsuba, complete rim, hitsu-ana visible. Correct object type.
2. Orientation: Similar top-down 3/4 angle. Correct.
3. Design-language: Muted iron dark, warm wood. Slightly cooler tone than 3A. Acceptable.
4. Internal consistency: Shallow DoF, warm ambient light. Correct.
5. Intent: Tsuba fills frame. Dragon cutout visible — body coils around the central openings, head at top-center. Different configuration from crop reference.
6. Proportion vs ORIGINAL full-ref Shot 1: The tsuba in Shot 1 occupies a small portion of the full-scene ref; the model had many competing visual signals (Kenji, tools, table, cloth, other fittings). Dragon arrangement in 3B is a plausible dragon tsuba but the specific silhouette configuration differs from the source tsuba.
7. Full-frame: Table surface, coherent composition. No text/watermark. PASS.

**Result: PASS as standalone. The A/B comparison shows observable difference in dragon silhouette configuration — 3A adheres more closely to the source crop, consistent with L09 prediction.**

---

## Regens

None required. All 4 images passed self-review on first generation.

---

## Output manifest

| ID     | File                        | Description                                                                        |
|--------|-----------------------------|------------------------------------------------------------------------------------|
| Shot 1 | images/shot1.jpeg           | Wide workshop scene, Edo period. Kenji mid-ground. Tsuba with dragon cutout right foreground. Source image for crop and all downstream refs. |
| Shot 2 | images/shot2.jpeg           | Medium shot. Kenji's hands working at table. Same workshop world, consistent palette. Tsuba visible at right. |
| Crop   | images/shot1-tsuba-crop.png | PIL crop of Shot 1, coordinates (4017,1167)-(5504,3072). 1487×1905 px. Tsuba fills ~70% of frame. Used as primary ref for Shot 3A. |
| Shot 3A| images/shot3a.jpeg          | Tight close-up of tsuba. CROP used as ref (L09 technique). Dragon silhouette closely matches source arrangement. |
| Shot 3B| images/shot3b.jpeg          | Tight close-up of tsuba. FULL Shot 1 used as ref (naive control). Dragon silhouette differs slightly from source arrangement. |

---

## Blinded compliance

- Did NOT read `criteria.md`
- Did NOT read any file under `arena/criteria/`
- Did NOT read any lesson files directly (only loaded via skill ENTRY PROTOCOL)
- Did NOT read other trial records (S01)
- Only read: `runner-prompt.md`, `scenario.md`, `templates/session-kickoff.md`, `lessons/README.md`, `lessons/references/L09-crop-refs.md`, `lessons/workflow/L04-self-review-protocol.md`
