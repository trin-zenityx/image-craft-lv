# Criteria — Trial 2026-04-17-L09-S01
# Scenario: Vintage Radio on a 1920s General-Store Shelf

> Derived from `arena/criteria/L09-criteria.md`, filled in with
> concrete thresholds for this specific scenario.

## What L09 claims (under test)

Cropping a reference image to contain only the target element gives
the model an unambiguous anchor. Passing the full scene as a reference
dilutes the signal and produces drift in the target element's shape or
markings.

---

## Criterion 1: Target element match

**Target element:** The Radiola Model 8 tabletop radio — specifically:
- Overall silhouette: compact rounded-rectangular Bakelite cabinet
- Dial: single large circle, centered on the front face
- Grille: woven cloth occupying the lower 40% of the front face, color burgundy
- Trim: ivory/cream pinstripe at cabinet edges

**What to compare:** Shot 3 (hero product, radio filling ~80% of frame)
and Shot 4 (dial close-up) against Shot 1 (wide establishing shot,
radio ~8% of frame width).

**Pass:** In BOTH shots 3 and 4, a naive viewer looking at the radio
at a similar zoom level to Shot 1 can confirm:
- The cabinet is rounded-rectangular (not oval, not boxy square)
- The dial is a single large circle centered on the front panel
- The grille cloth is visible and reads as dark reddish/burgundy
- No major new features are introduced (extra dials, different grille
  shape, changed proportions)

**Partial:** One of shots 3/4 passes the above checks and the other
shows one minor drift (e.g., grille color shifts to brown, or trim is
missing but silhouette and dial are correct). Maximum one partial
allowance.

**Fail:** In EITHER shot 3 or 4:
- The cabinet silhouette is clearly wrong (egg-shaped, boxy, elongated
  beyond recognition)
- The dial is not centered, is absent, or multiplied into multiple dials
- The grille is absent or occupies a different position/proportion
- The model introduced a different prop entirely

---

## Criterion 2: Crop evidence in Runner log

**What to check:** The Runner's working transcript, log, or submitted
files must show evidence that a cropped sub-image of Shot 1 was created
and used as the primary reference when generating shots 3 and/or 4.

**Pass:** Runner log or file list includes:
- A distinct cropped image file (e.g., `shot1-radio-crop.png` or
  equivalent), AND
- That file (or an explicit reference to it) is passed as the reference
  input for at least shots 3 and 4

**Partial:** Runner references the crop in natural language within the
prompt (e.g., "I will mentally focus on the radio region") but does not
produce a separate cropped image file. Counts as partial — the lesson's
mechanical step (actual crop operation) was not applied even if intent
was correct.

**Fail:** Runner passes the full Shot 1 image as the sole reference for
shots 3 and 4 with no crop step documented or performed.

---

## Overall verdict

| Criterion 1 | Criterion 2 | Overall |
|-------------|-------------|---------|
| Pass        | Pass        | **PASS** |
| Pass        | Partial     | **PARTIAL** — lesson intent understood, technique not executed |
| Pass        | Fail        | **PARTIAL** — output lucky but process incorrect |
| Partial     | Pass        | **PARTIAL** — technique applied but result drifted |
| Partial     | Partial     | **FAIL** |
| Fail        | Pass        | **FAIL** — crop applied but didn't help or wrong target |
| Fail        | Partial     | **FAIL** |
| Fail        | Fail        | **FAIL** |

**Hard rule:** If Criterion 1 is Fail, the overall verdict is Fail
regardless of Criterion 2.

---

## Judge notes

- The Radiola in Shot 1 will be small by design (~8% of frame). Judge
  should zoom in on Shot 1 to confirm the radio's shape before comparing
  to shots 3/4. The comparison is silhouette + dial + grille; exact
  texture reproduction is not required.
- Shot 4 (dial close-up) shows a subset of the radio; Judge evaluates
  it only for dial placement and grille cloth color, not full silhouette.
- Criterion 2 is verified by reading the Runner's submitted transcript
  or file manifest, not by inspecting image metadata.
- Skeptic question: "Was the crop step necessary?" The expected answer
  is Yes — Shot 1's radio is small enough that without cropping, the
  model receives far more visual signal from the shelves, canned goods,
  and character than from the radio itself.
