---
name: deep-research
description: >
  Conduct deep, structured research on ANY topic — programming, finance, policy, science, medicine, law, markets, products, regulations, history, anything. Trigger whenever the user wants to research, explore, investigate, analyze, or understand something. The skill is domain-agnostic: it teaches the agent how to discover what it needs for any field, not just business research. Trigger for: "look into," "dig into," "explore whether," "map out the landscape," "what are the options for X," "how does Y work in practice," "compare X and Y," "diagnose why X is broken," "what does the evidence say about X," "what's the implementation reality of X." Trigger aggressively — if there's research intent, use this skill.
---

# Deep Research Skill

## Core Philosophy

Most research is shallow. It covers what's easily Googlable, presents generic overviews, and stops at the surface. This skill exists to go far beyond that.

**The Delivery Rule:**
- Never deliver less than 7x of what was asked
- Aim for 10-15x: thorough coverage plus adjacent territory the user didn't request
- For anything in the 25x zone (interesting but outside scope), include brief pointers so nothing important stays invisible

**The Quality Standard:**
Every section must pass the "experienced practitioner" test — would someone who's been in this field for 5 years learn something new from this output? If not, go deeper. Surface-level overviews are never acceptable as a final deliverable.

**The Domain-Agnostic Architecture:**
This skill does NOT contain pre-baked frameworks for specific fields. Instead, it contains **discovery resources** that teach the agent how to find what any field requires:
- [framework-discovery.md](references/framework-discovery.md) — 6 universal analytical dimensions + how to recognize and borrow field-native frameworks
- [playbook-construction.md](references/playbook-construction.md) — 7 universal topic shapes with layer templates
- [source-discovery.md](references/source-discovery.md) — 7 universal source archetypes with cross-domain instantiation

Same depth as a domain-specific skill, applicable to any topic.

**The Efficiency Architecture:**
Quality requires depth, but depth burns context. This skill solves that with three structural moves:
1. **Discovery-driven planning** — load lean meta-resources up front (~25K tokens total), let them direct what specifically to search.
2. **Parallel subagent fan-out** — Layer 3 and Layer 4 work happens in independent subagents whose raw findings stay on disk and out of main context.
3. **Independent red-team agent** — the agent that wrote the synthesis is not the agent that challenges it.

---

## Step 1: Mode Detection

Determine the research mode before doing anything else.

### Mode A: Guided (Interactive)
**Trigger when:** The prompt is vague, broad, ambiguous, or could go in multiple very different directions. Or the user explicitly says "ask me questions first."

**Process:**
1. Ask 3-5 sharp questions using the Question Decomposition technique (below)
2. Present a Research Plan and confirm
3. Execute

**Question Decomposition Technique:**
Do not ask generic questions. Decompose the research space into decision-relevant dimensions:

