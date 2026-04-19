# Runner log — 2026-04-17-L09-S04

## Session summary

- **Model:** nano-banana-pro (all 6 generations)
- **Total images generated:** 6 (1 source + 5 hero shots)
- **Total estimated cost:** ~$0.24 (6 × ~$0.04)
- **Trial date:** 2026-04-17
- **Status:** COMPLETE — no budget overrun, blinded maintained

---

## Identical sparse text prompt (verbatim)

All 5 hero shots used this exact text — no variation:

> "Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory"

No directional or structural adjectives for the orrery were included. Strictly name + implied trait ("mechanical") as allowed by scenario constraint.

---

## Crop dimensions

| Crop | Native (from Shot 1, 5504×3072) | Crop box (x1,y1,x2,y2) | Final saved size |
|------|----------------------------------|-------------------------|-----------------|
| crop-small.png | 1018 × 1475 px | (2807, 890, 3825, 2365) | 353 × 512 px |
| crop-large.png | 2642 × 2366 px | (1651, 552, 4128, 2918) | 2048 × 1834 px |

**Small crop:** tight bounding box around the orrery instrument only — approximately 51%–69.5% of width, 29%–77% of height. Orrery fills majority of frame. Dr. Ashby's hand on base ring is partially visible (unavoidable given composition). Resized to ~512px on longest side.

**Large crop:** wider bounding box including orrery, Dr. Ashby's hands on base ring, immediate table surface — approximately 30%–78% of width, 18%–95% of height. Does not include far-wall shelving or windows. Resized to ~2048px on longest side.

---

## Prompts used

### img01 — Shot 1 (wide establishing scene, no ref)

**Prompt:**
> Wide Victorian natural-philosophy laboratory, ca. 1885. Dr. Eleanor Ashby, mid-40s female scientist, pale complexion, dark auburn hair streaked with grey in a chignon, wearing a steel-blue laboratory coat with rolled cuffs over a white high-collar blouse, stands three-quarter to camera looking down with focused concentration. Her right hand rests on the base ring of a mechanical brass orrery on the central work table; her left holds a brass caliper. The orrery is roughly 45 cm tall with an asymmetric arm configuration: main ecliptic ring tilts 15 degrees off-horizontal leaning left, a secondary arm extends right terminating in a copper Saturn-ring model hanging lower than all other planets, the central sun-sphere is off-center to the right of the base, and the Earth arm curves leftward terminating in a small blue-glass sphere. Room details: three arched frosted-glass windows on the left wall admitting grey London daylight, a row of gas-jet wall sconces on the right wall casting warm amber pools against cool slate-grey stone, floor-to-ceiling mahogany shelving on the far wall packed with leather-bound folios, specimen jars with amber fluid, and a large brass barometer mounted center-right on the shelf, a deep burgundy Persian rug with geometric border on the floor. Camera at mid-height slight upward tilt, 35 mm lens, full-room editorial shot. Palette: steel-blue dominant from window light, warm amber in sconce pools, brass and dark mahogany accents. Scientific-illustration grade rendering, clean, slightly formal, no cinematic lens blur. No text, no watermark, no modern elements.

**Ref images:** None
**Model:** nano-banana-pro | **Aspect ratio:** 16:9 | **Resolution:** 4K
**Task ID:** 8c368dda7c561aae34921fb79ccced23
**Local file:** `images/shot1-full.jpeg`
**Notes:** Ground-truth source image. All scene elements present (SE1 barometer, SE2 sconces, SE3 arched windows, Persian rug, specimen jars, orrery with asymmetric config).

---

### img02 — 3A-small (crop-small only ref)

**Prompt (verbatim):**
> Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory

**Ref images:** `[images/crop-small.png]` (353 × 512 px, orrery instrument only)
**Pass order:** crop-small is the sole ref
**Model:** nano-banana-pro | **Aspect ratio:** 4:3 | **Resolution:** 4K
**Task ID:** a7b5d8493e3b7f18052b10edc83918d7
**Local file:** `images/3A-small.jpeg`
**Notes:** Outfit drifted to tweed jacket (not steel-blue lab coat). Palette shifted warm. Small crop lacked clothing/scene context. Magnifying glass substituted for caliper. Scene elements SE2/SE3 weakly reproduced.

---

### img03 — 3A-large (crop-large only ref)

**Prompt (verbatim):**
> Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory

