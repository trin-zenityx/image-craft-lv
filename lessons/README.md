# Lessons Library Index

> Themed roster of every lesson. Sister file: `../VALIDATION_LEDGER.md` for the cross-project pass/fail log.

## Status summary

- **Validated:** 1 (L09)
- **Pending:** 11 (+L12 new 2026-04-17)
- **Retired:** 0

## By theme

### Consistency (3)
- [L01 — Reference chains beat text-only for multi-shot sets](consistency/L01-ref-chains.md) · macro · pending 1/5
- [L03 — Opaque vs transparent container surfaces must match across the set](consistency/L03-opaque-transparent.md) · meso · pending 1/3
- [L08 — Palette consistency within same world/time must be explicit](consistency/L08-palette-consistency.md) · meso · pending 1/3

### References (3)
- [L05 — Back-view character refs cannot lock face identity](references/L05-back-view-refs.md) · meso · pending 0/3
- [L09 — Crop reference images to isolate the target element](references/L09-crop-refs.md) · meso · **validated** 2.5/3 (1 DHYANA pass + 1 arena partial + 1 arena pass across 3 projects)
- [L11 — Tier 1 refs must be designed for video continuity, not just standalone beauty](references/L11-video-continuity-refs.md) · macro · pending 0/5
- [L12 — Dual-ref (crop + full-scene) locks target AND scene context](references/L12-dual-ref-for-context.md) · meso · pending 0/3 (origin arena:S04)

### Orientation (1)
- [L02 — Face orientation inside containers must be explicit](orientation/L02-face-orientation.md) · meso · pending 1/3

### Character (1)
- [L06 — Different characters in similar contexts must be made visibly distinct](character/L06-distinguishable-characters.md) · meso · pending 1/3

### Delivery (1)
- [L07 — Deliverables must be packaged as reviewable artifacts](delivery/L07-reviewable-artifacts.md) · macro · pending 1/5

### Workflow (1)
- [L04 — Self-review before showing output prevents obvious failures](workflow/L04-self-review-protocol.md) · macro · pending 0/5

### Model-limits (1)
- [L10 — Recognize prominence floor; stop diminishing-return regens](model-limits/L10-prominence-floor.md) · macro · pending 1/5

## Retrieval cheatsheet

| Task | Load |
|------|------|
| Multi-shot character/location | `consistency/*` + `character/*` + `orientation/*` |
| Using refs | `references/*` |
| Shipping a batch | `delivery/*` |
| First gen of a session | `workflow/L04` (always) |
| Hard-to-render element | `model-limits/*` |

## Where to write new lessons

Copy `../templates/lesson-template.md`, place under the matching theme folder, name `L##-short-title.md`. Then:
1. Append a row to `../VALIDATION_LEDGER.md` for every application.
2. Mirror that row into the lesson's own Validation log.
3. When the validation threshold is met (see `../CHANGELOG.md` for promotion rules), promote and bump LV.
