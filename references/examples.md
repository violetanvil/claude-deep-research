# Examples: Discovery Process Across Domains

This file shows what good *discovery* looks like — the agent encountering an unfamiliar topic and using the meta-resources to figure out what it needs. It does not show full research outputs (those would balloon this file). It shows the planning step, where most of the leverage lives.

Each example walks through:
1. The user prompt
2. Topic shape selection (from [playbook-construction.md](playbook-construction.md))
3. Analytical dimensions selection (from [framework-discovery.md](framework-discovery.md))
4. Source archetype mapping (from [source-discovery.md](source-discovery.md))
5. The Parallel Threads list
6. A short "good vs bad" contrast — what a shallow approach would miss

Read whichever example is closest to the current research. The point is the *process*, not the specific topic.

---

## Example 1: OS / Systems Programming

**User prompt:** "What are the tradeoffs in choosing between io_uring and epoll for a high-throughput proxy?"

### Topic shape
**Evaluate Alternatives.** The user named two specific options and wants a defensible comparison.

### Analytical dimensions
- **Comparative** (the central operation — these are explicitly being weighed against each other)
- **Constraint** (kernel-version requirements, observability tooling, security posture)
- **Causal** (what drives the performance difference under what conditions)
- **Incentive** (who's investing in each, what the maintainer trajectories look like — io_uring is younger and evolving fast)

Not load-bearing here: Structural in any deep sense (both are well-documented), Dynamic (both stable enough to evaluate now), History (interesting but not decision-relevant).

### Field-native framework borrowed
**USE Method (Utilization/Saturation/Errors)** for the per-resource performance comparison, plus **architecture-decision-record (ADR) format** for documenting the choice. Both are standard in systems engineering. Prerequisites met: bounded resource model, named decision context.

### Source archetype map

| Archetype | Concrete instance | Why for this topic |
|---|---|---|
| Authoritative Record | Kernel source (fs/io_uring/, fs/eventpoll.c), man pages (io_uring(7), epoll(7)), LWN.net's io_uring article series | Ground claims about what the syscalls actually do |
| Practitioner Argument | LKML threads on io_uring perf, lobste.rs threads, HN discussions on production io_uring usage | Where benchmarks get fought over |
| Failure Documentation | CVE database for io_uring, Cloudflare's io_uring vulnerability blog post, kernel regression reports | Real-world failure modes, not theoretical ones |
| Critic / Skeptic | Skeptical posts on "io_uring complexity is not worth it," kernel devs who pushed back on its design | Counter-narrative to the io_uring hype |
| Money / Incentive | Jens Axboe's funding context (Meta), commit author histories on each subsystem | Whose roadmap drives io_uring's evolution |
| Comparative | kqueue (BSD/macOS), IOCP (Windows), Solaris event ports | Cross-platform context for portable design decisions |
| Synthesis | "Linux Programming Interface" (Kerrisk) chapter on I/O multiplexing | Compressed expert overview |

### Parallel Threads (illustrative)
1. **L3-T1:** io_uring real-world performance data + named production users (LWN, kernel.dk, axboe github, "io_uring production" on HN). Returns digest + raw notes to `runs/<date>-iouring-vs-epoll/L3-iouring-perf.md`
2. **L3-T2:** epoll real-world performance data under matched workloads. Returns to `L3-epoll-perf.md`
3. **L3-T3:** io_uring CVE / failure history + known gotchas (CVE database, Cloudflare blog, security mailing lists). Returns to `L3-iouring-failures.md`
4. **L3-T4:** Production proxy choices — what did Envoy, HAProxy, Cloudflare's stack pick and why (engineering blogs, talks). Returns to `L3-prod-choices.md`
5. **L3-T5:** Skeptic / critic perspective — who argued against io_uring and on what grounds (lobste.rs, certain kernel devs, security researchers). Returns to `L3-iouring-criticism.md`
6. **L4-T1:** Cross-platform alternatives (kqueue, IOCP, Solaris event ports) for portable-design context. Returns to `L4-cross-platform.md`
7. **L4-T2:** User-space networking as a reframing (DPDK, AF_XDP) — does the question even matter if you bypass the kernel? Returns to `L4-userspace-networking.md`

### Good vs bad

**Bad approach:** Search "io_uring vs epoll," skim the top 3 blog posts, summarize. Misses CVE history, misses production-user reports, misses critic perspective, misses cross-platform context. Output reads like a generic comparison anyone could write in 20 minutes.

**Discovery-driven approach:** Names 7 specific source channels with concrete searches. Forces the critic perspective explicitly (so the analysis isn't just io_uring marketing). Forces the comparative dimension cross-platform. Surfaces CVEs that would matter for security-sensitive proxies. Output reflects what an engineer with 5 years in this space would write.

---

## Example 2: Finance / Markets

**User prompt:** "How did the 2023 regional banking stress unfold and what's the systemic-risk read?"

### Topic shape
**Diagnose a Failure** as the backbone (what specifically broke?), with a **Trace a History** secondary thread (the run-up to it).

### Analytical dimensions
- **Causal** (the central operation — what triggered what)
- **Structural** (regional bank balance sheets, deposit composition, mark-to-market vs. held-to-maturity)
- **Incentive** (depositor incentives to flee under uninsured-balance fears, supervisor incentives that may have softened scrutiny)
- **Constraint** (regulatory thresholds — $250B SIFI line, stress test exemptions for sub-$250B banks)

### Field-native framework borrowed
**Risk decomposition (interest-rate / liquidity / credit / operational)** for separating the failure modes, plus **CAMELS supervisory framework** for the bank-level analysis. Both are standard in bank analysis. Prerequisites met.

### Source archetype map

| Archetype | Concrete instance | Why |
|---|---|---|
| Authoritative Record | SVB / Signature / First Republic 10-Ks and 10-Qs (EDGAR), Fed FOMC minutes, FDIC press releases on resolutions | Ground claims about balance sheets and policy actions |
| Practitioner Argument | FinTwit (X), bank-analyst Substacks (Marc Rubinstein, Net Interest), r/SecurityAnalysis | Real-time analyst reasoning during the event |
| Failure Documentation | Fed's post-mortem on SVB (the Barr report, April 2023), FDIC's SVB / Signature reports, GAO bank-supervision reports | Official failure analysis |
| Critic / Skeptic | Critiques of the Fed's response (Levy, Calomiris), arguments that the unrealized-loss framing was misleading, opposing views on whether systemic risk was real | Counter to the consensus narrative |
| Money / Incentive | SVB insider sales prior to collapse, which depositors fled and why, who was made whole and who wasn't | Motivation analysis |
| Comparative | Continental Illinois 1984, S&L crisis, 2008 IndyMac, regional bank stress in Japan / Europe | Historical / cross-jurisdictional analogs |
| Synthesis | "Lords of Easy Money" (Leonard), Brookings papers on the episode, IMF GFSR coverage | Compressed expert overviews |

### Parallel Threads (illustrative)
1. **L3-T1:** SVB-specific failure mechanics — bond portfolio MTM losses, deposit composition, run dynamics (Barr report, 10-K, contemporaneous FinTwit analysis). Returns to `L3-svb-mechanics.md`
2. **L3-T2:** Signature / First Republic — same depth, different failure profile (deposit franchise, crypto exposure for Signature). Returns to `L3-signature-fr.md`
3. **L3-T3:** Fed's supervisory failure — what the Barr report admits, what critics say it doesn't. Returns to `L3-supervisory-failure.md`
4. **L3-T4:** Skeptic read — was systemic risk real, or did the Fed overreact? (Calomiris, Levy, opposing views). Returns to `L3-systemic-skeptics.md`
5. **L4-T1:** Continental Illinois 1984 + S&L crisis as historical analogs. Returns to `L4-historical-analogs.md`
6. **L4-T2:** Adjacent risks not yet realized — CRE exposure, commercial deposit flight, BTFP wind-down implications. Returns to `L4-adjacent-risks.md`

### Good vs bad

**Bad approach:** Read NYT / WSJ retrospectives, summarize the consensus narrative ("rising rates + uninsured deposits + Twitter-speed runs"). Misses the supervisory-failure debate, misses the skeptic view, misses the historical analogs that frame whether this was novel or recurring.

**Discovery-driven approach:** Forces the Critic archetype to surface the "the Fed overreacted" thesis. Forces Comparative to test whether the "Twitter-speed run" framing is actually historically novel (it isn't — Continental Illinois had a fax-and-phone run that was nearly as fast). Surfaces the Money / Incentive trail (who knew what when, who was made whole). Output looks like what a buy-side analyst would produce, not a news summary.

---

## Example 3: Policy / Regulation

**User prompt:** "What's the implementation reality of state-level AI disclosure laws?"

### Topic shape
**Understand a System.** The user wants to know how these laws actually function — not whether they're good, not which states have them, but what really happens.

### Analytical dimensions
- **Structural** (statute architecture, agency assignment, enforcement mechanism)
- **Incentive** (compliance lawyers' incentives, agencies' staffing realities, industry's compliance-vs-evasion calculus)
- **Constraint** (agency budgets, statutory ambiguity that hasn't been litigated)
- **Comparative** (across states, vs. EU AI Act, vs. adjacent disclosure regimes like CCPA / HIPAA)

### Field-native framework borrowed
**Regulatory impact analysis (RIA) structure** for organizing the cost / benefit / unintended-consequences view, plus **stakeholder analysis (power × interest matrix)** for mapping who's actually affected and how they respond.

### Source archetype map

| Archetype | Concrete instance | Why |
|---|---|---|
| Authoritative Record | Statute text + implementing regulations (state code, official rulemakings), AG guidance documents | Ground claims about what the law literally requires |
| Practitioner Argument | Law-firm client alerts, bar association CLE materials, compliance-officer LinkedIn posts | Where compliance lawyers signal what's actually hard |
| Failure Documentation | Enforcement actions to date, any settled cases, AG complaints filed | What's actually being prosecuted vs. what's on the books |
| Critic / Skeptic | Industry comment letters arguing the law is overbroad, civil-liberties critiques arguing it's underpowered | Both sides of the "is this law working" debate |
| Money / Incentive | Lobbying records during the bill's passage, campaign finance for sponsors, industry trade-association funding of opposing comment letters | Who pushed for this and who pushed against |
| Comparative | EU AI Act disclosure provisions, CCPA / HIPAA / Sunshine-Act analog regimes, other states' similar bills | What the disclosure-regime archetype looks like elsewhere |
| Synthesis | CRS report on AI regulation landscape, university-tech-policy program write-ups, Brookings AI policy series | Compressed scholarly overview |

### Parallel Threads (illustrative)
1. **L2-T1:** Statute text + rulemakings for each state with such a law (state code searches, official register)
2. **L3-T1:** Enforcement actions to date — anyone sanctioned? On what grounds? (AG offices, court records)
3. **L3-T2:** Compliance-lawyer commentary — where is compliance hardest, where are the loopholes (firm client alerts, CLE recordings)
4. **L3-T3:** Industry comment letters during rulemaking — reveals where the industry pushed back and won (regulations.gov, state register)
5. **L3-T4:** Civil-liberties / consumer-advocacy critique — what these laws don't cover (EFF, EPIC, CDT publications)
6. **L4-T1:** EU AI Act disclosure provisions vs. these state laws — convergence or divergence
7. **L4-T2:** Adjacent disclosure regimes' implementation history (CCPA's first 3 years, HIPAA's enforcement trajectory) as templates for likely AI-disclosure trajectory

### Good vs bad

**Bad approach:** List the states, summarize what each law requires, note "implementation is still developing." Generic, accurate, useless. The user already knew that.

**Discovery-driven approach:** Forces the Failure Documentation archetype (what's actually been enforced) — which surfaces that on most state AI laws, the answer is "nothing yet, and that itself is informative." Forces Incentive analysis on lobbying records, which reveals which provisions got watered down and how. Forces Comparative against CCPA's first-3-years trajectory, which tells the user what to expect over the next 3 years for AI disclosure. Output is a working model of these regimes, not a list.

---

## Example 4: Scientific / Clinical Literature

**User prompt:** "What does the current evidence say about the long-term cardiovascular effects of GLP-1 agonists?"

### Topic shape
**Understand a System** (the current evidence base) with **Evaluate Alternatives** secondary (different drugs in the class).

### Analytical dimensions
- **Causal** (proposed mechanisms — direct cardiovascular protection vs. indirect via weight loss / glycemic control)
- **Comparative** (across drugs in the class, against placebo, against prior diabetes drugs with cardiovascular effects)
- **Constraint** (trial follow-up duration, generalizability beyond enrolled populations, off-label use evidence gaps)
- **Incentive** (industry funding of nearly all major trials, FDA accelerated-approval implications)

### Field-native framework borrowed
**Evidence hierarchy** (RCT > observational > mechanistic) plus **PICO** for structuring the comparison, plus **Hill criteria** for evaluating causal claims about the proposed cardiovascular protection.

### Source archetype map

| Archetype | Concrete instance | Why |
|---|---|---|
| Authoritative Record | Cardiovascular outcome trials (LEADER, SUSTAIN-6, REWIND, SELECT, etc. — published in NEJM/Lancet), FDA labels, ACC/AHA guidelines | Ground claims in published primary trials |
| Practitioner Argument | Cardiology / endocrinology Twitter (MedTwitter), specialty-society listservs, podcast discussions (Curbsiders, Cardionerds) | Real-time clinical reasoning, including dissent from guidelines |
| Failure Documentation | FDA adverse event reports (FAERS), retraction watch (any GLP-1 study retractions?), Cochrane "low quality of evidence" notes where applicable | Real-world adverse signals not captured in trials |
| Critic / Skeptic | BMJ "Too Much Medicine" series on GLP-1 expansion, critiques of trial design (composite endpoints, sponsor analysis), Vinay Prasad / John Mandrola critical commentary | Counter to the "GLP-1 is a wonder drug" narrative |
| Money / Incentive | Open Payments database (which guideline authors received pharma payments), trial sponsor disclosure, ICMJE conflict declarations | Sponsorship-bias check on the evidence base |
| Comparative | Other classes' cardiovascular trials (SGLT2 inhibitors, statins as historical analog), prior diabetes drugs with cardiovascular signals (rosiglitazone failure case) | Cross-class context |
| Synthesis | Cochrane reviews, NEJM review articles, ESC / AHA position statements | Compressed expert consensus |

### Parallel Threads (illustrative)
1. **L1-T1 / L2-T1:** Trial-by-trial summary of major cardiovascular outcome trials (PICO structure for each)
2. **L3-T1:** Sponsor / conflict analysis on the trial set — who paid for what, who analyzed the data
3. **L3-T2:** Critic / skeptic literature — composite-endpoint critiques, the "absolute vs relative risk reduction" framing problem
4. **L3-T3:** Adverse event signal in real-world data (FAERS, post-marketing surveillance) vs. trial AE rates
5. **L3-T4:** SGLT2 inhibitor cardiovascular trials as comparative class — same surprise-cardiovascular-benefit story or different
6. **L4-T1:** Rosiglitazone case as cautionary historical analog (drug class with apparent benefit, then cardiovascular harm signal)

### Good vs bad

**Bad approach:** Quote the SELECT trial's headline result, cite the ACC/AHA guideline update, conclude "GLP-1s reduce cardiovascular events in eligible populations." Misses the absolute-vs-relative framing, misses the sponsorship-uniformity, misses the rosiglitazone analog.

**Discovery-driven approach:** Forces the Money / Incentive archetype, which reveals every major trial was sponsor-run; forces the Critic archetype, which surfaces the absolute-risk-reduction reframing (often <2 percentage points over 3-5 years for primary prevention); forces the Comparative archetype to bring in the rosiglitazone cautionary tale where surrogate endpoints looked great until cardiovascular harm emerged. Output is what an evidence-based-medicine specialist would write, not a guideline summary.

---

## Universal patterns across all 4 examples

Notice what every example does:

1. **Names the topic shape explicitly.** This isn't decoration — it determines what goes in each layer.
2. **Picks 3-4 dimensions from the universal 6, justified by the specific topic.** Doesn't pretend all 6 are equally important.
3. **Borrows a field-native framework when one cleanly fits, instead of reinventing.** Practitioners recognize the shape; the analysis inherits decades of refinement.
4. **Maps each of the 7 source archetypes to a CONCRETE instance for this field.** Not "blogs" — names a specific blog. Not "papers" — names a specific journal or trial set.
5. **Forces the Critic / Skeptic and Failure Documentation archetypes especially hard.** These are where the depth lives. Most shallow research skips them; this skill won't.
6. **Generates 5-8 Parallel Threads, each tied to a layer + archetype + concrete search.** No vague threads.

If your discovery for the current research run does these 6 things, the depth of the output will be 10x+ a single-shot answer. If it skips any, identify which and patch it before fanning out.
