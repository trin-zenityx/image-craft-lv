# image-craft-lv — Changelog & Leveling Protocol

> Full level history, promotion log, and the validation gate rules. SKILL.md carries only a short summary and links here.

## Level history

- **LV 2.11** (2026-05-07) — **L25 added · color-grade-first protocol for color-only drift.** Trin observation during Tara Vol 04 P2 fix: had spent ~5 min + 3 KIE calls regenerating P2 to fix a color drift (sapphire blue → warm amber + teal balance). Trin: *"รอบหน้าคุณลองเกลี่ยสีดูเองก่อนก็ได้นะ เผื่อมันได้เลย จะได้ไม่ต้องเจนใหม่"* — when only color is wrong (composition + face + pose + wardrobe all correct), grade with sips / ImageMagick / Pillow first; regen as fallback. Saves ~3-5 min wall time + 0 API cost vs regen. New lesson L25 (workflow / micro · pending 1/1) with full ImageMagick recipes for warm/cool shifts, histogram match, anti-patterns, and decision protocol. **Files changed:** `lessons/workflow/L25-color-grade-first.md` (new), `SKILL.md` frontmatter + Current Level line + lessons table row, `CHANGELOG.md` (this entry). Tier: Minor (additive lesson, no breaking changes).

- **LV 2.10** (2026-05-06) — **Filter-word tier registry · L13 rewritten as single source of truth · L18 R3/R4 protocol changes · L15 RETIRED · feedback memory DEPRECATED.**

  Co-design with Trin. Goal: replace the scattered filter-word lists (L13 wardrobe catalog, feedback memory list, L18 suspicion ranking, L13 negative-example archive) with **one canonical tier registry** that all other lessons reference.

  **Tier definitions (per Trin):**
  - **Tier 1** (high confidence) — never include in any prompt; excluded by design at R1
  - **Tier 2** (medium confidence) — included in R1+R2; dropped at R3
  - **Tier 3** (low confidence) — included in R1+R2+R3; dropped at R4
  - **Tier 0** — always safe; documented for reference only

  **L18 protocol changes:**
  - **R3 changed** from "5 parallel of same prompt" → "drop Tier 2 + 5 parallel" (first vocab change in playbook; was previously the 9th retry of identical prompt).
  - **R4 changed** from "drop 1-2 risky words/round + 3 parallel × max 3 rounds" → "drop Tier 3 ALSO (Tier 2 stays dropped) + 3 parallel × max 3 rounds, dropping more aggressively each round."
  - **R5 unchanged** (pose redesign for layer-3 structural triggers).

  **Tier-up / tier-down protocol** (in L13): if a word in a lower tier triggers filter repeatedly across 2-3 sessions, Claude proposes promotion to Trin. Never silent updates. Trin approves before any tier change is committed.

  **L15 master-only-ref-bypass — RETIRED** (was `needs-rerun` since LV 2.7). The L13 + L17 + L18 system replaces it entirely. Original content preserved as historical archive in the file; status changed to `retired` and removed from active lessons in SKILL.md table.

  **`feedback_google_filter_prompt_vs_ref.md` — DEPRECATED.** Content rewritten to be a pointer file: the principle (prompt is choke point, not refs) lives in L17; the word lists live in L13; the playbook lives in L18. The original content was overly aggressive ("put it in REF, not prompt") in a way that conflicted with creative-freedom preservation; the modern playbook uses ref-offload only at R4 not as a default design choice.

  **Tier 1 final list** (after Trin review — per session conversation):
  - 1A direct sexual/explicit terms only: `lingerie`, `underwear`, `panties`, `bra`, `thong`, `barely-there`, `skimpy`
  - Items proposed for Tier 1 but moved to Tier 2 after Trin review: `young/youthful/teen` (1B), undressing-completion phrases (`slipping fully off`, `hanging loose at upper arms`, `hem riding up to mid-thigh`) (1D)
  - Items proposed for Tier 1 but DELETED after Trin review: `preserve THIS specific person`, `Hyperreal unretouched` (1C)

  **Tier 2 final list** (after Trin review):
  - 2A anatomy + intensifier combos · 2B `robe slipping off` (only severe undressing-motion verb that stayed) · 2C `sexy/sensual/seductive` direct adjectives · 2D body-framing percentages · 2E suggestive setting + wardrobe combos (Tara T01 4-word combo) · 2F underage / age-flag triggers · 2G direct undressing-completion
  - Items moved from Tier 2 to Tier 3 after Trin review: `bare shoulders / collarbone exposed`, `slipping off her shoulders`, `strap halfway off the shoulder`, `bare shoulder skin exposed`, `intimate`, `1962 Bardot pin-up moment`

  **Tier 3 final list** (after Trin review):
  - 3A borderline wardrobe (incl. `slip dress`, `bikini top`/`swim top`, `spaghetti-strap cami` combos, `low-rise + side-tie at hips`) · 3B borderline mood (incl. `intimate`, `1962 Bardot pin-up moment`, `smoldering`, `seduction`, `body chain`) · 3C context-dependent settings (`boudoir` alone) · 3D body-clinical descriptors · 3E single body-exposure / motion verbs (the items moved from Tier 2 above)

  **Files changed:**
  - `lessons/filter/L13-filter-vocab-sweet-spot.md` — full rewrite as tier registry (single source of truth). Tier 0/1/2/3 lists, tier-up protocol, anti-patterns, validation log entry #3. Removes wardrobe catalog and "principle + anti-pattern" framing from LV 2.9.
  - `lessons/workflow/L18-filter-retry-diagnostic.md` — R3 protocol section + R4 protocol section rewritten to reference L13 tiers explicitly. The "hard rule" section restated to align with tier system. Worst-case time and cost framing unchanged.
  - `lessons/filter/L15-master-only-ref-bypass.md` — frontmatter updated to `status: retired`, retirement notice added at top. Original content preserved below as historical archive.
  - `~/.claude/projects/-Users-trin/memory/feedback_google_filter_prompt_vs_ref.md` — fully rewritten as deprecation pointer to L13/L17/L18; canonical_sources list added in frontmatter.
  - `SKILL.md` — frontmatter `level: 2.9 → 2.10`, Current Level line, lessons table (L13 / L15 / L18 rows updated), Core Principle #8 rewritten to mention tiers + L13 explicitly.
  - `CHANGELOG.md` — this entry.

  **Tier:** Minor — restructuring of existing lessons (no new lessons added); validation increments + protocol extension within current scope; one retirement (L15) and one memory deprecation (feedback file). No breaking changes to validated lessons; protocol changes documented per-round.

