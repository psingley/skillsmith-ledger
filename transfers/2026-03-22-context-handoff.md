# Context Transfer: 2026-03-22

**From:** Manus session (context overflow recovery)
**To:** Any future agent session
**Purpose:** Full state reconstruction after context limit exceeded

## Current State Summary

The Skillsmith project has completed its architecture phase and is ready to begin implementation. All design decisions are documented, both worker CLI harnesses (Codex CLI with GPT 5.4, Claude Code CLI with Opus 4.6) are authenticated and tested, and the GitHub repositories are set up.

## Repositories

| Repository | URL | Purpose |
|---|---|---|
| `psingley/skillsmith` | https://github.com/psingley/skillsmith | Working implementation |
| `psingley/skillsmith-ledger` | https://github.com/psingley/skillsmith-ledger | Conversation and decision log |

## Key Files to Read (in order)

1. `psingley/skillsmith/AGENTS.md` — Project context and how to work on the repo
2. `psingley/skillsmith/Plan.md` — Current milestone and task list
3. `psingley/skillsmith/Implement.md` — Execution rules for agents
4. `psingley/skillsmith/Prompt.md` — Frozen project specification
5. `psingley/skillsmith-ledger/sessions/2026-03-22-manus-full-history.md` — Complete session history

## Current Milestone

**Milestone 1: The Forge Skeleton** — Build the basic CLI structure with `create` and `doctor` commands.

No tasks from Milestone 1 have been started yet. The TypeScript project has not been initialized.

## Technology Decisions Locked In

| Decision | Choice | Rationale |
|---|---|---|
| Language | TypeScript (Node.js) | Best ecosystem for CLI tools, agent-friendly |
| CLI framework | Commander.js | Lightweight, well-documented |
| State layer | SQLite via better-sqlite3 | Zero external deps, Dolt-compatible schema |
| Schema validation | Zod | Runtime YAML validation |
| Testing | Vitest | Fast, TypeScript-native |
| Package manager | pnpm | Strict dependency resolution |
| Optimization engine | GEPA/DSPy (Milestone 5) | Deferred, stub for now |

## Worker Agent Capabilities

| Agent | Model | Auth Method | Best For |
|---|---|---|---|
| Codex CLI | GPT 5.4 xhigh | PKCE OAuth | Deep reasoning, architecture, complex refactors |
| Claude Code CLI | Opus 4.6 | Anthropic Max subscription | Long-running implementation, file-heavy work |
| Manus | Internal | Sandbox | Orchestration, research, browser automation |

## Recursive Workflow Pattern

Manus acts as the orchestrator. It dispatches work to Codex CLI or Claude Code CLI for implementation. Those workers follow the durable memory pattern (read AGENTS.md first, then Plan.md, then pick up tasks). Skillsmith, once built, becomes a skill generator that the workers can also use.

## Unresolved Questions

1. **Model routing:** When should Manus use Codex CLI vs. Claude Code CLI vs. doing the work itself?
2. **Worker dispatch format:** How exactly does Manus invoke worker CLIs with structured task descriptions?
3. **Skill-level init patterns:** Should each skill directory have its own AGENTS.md equivalent for worker agents?
