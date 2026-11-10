# Judgment and Lens Separation

> The principles behind decomposing at the point of judgment and assigning one analytical lens per agent.

---

## Why Judgment, Not Task

When you decompose by task ("this agent qualifies leads"), you're mirroring how humans divide labour. But a single task frequently requires multiple, conflicting perspectives. When one agent holds multiple perspectives simultaneously, the model doesn't evaluate each dimension independently and then synthesise. It cross-pollinates — finding coherence across everything in context. Coherence across competing perspectives isn't analysis. It's rationalisation.

Decompose by judgment instead. Ask: "Where are the distinct judgment calls?" Each judgment is a point where something has to be assessed, interpreted, classified, or decided — where the quality of the thinking matters, not just the execution.

## Procedural vs Interpretive Judgment

Most real-world judgments are one of two types:

**Procedural judgment** follows a defined method against structured data. The method can be specified step by step — which dimensions to assess, how to weight them, what confidence levels look like, what the output format is. When the procedure is specific enough, it fills the agent's entire reasoning space.

**Interpretive judgment** makes sense of messy, unstructured, or ambiguous information. CRM notes, transcripts, human edits. You can't write step-by-step instructions for these because every instance is different. Instead, you provide a reasoning framework — a taxonomy of what kinds of things the agent might find, interpretation rules for each category, confidence thresholds, and guidance on how to express uncertainty well.

Most agent tasks involve both kinds. A scoring agent follows a procedure to load the right profiles and query the right data (procedural). Then it reads raw input and assesses whether the language resonates with a particular audience (interpretive). Both fill the scope. Both prevent drift. They do it differently.

## One Lens Per Agent

A lens is an analytical viewpoint applied through a specific framework against specific data. A market lens sees market data through market frameworks. A competitive lens sees competitive data through competitive frameworks.

The rule is simple and absolute: one lens per agent. When a monolith holds multiple lenses:

- The competitive data makes the market fit look weaker than it is
- The strategic alignment makes the pricing seem more defensible
- The model finds a narrative that accommodates everything
- The conflicts — which are the actual information — get smoothed away

Separated, each assessment is honest. Combined with tensions preserved, the decision-maker sees the full picture.

## When Separation Isn't Needed

Not every judgment needs its own agent. A formatting agent that structures output according to a template has a singular judgment: does this match the format? One lens, one agent, done.

The test: does this judgment involve evaluation, assessment, or recommendation? Does it require weighing evidence, interpreting signals, or forming opinions? If yes, check whether multiple perspectives are involved. The moment you identify multiple perspectives within a single judgment, you've identified multiple agents.

## Identifying Cross-Contamination Risk

Cross-contamination happens when two judgments share a context window and the model finds coherence between them. Signs that your judgments need separation:

- The output reads as "integrated" or "balanced" — the model found a narrative
- Changing one input changes assessments in unrelated dimensions
- The agent produces recommendations that feel "obvious" — it rationalised rather than analysed
- You can't trace which specific evidence drove which specific conclusion
- Tensions between perspectives are absent from the output — smoothed away
