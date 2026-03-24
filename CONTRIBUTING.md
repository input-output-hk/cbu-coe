# Contributing to cbu-coe

Thanks for considering a contribution. This repo provides guidance and reusable
materials for CBU engineering teams — templates, skills, and standards.

## How to contribute

1. **Fork or branch.** Create a feature branch from `main`.
2. **Make your changes.** Follow the [communication standards](CLAUDE.md#communication-standards) — collaborative tone, technical precision, no unsupported claims.
3. **Open a PR.** Describe *why* the change is useful, not just *what* changed.
4. **Review.** CoE (@dorin100) reviews and merges.

## What belongs here

- **CLAUDE.md / AGENTS.md templates** — role-based or project-specific AI configuration
- **Skills** — Claude Code skills that improve output quality (see `skills/`)
- **Knowledge** — research and best practices for CoE topics (see `golden-paths/knowledge/`)
- **ADRs** — decisions that affect this repo's structure or content (see `docs/decisions/`)

## What belongs in cbu-coe-toolkit

Measurement models, scoring rules, scan scripts, scan results, automation.
If it measures something, it goes in [cbu-coe-toolkit](https://github.com/input-output-hk/cbu-coe-toolkit).

## Style guidelines

- Keep CLAUDE.md templates under 300 lines. Use progressive disclosure.
- Skills follow the structure in `golden-paths/knowledge/skills-creation/best-practices.md`.
- No secrets, tokens, or credentials in any file.

## Questions?

Open an issue or reach out in `#ai-collaboration-circles` on Slack.
