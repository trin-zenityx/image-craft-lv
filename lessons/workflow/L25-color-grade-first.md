---
id: L25
title: For color/tone drift only, color-grade first (sips / ImageMagick) before regenerating
theme: workflow
tier: micro
status: pending
validation: 1/1
tags: [color-grading, sips, imagemagick, post-processing, regen-cost-avoidance, tone-drift]
origin_project: tara-sun-and-water-vol04
created: 2026-05-07
last_updated: 2026-05-07
supersedes: []
related: [L18, L24]
---

# L25 — For color/tone drift only, color-grade first (sips / ImageMagick) before regenerating

## TL;DR

When a plate's only problem is **color/tone drift** (white balance, saturation, warm/cool balance) and EVERYTHING ELSE is correct (composition, face identity, pose, wardrobe, framing, lighting direction) — try **color grading the existing image first** with `sips` or ImageMagick. Only if grading can't reach the target should you regen.

## When this lesson applies

✅ **Use color-grade first when:**
- Composition is correct
- Face identity is correct (most important)
- Pose is correct
- Wardrobe is correct
- Lighting direction is correct
- ONLY color temperature / hue / saturation / warm-cool balance is off

❌ **DO NOT use color-grade first when:**
- Face has drifted (regen with stronger FACE_LOCK per L23)
- Pose is wrong (regen with revised POSE block)
- Wardrobe color or style is wrong (regen — color-grade can shift palette but not change a slip dress to a halter top)
- Composition / framing is wrong (regen)
- Subject is the wrong person (regen)

If face/pose/wardrobe is ALSO wrong, regen wins because color grading the wrong image still yields the wrong image.

## Why this matters (cost framing)

| Approach | Wall time | API cost | Risk of new bugs |
|---|---|---|---|
| Color grade with `sips` or `magick` | ~5-30 sec | $0 | Low — only color shifts |
| Regen 3 parallel | ~3-5 min | $0.18 (3× $0.06, 1 winner kept) | High — face/pose may drift |
| Regen 5 parallel | ~3-5 min | $0.30 | High |

For color-only fixes, regen is **expensive AND risky** because the model's stochastic identity-rendering may drift face / pose / framing while you were only trying to warm up the background.

## Tooling

### `sips` (macOS built-in, no install)

Limited but always available. Best for:
- Format conversion (already used heavily for thumbnail / web JPEGs)
- Crop, resize
- Limited color-profile assignment

Limitations: `sips` does NOT support hue/saturation/curves shifts. For real grading use ImageMagick.

### ImageMagick `magick` / `convert` (install: `brew install imagemagick`)

Powerful per-pixel operations. Common color-grade recipes:

**Warm up cool/blue image:**
```bash
magick input.png -modulate 100,110,98 \
  -level 0%,100%,1.05 \
  -channel R -evaluate Multiply 1.06 \
  -channel B -evaluate Multiply 0.94 \
  +channel \
  output.png
```
- `-modulate 100,110,98` = brightness 100% / saturation 110% / hue shift -2% (slight warm-shift)
- `-level 0%,100%,1.05` = gentle gamma lift
- `-channel R/B` = boost red, reduce blue → warmer overall

**Cool down warm/orange image:**
```bash
magick input.png -modulate 100,105,102 \
  -channel R -evaluate Multiply 0.95 \
  -channel B -evaluate Multiply 1.06 \
  +channel \
  output.png
```

**Lift shadows + add warmth (twilight balance):**
```bash
magick input.png \
  -level 5%,98%,1.1 \
  -modulate 102,108,99 \
  -channel R -evaluate Multiply 1.04 \
  -channel B -evaluate Multiply 0.96 \
  +channel \
  output.png
```

**Reference-match grading (advanced):**
```bash
# Histogram match against reference
magick input.png reference.png -histogram-match output.png
```
Useful when you have a reference image (e.g., another plate from same set) whose color you want to match.

### Python (Pillow / opencv) for batch / programmatic

For programmatic grading in scripts:

```python
from PIL import Image, ImageEnhance
img = Image.open("input.png")
img = ImageEnhance.Color(img).enhance(1.10)       # +10% saturation
img = ImageEnhance.Contrast(img).enhance(1.03)    # +3% contrast
img.save("output.png")
```

For warm/cool shift in PIL:
```python
r, g, b = img.split()
r = r.point(lambda v: min(255, int(v * 1.06)))
b = b.point(lambda v: int(v * 0.94))
Image.merge("RGB", (r, g, b)).save("output.png")
```

## Decision protocol

When a plate has color/tone drift:

```
1. Diagnose: is it ONLY color/tone, or also face/pose/wardrobe?
   ↓ ONLY color
2. Backup original to .v1.png (always, never destructive)
3. Try sips / ImageMagick / Pillow grade with target curve
4. Compare graded vs target reference plate (e.g., another plate in same set)
5. If acceptable → use graded as new main; archive .v1.png
   If still off but close → iterate grade params
   If grade can't reach target without artifacts → regen as fallback
```

## Anti-patterns

- ❌ Regenerate immediately when only color drifts (wastes 3-5 min + risks new bugs)
- ❌ Color-grade when face/pose/wardrobe is also wrong (graded wrong image = still wrong)
- ❌ Apply grade without backup (always `.v1.png` backup before destructive grade)
- ❌ Over-saturate to "punch up" warmth (introduces banding / artifacts)
- ❌ Use `sips` for hue shift (doesn't support it — use ImageMagick instead)

## Validation log

| # | Project | Date | Technique | Outcome | Notes |
|---|---------|------|-----------|---------|-------|
| 1 | Tara Sun & Water Vol 04 (T03 P2) | 2026-05-07 | Originally regenerated 3 candidates with color-fix prompt; passed but spent ~5 min wall time + 3 KIE calls. Trin observation: *"รอบหน้าคุณลองเกลี่ยสีดูเองก่อนก็ได้นะ เผื่อมันได้เลย จะได้ไม่ต้องเจนใหม่"* — codified as L25. Lesson would have applied: P2 had face + composition + pose + wardrobe ALL correct, only twilight color drifted from teal+amber balance to pure sapphire blue. ImageMagick `magick -modulate -channel R/B` could likely have warmed it up in seconds. | pending validation | First instance — codified, not yet applied to a fix. Will validate next time a color-only drift appears. |

## Cross-references

- Related lessons: L18 (escalation playbook — L25 fits as a pre-R2 step for color-only issues), L24 if introduced (post-processing checklist)
- Tooling: `sips` (built-in), `magick` (brew install imagemagick), `Pillow` (pip install)
- Memory: none yet
- Checklist items affected: post-generate self-review — when reviewing a plate, classify the failure mode (face / pose / wardrobe / color) and route to the correct fix tier
