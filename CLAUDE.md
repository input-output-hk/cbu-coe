# CLAUDE.md — cbu-coe

> Context file for AI agents. Under 200 lines. Use progressive disclosure.

## Project

- **Repo:** `cbu-coe` — guidance, templates, and skills for CBU engineering teams
- **Owner:** Centre of Excellence (CoE), Cardano Business Unit, IOG
- **Audience:** Engineers, PMs, architects, QA across CBU
- **Sibling:** [`cbu-coe-toolkit`](https://github.com/input-output-hk/cbu-coe-toolkit) — measurement models, scans, automation

## Structure

```
cbu-coe/
├── golden-paths/ai-config/       # CLAUDE.md / AGENTS.md starter templates
│   ├── by-role/                   # 8 roles (Haskell, Rust, TS, QA, DevOps, ...)
│   └── by-project/                # 4 projects (cardano-node, mithril, hydra, lace)
├── skills/quality-gate/           # Quality gate skill (self-score → 9.0+)
└── docs/
    ├── decisions/                 # Architecture Decision Records (ADRs)
    ├── learnings.md               # Operational insights log
    └── knowledge/                 # Reference sources for CoE topics
```

## Source of truth

1. **GitHub** (this repo + toolkit) — definitions, templates, scoring rules
2. **Confluence** — entry point, published guidance
3. **Notion** — display layer for scan results

When they diverge, GitHub wins.

## Content principles

- Collaborative tone — "consider", "a good starting point", not "must" or "required"
- Technical precision — vague claims undermine credibility with CBU teams
- No unsupported value claims — back with Engineering Vitals data or don't claim
- Add to existing practices, never replace

## Rules

1. **Never commit to `main`.** Branch → PR → owner review → merge.
2. **Never expose secrets.** No printing, logging, or committing API keys, tokens, passwords, or env variable values. Reference by name only (`$GITHUB_TOKEN`).
3. **Check for secrets before every commit.** Run `git diff --cached`, review every line, check `git status` for files that should not be tracked.
4. **Quality gate.** Invoke the `quality-gate` skill before declaring any task complete. Skip for questions, explanations, and simple lookups.
5. **Read context first.** Start every session by reading `docs/learnings.md` and scanning `docs/decisions/`.
6. **Validate skills against sources.** Before creating or modifying a skill, consult `docs/knowledge/skills-creation/best-practices.md`.
7. **Templates under 300 lines.** Use progressive disclosure.
8. **No measurement content here.** Scoring, models, scan scripts belong in `cbu-coe-toolkit`.
9. **PRs explain why**, not just what.
10. **When unsure, ask.**

## Session handoff

Before ending a session, propose knowledge capture:

1. **Learnings** — draft entries for `docs/learnings.md` (format: `- **Title:** Description` under a dated heading).
2. **Decisions** — if significant choices were made, draft an ADR following `docs/decisions/000-template.md`.
3. **Present to the operator for review.** Do not commit without approval.

## References

- [Confluence CoE page](https://input-output.atlassian.net/wiki/spaces/IOE/pages/5700845586/)
- Sibling repo: `cbu-coe-toolkit`
