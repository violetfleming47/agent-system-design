---
name: agent-design-lens-identification
description: Determine the single analytical lens each agent judgment requires (one lens per agent) to stop agents cross-contaminating perspectives. Use after judgment mapping, when assigning a perspective to each agent in a system design.
---

# Lens Identification

> Determine what analytical perspective each judgment requires — because the lens creates the finding, not the other way around.

---

## What This Skill Does

You've mapped the judgments in your workflow. You know where the distinct thinking happens. The next question isn't "what should each agent do?" — that's the task-based thinking creeping back in. The question is: "what perspective does each judgment need to see through?"

This distinction matters more than it sounds like it should. A perspective — a lens — is an analytical viewpoint applied through a specific framework against specific data. A market lens sees market data through market frameworks. A competitive lens sees competitive data through competitive frameworks. Each lens produces an honest, independent assessment that hasn't been contaminated by the others.

When one agent holds multiple lenses, something happens that feels like good analysis but isn't. The model doesn't evaluate each dimension independently and then carefully combine them. It processes everything together, and in processing, it finds connections. The competitive pressure makes the market opportunity feel smaller. The strategic alignment makes the financial risk feel more acceptable. The model weaves a coherent narrative across all perspectives — and coherence across competing perspectives isn't analysis. It's rationalisation.

I keep coming back to this because it's the most counterintuitive principle in agent design. We're trained to think integrated analysis is better. In human cognition, synthesis is a high-order skill. But a model isn't synthesising — it's finding patterns across everything in its context window, and patterns that cross analytical boundaries produce conclusions that feel sophisticated but can't be traced to specific evidence.

---

## Why One Lens Per Agent

Think about how an experienced team works on a major decision. The market analyst doesn't look at the competitive landscape — they look at market data and say what they see. The competitive analyst does the same with their data. The finance lead runs the numbers without worrying about strategic fit. The strategy person assesses alignment without second-guessing the financials.

Then they sit in a room together and present their findings. The market is strong. Competition is increasing. The margins are thin. It aligns with strategy. Those four assessments contain tensions — real, important tensions that the decision-maker needs to see. The market is strong *and* competition is increasing. The margins are thin *but* it aligns with strategy. Those "ands" and "buts" are the information.

If one person had done all four analyses simultaneously, they'd have produced a balanced recommendation. "On balance, this looks promising with manageable risks." Technically true. Practically useless. The tensions got smoothed into a narrative. The decision-maker gets comfort instead of information.

That's exactly what a monolithic agent does. It finds coherence. It produces a balanced view. It smooths the tensions. And the output reads well — it's comprehensive, it's integrated, it addresses every dimension. It just doesn't tell you anything you couldn't have guessed.

One lens per agent preserves the tensions. Each assessment is honest because it was made independently. When you combine them, the conflicts are visible. And the conflicts are where the real decisions live.

---

## How to Identify the Lens

For each judgment in your map, I'll help you determine:

### The analytical perspective

What kind of thinking does this judgment require? Not "what data does it need" — that's implementation. What viewpoint is it applying?

A market perspective evaluates opportunity — size, timing, fit, trajectory. A competitive perspective evaluates positioning — who else is there, how they're different, where you win and lose. A financial perspective evaluates viability — can we make money doing this, at what cost, over what timeframe. A quality perspective evaluates standards — does this meet the bar, where does it fall short, what needs fixing.

Name the perspective. You need to be able to describe what this lens sees and what it deliberately ignores. If you can't describe what it ignores, you haven't defined it clearly enough.

### What data this lens needs

Only the data relevant to this perspective. This sounds obvious, but in practice it's where most people compromise. "Well, the competitive agent should probably see the market data too, just for context." No. If the competitive agent can see market data, it will factor market conditions into its competitive assessment. The competitive assessment is no longer independent. It's been contaminated with a market perspective that belongs to a different agent.

A competitive agent needs competitive data and competitive frameworks. Full stop. The market assessment exists — it was made by the market agent. If the competitive agent needs to account for market conditions, it receives the market agent's *conclusion* (the assessment), not the market *data* (the raw inputs). The conclusion is a clean input. The raw data is an invitation to re-analyse.

### What frameworks this lens applies

Each lens has its own interpretive structure. How does this perspective evaluate what it sees? What dimensions does it assess? What makes something significant through this lens? What's noise?

A quality lens for content might assess: voice consistency, evidence integration, audience alignment, differentiation from recent output. Each dimension has criteria. Each criterion has a threshold. The framework fills the agent's reasoning space with enough specific work that it doesn't wander into territory that belongs to other lenses.

### What this lens explicitly cannot see

This is the critical design decision, and it's where the articles' principle of framework loading comes alive.

A model with a risk assessment framework loaded will find risks. A model with a scoring rubric loaded will produce scores. A model with audience profiles loaded will evaluate audience fit. The analytical lens creates the finding, not the other way around. You don't load a framework and hope the agent uses it wisely. You load a framework and the agent *will* apply it — to everything it can see.

So if you don't want the validation agent evaluating audience fit, don't give it audience profiles. It doesn't have to resist the temptation to over-analyse. The analytical tools simply aren't in the room. The agent can't access a framework it can't misuse.

