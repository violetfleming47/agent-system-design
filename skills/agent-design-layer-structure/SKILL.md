---
name: agent-design-layer-structure
description: Identify the eight architectural layers an agent system needs (routing, orchestration, data-reading guides, reasoning frameworks, skills, context assembly, metadata and learning, lifecycle). Use when auditing or planning the overall structure of an agent system.
---

# Layer Structure

> Determine where routing, orchestration, context assembly, and lifecycle sit — and keep them separate from domain agents.

---

## What This Skill Does

Every agentic system that works in production has layers. Most people building them don't separate the layers cleanly, and that's where the problems start — not immediately, but the moment you try to change something.

A skill that contains orchestration logic can't be recomposed into a different flow. A framework embedded inside a skill can't be shared across agents or updated independently. Metadata mixed into output can't be queried for learning signals. Context assembly buried inside a generation step creates a failure surface nobody can debug.

These sound like software engineering concerns, and they are. But they're also the reason systems that work beautifully in a demo fall apart in production. In a demo, everything is together and it works. In production, you need to change the orchestration without touching the skills, update a framework without rewriting every agent that uses it, add a new capability without restructuring the whole pipeline. That's only possible when the layers are separated.

This skill helps you identify what layers your system needs and where to draw the boundaries between them.

---

## The Whiteboard Version: Four Layers

When someone asks you to explain your system's architecture on a whiteboard, four layers is the right level:

**Orchestration** — what runs when, in what order, with what dependencies. The traffic controller.

**Frameworks** — how agents interpret data and make judgments. The encoded expertise.

**Skills** — the agents themselves, each with defined scope and contracts. Where the judgments live.

**Metadata** — the system's memory. Every decision tagged, traced, and linked.

These are real. They're the right starting point. But if you build a production system against them, you'll discover that several contain distinct functions that need to be separated — because they have different rules, different tempos, different relationships to human control, and different reasons to change.

---

## Where the Four Become Eight

### Routing separates from Orchestration

Orchestration manages flow — what runs when, in what order. But before orchestration begins, something needs to decide *how the system should approach this specific piece of work*. Is this a standard pipeline run? Is it pre-written content that just needs scoring and validation? Is it a newsletter edition that skips half the pipeline?

That classification is routing, and it's a different function from orchestration. Routing is about judgment — "how should we think about this?" Orchestration is about logistics — "what runs next?"

They also need different defaults. Orchestration defaults should be conservative about flow: retry, degrade gracefully, halt if necessary. Routing defaults should be conservative about depth: when intent is ambiguous, assume the user wants facts, not analysis. Never default to the most analytical mode. These opposing default logics confirm they're separate functions.

In practice, a routing agent reads the incoming input and classifies it along defined dimensions — origin, type, priority, complexity. The classification determines which agents run, which frameworks get loaded, and at what depth. Then the orchestrator takes over and manages the actual flow.

### Frameworks split into Data Reading Guides and Reasoning Frameworks

Inside the frameworks layer, there are two distinct types doing different work. Both teach agents how to interpret what they encounter. But they come from different sources of knowledge, they're written by different people in practice, and they change for different reasons.

**Data reading guides** teach the agent how to interact with your actual systems. How to query correctly. What to trust. What to cross-reference. What the data architecture looks like underneath. Never infer what you didn't pull. Always distinguish empty from missing. Never trust a single data layer. Handle pagination. Respect filter limits. These are operational rules. They come from knowing the system — its quirks, its limitations, its field-level reliability.

**Reasoning frameworks** teach the agent how to think about what it found. How to decompose a messy note into distinct signals. How to classify each signal against a defined taxonomy. How to assess confidence. How to attribute a signal to the right person. How to score qualification. These come from knowing the business — accumulated expertise about what matters, what signals carry weight, how experienced operators think about data.

The split matters because they change for different reasons at different rates. Your query pagination rules don't change when your sales methodology evolves. Your signal taxonomy doesn't change when you add a new API endpoint. An agent can load a data reading guide without a reasoning framework (when it just needs to pull accurate data) and a reasoning framework without a data reading guide (when it's interpreting data that's already been pulled). They're both frameworks. They do different jobs.

### Learning separates from Metadata

Metadata records what happened — every decision tagged, every output linked to its inputs, every human correction traced. That's a record. It's passive. It doesn't change the system's behaviour.

Learning detects patterns in what happened and proposes changes based on those patterns. That's fundamentally different. Learning changes behaviour. And the distinction between automatic changes (soft adjustments) and human-gated changes (permanent structural updates) is the most important governance boundary in the entire architecture.

The learning system has rules that don't apply to metadata: a single observation never triggers a system change. Several confirmed instances produce a soft runtime adjustment — automatic, weighted, decaying. Many instances over weeks produce a proposal for permanent change — human-gated, explicit, with preserved rollback. Adjustments that aren't reinforced lose confidence over time.

It also has its own tempo. Metadata is written continuously, as work flows through the system. Learning operates on cycles — per-event observation, weekly pattern analysis, monthly structural review. These cycles have minimum thresholds, confidence requirements, and decay schedules that don't exist in the metadata layer.

