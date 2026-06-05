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

## Have Your Agents Install This

Paste this into Claude Code or Codex:

```text
Install the global agent context templates from:
https://github.com/DDay-FG/agent-context-templates

Goal:
Safely adopt the right template for this tool without dropping critical local
context from the existing global instruction file.

Rules:
- Do not overwrite the current global file until you have staged the new file,
  inspected the old file, preserved critical local context, and shown a diff.
- Do not copy secrets, tokens, private employer/client data, or stale project
  facts into any shared repo file.
- Local private paths may belong in the user's private global file. They do not
  belong in a public template.
- Keep Claude Code and Codex files distinct. Do not blindly convert one format
  into the other.

1. Detect the tool and target file.

- Claude Code target:
  ~/.claude/CLAUDE.md
- Codex target:
  ~/.codex/AGENTS.md

For Codex, also inspect ~/.codex/AGENTS.override.md and ~/.codex/config.toml if
they exist. If this machine has a CODEX.md file or a configured fallback name,
inspect it too and explain whether Codex actually loads it. Do not assume
CODEX.md is the governing file unless local config proves it.

2. Download templates into a staging directory.

Run:

mkdir -p "${TMPDIR:-/tmp}/agent-context-templates-install"
cd "${TMPDIR:-/tmp}/agent-context-templates-install"
curl -fsSL https://raw.githubusercontent.com/DDay-FG/agent-context-templates/main/CLAUDE.md -o CLAUDE.md
curl -fsSL https://raw.githubusercontent.com/DDay-FG/agent-context-templates/main/AGENTS.md -o AGENTS.md
wc -l CLAUDE.md AGENTS.md

Read the staged file for this tool before editing it.

3. Inspect the existing global context before changing anything.

Read the target file if it exists. Also inspect nearby files that may affect
loading:

- Claude Code: ~/.claude/CLAUDE.md, ~/.claude/CLAUDE.local.md, relevant
  .claude/rules files, and managed/user settings if available.
- Codex: ~/.codex/AGENTS.md, ~/.codex/AGENTS.override.md, ~/.codex/config.toml,
  and any configured fallback instruction filename.

Summarize what currently matters. Preserve only current, useful guidance.

4. Merge critical local context into the staged template.

Keep or add durable local facts such as:

- operating system, shell, package manager, and common runtimes
- active project roots and path-drift rules
- local reporting, memory, skill, hook, or review workflows
- security rules, privacy boundaries, and approval expectations
- default verification commands that apply across most projects
- tool-specific loading notes that are true on this machine

Remove placeholder text and generic sections that do not fit. If a rule belongs
to one repository, move it to that repository's local CLAUDE.md or AGENTS.md
instead of putting it in the global file.

5. Build a candidate file and show the user the diff.

Create a candidate next to the target, for example:

- ~/.claude/CLAUDE.md.candidate
- ~/.codex/AGENTS.md.candidate

Compare old versus candidate. Explain:

- what was preserved
- what was removed
- what was added from the template
- any uncertain item that needs user approval

6. Install only after review.

Set the install variables for the current tool:

Claude Code:

TARGET="$HOME/.claude/CLAUDE.md"
CANDIDATE="$HOME/.claude/CLAUDE.md.candidate"

Codex:

TARGET="${CODEX_HOME:-$HOME/.codex}/AGENTS.md"
CANDIDATE="${TARGET}.candidate"

After the user approves, create a timestamped backup and replace the target:

ts="$(date +%Y%m%d-%H%M%S)"
mkdir -p "$(dirname "$TARGET")"
[ -f "$TARGET" ] && cp "$TARGET" "$TARGET.backup.$ts"
cp "$CANDIDATE" "$TARGET"

If the user asked for a fully autonomous install, use the same backup flow and
report the backup path.

7. Verify loading.

- Claude Code: start a fresh session or clear/reload context, then use the
  available context command to confirm the loaded CLAUDE.md files.
- Codex: start a fresh session, then use the available status/log command to
  confirm the loaded AGENTS.md chain and config.

Report the final target path, backup path, key preserved local sections, and any
follow-up needed. If you cannot prove the tool loaded the file, say so clearly.
```

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
