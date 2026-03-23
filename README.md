# cbu-coe

Knowledge, guidance, and reusable tools for CBU engineering teams at IOG.

This repo is the **guidance layer** of the CBU Centre of Excellence. It contains
templates, skills, and standards that teams can adopt directly — no measurement
infrastructure needed. The companion repo
[cbu-coe-toolkit](https://github.com/input-output-hk/cbu-coe-toolkit) holds the
measurement machinery.

---

## What's here

### `golden-paths/ai-config/`

Starter templates for `CLAUDE.md` and `AGENTS.md` — the configuration files
that give AI assistants context about your project.

- **`by-role/`** — 8 role-based templates: Haskell developer, Rust developer,
  TypeScript developer, test engineer, DevOps/SRE, release manager, project
  manager, architect
- **`by-project/`** — project-specific overlays for cardano-node, mithril,
  hydra, lace

Pick the template closest to your role, adapt it to your project, and you have
a working AI configuration in minutes.

### `skills/quality-gate/`

A universal quality gate for Claude Code. Before declaring any task complete,
Claude scores its work on a structured rubric and iterates to 9.0+ before
delivering. Works for code, documents, plans, architecture decisions, and QA
artefacts.

See [`skills/quality-gate/README.md`](skills/quality-gate/README.md) for
installation instructions.

### `docs/`

- `decisions/` — Architecture Decision Records for this repo
- `learnings.md` — operational insights accumulated across sessions

---

## Who this is for

Engineers, PMs, architects, QA — anyone in CBU who wants to work more
effectively with AI tools. Materials here are designed to add to existing
practices, not replace them.

---

## Contributing

Open a pull request. CoE (@dorin100) reviews and merges. When proposing new
templates or skills, include a brief note on what problem they solve and who
they are for.

---

## Related

- [cbu-coe-toolkit](https://github.com/input-output-hk/cbu-coe-toolkit) —
  measurement models, scan scripts, results history
- [CoE Confluence page](https://input-output.atlassian.net/wiki/spaces/IOE/pages/5700845586/) —
  entry point and published guidance (internal)

---

© Input Output Global, Inc. Internal use.
