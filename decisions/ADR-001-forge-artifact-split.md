# ADR-001: The Forge vs. Artifact Split

**Date:** 2026-03-19
**Status:** Accepted
**Agents:** GPT 5.4 xhigh (Codex CLI), Human (psingley)

## Context

Skillsmith needs to be both a tool that creates skills and a skill itself. The initial designs conflated the runtime artifact (what agents load) with the development tooling (what builds, diagnoses, and optimizes skills). This created confusion about what ships to end users versus what stays local.

## Decision

Separate the system into two distinct concerns:

**The Artifact** is the published skill bundle. It is immutable, standards-compliant, and has zero hidden dependencies. Any agent can load it. It consists of `SKILL.md`, optional `references/`, `scripts/`, and `templates/` directories, and a `skillsmith.yaml` manifest.

**The Forge** is the local CLI (`skillsmith`). It owns the Doctor (health diagnostics), the Optimizer (GEPA-powered auto-research), the Gauntlet (formal promotion gates), the State Layer (SQLite for XP, telemetry, lineage), and the Factory (skill generation from templates). The Forge lives in the hidden `.skillsmith/` directory within each skill folder.

## Alternatives Considered

| Alternative | Why Rejected |
|---|---|
| Single monolithic skill directory | Agents would load forge internals into context, wasting tokens and confusing the agent |
| Global `~/.skillsmith/` installation | Violates the self-contained constraint; skills would not be portable |
| Forge as a separate npm package only | Loses the self-hosting property; Skillsmith could not be its own skill |

## Consequences

The `.skillsmith/` directory must be invisible to standard agent loaders. Progressive disclosure rules in `SKILL.md` control when agents access the hidden layers. This adds complexity to the directory structure but preserves both portability and power.

## Linked Commits

- `psingley/skillsmith@bb10d14` — Initial architecture and durable memory files
