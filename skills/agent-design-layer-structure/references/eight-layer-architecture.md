# Eight-Layer Architecture

> Four layers on the whiteboard. Eight in production. Understanding the four gets you started. Understanding the eight is what keeps the system alive.

---

## The Simple Four

1. **Orchestration** — what runs when, in what order, with what dependencies
2. **Frameworks** — how agents interpret data and make judgments
3. **Skills** — the agents themselves, each with defined scope and contracts
4. **Metadata** — the system's memory, every decision tagged and traced

These are real. They're the right starting point. But they contain distinct functions that need separating — because they have different rules, different tempos, and different relationships to human control.

## Where the Four Become Eight

### Routing separates from Orchestration

Orchestration manages flow. Routing decides how the system should approach this specific piece of work — which mode, which frameworks to load, at what depth.

Routing is about judgment (how should we think about this?). Orchestration is about logistics (what runs next?). They need different defaults: routing defaults conservative on depth (when ambiguous, assume facts not analysis), orchestration defaults conservative on flow (retry, degrade, halt).

### Frameworks split into Data Reading Guides and Reasoning Frameworks

**Data reading guides** teach the agent how to interact with your systems. Query correctly. Distinguish empty from missing. Handle pagination. Check freshness. Never infer what you didn't pull. These come from knowing the system and change when the data architecture changes.

**Reasoning frameworks** teach the agent how to think about what it found. Decompose messy notes into distinct signals. Classify, assess confidence, interpret in context. These come from knowing the business and change when the business changes.

They change for different reasons at different rates. An agent can load one without the other. They're both "frameworks" but they do different jobs.

### Learning separates from Metadata

Metadata records what happened. Learning detects patterns in what happened and proposes changes. These are fundamentally different activities with different rules:

- A single observation never triggers a change
- Soft adjustments are automatic, weighted, decaying
- Permanent changes are human-gated with rollback
- Learning operates on cycles (per-event, weekly, monthly) with minimum thresholds

When learning is treated as "metadata plus some logic," the governance boundaries get blurry.

### Lifecycle separates from Metadata

Metadata tracks timestamps. Lifecycle acts on them — decaying what's stale, archiving what's expired, extending what's actively used.

Lifecycle runs on its own schedule, before everything else. By the time agents start work, the intelligence layer has been cleaned. Without it, stale intelligence accumulates — an agent reads a signal from three months ago and treats it as current.

### Context Assembly separates from Skills

The translator between structured agent outputs and downstream consumers. Not a skill (no domain opinion), not orchestration (not about flow). Reads structured outputs, strips noise, resolves contradictions, produces clean briefs.

## The Full Eight

1. **Routing** — classifies intent, sets analytical mode and framework depth
2. **Orchestration** — manages flow, sequencing, parallelism, state, the human boundary
3. **Data Reading Guides** — operational rules for query accuracy, field trust, freshness, pagination
4. **Reasoning Frameworks** — encoded expertise for interpretation, signal taxonomy, confidence, qualification
5. **Skills** — the agents, each with defined scope, contracts, and prohibitions
6. **Context Assembly** — translates structured outputs into clean briefs, resolves inter-agent conflicts
7. **Metadata and Learning** — records decisions for provenance; detects patterns and proposes changes with two-speed governance
8. **Lifecycle** — maintains intelligence freshness through decay, archival, and cleanup

## Implementation Varies

In a Claude skill architecture: skills are .md files, frameworks are reference files skills load, orchestration is a system skill, context assembly is a dedicated system skill, metadata lives in a database, learning is a dedicated agent, lifecycle is a cron-triggered system skill.

In LangChain or CrewAI: skills might be tool definitions, frameworks might be system prompts, orchestration might be a chain or graph, context assembly might be a preprocessing step.

In a custom runtime: orchestration is the workflow engine, skills are API calls, frameworks are loaded from a knowledge store.

The layers are the same. The implementation varies. What matters is that they're separated.
