# Human-in-the-Loop Design

> Where humans sit and why the decision boundary matters for both safety and learning.

---

## The Decision Boundary

The human sits after the agent has done its complete work, before anything consequential happens. Not partway through. Not at every checkpoint. At one meaningful point where the agent has committed to an output and the human can react to a complete decision.

This produces the richest learning signal. Both feedback paths are meaningful:

**Direct editing:** The human changes the output. The gap between the AI's version and the human's published version is the learning signal. Structural, visible, contained. The system preserves both versions — the edit delta is what the learning agent observes.

**Verbal direction:** The human sends notes back. "Soften the opening." "Lead with the data." The system re-runs with the original brief plus the human's notes verbatim — never summarised, never interpreted. The human's words are the instruction.

Both paths end with a completed output. The learning system can compare what the agent produced with what the human approved. That difference, accumulated over time, is how frameworks evolve.

## Why Checkpoints Everywhere Fails

When humans review every intermediate step, three things happen:

1. **Every checkpoint is a bottleneck.** The system can only move as fast as the human reviews.
2. **No checkpoint produces a clean signal.** The human is intervening before the agent has finished thinking. Was the intermediate output wrong, or was it an incomplete step that would have been corrected downstream?
3. **The human's corrections are fragmented.** A note on the scoring step, a note on the format step, a note on the evidence step — none of these captures what the human actually wanted the final output to look like.

## Why No Humans Fails

Systems without human oversight run on raw model capability. They're confident, fast, and increasingly disconnected from what "good" looks like in the specific domain. Without human corrections, the learning system has nothing to learn from. Without human review, trust can never be calibrated. The system doesn't know what it doesn't know.

## The Approve-Edit-Redirect Pattern

At the decision boundary, the human has a small set of options:

- **Approve** — the output is good. A positive data point for the learning system. Clean approval, no delta.
- **Edit directly** — the output needs changes. The delta is the learning signal. Both versions preserved.
- **Send back with notes** — the output needs a different approach. Re-stimulation with human direction. The system tries again.
- **Kill** — the output shouldn't exist. Reason logged. A strong negative signal.

Each option produces a distinct signal for the learning system. Approve = confirmation. Edit = correction. Send back = redirection. Kill = rejection. The system accumulates all four.

## Designing the Review Experience

The human needs to see:
- The complete output (not intermediate structured data)
- The agent's reasoning (why it made the choices it made)
- Any flags from upstream agents (low confidence, thin evidence, gap warnings)
- The context that produced this output (what brief, what evidence, what audience)

They don't need to see:
- Internal IDs, JSONB, or database structure
- Confidence percentages from intermediate steps
- The full reasoning trace of every upstream agent

The review experience is designed so the human can make a fast, informed decision. Not parse system internals.
