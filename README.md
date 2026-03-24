# cbu-coe

Guidance, templates, and skills for CBU engineering teams at IOG.

This repo is the **guidance layer** of the CBU Centre of Excellence. Teams adopt materials directly — no measurement infrastructure needed. The companion repo [cbu-coe-toolkit](https://github.com/input-output-hk/cbu-coe-toolkit) holds the measurement machinery (models, scans, scoring).

---

## What's here

### AI config templates — [`golden-paths/ai-config/`](golden-paths/ai-config/)

Starter `CLAUDE.md` and `AGENTS.md` files that give AI assistants context about your project.

- **[`by-role/`](golden-paths/ai-config/by-role/)** — 8 roles: Haskell, Rust, TypeScript developer, test engineer, DevOps/SRE, release manager, project manager, architect
- **[`by-project/`](golden-paths/ai-config/by-project/)** — overlays for cardano-node, mithril, hydra, lace

Pick the template closest to your role, adapt it, and you have a working AI configuration in minutes.

### Quality gate skill — [`skills/quality-gate/`](skills/quality-gate/)

A Claude Code skill that scores work against a structured rubric and iterates to 9.0+ before delivering. Works for code, documents, plans, architecture decisions, and QA artefacts. See the [install guide](skills/quality-gate/README.md).

### Documentation — [`docs/`](docs/)

- [`decisions/`](docs/decisions/) — Architecture Decision Records
- [`learnings.md`](docs/learnings.md) — operational insights accumulated across sessions
- [`knowledge/`](docs/knowledge/) — reference sources for CoE topics

---

## Who this is for

Engineers, PMs, architects, QA — anyone in CBU working with AI tools. Materials here add to existing practices, not replace them.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Open a pull request describing why the change is useful. CoE ([@dorin100](https://github.com/dorin100)) reviews and merges.

---

## Related

- [cbu-coe-toolkit](https://github.com/input-output-hk/cbu-coe-toolkit) — measurement models, scan scripts, results
- [CoE Confluence page](https://input-output.atlassian.net/wiki/spaces/IOE/pages/5700845586/) — entry point and published guidance

---

© Input Output Global, Inc.
