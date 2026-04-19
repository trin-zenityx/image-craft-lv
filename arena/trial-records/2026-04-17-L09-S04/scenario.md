# Scenario S04 — Victorian Laboratory Orrery (Multi-Factor: Ref Strategy × Crop Size)

## Goal

Test whether dual-ref (crop + full-scene) resolves the scene-context sacrifice observed in S03's crop-only shot, AND whether crop resolution (small ~512px vs large ~2048px) affects target-element fidelity — producing actionable findings on the scope of L09 and the feasibility of L12 (dual-ref technique).

## Axis fingerprint

```
char=middle-aged-Victorian-female-scientist; era=Victorian-steampunk;
genre=editorial; palette=cool-steel-gaslight; model=nano-banana-pro;
modality=hero-shot-set; culture=Western-European; scale=small-set;
domain=scientific-illustration
```

## Flipped axes vs DHYANA

DHYANA baseline:
```
char=adult-tibetan-monk; era=sci-fi-spiritual; genre=drama;
palette=cyan-amber; model=nano-banana-pro; modality=large-storyboard;
culture=east-asian-spiritual; scale=large-set; domain=film-still
```

1. **char**: adult-tibetan-monk → middle-aged-Victorian-female-scientist
2. **era**: sci-fi-spiritual → Victorian-steampunk
3. **genre**: drama → editorial
4. **palette**: cyan-amber → cool-steel-gaslight (blue-grey gaslit + warm brass)
5. **modality**: large-storyboard → hero-shot-set
6. **culture**: east-asian-spiritual → Western-European
7. **scale**: large-set → small-set
8. **domain**: film-still → scientific-illustration

**8 of 9 axes flipped from DHYANA.** ✓

## Flipped axes vs prior L09 scenarios

### vs S01 (1920s American general store, female shopkeeper, warm earth, commercial-product, small-set)

1. **era**: 1920s-American → Victorian-steampunk ✓
2. **genre**: (commercial-product adjacent) → editorial ✓
3. **palette**: warm-earth → cool-steel-gaslight ✓
4. **domain**: commercial-product → scientific-illustration ✓

**4 axes flipped from S01.** ✓ (requirement: ≥2)

### vs S02 (Feudal Japan tsuba workshop, male artisan, documentary, muted indigo-ochre, editorial)

1. **era**: feudal-japan → Victorian-steampunk ✓
2. **char**: male-artisan → middle-aged-female-scientist ✓
3. **genre**: documentary → editorial ✓
4. **culture**: east-asian-secular → Western-European ✓
5. **palette**: muted-indigo-ochre → cool-steel-gaslight ✓

**5 axes flipped from S02.** ✓ (requirement: ≥2)

### vs S03 (Ancient Aztec temple plaza, elderly priest, fantasy, jade-terracotta, game-concept)

1. **era**: ancient-mesoamerican → Victorian-steampunk ✓
2. **char**: elderly-priest → middle-aged-female-scientist ✓
3. **genre**: fantasy → editorial ✓
4. **palette**: jade-terracotta → cool-steel-gaslight ✓
5. **domain**: game-concept → scientific-illustration ✓

**5 axes flipped from S03.** ✓ (requirement: ≥2)

---

## Scenario description

### Setting

A Victorian natural-philosophy laboratory, ca. 1885. The room is a converted ground-floor study: a high stone ceiling with exposed oak joists, three arched windows along the left wall letting in grey London daylight filtered through frosted glass. A row of gas-jet wall sconces lines the right wall, casting warm amber pools against the cool slate-grey stone. The far wall is floor-to-ceiling mahogany shelving packed with leather-bound folios, specimen jars (amber fluid, pale specimens), and a large brass barometer mounted at center-right of the shelf. A Persian rug — deep burgundy with a geometric border — covers the floor beneath the central work table.

On the central work table stands the **target element**: a **mechanical orrery**, an intricate brass astronomical model roughly 45 cm tall. This specific orrery has a distinctly **asymmetric arm configuration**: the main ecliptic ring tilts 15° off-horizontal, leaning toward the viewer's left; a secondary arm extends at a low right-angle to the right, terminating in a copper Saturn-ring model that hangs lower than any other planet. The central sun-sphere is off-center to the right of the base, and the Earth arm — the tallest — curves leftward before terminating in a small blue-glass sphere. No other orrery built to this design exists: the asymmetry is the scientist's personal modification to demonstrate orbital inclination.

