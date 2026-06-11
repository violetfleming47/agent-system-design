# Human Placement

> Design where humans sit in the loop and what governance boundaries keep the system aligned over time.

---

## What This Skill Does

This is the skill most teams either overcorrect or undercorrect on, and both directions fail.

The overcorrection: humans at every checkpoint. Review the scoring output. Approve the format recommendation. Confirm the evidence selection. Edit the brief. Review the draft. The system can't move faster than the human can click, and none of the checkpoints produce a clean learning signal because the human is intervening before the agent has finished thinking.

The undercorrection: remove humans entirely. The system runs on raw model capability. It's fast, it's scalable, and it's increasingly disconnected from reality. Without human corrections, the learning system has nothing to learn from. Without human review, trust can't be calibrated. The system doesn't know what it doesn't know, and nothing tells it.

The architecture that works is neither. It places the human at exactly the right points — after the agent has done its complete work, before anything consequential happens — and designs the system so every human interaction produces a signal the system can learn from.

---

## The Decision Boundary

Here's the principle: the human sits after the agent has done its complete work, before anything consequential happens.

Not partway through. Not at every intermediate step. At one meaningful point where the agent has committed to a complete output and the human can react to a finished decision.

This matters for two reasons. First, it's the only way to get a clean learning signal. When a human reviews a finished output and edits it, the gap between what the AI produced and what the human published is a precise, structural signal. The system committed to something specific. The human changed specific things. The delta is the lesson.

When a human intervenes partway through — "the scoring looks off, let me adjust it" — the learning signal is fragmented. Was the scoring actually wrong, or was it an intermediate step that would have been corrected downstream? Would the final output have been fine if the human had let it complete? You can't tell, because the system never finished thinking.

Second, it's the only way to avoid bottlenecks. Every human checkpoint is a queue. If five checkpoints each take two minutes of human attention, the pipeline takes ten minutes of human time per piece. If one checkpoint takes three minutes but the other four were automated steps that run in seconds, the pipeline takes three minutes of human time. And that three minutes produces a richer signal than the ten, because the human is reacting to the system's complete reasoning, not interrupting fragments of it.

---

## Feedback Paths

At the decision boundary, the human has a small set of options. Each one produces a distinct signal for the learning system:

**Approve.** The output is good. This is a positive data point — the system committed to something and the human confirmed it was right. Not dramatic, but meaningful. The system learns what "good" looks like through accumulation of clean approvals.

**Edit directly (delta capture).** The human changes the output. The system preserves both the original AI version and the human's edited version. The gap between them is the primary learning signal. "The opening was softened from confrontational to curious. The second company reference was removed. The closing was changed from a question to a declarative reframe." That delta, linked to its full context — which audience, which format, which topic, which channel — is what the learning system observes over time.

**Send back with notes (re-stimulation).** The human writes direction: "Soften the opening hook. Move the regulatory reference earlier. Less company promotion." These notes go back to the system verbatim — never summarised, never interpreted. The system re-runs with the original brief plus the human's exact words. The generation agent tries again with human guidance layered on. Then the revised output returns to the human for another decision.

**Kill.** The output shouldn't exist. Reason logged. Pipeline terminates. This is a strong negative signal — something went wrong enough that the piece isn't salvageable.

Both edit paths can happen on the same piece. The human sends notes (re-stimulation), the system revises, and then the human makes final edits (delta capture). The delta captured is between the system's final best effort and what the human actually published — the most useful signal, because the system had the maximum chance to get it right.

---

## The Trust Model

Trust should be earned, not configured. Most systems are deployed with a fixed level of human oversight — either everything is reviewed or nothing is. Neither is right. The system should start with maximum human oversight and earn autonomy through demonstrated performance.

### Level 1 — Full Review

Everything goes to the human. Starting level and safety default. This is where the system proves itself. Every piece is reviewed, every edit is captured, every decision is validated.

This is not a limitation. It's the foundation. The system is building a track record. The learning system is accumulating observations. The baselines are being established. Skip this level and the system has no calibration — it's operating on raw model capability without contextual grounding.

### Level 2 — Standard Autonomy

High-quality output auto-proceeds based on quality scores. The system has demonstrated, through sustained performance at Level 1, that it can produce reliable output within defined parameters.

