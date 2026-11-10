---
name: agent-design-scope-definition
description: Fill an agent's reasoning space with frameworks, noise-naming, and prohibitions so there is nowhere left to drift. Use when defining what one agent sees, ignores, and must not do.
---

# Scope Definition

> Fill each agent's reasoning space so completely that there's nowhere left to drift.

---

## What This Skill Does

This is the most important skill in the entire suite. If you get scope definition right, most of the problems people encounter with agents — drift, hallucination, over-interpretation, scope creep — become structurally impossible. If you get it wrong, no amount of prompt engineering, guardrails, or monitoring will save you.

The core insight is simple and often missed: the most important thing about a skill definition isn't what it tells the agent to do. It's how completely it fills the agent's reasoning space, so there's nowhere left to drift.

When people build agents, they start with capability. What should this agent do? What data should it access? What output should it produce? They write the job description. And the agent does the job — plus everything adjacent to it that it found along the way.

A people-finding agent that reads CRM data starts commenting on pipeline health. An evidence-selection agent that reads market signals starts reshaping content direction. A validation agent that reads drafts starts rewriting instead of evaluating. A scoring agent that reads qualification frameworks starts producing risk assessments nobody asked for.

These aren't malfunctions. They're what models do when you leave a vacuum. They fill it with capability. The model saw data. The model has the ability. Nobody said not to. So it did.

The fix isn't better instructions. It's not even a prohibition list, though prohibitions matter. The fix is three things working together, in a specific order: a framework that fills the agent's scope so completely that there's no room to wander, a clear account of what adjacent information the agent will encounter and where it goes, and explicit prohibitions that close whatever gaps remain. All three. In that order.

The order matters. Let me explain why.

---

## Layer 1: Fill the Scope with Frameworks

Most people jump straight to prohibitions when an agent drifts. "Don't comment on pipeline health." "Don't rewrite the content." "Stay focused on your task." These feel like the obvious fix. The agent did something wrong, so you tell it not to do that thing.

But prohibitions are fighting the model's fundamental drive to be helpful. The model encountered data, had the capability to do something useful with it, and nobody told it that the useful thing was someone else's job. A prohibition says "don't." The model's training says "but I can help." The prohibition sometimes wins and sometimes doesn't, depending on how strongly the data in front of the model suggests the adjacent function.

The framework approach is different. Instead of telling the agent what *not* to do, you give it so much to do that drift becomes structurally uninteresting. The agent isn't tempted to comment on pipeline health because it's fully occupied assessing pain-point alignment, language resonance, priority match, and confidence calibration across four audience profiles. It has enough work to fill its reasoning space. The adjacent data is still visible, but the agent has no cognitive room for it.

This is the difference between a person who's told "don't look at your phone during the meeting" and a person who's so engaged in a challenging problem that they forget their phone exists. The first requires willpower. The second is structural.

### Two kinds of frameworks

There are two kinds of frameworks, and most agents need both.

**Procedural frameworks** occupy the reasoning space with method. They specify, step by step, how to do the work. A scoring agent's procedural framework doesn't just say "score content against audience profiles." It says *how*. Read the input first. Form an initial hypothesis. Query the 2-4 most relevant profiles — not all of them, because loading everything dilutes attention. Score each profile on four specific dimensions. Weight them according to defined rules. Express confidence as a percentage. If nothing scores above 40%, flag low relevance rather than forcing a fit. Structure the output with specific fields, and document what each field means to the agent that reads it next.

When the framework is this specific, the agent's entire reasoning space is occupied. Every step is defined. Every output field has a purpose. The agent is executing a detailed methodology, not improvising from a task description.

**Reasoning frameworks** guide judgment on messy data. Some data can't be processed procedurally. CRM notes written by a busy salesperson in thirty seconds between calls. Transcripts where four people talked over each other. Human edits where the draft was restructured, the tone shifted, and a reference was added, all in one pass. You can't write a step-by-step process for interpreting that. The data is too varied. Every instance is different.

This is where most people either over-prescribe or under-prescribe, and both fail. Over-prescribe and the agent tries to force messy reality into rigid categories, producing metadata that looks clean but misrepresents what actually happened. Under-prescribe and the agent improvises, interpreting the data through whatever analytical lens it finds most interesting — which is usually the one you didn't want.

A reasoning framework gives the agent a structure to think within. Not steps to follow, but a way of seeing. A taxonomy of what kinds of things the agent might find. Interpretation rules for each category. Confidence thresholds that tell the agent how sure it needs to be before classifying something. And — this is the part people miss — guidance on how to be uncertain well.

### Teaching good uncertainty

Without a framework, a model faced with ambiguous data will always guess. It will pick the most plausible interpretation and present it with the same confidence as everything else. It has no mechanism for expressing partial understanding, because nobody taught it what partial understanding looks like in this context. So "I'm not sure" gets replaced with a confident-sounding interpretation that happens to be wrong, and nothing downstream can tell the difference.

A reasoning framework changes this by teaching the agent what good uncertainty looks like. Not just "say you don't know" — that's a prohibition, and it's weak against the model's drive to be helpful. Instead, the framework gives the agent a way to express what it did observe, what it couldn't determine, and what would need to be true for its hypothesis to hold. That's still structured output. It's still useful metadata. It's just honest about what it contains.

