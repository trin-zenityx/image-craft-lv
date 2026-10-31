---
id: L09
title: Crop reference images to isolate the target element
theme: references
added_at_lv: 1.0
tags: [reference-image, cropping, edit-mode, target-anchor]
created: 2026-04-16
last_updated: 2026-04-16
supersedes: []
related: [L01, L05, L12]
---

# L09 — Crop reference images to isolate the target element

## TL;DR

When a ref must lock ONE specific element (object, pose, color), crop it so that element fills the frame. Full-scene refs dilute the anchor.

## Context

DHYANA #07 pod detail — multiple regen attempts (v3, v4, v5, v6) all used the full pod corridor image (#06) as reference. Each regen produced pods with different shapes — a bulgy egg, a compact head-only capsule, a disproportioned hybrid — none matched the sleek elongated capsule shape visible in #06.

## Mistake

Passed the entire corridor image as ref when only ONE specific object needed to be matched exactly. The model had too much visual information (corridor, water, multiple pods at various angles, background racks) and couldn't decide which element was the "target". It reinterpreted pod shape each generation.

## Why it happened

Treated "use reference" as "pass the related image". Did not consider that the ref's job is to anchor a specific visual element, and including unrelated elements dilutes that anchor.

## Fix

When a ref needs to lock ONE element (specific object, specific pose, specific color), crop the source image to contain ONLY that element. Use PIL/ImageMagick to extract the tight region. Pass the crop as the primary ref. This gives the model an unambiguous visual target.

## Broader rule

A reference image teaches the model what it shows, in proportion to how much of the frame that thing occupies. If the pod is 10% of a scene ref, the pod design is 10% "loud" to the model. If the pod fills the frame of a cropped ref, it is 100% loud.

## Scope limits (added from arena:S04 findings)

**L09 alone is NOT sufficient when the new shot is wider than the crop.** A crop-only ref anchors the target element but unanchors everything else in the frame — model re-imagines bg/character/palette from text prior. For shots that include surrounding context, **combine L09 with L12 (dual-ref)**: pass both the crop and the full-scene source.

**Crop resolution matters.** Arena:S04 found that small crops (< output resolution, e.g. 353×512px feeding a 4K hero shot) can fail to convey fine target detail even when the crop correctly isolates the element. Rule of thumb: **the crop's long side should be ≥ ½ of the output's long side**. Use the native-resolution crop of Shot 1 when possible; downscale the crop only when the generated shot is similarly small.

## Cross-references

- Related lessons: L01 (ref chains), L05 (back-view refs), **L12 (dual-ref — use together when new shot wider than crop)**
- Checklist items affected: pre-submit C.1, C.3

## Related technique

Per research, Nano Banana Pro treats reference images with edit-style prompting ("match THIS exactly", "preserve the pod in the reference") more restrictively than generation-style prompting ("in the style of..."). Combine cropped refs with edit-style language when you need exact matching.

## Reinforcement (added 2026-05-04 from Mila Power Suit session)

**Center the crop on the actual feature — don't use fixed-percentage coordinates from image edges.**

A common mistake when applying L09 to face-cropping (per L17, L18, character-sheet-builder L18): using formulaic coordinates like `left=20%`, `top=10%`, `width=55%`, `height=30%` from image edges. This produces an off-center crop where the face takes only ~40% of the frame and 30% is empty background.

**Effect of off-center crop:**
- Face dominance in frame: ~40% (weak identity signal)
- AI gets ambiguous anchor — must choose between empty-frame interpretation and the actual face
- Even when paired with master full-body ref, the face-crop's signal is diluted

**Correct approach:**
1. **Estimate the feature's center** in the source image (for portraits: face center ≈ x:50%, y:18-25% from top)
2. **Crop around that center**, not from image edges
3. Aspect ratio: 3:4 portrait works well for face+shoulders refs
4. Verify after cropping: face should fill ≥60% of crop area, centered

**Python pattern (validated):**
```python
from PIL import Image
img = Image.open(master_path)
w, h = img.size

# Estimate face center for typical portrait
face_x = int(w * 0.50)  # horizontally centered
face_y = int(h * 0.22)  # eye-line at ~22% from top

# Crop dimensions (face+shoulders)
crop_w = int(w * 0.55)
crop_h = int(crop_w * 4 / 3)  # 3:4 portrait

# Center crop on face point
left = max(0, face_x - crop_w // 2)
top = max(0, face_y - int(crop_h * 0.40))  # 40% above center, 60% below

face_crop = img.crop((left, top, left + crop_w, top + crop_h))
```

**Validated on:** Mila Power Suit master_face_crop v2 (2026-05-04). v1 used fixed-percentage coords → off-center, face at right portion of frame, ~30% empty space on left → may have contributed to identity drift in plates that used it. v2 face-centered → cleaner anchor.

**Skill-level implication:** When a downstream lesson (L17, L18, character-sheet-builder L18) prescribes "use master_face_crop", it implicitly requires this centered-crop discipline. Off-center crops violate the spirit of L09.
