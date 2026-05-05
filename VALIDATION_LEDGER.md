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
| 12 | 2026-05-05 | Alisa Glamour Photobook G01 v4 + Jira/Mila KIE state file audit | 2-ref `master + hero` chain across multi-plate sets (~70 plates total: Alisa 35 + Jira 9-13 × 3 sets + Mila ~9) | L01 | 2-ref chain dependency graph applied across 5 distinct production sets in 3 distinct projects | pass | Ref chain held identity across all audited plates. L01 validation count 1→2/5. | self |
| 13 | 2026-05-05 | Alisa Glamour Photobook G01 v4 + Jira/Mila KIE state file audit | Per-pose Tier-1 refs (master + hero pose pairs) used across multi-plate sets | L11 | Verified compatibility-matrix discipline in real production projects | pass | First real-project pass since DHYANA (origin). L11 validation count 0→1/5. | self |
| 14 | 2026-05-05 | Alisa Glamour Photobook G01 v4 batch | Sweet-spot wardrobe vocab ("silk wrap", "asymmetric drape", etc.) on multi-plate sexy-glamour set | L13 | 2nd validation case (after Lily L1 P1) crossed 2-project threshold | **pass** | **Triggers L13 promotion to validated** (2/3 across 2 projects: Lily + Alisa). | self |
| 15 | 2026-05-05 | Alisa Glamour Photobook + cross-project audit (Jira/Mila/Lily/Pupae) | Used revealing hero refs alongside filter-safe prompt vocab. Audited filter pass/block patterns vs ref content. | L17 | Field test: revealing refs routinely pass when prompt vocab is in L13 sweet spot | pass | Confirms filter triggers on prompt text not ref content (Google/Imagen). Counter-evidence for L15. L17 validation 0→1/3. | self |
| 16 | 2026-05-05 | Alisa Glamour Photobook G01 v4 batch | Retry-first protocol on filter-blocked plates (3-5× retry before any prompt edit) | L18 | Distinguished stochastic (output) vs deterministic (input) filter blocks | pass | ~half of blocks resolved on retry without prompt change. Net: less prompt churn. L18 validation 0→1/3. | self |
| 17 | 2026-05-05 | Alisa Glamour Photobook v2-v4 + Jira/Mila prompt archive cross-check | Narrative pose per plate (action verb + prop + sub-location + body interaction + camera) replaced generic framing template from v1 | L19 | Multi-plate set pose-variety test, A/B vs v1 generic-framing baseline | pass | v1 (counter-example) mono-angle output; v2-v4 (validation) genuinely varied compositions; Jira/Mila independently use the narrative-pose pattern. L19 validation 0→1/3. | self |
| 18 | 2026-05-05 | Alisa Glamour Photobook v2-v4 + Jira/Mila prompt archive cross-check | Camera body + film stock + skin description replaced lens-only spec | L20 | Naturalness test, A/B vs v1 plastic skin baseline | pass | v1 (counter-example) plastic CGI skin from "85mm f/1.4"; v2-v4 (validation) natural skin from "Hasselblad X2D · 90mm · Kodak Portra 400" + skin description; Jira/Mila independently use body+stock specs. L20 validation 0→1/3. | self |
| 19 | 2026-05-05 | Alisa Glamour Photobook v1-v4 progression | Designer aesthetic anchor progression: none (v1) → Newton (v2) → Khaite (v3) → Newton×Khaite hybrid (v4) | L21 | Mood/polish test across 4 anchor configurations | pass | v1 (counter-example) generic AI-glamour without anchor; v2-v4 (validation) each anchor produced distinct on-brief mood; hybrid anchor locked the brief. L21 validation 0→1/3. | self |
| 20 | 2026-05-05 | Alisa Glamour Photobook v3-v4 | Anti-overproduction directive count reduced 4→1 + paired with positive replacements | L22 | Calibration test: stacked anti-directives over-corrected; surgical anti + positive replacement landed correctly | pass | v3 (counter-example) over-corrected modest output from "NOT magazine glamour, NOT boudoir, NOT lingerie, NOT over-retouched"; v4 (validation) on-brief glamour-natural from single anti-directive + positive replacements. L22 validation 0→1/3. | self |
| 21 | 2026-05-05 | Alisa Glamour Photobook v3-v4 | Face EXPRESSION pulled into dedicated prompt block with positive descriptors + "NOT hard, NOT stiff" anti-pattern | L23 | A/B vs v2 where expression was buried in pose | pass | v2 (counter-example) hard AI fashion-model resting face; v3-v4 (validation) natural expressive on-brief faces across plate set. L23 validation 0→1/3. | self |
| 22 | 2026-05-05 | Alisa Glamour Photobook v3→v5 reanalysis (Lily L1 P1 origin trial) | Reviewed original L15 trial — confirmed 2 variables changed simultaneously (ref drop + pose change) | L15 | Causal attribution audit | **demote** | Single-variable design not isolated; user field testing showed refs rarely trigger filter. L15 demoted from `pending 1/3` to `needs-rerun · attribution unclear`, validation reset 1→0/3. | self |

## Pending promotions

> Auto-curated. When a lesson meets its tier threshold, list it here until the CHANGELOG promotion entry is written and the lesson's status flips to `validated`.

- (none pending — L13 promoted via LV 2.7 entry below)

## Promotion history

> Log each promotion event. Format: `YYYY-MM-DD · LXX · pending (X/Y) → validated · LV bump Z.N → Z.N+1 · reviewer`.

- **2026-04-17** · L09 · `pending (1.5/3)` → `validated` · LV bump 2.2 → 2.3 · AI-jury · Evidence: DHYANA row #5 (pass) + arena:S02 row #9 (partial 2/4) + arena:S03 row #10 (pass 3/4)
- **2026-05-05** · L13 · `pending (1/3)` → `validated` · LV bump 2.6.2 → 2.7 · self · Evidence: Lily Beach Swim row (origin, 2026-05-01) + Alisa Glamour Photobook G01 v4 row #14 (2-project cross-validation: Lily + Alisa)

## Demotion / rerun history

> Log each demotion or rerun event for transparency.

- **2026-05-05** · L15 · `pending (1/3)` → `needs-rerun · attribution unclear` · LV bump 2.6.2 → 2.7 · self · Reason: original trial (Lily L1 P1 v3→v5) changed 2 variables (ref drop + pose change) simultaneously, so causal attribution between "drop hero ref" and "filter pass" was not isolated. User field testing showed refs rarely trigger filter alone (see new L17). Validation reset 1→0/3 pending single-variable rerun.
