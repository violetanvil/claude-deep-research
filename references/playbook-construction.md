# Playbook Construction

This file teaches the agent how to build a research execution sequence for ANY topic. It does not list playbooks for specific business categories. It identifies the **topic shape** of any research request, then provides a layer-by-layer template for that shape.

The principle: the 5 layers are the constant. What goes *in* each layer depends on the shape of the question. There are 7 recurring shapes that cover almost any research request. Identify the shape, fill the template, fan out.

---

## The 7 Topic Shapes

Identify which shape best matches the user's request. If multiple shapes apply, pick the dominant one as the backbone and pull techniques from secondary shapes.

| Shape | Trigger phrasing | What the user really wants |
|---|---|---|
| **Evaluate alternatives** | "Should we use X or Y?" "Which X is best for…?" "Compare X, Y, Z." | A defensible ranked comparison with the conditions under which each option wins |
| **Understand a system** | "How does X work?" "Explain the architecture of X." "Walk me through X." | A working mental model of structure + dynamics, not just a definition |
| **Explore a problem space** | "What are the options for X?" "What approaches exist for…?" "Map the landscape of X." | An exhaustive map of approaches with the decision logic that branches them |
| **Diagnose a failure** | "Why is X broken?" "What went wrong with X?" "Why isn't X working?" | The actual root cause(s) and the failure mode pattern, not a list of plausible suspects |
| **Trace a history** | "How did X come to be?" "What's the story behind X?" "Why does X exist?" | The causal chain and the surviving consequences, not a chronology |
| **Predict a trajectory** | "Where is X going?" "What's the future of X?" "Will X happen?" | A defensible forecast with the load-bearing assumptions visible |
| **Assess a decision** | "Should we do X?" "Is X a good idea?" "What's the case for/against X?" | A clean tradeoff frame with the strongest counter-argument addressed |

If the user asks something genuinely off this map, fall back to the 5-layer scaffold without a per-shape template — the scaffold alone is sufficient.

---

## Layer Templates by Shape

For each shape: what goes in each of the 5 layers, and the natural Parallel Threads to spawn in Step 3.

### Shape 1: Evaluate Alternatives

**Layer 1 (Surface Scan):** The candidate set — every alternative the field recognizes, with one-line description and current adoption signal.

**Layer 2 (Structure & Landscape):** The decision dimensions — what attributes matter for choosing. Then a comparison matrix at the dimension × alternative grid. Note where alternatives genuinely differ vs. where they're equivalent.

**Layer 3 (Depth Dive):** For each surviving alternative (after first-pass elimination), the implementation reality: actual user experience, hidden costs, failure modes, edge cases. Read negative reviews / failure documentation explicitly. **Talk to losers as well as winners.**

**Layer 4 (Adjacent Opportunities):** Substitute approaches the user didn't ask about. Hybrid approaches (use A for X, B for Y). Build-vs-buy alternatives if the request implied one mode.

**Layer 5 (Horizon):** Pre-pre-release alternatives, research-stage approaches, deprecated approaches that might return.

**Natural Parallel Threads:**
- One thread per alternative, deep-diving its real-world experience
- One thread on negative reviews / failure stories across all alternatives
- One thread on the "build vs buy vs integrate" axis
- One thread on hidden costs / total-cost-of-ownership
- One thread on the comparative dimension nobody talks about (often interoperability or migration cost)

### Shape 2: Understand a System

**Layer 1 (Surface Scan):** The standard description — definition, the canonical diagram, the textbook explanation. Establish vocabulary fast.

**Layer 2 (Structure & Landscape):** The architecture — components, interfaces, data/control flow, dependencies. Layered or zoomed views (start coarse, refine). The "if I had to draw it on a whiteboard" version.

**Layer 3 (Depth Dive):** How it actually behaves under load, edge cases, undocumented quirks, the gap between docs and source. Failure modes and how the system signals them. What experienced practitioners know that newcomers learn the hard way.

**Layer 4 (Adjacent Opportunities):** Subsystems that interact with this one. Alternative implementations of the same concept (other OSes, other languages, other eras). Higher-level systems that depend on this one.

