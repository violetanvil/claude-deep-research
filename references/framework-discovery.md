# Framework Discovery

This file teaches the agent how to apply analytical rigor to ANY topic — software internals, monetary policy, drug efficacy, legal doctrine, climate models, anything. It does not list specific frameworks (like PESTEL or SWOT). It teaches the operation those frameworks perform, then shows how to either borrow a field-native framework or apply universal dimensions directly.

The principle: every analytical framework is a **forced multi-perspective check**. PESTEL forces the analyst across 6 macro dimensions; Porter's Five Forces forces 5 competitive angles; JTBD forces customer-job thinking. The frameworks differ. The operation is the same: pick a topic, force yourself to look at it from N pre-specified angles, refuse to skip any.

Without this discipline, analysis collapses into "whatever you happened to think of first." With it, analysis surfaces what you would have missed.

---

## The 6 Universal Analytical Dimensions

These apply to nearly any topic. For your research run, identify which **2-4** matter most and apply them explicitly. The 6-dimension check is the floor — never fewer than 2 actively applied.

### 1. Structural

How is the system organized? What are its parts and how do they fit?

- For software: components, layers, interfaces, data flows
- For markets: segments, value chain, intermediaries, capital flows
- For policy: agencies, statutes, jurisdictions, decision rights
- For science: hypotheses, methods, evidence types, knowledge hierarchy
- For institutions: roles, authority lines, dependencies, gatekeepers

**Forcing question:** "If I had to draw this system on a whiteboard with all its connections, what would I draw?"

### 2. Dynamic (Over Time)

How does it change? What's its history, lifecycle, trajectory?

- For software: version history, deprecation cycles, performance trends
- For markets: cyclicality, secular trends, maturity stage
- For policy: enactment history, amendment trail, sunset clauses, enforcement evolution
- For science: paradigm shifts, replication trajectory, citation half-life
- For institutions: founding intent vs. current behavior, reform attempts

**Forcing question:** "What did this look like 5 years ago, and what will it look like 5 years from now?"

### 3. Comparative

What are the alternatives? What could be substituted? What's the analog elsewhere?

- For software: alternative implementations, other languages' approach, prior generations
- For markets: substitute products, comparable markets in other geographies, asset-class alternatives
- For policy: other jurisdictions' approach, prior policy regimes, comparative case studies
- For science: competing theories, alternative methodologies, contested replications
- For institutions: peer institutions, prior versions, foreign analogs

**Forcing question:** "What's the closest thing to this in a different context, and how does it differ?"

### 4. Causal

What drives what? Where are the root causes, feedback loops, and second-order effects?

- For software: what triggers this code path, what state changes follow, what failure cascades exist
- For markets: what drives prices/flows, what reflexive feedback exists (Soros-style), what creates bubbles or crashes
- For policy: what behavior does this incentivize, what unintended effects appear, what regulatory feedback loops exist
- For science: what causes the observed effect, what mechanisms are proposed, what alternative explanations exist
- For institutions: what drives the institution's actions, what creates path dependency

**Forcing question:** "If I traced this back 3 steps, what's the upstream cause? If I traced it forward 3 steps, what's the downstream effect?"

### 5. Constraint

What limits the system? What are the bottlenecks, hard ceilings, immovable forces?

- For software: hardware limits, latency floors, complexity ceilings, backwards-compat constraints
- For markets: capacity constraints, regulatory caps, capital availability, talent scarcity
- For policy: constitutional limits, budget reality, political feasibility, implementation capacity
- For science: measurement limits, sample size limits, ethical constraints, paradigm boundaries
- For institutions: chartered authority, funding model, founder intent, legal liability

**Forcing question:** "What could we never change about this even if we wanted to? What would have to break for the constraint to lift?"

### 6. Incentive

Who benefits? Who pays? Who'd kill it? Who's invested in keeping it as-is?

- For software: maintainer incentives, vendor interests, contributor base, user lock-in
- For markets: principal-agent dynamics, insider vs. outsider information, conflicting fee structures
- For policy: agency capture, beneficiary coalitions, opposition coalitions, rent-seeking
- For science: funding sources, publication incentives, career incentives, replication disincentives
- For institutions: who controls budget, who selects leadership, who'd lose if it changed

**Forcing question:** "Who would fight hardest to preserve this exactly as it is, and why?"

---

## Step 1: Identify the 2-4 dimensions that matter for THIS topic

Not every dimension is load-bearing for every topic. A research run on "how does the Linux scheduler work" leans heavily on Structural + Dynamic + Constraint. A research run on "should we adopt this open-source library" leans on Comparative + Constraint + Incentive. A research run on "why did this regulation backfire" leans on Causal + Incentive + History.

Pick the 2-4 dominant dimensions. Walk through the topic explicitly under each. Each dimension gets at least one paragraph with concrete content — not "we should consider the structural dimension," but the actual structural analysis.

If you can't generate a paragraph for a dimension, either it's genuinely not relevant (skip it) or you don't know enough yet (mark it as a Known Unknown for Layer 3 fan-out).

---

## Step 2: Decide whether to borrow a field-native framework

Most fields have evolved their own analytical frameworks because they capture domain dimensions cleanly. When one fits your dimensions, **borrow it** — practitioners will recognize the shape and you inherit decades of refinement.

