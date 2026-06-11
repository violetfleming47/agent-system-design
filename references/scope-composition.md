# Scope Composition

> The three-layer containment pattern: frameworks fill the space, noise-naming directs the adjacent, prohibitions close the gaps.

---

## The Three Layers, In Order

### 1. Fill the Scope with Frameworks

The most important thing about a skill definition isn't what it tells the agent to do. It's how completely it fills the agent's reasoning space. When the framework is specific enough — which dimensions to assess, how to weight them, what confidence levels look like, what the output format is field by field — the agent's entire reasoning space is occupied. It's not thinking about what else it could do with this data, because the framework has given it enough to do.

A scoring agent with a framework that specifies four scoring dimensions, context loading procedure, hypothesis formation, profile querying logic, confidence calibration, and output structure is too busy doing its job to drift. The work fills the space.

The framework is the skill. Not documentation. Not overhead. The reasoning structure that makes the agent competent at its specific job.

### 2. Name the Noise

Even with frameworks filling the scope, agents encounter data outside their task. This is inevitable with live data. The instinct is to say "just focus on your task." But the model has already processed the information — it's in context. The model's default is to include anything potentially relevant.

The fix: name it in advance.

"You will encounter deal stage information and pipeline values. These are not your concern. You are delivering a list of people relevant to this task."

When information arrives pre-classified, the model processes it and releases it instead of absorbing it into the deliverable. The decision — "is this relevant?" — doesn't fire because you already answered it.

The critical addition: give the noise somewhere to go. A scratchpad, a separate field, a log. The noise has a named destination that isn't the deliverable. The agent doesn't choose between including it and losing it. It has a third option: acknowledge it and route it elsewhere.

### 3. Close the Gaps with Prohibitions

After frameworks and noise-naming, there are still specific adjacent functions the agent could drift into. These are particular temptations the data creates:

- A people-finding agent: you do not assess deal health, produce pipeline commentary, or track lifecycle stages.
- A validation agent: you evaluate, never rewrite, never suggest alternatives, never re-score.
- An evidence agent: you select evidence, never reshape the argument to fit what's available, never decide the audience.

Prohibitions are the last line of defence, not the first. Written without frameworks and noise-naming, a prohibition list is a list of "don't" instructions fighting the model's drive to be helpful. Written after frameworks fill the scope and noise is named, prohibitions catch the specific remaining temptations that live in the narrow gap between "I know what I'm supposed to do" and "but this data is right here."

## Why the Order Matters

Start with prohibitions (what most people do) and you get a restrictive agent fighting its own helpfulness. Start with frameworks and you get an agent that doesn't want to drift because it has enough to do. Add noise-naming and it knows how to handle what it encounters outside its scope. Add prohibitions and the remaining edge cases are closed.

The three layers create complete containment:
- The agent has enough work to fill its reasoning
- It knows what it will encounter outside that work and where it goes
- The specific adjacent functions it might still drift into are explicitly closed
