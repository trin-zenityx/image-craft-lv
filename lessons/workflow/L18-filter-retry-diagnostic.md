---
id: L18
title: "[MIGRATED] Filter R1→R5 retry playbook → filter-craft-lv/PLAYBOOK.md"
theme: workflow
status: migrated
migrated_at_lv: 2.13
related: [L13, L17]
---

# L18 — MIGRATED to `filter-craft-lv`

The "filter blocks are free → R1→R5 escalation playbook" (classify-first, parallel
free retries, vocab trim at R3, pose redesign at R5) now lives at:

→ **`filter-craft-lv/PLAYBOOK.md`** (full) + **`filter-craft-lv/SKILL.md`** (summary)
→ failure classification: **`filter-craft-lv/ERROR-CODES.md`** + `scripts/classify_fail.py`

Invoke **filter-craft-lv** whenever a generation fails or returns a filter error.