**Ref images:** `[images/crop-large.png]` (2048 × 1834 px, orrery + hands + table surface)
**Pass order:** crop-large is the sole ref
**Model:** nano-banana-pro | **Aspect ratio:** 4:3 | **Resolution:** 4K
**Task ID:** 1f348a240bf1710f4d17e7edd680db32
**Local file:** `images/3A-large.jpeg`
**Notes:** Steel-blue lab coat restored. Caliper present. Saturn arm and asymmetric orrery config reproduced. SE1 (barometer) present. SE2/SE3 partial. Better character and orrery fidelity than 3A-small.

---

### img04 — 3D-small (crop-small + shot1-full, crop first)

**Prompt (verbatim):**
> Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory

**Ref images:** `[images/crop-small.png, images/shot1-full.jpeg]`
**Pass order:** crop-small listed first (to anchor target element); shot1-full listed second (to supply scene context)
**Model:** nano-banana-pro | **Aspect ratio:** 4:3 | **Resolution:** 4K
**Task ID:** c89142e96ba02fb5b7f3edf5a833e9b1
**Local file:** `images/3D-small.jpeg`
**Notes:** Strongest scene element recovery among all hero shots. SE1 (barometer) ✓, SE2 (sconce amber glow) ✓, SE3 (arched frosted windows) ✓. Steel-blue lab coat ✓, caliper ✓. Orrery asymmetric config reproduced. Full-scene ref successfully restored scene context despite small crop.

---

### img05 — 3D-large (crop-large + shot1-full, crop first)

**Prompt (verbatim):**
> Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory

**Ref images:** `[images/crop-large.png, images/shot1-full.jpeg]`
**Pass order:** crop-large listed first (to anchor target element); shot1-full listed second (to supply scene context)
**Model:** nano-banana-pro | **Aspect ratio:** 4:3 | **Resolution:** 4K
**Task ID:** c464b919719414e882b25f33c74b916a
**Local file:** `images/3D-large.jpeg`
**Notes:** Near-identical scene vocabulary to 3D-small. SE1 ✓, SE2 ✓, SE3 ✓. Steel-blue coat ✓, caliper ✓. Orrery asymmetric config ✓. Suggests the full-scene ref dominates scene reconstruction regardless of crop size.

---

### img06 — 3B (shot1-full only ref, no crop)

**Prompt (verbatim):**
> Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory

**Ref images:** `[images/shot1-full.jpeg]`
**Pass order:** shot1-full is the sole ref
**Model:** nano-banana-pro | **Aspect ratio:** 4:3 | **Resolution:** 4K
**Task ID:** 1e7058d3212e9605ee08cba3ad5de2c0
**Local file:** `images/3B.jpeg`
**Notes:** Strongest overall scene fidelity. SE1 (barometer) ✓, SE2 (amber sconce glow) ✓, SE3 (arched windows) ✓, Persian rug ✓. Steel-blue coat ✓, caliper ✓. Orrery asymmetric config reproduced. Baseline for naive full-ref strategy.

---

## Pre-submit Checklist compliance

| Section | Item | Status |
|---------|------|--------|
| A | Recurring character — Dr. Ashby anchored via Shot 1 crops | ✓ |
| A | Recurring prop (orrery) — Shot 1 used as ground-truth ref | ✓ |
| A | Design-language — steel-blue/gaslight palette; identical params all 5 hero shots | ✓ |
| B | Camera angle: 4:3 medium close-up, editorial framing | ✓ |
| B | Negative prompts: included in Shot 1 prompt; sparse text for hero shots per scenario constraint | ✓ |
| B | Dimensions: orrery described with numbers in Shot 1 prompt (~45 cm, 15 degrees) | ✓ |
| C | Refs chosen: crop-small isolates orrery instrument; crop-large adds hand/table context; shot1-full supplies scene | ✓ |
| C | Under model ref limit (max 8; used max 2 per shot) | ✓ |
| C | Pass order for dual-ref: crop listed first to anchor target element, full scene listed second | ✓ |
| D | Phase plan: Shot 1 → crops → 5 hero shots | ✓ |

---

## Post-generate Self-review notes

### Shot 1
All seven checks passed. Scene ground-truth established: Dr. Ashby in steel-blue coat, asymmetric orrery on table, three arched frosted windows (left), gas-jet sconces (right), mahogany shelving with barometer (far wall), Persian rug.

