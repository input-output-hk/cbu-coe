# Claude Code Skills — Creation Best Practices

> Research compiled from Anthropic's official skill authoring guide,
> SmartScope skill-creator evaluation pipeline, and community patterns.
> Reference for CoE skill authors. Updated 2026-03-24.

---

## Skill Structure

A skill lives in a folder with this layout:

```
skills/<skill-name>/
  SKILL.md        # Claude-facing — loaded into context when skill activates
  README.md       # Human-facing — install, usage, why it works, credits
  references/     # Optional — supporting files the skill can reference
```

**Rules:**
- `SKILL.md` contains ONLY instructions for Claude. Every token counts.
- Human-facing content (how to install, why it works, credits) goes in `README.md`.
- Never place a standalone `README.md` inside the skill folder that duplicates
  SKILL.md content — keep audiences separate.
- Keep SKILL.md under 500 lines. Under 150 is ideal for token efficiency.

---

## SKILL.md Frontmatter

The frontmatter is how Claude discovers and selects skills. Get this wrong and
the skill either never activates or activates on everything.

```yaml
---
name: skill-name
description: >
  [WHAT] One sentence describing what the skill does.
  [WHEN — positive triggers] Use when/after [specific conditions].
  [WHEN — negative triggers] Do NOT use for [specific exclusions].
---
```

### Description Best Practices

| Do | Don't |
|---|---|
| Include specific trigger conditions | Say "universal" or "for all work" |
| List task types as keywords | Be abstract about when to use |
| Add negative triggers (Do NOT use for...) | Assume Claude will read the body to decide |
| Name the activity, not just the concept | Use only noun phrases |

**Why this matters:** Claude decides whether to load a skill based on the
description alone. If it's vague, Claude either over-triggers (activating on
simple questions) or under-triggers (deciding it can handle the task without
the skill).

### Example — Good vs Bad

Bad:
```yaml
description: >
  Universal quality gate for all work. Scores on dimensions and iterates.
```

Good:
```yaml
description: >
  Quality gate that scores work before delivery on Correctness, Completeness,
  Clarity, User Intent + domain-specific dimensions. Iterates to 9.0+
  automatically. Use after completing any non-trivial task: code, documents,
  architecture decisions, plans, analysis. Do NOT use for: simple questions,
  explanations, lookups, single-line edits, typo fixes.
```

---

## Naming Convention

Anthropic recommends **gerund form** (verb-ing): `processing-pdfs`,
`analyzing-spreadsheets`, `scoring-quality`.

**Noun phrases** (`quality-gate`, `peer-review`) are acceptable alternatives,
especially when the name is already established and referenced elsewhere.

Rule of thumb: if you haven't shipped yet, use gerund form. If the name is
already in use across repos and CLAUDE.md files, don't rename for convention
alone.

---

## SKILL.md Content — What to Include

Focus on what Claude needs to execute the skill correctly:

1. **One-line purpose** — what does this skill enforce?
2. **When this runs** — trigger conditions (reinforces frontmatter)
3. **Pre-task checklist** — catches problems before they happen
4. **Instructions / rubric** — the actual logic Claude follows
5. **Red flags / anti-patterns** — what NOT to do (negative examples)
6. **Default technique** — when multiple options exist, specify a default
7. **One concrete example** — input/output pair showing expected behavior

### What NOT to include in SKILL.md

These belong in README.md:

- Why this works (theory/explanation)
- Installation instructions
- Session hygiene tips
- Credits / authorship
- Contributing guidelines
- Evaluation scenarios (these are for humans testing the skill)

**Why:** Every token in SKILL.md is loaded into Claude's context window.
Human-facing content wastes context budget and dilutes the instructions.

---

## Examples — The Highest-Impact Addition

> "One example beats ten paragraphs of instructions."
> — SmartScope skill-creator guide

A concrete input/output example:
- Shows Claude the expected format and level of detail
- Removes ambiguity that prose instructions leave open
- Takes ~20 lines and is worth more than entire explanation sections

### Example Pattern

```markdown
## Example

Task: "[typical task description]"

### [Skill Output]

[Show what Claude should produce when the skill activates]

[If the skill iterates, show the iteration cycle briefly]
```

---

## Evaluation Scenarios

Create 3-5 test scenarios in README.md:

- **Positive triggers** — tasks where the skill SHOULD activate
- **Negative triggers** — tasks where the skill should NOT activate
- **Expected behavior** — what the output should look like

Without evals, you cannot verify:
- Whether the skill actually activates when it should
- Whether it interferes with simple tasks
- Whether updates cause regressions

---

## Enforcement Layers

Skills alone are passive — Claude may or may not use them. Enforcement options
from weakest to strongest:

| Layer | Mechanism | Reliability |
|---|---|---|
| Skill exists in `.claude/skills/` | Claude discovers via description | Low — depends on description quality |
| CLAUDE.md instruction | "invoke skill X before completing tasks" | Medium — Claude usually follows |
| Hook in `settings.json` | Terminal reminder after each response | Low — reminder only, not enforced |
| Superpowers skill (system prompt) | Loaded automatically, appears in skill list | High — system-level integration |

For critical skills, use **skill + CLAUDE.md instruction** together.

---

## Common Anti-Patterns

| Anti-pattern | Problem | Fix |
|---|---|---|
| Mixing audiences in SKILL.md | Wastes tokens on human-facing content | Split into SKILL.md + README.md |
| Vague description | Skill doesn't activate reliably | Add trigger + negative trigger keywords |
| No examples | Claude guesses the expected format | Add one concrete input/output pair |
| Too many options without defaults | Claude picks randomly or freezes | Specify a default, list alternatives |
| Installing as command not skill | Registers as `/command`, not auto-discoverable skill | Use `.claude/skills/<name>/SKILL.md` |
| No evaluation scenarios | Can't verify skill works or detect regressions | Add 3-5 test cases in README.md |
| Over-long SKILL.md (300+ lines) | Context window pollution | Move non-essential content to README.md |

---

## Checklist — Before Shipping a Skill

- [ ] Description has WHAT + WHEN (positive triggers) + WHEN NOT (negative triggers)
- [ ] SKILL.md contains only Claude-facing instructions
- [ ] Human-facing content is in README.md
- [ ] SKILL.md is under 150 lines (ideal) or 500 lines (max)
- [ ] At least one concrete example with input/output
- [ ] Red flags / anti-patterns section for known failure modes
- [ ] Default specified when multiple techniques exist
- [ ] 3-5 evaluation scenarios in README.md
- [ ] Installed in `.claude/skills/<name>/SKILL.md` (not commands)
- [ ] CLAUDE.md enforcement line added if automatic activation needed

---

## Sources

- [Anthropic — Claude Code Skills Best Practices](https://docs.anthropic.com/en/docs/claude-code/skills)
- [SmartScope — Skill Creator & Eval Pipeline Guide](https://smartscope.blog/en/generative-ai/claude/skill-creator-eval-pipeline-guide/)
- [SmartScope — Claude Code Skills Deep Dive](https://smartscope.blog/en/generative-ai/claude/claude-code-skills-deep-dive/)
- CoE internal review of quality-gate skill (2026-03-24)
