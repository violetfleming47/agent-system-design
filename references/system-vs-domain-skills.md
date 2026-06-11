# System Skills vs Domain Skills

> Infrastructure has no domain opinion. Domain agents have no infrastructure concerns. Keep them separate.

---

## The Distinction

**Domain skills** make judgments about the actual work. They score, shape, curate, generate, validate, observe, learn. They have frameworks, they load data relevant to their lens, they produce assessments with confidence. They're where the design effort goes.

**System skills** handle infrastructure. Routing, orchestration, context assembly, lifecycle management, rendering. They have no domain opinion and no learning loop. They coordinate, translate, clean up, and enforce process.

## Why It Matters

When a system skill absorbs domain logic:
- The orchestrator starts making content decisions (it should only manage flow)
- The router starts scoring quality (it should only classify intent)
- The lifecycle agent starts interpreting signals (it should only check timestamps)

When a domain skill absorbs infrastructure:
- The generation agent parses structured data (it should only read a clean brief)
- The scoring agent manages its own retry logic (orchestration's job)
- The learning agent triggers its own schedule (the cron system's job)

Each absorption creates an entanglement. Change the domain logic and you break the infrastructure. Change the infrastructure and you break the domain judgment.

## Common System Skills

**Router** — the front door. Classifies input along defined dimensions (origin, type, priority). Creates records. Makes no quality judgments.

**Orchestrator** — the traffic controller. Manages sequencing, parallelism, dependencies, timeouts, revision loops, the human boundary. Reasons about process, never about content.

**Context Assembly / Prompt Assembler** — the translator. Reads structured outputs from upstream agents, strips system noise, resolves conflicts with predefined rules, produces clean briefs. Has no domain opinion.

**Lifecycle Manager** — the janitor. Runs before everything else. Expires stale data, decays confidence on aging intelligence, cleans up orphaned records. Applies timestamp-based rules, never interprets content.

**Visual Producer / Renderer** — converts structured content into formatted output. Applies design system rules mechanically.

**Calendar / Queue** — surfaces work items for human decision. Provides context (cadence, coverage, gaps) but doesn't make the decision.

## Common Domain Skills

**Scorers / Classifiers** — evaluate input against frameworks. Produce assessments with confidence.

**Shapers / Formatters** — decide form, structure, and channel based on domain-specific reasoning.

**Curators / Selectors** — choose evidence, contacts, or content based on relevance, quality, and freshness.

**Generators / Writers** — produce output from assembled briefs. Load voice and style frameworks.

**Validators** — assess quality against defined criteria. Route to human review, auto-approve, or revision.

**Learners / Observers** — watch human corrections, detect patterns, propose framework changes.

**Monitors** — detect repetition, drift, or degradation. Advisory only — they report, never block.

**Reporters** — synthesise system state into human-readable intelligence.

## Agent Categories

Domain skills can be further categorised by their relationship to learning:

**Autonomous Learners** — have their own scratchpad, run self-analysis, share learnings with the system. Their framework changes are human-gated, but they accumulate and share runtime intelligence automatically.

**Informed Executors** — read shared intelligence from autonomous learners. Improve through human skill edits and richer shared data, but don't run their own learning cycles.

**System Skills** — no learning loop. Infrastructure only. When they need to change, a human changes them.

This categorisation determines what each agent can write to and what it reads from. Autonomous learners write to shared intelligence stores. Informed executors read from them. System skills touch neither.
