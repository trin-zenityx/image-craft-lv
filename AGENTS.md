# AGENTS.md

This repo is an **agent skill**: `SKILL.md` at the root is the entry point (frontmatter `name` + `description`),
the other files are its references. Read `SKILL.md` fully before using the skill.

- **Codex:** to install for all folders, clone or symlink this repo as `~/.agents/skills/image-craft-lv/`
  (Codex discovers `~/.agents/skills/*/SKILL.md`). Then pick it with `$` or `/skills`.
- **Claude Code:** clone it as `~/.claude/skills/image-craft-lv/`.
- When you change the skill: bump the level/CHANGELOG as the skill describes, keep `name`/`description` valid
  (description ≤ 1024 chars), and never commit API keys or tokens.
- Copies of this skill may be vendored into project repos (`.agents/skills/image-craft-lv/`) by a sync script; edit this
  repo, not the copies.