**Layer 5 (Horizon):** Future evolution (RFCs, design docs, research projects). Historical alternatives that lost.

**Natural Parallel Threads:**
- One thread on the canonical explanation (textbook + spec + reference docs)
- One thread on the source / primary materials
- One thread on practitioner-level "gotchas" (forums, mailing lists)
- One thread on failure documentation (CVEs, post-mortems, bug reports)
- One thread on alternative implementations / comparable systems elsewhere

### Shape 3: Explore a Problem Space

**Layer 1 (Surface Scan):** The named approaches that already exist. The terminology. The boundaries of the space.

**Layer 2 (Structure & Landscape):** The decision tree — how the approaches branch by use case. What conditions favor which branch. The "map" of the space.

**Layer 3 (Depth Dive):** For 2-3 of the most plausible branches given the user's context: implementation reality, gotchas, real-world results. Cases where the branch worked and cases where it didn't.

**Layer 4 (Adjacent Opportunities):** Approaches that combine branches (hybrid). Approaches that bypass the problem entirely. Reframings of the problem itself.

**Layer 5 (Horizon):** Emerging approaches not yet mainstream. Approaches from adjacent fields not yet imported.

**Natural Parallel Threads:**
- One thread per branch's depth-dive
- One thread on hybrid / unconventional approaches
- One thread on "did anyone solve this without solving it" (problem dissolution)
- One thread on the loudest critic of the dominant branch

### Shape 4: Diagnose a Failure

**Layer 1 (Surface Scan):** The symptom — what specifically isn't working, when did it start, who's affected. Quantify if possible.

**Layer 2 (Structure & Landscape):** The system architecture relevant to the failure. The failure points where this could happen.

**Layer 3 (Depth Dive):** The actual evidence — logs, reports, similar past failures, expert diagnosis of analogous cases. Apply elimination: which failure points are consistent with the symptom, which can be ruled out. **Look hard for prior occurrences in the field's failure documentation.**

**Layer 4 (Adjacent Opportunities):** Other failure modes that share root causes with the diagnosed one. Other systems that have the same vulnerability. Systemic issues that this is a symptom of.

**Layer 5 (Horizon):** Patterns this failure fits into (industry-wide, era-wide). Whether the failure is recurring or novel.

**Natural Parallel Threads:**
- One thread on the specific symptom evidence
- One thread per plausible root cause, gathering evidence for/against
- One thread on analogous past failures (in this field and adjacent ones)
- One thread on the systemic-issue read (is this a one-off or a pattern?)

### Shape 5: Trace a History

**Layer 1 (Surface Scan):** The standard chronology. The dates, the named events, the canonical "why."

**Layer 2 (Structure & Landscape):** The actors involved and their motivations. The structural conditions that made the history possible. The decision points where it could have gone differently.

**Layer 3 (Depth Dive):** Primary sources — what people said at the time, not what historians said later. Disputed accounts. Counter-narratives. The mundane mechanics nobody bothered to record.

**Layer 4 (Adjacent Opportunities):** Parallel histories elsewhere (other countries, other industries, other eras). Counterfactuals — what would have happened if a key decision had gone the other way.

**Layer 5 (Horizon):** Surviving consequences — institutions, conventions, regulations, codebases that exist today because of this history. What the history tells us about analogous current situations.

**Natural Parallel Threads:**
- One thread on primary sources (contemporary accounts, original documents)
- One thread on the standard historical narrative + canonical historians
- One thread on revisionist / minority accounts
- One thread on parallel histories in other contexts
- One thread on surviving consequences and present-day implications

### Shape 6: Predict a Trajectory

**Layer 1 (Surface Scan):** The current state and recent direction. What everyone agrees has been happening.

**Layer 2 (Structure & Landscape):** The drivers — what forces push the trajectory. Apply the Causal dimension explicitly. Distinguish secular trends from cyclical patterns from one-off shocks.

