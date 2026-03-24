<!-- Scope: Append-only log of operational insights discovered during agent sessions. Edge cases, technical discoveries, process improvements. Agents propose new entries at the end of each session. -->

# Learnings Log

Newest entries first. Each entry includes the date and a brief context tag.

---

### 2026-03-24 — Skills creation best practices

- **Skills go in `.claude/skills/`, not `.claude/commands/`:** Commands register as `/slash-commands` (on-demand). Skills in `.claude/skills/<name>/SKILL.md` are auto-discoverable by Claude. The quality-gate was incorrectly installed as a command; fixed across cbu-coe and cbu-coe-toolkit.
- **SKILL.md is Claude-facing only:** Human-facing content (install instructions, why it works, credits, session hygiene) wastes context tokens. Split into SKILL.md (Claude) + README.md (humans). Reduced quality-gate SKILL.md from ~188 lines to ~120 lines.
- **Description field drives discovery:** Claude decides whether to load a skill based on the description alone. Must include: WHAT it does, WHEN to trigger (positive), WHEN NOT to trigger (negative). Vague descriptions like "universal gate for all work" cause unreliable activation.
- **One example > ten paragraphs:** A concrete input/output example removes ambiguity that prose instructions leave open. Added scorecard example to quality-gate.
- **Validate future skills against best practices:** Before creating or shipping any new skill, review `docs/knowledge/skills-creation/best-practices.md` — includes checklist, anti-patterns, and sourced guidance from Anthropic and SmartScope.

---

### 2026-03-13 — Initial setup

- **Directory scaffolding complete:** Both repos scaffolded per project brief v1.1 Section 3. All placeholder files created with scope comments.
- **Knowledge capture system adopted:** Three-layer system (decisions, learnings, session handoff) in place for both repos. See ADR-001.
