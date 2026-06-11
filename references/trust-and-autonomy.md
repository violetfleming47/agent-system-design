# Trust and Autonomy

> Earning trust through demonstrated performance, with asymmetric boundaries that are fast toward safety and slow toward authority.

---

## Trust Is Earned, Not Configured

The system starts at maximum human oversight. Every output goes to a human. This isn't a limitation — it's the starting position from which trust is earned through demonstrated performance.

## Trust Levels

**Level 1 — Full Review.** Everything goes to the human. The starting level and the safety default. The system falls back here whenever something goes wrong.

**Level 2 — Standard Autonomy.** High-quality output auto-proceeds based on quality scores. The system has proven it can produce reliable output within defined parameters. Upgrade criteria are quantitative: a minimum volume of pieces reviewed at Level 1, edit rates below a defined threshold, no trust incidents over a defined period, and explicit human approval.

**Level 3 — High Trust.** Broader auto-approval with spot-checking. A percentage of auto-approved work is randomly sampled for human review — not because it's suspected to be wrong, but because the system continues to validate its own judgment. Criteria are stricter: larger volume at Level 2, auto-approved quality within a tight margin of human-reviewed quality, lower edit rates, longer incident-free periods, high spot-check pass rates, and explicit human approval.

## Asymmetric Boundaries

Every boundary is asymmetric. Fast in the direction of safety. Slow in the direction of authority.

**Upgrades are slow:**
- Require meeting quantitative criteria over sustained periods
- Require explicit human approval — the system proposes, the human decides
- The criteria are the same for initial upgrade and recovery after downgrade — no shortcuts

**Downgrades are fast:**
- Trust incidents trigger immediate downgrade without waiting for human confirmation
- The system doesn't wait for the weekly assessment — safety downgrades happen in real time
- Trust incidents include: factual errors in published output, wrong voice or brand representation, claims that don't match the source of truth, content requiring public retraction, quality gate failures on auto-approved content

**Defaults are safe:**
- If the trust system is unavailable, default to Level 1 — never default upward
- If the quality gate crashes, route to human review — never auto-approve on error
- If any component that contributes to the trust assessment is missing data, assume the most conservative interpretation

## What Constitutes a Trust Incident

Trust incidents are defined in advance, not discovered at runtime:

- Published content with a factual error
- Published content with wrong voice or brand representation
- Claims about the company or product that don't match the authoritative source
- Content that had to be publicly retracted or corrected
- Any hard quality failure on content that was auto-approved

Each incident is logged with context: what happened, which agent produced it, what data it was working from, what the trust level was at the time. This trail is essential for understanding whether the incident was a systemic issue or an edge case.

## Recovery

Recovery from a trust incident requires meeting the same criteria as the original upgrade. The system doesn't get credit for "most of the time it was fine." If trust was earned over 50 pieces and lost on one incident, it's earned back over another 50 pieces.

This seems harsh. It's intentional. A system that can fast-track its way back to autonomy after a failure is a system that treats trust incidents as acceptable cost. They're not. They're the most important signal in the system.
