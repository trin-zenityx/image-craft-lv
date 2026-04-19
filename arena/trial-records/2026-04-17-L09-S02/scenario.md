# Scenario S02 — Iron Tsuba, Workshop Light

## Goal

Prove that cropping a wide-scene reference to isolate a small target object produces measurably better element-lock than using the full-scene reference — by comparing Shots 3A (crop-ref) and 3B (full-ref) of the same target under identical text prompts.

## Axis fingerprint

```
char=young-japanese-male-artisan; era=feudal-japan; genre=documentary;
palette=muted-indigo-ochre; model=nano-banana-pro; modality=single-hero-pair;
culture=east-asian-secular; scale=small-set; domain=editorial
```

## Flipped axes vs DHYANA

| # | Axis | DHYANA value | S02 value | Flipped? |
|---|------|-------------|-----------|----------|
| 1 | char | adult-tibetan-monk | young-japanese-male-artisan | YES |
| 2 | era | sci-fi-spiritual | feudal-japan | YES |
| 3 | genre | drama | documentary | YES |
| 4 | palette | cyan-amber | muted-indigo-ochre | YES |
| 5 | model | nano-banana-pro | nano-banana-pro | no |
| 6 | modality | large-storyboard | single-hero-pair | YES |
| 7 | culture | east-asian-spiritual | east-asian-secular | YES |
| 8 | scale | large-set | small-set | YES |
| 9 | domain | film-still | editorial | YES |

**Flipped vs DHYANA: 7 axes (char, era, genre, palette, modality, culture, scale, domain).** Requirement ≥3 — satisfied.

## Flipped axes vs prior scenarios for L09

**Prior L09 scenario:** 2026-04-17-L09-S01
```
char=middle-aged-white-female-shopkeeper; era=1920s-art-deco; genre=slice-of-life;
palette=warm-earth; model=nano-banana-pro; modality=small-4-shot-set;
culture=western; scale=small-set; domain=commercial-product
```

| # | Axis | S01 value | S02 value | Flipped? |
|---|------|-----------|-----------|----------|
| 1 | char | middle-aged-white-female-shopkeeper | young-japanese-male-artisan | YES |
| 2 | era | 1920s-art-deco | feudal-japan | YES |
| 3 | genre | slice-of-life | documentary | YES |
| 4 | palette | warm-earth | muted-indigo-ochre | YES |
| 5 | model | nano-banana-pro | nano-banana-pro | no |
| 6 | modality | small-4-shot-set | single-hero-pair | YES |
| 7 | culture | western | east-asian-secular | YES |
| 8 | scale | small-set | small-set | no |
| 9 | domain | commercial-product | editorial | YES |

**Flipped vs S01: 7 axes (char, era, genre, palette, modality, culture, domain).** Requirement ≥2 — satisfied.

---

## Scenario description

**Setting.** A traditional Japanese sword-fittings workshop (tosogu-ya), Edo period. A single low table dominates the foreground. Iron and shakudo fittings are arranged along the near edge of the table. Natural light filters through shoji screens — soft, directionless, with an ochre cast from aged paper. Indigo-dyed cloth wraps several completed pieces.

**Character.** Kenji, a young Japanese male artisan (mid-twenties), lean, ink-stained fingers, wearing a plain indigo kosode and a leather apron. He is not the visual target — he provides human scale and documentary authenticity. He should read as focused and calm, not theatrical.

**The target element.** An iron tsuba (sword hand guard) with a dragon cutout motif, approximately 8 cm across, resting on the table near the right foreground. It appears in Shot 1 but occupies roughly 6–9% of the frame width — small, but its cutout silhouette is distinctive. **Text description in all prompts must remain:** "the iron tsuba with a dragon cutout" — nothing more. No color, no patina details, no dimensions.

**Why this tests L09.** The tsuba's dragon cutout is a specific, intricate silhouette — open negative space, curved serpentine body, discrete claw forms. A full-scene reference will give the model many competing visual signals (tools, cloth, other fittings, Kenji's figure). A tight crop of the tsuba fills the frame with only the cutout, making the silhouette 100% loud. Shots 3A and 3B are generated with identical sparse text; the only variable is which reference is passed. If the lesson is valid, 3A (crop-ref) will show a closer silhouette match to Shot 1's tsuba than 3B (full-ref).

