# image-craft-lv — Changelog & Leveling Protocol

> Full level history, promotion log, and the validation gate rules. SKILL.md carries only a short summary and links here.

## Level history

- **LV 1** (baseline) — Text-only prompting. Relied on repeating prose descriptions to maintain consistency across multi-image sets. Trusted the model to interpret prose faithfully.

- **LV 2** (2026-04-15) — Learned: reference chains (L01), explicit face orientation (L02), opaque/transparent container vocabulary (L03), mandatory self-review before delivery (L04). Added tiered Validation Gate and per-lesson Status. All 4 lessons recorded as `pending (X/Y)`.

- **LV 2 (lessons added 2026-04-16)** — L05 back-view face anchors, L06 distinguishable lookalike characters, L07 reviewable-artifact delivery, L08 palette consistency, L09 crop-isolate refs, L10 prominence-floor / diminishing returns, L11 Tier-1 video-continuity refs. Level not bumped — no lesson yet cross-project-validated.

- **LV 2.1** (2026-04-16) — **Modular redesign + rename.** Restructured the skill from a single 261-line SKILL.md into an engine (SKILL.md) + themed `lessons/` + append-only `VALIDATION_LEDGER.md` + this CHANGELOG + three templates. Renamed `prompt-craft-lv` → `image-craft-lv` to parallel `seedance-craft-lv` and remove video-scope ambiguity. Ported the Batch Discipline Gate from seedance-craft-lv. Introduced the cross-project validation requirement (meso = ≥2 projects, macro = ≥3 projects) — DHYANA-only wins no longer promote. Promoted the proportion-comparison and full-frame-scan CRITICAL rules into first-class checklist items. No lesson content deleted; all prose preserved in the new lesson files.

## Leveling Protocol

### Validation Gate

Before a lesson can move from `pending` to `validated`, and before the level bumps, it must pass tiered validation:

| Tier   | Definition                                                        | Required passes | Project spread                    |
|--------|-------------------------------------------------------------------|-----------------|-----------------------------------|
| Micro  | Small phrasing/naming/convention change, low blast radius         | 1               | 1 project                         |
| Meso   | Technique affecting a single shot/image                           | 2 of 3 attempts | **≥2 distinct projects**          |
| Macro  | Workflow-level change affecting whole projects                    | 3 of 5 attempts | **≥3 distinct projects** (or 3 passes + 1 deliberate counter-test) |

Project-spread is the new (LV 2.1) requirement. It prevents a single origin project from self-validating all of its lessons.

### Status field

Lessons carry `status:` in their frontmatter.

- `pending (X/Y)` — still being validated; X passes recorded out of Y required.
- `validated` — threshold met; safe to rely on.
- `retired` — superseded by a newer lesson or proven wrong. Keep the file for history; mark the reason in its body; list its ID in the superseding lesson's `supersedes: [LXX]` frontmatter field.

### Process

1. **Spot a new mistake → log a lesson immediately** as `pending (0/Y)`. Do not wait for certainty; the log forces investigation.
2. **Apply the fix → record** in `VALIDATION_LEDGER.md` AND mirror the row into the lesson's own Validation log.
3. **When X reaches Y** with the project-spread requirement met:
   - If pass threshold met → promote `status: pending → validated`, bump LV, add an entry to this CHANGELOG.
   - If not met → rewrite the lesson (what actually works differs from the first guess), reset validation counter to 0/Y, log the reset in the body.
4. **Never bump LV** without at least one `pending → validated` promotion in the CHANGELOG for that LV.

### Classifying a new lesson

Blast radius = "if this fix is wrong, how many future generations break?"

- Small single-prompt tweak = Micro.
- Per-shot discipline = Meso.
- Changes workflow = Macro.

When unsure, pick the higher tier.

### Rollback

Skill is under git. To undo a bad promotion:
```
git log SKILL.md
git revert <sha>
```
Document the rollback reason in a new CHANGELOG entry. Never silently edit old lessons or CHANGELOG entries — they are history. Use `retired` status or `git revert`.

### Relationship to sister skills

- `seedance-craft-lv` — video generation. Cross-pollinates with this skill via shared Tier-1 ref discipline (see L11).
- `kie-nano-banana` — API execution layer. This skill is the *strategy* layer above it.
