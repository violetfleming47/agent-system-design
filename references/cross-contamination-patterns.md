# Cross-Contamination Patterns

> How models cross-pollinate when holding multiple perspectives, and why the output looks fine when it isn't.

---

## The Mechanism

When a model holds data from multiple domains in the same context window, it doesn't process each domain independently. It builds coherence. The competitive intelligence colours the market assessment. The audience profile influences the format choice. The financial data shifts the strategic evaluation.

This isn't a bug. It's how language models work — they find patterns and connections across everything in context. The problem is that connections across competing perspectives produce rationalisation, not analysis.

## The Invisible Failure

Cross-contaminated output passes every quality check. It's well-structured. It addresses every dimension. It includes evidence. The conclusions support each other. That's the problem — in reality, those dimensions often point in different directions. When they all agree in the output, the model smoothed the tensions away.

A content piece produced by a monolith that scores, shapes, curates, and generates in one pass looks correct. The audience is identified. The format is chosen. The evidence is selected. The draft is written. But every decision was made in the same context window, influenced by every other decision:

- The format influenced the scoring (picked the audience that fit the format best)
- The evidence reshaped the framing (argued from available evidence rather than the right evidence)
- The generation ran against a brief that was never locked down (nothing forced the brief to be finished before writing started)

The output isn't wrong. It's mushy. Every edge is soft. The audience targeting is approximate. The evidence selection is convenient rather than deliberate. Nobody catches it because it passes every check.

## Common Patterns

**Anchor bias.** The first perspective encountered dominates. In a deal evaluation with market, competitive, financial, and strategic data all present, the model anchors on whichever it processes first and bends the rest to fit.

**Narrative smoothing.** The model finds a story that accommodates all the data, even when the data genuinely points in conflicting directions. A strong market fit and increasing competitive pressure should produce tension. In a monolith, the competitive pressure gets framed as "opportunity in a growing market" — technically true, but the threat is neutralised.

**Scope absorption.** An agent with access to data outside its task uses that data. The scoring agent that can see pipeline values starts commenting on deal health. The validation agent that can see audience profiles starts re-scoring the audience. Not because it's malfunctioning — because it was trained to be comprehensive, and inclusion is always safer than omission for a model optimised on helpfulness.

**Re-interpretation drift.** When multiple agents each apply their own interpretation of an upstream decision, the decision drifts. Five agents, five slight re-interpretations, and by the final agent, the audience has shifted, the framing has morphed, and the evidence supports a subtly different argument. Nobody diverged dramatically. Nobody converged either.

**Framework contamination.** A model with a risk assessment framework loaded will find risks. A model with a scoring rubric loaded will produce scores. The analytical lens creates the finding. If a validation agent has audience profiles loaded, it will evaluate audience fit — even though that judgment was already made upstream.

## The Compounding Problem

One mushy piece is fine. Thirty mushy pieces and the system has no identity. The voice drifts. The audience targeting is inconsistent. The evidence reuse is invisible. The format distribution is random. Nobody made a bad decision. Nobody made a clean one either.

This is the failure mode that scales. Not a dramatic collapse, but a slow loss of precision that makes teams lose trust in their agents without being able to name what went wrong.

## The Fix

Separate at the point of judgment. One lens per agent. Each agent loads only the data and frameworks relevant to its perspective. The synthesis layer combines independent assessments with tensions preserved. Tensions are the information. The places where perspectives disagree are where human judgment is needed most.

A system that surfaces tensions is more useful than one that resolves them — because the resolution was done by a model finding coherence, not by a decision-maker weighing evidence.