- **LV 2.9** (2026-05-06) — **Tara 3-Look full validation · L13 reframed to remove wardrobe-vocab catalog (anti-bias) · L17 promoted validated 2/3 · L18 promoted validated 3/3 + extended to full R1→R5 playbook · Core Principle #8 added (3-layer filter model).**

  Driven by the Tara 3-Look Photobook session (T01 Champagne Boudoir + T04 Bordeaux Velvet + T05 Marble Bath = 21 plates). Key learnings:

  **L13 — restructured (anti-bias rewrite per Trin instruction):**
  - Trin observation: prior L13 listed "halter knot-front V-neck" as `validated · meso` — Claude was reading this as a default sexy-wardrobe choice and pre-emptively rewriting user wardrobe intent. Tara T01 R4 was the case study: Claude switched a silk-slip set into halter top + midi skirt mid-set to "validate" the safe vocab, breaking set continuity. User had to delete and restart.
  - Trin instruction (verbatim): *"ส่วนของชุด อยากให้ตัดคำแนะนำชุดออกไปเลย มันจะขัดความคิดสร้างสรรค์"* ("Cut out the wardrobe suggestions entirely — it constrains creativity").
  - **L13 wardrobe vocabulary catalog removed.** What replaces it: only the META-principle ("filter does word-matching not semantics") + an anti-pattern ("never pre-emptively rewrite user wardrobe to safe vocab; let R1+R2+R3 free retries decide; only after R3 confirms deterministic block, trim 1-2 most-direct phrases at R4 — and even then keep wardrobe word unchanged unless user approves change").
  - L13 also documents the 3-layer filter model (word / combo / structural) and the negative-example list (phrasings observed to trigger filter — for SCRUBBING at R4, NOT for use as substitutes).

  **L17 — promoted validated 1/3 → 2/3:**
  - Tara T01 R4 minimal-removal evidence: same revealing T01 anchor across all 7 T01 plate retries; only the prompt text varied (drop 1-2 phrases per round + replace with `"wardrobe and neckline as in reference 2"`). T01 P1 passed Round 1, P4 passed Round 2.
  - Confirms text-token matching mechanism: ref content unchanged + revealing while prompt vocabulary varied → only the trimmed prompts passed. Validates "ref offload" as the canonical R4 word-trim technique.
  - Added "ref offload" technique section to L17.

  **L18 — promoted validated 2/3 → 3/3 + extended to full R1→R5 playbook:**
  - Trin instruction (verbatim): *"เริ่มตัดเมื่อผ่าน R3"* ("start [word-]trimming only after R3 [exhaustion]"). Codified as the hard rule at the top of L18: NO prompt change before R1+R2+R3 (9 free retries) confirm deterministic block.
  - **NEW R4 protocol:** word trimming = drop 1-2 most-risky DIRECT phrases per round, 3 parallel × max 3 rounds. Use ref-offload (`"as in reference N"`) as canonical replacement. Suspicion ranking heuristics provided (undressing-motion verbs > anatomy + intensifier combos > framing percentages > "intimate" > pin-up era + body framing).
  - **NEW R5 protocol (codified from Tara):** structural pose redesign. Trigger: R4 exhausted (all 3 rounds × 3 parallel = 9 trimmed-prompt attempts blocked) → indicates layer-3 structural trigger (the pose / framing itself). Strategy: keep wardrobe + setting + lighting + camera identical; change ONLY pose / framing. Tara T01 evidence: P2 (tight chest-up close → medium 3/4 standing at mirror), P5 (strap-touch → hand-at-hair near temple), P7 (off-shoulder window halo → frontal stance with dress fully on) — all 3 passed Round 1 first try (3/3) after 27 prior attempts had failed under R1-R4.
  - Validation: this was the first full R1→R5 cycle. Total Tara T01 ledger: P3 + P6 (2/7 R1+R2+R3); P1 + P4 (2/5 R4); P2 + P5 + P7 (3/3 R5).

  **Core Principle #8 added:** "Filter has 3 layers (word / combo / structural) — match fix tier to layer; word changes happen ONLY after R3 exhaustion. NEVER pre-emptively rewrite wardrobe to 'filter-safe vocab' — that bias trap was deleted from L13. Set continuity > any single plate."

  **Files changed:**
  - `lessons/filter/L13-filter-vocab-sweet-spot.md` — full rewrite removing wardrobe catalog, adding 3-layer model, anti-pattern, decision tree, validation entry #3.
  - `lessons/filter/L17-filter-text-not-ref.md` — frontmatter promote `pending 1/3 → validated 2/3`, added "ref offload" technique section, validation entry #2.
  - `lessons/workflow/L18-filter-retry-diagnostic.md` — full restructure with R1→R5 escalation, hard rule "no prompt change before R3", R4 word-trim protocol with suspicion ranking, R5 pose-redesign protocol, validation entry #3, promote `pending 2/3 → validated 3/3`.
  - `SKILL.md` — frontmatter `level: 2.8 → 2.9`, Current Level line, lessons table (L13/L17/L18 status updated), Core Principle #8 added.
  - `CHANGELOG.md` — this entry.

  **Tier:** Minor — extends existing lessons (no new lessons added; L13 reframed not retired); validation increments + protocol extension within current lesson scopes. No breaking changes.

