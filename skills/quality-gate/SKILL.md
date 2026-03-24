---
name: quality-gate
description: >
  Quality gate that scores work before delivery on Correctness, Completeness,
  Clarity, User Intent + domain-specific dimensions. Iterates to 9.0+
  automatically. Use after completing any non-trivial task: code, documents,
  architecture decisions, plans, analysis, QA artefacts. Use when task involves
  implementation, creation, or design. Do NOT use for: simple questions,
  explanations, lookups, single-line edits, typo fixes.
---

# Quality Gate

Score every non-trivial output before delivery. If below 9.0, improve and
re-score. Maximum 2 iterations. Deliver the best version directly — never
surface intermediate drafts, never ask for approval before improving.

---

## Pre-Task Checklist

Before producing output:

- Is the approach clear? If not — outline first, then implement.
- Is the task complex (3+ moving parts)? If yes — break into steps.
- Is an example of good output available? If yes — reference it explicitly.

---

## Self-Scoring Rubric

### Universal dimensions (always scored)

| Dimension | What it measures |
|---|---|
| **Correctness** | Factually and logically right; edge cases handled |
| **Completeness** | All requirements met, including implicit ones |
| **Clarity** | Clear to the target audience — engineer, PM, or stakeholder |
| **User Intent** | Solves what was meant, not just what was literally asked |

### Domain extensions (activate based on task type)

**Code / technical implementation**
- Code Quality — readable, idiomatic, a senior engineer approves without comments
- Performance — efficient for the context, no obvious waste
- Security — no vulnerabilities introduced, inputs validated

**Architecture / design decisions**
- Trade-off Analysis — alternatives considered, reasoning explicit
- Simplicity — no unnecessary complexity introduced
- Future-proofing — handles foreseeable change without full rewrite

**Documents / plans / requirements**
- Actionability — reader knows exactly what to do next
- Risk Coverage — failure modes and mitigations identified
- Stakeholder Alignment — works for all audiences named in the task

**QA / testing**
- Coverage — happy path, edge cases, and failure paths addressed
- Reproducibility — steps are deterministic, environment assumptions stated
- Edge Case Handling — boundary conditions explicit, not assumed

---

## Scoring Rules

1. Score the 4 universal dimensions on every task.
2. Identify the task type → add the relevant domain dimensions.
3. Mark a dimension N/A only when it genuinely cannot apply.
4. If overall average ≥ 9.0 → deliver output + show scorecard.
5. If overall average < 9.0 → identify specific improvements, implement them,
   re-score, then deliver the improved version.
6. Maximum 2 improvement iterations. If still below 9.0 after 2 passes,
   deliver the best version and flag remaining gaps explicitly.

---

## Red Flags (score inflation patterns)

| Pattern | Problem |
|---|---|
| Every dimension 9.0+ on first pass | Inflation — push back on yourself |
| All scores identical across dimensions | Lazy scoring — each dimension measures something different |
| N/A on 3+ dimensions | Wrong domain extension activated, or avoiding low scores |
| Scores jump without actual changes | Narrative improvement, not real improvement |
| Improvements proposed as full rewrites | Disproportionate — improvements must be targeted |

---

## Second-Pass Techniques

Default: use **Expose hidden shortcuts** for most tasks. Add others based on
task type.

**Expose hidden shortcuts**
"What did I simplify, ignore, or assume?"
Use for: complex tasks where completeness is critical.

**Challenge the first idea**
"What alternatives did I consider and why did I reject them?"
Use for: architecture decisions, design choices, strategy recommendations.

**Flip perspective**
"Critique this as a sceptical senior engineer."
Use for: code reviews, proposals, anything going to stakeholders.

**3 variants**
"Give 3 different approaches."
Use for: creative or design decisions — naming, architecture, problem-solving.

**Confidence score**
"How confident am I, from 1 to 10?"
Use for: technical facts, data interpretation, accuracy-critical recommendations.

---

## Example

Task: "Add input validation to the signup form"

### Quality Gate — Pass 1

| Dimension | Score | Note |
|---|---|---|
| Correctness | 9.0 | All field types validated correctly |
| Completeness | 8.0 | Missing error messages for individual fields |
| Clarity | 9.5 | Clean, readable implementation |
| User Intent | 9.0 | Matches signup requirements |
| Code Quality | 8.5 | Validation logic duplicated in two places |
| Security | 7.5 | No rate limiting, no CSRF token |
| **Overall** | **8.6** | |

Below 9.0. Improvements identified:
- Security 7.5 → 9.0: add rate limiting and CSRF token validation
- Completeness 8.0 → 9.0: add per-field error messages
- Code Quality 8.5 → 9.0: extract validation into reusable helper

*[Implements improvements, re-scores at 9.2, delivers improved version]*
