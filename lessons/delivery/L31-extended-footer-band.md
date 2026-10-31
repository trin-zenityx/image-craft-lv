---
id: L31
title: Extended footer band — a proven option for logo + info on AI posters (guide, not a rule)
theme: delivery
added_at_lv: 2.15
tags: [delivery, poster, logo-placement, compositing, typography, thai-text, canvas-extend]
created: 2026-08-12
last_updated: 2026-08-12
supersedes: []
related: [L07, L16]
---

# L31 — Extended footer band — a proven option for logo + info on AI posters

## TL;DR

When an AI-generated poster needs a real logo plus real info text (date, host, channel), **extending the canvas downward by ~12% and putting the brand band in that new strip** is a validated technique — it never fights the artwork and stays identical across a whole set. **It is one option, not the default.** Analyse each poster and decide where the brand block belongs; just know this trick exists and works.

## Context

ZenityX Catch-Up Class poster set for Hermes Agent (2026-08-12). 10 posters — 5 concepts × Nano Banana Pro and GPT-Image-2, 3:4 vertical, artwork generated clean (no logo baked in, per `zenityx-pr-lv`), then the ZenityX logo + a two-line Thai info block composited afterwards.

## Observation

Both models pushed their own headline typography to roughly 88–95% of frame height, even though every prompt asked to "keep the bottom 12–14% calm". The models honour the request as *visual* calm (dark, low-detail) but still place text there. So the planned overlay scrim would have landed straight on top of the generated headline in most of the set — and the amount of usable space differed per image, meaning per-image placement decisions and an inconsistent-looking set.

Extending the canvas instead (`new_canvas = art_height + 0.125 × art_height`, band filled `#0A0A0C`) produced: no collision with any artwork, one shared band geometry across all 10 posters, and enough room for a properly sized logo plus two lines of real Thai type.

## Technique (when it fits)

- Band height ≈ **12–13%** of the artwork height. A 3:4 artwork becomes ≈ 3:4.5 — still portrait, still fine for FB/IG feed and LINE.
- Logo trimmed to its ink bbox first (`alpha.getbbox()`), then scaled to ≈ **50% of band height**, left-aligned at ≈ 7% margin. Trimming matters — the shipped ZenityX PNGs carry large transparent padding, so an untrimmed paste looks tiny.
- Info text right-aligned in the same band: line 1 IBM Plex Sans Thai Bold (white), line 2 Sarabun SemiBold (grey). Real fonts, so Thai never comes out mangled the way in-image AI Thai can.
- A short gold rule above the band edge ties the band to the artwork instead of looking bolted on.
- Band colour near-black works over both dark artwork and a saturated red brand poster — and it gives the red X in the logo a legal backdrop (a logo can never sit on red).

## When to reach for something else

- The artwork already has a genuine calm zone (a real empty corner, a dark plate, a stage/podium surface) → place the logo **inside** the composition; an added band would waste it. Use `zenityx-pr-lv/scripts/find_logo_spot.py` to score zones.
- Aspect ratio is locked by the platform (1:1 FB post, 9:16 story, fixed ad slot) → extending changes the ratio, so overlay or regenerate instead.
- The poster is a single hero piece where the composition is the point → an added strip reads as a template.

## Broader rule

**Decide brand-block placement per poster, from the finished artwork — but keep "extend the canvas" in the toolbox.** It is the strongest option when (a) generated text crowds the bottom edge, (b) a whole set must look uniform, or (c) real-font Thai/info text must be legible and unmistakably correct. Analysis first, technique second.

## Cross-references

- Related lessons: L07 (reviewable artifacts), L16 (local board asset strategy)
- Sister skill: `zenityx-pr-lv` — §4 logo composite (analyse the image before placing; X stays red; never bake brand into the AI image)
- Validated in: Hermes Catch-Up Class poster set, 2026-08-12 (`/Volumes/Studio/active/ทำภาพทั่วไป/hermes-catchup-poster/make_final.py`)