**Palette.** Muted indigo-ochre: aged iron (near-black), warm wood, ochre paper light, indigo cloth accents. No saturated color. Slight desaturation overall.

**Era / mood.** Feudal Japan, documentary register — as if photographed by a still camera with a long lens inside the workshop. Quiet, observational, no stylized drama.

---

## Shot list

### Shot 1 — Wide workshop scene (source for crop)
- **Frame:** wide shot, full table visible, Kenji at work in mid-ground
- **Key element:** the iron tsuba with a dragon cutout sits on the right foreground of the table, occupying ~6–9% of frame width
- **Purpose:** establishes the scene; this image will be cropped to produce the crop-ref for Shot 3A
- **Reference:** none (first generation, no ref image)
- **Text prompt discipline:** Runner may describe the workshop and Kenji normally; describe the tsuba as "the iron tsuba with a dragon cutout" only

### Shot 2 — Medium context shot
- **Frame:** medium shot, Kenji's hands close on a piece of cloth, tsuba visible but not dominant
- **Purpose:** establishes human scale and workshop texture; provides secondary scene context
- **Reference:** Shot 1 as scene-consistency ref (full scene acceptable here — we are not anchoring the tsuba in this shot)
- **Text prompt discipline:** same sparse tsuba description if tsuba appears

### Shot 3A — Tsuba hero close-up, CROP-REF (L09 technique applied)
- **Frame:** tight close-up of the tsuba filling the frame, shallow depth of field, table texture visible
- **Purpose:** L09 technique shot — uses the cropped version of Shot 1 (tsuba isolated) as primary reference
- **Reference (primary):** crop of Shot 1, tightly framing the tsuba only — Runner must produce this crop (PIL/ImageMagick) before calling the model
- **Text prompt:** "the iron tsuba with a dragon cutout" — no further description of design, dimensions, or patina
- **Edit-style language:** Runner should use reference-lock language ("match the tsuba in the reference exactly", "preserve the hand guard shape from the reference")

### Shot 3B — Tsuba hero close-up, FULL-REF (naive control)
- **Frame:** identical framing goal as 3A (tight close-up of the tsuba)
- **Purpose:** control condition — same scene, same sparse text, but full Shot 1 used as sole reference (no crop)
- **Reference (primary):** Shot 1 at full resolution, unmodified
- **Text prompt:** identical to 3A — "the iron tsuba with a dragon cutout" — word for word
- **Edit-style language:** identical to 3A — same reference-lock phrasing
- **IMPORTANT:** the ONLY variable between 3A and 3B is the reference image. Everything else — text prompt, model, generation parameters, framing intent — must be held constant.

---

## Recommended Runner inputs

1. **Generate Shot 1** (wide workshop scene) — no ref. Record the full-resolution output.
2. **Generate Shot 2** (medium context) — Shot 1 as scene-ref (full image acceptable).
3. **Produce the crop-ref:** Using PIL or ImageMagick, crop Shot 1 to isolate the tsuba. The crop must contain only the tsuba (and a small margin). Save as `images/shot1-tsuba-crop.png`.
4. **Generate Shot 3A** — use `images/shot1-tsuba-crop.png` as primary reference. Sparse text only: "the iron tsuba with a dragon cutout". Edit-style reference-lock language.
5. **Generate Shot 3B** — use Shot 1 full image as primary reference. Identical text and reference-lock language to 3A. Save alongside 3A for direct Judge comparison.
6. Log the crop dimensions and source coordinates in `runner-log.md`.

---

## Pre-registered pass criteria

*(Full detail in `criteria.md`.)*

- **Criterion 1 (element match — 3A vs reference):** The tsuba's dragon-cutout silhouette in Shot 3A must match the tsuba visible in Shot 1's crop to a standard defined in criteria.md.
- **Criterion 2 (causal comparison — 3A vs 3B):** Shot 3A must show measurably better dragon-cutout silhouette fidelity than Shot 3B. If 3A and 3B are indistinguishable, the trial fails regardless of Criterion 1 outcome.

**Overall:** Pass only if both criteria pass. Criterion 2 failure = trial fail (lesson not proven necessary).
