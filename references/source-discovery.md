# Source Discovery

This file teaches the agent how to identify high-signal sources for ANY domain — programming, finance, policy, science, medicine, law, history, anything. It does not list specific sources. It lists **source archetypes** that exist in every serious field, then gives heuristics for finding their concrete instances in a domain you may know nothing about.

The principle: every mature field has the same structural source types. The names and addresses change. Your job is to find the local instance of each archetype.

---

## Step 1: Identify the field

Before searching for sources, name the field precisely. Not "AI" but "post-training methods for foundation models." Not "the economy" but "US monetary policy transmission mechanisms." Not "kernels" but "Linux memory management subsystem."

Precision matters because each archetype below has a *different concrete address* in different sub-fields, even within the same parent domain. Healthcare-finance and healthcare-clinical-research have entirely different practitioner forums.

---

## Step 2: Map the 7 source archetypes

Every serious field has these 7. For your field, identify the concrete instance of each — search for it explicitly if you don't know it.

### Archetype 1 — Authoritative Record
**What it is:** The formal, citable, defensible knowledge. What you'd point at if challenged.

**Examples across domains:**
- Software / OS: source code itself, language specs, RFCs, kernel commit history, reference docs
- Finance: SEC filings (10-K, 10-Q, 8-K), Federal Reserve releases, IMF/World Bank statistics, central bank minutes
- Law: statutes, case law, regulations, court opinions
- Science: peer-reviewed papers, preprint servers (arXiv, bioRxiv), conference proceedings (NeurIPS, ICML, OSDI, SOSP)
- Medicine: FDA labels, Cochrane reviews, clinical trial registries (ClinicalTrials.gov), guideline documents (NCCN, USPSTF)
- Policy: legislative text, agency rulemakings, CRS reports, GAO reports
- Engineering / standards: IEEE/ISO/W3C standards, IETF RFCs

**Search heuristic:** "official documentation [field]," "[field] standards body," "[field] primary sources." Look for .gov, .org, .edu, official-issuer URLs. The Authoritative Record is what insiders cite when arguing.

**Strength:** unimpeachable on what's *written*. **Weakness:** says nothing about what's *practiced*.

### Archetype 2 — Practitioner Argument Zone
**What it is:** Where working practitioners argue with each other, in public, with low PR filtering. The most candid signal in any field.

**Examples across domains:**
- Software / OS: LKML (lore.kernel.org), GitHub issues + PR discussions, Hacker News comments, Stack Overflow, language-specific subreddits, internals.rust-lang.org, Discord servers
- Finance: FinTwit (X), r/SecurityAnalysis, r/wallstreetbets (for retail dynamics), Bogleheads, professional Slack/Discord communities, SeekingAlpha comments
- Law: r/lawyers, lawyer Twitter, ABA committee discussions, jurisdiction-specific bar forums
- Science: peer-review reports (open-review platforms), academic Twitter, Reddit r/AskScience for accessibility-friendly arguments, departmental seminars (look for recordings)
- Medicine: Twitter MedTwitter, r/medicine, specialty society listservs, Doximity discussions
- Policy: think-tank blog posts (especially comment sections), Congressional staff Twitter, journalist Twitter beats
- General trades: subreddits for the trade, profession-specific Discord servers, LinkedIn comment threads on practitioner posts

**Search heuristic:** "[topic] reddit," "[topic] hacker news," "[topic] twitter," "[topic] mailing list," "[topic] forum." If you can't find one in 3 minutes, the field may be too small to have one — that's itself informative.

**Strength:** real practitioner experience, candid critique, edge cases that don't make it to docs. **Weakness:** loud minorities, recency bias, often anonymous.

### Archetype 3 — Failure Documentation
**What it is:** Where things that went wrong get recorded. Failures teach more than successes because survivors edit their narratives; failures are forced into the open by some external mechanism (regulator, victim, court, debugger).

**Examples across domains:**
- Software / OS: CVE database, kernel bug tracker, GitHub closed issues with "wontfix" or "regression," post-mortem culture sites (e.g., danluu.com curated lists), AWS/Cloudflare/GitLab status-page incident reports
- Finance: SEC enforcement actions, FINRA disciplinary actions, bankruptcy filings, restatement disclosures, short-seller reports (Hindenburg, Muddy Waters)
- Law: malpractice case databases, attorney discipline records, overturned-on-appeal opinions
- Science: retraction watch (retractionwatch.com), failed-replication databases, Cochrane "low quality of evidence" notes, registered-report null results
- Medicine: FDA adverse event reports (FAERS), MAUDE database (devices), recall notices, malpractice case summaries
- Policy: GAO failed-program audits, IG reports, congressional oversight hearing transcripts, sunset reviews
- Engineering: NTSB accident reports, industry incident databases (CHIRP for aviation, MARS for marine), RCA publications