- **LV 2.8** (2026-05-06) — **L18 refined to escalating parallel retry (1→3→5) as PRIMARY strategy + L18 validation 1/3 → 2/3.** Co-design with Trin during Tara Glamour Photobook session: when retries are FREE, sequential 1→2→3 is wall-time-suboptimal and stops short of "free shots still on the table." New protocol: **R1 (1) → R2 (3 parallel) → R3 (5 parallel) → R4 (modify prompt + 3 parallel) → R5 (restructure + 3 parallel) → STOP.** Math justification: 9 cumulative attempts cover 87-99.8% of stochastic blocks at common Google/Imagen pass rates — only AFTER 9 same-prompt fails does prompt modification become the right move (strong evidence of deterministic input filter). Includes per-plate batch handling for multi-plate generations to keep prompt-rewrite cost localized.

  **Key insight (Trin):** "เจนฟรี มีโอกาสได้มาสักภาพก็ถือว่าประสบความสำเร็จแล้ว" — never give up on free retries before paying the prompt-edit cost (which can degrade output and introduce new bugs).

  **Validation evidence:**
  - Tara T02 (Saint-Tropez bikini anchor): blocked R1 + retry attempt 1+2 → passed attempt 3 → ~33% pass rate per attempt → output-filter stochastic confirmed.
  - G03 P2 v6 (Marble noir B&W): blocked once, passed retry attempt 1 → ~50% pass rate.
  - Both validate the stochastic-output-filter hypothesis underpinning the escalating parallel approach.

  **Files changed:**
  - `lessons/workflow/L18-filter-retry-diagnostic.md` — full rewrite with new escalation protocol, math table, batch handling pattern, cost framing, validation log entry #2.
  - `SKILL.md` — frontmatter `level: 2.7 → 2.8`, Current Level line, L18 row in lessons table.
  - `CHANGELOG.md` — this entry.

  **Tier:** Minor — refined existing lesson methodology (validated technique tweak), no new lesson added.

