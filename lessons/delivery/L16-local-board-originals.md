---
id: L16
title: Local review boards reference originals via file:// — never copy + resize
theme: delivery
added_at_lv: 2.6
tags: [delivery, review-board, local-html, file-reference, disk-usage, image-quality, avif-thumbs, click-to-zoom-modal]
created: 2026-05-04
last_updated: 2026-05-04
supersedes: []
related: [L07]
---

# L16 — Local review boards reference originals via file:// — never copy + resize

## TL;DR

For HTML review boards opened locally on the user's machine (audit dashboards, comparison boards, before/after pages), reference original image files via `file:///absolute/path/to/original.png` URLs. **Never copy + resize images into the board folder.** Originals stay full-resolution, no disk waste, no quality loss, edits to source propagate instantly.

## Context

L4 Mila Power Suit redo session (2026-05-04). Built `/tmp/l4_redo_board/index.html` to show user 6 images (master + hero + 4 plates) for audit before composite + ship. Default reflex was to `sips -Z 1200 -s formatOptions 88` everything into the board folder.

User flagged it: "ทำไมภาพไม่ชัด เหมือนภาพถูกย่อ ขนาดเหลือ 179 kb". After bumping to 2048×q95 (2nd attempt), user pointed out the deeper issue: "ถ้าบอร์ด ที่เปิดใน PC คุณไม่จำเป็นต้องย่อไฟล์ภาพหนิ คุณแค่ระบุตำแหน่งของภาพต้นฉบับก็พอ จะได้ไม่ต้องเปลืองพื้นที่ด้วย และได้ภาพขนาดเต็ม อย่าลืมว่า มันใช้ใน Local".

## Mistake

Defaulted to "downsize everything into the board folder" because that's the pattern for **public web deploy** (Vercel uploads, FB/IG posts, R2 catalog). Did not consider that local boards have entirely different constraints:
- No bandwidth cost (file:// is instant local read)
- No image upload step
- User has full disk access — no need to bundle
- Originals live next door

Result: 6 originals (~50MB combined) → resized JPGs (~1.6MB combined) at degraded quality. Twice as many files on disk for worse output.

## Why it happened

Conflated two different deliverable contexts:
1. **Public web** (catalog, FB, social posts) → MUST resize/optimize for bandwidth + filesize quotas
2. **Local review board** (audit before ship, comparison page on user's PC) → MUST reference originals for full quality + zero copy overhead

The skill's previous lessons (L07 reviewable artifacts) covered "package as one HTML" but didn't specify the asset-handling discipline.

## Fix

**Decision rule before building any HTML board:**

| Board type | Asset strategy | Why |
|---|---|---|
| **Local review · ≤10 images** | `file:///abs/path/original.png` direct + click-to-zoom | Full quality, zero copy, edits propagate |
| **Local review · >10 images** | AVIF q90 thumbs in `_thumbs/` + click-to-zoom links full original | Avoid Chrome strain on multi-image grids |
| **Cloudflare/Vercel deploy** (public URL) | Copy + resize 2048px q95 to board folder | Bandwidth + R2 quota |
| **Email/Slack share** (single recipient) | Copy + resize 2048px q95 to board folder | Recipient won't have file paths |

Rule: **if the path starts with `/tmp/` or `~/Desktop/`, default to file:// references for the originals; use AVIF thumbs in grid view if image count > 10.** Only full-resize copy when deploying to a remote URL.

**Universal:** click-to-zoom is required on every internal review board so the user can review at full resolution. **Visual presentation of the zoom (modal · lightbox · side panel · new tab) is per-board freedom — not codified here.**

**Technical primitives** (thumb size formula, AVIF generator, XSS-safe DOM updates, path encoding, perf attributes, drop-in modal snippets) live in the **`internal-board-builder`** skill (`~/.claude/skills/internal-board-builder/`) — single source of truth. Each board imports primitives from `lib/` and designs its own layout. Layout/field-arrangement/theme decisions are intentionally NOT codified — each board's freedom.

### Code pattern (validated)

```html
<!-- ✓ correct for local board -->
<img src="file:///Users/trin/Claude-Workspace/Studio/.../master.jpeg" alt="master">

<!-- ✗ wrong for local board (only correct for public deploy) -->
<img src="master.jpg" alt="master">
```

URL-encode any non-ASCII path segments (Thai folder names, spaces) — e.g. `ภาพ นางแบบ` → `%E0%B8%A0%E0%B8%B2%E0%B8%9E%20%E0%B8%99%E0%B8%B2%E0%B8%87%E0%B9%81%E0%B8%9A%E0%B8%9A`.

In Python:

```python
from urllib.parse import quote
src = "file://" + quote(str(absolute_path), safe="/")
```

## Broader rule

**Match asset strategy to delivery target.** Local = reference originals. Remote = bundle optimized copies. Never copy when copying gains nothing.

## Cross-references

- Related lessons: L07 (reviewable artifacts — this lesson refines L07's asset-handling)
- Checklist items affected: post-generate review board build
- Skill bump: LV 2.5.1 → LV 2.6

## Reinforcement (added 2026-05-04)

**Anti-pattern to detect at session start:** if you're about to run `sips -Z`, `magick convert -resize`, or `cp <original> <board_folder>/<smaller>.jpg`, ask first: "Is this board going to a remote URL or staying local?" If local → revert to file:// refs.

**Audit hook for self-review (post-board build):**
- Did I copy any images into the board folder? → If board is local, that's a violation.
- Are the images still full original resolution? → Open the board, right-click → "View Image Info" / inspect element.
- Does the board still work if I edit/regen one of the source images? → file:// refs auto-update. Copies don't.
