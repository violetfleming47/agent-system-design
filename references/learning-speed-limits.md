# Learning Speed Limits

> Two-speed governance: soft adjustments are automatic and decaying. Permanent changes are human-gated and evidence-backed.

---

## A Single Observation Is Not a Pattern

This is the most important design constraint in the learning system. A single correction, no matter how clear, is not a pattern. Two corrections are not a pattern. The system records them, links them to the specific context that produced the output, and waits.

If a learning agent can act on a single observation, one atypical edit ripples through the entire system. The CEO edited one piece differently because they were in a different mood, and now the system has shifted its tone for the next twenty pieces. That's not learning. That's volatility.

## Speed 1: Observe

Every human edit is captured as an observation. The learning agent reads both versions — the AI's draft and the human's published version — and writes a free-form synopsis: its interpretation of what changed and why.

"The opening was softened from confrontational to curious. The second company reference was removed. The closing was changed from a question to a declarative reframe."

This is pure observation. No system changes. The synopsis accumulates alongside its full context — which audience, which format, which topic, which channel.

## Speed 2a: Adjust (Automatic)

On a regular cycle (typically weekly), the learning agent reviews several weeks of observations. It groups them by context — audience × format × topic × change type — and looks for patterns.

At a defined threshold of similar observations (e.g., five instances of the same kind of correction), it writes a soft runtime adjustment. These are automatic — no human gate. But they're deliberately gentle:

- **Weighted by confidence.** A pattern from five observations carries less weight than one from fifteen.
- **Scoped to context.** "For this audience on this topic, soften contrarian openings." Not "soften all openings."
- **Decaying.** If not reinforced by new observations within a defined window, confidence drops. Eventually the adjustment archives itself.

Pipeline agents treat these as weighted signals, not hard rules. The scoring agent factors them in. The generation agent nudges in their direction. But a low-confidence adjustment doesn't override explicit framework guidance.

## Speed 2b: Evolve (Human-Gated)

When a pattern sustains across enough instances (e.g., ten instances over four weeks), the learning agent doesn't just adjust at runtime. It proposes a permanent change to the framework itself.

The proposal includes:
- The pattern detected
- The evidence — specific observations, with links to the content records that produced them
- The specific recommendation — what should change in the framework
- The impact assessment — which agents would be affected

This sits in a staging queue until a human reviews it. The human examines the evidence, assesses whether the pattern is real and worth encoding permanently, and decides:
- **Approve** — the framework is updated. Previous version preserved for rollback.
- **Modify** — the framework is updated with the human's adjustments.
- **Reject** — the proposal is discarded. The underlying observations remain.

If approved, the corresponding soft adjustment can be archived — the permanent change supersedes it.

## Structural Separation

The boundary between observation and action must be structural, not aspirational.

The observing agent literally cannot write to the frameworks. It writes to an observation store. A separate pattern-detection process reads that store on its own cycle. Only the pattern-detection process can propose changes. And only the human can approve permanent changes.

This separation does three things:
1. Prevents knee-jerk reactions to outliers
2. Forces the system to accumulate evidence before changing behaviour
3. Creates a complete audit trail — every framework change traces back through the pattern, through the observations, through the specific human interactions that produced each observation

## Decay

Adjustments that aren't reinforced lose confidence over time. This is deliberate. An observation from six months ago in a fast-moving environment may no longer be relevant. The system should forget what it hasn't re-learned.

Typical decay schedule:
- Not reinforced in 60 days → confidence reduced
- Not reinforced in 90 days AND confidence below a threshold → archived
- Superseded by a permanent framework change → archived immediately

Archived adjustments aren't deleted. They're historical — available for trend analysis but removed from active reasoning.
