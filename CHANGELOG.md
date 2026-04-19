# image-craft-lv — Changelog & Leveling Protocol

> Full level history, promotion log, and the validation gate rules. SKILL.md carries only a short summary and links here.

## Level history

- **LV 1** (baseline) — Text-only prompting. Relied on repeating prose descriptions to maintain consistency across multi-image sets. Trusted the model to interpret prose faithfully.

- **LV 2** (2026-04-15) — Learned: reference chains (L01), explicit face orientation (L02), opaque/transparent container vocabulary (L03), mandatory self-review before delivery (L04). Added tiered Validation Gate and per-lesson Status. All 4 lessons recorded as `pending (X/Y)`.

- **LV 2 (lessons added 2026-04-16)** — L05 back-view face anchors, L06 distinguishable lookalike characters, L07 reviewable-artifact delivery, L08 palette consistency, L09 crop-isolate refs, L10 prominence-floor / diminishing returns, L11 Tier-1 video-continuity refs. Level not bumped — no lesson yet cross-project-validated.

- **LV 2.1** (2026-04-16) — **Modular redesign + rename.** Restructured the skill from a single 261-line SKILL.md into an engine (SKILL.md) + themed `lessons/` + append-only `VALIDATION_LEDGER.md` + this CHANGELOG + three templates. Renamed `prompt-craft-lv` → `image-craft-lv` to parallel `seedance-craft-lv` and remove video-scope ambiguity. Ported the Batch Discipline Gate from seedance-craft-lv. Introduced the cross-project validation requirement (meso = ≥2 projects, macro = ≥3 projects) — DHYANA-only wins no longer promote. Promoted the proportion-comparison and full-frame-scan CRITICAL rules into first-class checklist items. No lesson content deleted; all prose preserved in the new lesson files.

- **LV 2.2** (2026-04-17) — **Auto-Leveling Arena.** Added adversarial
  synthetic-validation system (4 AI roles: 🎲 Generator / 🖌️ Runner
  (blinded) / ⚖️ Judge / 🕵️ Skeptic). Scenarios must flip ≥3 of 9
  axes from DHYANA and ≥2 axes from every prior scenario for the
  same lesson. Pre-registered criteria locked to git before Runner
  starts. Skeptic's adversarial review gates every ledger entry.
  Arena trials count toward cross-project validation: `arena:SXX`
  is a distinct project from `DHYANA` and from other arena scenarios
  that pass axis-diversity. Enables self-leveling when real projects
  are scarce. Single human checkpoint at scenario approval; rest is
  autonomous with a $2/trial cost cap. No lesson promoted in this
  LV bump — LV 2.2 is the infrastructure release; LV 2.3+ come when
  the first promotions occur.

- **LV 2.3** (2026-04-17) — **First lesson promotion · L09 validated.**
  L09 (crop refs to isolate target element) promoted from `pending` to
  `validated` after accumulating 2.5/3 passes across 3 axis-distinct
  projects: 1 DHYANA pass + 1 arena:S02 partial + 1 arena:S03 pass.
  S03's Aztec penacho A/B control (all 4 scoring dimensions were
  directional/asymmetric) produced a clean 3/4 win for crop-ref over
  full-ref with identical sparse text — the first arena scenario
  explicitly designed to eliminate S02's "structural tie" problem, and
  it worked. Total arena cost to reach first promotion: ~$0.93 across
  3 trials (1 void + 1 partial + 1 pass). Meso promotion rule
  (2 of 3 passes across ≥2 projects with axis spread) met decisively.
  First empirical proof the arena system can evolve lessons without
  real-world projects.

- **LV 2.4** (2026-04-17) — **Methodology investigation + L12 birth.**
  Following LV 2.3 (L09 promoted), human review of the S03 crop-ref shot
  revealed that crop-only references anchor the target element but
  **completely re-imagine the surrounding scene** (S03 3A lost Templo
  Mayor pyramid, drum players, crowd — all replaced by different
  buildings/people despite identical prompt). Arena trial S04
  (Victorian orrery, 6-gen multi-factor: ref-strategy × crop-size) was
  designed to test dual-ref (crop + full-scene) as a remedy. Findings:
  H1 PASS (crop-only sacrifices scene), H2 PASS with fragile margin
  (3D-small ranked #1 at D3=2.000 vs 3B at 1.875), H3 PASS (larger crop
  = better target fidelity, dramatic gap), H4 PARTIAL (one scene
  element dropped in 3D-large, possibly stochastic). Skeptic returned
  `adversarial-valid` with conservative recommendation: act on H1+H3
  (narrow L09 scope, create L12 as pending), hold on H4 and arena-prompt
  changes until replicated. **Actions:** L09 body updated with "Scope
  limits" section explaining the crop-only tradeoff + crop-resolution
  sub-rule; new lesson **L12 (dual-ref for context)** created as
  `pending 0/3` with S04 as origin-experiment (not counted as
  validation per Skeptic's fragile-margin note). Total arena cost since
  LV 2.3: ~$0.24 for 6 multi-factor generations.

## Promotion history

- **2026-04-17** · L09 · `pending (1.5/3)` → `validated` · LV bump 2.2 → 2.3 · AI-jury (DHYANA + arena:S02 + arena:S03)

## Leveling Protocol

### Validation Gate

Before a lesson can move from `pending` to `validated`, and before the level bumps, it must pass tiered validation:

| Tier   | Definition                                                        | Required passes | Project spread                    |
|--------|-------------------------------------------------------------------|-----------------|-----------------------------------|
| Micro  | Small phrasing/naming/convention change, low blast radius         | 1               | 1 project                         |
| Meso   | Technique affecting a single shot/image                           | 2 of 3 attempts | **≥2 distinct projects**          |
| Macro  | Workflow-level change affecting whole projects                    | 3 of 5 attempts | **≥3 distinct projects** (or 3 passes + 1 deliberate counter-test) |

Project-spread is the new (LV 2.1) requirement. It prevents a single origin project from self-validating all of its lessons.

**Axis-diversity (LV 2.2 refinement):** "Distinct project" for arena
trials means the scenario's axis fingerprint differs from every prior
arena trial for the same lesson on ≥2 of 9 axes (defined in
`arena/axes.md`). `DHYANA` and `arena:SXX` are always distinct.
Trials whose fingerprints do NOT meet this bar can still be run for
diagnostic value, but cannot be counted toward promotion.

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