### How to find the field-native framework

Search explicitly:
- "[field] analytical framework"
- "[field] decision framework"
- "how do [field] practitioners structure analysis of [topic-type]"
- "[field] textbook table of contents" (the headings often reveal the field's standard analytical lenses)

### Examples of field-native frameworks worth borrowing

| Field | Framework | What it forces |
|---|---|---|
| Software architecture | Architecture Decision Records (ADRs) | Context, options considered, decision, consequences |
| Software design | C4 model (Context/Containers/Components/Code) | Multi-zoom-level structural views |
| Systems performance | USE method (Utilization/Saturation/Errors) | Resource-level diagnostic checklist |
| Systems performance | RED method (Rate/Errors/Duration) | Service-level diagnostic checklist |
| Law | IRAC (Issue/Rule/Application/Conclusion) | Disciplined legal analysis structure |
| Law | Comparative law: doctrinal / functional / contextual | Multi-perspective cross-jurisdiction analysis |
| Medicine | Differential diagnosis | Force enumeration of all plausible causes before ranking |
| Medicine | PICO (Population/Intervention/Comparison/Outcome) | Structure clinical research questions |
| Finance | DCF + comparables + precedent transactions | Triangulated valuation |
| Finance | Risk decomposition (market/credit/liquidity/operational) | Multi-axis risk surfacing |
| Science | Hypothesis-method-result-discussion-limitations | Force surfacing of own weaknesses |
| Science | Hill criteria (causation in epidemiology) | Multi-criterion causal inference |
| Engineering | FMEA (Failure Mode and Effects Analysis) | Systematic failure-mode enumeration |
| Engineering | Fault tree analysis | Top-down causal decomposition |
| Strategy / business | PESTEL, Porter's Five Forces, JTBD, Business Model Canvas | (the old library — borrow when topic is in this domain) |
| Policy / public admin | Regulatory impact analysis (RIA), cost-benefit analysis | Force quantification of tradeoffs |
| Policy | Stakeholder analysis (power × interest matrix) | Multi-actor mapping |
| History | Periodization, comparative case method, longue durée | Time-frame discipline |
| Negotiation / dispute | BATNA / ZOPA analysis | Decision space + walkaway thresholds |

Don't memorize this list — use it as proof that field-native frameworks exist for almost everything. **Search for the one that fits your topic.**

### When to borrow vs. apply universal dimensions directly

**Borrow** when:
- A field-native framework cleanly captures 2+ of your needed dimensions
- Practitioners in the field recognize and use the framework (not academic-only)
- You can read the framework's instructions and prerequisites in <10 minutes

**Apply universal dimensions directly** when:
- No field-native framework cleanly fits
- Multiple frameworks each cover only one dimension you need
- The topic spans fields in a way no single framework anticipated
- The borrowed framework would force the analysis into the wrong shape

A borrowed framework applied poorly is worse than the 6-dimension check applied honestly. If the framework requires inputs you don't have or assumptions that don't hold, drop it and use the dimensions directly.

---

## Step 3: Document the framework choice

In the Research Plan (SKILL.md Step 2), state:

> **Analytical dimensions selected:** [2-4 of the 6, with one-sentence justification each]
>
> **Field-native framework borrowed:** [name + source, OR "none — applying universal dimensions directly because [reason]"]
>
> **Prerequisite check:** [for the borrowed framework: does the topic actually meet its prerequisites? E.g., DCF requires forecastable cash flows; FMEA requires bounded failure modes; IRAC requires a defined legal issue. If prerequisites don't hold, drop the framework.]

This forces explicit commitment before Layer 3 fan-out and gives the synthesis step a structure to organize findings against.

---

## Quality gate

Before proceeding to Step 3 (research execution), verify:

- [ ] At least 2 of the 6 universal dimensions named, with concrete content (not just "we'll consider the causal dimension" but actual causal analysis)
- [ ] If a field-native framework was borrowed, the choice is documented with the framework's name and source
- [ ] Prerequisite check passed (or the framework was dropped because it didn't pass)
- [ ] If no framework was borrowed, the reason is documented (and the universal dimensions ARE being applied directly, not ignored)

If 2+ items fail, the framework discovery was rushed. Tighten it before fanning out — the dimensions you skip in Step 2 are the dimensions Layer 3 won't surface.

---

## Common failure modes

- **Picking dimensions to confirm a pre-existing answer.** If the dimensions you select all happen to support what you already think, that's motivated reasoning. Force at least one dimension that could falsify your prior — usually Constraint or Incentive does the work.

- **Borrowing a framework you don't actually understand.** A checkbox PESTEL is worse than no PESTEL — it gives false confidence of rigor. If you can't explain the framework's logic in 3 sentences, don't use it.

- **Applying every dimension equally.** 2-4 dimensions dominate any given topic. The other 2-4 are background. Pretending all 6 are equal-weight produces flat, generic output.

- **Skipping the field-native search.** "I don't know one for this field" usually means "I didn't search for one." 5 minutes of explicit search before defaulting to universal dimensions is worth the time.

- **Treating the framework as the analysis.** The framework is a *forcing function* for the analysis. Filling in the framework's boxes is not the deliverable — what the boxes reveal is the deliverable.
