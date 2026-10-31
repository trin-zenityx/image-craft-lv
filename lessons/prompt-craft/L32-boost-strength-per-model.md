---
id: L32
title: Body/figure emphasis must be re-calibrated per model — NB 2.1 needs the STRONG block
theme: prompt-craft
added: LV 2.15
status: active
---

# L32 — Figure-emphasis wording is model-specific; re-calibrate when you switch models

## Observation

Ploy's clean-studio set (5 plates) was generated twice with the **same prompt and the same 4 refs**, once on
`nano-banana-pro` and once on `nano-banana-2-1` (2026-10-31). The Pro set honoured the bust-forward brief; the
2.1 set rendered a visibly slimmer, flatter figure on every plate — worst on the 90° side profile, where the
chest barely projected past the ribcage.

Re-running 2.1 with a strengthened BODY_BOOST block (nothing else changed) restored the brief on all five, and
the side profile went from the weakest plate to equal-or-better than Pro.

## Rule

**When you switch image models, figure/anatomy emphasis is NOT portable — re-test and re-calibrate it.** A block
that reads "strong enough" on one model can read as a mild suggestion on another.

The calibrated block that works (keep verbatim, swap the fabric word):

> BODY_BOOST (signature — must read UNMISTAKABLY, this is the brief): a VERY FULL, heavy, voluptuous large bust
> as the single most prominent feature of the figure, noticeably fuller than a slim model's — a deep, clearly
> defined décolletage with a visible cleavage line where the plunging neckline opens. Dramatic hourglass: the
> very full chest and rounded hips contrast a tightly cinched narrow waist. The silk is stretched taut across the
> full chest and falls away from it, so the volume of the bust is obvious in the silhouette. NOT slim-chested,
> NOT athletic-flat, NOT a petite runway figure.

Three ingredients do the work — all three are needed:
1. **Superlative + comparison** — "VERY FULL … noticeably fuller than a slim model's" (plain "full, voluptuous"
   under-delivers).
2. **Explicit negatives** — "NOT slim-chested, NOT athletic-flat, NOT a petite runway figure".
3. **Geometry, not adjectives** — how the fabric behaves and what the silhouette does; per pose, add
   "in this side view the chest projects clearly and roundly forward of the ribcage" or "she leans toward the lens
   so the neckline falls open".

## Caveat (why this is safe now)

Pushing figure emphasis used to drift the face (Mila Vol 02, Ploy G3). It did **not** here because the prompt ran
with a 4-ref identity lock (master + portrait + character sheet + wardrobe anchor) plus the anti-glam FACE_LOCK
clause. Strong body wording is safe **only** behind a strong ref lock — with 1–2 refs, expect the old drift.

## Origin

Ploy NOCTURNE clean-studio set, 2026-10-31 · three-way board `Ploy_nocturne_concepts/compare_pro_vs_nb21.html`
(Pro | 2.1 mild | 2.1 strong) · Trin: "ปรับไปใช้ เวอร์ชั่น NB 2.1 · คำแรงขึ้น เลยครับ".
