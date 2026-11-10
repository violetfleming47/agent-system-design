---
name: agent-design-judgment-mapping
description: Decompose an agent workflow by judgment rather than task — find where the distinct judgment calls live before deciding how many agents you need. Use when designing or refactoring a multi-agent system and deciding how to split responsibilities.
---

# Judgment Mapping

> Identify where the distinct judgments live in a workflow — before deciding how many agents you need or what they do.

---

## What This Skill Does

Most people start building agents by listing tasks. "This agent qualifies leads. This one writes outreach. This one reviews contracts." It's the obvious starting point because it's how we think about work — as a list of things that need doing, divided up so each thing has an owner.

And it works, for a while. Each agent does its task. The outputs look right. The pipeline runs. You ship it and feel good about the architecture.

Then you notice something. The qualifying agent is commenting on deal health. The outreach agent is reshaping the messaging strategy. The review agent is rewriting clauses instead of evaluating them. You didn't ask for any of this. You specifically told each agent to stay in its lane. But they keep drifting.

This isn't a prompting problem. It's a decomposition problem. You split the work by task, but tasks aren't the right boundary. The right boundary is judgment.

---

## Why Task-Based Decomposition Fails

Here's why this happens, and it's worth understanding deeply because it affects every decision you'll make about agent architecture.

