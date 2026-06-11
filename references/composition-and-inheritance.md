# Composition and Inheritance

> One agent makes the call. Everyone else builds on it. The judgment is made once and carried forward.

---

## The Inheritance Principle

Every agent in a well-composed pipeline receives the previous agent's distilled decisions — not raw framework data. The scoring output travels downstream. The shaping agent reads it. The curation agent reads it. The generation agent reads it. None of them re-query the audience frameworks. None of them re-score the audience. They inherit the decision and build on it.

This means the upstream agent has to be right, or at least transparent about its confidence. Every confidence score is a percentage. If nothing scores above 40%, the agent says so. It doesn't force content to fit an audience. That honest uncertainty travels downstream. Every subsequent agent sees it and adjusts.

## What Re-Interpretation Looks Like

The alternative: every skill running its own audience analysis. Five agents, five independent assessments, five chances for the targeting to shift slightly between steps.

By the time the generation agent receives its brief, the audience has been reinterpreted at every stage. Nobody diverged dramatically. But nobody converged either. The output addresses a slightly different audience at every level of its construction. It reads fine on the surface and feels off underneath.

This is invisible drift. Not a dramatic failure — a gradual loss of precision across the pipeline.

## What Travels Between Agents

Each agent produces a structured decision — the minimum downstream agents need to build on it:

- **Fields with defined meaning.** Not raw data, not the full reasoning trace. A scoring output includes primary ICP (with confidence), selected beliefs, pillar alignment, and framing direction. That's what travels.
- **Confidence that propagates.** Low confidence upstream must be visible downstream. A generation agent writing with full conviction on a brief the scorer was 35% sure about is polished output built on sand.
- **Gap flags that persist.** Thin evidence, low relevance, missing data — these flags travel so downstream agents can work around them rather than writing with false confidence.
- **Decisions, not frameworks.** The downstream agent gets the result, not the tools used to reach it. Loading the framework downstream would cause re-evaluation.

## What Gets Stripped

Between agents, strip:
- Raw framework data (the downstream agent would re-apply it)
- Internal reasoning traces (the downstream agent would factor them into its own judgment)
- Data outside the downstream agent's scope (it would use it)
- System noise — database IDs, taxonomy codes, internal labels

## Parallel Composition

Some judgments can run in parallel because they don't depend on each other's decisions. Format selection, evidence curation, and repetition monitoring can all follow scoring simultaneously — each reads the scoring output independently.

When parallel agents run, track completion by field presence, not status. A single status field can't represent three concurrent states. All three must complete before the pipeline advances.

## Sequential Composition

Where decisions depend on upstream judgments, enforce the dependency. The generation agent cannot start until scoring, shaping, evidence selection, and the prompt assembly step have all completed. The orchestrator manages this — it tracks what's done, what's pending, and what's blocked.

Revision loops need special handling. The orchestrator counts revisions and enforces a hard cap — because models hate stopping and, left unchecked, a revision loop runs indefinitely.
