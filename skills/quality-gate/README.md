# quality-gate

A universal quality gate for Claude Code. Scores work against a rubric before
completion and iterates to 9.0+ before delivering. Works for code, documents,
plans, architecture decisions, and QA artefacts.

---

## Install

### Claude Code — personal (all your projects)

```bash
mkdir -p ~/.claude/skills/quality-gate && \
curl -fsSL https://raw.githubusercontent.com/input-output-hk/cbu-coe/main/skills/quality-gate/SKILL.md \
  -o ~/.claude/skills/quality-gate/SKILL.md
```

The skill becomes available in every project on your machine.

### Claude Code — repo-level (one project only)

```bash
mkdir -p .claude/skills/quality-gate && \
curl -fsSL https://raw.githubusercontent.com/input-output-hk/cbu-coe/main/skills/quality-gate/SKILL.md \
  -o .claude/skills/quality-gate/SKILL.md
```

Commit `.claude/skills/quality-gate/SKILL.md` so teammates get it automatically
when they clone the repo.

---

## Update

Re-run the same install command. It overwrites the local file with the latest
version from `main`.

To see what changed before updating, check the
[commit history](https://github.com/input-output-hk/cbu-coe/commits/main/skills/quality-gate/SKILL.md)
for this file.

---

## Stronger enforcement (recommended)

By default the skill is available but Claude may not apply it consistently.
For automatic enforcement — Claude runs the gate before declaring any task
complete — add this line to your `~/.claude/CLAUDE.md` (global) or your
project's `CLAUDE.md`:

```markdown
- **Quality gate** — invoke the `quality-gate` skill before declaring any task
  complete. Skip for questions, explanations, and simple lookups.
```

---

## Hook (advanced)

For a terminal reminder after every response, add this to
`.claude/settings.json`:

```json
{
  "hooks": {
    "Stop": [{
      "matcher": "",
      "hooks": [{
        "type": "command",
        "command": "echo '[quality-gate] Did you score this work before stopping?'"
      }]
    }]
  }
}
```

**Note:** this hook prints to the terminal — it does not inject a prompt into
Claude. The CLAUDE.md rule above is more effective for behavioural enforcement.
Use the hook as an additional visual reminder, not as a replacement.

---

## No Claude Code?

If you are using Claude via claude.ai or another interface without Claude Code,
paste this at the start of your prompt:

```
Before delivering your final answer, score your work on these dimensions
(1–10 each): Correctness, Completeness, Clarity, User Intent. If any score
is below 9, state what you would change to reach 9+ and implement those
changes before delivering. Show me the final scores.
```

No installation needed. Works in any Claude conversation.

---

## Why This Works

LLMs structurally satisfice: they produce the most statistically probable
(good-enough) output rather than the best possible output. Any technique that
forces a deliberate second pass — evaluation, reflection, self-critique —
consistently produces better results than the first draft.

This is not peer review. It is the same model with the same blind spots. It
will not catch hallucinations or replace domain expertise. It adds a few
seconds per task. The trade-off is worth it for anything non-trivial.

## What This Is Not

This skill is **forced iteration**, not independent quality assurance. The
same model evaluating its own output shares the same biases and blind spots.
It will not catch structural flaws, hallucinations, or domain-specific errors
that the model doesn't know it's making.

For those, you need domain-specific process checks (role-specific templates,
hooks that enforce structure during work, human review). This skill is one
layer in a multi-layer quality approach — the lightweight, zero-cost layer
that consistently improves first-draft output.

---

## Session Hygiene

**Start fresh when quality drops.**
If responses become weaker, repetitive, or Claude forgets earlier context, the
context window is saturating. Before starting over, ask:
"Summarise the current state — files changed, decisions made, open issues —
as a prompt I can paste into a new conversation."
Clean handoff, no progress lost. Do this before context reaches 70%. At 90%
Claude is already working with a compressed view.

**Never paste secrets.**
API keys, tokens, passwords, PII — use placeholders or env variable references.
Once sent, cannot be unsent. Ask Claude to write code that reads from
environment variables from the start, never hardcoded values.

---

## Evaluation Scenarios

Test these with and without the skill loaded to verify it works:

1. **"Write a function that parses CSV files with error handling"**
   Expected: skill triggers, scores below 9.0 on first pass, improves
   error handling and edge cases before delivering.

2. **"What is dependency injection?"**
   Expected: skill does NOT trigger (simple explanation).

3. **"Write a PRD for a notification service"**
   Expected: skill triggers, activates Documents domain extension,
   scores on Actionability and Stakeholder Alignment.

4. **"Add retry logic to the API client"**
   Expected: skill triggers, activates Code domain extension,
   scores on Security and Performance.

5. **"Fix the typo in line 42"**
   Expected: skill does NOT trigger (trivial edit).

---

## Credits

Built from a conversation in `#ai-collaboration-circles` (March 2026):

- **Dorin Solomon** — self-scoring technique, tips catalog, CoE resource vision
- **Ivan Irakoze** — 7-dimension rubric, first skill implementation ([claude-self-score](https://github.com/augmentedivan/claude-self-score))
- **Dominik Guzei** — simplified command format (`improve.md`)
- **Stefano Leone** — skills + memory + hooks layered architecture
- **Konstantinos Kogkalidis, Piotr Krogulski** — critical feedback on self-review limitations
- **Sean Gillespie** — validation on test case generation

---

## Contributing

PRs welcome. Open a pull request against
[input-output-hk/cbu-coe](https://github.com/input-output-hk/cbu-coe).
CoE (@dorin100) reviews and merges.

When proposing changes to the rubric or scoring rules, include at least one
concrete example showing why the change improves output quality.

---

## License

© Input Output Global, Inc. Internal use only. Not for external distribution.