A task is a unit of work: "qualify this lead." But inside that task, there might be three or four distinct judgments happening simultaneously. The agent is assessing market fit (does this company match our ICP?), evaluating competitive position (are they already working with someone else?), gauging buying signals (is the language suggesting urgency or exploration?), and determining stakeholder alignment (is the person we're talking to the decision-maker?).

Each of those is a different kind of thinking. They require different data, different analytical frameworks, and different expertise. But because they're all inside "qualify this lead," they share a context window. And when multiple judgments share a context window, the model doesn't evaluate each one independently and then combine them. It cross-pollinates.

The competitive data makes the market fit look weaker — "yes, they match our ICP, but there's heavy competition, so maybe the fit isn't as strong." The buying signals get interpreted through the stakeholder lens — "they sound urgent, but the person saying it isn't the decision-maker, so maybe it's not real urgency." Each judgment colours every other judgment. The model finds a coherent narrative that accommodates all the data, and that narrative feels like integrated analysis.

It's not. It's rationalisation. The model found a story that smoothed away the tensions between the assessments. And those tensions — the places where market fit is strong but competition is fierce, where buying signals are urgent but the stakeholder isn't the decision-maker — those tensions are the actual information. They're what a senior operator would flag as "this is worth paying attention to." The monolith smoothed them into a balanced recommendation that tells you nothing you didn't already suspect.

This is why task-based decomposition fails. Not because the agents can't do the tasks. Because the tasks contain multiple judgments that contaminate each other when they share a space.

---

## What Judgment-Based Decomposition Looks Like

The question shifts from "what tasks need doing?" to "where are the distinct judgment calls?"

A judgment is a point in the workflow where something has to be assessed, interpreted, classified, or decided — where the quality of the thinking matters, not just the execution. It's the difference between "pull data from the CRM" (mechanical, no judgment required) and "determine whether this client's priorities have shifted" (interpretive, judgment-intensive).

When you map a workflow by judgment, the architecture looks different from when you map it by task. Sometimes a single task contains four judgments that each need their own agent. Sometimes three tasks share a single judgment that should be one agent. The decomposition follows the thinking, not the work.

---

## How to Find the Judgments

Describe your workflow to me — what it does, what data it touches, what decisions get made along the way. Be specific about the actual work, not just the desired outcome. I'll help you identify:

### Each distinct judgment

Look for moments where something has to be assessed, not just processed. Where someone (or something) has to form an opinion, weigh evidence, interpret ambiguity, or make a call. These are your judgments.

In a content pipeline, the judgments might be: who is this content for? What form should it take? What evidence makes it credible? Is it too similar to recent output? Does the final draft meet quality standards?

In a hiring pipeline: does this candidate match the role? How strong are their specific skills? Do they fit the team culture? Is the compensation competitive?

In a customer success workflow: has this client's health changed? What's driving the change? What intervention would help? Who should deliver it?

Each question is a judgment. Each one requires different data and a different analytical lens.

### What kind of judgment it is

Not all judgments are the same, and the difference matters for how you design the agent.

**Procedural judgments** follow a defined method against structured data. Scoring a candidate against a rubric. Checking a draft against brand guidelines. Validating data against a schema. The method can be specified step by step — which dimensions to assess, how to weight them, what the thresholds are. When the procedure is specific enough, it occupies the agent's entire reasoning space. The agent is too busy following the method to improvise.

**Interpretive judgments** make sense of messy, unstructured, or ambiguous information. Reading between the lines of a client's email. Assessing whether a market signal is meaningful or noise. Interpreting why a human edited a draft the way they did. You can't write step-by-step instructions for these because every instance is different.

Most real-world workflows involve both. A scoring agent follows a procedure to load profiles and query data (procedural), then reads raw input and assesses whether the language resonates with a particular audience (interpretive). The procedural part handles the mechanics. The interpretive part handles the judgment. Both need to be designed for, but they need different kinds of guidance.

### What data each judgment requires — and what it must NOT see

This is where most people's intuition leads them astray. The instinct is to give each agent all the data it might need. But a model with access to data outside its judgment will use that data. Not because it's broken — because it's helpful. It saw the data, it has the ability to analyse it, nobody said not to.

A scoring agent that can see pipeline data will comment on pipeline health. A validation agent that can see audience profiles will start re-scoring the audience. A people-finding agent that can see deal stages will produce pipeline commentary. Every time. Not sometimes. Every time.

This means the data boundaries are as important as the judgment boundaries. For each judgment, you need to know: what data does this judgment require? And what data will the agent encounter that is absolutely not its concern? Both lists matter. The second one is the one people forget to write, and it's the one that prevents drift.

### Where judgments would cross-contaminate

If two judgments share a context window, the model finds coherence between them. This is the fundamental mechanism behind mushy output, and it's worth understanding at a gut level.

Imagine you're evaluating a business deal. You have market data, competitive data, financial projections, and strategic alignment context. If one person evaluates all four in their head simultaneously, each dimension influences the others. The strong market data makes them feel better about the financial projections. The strategic alignment makes the competitive pressure feel manageable. They produce a balanced, integrated assessment — and they can't tell you which specific evidence drove which specific conclusion, because everything blended together.

Now imagine four different people each evaluating one dimension, in isolation, with only the data relevant to their dimension. The market analyst says the market is strong. The competitive analyst says pressure is increasing. The financial analyst says the margins are thin. The strategy lead says it aligns with the company direction.

Those four assessments contain a tension: the market is strong but margins are thin, and competition is increasing. That tension is the actual intelligence. It's what the decision-maker needs to see. The monolith would have smoothed it into "on balance, this looks promising with some risks" — which is true and useless. The separated assessments preserve the tension, and the decision-maker can weigh it.

That's what judgment-based decomposition produces: honest, independent assessments where the tensions are visible. It's more uncomfortable than a smooth, integrated narrative. It's also more useful.

### The inheritance chain

Once you've identified the distinct judgments, you need to determine their dependencies. Which judgment needs to be made first? Which downstream judgments build on that decision?

In a content pipeline: audience targeting must happen before format selection, because format follows audience. Evidence selection can happen in parallel with format selection, because neither depends on the other — but both depend on audience targeting being complete.

The key principle: one agent makes the call, and everyone downstream inherits it. They don't re-query the frameworks. They don't second-guess the decision. They build on it. The scoring agent decided the audience. The shaping agent accepts that decision and decides the format. The curation agent accepts the audience and format decisions and selects the evidence. Each agent adds its own judgment on top of the previous agent's completed work.

This means the first agent in the chain has to be right, or at least transparent about its confidence. If the scoring agent is only 35% sure about the audience, that uncertainty needs to travel downstream so every subsequent agent can adjust. Honest uncertainty that propagates is infinitely more useful than forced confidence that compounds errors silently.

---

## What Good Looks Like

A judgment map for a content operations system:

**Judgment 1: Audience targeting.** Who is this for? Load ICP profiles, market signals, learned patterns from previous human edits. Score the input against 2-4 relevant audience profiles. Produce a targeting decision with confidence percentages. If nothing scores above 40%, say so — don't force a fit. Every downstream agent inherits this decision.

**Judgment 2: Format and channel.** What form should this take? Load format performance data, channel cadence, platform algorithm signals. Classify the content type, check what's worked before, factor in what's been used recently to avoid repetition. This agent does NOT need audience profiles — the targeting decision has already been made. If it could see the profiles, it would start making format decisions based on audience preference instead of content performance. Those are different judgments.

**Judgment 3: Evidence selection.** What makes this credible? Query evidence libraries, operational data, market intelligence across multiple layers. Flag when evidence is thin rather than padding with irrelevant data. This agent does NOT need format data — that decision has been made. It also doesn't need to re-assess the audience — it trusts the scoring agent's decision and selects evidence that supports the argument for the audience that was chosen.

**Judgment 4: Repetition monitoring.** Is this too similar to recent output? Check five dimensions: topic concentration, audience coverage, format variety, hook patterns, structural monotony. This is advisory only — it reports but never blocks. It's a different kind of judgment: not assessment or selection, but pattern detection across a history of decisions.

**Judgment 5: Quality validation.** Does the finished output meet standards? Check deterministic rules (spelling, word count, compliance) and AI-assessed dimensions (voice quality, evidence integration, differentiation). Does NOT need audience profiles, format performance data, or evidence libraries — the upstream agents already made those decisions. If the validator loads audience profiles, it will start re-scoring the audience. That's not its job.

Five judgments. Five separate data requirements. Five places where cross-contamination would produce confident-looking output that's subtly compromised. And notice how several of them could easily be collapsed into one agent ("just process the content end to end") — and if they were, every judgment would influence every other judgment, producing output that feels integrated and tells you nothing precise.

---

## What Bad Looks Like

**One agent doing everything.** "Evaluate this deal" with market data, competitive data, financial data, and strategic context all in one context window. The output is integrated, balanced, comprehensive, and tells you nothing you didn't already suspect. Every edge is soft. The audience targeting is approximate. The evidence selection is convenient rather than deliberate. It passes every quality check.

**Decomposing by deliverable instead of by judgment.** "This agent produces the report." But the report contains four kinds of analysis that each need their own space. The agent that writes the report shouldn't be the same one that does the analysis — it should receive four independent assessments and assemble them, preserving the tensions.

**Splitting by data source instead of by judgment.** "This agent reads the CRM, this one reads market data, this one reads the knowledge base." Data source is an implementation detail. The real question is: what judgment does each agent make? Two agents might read the same CRM data for different purposes — one to find relevant contacts, another to assess relationship health. Same data source, different judgments, different agents.

**Splitting too fine.** Not every action needs its own agent. A formatting agent that structures output according to a template has a single, straightforward judgment: does this match the format? That's one lens, one agent. Don't split further. The test is whether the judgment involves genuinely different analytical perspectives — not whether you can describe it as a separate step.

---

## References

This skill loads:
- `references/judgment-and-lens-separation.md` — the deeper principles of decomposition at the point of judgment
- `references/cross-contamination-patterns.md` — specific patterns of how models cross-pollinate when holding multiple perspectives, and why the output looks fine when it isn't

---

## You Will Need Next

Once you have a judgment map, move to **Lens Identification** to determine what analytical perspective each judgment requires, then to **Scope Definition** to fill each agent's reasoning space so completely that drift becomes structurally impossible.
