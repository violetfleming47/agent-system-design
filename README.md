# Agent System Design

> Design and decompose agent systems that hold in production — not by task, but by judgment.

---

## What This Package Does

Most people decompose agent workflows by task: "this agent qualifies leads, this one writes outreach, this one reviews contracts." That mirrors how humans divide labour. It's intuitive. And it produces agents that drift, cross-pollinate, and generate mushy output that passes every quality check except the one that matters.

This package walks you through a different approach: decompose at the point of judgment, fill each agent's reasoning space so completely that there's nowhere to drift, and compose agents through inheritance so decisions flow forward without re-interpretation.

Six skills, each handling a distinct phase of the design process. Use them in order for a full system design, or independently for specific design challenges.

---

## Skills

### 01 — Judgment Mapping
Find where the distinct judgments live in your workflow. Not tasks — judgment calls. Points where something has to be assessed, interpreted, classified, or decided. The quality of this decomposition determines everything downstream.

### 02 — Lens Identification
Determine what analytical perspective each judgment requires. One lens per agent. When a model holds multiple lenses, it cross-pollinates — finding coherence instead of preserving the tensions that are the actual information.

### 03 — Scope Definition
Fill each agent's reasoning space with three layers, in order: frameworks that occupy the space so completely there's no room to wander, noise-naming that accounts for adjacent data before the agent encounters it, and prohibitions that close the remaining gaps.

### 04 — Composition
Design how decisions flow between agents. One agent makes the call, everyone downstream inherits it. No re-interpretation. No re-querying upstream frameworks. Decisions travel forward with confidence that propagates — including honest uncertainty.

### 05 — Layer Structure
Identify the eight layers your system needs: routing, orchestration, data reading guides, reasoning frameworks, skills, context assembly, metadata and learning, and lifecycle. Most teams have skills and some orchestration. Most are missing half the layers.

### 06 — Human Placement
Design where humans sit in the loop. After complete work, before consequences. One meaningful decision point that produces the richest learning signal. Trust that's earned through demonstrated performance, with asymmetric boundaries — fast toward safety, slow toward authority.

---

## Reference Documents

The `references/` directory contains the principles and patterns each skill draws from:

- **Judgment and Lens Separation** — why one lens per agent, and how to identify genuine judgment boundaries
- **Cross-Contamination Patterns** — how models cross-pollinate perspectives and why the output looks fine when it isn't
- **Scope Composition** — the three-layer containment pattern
- **Uncertainty and Confidence** — teaching agents what good uncertainty looks like
- **Framework Types** — procedural vs reasoning frameworks, when to use each
- **Synthesis Layer Design** — combining independent assessments without reintroducing bias
- **Composition and Inheritance** — how decisions flow downstream
- **Context Assembly** — the translator layer between structured outputs and downstream consumers
- **Conflict Resolution Patterns** — defining precedence rules for contradictory outputs
- **Eight-Layer Architecture** — the full layer model
- **System vs Domain Skills** — separating infrastructure from domain judgment
- **Human-in-the-Loop Design** — where humans sit and why
- **Trust and Autonomy** — earning trust with asymmetric boundaries
- **Learning Speed Limits** — two-speed governance for system learning

---

## How to Use This

Bring a workflow, a system, or a problem. Start with Judgment Mapping and work through the skills in order. Or jump to the specific skill that matches your current challenge.

Each skill is conversational — describe your situation and the skill walks you through the design methodology, producing architecture decisions grounded in the principles from the reference documents.

---

## About

Created by [Violet Fleming](https://github.com/violetfleming47). These tools are grounded in a design philosophy developed across production multi-agent systems — the same thinking behind [Orion](https://github.com/violetfleming47).

Part of a suite of open-source agent design tools:
- **Agent System Design** — design and decompose agent systems
- [Agent Knowledge Curator](https://github.com/violetfleming47/agent-knowledge-curator) — capture institutional knowledge
- [Agent Drift Prevention](https://github.com/violetfleming47/agent-drift-prevention) — prevent silent degradation
- [Agent Edge Cases](https://github.com/violetfleming47/agent-edge-cases) — failure modes you haven't considered
- [Agent System Review](https://github.com/violetfleming47/agent-system-review) — architectural review of existing systems

Licensed under [CC BY-NC 4.0](LICENSE).
