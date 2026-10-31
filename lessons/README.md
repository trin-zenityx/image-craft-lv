# Lessons Library Index

> Themed roster of every active lesson. One lesson per file. Archived lessons are listed at the bottom.

## Retrieval cheatsheet — load only what's relevant

| Task | Load |
|------|------|
| Multi-shot character/location | `consistency/*` + `character/*` + `orientation/*` |
| Using refs | `references/*` |
| Shipping a batch | `delivery/*` |
| First gen of a session | `workflow/L04` (always) · filter handling → skill **`filter-craft-lv`** |
| Hard-to-render element | `model-limits/*` |
| Sexy/revealing wardrobe (bikini, lingerie, glamour) | skill **`filter-craft-lv`** (vocab tiers + R1→R5 + text-not-ref) + `character/L14` |
| **"Soft Veil" named style** (Trin says "Soft Veil") | `aesthetic/L30` — filter-safe artistic-suggestive thin-fabric · apply **ONLY** on explicit request, never auto |
| Real-person with distinctive marker (mole, scar) | `character/L14` |
| Editorial / glamour / photobook (naturalness) | `pose/L19` + `camera/L20` + `aesthetic/L21` + `prompt-craft/L22` + `character/L23` |
| Multi-plate set (any) — diversity discipline | `workflow/L26` (build matrix BEFORE writing prompts) + `pose/L19` |
| Switching image model (Pro ↔ NB 2.1 ↔ GPT) · bust/figure emphasis looks weaker than the brief | `prompt-craft/L32` (re-calibrate the BODY_BOOST block; strong wording needs a 4-ref lock) |
| Lifestyle vs editorial photobook decision | `prompt-craft/L29` (recipe-classification — pick ONE vocabulary set) |
| Detail / object close-up plate | `pose/L27` (keep body anchor — never pure disembodied details) |
| Wide environmental OR motion shot | `character/L28` (face-pixel-budget — bring closer or stop motion) |
| Color drift only (composition / face / pose all correct) | `workflow/L25` (color-grade first; regen as fallback) |
| Poster / KV that needs a real logo + info text on it | `delivery/L31` (options for the brand block — analyse the finished art first) |

## Active lessons by theme

### Consistency (3)
- [L01 — Reference chains beat text-only for multi-shot sets](consistency/L01-ref-chains.md) · *added LV 1.0*
- [L03 — Opaque vs transparent container surfaces must match across the set](consistency/L03-opaque-transparent.md) · *added LV 1.0*
- [L08 — Palette consistency within same world/time must be explicit](consistency/L08-palette-consistency.md) · *added LV 1.0*

### References (4)
- [L05 — Back-view character refs cannot lock face identity](references/L05-back-view-refs.md) · *added LV 1.0*
- [L09 — Crop reference images to isolate the target element](references/L09-crop-refs.md) · *added LV 1.0*
- [L11 — Tier 1 refs must be designed for video continuity, not just standalone beauty](references/L11-video-continuity-refs.md) · *added LV 2.0*
- [L12 — Dual-ref (crop + full-scene) locks target AND scene context](references/L12-dual-ref-for-context.md) · *added LV 2.0*

### Orientation (1)
- [L02 — Face orientation inside containers must be explicit](orientation/L02-face-orientation.md) · *added LV 1.0*

### Character (4)
- [L06 — Different characters in similar contexts must be made visibly distinct](character/L06-distinguishable-characters.md) · *added LV 1.0*
- [L14 — Identity-marker mention (mole/tattoo) → AI multiplies; drop and let ref carry it](character/L14-identity-marker-multiplication.md) · *added LV 2.5*
- [L23 — Face EXPRESSION as separate prompt block with "NOT hard" anti-pattern](character/L23-face-expression-as-separate-block.md) · *added LV 2.7*
- [L28 — Distance + motion = face drift risk (face <15% of frame OR motion = identity loss)](character/L28-distance-motion-face-drift.md) · *added LV 2.12*

