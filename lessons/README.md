# Lessons Library Index

> Themed roster of every lesson. Sister file: `../VALIDATION_LEDGER.md` for the cross-project pass/fail log.

## Status summary

- **Validated:** 2 (L09, L13)
- **Pending:** 19
- **Needs-rerun:** 1 (L15 · attribution unclear, demoted from pending 2026-05-05)
- **Retired:** 0

## By theme

### Consistency (3)
- [L01 — Reference chains beat text-only for multi-shot sets](consistency/L01-ref-chains.md) · macro · pending 2/5
- [L03 — Opaque vs transparent container surfaces must match across the set](consistency/L03-opaque-transparent.md) · meso · pending 1/3
- [L08 — Palette consistency within same world/time must be explicit](consistency/L08-palette-consistency.md) · meso · pending 1/3

### References (4)
- [L05 — Back-view character refs cannot lock face identity](references/L05-back-view-refs.md) · meso · pending 0/3
- [L09 — Crop reference images to isolate the target element](references/L09-crop-refs.md) · meso · **validated** 2.5/3 (1 DHYANA pass + 1 arena partial + 1 arena pass across 3 projects)
- [L11 — Tier 1 refs must be designed for video continuity, not just standalone beauty](references/L11-video-continuity-refs.md) · macro · pending 1/5 *(+ Jira/Mila evidence 2026-05-05)*
- [L12 — Dual-ref (crop + full-scene) locks target AND scene context](references/L12-dual-ref-for-context.md) · meso · pending 0/3 (origin arena:S04)

### Orientation (1)
- [L02 — Face orientation inside containers must be explicit](orientation/L02-face-orientation.md) · meso · pending 1/3

### Character (3)
- [L06 — Different characters in similar contexts must be made visibly distinct](character/L06-distinguishable-characters.md) · meso · pending 1/3
- [L14 — Identity-marker mention (mole/tattoo) → AI multiplies; drop and let ref carry it](character/L14-identity-marker-multiplication.md) · meso · pending 1/3 *(added 2026-05-01)*
- [L23 — Face EXPRESSION as separate prompt block with "NOT hard" anti-pattern](character/L23-face-expression-as-separate-block.md) · meso · pending 1/3 *(added 2026-05-05)*

### Delivery (2)
- [L07 — Deliverables must be packaged as reviewable artifacts](delivery/L07-reviewable-artifacts.md) · macro · pending 1/5
- [L16 — Local boards: defer to `internal-board-builder` skill for primitives](delivery/L16-local-board-originals.md) · meso · pending 2/3

### Workflow (2)
- [L04 — Self-review before showing output prevents obvious failures](workflow/L04-self-review-protocol.md) · macro · pending 0/5 · **expanded 2026-05-01 with edge-artifact + back-view-ID + P2-vs-P3 angle audit checks**
- [L18 — Filter blocks don't cost credits → retry 3-5× as diagnostic before modifying prompt](workflow/L18-filter-retry-diagnostic.md) · meso · pending 1/3 *(added 2026-05-05)*

### Model-limits (1)
- [L10 — Recognize prominence floor; stop diminishing-return regens](model-limits/L10-prominence-floor.md) · macro · pending 1/5

### Filter (3) — *L13/L14/L15 added 2026-05-01 · L17 added 2026-05-05*
- [L13 — Filter-vocab sweet spot for sexy/revealing wardrobe (halter knot-front V-neck)](filter/L13-filter-vocab-sweet-spot.md) · meso · **validated** 2/3 *(promoted 2026-05-05 with Alisa cross-project pass)*
- [L15 — Master-only ref bypass](filter/L15-master-only-ref-bypass.md) · meso · **needs-rerun** *(demoted 2026-05-05 — attribution unclear; see L17)*
- [L17 — Filter triggers on prompt text, not on ref image content (Google / Imagen)](filter/L17-filter-text-not-ref.md) · meso · pending 1/3 *(added 2026-05-05)*

### Pose (1) — *added 2026-05-05*
- [L19 — Narrative pose per plate beats generic framing templates](pose/L19-narrative-pose-per-plate.md) · meso · pending 1/3

### Camera (1) — *added 2026-05-05*
- [L20 — Camera body + film stock specificity beats lens-only spec](camera/L20-camera-body-film-stock.md) · meso · pending 1/3

### Aesthetic (1) — *added 2026-05-05*
- [L21 — Designer / aesthetic reference choice drives mood and polish](aesthetic/L21-designer-aesthetic-mood.md) · meso · pending 1/3

### Prompt-craft (1) — *added 2026-05-05*
- [L22 — Anti-overproduction directives = calibration tool, not blanket switch](prompt-craft/L22-anti-overproduction-calibration.md) · meso · pending 1/3

## Retrieval cheatsheet

| Task | Load |
|------|------|
| Multi-shot character/location | `consistency/*` + `character/*` + `orientation/*` |
| Using refs | `references/*` |
| Shipping a batch | `delivery/*` |
| First gen of a session | `workflow/L04` (always) + `workflow/L18` for filter handling |
| Hard-to-render element | `model-limits/*` |
| Sexy/revealing wardrobe (bikini, lingerie, glamour) | `filter/L13` + `filter/L17` + `workflow/L18` + `character/L14` |
| Real-person with distinctive marker (mole, scar) | `character/L14` |
| Editorial / glamour / photobook (naturalness) | `pose/L19` + `camera/L20` + `aesthetic/L21` + `prompt-craft/L22` + `character/L23` |
| Multi-plate set with pose variety required | `pose/L19` (narrative pose per plate) |

## Where to write new lessons

Copy `../templates/lesson-template.md`, place under the matching theme folder, name `L##-short-title.md`. Then:
1. Append a row to `../VALIDATION_LEDGER.md` for every application.
2. Mirror that row into the lesson's own Validation log.
3. When the validation threshold is met (see `../CHANGELOG.md` for promotion rules), promote and bump LV.