**Search heuristic:** "[topic] post-mortem," "[topic] failure," "[topic] CVE," "[topic] enforcement action," "[topic] retraction," "[topic] bug." Add "site:reddit.com" or "site:lobste.rs" for community-collected failure stories.

**Strength:** unfiltered reality. **Weakness:** reports the dramatic failures, misses the slow-burn ones.

### Archetype 4 — Critic and Skeptic Channel
**What it is:** Voices that dispute the dominant narrative. Every field has a school of thought that says the consensus is wrong. Even when they're wrong, they probe weaknesses the consensus glosses over.

**Examples across domains:**
- Software / OS: skeptical-language blogs (Drew DeVault, Steve Yegge, Hillel Wayne), "[language] considered harmful" essays, alternative-architecture advocates (microkernel proponents, Lisp/Smalltalk advocates), formal-verification skeptics-of-mainstream
- Finance: short-sellers, value-investor critics of growth narratives, MMT economists vs. mainstream, gold-bugs vs. fiat, permabears
- Law: dissenting opinions, law-review critiques, originalist vs. living-constitution debates, defense-bar vs. prosecution-bar publications
- Science: replication-crisis researchers (Ioannidis, Nosek), heterodox journals, paradigm-challenging preprints
- Medicine: BMJ "Too Much Medicine" series, USPSTF dissents, contrarian guideline authors, Cochrane vs. industry-funded RCT critiques
- Policy: opposition think tanks (left and right), advocacy-group critiques of agency actions, academic critiques of policy implementation
- General: "[topic] criticism," "[topic] limitations," "[topic] is overrated"

**Search heuristic:** "criticism of [topic]," "problems with [topic]," "[topic] is wrong," "[topic] alternatives." Search opposite-sided publications deliberately. If your sources all agree, you have a source-bias problem.

**Strength:** surfaces unchallenged assumptions. **Weakness:** can be motivated reasoning; needs Archetype 1 cross-check.

### Archetype 5 — Money and Incentive Trail
**What it is:** Who's paying for what, and why. Following the money explains motivations that public statements obscure.

