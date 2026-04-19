# Validation Ledger

> Append-only log of lesson applications. Never rewrite past entries. After each row here, also update the Validation log table inside the lesson's own file.

## How to use
1. Every time you apply a lesson to real work, append a row below.
2. Outcome must be `pass`, `partial`, or `fail`.
3. Mirror the row into the lesson's own Validation log table.
4. When a lesson's row count + pass ratio meets its tier threshold **across ≥2 projects** (meso) or **≥3 projects** (macro), promote it per the protocol in `CHANGELOG.md` and bump LV.
5. Arena trials use `Project = arena:SXX` (scenario ID from `arena/scenario-bank/README.md`) and `Reviewer = AI-jury`. They count as distinct projects only if their axis fingerprint differs from every prior arena row for the same lesson on ≥2 of 9 axes (see `arena/axes.md`).
6. `DHYANA` and any `arena:SXX` are always distinct from each other. Arena-to-arena distinctness is governed by the axis rule in item 5.

## Ledger

> `Project` = `DHYANA` (real) or `arena:S##` (synthetic scenario).
> `Reviewer` = `self` (real project) or `AI-jury` (arena).

| # | Date       | Project | Shot / Context         | Lesson | Technique applied                                    | Outcome | Notes                               | Reviewer |
|---|------------|---------|------------------------|--------|------------------------------------------------------|---------|-------------------------------------|----------|
| 1 | 2026-04-15 | DHYANA  | Tier 1 v2 (12 imgs)    | L01    | Ref chain dependency graph                           | pass    | Face + architecture locked          | self     |
| 2 | 2026-04-15 | DHYANA  | #7 v5                  | L02    | Explicit face-UP orientation                         | pass    | —                                   | self     |
| 3 | 2026-04-15 | DHYANA  | #7 v4                  | L03    | Opaque-body + face-window phrase unified             | pass    | Matched #6                          | self     |
| 4 | 2026-04-16 | DHYANA  | #08 v2                 | L08    | Warm-amber palette stated + matched #04              | pass    | Memory flashback cohesion           | self     |
| 5 | 2026-04-16 | DHYANA  | #07 v7                 | L09    | Cropped pod front 1885×1280 used as primary ref      | pass    | Silhouette finally matched          | self     |
| 6 | 2026-04-16 | DHYANA  | g10a v2                | L06    | Adult male grey hair, distinct from g15b mother      | pass    | Reveal integrity preserved          | self     |
| 7 | 2026-04-16 | DHYANA  | #07 v10                | L10    | Stopped at 17% face-window ratio (target 13%)        | pass    | 7-regen diminishing curve observed  | self     |
| 8 | 2026-04-16 | DHYANA  | Tier 1+2 batch         | L07    | HTML storyboard delivered via browser open           | pass    | Confirmed CC preview mismatch       | self     |
| 9 | 2026-04-17 | arena:S02 | Iron tsuba A/B (3A vs 3B) | L09 | Cropped ref vs full-ref control, identical sparse text | partial | 3A beat 3B on 2/4 dims (arc dir + overall fidelity); Skeptic adversarial-valid | AI-jury |
| 10 | 2026-04-17 | arena:S03 | Aztec penacho A/B (3A vs 3B) | L09 | Cropped ref vs full-ref control, 4 directional dims | **pass** | 3A beat 3B on 3/4 dims (left-fan + crown lean + overall fidelity); Skeptic adversarial-valid. **Triggers L09 promotion to validated** | AI-jury |
| 11 | 2026-04-17 | arena:S04 | Victorian orrery multi-factor (6-gen experiment) | L09+L12 | Ref strategy × crop size methodology investigation | **findings** (not pass/fail) | H1 PASS (crop-only loses scene), H2 PASS but margin-fragile (3D-small ranked #1), H3 PASS (larger crop = better target), H4 PARTIAL. Skeptic adversarial-valid with conservative recommendation: act on H1+H3, create L12 pending 0/3 (NOT counting as validation), hold on H4 and arena-prompt changes | AI-jury |

## Pending promotions

> Auto-curated. When a lesson meets its tier threshold, list it here until the CHANGELOG promotion entry is written and the lesson's status flips to `validated`.

- (none pending — L09 was first candidate and has now been promoted per CHANGELOG entry below)

## Promotion history

> Log each promotion event. Format: `YYYY-MM-DD · LXX · pending (X/Y) → validated · LV bump Z.N → Z.N+1 · reviewer`.

- **2026-04-17** · L09 · `pending (1.5/3)` → `validated` · LV bump 2.2 → 2.3 · AI-jury · Evidence: DHYANA row #5 (pass) + arena:S02 row #9 (partial 2/4) + arena:S03 row #10 (pass 3/4)