When learning is treated as "metadata plus some logic," the governance boundaries get blurry. Observations start triggering immediate changes. Pattern detection runs without minimum thresholds. The system becomes volatile instead of stable. Separate the layers and the boundaries stay sharp.

### Lifecycle separates from Metadata

Metadata tracks when things were created and last updated. Lifecycle acts on that information — decaying what's stale, archiving what's expired, extending what's actively in use.

This is a distinct function that runs on its own schedule, before anything else in the system starts its day. By the time agents begin their work, the intelligence layer has been cleaned. Stale signals have been aged or archived. Expired suggestions have been removed. Learned adjustments that haven't been reinforced have had their confidence reduced. Campaign deadlines have been checked.

Without a dedicated lifecycle layer, stale intelligence accumulates invisibly. An agent reads a market signal from three months ago and treats it as current. A learned adjustment from a context that no longer applies quietly influences output. A suggestion that expired two weeks ago sits in the queue looking active. These aren't dramatic failures. They're slow degradation — the system getting slightly less trustworthy every day without anyone noticing.

Lifecycle management is the 6AM janitorial run that nobody sees. It's the reason the system is still trustworthy in month twelve, not just month one.

### Context Assembly separates from Skills

Covered in depth in the Composition skill, but worth noting here as a layer: context assembly is a dedicated translation function that sits between structured agent outputs and downstream consumers. Not a skill (no domain opinion). Not orchestration (not about flow). A translator.

---

## The Full Eight

1. **Routing** — classifies intent, sets analytical mode and framework depth
2. **Orchestration** — manages flow, sequencing, parallelism, state, the human boundary
3. **Data Reading Guides** — operational rules for query accuracy, field trust, freshness, pagination
4. **Reasoning Frameworks** — encoded expertise for interpretation, signal taxonomy, confidence, qualification
5. **Skills** — the agents, each with defined scope, contracts, and prohibitions
6. **Context Assembly** — translates structured outputs into clean briefs, resolves inter-agent conflicts
7. **Metadata and Learning** — records decisions for provenance; detects patterns and proposes changes with two-speed governance
8. **Lifecycle** — maintains intelligence freshness through decay, archival, and cleanup

You might reasonably argue that metadata and learning should be fully separate, making nine. In practice they're deeply coupled — learning reads metadata, and the metadata schema is designed around what learning needs to detect. But the governance boundary between them (metadata records passively, learning changes behaviour actively) should be explicit even if they share a layer.

---

## System Skills vs Domain Skills

One more distinction that determines whether your system stays clean as it grows.

**Domain skills** make judgments about the actual work. They score, shape, curate, generate, validate, observe, learn. They have frameworks, they load data relevant to their lens, they produce assessments with confidence. They're where the design effort goes.

**System skills** handle infrastructure. Routing, orchestration, context assembly, lifecycle management, rendering. They have no domain opinion and no learning loop. They coordinate, translate, clean up, and enforce process. They should never make decisions about content, quality, or strategy — only about flow, format, and timing.

When a system skill absorbs domain logic, the orchestrator starts making content decisions and you can't change the content logic without changing the orchestration. When a domain skill absorbs infrastructure, the generation agent starts parsing structured data and you can't change the data format without rewriting the generation prompt.

Each absorption creates an entanglement. Every entanglement makes the system harder to change. Separation is what makes evolution surgical instead of risky.

---

## How to Use This

Describe your system architecture — or the system you're planning to build. I'll help you:

1. **Identify which layers you have and which are missing.** Most teams have skills and some orchestration. Most are missing routing, context assembly, lifecycle, or a clean separation between data reading guides and reasoning frameworks.

2. **Find where layers are collapsed.** An orchestrator making content decisions. A skill containing its own routing logic. Context assembly buried inside generation. Framework loading rules embedded in orchestration.

3. **Design the separation.** Each layer independently changeable. Change the flow? Update the orchestrator. Refine how agents query the CRM? Update the data reading guide. Refine how they interpret findings? Update the reasoning framework. Add a new capability? Add a new skill. Everything else stays the same.

4. **Determine what's infrastructure vs domain.** System skills coordinate. Domain skills judge. Keep them apart.

---

## How You Implement This Depends on What You're Building On

In a Claude skill architecture: skills are .md files, frameworks are reference files skills load, orchestration and routing are system skills, context assembly is a dedicated system skill, metadata lives in a database, learning is a dedicated agent, lifecycle is a cron-triggered system skill.

In LangChain or CrewAI: skills might be tool definitions or agent configurations, frameworks might be system prompts or retrieval sources, orchestration might be a chain or graph definition, context assembly might be a preprocessing step.

In a custom runtime with workflow engines: orchestration is the workflow engine, skills are API calls, frameworks are loaded from a knowledge store, context assembly is a dedicated step.

The layers are the same. The implementation varies. What matters is that they're separated — because separation is what makes the system evolvable.

---

## References

This skill loads:
- `references/eight-layer-architecture.md` — the full layer model with split rationale
- `references/system-vs-domain-skills.md` — how to distinguish infrastructure from domain judgment

---

## You Will Need Next

With layers identified and separated, move to **Human Placement** to design where humans sit in the loop and what governance boundaries keep the system safe as it earns trust.