Upgrade criteria are quantitative and auditable. Not "it seems to be working" — specific numbers. A meaningful volume of pieces reviewed at Level 1 (enough to be statistically significant). Edit rates below a defined threshold (the human isn't changing much). No trust incidents over a defined period (nothing went seriously wrong). And explicit human approval — the system proposes the upgrade, the human decides.

At Level 2, the system auto-approves output that scores above a quality threshold. Below-threshold output still goes to human review. The learning system continues accumulating observations from both paths — learning from what was auto-approved (by tracking downstream engagement and performance) and from what was human-edited (through direct delta capture).

### Level 3 — High Trust

Broader auto-approval with spot-checking. The quality threshold drops slightly, but a percentage of auto-approved content is randomly selected for human review — not because it's suspected to be wrong, but because the system continues to validate its own judgment.

The criteria for Level 3 are stricter than Level 2: even larger volume at the previous level, auto-approved quality within a tight margin of human-reviewed quality (the system's unsupervised output is nearly as good as its supervised output), lower edit rates, longer incident-free periods, high spot-check pass rates, and explicit human approval.

Spot-checking is the system's honesty mechanism. It's saying: "I'm confident enough to auto-approve, but I'm not confident enough to stop checking." If spot-check pass rates drop, that's a signal that the system's judgment is drifting — and it can trigger re-evaluation of the trust level.

---

## Asymmetric Boundaries

This is the governance principle that holds everything together: every boundary in the system should be asymmetric. Fast in the direction of safety. Slow in the direction of authority.

**Upgrades are slow.** They require meeting quantitative criteria over sustained periods. They require explicit human approval. The system proposes; the human decides. There are no shortcuts — the criteria are the same for initial upgrade and for recovery after a downgrade.

**Downgrades are fast.** Trust incidents trigger immediate downgrade without waiting for human confirmation. Published content with a factual error → immediate downgrade. Wrong voice or brand representation → immediate downgrade. Claims that don't match the authoritative source → immediate downgrade. Content requiring public retraction → immediate downgrade. Any quality gate failure on auto-approved content → immediate downgrade.

The system doesn't wait for the weekly assessment to downgrade. Safety downgrades happen in real time. The asymmetry is deliberate: the cost of granting authority prematurely is higher than the cost of restricting authority unnecessarily. So upgrading is slow and gated, and downgrading is fast and automatic.

**Recovery requires the same criteria as the original upgrade.** If trust was earned over fifty pieces and lost on one incident, it's earned back over another fifty pieces. This seems harsh. It's intentional. A system that can fast-track its way back to autonomy after a failure is a system that treats trust incidents as acceptable cost. They're not.

**Defaults are safe.** If the trust system itself is unavailable, default to Level 1 — never default upward. If the quality gate crashes, route to human review — never auto-approve on error. If any component contributing to the trust assessment is missing data, assume the most conservative interpretation. Never default upward on error.

---

## The Observation-Action Boundary

The subtlest and most important boundary in the whole system: the line between watching and doing.

A learning agent should observe every human edit. It reads the draft, reads the published version, and writes a synopsis of what changed and why. That's it. It doesn't create system-wide adjustments from a single observation. It doesn't change any shared data. It doesn't write anything that affects the next pipeline run. Observation mode is observation only.

That restraint has to be structural, not aspirational. The observing agent literally cannot write to the frameworks. It writes to an observation store. A separate pattern-detection process reads that store on its own cycle — daily, weekly, depending on the domain. And only the pattern-detection process can propose changes, which then go through the two-speed governance.

Why? Because a single observation isn't a pattern. Two observations aren't a pattern. The system should need several confirmed instances before a soft runtime adjustment and many instances over weeks before proposing a permanent change. If a learning agent can act on a single observation, one atypical edit — the CEO was in a bad mood, the reviewer was rushing, the piece was experimental — ripples through the entire system.

The same principle applies to monitoring agents. An agent that watches for content repetition should detect and flag. It should never block. Every flag should be advisory. It reports, and the human or the system decides.

And it applies to the trust tracker. A trust-tracking agent can downgrade autonomy instantly but can never upgrade it without human approval. Fast toward safety. Slow toward authority. Every boundary. Everywhere.

---

## Learning Speed Limits

Human corrections feed the system — but not instantly and not unconditionally. This is the two-speed governance model:

**Speed 1: Soft runtime adjustments.** After enough instances of the same pattern (five similar corrections, grouped by context), the learning system creates a weighted adjustment. Automatic, no human gate. But deliberately gentle — scoped to the specific context ("for Gatekeeper content on regulatory compliance, soften contrarian openings"), weighted by confidence, and decaying if not reinforced by new observations within a defined window. Pipeline agents treat these as signals, not rules.

**Speed 2: Permanent framework changes.** After sustained patterns (ten instances over four weeks), the learning system proposes a change to the framework itself. The proposal includes the evidence, the pattern, the recommendation, and the impact assessment. It sits in a staging queue until a human reviews it. The human examines the evidence, decides whether the pattern is real and worth encoding permanently, and approves, modifies, or rejects.

The distinction between these two speeds is the most important governance boundary in the system. Soft adjustments let the system respond to emerging patterns without human bottlenecks. Permanent changes keep the frameworks under human ownership. The system adapts at the pace of its observation, but its foundational reasoning structures only evolve through human judgment.

---

## What This Produces

A human placement design specifies:
- Where in the flow the human sits (after complete work, before consequences)
- What feedback paths exist (approve, edit, redirect, kill) and what signal each produces
- The trust model (levels, quantitative criteria, progression rules)
- Asymmetric boundaries (fast toward safety, slow toward authority, safe defaults)
- What monitoring agents can observe vs do (advisory flags, never blocks)
- Learning speed limits (soft adjustments vs permanent changes, minimum thresholds, decay)

---

## References

This skill loads:
- `references/human-in-the-loop-design.md` — where humans sit and why the decision boundary matters
- `references/trust-and-autonomy.md` — earning trust through demonstrated performance, asymmetric boundaries
- `references/learning-speed-limits.md` — two-speed governance, observation vs action

---

## This Completes the Agent System Design Package

You now have:
1. **Judgment Map** — where the distinct judgments are
2. **Lens Identification** — what perspective each judgment needs
3. **Scope Definition** — frameworks, noise-naming, and prohibitions for each agent
4. **Composition** — how decisions flow and inherit
5. **Layer Structure** — where infrastructure and domain separate
6. **Human Placement** — governance, trust, and the learning boundary

To fill your agents with the right knowledge, move to **Agent Knowledge Curator**. To understand where your system might be fragile, use **Agent Drift Prevention**. To challenge your assumptions, try **Agent Blind Spots**.
