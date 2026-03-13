# CLAUDE.md — cbu-coe

> Root context file for AI agents working in this repository.
> Keep under 300 lines. Link to detail files rather than inlining everything.

## Repository Identity

- **Repo:** `cbu-coe`
- **Purpose:** Knowledge, guidance, and reusable materials for CBU engineering teams
- **Owner:** Dorin Solomon, CoE Head, Cardano Business Unit (CBU) at IOG
- **Audience:** Engineers, PMs, architects, QA — anyone adopting engineering practices
- **Sibling repo:** `cbu-coe-toolkit` (measurement machinery, scan prompts, scoring — not in this repo)

## What This Repo Contains

```
cbu-coe/
├── CLAUDE.md                         ← You are here
├── README.md                         # Human-readable overview
├── golden-paths/                     # Reusable materials across the SDLC
│   ├── ai-config/                    # CLAUDE.md / AGENTS.md templates
│   │   ├── by-role/                  # Role-based starter templates
│   │   └── by-project/               # Project-specific overlays
│   ├── ci-cd/                        # CI/CD templates and patterns
│   ├── security/                     # Security baselines and checklists
│   └── testing/                      # Testing strategy templates
├── guides/                           # Engineering guides and standards
│   ├── development-guide.md          # MV-EOS Development Guide
│   ├── sdlc/                         # SDLC process documentation
│   └── onboarding/                   # New engineer onboarding materials
└── docs/
    └── contributing.md               # How to contribute to this repo
```

## Organizational Context

### Who We Serve

CBU encompasses Cardano blockchain development (Haskell), Hydra (Haskell), Mithril (Rust), and Leios (Haskell). The CoE exists to improve predictability, quality, and delivery speed across all CBU projects.

### Stakeholder Sensitivities

- **Haskell engineers** are extremely technical. They require precision in communication and respect for their domain expertise. Never be vague or make unsupported claims about AI value. Frame everything as "adding to" their capabilities, never "replacing" their judgment.
- **Project leaders** are under delivery pressure. Materials from this repo should reduce their burden, not add process overhead.
- **Leadership (VP, CEO)** care about predictability and data-driven reporting. Materials should connect to delivery outcomes, not just process compliance.

### Resistance Patterns

- Anything that resembles "corporate bureaucracy" triggers pushback.
- AI skepticism is real — many engineers believe AI cannot handle Haskell complexity.
- Teams have historically operated without strong Product/UX involvement.

## Communication Standards

All content in this repo follows these language principles:

- **Tone:** Collaborative, clear, actionable — never directive or bureaucratic.
- **Avoid:** "must", "your role is", "you need to", "mandatory", "required".
- **Prefer:** "consider", "we recommend", "teams that have found success with…", "a good starting point is…"
- **Framing:** "Adding to" not "replacing" existing practices.
- **Business case:** Always make the connection to Intersect commitments, ecosystem growth, or user adoption explicit.
- **Technical precision:** Especially when addressing Haskell teams. Vague claims undermine credibility.
- **No unsupported value claims:** Do not say AI augmentation delivers "exponential value" unless Engineering Vitals data backs it up.

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

1. **Read the project brief first** if you need full context — ask the human operator for it.
2. **Respect the tone guidelines** above in all content you create or edit.
3. **Keep CLAUDE.md templates under 300 lines.** Use progressive disclosure.
4. **Do not create measurement or scoring content here.** That belongs in `cbu-coe-toolkit`.
5. **Test any commands you include** in templates — they should work out of the box.
6. **Propose changes via PR descriptions** that explain *why*, not just *what*.
7. **When unsure, ask.** The human operator (Dorin) reviews everything.

## Key References

- Project brief: ask the human operator (contains full organizational context, model definitions, implementation plan)
- Confluence CoE page: `https://input-output.atlassian.net/wiki/spaces/IOE/pages/5700845586/`
- Sibling repo: `cbu-coe-toolkit` (measurement, scans, automation)
