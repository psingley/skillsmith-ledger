# Skillsmith Conversation Ledger

> Append-only log of all human-agent dialogue, decisions, and context transfers for the Skillsmith project.

## Purpose

This repository exists because AI agent sessions are ephemeral. Context windows overflow, sandboxes hibernate, and sessions expire. The Conversation Ledger preserves **full-fidelity records** of every significant interaction so that any future agent (Manus, Codex, Claude, or a human) can reconstruct the project's decision history without re-deriving it.

## What Goes Here

| Content Type | Description | Example |
|---|---|---|
| Session logs | Raw or summarized transcripts of human-agent dialogue | `sessions/2026-03-22-manus-setup.md` |
| Decision records | Architectural decisions with rationale and alternatives considered | `decisions/ADR-001-forge-artifact-split.md` |
| Context transfers | Compressed state documents for handing off between sessions | `transfers/2026-03-22-context-handoff.md` |
| Retrospectives | Post-session analysis of what worked and what did not | `retros/2026-03-22-retro.md` |

## What Does NOT Go Here

- Source code (that lives in `psingley/skillsmith`)
- Architecture specs (those live in `psingley/skillsmith/docs/`)
- Temporary scratch files or debugging output

## Structure

```
skillsmith-ledger/
├── README.md
├── sessions/           # Chronological session logs
│   └── YYYY-MM-DD-<agent>-<topic>.md
├── decisions/          # Architecture Decision Records (ADRs)
│   └── ADR-NNN-<slug>.md
├── transfers/          # Context transfer documents for session handoffs
│   └── YYYY-MM-DD-context-handoff.md
└── retros/             # Post-session retrospectives
    └── YYYY-MM-DD-retro.md
```

## Conventions

1. **Append-only.** Never edit a session log after it is committed. Corrections go in a new entry.
2. **Chronological naming.** All files start with `YYYY-MM-DD` for natural sorting.
3. **Agent attribution.** Session logs identify which agent(s) participated (Manus, Codex CLI, Claude Code, human).
4. **Decision rationale.** Every ADR must include the alternatives considered and why they were rejected.
5. **Linked commits.** When a decision leads to implementation, link to the relevant commit in `psingley/skillsmith`.

## Related Repositories

- [`psingley/skillsmith`](https://github.com/psingley/skillsmith) — The working implementation repository
