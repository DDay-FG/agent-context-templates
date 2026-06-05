# Agent Context Templates

Global instruction files for Claude Code and Codex.

These templates came from repeated agent work: missed assumptions, swollen
diffs, stale memory, skipped checks, and tool sprawl. They are built to keep an
agent close to the work.

Use them as starting points. Cut them hard. Keep only rules that survive contact
with your own repos.

## Credits

This work is inspired by [Andrej Karpathy](https://github.com/karpathy)'s
public commentary on coding agents: the tendency to assume too much,
overcomplicate code, touch unrelated files, and skip clear success criteria.

It also builds on the path opened by
[multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills/tree/main),
an early community project that turned those observations into reusable Claude
Code guidance.

This repo generalizes that idea for both Claude Code and Codex, with more
emphasis on instruction-loading reality, privacy boundaries, enforcement
layers, and where global guidance should stop.

## The Problem

Agent failures usually look ordinary:

- the agent silently chooses the wrong interpretation
- the diff grows beyond the request
- verification becomes a closing sentence instead of an observed result
- global files collect project facts that belong near the code
- prose tries to enforce behavior that should live in settings, hooks, tests,
  permissions, or sandboxing

Better agent behavior starts with a smaller instruction file and sharper
boundaries.

## Files

- `CLAUDE.md`: global context for Claude Code.
- `AGENTS.md`: global context for Codex.

Each file keeps a firm line between:

- durable guidance for every session
- project guidance that belongs near the code
- enforcement that belongs in settings, hooks, tests, linters, sandboxing, or
  pre-commit checks

## What This Adds

| Area | Why it matters |
| --- | --- |
| Loading rules | Claude Code and Codex read different files in different orders. |
| Scope control | Global files should shape behavior, not replace repo docs. |
| Verification | Agents need concrete checks before success claims. |
| Privacy | Public templates should never carry private paths, employers, clients, or memory. |
| Enforcement | Prose is guidance. Hooks, settings, tests, and permissions do the blocking. |

## Install

Copy the file for your tool:

```text
Claude Code: ~/.claude/CLAUDE.md
Codex:       ~/.codex/AGENTS.md
```

Then edit it.

Remove anything that does not match your machine. Add only facts an agent should
carry into every session. Put build commands, repo architecture, deployment
rules, and PR rules in project-level files.

Do not paste secrets, private paths, employer data, customer data, or personal
memory into global instructions.

After installation, ask the tool to list the instruction files it loaded. Trust
the file only after the tool proves it is reading it.

## Adapt

Keep global files about durable operating style. Put project rules in the
nearest project-level file:

```markdown
## Project Context

- Runtime:
- Build:
- Test:
- Lint:
- Deploy:
- Security constraints:
- Repo-specific review rules:
```

If a rule only matters inside one repository, it does not belong in your global
file.

## Bias

The templates favor:

- small diffs
- explicit assumptions
- tests before success claims
- concrete handling of untrusted context
- fewer default tools
- repo-local detail

A short true rule beats a long impressive one.

## Working Signs

These templates are working when:

- the agent reads the right local file before editing
- assumptions are named early
- diffs stay close to the request
- tests or concrete checks appear before success claims
- private context stays out of public files
- tool-specific behavior differs where Claude Code and Codex actually differ

For trivial one-line work, use judgment. The goal is lower mistake cost on
non-trivial work, with no ceremony for one-liners.

## License

MIT.
