# Uncertainty and Confidence

> How to teach agents what good uncertainty looks like — structured, useful, and honest about what it contains.

---

## The Problem with Model Confidence

Without guidance, a model faced with ambiguous data will always guess. It picks the most plausible interpretation and presents it with the same confidence as everything else. It has no mechanism for expressing partial understanding, because nobody taught it what partial understanding looks like in this context. "I'm not sure" gets replaced with a confident-sounding interpretation that happens to be wrong, and nothing downstream can tell the difference.

Telling the agent to "say you don't know" is a prohibition, and prohibitions alone are weak against a model's drive to be helpful.

## Teaching Good Uncertainty

A reasoning framework teaches the agent what good uncertainty looks like by giving it a structured way to express partial knowledge:

- **What it did observe** — the specific data points, signals, or patterns it found
- **What it couldn't determine** — what was ambiguous, missing, or contradictory
- **What would need to be true for its hypothesis to hold** — the conditions under which its interpretation is correct
- **What confidence level it assigns** — always a percentage, never binary

The output from a well-guided uncertain agent is often more valuable than a confident one:

"The opening was softened, but I'm not sure whether this is an audience-specific preference or a general tone shift. This is the third time I've seen it for this audience, but also the second time this week across all audiences."

That gives the system something to work with. It's an observation with context, not a guess dressed as a conclusion. Downstream agents can use it. A pattern-detection cycle can accumulate it. A human reviewer can see exactly what the agent saw and what it made of it.

## Confidence Scores

Every confidence score should be a percentage (0-100), never binary (yes/no, high/low). Binary confidence hides the distribution — there's a world of difference between 42% and 78%, but both might be "medium" in a three-tier system.

When nothing scores above a meaningful threshold, the agent says so. A scoring agent where no audience profile exceeds 40% confidence flags `low_relevance` rather than forcing a fit. That honest low score is more useful than a forced high one, because downstream agents can adjust:

- The format agent might recommend a broader, less persona-specific format
- The evidence agent might select more general evidence
- The human reviewer might redirect the piece entirely

## Absence vs Presence

Without explicit guidance, models treat absence as signal. An empty CRM field becomes a "gap finding." A quiet period becomes "stalling." A missing relationship becomes "single-thread risk."

Sometimes this is correct — in a diagnostic context, absence can be meaningful. But the same absence, in a factual context, is just an empty field. Maybe nobody logged it. Maybe it doesn't apply.

The framework must define when absence-as-signal reasoning is permitted and when it isn't. Without that explicit control, models default to treating every gap as a finding, because analytical writing trains them to treat noting gaps as thorough.

## Confidence That Travels

Honest uncertainty is only useful if it travels downstream. When an upstream agent flags low confidence, every subsequent agent needs to see that flag and adjust accordingly. A generation agent writing with full confidence against a brief that the scoring agent was 35% sure about produces polished output built on sand.

Design the inheritance chain so that uncertainty propagates:
- Low-confidence scoring → the brief includes the uncertainty
- Thin evidence → the draft acknowledges the gap rather than writing around it
- Conflicting signals → the synthesis preserves the conflict rather than resolving it

Uncertainty isn't a failure state. It's information. The system that surfaces it honestly is more trustworthy than the one that hides it behind confident language.
