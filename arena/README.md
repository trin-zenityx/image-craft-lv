# Arena — Auto-Leveling Synthetic Validation

> LV 2.2 subsystem. Lets lessons promote `pending → validated` when real
> projects are rare. Designed to resist Goodhart's law via adversarial
> scenarios + skeptic review + pre-registered criteria + blinded runner.

## One-line flow

`/arena run L##` → Generator → **you approve scenario** → Runner (blinded)
→ Judge → Skeptic → ledger update or void → archive.

## Components

| Path | Purpose |
|------|---------|
| `axes.md` | 9 axes of scenario diversity + DHYANA baseline + anti-reuse rule |
| `prompts/generator-prompt.md` | 🎲 Scenario + criteria generator |
| `prompts/runner-prompt.md` | 🖌️ Blinded test runner (real image gen) |
| `prompts/judge-prompt.md` | ⚖️ Evaluates against pre-registered criteria |
| `prompts/skeptic-prompt.md` | 🕵️ Anti-Goodhart challenger |
| `criteria/L##-criteria.md` | Per-lesson pass-criteria templates |
| `scenario-bank/README.md` | Index of every scenario run (axis fingerprint, outcome) |
| `trial-records/<date>-L##-S##/` | Per-trial archive |
| `run-playbook.md` | Step-by-step dispatch instructions (MVP copy-paste) |
| `void-log.md` | Rejected trials (not counted in ledger) |
| `tools/` | Reserved for Phase 2 Python quant scripts |

## Roles (one fresh Claude subagent session each)

- **🎲 Generator** — reads lesson + DHYANA profile + scenario-bank index,
  produces one scenario that flips ≥3 of 9 axes from DHYANA and ≥2 axes
  from any prior scenario for the same lesson. Also writes
  pre-registered `criteria.md`.
- **🖌️ Runner** — receives ONLY the scenario (no knowledge of which
  lesson is being tested). Invokes image-craft-lv normally. Makes real
  Nano Banana calls. Produces images + prompt log.
- **⚖️ Judge** — evaluates images against locked criteria. Cannot modify
  criteria. Returns pass / partial / fail / criteria-broken.
- **🕵️ Skeptic** — reviews full trial record. Returns `adversarial-valid`,
  `void-too-easy`, `void-criteria-weak`, or `void-lesson-unnecessary`.

## Promotion arithmetic (updated LV 2.2 rule)

- Each arena trial counted only if **axis-distinct** from every prior
  trial for the same lesson (≥2 of 9 axes must differ).
- `DHYANA` and `arena:SXX` are always distinct projects.
- Meso promotion: 2 passes across ≥2 axis-distinct projects.
- Macro promotion: 3 passes across ≥3 axis-distinct projects.

## Safeguards

1. Human approves scenario before Runner burns API credit.
2. Per-trial hard cost cap: $2. Runner aborts if exceeded.
3. Skeptic can void a trial even if Judge passed it.
4. Axis-diversity rule rejects near-duplicate scenarios.
5. Criteria is git-committed BEFORE Runner runs — moving the
   goalpost is physically impossible after that.
6. Runner is blinded — does not know which lesson is tested.
7. Lessons that void 3 times consecutively get flagged
   `arena-unresolvable` and must be rewritten or retired.

## First-time user

Read `run-playbook.md` next. Start with an easy lesson (L09 —
crop refs is self-contained and cheap to test).

## Full design rationale

See spec `2026-04-17-image-craft-lv-arena-design.md` (in the upstream
Seedance worktree that birthed this subsystem).
