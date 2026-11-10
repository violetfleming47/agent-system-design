---
name: agent-design-composition
description: Design how decisions flow between agents through inheritance so downstream agents do not re-interpret upstream calls. Use when chaining multiple agents into a pipeline and passing context and confidence forward.
---

# Composition

> Design how agents inherit decisions and what flows between them — so no judgment gets re-interpreted downstream.

---

## What This Skill Does

You've mapped the judgments, identified the lenses, and defined the scope for each agent. Now comes the question that determines whether the system actually coheres or just runs: how do decisions flow between agents?

This sounds like a plumbing problem — which agent's output feeds into which agent's input. And the plumbing matters. But the real design question is deeper: when a downstream agent receives an upstream decision, does it inherit it and build on it? Or does it subtly re-interpret it?

The difference between these two is the difference between a system that holds and one that slowly, invisibly drifts.

---

## The Re-Interpretation Problem

Here's what happens when you don't design composition deliberately.

The scoring agent decides: this content is for the Gatekeeper persona, confidence 78%, with a regulatory compliance angle. That decision gets written to a record and passed downstream.

The shaping agent reads it. "Gatekeeper, regulatory compliance. Okay, but the format data I'm looking at suggests Gatekeeper content performs best as long-form analysis. Let me factor that in..." The shaping agent has subtly reinterpreted the audience decision. It didn't override it — it just nudged it toward the format it thinks works best. Now the audience isn't quite "Gatekeeper" — it's "Gatekeeper-as-long-form-reader," which is a slightly different persona.

The curation agent reads the shaping agent's output. "Long-form analysis for Gatekeeper... I should select evidence that supports deep regulatory analysis." The curation agent has now interpreted the audience through the lens of the format, selecting evidence for a piece that's already drifting from the original targeting.

The generation agent reads everything and produces a draft. By now, the audience has been reinterpreted at every stage. The scoring agent said "Gatekeeper, regulatory compliance." The generation agent is writing for "Gatekeeper who reads long-form regulatory deep-dives and cares about detailed evidence." That's not wrong, exactly. It's just not what the scoring agent decided. Nobody diverged dramatically. Nobody converged either. The output addresses a slightly different audience at every level of its construction.

It reads fine on the surface. It feels off underneath. And nobody can point to where it went wrong, because at each step, the reinterpretation was reasonable. This is invisible drift. It's the failure mode that compounds across thirty pieces into a system with no coherent identity.

---

## Inheritance, Not Repetition

The fix is compositional inheritance. One agent makes the call. Everyone downstream inherits it. They don't re-query the frameworks. They don't apply their own interpretation. They accept the decision and add their own judgment on top of it.

The scoring agent decides the audience. The shaping agent accepts that audience decision and makes its own judgment: what format works for this audience and this content? The curation agent accepts both the audience and format decisions and makes its own judgment: what evidence supports this argument for this audience in this format? Each agent adds its layer without revisiting the layers below.

This requires something specific: the upstream agent's output must be clear enough that the downstream agent doesn't need to interpret it. The scoring output isn't "this seems like a Gatekeeper piece" — it's a structured decision with primary ICP (Gatekeeper, 78%), secondary ICP (if any), selected beliefs with expression strength, pillar alignment, and framing direction. The downstream agent doesn't need to figure out what the scoring agent meant. The meaning is explicit.

---

## What Travels Between Agents

This is where design precision matters. Each agent produces a distilled decision — the minimum downstream agents need to build on it. Not raw data. Not the full reasoning trace. Not the frameworks that produced the decision. The decision itself.

### Fields with defined meaning

Every field in the output should mean something specific to the agent that reads it next. Not just a value — a meaning. "Primary ICP: Gatekeeper, confidence 78%" tells the downstream agent who the content is for and how sure the system is. "Framing direction: regulatory compliance angle, moderate belief expression" tells the downstream agent what rhetorical approach to take. Each field is a clean input for the next judgment.

### Confidence that propagates

This is often missed, and it's critical. When the scoring agent is only 35% confident about the audience, that uncertainty must be visible downstream. If the generation agent writes with full conviction on a brief that the scorer was uncertain about, you get polished output built on sand.

Confidence should always be a percentage, never binary. Binary confidence (high/medium/low) hides the distribution — there's a meaningful difference between 42% and 78%, but both might be "medium" in a three-tier system. And when nothing scores above a meaningful threshold, the agent says so rather than forcing a fit. That honest uncertainty propagates: the format agent might recommend a broader, less persona-specific format. The evidence agent might select more general evidence. The generation agent might adopt a less targeted tone.

A system that propagates uncertainty honestly produces output that's calibrated to what it actually knows. A system that hides uncertainty produces output that's confidently wrong.

### Gap flags that persist

When an upstream agent identifies a gap — thin evidence, missing data, low confidence — that flag must travel downstream. The evidence agent flagging thin evidence means the generation agent can work around the gap rather than writing with false confidence. The scoring agent flagging low ICP relevance means the format agent can adjust its approach.

