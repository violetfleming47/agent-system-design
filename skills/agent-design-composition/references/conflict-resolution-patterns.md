# Conflict Resolution Patterns

> How to define precedence rules for contradictory agent outputs.

---

## Why Conflicts Happen

When multiple agents run in parallel — each with its own lens, its own data, its own framework — they will sometimes produce contradictory outputs. This is a feature, not a bug. Contradiction means two honest perspectives disagree. That's information.

But downstream agents can't act on contradictions. The generation agent can't simultaneously use the hook type the format agent recommended and avoid the hook type the repetition monitor flagged. Someone has to resolve it before the brief is assembled.

## Resolution Is Architecture, Not Runtime

Conflict resolution rules are defined at the architecture level. They're part of the system design, decided in advance, not discovered by the context assembly layer at runtime.

This matters because runtime resolution means the assembly layer is making judgment calls — it's deciding which agent is "more right." That's a domain opinion in a layer that shouldn't have one.

## Common Precedence Patterns

### Safety Over Optimisation

When one agent optimises and another protects, the protector wins.

- Repetition monitor flags a hook type → that hook type is suppressed, even if the format agent recommended it
- Evidence agent flags thin evidence → the gap flag persists, even if the scoring agent rated the topic highly
- Trust tracker downgrades autonomy → all content routes to human review, regardless of quality scores

### Specificity Over Generality

When two agents produce guidance at different levels of specificity, the more specific wins.

- Format agent recommends "7-slide carousel, 480x480" → overrides a general "visual content" recommendation
- Channel-specific conventions → override general format defaults
- Per-piece voice notes from learned adjustments → override general voice guidelines

### Upstream Over Downstream

Decisions made earlier in the pipeline are authoritative for agents later in the pipeline.

- Scoring agent's audience decision → not re-evaluated by shaping or curation agents
- Shaping agent's pillar assignment → accepted by the prompt assembler without second-guessing
- The inheritance chain: decisions flow forward, never backward

### Advisory Over Blocking

Monitoring agents report but never block. Their flags are information for the downstream agent, not vetoes.

- Repetition warnings influence but don't prevent
- Low-confidence flags travel but don't halt the pipeline
- Gap assessments are visible but don't terminate processing

The exception: hard safety failures (factual errors, compliance violations) can block.

## Documenting Resolutions

Every conflict resolution should be auditable. The context assembly layer captures:
- Which agents conflicted
- What each said
- Which rule applied
- What the resolution was

This audit trail sits alongside the assembled brief, not inside it. The downstream agent sees the clean resolution. The system has the full record for debugging and learning.