### Delivery (3)
- [L07 — Deliverables must be packaged as reviewable artifacts](delivery/L07-reviewable-artifacts.md) · *added LV 1.0*
- [L16 — Local boards: defer to `internal-board-builder` skill for primitives](delivery/L16-local-board-originals.md) · *added LV 2.6*
- [L31 — Extended footer band for logo + info on AI posters (guide, not a rule — analyse each poster)](delivery/L31-extended-footer-band.md) · *added LV 2.15*

### Workflow (3)
- [L04 — Self-review before showing output prevents obvious failures](workflow/L04-self-review-protocol.md) · *added LV 1.0*
- [L25 — Color-grade first (sips / ImageMagick / Pillow) before regen for color-only drift](workflow/L25-color-grade-first.md) · *added LV 2.11*
- [L26 — Diversity matrix per plate BEFORE generation (4-axis: distance / angle / pose / action)](workflow/L26-diversity-matrix.md) · *added LV 2.12*

### Model-limits (1)
- [L10 — Recognize prominence floor; stop diminishing-return regens](model-limits/L10-prominence-floor.md) · *added LV 1.0*

### Filter → migrated to skill `filter-craft-lv` (LV 2.13)
L13 (vocab tiers), L17 (filter triggers on prompt text, not refs), and L18 (R1→R5 playbook) moved into the standalone **`filter-craft-lv`** skill. `status: migrated` pointer stubs remain at `filter/L13`, `filter/L17`, and `workflow/L18`. Invoke `filter-craft-lv` for any filter / edgy-wardrobe work.

### Pose (2)
- [L19 — Narrative pose per plate beats generic framing templates](pose/L19-narrative-pose-per-plate.md) · *added LV 2.7*
- [L27 — Avoid disembodied detail shots — keep partial body context as identity anchor](pose/L27-avoid-disembodied-details.md) · *added LV 2.12*

### Camera (1)
- [L20 — Camera body + film stock specificity beats lens-only spec](camera/L20-camera-body-film-stock.md) · *added LV 2.7*

### Aesthetic (2)
- [L21 — Designer / aesthetic reference choice drives mood and polish](aesthetic/L21-designer-aesthetic-mood.md) · *added LV 2.7*
- [L30 — "Soft Veil" named style: filter-safe artistic-suggestive thin-fabric look (ON-DEMAND only)](aesthetic/L30-soft-veil.md) · *added LV 2.14*

### Prompt-craft (3)
- [L22 — Anti-overproduction directives = calibration tool, not blanket switch](prompt-craft/L22-anti-overproduction-calibration.md) · *added LV 2.7*
- [L32 — Figure-emphasis wording is model-specific; re-calibrate on a model switch (NB 2.1 needs the STRONG block)](prompt-craft/L32-boost-strength-per-model.md) · *added LV 2.15*
- [L29 — Lifestyle vs Editorial recipes — choose ONE entire vocabulary set; never mix](prompt-craft/L29-lifestyle-vs-editorial-recipes.md) · *added LV 2.12*

## Archived lessons

Stored in [`archive/`](archive/) — kept for reference, not loaded.

- [L15 — Master-only ref bypass](archive/L15-master-only-ref-bypass.md) — *archived LV 2.10. Replaced by the L13 + L17 + L18 system — now the standalone `filter-craft-lv` skill (filter triggers on prompt text, not ref content; modern playbook fixes via word-trim + pose redesign).*

## Adding a new lesson

1. Claude proposes the lesson with reasoning. User says yes/edit/no.
2. If yes: copy `../templates/lesson-template.md`, place in the right theme folder, name `L##-short-title.md`.
3. Add a row to the table above with `added LV X.X`.

## Archiving a lesson

When a lesson is no longer useful (model changed, superseded, proved wrong):

1. Move the file to `archive/`.
2. Remove its row from the active table; add a one-line note under "Archived lessons" with the reason.
3. If superseded, set `supersedes:` on the new lesson's frontmatter.
