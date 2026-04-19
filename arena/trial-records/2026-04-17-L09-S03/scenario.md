# Scenario S03 — The Penacho Trial

## Goal

Test whether cropping a reference image to isolate a single distinctive ceremonial object (a pre-Columbian feathered headdress) causes the model to reproduce its specific silhouette more accurately than passing the full-scene reference — exactly as L09 predicts.

## Axis fingerprint

```
char=elderly-aztec-high-priest; era=ancient-mesoamerican; genre=fantasy;
palette=jade-terracotta; model=nano-banana-pro; modality=small-hero-pair;
culture=latin-american-indigenous; scale=small-set; domain=game-concept
```

## Flipped axes vs DHYANA

1. **char**: adult-tibetan-monk → elderly-aztec-high-priest
2. **era**: sci-fi-spiritual → ancient-mesoamerican
3. **genre**: drama → fantasy
4. **palette**: cyan-amber → jade-terracotta
5. **culture**: east-asian-spiritual → latin-american-indigenous
6. **domain**: film-still → game-concept

Total: **6 of 9 axes flipped** (requirement: ≥3). ✓

## Flipped axes vs prior scenarios for L09

### vs S01 (1920s American general store)
1. **char**: middle-aged-white-female-shopkeeper → elderly-aztec-high-priest
2. **era**: 1920s-art-deco → ancient-mesoamerican
3. **genre**: slice-of-life → fantasy
4. **palette**: warm-earth → jade-terracotta
5. **culture**: western → latin-american-indigenous
6. **domain**: commercial-product → game-concept

Total: **6 of 9 axes flipped** (requirement: ≥2). ✓

### vs S02 (Feudal Japan tsuba workshop)
1. **char**: young-japanese-male-artisan → elderly-aztec-high-priest
2. **era**: feudal-japan → ancient-mesoamerican
3. **genre**: documentary → fantasy
4. **palette**: muted-indigo-ochre → jade-terracotta
5. **culture**: east-asian-secular → latin-american-indigenous
6. **domain**: editorial → game-concept

Total: **6 of 9 axes flipped** (requirement: ≥2). ✓

## Scenario description

**Project:** "Xiuhpilli" — a 2D action-fantasy game set in a mythologized pre-Columbian Mesoamerica. Art style: vivid painted illustration with a game-concept feel — stylized but not cartoony, closer to a high-production fantasy card game aesthetic.

**Character — Ixtli Quauhtli:** An elderly Aztec high priest, male, 70s, gaunt weathered face, jade-bead pectoral, bare feet, dark ceremonial robe with terracotta geometric embroidery. His defining, unmistakable feature is the **Penacho** — a towering ceremonial feathered headdress. The headdress is asymmetric: the left side fans higher and wider than the right, with a pronounced rightward lean at the crown; long quetzal tail feathers (bright emerald green, ~3× head height) cascade from the apex and curve leftward; turquoise mosaic base-band sits just above the brow. No other headdress arrangement is correct — the left-fan-right-lean is the specific silhouette that the lesson's crop ref must lock down.

**Why this target is ideal for the lesson:**
The model's text prior for "Aztec headdress" defaults to a symmetric, centered fan — the romanticized museum-reconstruction version. The actual Penacho reference in this scenario has an asymmetric left-dominant fan with a distinctive lean. A full-scene reference buries this asymmetry among competing elements (crowd, temple, smoke, other costumed figures). A cropped reference that fills the frame with only the headdress makes the left-lean unambiguous. The text description alone cannot specify "left-leaning asymmetric fan" with enough force to override the model's symmetric default.

**Location:** The great plaza before Templo Mayor at dusk. The plaza is densely populated: hundreds of costumed festival participants, incense smoke columns, giant flower-marigold garlands strung between posts, ceremonial drummers in foreground, merchants' canopies at left edge, a wide stone staircase ascending to the temple at right. Braziers throw warm amber light upward against a deep teal sky. **The scene is intentionally maximally busy** — at minimum 8 distinct visual clusters compete for the model's attention when the full scene is used as reference.

**Shot list (modality: small-hero-pair, scale: small-set):**

- **Shot 1 (Scene Reference):** Full plaza shot at medium distance. Ixtli stands at center-left, arms raised in blessing pose, headdress at its full height. Many festival figures partially occlude the frame's lower half. Headdress occupies approximately 8–12% of total frame area. This image is also the reference that the Runner will be instructed to use.
- **Shot 3A (Target — crop-ref variant):** Close hero portrait of Ixtli, head and shoulders only. Runner must crop Shot 1's reference down to the headdress-plus-face region before passing as ref. Prompt text: "Ixtli, elderly Aztec high priest, wearing penacho headdress" — no further headdress description. Model must infer headdress shape exclusively from the cropped ref.
- **Shot 3B (Control — full-ref variant):** Same prompt as 3A, identical sparse text. Runner passes the full Shot 1 image (uncropped) as reference. No other difference.

**Observable target dimensions (pre-registered):**
1. Left-fan dominance: does the headdress fan visibly higher/wider on the left than the right?
2. Crown lean direction: does the headdress apex lean rightward (away from the viewer's left)?
3. Quetzal feather cascade direction: do the long tail feathers curve leftward from the apex?
4. Overall silhouette fidelity: naive viewer test — does the headdress look like the same specific headdress as in the reference crop?

**Palette:** Jade green (quetzal feathers, bead pectoral, mosaic band) + terracotta (robe embroidery, stone temple, torch flames) + deep teal (night sky) + amber (brazier uplighting on skin and costume). High chromatic saturation, deep shadows with warm fill.

**Model:** Nano Banana Pro.

**Domain:** Game concept art.

## Recommended Runner inputs

1. Generate Shot 1 first (full plaza scene) using the scenario description — this becomes the reference image pool.
2. **Crop operation (3A):** Extract from Shot 1 the bounding box containing the headdress and Ixtli's face/shoulders. The crop should include the full headdress height with ≤20% surrounding negative space. Save as `shot1-crop-headdress.png`.
3. Generate Shot 3A using `shot1-crop-headdress.png` as reference. Prompt text (sparse): `"Ixtli, elderly Aztec high priest, wearing penacho headdress. Game concept art, jade and terracotta palette, dusk lighting."`
4. Generate Shot 3B using the full Shot 1 image (uncropped) as reference. Exact same prompt text as 3A.
5. Log the crop coordinates used for Shot 3A.
6. Judge both on the 4 observable dimensions vs the crop reference.

## Pre-registered pass criteria

Criterion 1 (Target silhouette fidelity): 3A must match the headdress reference on ≥3 of the 4 observable dimensions above. 3B must fail or be weaker on ≥2 of those same dimensions.

Criterion 2 (Causal control): The prompt text is identical for 3A and 3B; the only variable is reference type (crop vs full). Runner log must confirm this.

Criterion 3 (Comparative judgment — the PASS gate): 3A beats 3B on ≥3 of 4 observable dimensions, including overall silhouette fidelity. A tie on any dimension scores for neither.

**Overall:** PASS if Criterion 3 is met (3A wins ≥3/4 dims incl. overall). PARTIAL if 3A wins exactly 2/4 dims. FAIL if 3A wins <2/4 dims or if Criterion 2 is violated (refs were not actually controlled).
