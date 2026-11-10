# Synthesis Layer Design

> How to combine independent assessments without reintroducing the bias you just eliminated.

---

## The Synthesis Layer Is Not a Fifth Opinion

The most common mistake: creating separate lens-agents and then building a synthesis agent that re-evaluates everything. Now you have five agents — four with clean perspectives and one monolith that recombines them and reintroduces all the cross-pollination you just eliminated.

The synthesis layer must be architecturally dumb about the domain. It doesn't have analytical frameworks. It doesn't score, assess, or evaluate. It assembles.

## What It Does

1. **Takes independent outputs** from each lens-agent
2. **Resolves formatting conflicts** — normalises structure, terminology, output shape
3. **Flags substantive contradictions** — where two agents disagree on something material
4. **Presents the combined view** with each perspective's independence preserved

If Agent A says the market is strong and Agent B says competitive pressure is increasing, the synthesis layer reports both. It doesn't resolve the tension. It surfaces it.

## Conflict Resolution

Some conflicts need to be resolved before the downstream agent can proceed. Not all tensions can be left for the human.

Define explicit precedence rules at the architecture level:
- If the repetition monitor flags a hook type the format agent recommended, the monitor wins (safety over optimisation)
- If the evidence agent flags thin evidence but the scoring agent rated the topic highly, the draft proceeds with an evidence gap flag (the scoring decision stands, but the gap is visible)
- If two agents produce contradictory format guidance, the agent with the narrower scope wins (specificity over generality)

These rules are defined in advance, not discovered at runtime. The synthesis layer applies them mechanically. It doesn't reason about which agent is "more right."

## What It Strips

Downstream agents should not receive:
- Internal IDs, database terminology, or system noise
- Raw confidence percentages from intermediate steps (unless the downstream agent specifically needs them)
- Framework taxonomy terms that only make sense to the producing agent
- Reasoning traces that would cause the downstream agent to re-evaluate

The synthesis layer translates from the system's internal language to the downstream agent's input language.

## The Prompt Assembler Pattern

In a content pipeline, this layer often manifests as a "Prompt Assembler" — a dedicated step that reads all upstream structured outputs and produces a prose brief for the generation agent.

The Prompt Assembler:
- Knows which downstream agent will read the brief
- Delivers only what changes per piece (permanent voice rules live in the downstream agent)
- Checks live data sources for current context
- Resolves conflicts using defined precedence rules
- Writes in a fixed structure: audience → argument → evidence → context → format → channel

The generation agent reads only this assembled brief — never the structured data, never the database, never the raw framework outputs. All it sees is a creative director's handoff.