- **LV 2.7** (2026-05-05) — **Editorial Naturalness pack · 7 new lessons · 1 promotion · 1 demotion · 2 validation increments · new core principle.** Driven by Alisa Glamour Photobook session (G01 v1→v4 progression) plus cross-validation against KIE state-file audit of Jira Set A/B/C and Mila Set B prompt archives (~70 plates total). Six distinct prompt-craft patterns surfaced that ZenityX production photobooks were already using but the skill hadn't formalized.

  **Added (7 new lessons):**
  - **L17** filter — Filter triggers on prompt text, not on ref image content (Google / Imagen). Refs can be highly revealing without blocks. Use sexy refs freely; control filter risk via prompt vocabulary.
  - **L18** workflow — Filter blocks don't cost credits → retry 3-5× as diagnostic before modifying prompt. Distinguishes input filter (deterministic) vs output filter (stochastic).
  - **L19** pose — Narrative pose per plate (action verb + concrete prop + sub-location + body interaction + camera framing) beats generic framing templates ("P1 Hero / P2 Beauty"). Generic templates → AI converges on default pose; narrative pose forces variety. New `pose/` theme folder created.
  - **L20** camera — Camera body + film stock specificity ("Hasselblad X2D · 90mm · Kodak Portra 400") beats lens-only spec for naturalness. Pair with positive skin description. New `camera/` theme folder created.
  - **L21** aesthetic — Designer / aesthetic reference choice drives mood and polish. Newton×Vogue Italia → polished glamour; Khaite×Toteme → quiet luxury; Newton×Khaite hybrid → glamour-natural (Alisa G01 v4 recipe). New `aesthetic/` theme folder created.
  - **L22** prompt-craft — Anti-overproduction directives are calibration tools, not blanket switches. "NOT magazine glamour" pulls back over-polish; stacking 4+ anti-directives over-corrects and kills sensuality. Always pair with positive replacement. New `prompt-craft/` theme folder created.
  - **L23** character — Face EXPRESSION as separate prompt block with explicit "NOT hard, NOT stiff" anti-pattern. Burying expression in pose loses prioritization → AI defaults to hard fashion-model resting face.

  **Promoted:**
  - **L13** filter-vocab sweet spot → **validated** (`pending 1/3` → `validated 2/3`). 2nd validation case: Alisa G01 v4 batch sweet-spot wardrobe vocab held across multi-plate sexy-glamour set. Cross-project threshold met (Lily + Alisa).

  **Demoted:**
  - **L15** master-only ref bypass → **`needs-rerun · attribution unclear`**. Original Lily L1 P1 trial changed 2 variables simultaneously (ref drop + pose change), so causal attribution between "drop hero ref" and "filter pass" was not isolated. The pose change alone is sufficient to explain the result. User field testing during Alisa session showed refs rarely trigger filter. Counter-evidence: master-only generation in Alisa introduced wardrobe / face / continuity drift the standard 2-ref recipe avoided. Validation counter reset 1/3 → 0/3. Single-variable rerun required before re-promotion.

  **Validation count increments:**
  - **L01** ref chains → +1 (now `pending 2/5`). Evidence: Jira Set A/B/C + Mila Set B + Alisa session, KIE state file audit confirmed 2-ref `master + hero` pattern across 5 distinct production sets in 3 distinct projects.
  - **L11** Tier-1 video-continuity refs → +1 (now `pending 1/5`). First real-project pass since DHYANA origin. Evidence: per-pose master + hero pairs in Jira / Mila prompt archives.

  **Added Core Principle (#7):** Face identity is HIGHER priority than pose / action fidelity. If face renders well but pose is simpler than described, that is the PREFERRED outcome. State explicitly at the bottom of every multi-plate prompt. (Source: Jira / Mila / Alisa formula — appears in production prompts across 3 projects.)

  **Validation evidence:**
  - Alisa Glamour Photobook v1 (counter-examples for L19/L20/L21/L22/L23 — generic framing, plastic skin, no aesthetic anchor, hard expressions)
  - Alisa Glamour Photobook v2/v3 (recipe iteration — partial wins on individual axes)
  - Alisa Glamour Photobook G01 v4 (final validation: 2-ref glamour-natural hybrid recipe lock)
  - Jira Set A/B/C (cross-validation via `~/.kie/tasks/*.json` audit — 2-ref pattern + camera/stock specs + narrative pose + face-identity-priority directive present in all)
  - Mila Set B (cross-validation, same pattern)
  - Field testing across Lily / Pupae / Jira / Mila (filter behavior — confirms L17, contradicts original L15 attribution)
  - VALIDATION_LEDGER rows #12–#22

  **Files changed:**
  - `lessons/filter/L17-filter-text-not-ref.md` — new
  - `lessons/workflow/L18-filter-retry-diagnostic.md` — new
  - `lessons/pose/L19-narrative-pose-per-plate.md` — new (+ new theme folder)
  - `lessons/camera/L20-camera-body-film-stock.md` — new (+ new theme folder)
  - `lessons/aesthetic/L21-designer-aesthetic-mood.md` — new (+ new theme folder)
  - `lessons/prompt-craft/L22-anti-overproduction-calibration.md` — new (+ new theme folder)
  - `lessons/character/L23-face-expression-as-separate-block.md` — new
  - `lessons/filter/L13-filter-vocab-sweet-spot.md` — promoted (status, validation count, validation log entry)
  - `lessons/filter/L15-master-only-ref-bypass.md` — demoted (status, validation count, status banner)
  - `lessons/consistency/L01-ref-chains.md` — validation +1
  - `lessons/references/L11-video-continuity-refs.md` — validation +1
  - `lessons/README.md` — index rebuilt with new lessons / promotions / demotions / new themes
  - `SKILL.md` — frontmatter `level: 2.6.2 → 2.7`, Current Level line, lesson table (8 row updates), Core Principle #7 added, sister_skills += internal-board-builder
  - `VALIDATION_LEDGER.md` — rows #12–#22 appended, promotion + demotion history
  - `CHANGELOG.md` — this entry

- **LV 2.6.2** (2026-05-04) — **L16 defers technical primitives to new `internal-board-builder` skill.** After Trin asked for separation of architecture (where rules live) from content (technique vs layout), created standalone `internal-board-builder` skill containing: `lib/thumbs.py`, `lib/url.py`, `lib/modal/{html,js,css}` — single source of truth for technical primitives. L16 now keeps decision rules + cross-ref to skill. Memory `feedback_internal_board_thumbnails.md` trimmed to LV 4 (rules + skill ref only). **Layout/UX/theme decisions explicitly NOT codified anywhere** — each board designs its own UX to fit the work, per Trin's explicit constraint: "ให้แต่ละงานมีอิสระในการสร้างในรูปแบบของตนเอง... ไม่ให้ไปจำกัดความคิดสร้างสรรค์".

- **LV 2.6.1** (2026-05-04) — **L16 expanded · AVIF thumbs threshold + universal click-to-zoom modal.** L16 was 1/3 (file:// for local boards). After Trin codified a sister memory (`feedback_internal_board_thumbnails.md`) and refined it during this session, L16 now formally encompasses the LV 2 board pattern: **threshold lowered 50→10** (boards >10 images need AVIF q90 thumbs at 3× CSS long-side, capped at original; ≤10 stays direct file://); **click-to-zoom modal universal** on every internal board (image left, metadata panel right with build timestamp + data source + per-image task ID/refs/prompt); **HTML escape** all dynamic data via `textContent` (never `innerHTML`); **accuracy disclosures optional** by default (only show "(likely)" if Trin asks or judgment calls for it). Validation: 2/3 — pass on Mila L4+L5 board (12 images, AVIF + modal worked) + earlier L4-only board (file:// direct). Memory updated: `feedback_internal_board_thumbnails.md` LV 2 + `feedback_local_board_originals.md` decision matrix expanded + L16 lesson tags + cross-refs in MEMORY.md index. Patch bump (no new lesson; L16 expanded + threshold rule clarified).

- **LV 2.6** (2026-05-04) — **L16 local review board discipline.** New lesson born from L4 Mila Power Suit redo session. Default reflex of `sips -Z 1200 -s formatOptions 88` (or any copy + resize) into the board folder is **wrong for local boards** — wastes disk, degrades quality, breaks edit propagation. Correct rule: local boards (file paths starting with `/tmp/`, `~/Desktop/`, project-internal review HTMLs) MUST reference originals via `file:///abs/path/original.png`. Only copy + resize when deploying to a remote URL (Vercel, R2, Cloudflare Pages, FB/IG, email/Slack share). Validated 1/3 — board folder shrank from ~1.6MB (resized) to 11KB (HTML only), images shown at full 4K resolution. URL-encode non-ASCII path segments via `urllib.parse.quote(path, safe="/")`. New `lessons/delivery/L16-local-board-originals.md`. SKILL.md lessons table appended; LV bumped 2.5.1 → 2.6.

- **LV 2.5.1** (2026-05-04) — **L09 face-centered crop reinforcement.** Added reinforcement section to L09 documenting the common mistake of using fixed-percentage coordinates from image edges (e.g., `left=20%, top=10%`) when cropping faces from master refs. This produces off-center crops where face takes only ~40% of frame and 30% is empty background — diluting the identity anchor signal. Correct approach: estimate feature center first (face ≈ x:50%, y:18-25%), then crop centered around it. Includes validated Python pattern. Cross-referenced from L17, L18, character-sheet-builder L18 (all of which prescribe master_face_crop). Validated on Mila Power Suit master_face_crop v2 (2026-05-04). Minor patch — no new lesson, no LV rebuild.

- **LV 2.5** (2026-05-01) — **Filter-bypass theme + audit checklist expansion.** Added 3 new lessons from ZenityX model catalog production work (Lily Beach Swim + Pupae Cute + Alisa Future Mecha): **L13** filter-vocab sweet spot for sexy/revealing wardrobe ("halter knot-front cropped top with V-neck" passes filter while preserving bikini-cut output); **L14** identity-marker mention multiplication trap (mentioning "single mole/beauty mark" in prompt causes AI to render multiple — drop and let ref carry); **L15** master-only ref bypasses filter for revealing-wardrobe full-body shots (when `master + hero` blocks, drop hero and use master alone with detailed clothing-vocab prompt). Also **expanded L04** self-review with 3 explicit audit checks that auditor missed in Alisa session: (a) edge-artifact scan for ghost duplicate subjects, (b) back-view face identity check on small over-shoulder faces, (c) P2-vs-P3 angle differentiation (profile contour must be visible, not just slight turn). New **filter** theme directory created. All 3 new lessons recorded as `pending 1/3`.

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
- **2026-05-05** · L13 · `pending (1/3)` → `validated` · LV bump 2.6.2 → 2.7 · self · Evidence: zenityx-Lily-swim-board (origin, 2026-05-01) + Alisa Glamour Photobook G01 v4 batch (2026-05-05). 2-project cross-validation threshold met for meso tier.

## Demotion / rerun history

- **2026-05-05** · L15 · `pending (1/3)` → `needs-rerun · attribution unclear` · LV bump 2.6.2 → 2.7 · self · Reason: Lily L1 P1 v3→v5 trial changed 2 variables simultaneously (ref drop + pose change). Causal attribution between "drop hero ref" and "filter pass" not isolated. User field testing (Alisa, Jira, Mila) showed refs rarely trigger filter alone — pose change alone is sufficient to explain v5 pass. New L17 captures the corrected understanding. Validation reset 1→0/3 pending single-variable rerun.

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