**Examples across domains:**
- Software / OS: who funds the maintainers (Linux Foundation members, OpenJS funders, GitHub sponsors), corporate kernel contributors (LWN's "who wrote 6.x" series), VC investment in projects
- Finance: institutional ownership filings (13F), insider transactions (Form 4), short interest data, SEC EDGAR full-text search
- Law: campaign finance for judges (where elected), law-firm client lists, amicus brief funders
- Science: grant databases (NIH RePORTER, NSF awards), industry-funded vs. independent studies, conflict-of-interest disclosures, Open Payments database (medicine)
- Medicine: pharma/device payments (Open Payments / Sunshine Act), guideline-author conflict disclosures, journal sponsorship
- Policy: lobbying disclosures (OpenSecrets), think-tank funders, dark-money tracing (CRP), foundation grants (Foundation Directory)
- Universal: "who profits if this conclusion is accepted? who loses?"

**Search heuristic:** "[topic] funded by," "[topic] lobbying," "[author] disclosures," "[topic] industry ties," "[topic] grant database." For any source you cite, search for that source's funding before relying on it.

**Strength:** explains why narratives diverge. **Weakness:** funding ≠ corruption; correlation isn't causation.

### Archetype 6 — Comparative / Cross-Reference
**What it is:** How analogous problems were handled elsewhere — other countries, other industries, other historical periods, other languages, other ecosystems. Borrowed lenses reveal blind spots.

**Examples across domains:**
- Software / OS: how does BSD/Darwin/Windows/Plan-9/seL4 handle this? what did the previous generation (System V, OS/2, BeOS) do? how do other languages model this concept?
- Finance: how do Japan / EU / emerging markets handle this? what happened in 1929, 1987, 2008, 2020? other-asset-class equivalents?
- Law: comparative law (UK, EU, Canada), prior statutory regimes, restatements
- Science: prior paradigms in this field, analogous methods in adjacent fields (e.g., physics methods applied to biology)
- Medicine: how do other countries' systems handle this condition? historical treatments and why they were abandoned?
- Policy: international comparisons, prior-administration approaches, state-level natural experiments
- Universal: "what's the closest analog to this in a *different* domain or era, and what happened there?"

**Search heuristic:** "[topic] in [other country/era/industry]," "[topic] alternatives," "history of [topic]," "[adjacent field] approach to [problem]."

**Strength:** breaks single-context bias. **Weakness:** false analogies — context can matter more than structural similarity.

### Archetype 7 — Synthesis and Survey
**What it is:** Curated overviews — review articles, textbooks, "the X book," meta-analyses, encyclopedia-grade summaries. These compress decades of work but also bake in consensus assumptions.

**Examples across domains:**
- Software / OS: O'Reilly / NoStarch books, "The Linux Programming Interface" (Kerrisk), "Operating Systems: Three Easy Pieces," ACM Computing Surveys
- Finance: CFA curriculum, "Security Analysis" (Graham), Damodaran's writings, IMF / BIS working papers
- Law: hornbooks, restatements, treatises, law-review survey articles
- Science: review articles, Annual Review series, textbooks at the graduate level, meta-analyses
- Medicine: UpToDate, Cochrane reviews, NEJM review articles, specialty board review books
- Policy: CRS reports, RAND monographs, university-press policy books
- Universal: "[topic] textbook," "[topic] review article," "[topic] survey paper," "introduction to [topic] for [adjacent field] researchers"

**Search heuristic:** "[topic] review," "[topic] survey," "[topic] textbook," "introduction to [topic]." Use these to bootstrap Layer 1 fast, then move on.

**Strength:** compressed expertise. **Weakness:** lags by 1-5 years; hides controversies; reflects when-it-was-written consensus.

---

## Step 3: Build the source plan for THIS research

For your Research Plan (SKILL.md Step 2), produce a small table:

| Archetype | Concrete instance in this field | Why it matters here | How to query |
|---|---|---|---|
| Authoritative Record | [domain-specific] | [what claims it grounds] | [exact URL or search] |
| Practitioner Argument | [domain-specific] | [what edge cases it surfaces] | [exact forum / hashtag] |
| Failure Documentation | [domain-specific] | [what failure modes it reveals] | [exact database / archive] |
| Critic / Skeptic | [domain-specific] | [what assumption it challenges] | [exact author / publication] |
| Money / Incentive | [domain-specific] | [whose motivation it explains] | [exact filing type / database] |
| Comparative | [domain-specific] | [what analog it surfaces] | [other-context to compare] |
| Synthesis | [domain-specific] | [what overview it provides] | [exact textbook / review] |

If you can't fill a row, that's a gap to flag in the final output's "Sources & Confidence" section. **Don't pretend a missing archetype is found** — silence is data.

This table feeds directly into the Parallel Threads plan: each Layer 3 subagent prompt should be tied to one or two archetypes and given the concrete instances to search.

---

## Source weighting — universal heuristics

When sources conflict (and they will), weigh them by these criteria:

1. **Primary > Secondary > Tertiary.** A SEC filing beats a Bloomberg article beats a tweet about the article. The kernel source code beats a blog post about it.
2. **Recency matters when the field moves fast** (software, AI, recent law) and matters less when the substrate is stable (kernel internals from 2015, Roman law).
3. **Specificity beats generality.** A source that names this exact bug / this exact case / this exact firm beats one that talks about "the industry" generally.
4. **Disinterest beats interest.** A source with no stake in your conclusion is more credible than one that benefits from it. Apply Archetype 5 to every source.
5. **Skin in the game beats no skin.** Inverse of #4 in operational matters: a practitioner who'd have to live with a bad recommendation often understands the problem better than an outside expert.
6. **Track record where checkable.** Has this source's prior predictions / analyses been verified? Punditry without a track record is entertainment.

When applying #4 and #5 conflict (a vendor has skin in the game *and* is selling something), document both and treat the source as MEDIUM confidence at best.

---

## Red flags to discount sources

- Conclusion stated before evidence presented
- No methodology described (especially for "studies" and "reports")
- Single-source citations referenced as if multiple
- Anonymous quotes without verification mechanism
- Numbers without units, time period, or methodology
- Heavy use of qualifiers that hide weakness ("research suggests," "experts agree," "many believe")
- Funding disclosure missing or buried
- Old publication date treated as current
- "Common knowledge" claims that no one has rigorously checked
- Press release or marketing copy treated as journalism

When you spot these in a source, downgrade the confidence level on whatever claim it supports.

---

## When sources conflict

1. State the conflict explicitly. Don't pick a side silently.
2. Identify the *type* of conflict: factual disagreement, definitional difference, time-period difference, methodological difference, or perspective/incentive difference. Each type resolves differently.
3. If one source is more authoritative *for this specific claim*, say so and explain why.
4. If the conflict is genuinely unresolvable from available sources, present both and flag confidence as LOW or SPECULATIVE in [synthesis-engine.md](synthesis-engine.md) terms.
5. Use Archetype 6 (Comparative) to break ties — does an analogous case lean one way?

---

## Quality test for the source plan

Before executing Layer 3 fan-out, run this check on your Step-2 source table:
- [ ] At least 5 of the 7 archetypes have a concrete instance identified
- [ ] At least 2 archetypes provide *opposing* perspectives (e.g., Practitioner Argument + Critic, or Authoritative + Failure Documentation)
- [ ] No archetype is filled with a generic placeholder ("blogs," "news") — each entry is a specific named source or search target
- [ ] Each Parallel Thread maps to one or two archetypes with a clear search starting point

If 3+ items fail, your source plan is too thin. Strengthen it before fanning out — Layer 3 quality is bounded by source quality.
