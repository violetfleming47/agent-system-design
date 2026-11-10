# Context Assembly

> The translator layer between structured agent outputs and downstream consumers.

---

## What Context Assembly Is

Context assembly sits between agents that produce structured data and the agent that needs to act on it. It's neither a skill nor an orchestration concern. It's a translation layer.

Multiple agents produce structured outputs: classification results, format recommendations, evidence packages, repetition warnings. These outputs contain system noise — internal IDs, confidence percentages, selection reasoning, anti-repetition scores. They may contain contradictions — one agent recommends a hook type another agent flagged as overused. They reference frameworks and data structures the downstream consumer shouldn't need to know about.

Context assembly reads all of these, strips the noise, resolves contradictions (with explicit rules about which agent wins in which conflict), checks live data sources for current context, and produces a clean brief the downstream agent can act on.

## What It Is Not

**Not a skill.** Skills have domain responsibilities — they classify, evaluate, select, generate. Context assembly has no domain opinion.

**Not orchestration.** The orchestrator manages when this step runs. The assembly logic is about what reaches the agent's context window and in what form.

**Not a synthesis agent.** It doesn't re-evaluate. It doesn't add its own analysis. It translates and resolves according to predefined rules.

## When It's Collapsed

When context assembly is buried inside the downstream agent, that agent receives raw structured data and has to parse and resolve it itself. This introduces a new failure surface — the generation agent is now making judgment calls about conflicting signals and parsing JSONB instead of writing.

When context assembly is buried inside orchestration, the orchestrator starts making content-level decisions about what to include and how to resolve conflicts. This violates its traffic-control purity — it should manage flow, not content.

## What It Produces

A brief structured for the downstream agent's needs. In a content pipeline, this might follow a fixed structure:

1. **Audience** — who this is for, from the scoring agent's decision
2. **Argument** — the core point, incorporating learned adjustments
3. **Evidence** — selected evidence, with gap flags if evidence is thin
4. **Market context** — timely intelligence that should shape framing
5. **Format** — specific structural guidance from the shaping agent
6. **Channel** — platform conventions and constraints
7. **Per-piece notes** — anything that varies for this specific piece

Permanent rules (voice, brand, universal constraints) live in the downstream agent. The assembly layer delivers only what changes per piece.

## Conflict Resolution Rules

Define these at the architecture level, not at runtime:

- Repetition warnings override format recommendations (safety over optimisation)
- Learned adjustments override default framing (accumulated evidence over initial design)
- The shaping agent's pillar assignment is authoritative (the assembler doesn't second-guess pillar selection)
- When evidence is thin, the gap flag persists into the brief (the downstream agent writes around it, never with false confidence)

The assembly layer applies these rules mechanically. The audit trail captures which conflicts were resolved and how.
