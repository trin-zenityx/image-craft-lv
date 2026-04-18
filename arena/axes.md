# Axes of Scenario Diversity

> A scenario must flip ≥3 of these 9 axes from the DHYANA baseline.
> An arena trial counts as a distinct project only if its axis
> fingerprint differs from every prior arena trial for the same lesson
> on ≥2 of 9 axes.

## The 9 axes

| # | Axis | Example values | DHYANA value |
|---|------|----------------|--------------|
| 1 | Character demographics | age, gender, ethnicity, body type | adult Tibetan Buddhist monk |
| 2 | Aesthetic/era | cyberpunk, medieval, period piece, surreal, pastoral realism, retrofuturism | sci-fi-spiritual |
| 3 | Narrative genre | drama, thriller, horror, slice-of-life, documentary, editorial, action | drama |
| 4 | Palette family | warm earth, cool teal, high-contrast mono, neon pastel, muted desaturated | cyan + amber |
| 5 | Model target | Nano Banana Pro, NB 2, Midjourney, Flux | Nano Banana Pro |
| 6 | Output modality | single hero shot, 3-shot set, 12-shot storyboard, character sheet, magazine spread | 25-shot storyboard |
| 7 | Cultural context | Western, East Asian, South Asian, Middle Eastern, African, Latin American | East Asian-spiritual |
| 8 | Scale | single image, small set (2–5), medium set (6–15), large set (16+), series | large set |
| 9 | Domain | film still, game concept, editorial, commercial product, architectural viz | film still |

## DHYANA fingerprint (the origin to avoid re-running)

```
char=adult-tibetan-monk; era=sci-fi-spiritual; genre=drama;
palette=cyan-amber; model=nano-banana-pro; modality=large-storyboard;
culture=east-asian-spiritual; scale=large-set; domain=film-still
```

## Axis-flip requirements

**For a scenario to be admitted:**
1. It flips ≥3 axes from the DHYANA fingerprint.
2. For each prior arena trial of the **same lesson**, it flips ≥2 axes
   from that trial's fingerprint.
3. Generator documents the flipped axes explicitly in `scenario.md`
   under a section titled "Axis fingerprint".

## Anti-reuse enforcement

The Generator must read `scenario-bank/README.md` before proposing a
new scenario. If the proposed fingerprint violates rule 2 above, the
Generator must re-propose or report BLOCKED.

## Examples

**Example 1 — tests L01 (ref chains):**
- Korean Joseon-period drama, palace court, 6 shots, warm earth palette,
  Midjourney, medium set, East Asian secular, period film still.
- Flipped axes vs DHYANA: era, genre, palette, model, modality (5 flipped). ✅

**Example 2 — tests L06 (distinguishable characters):**
- Cyberpunk Mumbai street market, 2 rival vendors who must read as
  clearly different people, 4 single hero shots, neon pastel, Flux,
  South Asian, small set, editorial.
- Flipped axes: era, culture, model, genre, modality, domain (6 flipped). ✅

**Example 3 — tests L09 (crop refs):**
- Medieval fantasy character sheet, single character in 6 poses, muted
  earth palette, Nano Banana 2, Western, series, game concept.
- Flipped axes: era, genre, palette, modality, domain (5 flipped). ✅

## Why 9 axes

Fewer axes → Generator easily produces near-duplicates.
More axes → combinatorial explosion and Generator struggles with coherence.
9 is a reasonable compromise covering the dimensions where image-gen
failures tend to cluster (character, style, palette, scale, cultural
norms, model idiosyncrasies).