### 3A-small
- **Anatomy:** Plausible but outfit drifted — tweed jacket instead of steel-blue lab coat.
- **Orientation:** Three-quarter to camera ✓
- **Design-language drift:** Significant — warm palette instead of cool-steel-gaslight. Small crop lacked clothing and room context, model fell back on text prior for "Victorian scientist" (→ generic warm Victorian).
- **Internal consistency:** Warm throughout, no cool/warm contrast. Internally consistent but wrong for this scene.
- **Intent fulfillment:** Magnifying glass substituted for caliper. Orrery present with partial asymmetric features. SE1 partially visible. SE2/SE3 weak.
- **Proportion vs ref:** Orrery scale reasonable.
- **Full-frame scan:** Missing arched windows clearly, no sconce amber glow, wrong outfit.
- **Decision:** NOT regenerated. This drift is the experimental data point — 3A-small is expected to sacrifice scene and character context. Shipping as-is is correct for blinded trial.

### 3A-large
- All seven checks largely passed. Steel-blue coat restored, caliper correct. Orrery asymmetric config well reproduced (Saturn arm, tilted ring, Earth blue sphere). SE1 ✓. SE2 partial (warm tones in shelving area). SE3 partial (windows visible but rectangular rather than arched). No regeneration needed.

### 3D-small
- All seven checks passed. Outstanding recovery of scene context despite small crop. All three SE elements clearly present. Full-frame scan clean. PASS.

### 3D-large
- All seven checks passed. Near-identical to 3D-small in scene vocabulary. PASS.

### 3B
- All seven checks passed. Best scene reproduction of all hero shots. All SE elements clearly present with strong amber glow and arched windows. PASS.

---

## Regens

**None.** 3A-small's design drift is the experimental artifact being captured, not a defect to fix. All other shots passed first-pass self-review. Diminishing-returns (L10) risk was not encountered.

---

## Identical param confirmation

All 5 hero shots:
- **Text prompt:** Identical (verbatim) — "Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory"
- **Model:** nano-banana-pro (identical)
- **Aspect ratio:** 4:3 (identical)
- **Resolution:** 4K (identical)
- **Only variable:** ref_images argument

| Shot | ref_images |
|------|-----------|
| 3A-small | `[crop-small.png]` |
| 3A-large | `[crop-large.png]` |
| 3D-small | `[crop-small.png, shot1-full.jpeg]` (crop first) |
| 3D-large | `[crop-large.png, shot1-full.jpeg]` (crop first) |
| 3B | `[shot1-full.jpeg]` |

Confirmed: the only variable across all 5 hero generations is the ref_images argument.

---

## Dual-ref pass order

For 3D-small and 3D-large: **crop image listed first, full-scene image listed second.** Rationale per scenario instructions: crop anchors the target element identity; full scene supplies room context.

No hiccups in dual-ref calls. Both submitted cleanly; model accepted two references without issue. Both 3D variants showed strong scene recovery vs their crop-only equivalents.

---

## Output manifest

| Shot label | File | Description |
|-----------|------|-------------|
| Shot 1 | `images/shot1-full.jpeg` | Wide establishing scene. Dr. Ashby three-quarter, orrery on table, full room visible. Ground truth for D2 scoring. |
| crop-small | `images/crop-small.png` | 353 × 512 px. Tight crop of orrery instrument only from Shot 1. |
| crop-large | `images/crop-large.png` | 2048 × 1834 px. Wide crop: orrery + hands + table surface from Shot 1. |
| 3A-small | `images/3A-small.jpeg` | Hero shot. Crop-small as only ref. Notable: outfit drift (tweed), palette shift warm. Orrery partially reproduced. |
| 3A-large | `images/3A-large.jpeg` | Hero shot. Crop-large as only ref. Steel-blue coat restored. Orrery asymmetric. SE1 ✓, SE2/SE3 partial. |
| 3D-small | `images/3D-small.jpeg` | Hero shot. Crop-small + shot1-full (dual-ref, crop first). All SE elements present. Scene context fully recovered. |
| 3D-large | `images/3D-large.jpeg` | Hero shot. Crop-large + shot1-full (dual-ref, crop first). Near-identical to 3D-small. All SE elements present. |
| 3B | `images/3B.jpeg` | Hero shot. Shot1-full as only ref. Strongest scene fidelity. All SE elements clearly present. |