This is attention control applied at the architectural level. You're not managing the agent's focus with instructions. You're managing it with access. What it can't see, it can't process. What it can't process, it can't misinterpret. The constraint is structural, not aspirational.

### Whether this judgment genuinely needs its own lens

Not everything does, and splitting too fine creates overhead without value.

A formatting agent that structures output according to a template doesn't need perspective separation. The judgment is singular: does this match the format? One lens, one agent, done. A data retrieval step that pulls records from an API doesn't involve judgment at all — it's mechanical processing.

The test is straightforward: does this judgment involve evaluation, assessment, or recommendation? Does it require weighing evidence, interpreting signals, or forming opinions? If yes, check whether multiple perspectives are involved. The moment you identify two perspectives within a single judgment — "this agent evaluates both market fit *and* competitive position" — you've identified two agents.

---

## The Synthesis Layer

When you separate by lens, you create a new problem: how do you bring the assessments back together? This is the synthesis layer, and it is the most commonly misdesigned part of a multi-agent system.

The mistake is building a synthesis agent that re-evaluates everything. You've done all the work of separating perspectives into clean, independent assessments — and then you build a fifth agent that holds all four assessments and produces its own integrated view. Now you have five agents: four with clean perspectives and one monolith that recombines them and reintroduces all the cross-pollination you just eliminated.

The synthesis layer must be architecturally dumb about the domain. It doesn't have analytical frameworks. It doesn't score, assess, or evaluate. It assembles. It takes four independent, honest assessments and presents them together. Including where they conflict.

If Agent A says the market is strong and Agent B says competitive pressure is increasing, the synthesis layer reports both. It doesn't resolve the tension. It surfaces it. It might format it, normalise the structure, strip internal system noise. But it doesn't add its own opinion.

When conflicts need to be resolved before the downstream agent can proceed — because not every tension can be left for the human — the resolution follows explicit precedence rules defined at the architecture level. "If the repetition monitor flags a hook type the format agent recommended, the monitor wins." That rule is defined in advance, not discovered by the synthesis agent at runtime. The synthesis layer applies it mechanically. It doesn't reason about which agent is "more right."

Resolution is either the human's job or a predefined rule's job. Never the synthesis layer's job.

---

## Patterns From Practice

**Content operations.** The scoring agent holds an audience lens — it sees ICP profiles, market signals, learned patterns, and nothing else. The shaping agent holds a format-and-channel lens — it sees performance data, algorithm signals, cadence information. The curation agent holds an evidence lens — it sees evidence libraries, operational data, market intelligence. None of them see each other's data. None of them re-interpret each other's decisions.

The scoring agent decides the audience. The shaping agent decides the packaging. The curation agent decides the evidence. Those are different judgments requiring different perspectives. When they run in parallel after scoring, each reads the scoring output independently. None re-scores the audience. They inherit the decision and build on it.

**Deal evaluation.** Market fit, competitive positioning, financial viability, and strategic alignment are four lenses. Four agents. Each loads its own data and its own framework. The synthesis presents all four assessments with preserved tensions. The deal review committee sees exactly where the assessments agree and where they conflict — and the conflicts are where their judgment is actually needed.

**Risk assessment.** Technical risk, regulatory risk, commercial risk, and operational risk are four lenses. A monolith that holds all four smooths the tensions — the technical risk makes the commercial case look riskier, and the regulatory compliance makes the operational risk look manageable. Separated, each assessment is honest. Combined with tensions visible, the decision-maker can actually weigh the trade-offs instead of reading a narrative that's already made the trade-offs for them.

---

## What Scales and What Doesn't

A monolith with four perspectives is fragile in ways that aren't obvious until you try to change it. Need to update the competitive framework? Everything in the monolith is entangled — the competitive framework interacts with the market data and the financial projections in ways you can't predict. Change one thing and you might destabilise the others.

Lens-separated agents scale linearly. Need to add a fifth perspective? Add a fifth agent. It loads its data, applies its framework, produces its assessment. The other four are completely unaffected. Need to update the competitive framework? Only the competitive agent is affected. Everything else holds.

It also makes the system debuggable. When a monolith produces a questionable recommendation, you can't trace which perspective was biased. When four separate agents produce their assessments, you can trace exactly which lens saw what, which evidence drove which conclusion, and where the judgment might have gone wrong.

And it makes the system evolvable. Learning cycles can operate per-lens. The market agent's judgment improves based on market-specific feedback. The competitive agent improves based on competitive-specific feedback. Each perspective compounds expertise in its own domain without contaminating the others. The market agent gets better at market analysis without that improvement accidentally making the competitive analysis worse.

---

## References

This skill loads:
- `references/judgment-and-lens-separation.md` — the deeper principles behind one lens per agent
- `references/cross-contamination-patterns.md` — specific patterns of how models cross-pollinate perspectives
- `references/synthesis-layer-design.md` — how to combine independent assessments without reintroducing bias

---

## You Will Need Next

With your lenses identified, move to **Scope Definition** to fill each agent's reasoning space — the frameworks, noise-naming, and prohibitions that make each lens airtight. That's where the design moves from "what this agent sees" to "how completely the agent's thinking is guided."