**Layer 3 (Depth Dive):** The leading indicators experts actually watch (often different from the indicators the public watches). Historical analogs and how they played out. The strongest case for the trajectory bending or breaking.

**Layer 4 (Adjacent Opportunities):** Adjacent systems that would also be affected. Second-order consequences if the trajectory continues. Reflexive feedback loops (the prediction itself changes the outcome).

**Layer 5 (Horizon):** Tail scenarios (low-probability, high-consequence). Black-swan precursors that would invalidate the prediction.

**Natural Parallel Threads:**
- One thread on the consensus forecast and its assumptions
- One thread on the strongest contrarian forecast
- One thread on historical analogs (where has this exact trajectory played out before?)
- One thread on the leading indicators practitioners watch
- One thread on what would have to be true for the trajectory to break

### Shape 7: Assess a Decision

**Layer 1 (Surface Scan):** The decision as stated. The default option (do nothing). The named alternatives.

**Layer 2 (Structure & Landscape):** The decision criteria — what dimensions matter for choosing. The constraints (Constraint dimension is usually load-bearing here). The stakeholders and their incentives (Incentive dimension also load-bearing).

**Layer 3 (Depth Dive):** Real-world cases of similar decisions: who chose Yes and what happened, who chose No and what happened. Implementation reality of each option. Hidden costs.

**Layer 4 (Adjacent Opportunities):** Reframings of the decision. Sequenced options (do A first, then decide B). Decisions adjacent to this one that should be made together.

**Layer 5 (Horizon):** Decisions this one forecloses or enables. Long-tail consequences that show up years later.

**Natural Parallel Threads:**
- One thread per option, deep-diving its real-world consequences
- One thread on the strongest case for "do nothing"
- One thread on hidden costs / second-order consequences
- One thread on the strongest objection from the most-affected stakeholder

---

## Step 1: Identify the topic shape

Read the user's prompt and pick the dominant shape from the table above. State it explicitly in the Research Plan:

> **Topic shape:** [shape name] — because [one-sentence reason]

If two shapes both fit (e.g., "Should we adopt X or Y?" is both Evaluate Alternatives and Assess a Decision), pick the dominant one as the backbone and add 1-2 threads from the secondary shape.

If no shape fits cleanly, name that explicitly: **"Topic shape: custom — applying the bare 5-layer scaffold because [reason]."** Then construct your own per-layer plan.

---

## Step 2: Fill the layer template

Walk through each of the 5 layers and write 2-4 sentences naming what specifically belongs in that layer for THIS topic. Don't paste the template language — particularize it. "Layer 3: implementation reality" is not enough; "Layer 3: how io_uring actually behaves under high concurrency, the known wakeup gotchas, and the comparative latency vs epoll under realistic workloads" is.

---

## Step 3: Generate the Parallel Threads list

Use the natural threads from the shape's template as a starting point. Customize each thread's prompt to the specific topic, source archetypes (from [source-discovery.md](source-discovery.md)), and analytical dimensions (from [framework-discovery.md](framework-discovery.md)).

Each thread should map to:
- A layer (mostly Layer 3, some Layer 4)
- 1-2 source archetypes from source-discovery.md
- A specific search starting point
- A scratchpad path (`runs/<date>-<slug>/L<n>-<thread-id>.md`)

Aim for 5-10 threads total. More than 10 is usually evidence the threads are too narrow — consolidate.

---

## Worked Example 1: Cross-domain (programming)

**User prompt:** "What are the tradeoffs in choosing between io_uring and epoll for a high-throughput proxy?"

**Topic shape:** Evaluate Alternatives — two named options, the user wants a defensible comparison.

