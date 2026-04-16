# Validation Ledger

> Append-only log of lesson applications. Never rewrite past entries. After each row here, also update the Validation log table inside the lesson's own file.

## How to use
1. Every time you apply a lesson to real work, append a row below.
2. Outcome must be `pass`, `partial`, or `fail`.
3. Mirror the row into the lesson's own Validation log table.
4. When a lesson's row count + pass ratio meets its tier threshold **across ≥2 projects** (meso) or **≥3 projects** (macro), promote it per the protocol in `CHANGELOG.md` and bump LV.

## Ledger

| # | Date       | Project | Shot / Context         | Lesson | Technique applied                                    | Outcome | Notes                               | Reviewer |
|---|------------|---------|------------------------|--------|------------------------------------------------------|---------|-------------------------------------|----------|
| 1 | 2026-04-15 | DHYANA  | Tier 1 v2 (12 imgs)    | L01    | Ref chain dependency graph                           | pass    | Face + architecture locked          | self     |
| 2 | 2026-04-15 | DHYANA  | #7 v5                  | L02    | Explicit face-UP orientation                         | pass    | —                                   | self     |
| 3 | 2026-04-15 | DHYANA  | #7 v4                  | L03    | Opaque-body + face-window phrase unified             | pass    | Matched #6                          | self     |
| 4 | 2026-04-16 | DHYANA  | #08 v2                 | L08    | Warm-amber palette stated + matched #04              | pass    | Memory flashback cohesion           | self     |
| 5 | 2026-04-16 | DHYANA  | #07 v7                 | L09    | Cropped pod front 1885×1280 used as primary ref      | pass    | Silhouette finally matched          | self     |
| 6 | 2026-04-16 | DHYANA  | g10a v2                | L06    | Adult male grey hair, distinct from g15b mother      | pass    | Reveal integrity preserved          | self     |
| 7 | 2026-04-16 | DHYANA  | #07 v10                | L10    | Stopped at 17% face-window ratio (target 13%)        | pass    | 7-regen diminishing curve observed  | self     |

## Pending promotions

> Auto-curated. When a lesson meets its tier threshold, list it here until the CHANGELOG promotion entry is written and the lesson's status flips to `validated`.

- (none yet — all current lessons have only single-project coverage; meso/macro requires ≥2 / ≥3 projects)

## Promotion history

> Log each promotion event. Format: `YYYY-MM-DD · LXX · pending (X/Y) → validated · LV bump Z.N → Z.N+1 · reviewer`.

- (none yet)