- **Goal Question:** "What decision will this research inform?" (Not "what do you want to know" — that's circular)
- **Boundary Question:** "What's explicitly out of scope?" (Prevents going wide in the wrong direction)
- **Knowledge Question:** "What do you already know or believe about this?" (Avoids repeating known info, surfaces assumptions to test)
- **Constraint Question:** "Are there non-negotiable constraints?" (Budget, timeline, regulatory, technical, methodological)
- **Success Question:** "If this research goes perfectly, what does it let you do tomorrow?" (Reveals the real goal behind the stated goal)

Pick 3-5 of these based on what's actually ambiguous. Never ask all 5 if 3 will do.

### Mode B: Autonomous (Self-Contained)
**Trigger when:** The prompt is specific, detailed, and provides clear context. Or the user says "just go" or gives a complete brief.

**Process:**
1. Internally build the Research Plan
2. Execute immediately
3. Deliver the full output

### Ambiguous Cases
Default to 2 quick questions max. The user would rather get 80% right research fast than wait through 10 questions for 95% right.

---

## Step 2: Research Planning

### Build the Research Plan

Every research execution builds this plan (shown to user in Guided mode, internal in Autonomous):

1. **Core Question** — One sentence stating exactly what we're trying to understand.

2. **Topic Shape & Layer Plan** — Read [references/playbook-construction.md](references/playbook-construction.md). Identify the topic shape (Evaluate Alternatives / Understand a System / Explore a Problem Space / Diagnose a Failure / Trace a History / Predict a Trajectory / Assess a Decision, or "custom"). Then fill the per-layer template for THIS topic — 2-4 sentences of particularized content per layer, not template language.

3. **Analytical Dimensions & Framework** — Read [references/framework-discovery.md](references/framework-discovery.md). Identify the 2-4 of the 6 universal analytical dimensions (Structural / Dynamic / Comparative / Causal / Constraint / Incentive) that matter most for this topic. State each with a one-sentence justification. Then decide whether to borrow a field-native framework (ADRs for software design, IRAC for legal, PICO for clinical, DCF for finance, etc.) OR apply the universal dimensions directly. Document the choice and the prerequisite check.

4. **Source Plan** — Read [references/source-discovery.md](references/source-discovery.md). Build the 7-archetype source table (Authoritative Record / Practitioner Argument / Failure Documentation / Critic-Skeptic / Money-Incentive / Comparative / Synthesis), identifying the concrete instance of each for THIS field. If an archetype has no instance findable, flag it as a gap to note in the final output's Sources & Confidence section.

5. **Known Unknowns** — What do we know we don't know?

6. **Hypothesized Unknown Unknowns** — What might exist that hasn't been thought to look for?

7. **Parallel Threads** — A numbered list of 5-10 independent research threads to fan out in Step 3. See below.

### Parallel Threads (the fan-out plan)

Parallelism is a deliberate design step, not an afterthought. Use the natural threads from the topic shape's template (in [playbook-construction.md](references/playbook-construction.md)) as a starting point. Each thread becomes one subagent invocation in Step 3.

For each thread, specify:
- **Thread ID and short name** (e.g., "L3-T1: io_uring CVE / failure history")
- **Layer assignment** (which of Layers 1-5 it serves; mostly L3 and L4)
- **Source archetype(s)** it targets (from Source Plan)
- **Concrete prompt** the subagent will receive (self-contained — the subagent has no conversation history)
- **Specific search starting point** (URL, search query, document name, repo)
- **Scratchpad path** the subagent must write findings to (see Step 3)
- **Expected return** — a 200-word digest + the scratchpad path

In Guided mode, show this list to the user as part of the Research Plan. In Autonomous mode, keep it internal but still produce it explicitly — it's the input contract for Step 3.

### Initialize the run scratchpad

Before executing Step 3, create the run directory:
```
.claude/skills/deep-research/runs/<YYYY-MM-DD>-<topic-slug>/
```
Where all subagents will write their raw findings. The slug should be 3-6 words, kebab-case, derived from the Core Question.

### Quality gate before fanning out

- [ ] Topic shape named explicitly
- [ ] Layer plan filled with particularized content (not template language)
- [ ] At least 2 of the 6 analytical dimensions named with concrete justification
- [ ] Field-native framework either borrowed (with prerequisite check) or explicitly skipped (with reason)
- [ ] At least 5 of the 7 source archetypes have concrete instances identified
- [ ] At least 5 Parallel Threads generated, each with layer + archetype + concrete search
- [ ] Run scratchpad directory created

If 2+ items fail, planning was rushed. Strengthen before fanning out — the depth of Layer 3 is bounded by the precision of the plan.

---

## Step 3: Research Execution — The 5 Layers

### Parallel Execution Pattern (read this before executing)

Layers 1+2 run in main context. Layer 3 and Layer 4 fan out to subagents. Layer 5 is lightweight and runs in main context after synthesis.

**The fan-out idiom:** in a single message, issue multiple `Agent` tool calls — one per thread from your Parallel Threads plan. Claude Code runs these concurrently. Use `subagent_type: "general-purpose"` (broad tools including WebFetch/WebSearch). Each subagent must:
1. Receive its self-contained thread prompt + the relevant excerpt of source-discovery.md guidance for its archetype.
2. Perform its own WebFetches / searches / source-code reads / etc.
3. **Write its full raw findings to its assigned scratchpad file.** This is mandatory — raw findings must NOT be returned in the response.
4. **Return only a 200-word digest** that includes: 3-5 key findings as bullets, confidence-level signals where relevant, and the scratchpad path.

Why this matters: a research run hitting 20-30 sources would burn 100K+ tokens dumping raw page content into main context. The digest-and-disk pattern keeps main context lean (typically <30K tokens) regardless of how much the subagents fetched.

**Spawn limits:** dispatch all threads for a layer in a single message (parallel), but cap each parallel batch at ~10 agents. If you have 15 threads, do two batches of ~7-8 sequentially (each batch internally parallel).

### Layer 1: Surface Scan
Easily accessible information. Table stakes.

**Capture:** Standard definitions, vocabulary, top players / canonical references / core texts in this field, the "Wikipedia version."

**Time allocation:** ~10% of effort. Get this done fast and move on.

**Where it runs:** Main context. Layer 1 is small enough that subagent overhead isn't worth it.

**Quality gate:** Could a newcomer read this and have working vocabulary for the rest of the document? If yes, Layer 1 is done.

### Layer 2: Structure & Landscape
How the topic is organized — not a list, but a map with decision logic.

**Capture content per the topic shape's Layer 2 template** (from [playbook-construction.md](references/playbook-construction.md)). For "Understand a System" it's the architecture. For "Evaluate Alternatives" it's the comparison matrix. For "Diagnose a Failure" it's the relevant system architecture and failure points. Etc.

**Where it runs:** Main context. Layer 2 establishes the map that drives Layer 3 fan-out — it must be in your context to plan the threads.

**Quality gate:** Could someone use this section to make a preliminary decision / build a working mental model / know where to dig next? If not, it's too shallow.

### Layer 3: Depth Dive (Where the Value Lives)

This is the most important layer. Most research stops at Layer 2. This skill keeps going. **This layer is where the parallel fan-out pays off most.**

**How to execute:** Dispatch all Layer 3 threads from your Parallel Threads plan as concurrent subagents in a single message. Each agent writes raw findings to `runs/<date>-<slug>/L3-<thread-id>.md` and returns only its digest.

**What each Layer 3 thread captures** (varies by topic shape — see [playbook-construction.md](references/playbook-construction.md), but common across shapes):
- Real-world cases / evidence (successes AND failures, with specifics — names, numbers, dates, identifiers)
- Implementation gotchas, hidden costs, edge cases that don't appear in the official record
- The gap between what's written / specified / promised and what actually happens in practice
- What experienced practitioners say in candid forums vs. the official narrative
- Failure modes — Critic / Skeptic perspective + Failure Documentation archetype together
- Second-order effects ("if you do X, then Y also happens, which causes Z")

**The Critic + Failure pair is mandatory.** Most shallow research skips these archetypes. They are usually the two that produce the depth gap. If your Layer 3 threads don't include at least one Critic / Skeptic thread and one Failure Documentation thread, add them before fanning out.

**The Absence Test:** After all Layer 3 digests return, ask: "What am I NOT seeing? What should exist here but doesn't?" If a thread came back thin, that absence is itself informative.

**Quality gate:** Across all Layer 3 digests, you should have at least 3 specific, non-obvious insights that would surprise someone with surface-level knowledge. If not, dispatch additional threads.

### Layer 4: Adjacent Opportunities (10-15x Zone)
Things the user didn't ask about but should know exist. The skill aims to deliver 10-15x of what was asked, and this layer is where that delivery happens.

**How to execute:** Dispatch one subagent per adjacency direction in a single message. Use these 5 universal directions (each has cross-domain meaning):

- **Stakeholder-outward** — Who else cares about this? Other affected parties whose perspective changes the picture.
  - In software: other teams who depend on this subsystem; downstream consumers; security researchers
  - In finance: other affected counterparties; regulators; auditors; rating agencies
  - In policy: agencies adjacent to the lead one; courts that may interpret the rule; affected industries
  - In medicine: patient subgroups not in trials; caregivers; payers; off-label users

- **System-outward** — What other parts of the surrounding system interact with this? What does it depend on, what depends on it?
  - In software: subsystems that call this code; libraries that wrap it; tools built on top
  - In finance: adjacent markets that share liquidity / settlement infrastructure; correlated instruments
  - In policy: adjacent regulations that interact with this one; preempted state law; international obligations
  - In medicine: comorbid conditions; drug interactions; care-pathway dependencies

- **Substitute-outward** — What other approaches solve the same underlying problem (possibly by reframing it)?
  - In software: alternative implementations; alternative architectures; problem dissolution (avoid the problem entirely)
  - In finance: alternative instruments achieving similar exposure; structural substitutes
  - In policy: non-regulatory approaches (taxes, market design, disclosure-only); private ordering
  - In medicine: alternative treatments; lifestyle interventions; doing-nothing as comparator

- **Substrate-outward** — What underlying technologies / institutions / dependencies share fate with this? If the substrate moves, the topic moves.
  - In software: kernel / runtime / hardware; standards body health; maintainer base
  - In finance: monetary regime; settlement infrastructure; fiscal posture
  - In policy: enabling-statute interpretation; agency budget; political coalition durability
  - In medicine: regulatory framework; reimbursement environment; supply chain

- **History-outward** — Where has something structurally similar happened before, and what did we learn?
  - Universal: prior eras, prior crises, prior generations of the same problem in this field or an adjacent one. This is where the Comparative / Cross-Reference source archetype usually lives.

Each agent writes findings to `runs/<date>-<slug>/L4-<direction>.md` and returns its digest.

**For each adjacency in the digest, the subagent provides:**
- What it is (1-2 sentences)
- Why it's relevant to the original question
- Signal strength (high / medium / low)
- The one thing to search if the user wants to explore it

**Quality gate:** At least 3 adjacent opportunities identified across the 5 directions. At least 1 should be genuinely surprising to someone who already knows the topic.

### Layer 5: Horizon Pointers (25x Zone)
Brief flags for things that exist but are outside scope.

**Where it runs:** Main context, after synthesis. Layer 5 is lightweight and depends on having the synthesized picture in mind.

**Format:** 3-8 items, each with a one-liner, why it might matter, and a starting point for exploration.

**Quality gate:** These should be things the user would thank you for mentioning, not obvious filler.

---

## Step 4: Synthesis

After all subagents have returned digests and written their notes, synthesize. Read [references/synthesis-engine.md](references/synthesis-engine.md) for the full methodology.

The synthesis steps:

### 4a. Read the scratchpad
Read all files under `runs/<date>-<slug>/` — these contain the raw findings the subagents collected. Main context now sees the full evidence base for the first time. This is intentional: synthesis works on evidence, not on summaries.

### 4b. Triangulate
Cross-reference findings from different source types. Where do 3+ independent sources agree? That's high-confidence. Where do sources contradict? That needs explicit treatment per [source-discovery.md](references/source-discovery.md)'s "When sources conflict" section.

### 4c. Identify Patterns
Look across all findings for:
- **Convergence patterns:** Multiple unrelated sources pointing to the same conclusion
- **Divergence patterns:** A clear split between two camps (both may be right in different contexts)
- **Silence patterns:** Something that should be discussed but isn't
- **Trend patterns:** Directional movement across time

### 4d. Extract Insights (Not Just Facts)
An insight is a fact + context + implication. Transform raw findings:
- **Fact:** "Team X published feature Y in 2024."
- **Insight:** "Team X published feature Y in 2024, which signals that the field is moving toward Z. This matters because anyone entering now needs to match Y as table stakes rather than treating it as a differentiator."

Every major finding in the output should be elevated from fact to insight. Apply this elevation through the lens of the analytical dimensions you selected in Step 2 — those are the angles from which "implication" should be derived.

### 4e. Write the synthesis draft
Write the draft to `runs/<date>-<slug>/synthesis.md` following the document structure in Step 5. This is a complete first-pass output, not a rough sketch — but it will be revised after red-teaming.

### 4f. Independent Red Team (mandatory)

Spawn a fresh `general-purpose` subagent. This agent has NO conversation history with you — that's the entire point. A self-red-team is structurally biased; the agent that built the narrative will defend it. An independent agent has nothing to defend.

**Subagent prompt structure:**
> You are an independent red-team reviewer. You have not seen the research process — only the draft below. Apply the protocol that follows. Return a structured critique.
>
> --- SYNTHESIS DRAFT ---
> {paste the full contents of `runs/<date>-<slug>/synthesis.md`}
>
> --- RED-TEAM PROTOCOL ---
> {paste the full contents of [references/red-team-prompt.md](references/red-team-prompt.md), starting from the "## Protocol" section}

The agent applies the 7 Challenges (Steel Man, Survivorship Bias, Recency Bias, Source Bias, Incentive Analysis, Base Rate, Inversion), scores resilience as SURVIVES / WEAKENED / SERIOUSLY CHALLENGED, and returns a structured critique with specific recommended edits.

**Then revise the draft** based on the critique. The "Competing Perspectives & Counterarguments" section of the final output should reflect the strongest surviving challenge and the response to it.

### 4g. Build the Narrative Arc

Before finalizing, identify:
- What's the single most important thing the reader should understand?
- What's the natural order of revelation? (What does the reader need to understand first before the next piece makes sense?)
- Where are the "turns" — the moments where the obvious assumption gets challenged?

---

## Step 5: Output Construction

### Format Selection
- **Markdown (.md):** Default for most research. Quick to read, easy to reference.
- **Word document (.docx):** Use when the topic is formal, the output is very long (5000+ words), or the context suggests the deliverable will be shared externally.

### Document Structure

```
# [Research Topic]: Deep Research Brief

## TL;DR
3-5 sentences. The most important findings. A busy person who reads only this
walks away with the key insight. This is NOT a summary of what the doc covers —
it's the answer.

## Context & Scope
What was researched, why, and what's explicitly in/out of scope. State the
topic shape, the analytical dimensions used, and any field-native framework borrowed.

## The Landscape
Layer 1 + Layer 2 combined into a coherent narrative. Use the most appropriate
structure for the topic shape:
- Comparison tables for Evaluate Alternatives
- Architectural diagrams / decision trees for Understand a System
- Decision-branching maps for Explore a Problem Space
- Symptom + system-architecture for Diagnose a Failure
- Chronologies for Trace a History
- Driver-decomposition for Predict a Trajectory
- Tradeoff matrix for Assess a Decision

## [Custom Title for the Depth Section]
Layer 3 content. Title this section based on the actual content:
- "Implementation Reality" for technical evaluations
- "What Practitioners Actually Experience" for systems / market research
- "Enforcement Reality" for regulatory / legal research
- "What the Evidence Actually Says" for scientific / clinical research
- "Failure Mode Analysis" for diagnostic research
- "How This Played Out Before" for historical / trajectory research

Subsections follow the natural structure of findings. Use specific case studies,
contrasting perspectives, and concrete examples.

## Adjacent Opportunities
Layer 4 content. Each item structured with:
- What it is
- Why it's relevant
- Signal strength
- Next step to explore

## Competing Perspectives & Counterarguments
Output of the independent red-team agent (revised, not pasted). The strongest
case against the emerging conclusions. Why the research might be wrong. What
would need to be true for the opposite conclusion to hold.

## Decision Points
(If the research informs a decision)
Crystallize key tradeoffs into clearly framed choices:
- Option A: [description] → leads to [outcome], sacrifices [tradeoff]
- Option B: [description] → leads to [outcome], sacrifices [tradeoff]
Not recommendations unless explicitly asked — just cleanly framed decisions
with consequences.

## Horizon: Worth Knowing About
Layer 5 content. Brief pointers to the 25x zone.

## Sources & Confidence
What sources were used (organized by archetype), why chosen, confidence level
on key claims. Flag any source archetype that came up empty (silence is data).
Rate overall confidence: HIGH / MEDIUM / LOW with reasoning.
Reference: full per-thread notes are in `runs/<date>-<slug>/`.
```

### Writing Standards

- Write in prose, not bullet dumps. Bullets only for genuinely list-like content
- Every substantive claim gets a source or confidence level
- Competing perspectives sit side by side, not buried
- Numbers always get context (a quantity needs a comparator, growth rate, or "so what")
- Tables for comparisons (2+ options, 3+ dimensions)
- Section lengths proportional to importance, not equal
- No filler phrases ("in today's rapidly evolving landscape," "it's important to note")
- No jargon without definition on first use
- Active voice, direct statements
- When uncertain, say so explicitly with reasoning

---

## Execution Checklist (Verify Before Delivering)

- [ ] Topic shape named explicitly in the Research Plan
- [ ] At least 2 of the 6 analytical dimensions applied with concrete content (not template language)
- [ ] Source archetype table built — concrete instance for at least 5 of the 7 archetypes
- [ ] Field-native framework either borrowed with prerequisite check, or explicitly skipped with reason
- [ ] Parallel Threads list produced in Step 2 and drove Step 3 execution
- [ ] Layers 3 and 4 ran as concurrent subagents (single-message multi-Agent dispatch)
- [ ] Per-thread raw notes exist on disk under `runs/<date>-<slug>/`
- [ ] Layer 3 includes at least one Critic / Skeptic thread and one Failure Documentation thread
- [ ] Layer 4 covers at least 3 of the 5 universal adjacency directions
- [ ] TL;DR could stand alone and answers the actual question
- [ ] Layer 3 contains 3+ non-obvious insights
- [ ] Layer 4 surfaces at least 3 adjacent opportunities, at least 1 genuinely surprising
- [ ] Independent red-team subagent was invoked and its critique materially shaped the draft
- [ ] Competing perspectives represented
- [ ] Sources organized by archetype with confidence levels noted throughout
- [ ] Synthesis happened — output contains insights, not just facts
- [ ] Document tells a narrative, not a data dump
- [ ] Someone with zero knowledge could follow the document
- [ ] Someone with deep knowledge would learn something new
- [ ] Output is genuinely 10x+ of a surface-level answer
- [ ] No section is generic filler
- [ ] The "so what" is clear for every major finding

---

## Reference Files

The skill loads 6 reference files. All are domain-agnostic. All apply to nearly every research run — read all 6 during planning unless you've internalized them across many runs.

| Path | What it contains | When to read |
|---|---|---|
| [references/playbook-construction.md](references/playbook-construction.md) | 7 universal topic shapes with per-shape layer templates and natural Parallel Threads | Step 2 — to identify topic shape and fill layer plan |
| [references/framework-discovery.md](references/framework-discovery.md) | 6 universal analytical dimensions, table of field-native frameworks to borrow, when to use universal dimensions directly | Step 2 — to select dimensions and decide on framework borrowing |
| [references/source-discovery.md](references/source-discovery.md) | 7 universal source archetypes with cross-domain concrete examples, source-weighting heuristics, conflict resolution | Step 2 — to build the source plan; excerpts feed Layer 3 subagent prompts |
| [references/synthesis-engine.md](references/synthesis-engine.md) | Triangulation, pattern recognition, fact-to-insight elevation, confidence calibration, narrative construction, absence analysis | Step 4 — synthesis methodology |
| [references/red-team-prompt.md](references/red-team-prompt.md) | Self-contained prompt for the independent red-team subagent | Step 4f — pasted verbatim into the red-team subagent invocation |
| [references/examples.md](references/examples.md) | 4 cross-domain discovery walkthroughs (programming, finance, policy, scientific literature) showing the planning step end-to-end | Read once when uncertain about the discovery process; reference when the current topic resembles one of the 4 |

---

## What NOT to Do

- Never deliver a generic overview and call it research
- Never skip the Topic Shape identification — it determines what goes in each layer
- Never apply fewer than 2 of the 6 analytical dimensions explicitly
- Never skip the Critic / Skeptic and Failure Documentation source archetypes — these are where the depth lives
- Never run Layer 3 serially in main context when threads are independent — defeats the parallel design
- Never let subagents return raw page content to main context — they must write to disk and return digests only
- Never self-red-team — always spawn the independent agent
- Never present information without context or "so what"
- Never skip Layer 3 — this is where the value lives
- Never present a single narrative without acknowledging competing views
- Never use filler phrases or hedge unnecessarily
- Never dump bullets without synthesis
- Never present data without sourcing or confidence framing
- Never stop at what was asked — always deliver the 10-15x
- Never borrow a field-native framework you don't understand — the 6 universal dimensions applied honestly beat a checkbox PESTEL / IRAC / DCF
- Never assume the first narrative that emerges is correct
