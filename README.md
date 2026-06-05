# Agent Context Templates

Global instruction files for Claude Code and Codex.

These templates came from repeated agent work: missed assumptions, swollen
diffs, stale memory, skipped checks, and tool sprawl. They are built to keep an
agent close to the work.

Use them as starting points. Cut them hard. Keep only rules that survive contact
with your own repos.

## Files

- `CLAUDE.md`: global context for Claude Code.
- `AGENTS.md`: global context for Codex.

Each file keeps a firm line between:

- durable guidance for every session
- project guidance that belongs near the code
- enforcement that belongs in settings, hooks, tests, linters, sandboxing, or
  pre-commit checks

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

## Bias

The templates favor:

- small diffs
- explicit assumptions
- tests before success claims
- concrete handling of untrusted context
- fewer default tools
- repo-local detail

A short true rule beats a long impressive one.

## License

MIT.