The **scientist** is Dr. Eleanor Ashby, mid-40s, pale complexion, dark auburn hair streaked with grey wound into a practical chignon. She wears a steel-blue laboratory coat (slightly too large, rolled cuffs) over a white high-collar blouse. Her right hand rests on the orrery's base ring; her left holds a brass caliper. She stands three-quarter to camera, looking down at the orrery with focused concentration.

### Shot 1 — Wide establishing scene (source / no ref)

Full-room editorial shot. Camera at mid-height, slight upward tilt. Dr. Ashby in the mid-ground, the orrery on the table before her. Visible in frame: the three arched frosted-glass windows (left), the gas-jet sconces with amber glow (right), the mahogany shelving with barometer (far wall), the Persian rug underfoot, specimen jars in mid-ground on the table edge. This is the scene ground-truth. Palette: steel-blue dominant (window light), warm amber in sconce pools, brass and dark mahogany accents. Scientific-illustration grade rendering (clean, slightly formal, no cinematic lens blur).

### Hero shots (Shots 3A-small, 3A-large, 3D-small, 3D-large, 3B) — Close-up on orrery

All five hero shots use **identical sparse text**:

> "Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory"

All five share identical output parameters (same resolution, same style/rendering settings). Only the reference image strategy differs.

The desired hero shot is a **medium close-up**: Dr. Ashby's upper body from waist to shoulders, the orrery filling roughly 40% of the frame in the foreground, with the laboratory background visible but not dominant — the barometer on the shelving behind should be visible, at least one sconce glowing, the frosted-glass windows partially in frame. The orrery's asymmetric arm configuration (tilted ecliptic ring, low-hanging Saturn-right arm, leftward-curving Earth arm) must be preserved.

