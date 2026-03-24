# Learnings

Operational insights discovered during work on this repo. Newest first. Contributors propose entries; the repo owner reviews before committing.

---

### 2026-03-24 — Skills architecture

- **Skills belong in `.claude/skills/`, not `.claude/commands/`.** Commands register as on-demand slash commands. Skills in `.claude/skills/<name>/SKILL.md` are auto-discoverable. Fixed across both repos.
- **SKILL.md is for Claude, README.md is for humans.** Mixing audiences wastes context tokens. The quality-gate SKILL.md was halved by moving human-facing content to README.md.
- **The description field drives skill discovery.** Include: what it does, when to trigger, when not to trigger. Vague descriptions cause unreliable activation.
- **One example outweighs paragraphs of instructions.** A concrete input/output pair removes ambiguity that prose cannot.

### 2026-03-13 — Initial setup

- **Repo scaffolded per project brief v1.1.** Both `cbu-coe` and `cbu-coe-toolkit` follow the same structure.
- **Three-layer knowledge capture adopted.** Decisions, learnings, and session handoff. See ADR-001.
