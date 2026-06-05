# Agent Context Templates

Hardened starting points for global Claude Code and Codex instructions.

These files are meant to be copied, edited, and made boringly specific to a
real workflow. The point is not to make an agent sound more confident. The
point is to make it slower to drift, cheaper to correct, and easier to verify.

## What Is Here

- `CLAUDE.md`: a global Claude Code context template.
- `AGENTS.md`: a global Codex context template.

Both files separate three concerns that are easy to blur:

- Durable guidance: what belongs in a global instruction file.
- Local/project guidance: what belongs in repo-level files.
- Enforcement: what belongs in settings, permissions, sandboxing, hooks, rules,
  tests, linters, and pre-commit checks instead of prose.

## How To Use

1. Read the file for the tool you use.
2. Replace bracketed placeholders and remove sections that do not match your
   workflow.
3. Keep global files compact. Put build commands, repo architecture, PR rules,
   and deployment details in the nearest project-level instruction file.
4. Do not paste secrets, private paths, employer/customer data, or personal
   memory into these files.
5. Verify the tool is actually loading the file before trusting it.

Typical targets:

```text
Claude Code: ~/.claude/CLAUDE.md
Codex:       ~/.codex/AGENTS.md
```

## Design Bias

These templates bias toward:

- small, traceable changes
- explicit assumptions
- tests or concrete checks before success claims
- clear handling of untrusted context
- fewer default tools and plugins
- repo-local instructions over global sprawl

They are intentionally not exhaustive. A short instruction that is true and
easy to obey beats a long instruction that sounds complete.

## License

MIT.