Gap flags are not failure states. They're information. An agent that says "I couldn't find strong evidence for this angle, here's what I have" is more useful than one that pads with irrelevant data to avoid looking incomplete.

### What gets stripped

Between agents, strip everything that would cause re-analysis:

- Raw framework data (the downstream agent would re-apply it and potentially reach a different conclusion)
- Internal reasoning traces (the downstream agent would factor them into its own judgment, second-guessing the upstream decision)
- Data outside the downstream agent's scope (it would use it)
- System noise — database IDs, taxonomy codes, confidence scores from intermediate steps that aren't relevant downstream

The downstream agent gets the decision, not the deliberation. Clean inputs produce clean judgments.

---

## The Context Assembly Layer

This is where composition meets implementation, and it's a piece of architecture most people don't know they need until they're debugging mysterious output quality problems.

Multiple agents produce structured outputs: classification results, format recommendations, evidence packages, repetition warnings. These outputs contain system noise — internal IDs, selection reasoning, anti-repetition scores, confidence percentages that are meaningful to the producing agent but irrelevant to the consumer. They may contain contradictions — one agent recommends a hook type that another agent flagged as overused. They reference frameworks and data structures that the downstream consumer shouldn't need to know about.

Context assembly sits between these structured outputs and the downstream agent. It reads everything, strips the system noise, resolves contradictions using explicit rules, checks live data for current context, and produces a clean brief the downstream agent can act on without parsing structured data or making judgment calls about conflicting signals.

This is not a skill — it has no domain opinion. It's not orchestration — the orchestrator manages when this step runs, but the assembly logic is about what reaches the agent's context window and in what form. It's a translator. And when it's missing, one of two things happens: either the downstream agent receives raw structured data and has to parse and interpret it (introducing a new failure surface), or the orchestrator starts making content-level decisions about what to include (violating its traffic-control purity).

In a content pipeline, this manifests as a Prompt Assembler — a dedicated step that reads all upstream structured outputs and produces a prose brief for the generation agent. The brief reads like a creative director's handoff to a writer: here's the audience, here's the argument, here's the evidence, here's the market context, here's the format, here's the channel, here are the per-piece voice notes. No database IDs. No JSONB. No confidence percentages from intermediate steps. The generation agent reads a brief and writes. It never sees infrastructure.

Permanent voice rules live in the generation agent itself. The context assembly layer delivers only what changes per piece. This separation means voice consistency comes from the agent's own definition, not from the brief — so the brief can change completely between pieces without the voice drifting.

---

## Parallel vs Sequential

Some judgments can run in parallel because they don't depend on each other's decisions. In a content pipeline, format selection, evidence curation, and repetition monitoring can all run simultaneously after scoring — each reads the scoring output independently, and none depends on the others.

But the generation agent can't start until all three are complete, because it needs the combined brief. And scoring must complete before any of the parallel agents start, because they all build on the scoring decision.

Designing the parallel and sequential structure requires thinking about decision dependencies, not task dependencies. Two tasks might feel sequential ("first we pick the format, then we pick the evidence") but the judgments might be independent — format selection doesn't depend on evidence selection, or vice versa. They both depend on audience targeting, but not on each other.

When parallel agents run, completion tracking needs to work by field presence, not by status. A single status field can't represent three concurrent states — "scoring_complete" becomes meaningless when three agents are running simultaneously. Instead, track whether each output field is populated: format recommendation present → shaping done. Evidence package present → curation done. Echo warnings present → repetition monitoring done. Only advance when all are populated.

---

## Conflict Resolution

When parallel agents produce contradictory outputs, someone has to resolve the conflict before the downstream agent sees it. Not the downstream agent — that introduces a new judgment at the wrong layer.

Define explicit precedence rules at the architecture level:

**Safety over optimisation.** If the repetition monitor flags a hook type the format agent recommended, the monitor wins. If the evidence agent flags thin evidence but the scorer rated the topic highly, the brief proceeds with a gap flag. Protection takes precedence over performance.

**Specificity over generality.** When two agents produce guidance at different levels of specificity, the more specific wins. Channel-specific conventions override general format defaults. Per-piece voice notes from learned adjustments override general voice guidelines.

**Upstream over downstream.** The scoring agent's audience decision is authoritative. The format agent's pillar assignment is accepted without second-guessing. Decisions made earlier in the pipeline set the frame; later agents work within it.

These rules are defined in advance. The context assembly layer applies them mechanically. The audit trail captures which conflicts were resolved and how — so when something goes wrong, you can trace it back to the specific resolution that didn't fit.

---

## References

This skill loads:
- `references/composition-and-inheritance.md` — how decisions flow downstream without re-interpretation
- `references/context-assembly.md` — the translator layer between structured agent outputs and downstream consumers
- `references/conflict-resolution-patterns.md` — how to define precedence rules for contradictory agent outputs

---

## You Will Need Next

With composition designed, move to **Layer Structure** to determine where routing, orchestration, context assembly, and system infrastructure sit — and how they separate from your domain agents.
