# How `docs/context.md` is produced

`docs/context.md` is a **generated** narrative primer for **Claude Projects** (claude.ai), where the reader has no filesystem or tool access. Don't edit it by hand: regenerate it with `/context-refresh primer` (skill at `~/.claude/skills/context-refresh/`).

## Sources of truth

| What | Where | Audience |
|---|---|---|
| Ecosystem relationships (all 7 projects) | `../CLAUDE.md` (`/Users/tiagosantos/git/cerberus/CLAUDE.md`) | agents, auto-loaded |
| Project context map | `docs/context/` (README, requirements, features, architecture, structure, decisions, glossary, gotchas) | coding agents with repo access |
| Agent behaviour rules | `AGENTS.md` | coding agents |
| Install/run | `README.md` | humans |
| **This primer** | `docs/context.md` — derived from the two rows above | reader with no file access |

If the primer and `docs/context/` disagree, `docs/context/` wins; fix it there first, then regenerate.

## When to regenerate

- Before refreshing the Claude Projects knowledge upload.
- After an architecture-level change (new subsystem, changed ecosystem relationship, replaced core component). Not for routine refactors.

## Primer template

First line after the title: `> Generated from docs/context/ on YYYY-MM-DD — do not edit directly; run /context-refresh primer.`

1. **Title + one-line tagline**
2. **What it is** — one paragraph (from `docs/context/README.md` TL;DR).
3. **What it does** — capabilities in plain language (from `features.md`).
4. **Purpose / why it exists** — problem solved in the Cerberus ecosystem.
5. **Ecosystem & relationships** — upstream/downstream projects, data-flow direction, read-only vs owned state (from `../CLAUDE.md` + `architecture.md`).
6. **Architecture** — stack, main modules and what each owns, end-to-end flow narrative (from `architecture.md`, `structure.md`).
7. **Entrypoints & CLI** — only if the project has commands (from `structure.md` generated block).
8. **Workflow walkthrough** — only for non-obvious multi-step lifecycles.
9. **Key concepts & terminology** (from `glossary.md`).
10. **Notable design decisions** with *why it matters* (from `decisions.md`, `requirements.md`).
11. **Current state / maturity** — for thin or early-stage projects; say plainly what exists vs aspirational.

## Rules

- Self-contained: no relative links, no "see file X" — the reader can't open files. Explain instead of indexing.
- Scale depth to the project: large projects (data, indicators, terminal, workbench) need concrete entrypoints, a walkthrough and real terminology; `cerberus_trader` stays short; archives/vaults (`delphi-archive`, `stock_research`) are shortest and say there is no runtime.
- Open source code only to fill narrative gaps the context map doesn't cover — and if you find such a gap, add it to `docs/context/` too.
- Final check: could someone who never saw this codebase explain what it does and how data/control flows through it, using only the primer?
