# Framework Types

> Procedural frameworks handle the mechanics. Reasoning frameworks handle the judgment. Most agents need both.

---

## Procedural Frameworks

A procedural framework specifies method. It tells the agent how to execute a defined process against structured data, step by step.

A scoring agent's procedural framework says:
- Read the input first and form a hypothesis before querying profiles
- Query 2-4 relevant profiles, not all of them
- Score each profile on four dimensions: pain-point alignment, use-case relevance, language resonance, priority match
- Weight dimensions according to defined rules
- Produce confidence as a percentage (0-100)
- If no profile scores above 40%, flag low relevance rather than forcing a fit
- Structure the output with specific fields: primary ICP, secondary ICP, beliefs, pillar alignment, framing direction

When a procedural framework is specific enough, it occupies the agent's entire reasoning space. The agent is too busy following the method to improvise.

Procedural frameworks work when:
- The input is structured or can be structured
- The method can be defined in advance
- Quality is measurable against defined criteria
- The output format is predictable

## Reasoning Frameworks

A reasoning framework guides judgment on messy, unstructured, or ambiguous data. It doesn't specify steps — it provides a structure to think within.

A learning agent's reasoning framework says:
- Look at what changed between the draft and the published version
- Describe what you think the human was doing and why
- Link it to the content's context: audience, format, topic, channel
- Note whether you've seen this pattern before
- State your confidence
- If you're not sure why the change was made, say so — and say what you did observe that might explain it

The framework doesn't dictate the answer. It dictates how to arrive at one — including how to arrive at an honest "I don't know yet."

Reasoning frameworks work when:
- The data is messy, natural language, or inconsistent
- Every instance is different
- Interpretation requires domain judgment
- The output is an assessment, not a calculation

## When Each Goes Wrong

**Over-prescribed reasoning:** Trying to make a reasoning task procedural. The agent forces messy reality into rigid categories, producing metadata that looks clean but misrepresents what happened. A CRM note contains four signals compressed into two sentences — a procedural framework that says "classify as one of these five categories" loses three of them.

**Under-prescribed procedure:** Leaving a procedural task open to interpretation. The agent improvises, applying whatever analytical lens it finds interesting. A scoring agent without a defined method might score on dimensions the system doesn't track, or weight dimensions based on what's most prominent in the current data rather than what the business cares about.

## Most Agents Need Both

A scoring agent follows a procedure to load profiles and query data (procedural). Then it reads raw input and assesses whether the language resonates with a particular audience (interpretive). The procedural framework handles the mechanics. The reasoning framework handles the judgment.

A curation agent follows a procedure to query six evidence layers with specific parameters (procedural). Then it interprets whether a market signal from a busy analyst's notes is genuinely relevant to this piece or just topically adjacent (interpretive).

A validation agent follows a procedure to check spelling, word count, and structural compliance (procedural — these are binary pass/fail). Then it assesses whether the voice quality, integration naturalness, and differentiation from recent output meet the bar (interpretive — these are scored judgments).

Both kinds fill the scope. Both prevent drift. They do it differently, and the agent needs both.

## Framework Loading Rules

Each skill loads the minimum frameworks for its judgment. Everything else is structurally inaccessible.

This is attention control. A model with a risk assessment loaded will find risks. A model with a scoring rubric loaded will produce scores. The analytical lens creates the finding. If a validation agent loads audience profiles, it will evaluate audience fit — even though that's not its job. It sees a framework, it applies a framework.

The fix: don't give it the framework. The agent doesn't have to resist the temptation to over-analyse, because the analytical tools aren't in the room.
