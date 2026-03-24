# CLAUDE.md — cbu-coe

> Root context file for AI agents working in this repository.
> Keep under 300 lines. Link to detail files rather than inlining everything.

## Repository Identity

- **Repo:** `cbu-coe`
- **Purpose:** Knowledge, guidance, and reusable materials for CBU engineering teams
- **Owner:** CoE (Centre of Excellence), Cardano Business Unit (CBU) at IOG
- **Audience:** Engineers, PMs, architects, QA — anyone adopting engineering practices
- **Sibling repo:** `cbu-coe-toolkit` (measurement machinery, scan prompts, scoring — not in this repo)

## What This Repo Contains

```
cbu-coe/
├── CLAUDE.md                         ← You are here
├── README.md                         # Human-readable overview
├── golden-paths/                     # Reusable materials — only what exists
│   ├── ai-config/                    # CLAUDE.md / AGENTS.md templates
│   │   ├── by-role/                  # Role-based starter templates (8 roles)
│   │   └── by-project/               # Project-specific overlays (4 projects)
│   └── knowledge/                    # Research & best practices for CoE topics
│       └── skills-creation/          # Claude Code skills authoring guide
├── skills/                           # Claude Code skills — CoE quality tools
│   └── quality-gate/
│       └── SKILL.md                  # Universal quality gate (self-score + iterate)
└── docs/
    ├── decisions/                    # Architecture Decision Records (ADRs)
    │   └── NNN-title.md             # One file per decision (see 000-template.md)
    ├── learnings.md                  # Append-only operational insights log
    └── contributing.md               # How to contribute to this repo
```

## Knowledge Capture System

This repo uses a three-layer system to preserve learnings across agent sessions (see ADR-001):

1. **`docs/decisions/`** — Architecture Decision Records. One file per significant decision, numbered sequentially. Read these first to understand constraints you should not re-litigate.

2. **`docs/learnings.md`** — Append-only operational insights. Edge cases, technical discoveries, process improvements. Read this to avoid repeating mistakes.

3. **Session handoff protocol** — See "Before Ending Any Session" in Agent Instructions below.

**Start of every session:** Read `docs/learnings.md` and scan `docs/decisions/` to load accumulated context.

## Communication Standards

All content in this repo follows these language principles:

- **Tone:** Collaborative, clear, actionable — never directive or bureaucratic.
- **Avoid:** "must", "your role is", "you need to", "mandatory", "required".
- **Prefer:** "consider", "we recommend", "teams that have found success with…", "a good starting point is…"
- **Framing:** "Adding to" not "replacing" existing practices.
- **Business case:** Make the connection to Intersect commitments, ecosystem growth, or user adoption explicit where relevant.
- **Technical precision:** CBU teams work with complex, specialized codebases. Vague or unsupported claims undermine credibility.
- **No unsupported value claims:** Do not claim AI augmentation delivers specific value unless Engineering Vitals data backs it up.

## Working With Golden Path Templates

### AI Config Templates (`golden-paths/ai-config/`)

- `by-role/` contains CLAUDE.md starter templates for 8 roles: Haskell developer, Rust developer, TypeScript developer, test engineer, DevOps/SRE, release manager, project manager, architect.
- `by-project/` contains project-specific overlays for cardano-node, mithril, hydra, lace.
- Templates should be **under 300 lines**, use **progressive disclosure** (reference detail files, don't inline), and include **actionable commands** (build, test, lint).

### Template Design Principles

1. Language-specific — Haskell, Rust, TypeScript have very different toolchains.
2. Non-prescriptive — use the collaborative tone defined above.
3. Composable — a role template + project overlay = a team-specific CLAUDE.md.
4. Self-improving — the scan agent in `cbu-coe-toolkit` observes template adoption and proposes improvements via PR.

## The Three-Model Architecture (Context)

The CoE operates three complementary measurement instruments. This repo provides the *guidance* layer; the *measurement* layer lives in `cbu-coe-toolkit`.

| Model | What It Measures | Where Defined |
|---|---|---|
| **Engineering Vitals Dashboard** | On-time delivery, value, cycle time, defects | Power BI (external) |
| **AI Augmentation Model** | Institutional AI readiness per repo | `cbu-coe-toolkit/models/ai-augmentation/` |
| **Capability Maturity Model** | Engineering practices, processes, standards | `cbu-coe-toolkit/models/capability-maturity/` |

Key principle: AI Augmentation stages are **informative and educational**, not performance judgment. The goal is showing teams what good looks like so they know what to focus on next.

## Source of Truth Hierarchy

1. **Confluence CoE page** → what the CoE is and how people find/use things ("front door")
2. **GitHub repos** (this repo + toolkit) → actual model definitions, templates, scoring rules ("engine")
3. **Notion** → display/presentation layer for scan results and dashboards ("dashboard")

When they diverge, GitHub wins.

## Agent Instructions

When working in this repo:

1. **Quality gate** — invoke the `quality-gate` skill before declaring any task complete. Skip for questions, explanations, and simple lookups.
2. **Skills validation** — before creating or modifying any skill, read `golden-paths/knowledge/skills-creation/best-practices.md` and validate against its checklist.
2. **Start by reading `docs/learnings.md` and scanning `docs/decisions/`.** This is accumulated context from all previous sessions.
2. **Respect the tone guidelines** above in all content you create or edit.
3. **Keep CLAUDE.md templates under 300 lines.** Use progressive disclosure.
4. **Do not create measurement or scoring content here.** That belongs in `cbu-coe-toolkit`.
5. **Test any commands you include** in templates — they should work out of the box.
6. **Propose changes via PR descriptions** that explain *why*, not just *what*.
7. **Before every commit — check for secrets.** Scan for API keys, tokens, passwords, private keys, `.env` files, or any credentials. Run `git diff --cached` and review every line. Check `git status` for files that should not be tracked. No internal URLs with auth tokens, no personal data, no sensitive organizational context. If in doubt, ask before committing. A leaked secret is harder to fix than a delayed commit.
8. **When unsure, ask.** The human operator reviews everything.

### Before Ending Any Session

**This step is not optional.** Before wrapping up, propose knowledge capture:

1. **Learnings:** Draft specific entries for `docs/learnings.md` — things discovered, edge cases hit, technical insights, anything the next agent would benefit from knowing. Use the format: `- **Short title:** Description.` under a dated heading.

2. **Decisions:** If any significant choices were made during the session (architectural, methodological, process-related), draft an ADR file following `docs/decisions/000-template.md`. Number it sequentially.

3. **Present all proposed additions to the human operator for review.** Do not commit without approval.

If the session produced no new learnings (unlikely), state that explicitly so the human operator knows you considered it.

## Key References

- Confluence CoE page: `https://input-output.atlassian.net/wiki/spaces/IOE/pages/5700845586/`
- Sibling repo: `cbu-coe-toolkit` (measurement, scans, automation)