This framing is deliberately **wider than the small crop** (which shows only the orrery instrument) but similar in width to the large crop (which shows orrery + immediate table surface + Dr. Ashby's hands). Background scene elements visible in the hero shot are NOT shown in either crop — only in Shot 1 (full ref) and in Shot 3D (which gets both).

### Target element's asymmetric/directional features (for D1 scoring)

The orrery has four unambiguous directional cues:

1. **Ecliptic ring tilt**: the main ring tilts left (viewer's left is higher, right is lower)
2. **Saturn arm direction**: extends to the viewer's right, terminates lower than all other arms
3. **Earth arm curve**: curves leftward before the blue sphere
4. **Sun-sphere off-center**: sits right-of-center on the base platform

All four are directional and cannot be reproduced by a "generic orrery" text prior — the text prior would generate a symmetric, level orrery. Successful reference lock requires the model to reproduce these specific asymmetries.

### Three distinctive scene elements (for D2 scoring)

Judge will evaluate these three scene elements in each hero shot against Shot 1:

1. **SE1 — Brass barometer on mahogany shelving** (visible on far wall, center-right behind Dr. Ashby)
2. **SE2 — Gas-jet wall sconces with amber glow** (right wall; warm amber light pools visible against cool grey stone)
3. **SE3 — Arched frosted-glass windows** (left wall; at least one arch partially visible, grey daylight quality)

These are spatially specific, visually distinctive, and unambiguously present or absent. A regenerated background that replaces the shelving with generic lab benches, replaces the sconce lighting with overhead fluorescents, or removes the arched windows fails scene preservation for those elements.

---

## Shot list — all 6 generations

| # | Label | Method | Ref images | Crop config | Purpose |
|---|-------|--------|------------|-------------|---------|
| 1 | **Shot 1** | No ref — free generation | None | — | Wide establishing scene; creates ground-truth for scene (D2) and provides the full-scene ref image for 3B/3D |
| 2 | **3A-small** | Crop-only, small | Small crop of orrery only (~512px wide) | Tight crop: orrery instrument only, no hands, no table edge | L09 baseline at low crop resolution |
| 3 | **3A-large** | Crop-only, large | Large crop of orrery + hands + table (~2048px wide) | Wide crop: orrery + Dr. Ashby's hands on base ring + immediate table surface | L09 baseline at high crop resolution |
| 4 | **3D-small** | Dual-ref (crop + full) | Small crop + Shot 1 full scene | Same small crop as 3A-small | L12 candidate: can dual-ref recover scene context vs 3A-small? |
| 5 | **3D-large** | Dual-ref (crop + full) | Large crop + Shot 1 full scene | Same large crop as 3A-large | L12 candidate: can dual-ref recover scene context vs 3A-large? |
| 6 | **3B** | Full-only | Shot 1 full scene | No crop | Naive baseline: full-scene ref only (standard practice) |

---

## Ref prep instructions for Runner

### Step 1: Generate Shot 1 (no ref)
Generate the wide establishing scene with NO reference image. Use sparse text:
> "Wide Victorian natural-philosophy laboratory, Dr. Eleanor Ashby examines a mechanical orrery, gas-jet sconces, arched frosted windows, mahogany shelving with barometer"

Save as `shot1-full.png`. This image becomes:
- The scene ground-truth for D2 scoring
- The full-scene ref for shots 3B, 3D-small, and 3D-large

### Step 2: Prepare small crop (~512px)
From `shot1-full.png`, crop a tight bounding box around the orrery instrument only — no hands, no table edge, no background. The orrery body should fill at least 80% of the crop frame. Target output dimensions: approximately **512 × 512 px** (or nearest square that contains only the instrument). Save as `crop-small.png`.

Tool suggestion: `convert shot1-full.png -crop <W>x<H>+<X>+<Y> -resize 512x512 crop-small.png` (ImageMagick), or equivalent PIL crop + resize.

### Step 3: Prepare large crop (~2048px)
From `shot1-full.png`, crop a wider bounding box that includes the orrery, Dr. Ashby's hands resting on the base ring, and the immediate table surface — but NOT the background (no shelving, no sconces, no windows). Target output dimensions: approximately **2048 × 1536 px** (wider than tall, instrument-centered). Save as `crop-large.png`.

Tool suggestion: `convert shot1-full.png -crop <W>x<H>+<X>+<Y> -resize 2048x1536 crop-large.png`

### Step 4: Generate the 5 hero shots

Use **identical sparse text for all 5**:
> "Dr. Eleanor Ashby examines a mechanical orrery in her Victorian laboratory"

Use **identical output resolution and generation parameters** for all 5.

| Shot | ref_images argument |
|------|---------------------|
| 3A-small | `[crop-small.png]` |
| 3A-large | `[crop-large.png]` |
| 3D-small | `[crop-small.png, shot1-full.png]` |
| 3D-large | `[crop-large.png, shot1-full.png]` |
| 3B | `[shot1-full.png]` |

For dual-ref shots (3D-small, 3D-large): pass both images as a list to the ref_images parameter. The crop should be listed first so it anchors the target element; the full scene listed second provides context.

### Sparse text constraint
The target element description in the sparse text MUST NOT include directional or structural adjectives for the orrery. Allowed: `"mechanical orrery"` — maximum 2 traits (e.g. `"brass mechanical orrery"` or `"antique mechanical orrery"`). Forbidden: any mention of tilt, asymmetry, arm direction, Saturn, inclination, specific sphere positions.

---

## Pre-registered pass criteria

(Full detail in `criteria.md`.)

### Hypothesis H1 (scene sacrifice)
3A-small and 3A-large score ≤ 3B on D2 (scene context preservation).
Pass if: majority of SE elements show worse preservation in both 3A variants vs 3B.

### Hypothesis H2 (dual-ref wins combined)
3D-small or 3D-large scores ≥ MAX(any 3A or 3B) on D3 composite.
Pass if: at least one 3D variant is the best overall performer.

### Hypothesis H3 (crop resolution affects target fidelity)
3A-large scores higher than 3A-small on D1 (target element fidelity).
Pass if: Judge finds 3A-large reproduces more of the 4 orrery asymmetries than 3A-small.

### Hypothesis H4 (dual-ref robust to crop size)
3D-small and 3D-large score similarly on D1 + D2 combined.
Pass if: the two 3D variants differ by ≤ 1 element on D1 and ≤ 1 SE element on D2.

### Overall outcome framing
This trial does NOT produce a pass/fail verdict for L09 (already validated). It produces **findings** that:
- Update L09's documented scope (does crop-only sacrifice scene context? at what conditions?)
- Determine whether L12 (dual-ref) is worth formalizing as a lesson
- Determine whether crop resolution is a material variable requiring its own lesson (L13 candidate)
