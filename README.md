# claude-deep-research

A domain-agnostic deep research skill for [Claude Code](https://docs.claude.com/en/docs/claude-code/overview). Conducts rigorous, structured investigation across any field — programming, finance, policy, science, medicine, law, markets, history — using parallel subagent fan-out, an independent red-team pass, and a discovery-driven planning architecture that adapts to the topic instead of forcing a fixed framework onto it.

## Why this exists

Most "research" output from LLMs is a Wikipedia-grade overview that stops at Layer 2. This skill is built around a delivery rule of **never less than 7x of what was asked, aiming for 10–15x**, with the depth concentrated where shallow research skips: practitioner-candid forums, failure documentation, and explicit critic/skeptic perspectives.

Three structural moves make that depth affordable in context:

1. **Discovery-driven planning** — lean meta-resources (~25K tokens) teach the agent how to find what any field requires, instead of pre-baking frameworks per domain.
2. **Parallel subagent fan-out** — Layer 3 and Layer 4 threads run as concurrent subagents that write raw findings to disk and return only 200-word digests, keeping main context lean regardless of how many sources got fetched.
3. **Independent red-team agent** — the agent that wrote the synthesis is not the agent that challenges it. A fresh subagent with no conversation history applies a 7-challenge protocol (Steel Man, Survivorship Bias, Recency Bias, Source Bias, Incentive Analysis, Base Rate, Inversion) and the draft is revised against its critique.

## Installation

Drop the skill into your Claude Code skills directory:

```bash
# Per-project
mkdir -p .claude/skills
git clone https://github.com/violetanvil/claude-deep-research.git .claude/skills/deep-research

# Or globally for your user
mkdir -p ~/.claude/skills
git clone https://github.com/violetanvil/claude-deep-research.git ~/.claude/skills/deep-research
```

Claude Code picks it up automatically on next launch.

## Usage

Trigger phrases the skill responds to:

- "look into…"
- "dig into…"
- "explore whether…"
- "map out the landscape for…"
- "what are the options for X"
- "how does Y work in practice"
- "compare X and Y"
- "diagnose why X is broken"
- "what does the evidence say about X"
- "what's the implementation reality of X"

The skill auto-detects mode:

- **Guided** — vague or ambiguous prompts get 3–5 sharp decomposition questions (Goal / Boundary / Knowledge / Constraint / Success) and a confirmable Research Plan before execution.
- **Autonomous** — specific, well-scoped prompts execute end-to-end and return the full deliverable.

## What it produces

A structured brief with:

- **TL;DR** — the answer, not a summary of what's covered
- **The Landscape** — Layers 1–2: vocabulary + the map with decision logic
- **Depth section** (custom-titled per topic shape) — Layer 3: the non-obvious findings, failure modes, and gap between official narrative and practitioner reality
- **Adjacent Opportunities** — Layer 4: 10–15x territory across stakeholder, system, substitute, substrate, and history adjacencies
- **Competing Perspectives & Counterarguments** — the surviving output of the independent red-team pass
- **Decision Points** — cleanly framed tradeoffs (when applicable)
- **Horizon: Worth Knowing About** — Layer 5: brief flags for the 25x zone
- **Sources & Confidence** — organized by archetype with calibrated confidence levels

Per-thread raw findings are persisted under `runs/<date>-<slug>/` so you can audit the evidence base directly.

## Architecture

Six reference files do the heavy lifting. All are domain-agnostic.

| File | Purpose |
|---|---|
| `references/playbook-construction.md` | 7 universal topic shapes (Evaluate Alternatives, Understand a System, Explore a Problem Space, Diagnose a Failure, Trace a History, Predict a Trajectory, Assess a Decision) with per-shape layer templates |
| `references/framework-discovery.md` | 6 universal analytical dimensions (Structural / Dynamic / Comparative / Causal / Constraint / Incentive) and a table of field-native frameworks (ADRs, IRAC, PICO, DCF, etc.) to borrow when the prerequisite check passes |
| `references/source-discovery.md` | 7 universal source archetypes (Authoritative Record, Practitioner Argument, Failure Documentation, Critic-Skeptic, Money-Incentive, Comparative, Synthesis) with cross-domain instantiation and conflict-resolution heuristics |
| `references/synthesis-engine.md` | Triangulation, pattern recognition, fact-to-insight elevation, confidence calibration, narrative construction, absence analysis |
| `references/red-team-prompt.md` | Self-contained prompt pasted verbatim into the independent red-team subagent |
| `references/examples.md` | Four end-to-end discovery walkthroughs across programming, finance, policy, and scientific literature |

## The 5-layer execution model

| Layer | Content | Where it runs |
|---|---|---|
| 1: Surface Scan | Vocabulary, canonical references, the "Wikipedia version" — ~10% of effort | Main context |
| 2: Structure & Landscape | The map with decision logic, not a flat list | Main context |
| 3: Depth Dive | Where the value lives — practitioner reality, failure modes, second-order effects | Parallel subagents |
| 4: Adjacent Opportunities | The 10–15x zone across 5 universal adjacency directions | Parallel subagents |
| 5: Horizon Pointers | Brief flags for the 25x zone | Main context |

Layer 3 mandatorily includes a Critic/Skeptic thread and a Failure Documentation thread — these are the archetypes shallow research skips, and they're where the depth gap usually lives.

## Credits

Inspired by [DishantPal/deep-research-skill](https://github.com/DishantPal/deep-research-skill). This version has been substantially restructured around a domain-agnostic discovery architecture, parallel subagent fan-out with on-disk scratchpads, and a mandatory independent red-team pass.

Apache 2.0 Lincense