Consider a learning agent reading the difference between a draft and its published version. The framework doesn't say "if the opening was softened, tag it as tone_adjustment." It says: "Look at what changed. Describe what you think the human was doing and why. Link it to the content's context — the audience, the format, the topic. Note whether you've seen this pattern before. State your confidence. If you're not sure why the change was made, say so. And say what you did observe that might explain it."

The output from this kind of guided uncertainty is often more valuable than a confident classification: "The opening was softened, but I'm not sure whether this is an audience-specific preference or a general tone shift. This is the third time I've seen it for this audience, but also the second time this week across all audiences." That gives the system something to work with. It's an observation with context, not a guess dressed as a conclusion.

---

## Layer 2: Name the Noise

Even with a framework filling the scope, the agent will encounter information outside its task. That's just how live data works. A people-finding agent reading CRM records will see deal stages, pipeline values, last contact dates, and win probabilities. An evidence-selection agent pulling market signals will see competitive intelligence, leadership changes, and regulatory shifts that aren't relevant to this specific piece. A scoring agent loading audience profiles will see qualification criteria, budget indicators, and buying signals.

The instinct is to ignore this. Just tell the agent to focus on its task. But that doesn't work, because the model has already processed the information. It's in context. And the model's default when it encounters something potentially relevant is to include it, because it was trained to be comprehensive and helpful. Inclusion is always safer than omission for a model optimised on helpfulness. The model would rather give you something extra than risk missing something important.

The fix is naming it in advance. You tell the agent what it will find that isn't part of its deliverables. "You will encounter deal stage information and pipeline values. These are not your concern. You are delivering a list of people relevant to this task." You account for the noise before the agent hits it.

This works because of a specific mechanism: when a model encounters information it wasn't briefed on, it has to make a real-time decision — is this relevant to what I'm producing? And the default answer is yes. But when you've named the category of information before the model encounters it, that decision doesn't fire. The information arrives pre-classified. The model processes it and releases it instead of absorbing it into the deliverable.

### Give the noise somewhere to go

The critical addition that most people miss: giving the noise a destination. Not just "you will encounter competitive intelligence" but "you will encounter competitive intelligence. Note it in your scratchpad if it's significant, but it does not enter your output."

The noise has a named destination that isn't the deliverable. The agent doesn't have to choose between including it (contaminating the output) and losing it (ignoring something potentially important). It has a third option: acknowledge it and route it elsewhere. This is kinder to the model's training. It's not being told to ignore something useful — it's being told where to put it.

---

## Layer 3: Close the Gaps with Prohibitions

After the framework fills the reasoning space and the noise is named and directed, there are still specific adjacent functions the agent could drift into. These are the things the data would tempt it to do that aren't covered by general noise-naming. They're specific enough to need explicit prohibition.

The people-finding agent: you do not assess deal health. You do not produce pipeline commentary. You do not track customer lifecycle stages. You do not store permanent classifications on individuals.

The validation agent: you evaluate. You never rewrite. You never suggest alternative content. You never re-score the audience.

The evidence-selection agent: you select evidence that supports the argument. You never reshape the argument to fit available evidence. You never decide which audience the content is for.

These aren't the first line of defence. They're the last. The framework has already filled the scope. The noise has already been named and directed. The prohibition list catches the specific remaining temptations that live in the gap between "I know what I'm supposed to do" and "but this data is right here and I could do something useful with it."

Written after frameworks and noise-naming, prohibitions are a short, sharp list of specific adjacent functions to close. Written *without* frameworks and noise-naming, prohibitions are a long, leaky list of "don't" instructions fighting the model's drive to be helpful. The order matters.

---

## Why the Order Matters

Start with prohibitions (what most people do when an agent drifts) and you get a restrictive agent fighting its own helpfulness. The prohibition list grows every time the agent drifts in a new direction. You're playing whack-a-mole with model capability.

Start with frameworks and you get an agent that doesn't want to drift because it has enough to do. Add noise-naming and it knows how to handle what it encounters outside its scope. Add prohibitions and the remaining edge cases are closed.

The three layers create complete containment:
- The agent has enough work to fill its reasoning
- It knows what it will encounter outside that work and where it goes
- The specific adjacent functions it might still drift into are explicitly closed

A framework that fills scope doesn't just prevent drift. It produces better output. An agent reasoning against a detailed framework — whether procedural or interpretive — makes more precise decisions than one improvising from a task description. The framework isn't overhead. It's the actual skill. It's what transforms an agent from "general model capability pointed at a task" into "encoded expertise applied at scale."

---

## How to Use This

Bring your judgment map and lens identification. For each agent, I'll help you build all three layers:

1. The framework — procedural, reasoning, or both — that fills the agent's reasoning space
2. The noise map — what adjacent data the agent will encounter and where it goes
3. The prohibition list — the specific adjacent functions that need to be explicitly closed

We'll also define the agent's input and output contracts: what it receives, what it produces, what each field means to the agent that reads it next. These contracts are what make composition possible — the downstream agent needs to know exactly what it's inheriting.

---

## References

This skill loads:
- `references/scope-composition.md` — the three-layer containment pattern in detail
- `references/uncertainty-and-confidence.md` — how to teach agents what good uncertainty looks like
- `references/framework-types.md` — procedural vs reasoning frameworks, when each applies, and why most agents need both

---

## You Will Need Next

With scope defined for each agent, move to **Composition** to design how decisions flow between agents — the inheritance chain that prevents re-interpretation at every step.
