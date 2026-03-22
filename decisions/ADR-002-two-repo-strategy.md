# ADR-002: Two-Repository Strategy

**Date:** 2026-03-22
**Status:** Accepted
**Agents:** Manus, Human (psingley)

## Context

AI agent sessions are ephemeral. Context windows overflow, sandboxes hibernate, and sessions expire. The Skillsmith project involves multiple agents (Manus, Codex CLI, Claude Code CLI) collaborating across sessions that may not share state. A single repository conflates implementation artifacts with the decision history needed to reconstruct context.

## Decision

Maintain two repositories:

**`psingley/skillsmith`** is the working implementation repository. It contains source code, architecture docs, durable memory files (AGENTS.md, Plan.md, Prompt.md, Implement.md), and the built skills. This is where agents write code and push features.

**`psingley/skillsmith-ledger`** is the append-only conversation ledger. It contains session logs, architecture decision records, context transfer documents, and retrospectives. This is where agents and humans record why decisions were made, what was tried, and what the current state is.

## Alternatives Considered

| Alternative | Why Rejected |
|---|---|
| Single repo with a `ledger/` directory | Session logs would pollute the working tree and bloat clones for agents that only need code |
| No ledger at all, rely on AGENTS.md | AGENTS.md captures current state but not decision history; context transfers between sessions lose fidelity |
| External wiki or Notion | Not accessible to CLI-based agents; breaks the Git-native workflow |

## Consequences

Every significant session should produce a ledger entry. Context transfers between Manus sessions should reference specific ledger entries rather than trying to compress all history into a single handoff document. The ledger is public so any agent can clone and read it without special access.
