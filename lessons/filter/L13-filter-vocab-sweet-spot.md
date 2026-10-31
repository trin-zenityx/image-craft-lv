---
id: L13
title: "[MIGRATED] Filter-word tier registry → filter-craft-lv/VOCAB.md"
theme: filter
status: migrated
migrated_at_lv: 2.13
related: [L17, L18]
---

# L13 — MIGRATED to `filter-craft-lv`

The filter-word **tier registry** (Tier 0/1/2/3 · single source of truth for
Google/Imagen prompt-token triggers) now lives in its own cross-cutting skill:

→ **`filter-craft-lv/VOCAB.md`**

Why: the filter system spans execution (error classification + retry) AND
prompt-craft (vocab), is used by image/kie/seedance/photobook alike, and has a
growable artifact (the vocab table) that should evolve on its own cadence.
See `filter-craft-lv/CHANGELOG.md` LV 1.0 (2026-05-29).

For any sexy / revealing / edgy wardrobe prompt: invoke **filter-craft-lv**.