**Filled layer template:**
- L1: Brief description of each, current Linux-version availability, named users in production
- L2: Comparison matrix on dimensions: throughput, latency tail, CPU overhead, complexity, kernel-version constraints, observability, security model
- L3: Real-world performance data from named workloads; known gotchas (io_uring CVE history, epoll edge-triggered pitfalls); how production proxy projects (Envoy, HAProxy, Cloudflare's stack) actually chose
- L4: Substitutes — io_uring SQPOLL mode, epoll + SO_REUSEPORT, alternative event models (kqueue on BSD, IOCP on Windows for cross-platform context); reframings — should we be using user-space networking (DPDK)?
- L5: Future direction — io_uring's roadmap, kernel maintainer signals on long-term priority

**Parallel Threads (illustrative subset):**
1. L3-T1: io_uring real-world performance data + production user reports (search: kernel.dk blog, LWN articles, axboe github, "io_uring production" on HN)
2. L3-T2: epoll real-world performance data + production user reports (search: same channels for epoll-vs-io_uring benchmarks)
3. L3-T3: io_uring CVE / failure history + known gotchas (CVE database, kernel security mailing list, Cloudflare blog post on io_uring vulnerabilities)
4. L3-T4: How named production proxies chose (Envoy / HAProxy / Cloudflare blog posts and engineering talks)
5. L4-T1: Alternative event models for cross-platform context (kqueue, IOCP), and user-space networking as a reframing

## Worked Example 2: Cross-domain (policy)

**User prompt:** "What's the implementation reality of state-level AI disclosure laws?"

**Topic shape:** Understand a System — the user wants a working mental model of how these laws actually function in practice.

**Filled layer template:**
- L1: Which states have such laws, when enacted, basic scope (which AI uses, who's required to disclose, to whom)
- L2: The structure — required disclosures, exemptions, enforcement mechanism, penalties on paper, agency responsible
- L3: Enforcement reality — has anyone been sanctioned? How are agencies actually staffing this? What do compliance lawyers tell clients vs. what's literally written? Where are the loopholes? What do critics say is missing?
- L4: Adjacent regimes — federal proposals, EU AI Act parallels, sector-specific disclosure laws (financial advice, healthcare AI), comparable disclosure regimes from privacy law
- L5: Trajectory — pending bills, attorney general signals, industry comment letters revealing where compliance is hardest

**Parallel Threads (illustrative subset):**
1. L2-T1: Statute text and rulemaking for each state with such a law
2. L3-T1: Enforcement actions and AG guidance to date
3. L3-T2: Compliance-lawyer commentary (firm client alerts, bar association CLE materials)
4. L3-T3: Industry comment letters and lobbying records (reveal where compliance is hardest)
5. L4-T1: EU AI Act parallel + how its disclosure provisions differ
6. L4-T2: Adjacent disclosure regimes (CCPA, HIPAA, financial-advice fiduciary disclosure) — what their implementation revealed

---

## Quality gate

Before proceeding to Step 3 (research execution), verify:

- [ ] Topic shape named explicitly (one of the 7, or "custom" with reason)
- [ ] Each of the 5 layers has 2-4 sentences of particularized content (not template language)
- [ ] At least 5 Parallel Threads generated, each with: layer, source archetypes, search starting point, scratchpad path
- [ ] Threads collectively cover the dominant analytical dimensions identified via [framework-discovery.md](framework-discovery.md)
- [ ] Threads reference concrete sources (from the [source-discovery.md](source-discovery.md) archetype table), not generic ones

If 2+ items fail, the playbook construction was rushed. The fan-out only finds what the threads specifically search for — vague threads return vague digests.

---

## Common failure modes

- **Picking the wrong shape.** "Should we use X or Y?" looks like Evaluate Alternatives but if the user actually wants to understand how X works to even know whether it applies, the real shape is Understand a System. Read the prompt twice; ask if uncertain.

- **Pasting the template instead of filling it.** "Layer 3: implementation reality" is a category, not content. Write what specifically goes in Layer 3 for this exact topic.

- **Too few threads.** Fewer than 5 threads means Layer 3 will be thin. Each missing thread is an entire angle missing from the final output.

- **Too many threads.** More than 10 threads usually means the threads overlap. Consolidate — two threads searching the same place are one thread.

- **Threads that don't tie to source archetypes.** A thread that says "research io_uring more deeply" without naming WHERE to research will return shallow results. Each thread must point to a concrete source archetype with a specific search starting point.
