# The cost of a shared AI reviewer

**Question this document answers:** If one team in a company owns a shared AI code reviewer that runs on every repository, what does that actually cost — in licence money, in triage labour, in ownership, and in the freedom to leave?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 03

**Last updated:** 2026-09-20

> **Method note, read this first.** The session's web-search budget was exhausted before this research began (200/200 calls used by other agents). Every finding below was obtained by fetching a URL I could name in advance, or by querying the arXiv and OpenAlex APIs directly. That biases coverage toward vendors and papers I already knew to look for. Threads 3 (ownership surveys) and 5 (exit costs) are materially thinner than the others as a direct result, and I have said so rather than filled the gap. No figure below is estimated unless the line says so.

## Main findings

- **The licence is the cheap part.** At published September 2026 list prices, a shared reviewer for 1,000 developers costs roughly **$144k–$864k/year** depending on vendor and tier. Per-review marginal prices are small and remarkably convergent across vendors: **$0.52** (GitHub Copilot, computed from 13 premium requests × $0.04), **$1.00** (Greptile, Entelligence), **~$1.67** (Qodo, computed from its own credit table).
- **Roughly half to three-fifths of what a shared reviewer says is not acted on, and this is the best-measured number in the whole field.** The largest independent study (Lin et al. 2026, 31,073 review/feedback pairs across 239 repositories) found **36.4% accepted, 56.3% rejected**. The leading vendor's own published figure agrees: Greptile reports a **43% comment acceptance rate**, up from 30%. Both numbers describe the same thing from opposite sides of the sales pitch.
- **The best-known industrial deployment made pull requests slower, not faster.** Cihan et al. (ICSE 2025 SEIP), 4,335 PRs, 238 practitioners: **73.8% of automated comments were resolved**, and median PR closure time rose **from 5h52m to 8h20m** — a ~42% increase.
- **The Bosu et al. 2025 citation in the brief does not exist.** The numbers are real but belong to **Cihan, Haratian, İçöz, Gül, Devran, Bayendur, Uçar and Tüzün**, arXiv 2412.18531, ICSE 2025 SEIP track. Amiangshu Bosu's publication record contains no such study. Corrected reference in §2.1.
- **The centralized-SAST precedent is a false-positive problem, and it has not improved.** Tencent's 2026 industrial study found **328 of 433 alarms (75.8%) were false positives**, each costing **10–20 minutes of manual inspection**. Johnson et al. (ICSE 2013, 529 citations) named false positives as the primary adoption barrier thirteen years earlier.
- **A model is measurably worse at reviewing code from its own family — and the effect is now quantified.** Greptile (July 2026, 2 × 500 PRs, ~1,500 ground-truth bugs): Claude Opus caught **62%** of bugs in Codex-authored PRs but only **53.7%** in Claude-authored ones; GPT 5.5 caught **60%** in Claude-authored PRs versus **50.5%** in Codex-authored ones. A single centrally mandated reviewer is a single correlated blind spot.

---

## 1. Money

### 1.1 Pricing table

All prices fetched **2026-09-20** from the vendor's own public pricing page unless the source column says otherwise. All are **vendor list prices** (not negotiated, not telemetry).

| Product | Plan | List price | Usage terms | Fetched | Source |
|---|---|---|---|---|---|
| GitHub Copilot | Pro | $10/user/mo | Code review included; $15/mo credits | 2026-09-20 | github.com/features/copilot/plans |
| GitHub Copilot | Pro+ | $39/user/mo | Code review included; $70/mo credits | 2026-09-20 | same |
| GitHub Copilot | Max | $100/user/mo | Code review included; $200/mo credits | 2026-09-20 | same |
| GitHub Copilot | — | **13 premium requests per code review** | $0.04/premium request; 1 AI credit = $0.01 | 2026-09-20 | docs.github.com/…/copilot-requests |
| CodeRabbit | Essentials | $24/dev/mo annual ($30 monthly) | 5 PR reviews/dev/hour | 2026-09-20 | coderabbit.ai/pricing |
| CodeRabbit | Team | $48/dev/mo annual ($60 monthly) | 8 PR reviews/dev/hour | 2026-09-20 | same |
| CodeRabbit | Advanced | $72/dev/mo annual | 10 PR reviews/dev/hour | 2026-09-20 | same |
| CodeRabbit | add-ons | **$0.25 per reviewed file**; **$0.40 per agent minute** | beyond included limits | 2026-09-20 | same |
| Greptile | Pro | **$30/seat/mo** | 50 credits/seat included, **$1 per additional credit** | 2026-09-20 | greptile.com/pricing |
| Cursor | Pro / Pro+ / Ultra | $20 / $60 / $200 per user/mo | Bugbot on **usage-based billing**, included on all paid tiers; no per-review rate published | 2026-09-20 | cursor.com/pricing; cursor.com/docs/bugbot |
| Graphite | Starter / Team | $20 / $40 per user/mo, billed annually | "Unlimited AI Reviews" on Team | 2026-09-20 | graphite.com/pricing |
| Qodo | Pro Team | $30/mo for up to 30 users | ~2,500 credits ≈ **18 reviews/mo**; **$0.012/credit**, pooled | 2026-09-20 | qodo.ai/pricing |
| Sourcery | Pro / Team | $12 / $24 per seat/mo | Team: 200+ repos, 3× review rate limits | 2026-09-20 | sourcery.ai/pricing |
| Codacy | Team | $18/dev/mo annual ($21 monthly) | ≤30 devs, ≤100 private repos; AI Reviewer & merge gates | 2026-09-20 | codacy.com/pricing |
| Baz | (single model) | **$30 per active developer/mo** + $0.01 per Engineering Work Credit | no cap published | 2026-09-20 | baz.ai/pricing |
| Entelligence | Startup (≤15 eng) | $750/mo | 300 reviews included, **$1 per extra review** | 2026-09-20 | entelligence.ai/pricing |
| Entelligence | Scale (16–50 eng) | $2,500/mo | 1,000 reviews included, **$1 per extra review** | 2026-09-20 | same |

**Note on Graphite Diamond.** The brief asks for "Graphite Diamond" pricing. As of 2026-09-20 there is no product called Diamond on graphite.com/pricing or graphite.com/docs/ai-reviews; `graphite.com/features/diamond` returns 404. The AI review capability is bundled into the Team tier as "Unlimited AI Reviews." Either the product was renamed or retired. Treat any Diamond price you see elsewhere as stale.

### 1.2 Marginal cost per review

These are the only three published or directly computable per-review prices I found.

- **GitHub Copilot — $0.52 per review (my arithmetic on two published figures).** GitHub documents: *"Each time Copilot reviews a pull request (when assigned as a reviewer) or reviews code in your IDE, 13 premium requests are consumed."* (docs.github.com, fetched 2026-09-20). Additional premium requests are $0.04. 13 × $0.04 = $0.52. GitHub does not itself state this product; the multiplication is mine.
- **Greptile / Entelligence — $1.00 per review.** Published directly. Greptile: *"The pricing is $30/developer/month, which includes 50 reviews/month, after which reviews cost $1 each."* (greptile.com/blog/greptile-v4, 5 March 2026).
- **Qodo — ~$1.67 per review (my arithmetic on Qodo's credit table).** Qodo publishes "~2,500 credits (~18 reviews/month)" and "$0.012/credit". 2,500 ÷ 18 ≈ 139 credits per review; 139 × $0.012 ≈ $1.67.

The convergence around $0.50–$1.70 matters for the chapter: **the marginal cost of one more review is trivial, which is precisely why a central owner has no natural brake on volume.** Nothing in any of these pricing models charges for a *wrong* review.

### 1.3 What a review costs self-hosted

**I could not verify a published token or compute cost per review from any vendor.** The closest available figures:

- Qodo's open-source PR-Agent README states only: *"Each tool (`/review`, `/improve`, `/ask`) uses a single LLM call (~30 seconds, low cost)"* (raw.githubusercontent.com/qodo-ai/pr-agent, fetched 2026-09-20). No token count, no dollar figure.
- CodeRabbit self-hosting is gated: *"The self-hosted option is available for CodeRabbit Enterprise customers with 500 or more user seats."* You may *"connect CodeRabbit to your own large language model provider or account"* — so you pay the model bill on top of an enterprise licence. Compute requirements are not public (docs.coderabbit.ai/self-hosted/github, fetched 2026-09-20).
- The nearest real compute number is from an adjacent task. Tencent's industrial study of LLM false-positive triage reports **$0.0011–$0.12 in monetary cost** and **2.1–109.5 seconds** per alarm analysed (Du et al., arXiv 2601.18844). This is triage of one static-analysis alarm, not a full PR review — but it establishes that raw inference is one to three orders of magnitude cheaper than the $0.52–$1.67 list prices above.

### 1.4 Annual licence cost at 1,000 developers

*My arithmetic on the list prices in §1.1. Ignores negotiated enterprise discounts and all usage overages.*

| Vendor / tier | Per dev/mo | 1,000 devs/year |
|---|---|---|
| Sourcery Pro | $12 | $144,000 |
| Codacy Team (annual) | $18 | $216,000 |
| CodeRabbit Essentials (annual) | $24 | $288,000 |
| Greptile Pro / Baz | $30 | $360,000 |
| CodeRabbit Team (annual) | $48 | $576,000 |
| CodeRabbit Advanced (annual) | $72 | $864,000 |

Copilot is not comparable in this table because code review is bundled into a plan bought for other reasons — which is itself an argument the chapter should make: **the shared reviewer's licence is often invisible because it rides on a seat the company already bought.**

---

## 2. Noise and triage

### 2.1 The industrial study (corrected citation)

**The brief attributes this to "Bosu et al. 2025." That attribution is wrong.** I queried the arXiv API for all papers by Amiangshu Bosu (23 results, 2020–2026); none is an industrial study of 4,335 pull requests. The numbers in the brief match, exactly, a different paper:

> **Cihan, U., Haratian, V., İçöz, A., Gül, M. K., Devran, Ö., Bayendur, E. F., Uçar, B. M., & Tüzün, E.** "Automated Code Review In Practice." arXiv:2412.18531, submitted 24 December 2024 (v2: 28 December 2024). **To be presented at ICSE 2025, 47th International Conference on Software Engineering, Software Engineering in Practice (SEIP) track.** https://arxiv.org/abs/2412.18531

*Classification: peer-reviewed research (ICSE SEIP track), industrial deployment study.*

Verified figures (arxiv.org/abs/2412.18531, fetched 2026-09-20):

- **4,335 pull requests** studied; **1,568** underwent automated review
- **238 practitioners** across **ten projects**
- Tool: an AI-assisted reviewer based on the open-source **Qodo PR Agent**
- **73.8% of automated comments were resolved**
- **PR closure time rose from 5 hours 52 minutes to 8 hours 20 minutes**
- **22 practitioners** in the broader opinion survey; *"Most practitioners reported a minor improvement in code quality"*

The paper's own framing is that the tool *"enhanced bug detection and code quality awareness while introducing longer closure times and faulty reviews."*

**Read the 73.8% carefully before the chapter leans on it.** "Resolved" is a workflow state, not a verdict on usefulness — and a later paper by an overlapping group says so explicitly (see §2.3).

### 2.2 The largest independent measurement of what developers actually do with AI review comments

> **Lin, H. Y., Liang, M., Thongtanunam, P., & Tantithamthavorn, K.** "Is Agentic Code Review Helpful? Mining Developers' Feedback to CodeRabbit Reviews in the Wild." arXiv:2607.03316, submitted 3 July 2026, revised 23 July 2026. https://arxiv.org/abs/2607.03316

*Classification: preprint, independent academic, large-scale mining study.*

- **31,073 pairs of code reviews and developer feedback, from 10,191 pull requests across 239 GitHub repositories**
- **Accepted: 36.4%** · **Triggered discussion: 7.3%** · **Rejected: 56.3%**
- Rejections stemmed from *"invalid suggestions that were false positives, redundant, or out of scope, as well as misalignment with developer intent and coding practices"*
- *"agentic reviews tend to focus more on functional concerns than evolvability-related comments, yet they were more likely to be invalid"*
- Rejection was predictable at **up to 76% F1** — i.e. the noise has structure, which is a quiet indictment: a filter could have caught it before a human did

### 2.3 Why "resolved" is not "useful"

> **Karakaya, V., Torun, U. B., Uçar, B. M., & Tüzün, E.** "Understanding the Limits of Automated Evaluation for Code Review Bots in Practice." arXiv:2604.24525, submitted 27 April 2026.

*Classification: preprint, independent academic, industrial data (Beko).*

- **2,604 bot-generated PR comments** from Beko, labelled fixed/wontFix by engineers
- G-Eval and LLM-as-a-Judge agreement with human labels: *"Agreement ratios range from approximately 0.44 to 0.62"*
- Conclusion: *developer labelling reflects workflow pressures and organizational constraints rather than objective comment quality*

This is the most load-bearing caveat in this document. A developer marking a bot comment "fixed" under deadline pressure is producing a compliance signal, not a quality signal. **A central owner reporting a high resolution rate may be measuring how hard it is to argue with the bot.**

### 2.4 Other 2026 measurements

> **Cynthia, S. T., Widyasari, R., Roy, B., Zhang, T., & Lo, D.** "'Go Home Copilot, You're Drunk': Understanding Developer Responses to Agent-Generated Code Review Comments." arXiv:2607.21997, 24 July 2026 (rev. 29 July).

*Classification: preprint, independent academic.* **54,791 comments** from five agents (Copilot, Cursor, Codex, Devin, Claude) across **342 Python repositories**. Copilot accounted for **72.9%** of resolved comments. **470 unresolved discussions** were card-sorted into ten patterns; the two most common were **"incorrect suggestions"** and **"intentional design decisions"**. Inline code suggestions were the strongest predictor of a comment being acted on; long, complex comments saw lower engagement.

> **Pereira, K., Sinha, N., Ghosh, R., & Dutta, D.** "CR-Bench: Evaluating the Real-World Utility of AI Code Review Agents." arXiv:2603.11078, 10 March 2026.

*Classification: preprint, independent.* Qualitative but precisely aimed at this chapter's argument: *"code review agents can exhibit a low signal-to-noise ratio when designed to identify all hidden issues, obscuring true progress and developer productivity when measured solely by resolution rates. Our analysis identifies the hidden trade-off between issue resolution and spurious findings, revealing a frontier that constrains effective agent design."* No numerical FP rate is given in the abstract.

> **Zheng, D., Wang, Y., Wang, X., Duan, K., Zhang, H., Liu, X., Ma, Y., & Zheng, Z.** "From Static to Dynamic: Benchmarking Real-World Code Review with MCR-Bench." arXiv:2608.27442, 27 August 2026. **Accepted at ISSTA 2026.**

*Classification: peer-reviewed (ISSTA 2026).* **2,269 real-world multi-round code review tasks** across five languages. Mainstream LLMs show limited defect-detection performance; performance **degrades significantly as interaction rounds increase**; *"semantically complex or low-salience defects"* are frequently missed, attributed to *"cross-round temporal misalignment and inadequate long-range memory."*

> **Cihan, U., İçöz, A., Haratian, V., & Tüzün, E.** "Evaluating Large Language Models for Code Review." arXiv:2505.20206, 26 May 2025.

*Classification: preprint, independent.* 492 AI-generated code blocks plus 164 canonical HumanEval blocks. With problem descriptions, **GPT-4o classified correctness correctly 68.50%** of the time, **Gemini 2.0 Flash 63.89%**. Both declined without descriptions. Roughly a third of verdicts wrong, on a benchmark far cleaner than a real diff.

### 2.5 Vendor precision claims

**Label these as vendor marketing.** They are directionally useful only because they point the same way as the independent data.

- **Greptile** (greptile.com/blog/greptile-v4, 5 March 2026): *"Addressed comments per PR went from 0.92 to 1.60, a 74% increase."* Comment acceptance rate **43%, up from 30%**. Positive replies per PR up 68% to 0.52; upvote reactions up 60%, from 0.05 to 0.08 per PR. **Read the other way: after a major upgrade, 57% of the vendor's own comments are still not addressed — and before it, 70% were not.**
- **Greptile v3** (26 Nov 2025): *"70.5% higher acceptance rates"*, *"256% better upvote/downvote ratios"*; Series A post claims *"3x more critical bugs."* Baselines undisclosed.
- **Cursor Bugbot**: publishes **no** precision or FP claim. Its docs expose an *"Acceptance rate"* analytic to customers — the metric exists, the number is not published (cursor.com/docs/bugbot, fetched 2026-09-20).
- **GitHub** publishes no accuracy figure and instead a disclaimer: *"Copilot is not guaranteed to spot all problems or issues in a pull request. Sometimes it will make mistakes. Always validate Copilot's feedback carefully. Supplement Copilot's feedback with a human review."* (docs.github.com/en/copilot/concepts/agents/code-review, fetched 2026-09-20).

**That last quote is the cheapest and strongest thing in this document.** The vendor of the most widely deployed shared reviewer states in its own documentation that its output requires a human review on top. The shared reviewer does not replace the second pair of eyes; by the vendor's own terms it adds a first pair that must itself be checked.

### 2.6 A triage-cost estimate for the chapter

*My arithmetic, clearly flagged as such, combining two independently sourced figures.* Take Lin et al.'s 56.3% rejection rate. Take Tencent's 10–20 minutes per false alarm (§4.2 — a static-analysis alarm, likely an overestimate for a chatty PR comment, so treat as an upper bound). A 1,000-developer org doing 20,000 reviews/month at, say, three comments per review produces ~60,000 comments, of which ~34,000 are rejected. Even at **two** minutes each — a tenth of Tencent's figure — that is **1,130 engineer-hours per month**. The licence at Greptile list price for the same month is $30,000. **The triage labour is the larger line item by a wide margin, and it is the line item nobody bills.**

---

## 3. Who owns it today

**This is the weakest thread in the document.** Three of the five reports named in the brief could not be verified as existing, and the two that do exist are behind download gates whose landing pages carry only teaser statistics.

### 3.1 What I could verify

**DORA 2025 State of AI-assisted Software Development** (*survey/perception*; cloud.google.com blog + dora.dev, fetched 2026-09-20):
- **Nearly 5,000 technology professionals**, plus over 100 hours of qualitative data
- **90% of respondents report using AI at work**
- **More than 80% believe AI has increased their productivity**
- **70% trust AI-generated code** — i.e. **30% report little or no trust**
- **90% of organizations have adopted at least one platform**, and DORA reports a direct correlation between high-quality internal platforms and the ability to unlock AI value
- Positive relationship between AI adoption and delivery throughput; **negative relationship with delivery stability** absent robust control systems
- Framing: *"AI acts as an amplifier, but the greatest returns come from focusing on the underlying sociotechnical systems."*

**GitLab 2026 Global DevSecOps Survey** (*survey/perception*; about.gitlab.com/developer-survey/, fetched 2026-09-20):
- **3,266 DevSecOps professionals**, 9th annual edition
- Code composition: *"34% AI-generated, 37% written from scratch, 29% copied from other sources"*
- *"83% using AI in the SDLC for multiple daily deployments"*
- **No ownership breakdown was available on the public landing page.** The full report requires form submission.

**BSIMM16** (*industry assessment*; blackduck.com, fetched 2026-09-20): published **January 2026**, covering *"the software security practices of 111 organizations."* **It does not publish an SSG-to-developer ratio on the public page.**

**Enforcement mechanism, verified.** Whoever owns the reviewer can make it mandatory. GitHub documents three levels of enablement for Copilot code review — personal, repository, and **organization/enterprise via rulesets**: *"You can enable automatic code reviews for repositories in your organization and customize how code reviews are performed."* Enterprise admins can create enterprise-level rulesets spanning multiple organizations. **The documentation does not describe a repository-level opt-out once an org ruleset is in place** (docs.github.com/…/configure-automatic-review, fetched 2026-09-20). Cursor is similar in spirit: team admins enable Bugbot per repository, with an allowlist/blocklist and an Admin API for bulk provisioning.

That asymmetry is the chapter's material. **The mandate is one ruleset; the opt-out is a conversation with the team that owns the ruleset.**

### 3.2 What does not exist or could not be reached

- **A 2026 DORA report.** dora.dev/research/ lists 2014–2025 only; `/research/2026/` returns 404. The latest is the 2025 State of AI-assisted Software Development.
- **A 2026 Stack Overflow Developer Survey.** survey.stackoverflow.co's index names 2025 as current; `/2026/` returns 404.
- **Atlassian State of DevEx 2026.** Three candidate URLs, all 404. Not verified to exist.
- **Puppet/Perforce State of DevOps, Platform Engineering Edition 2026.** puppet.com references a "State of DevOps Report: Platform Engineering Edition 2026" but the link target 404s; four candidate URLs failed. The only edition I could actually read was **2023** (11th edition, *"over 400 individuals conducting platform engineering"*, *"nearly 80% of organizations remain in the middle of their DevOps journey"*), which is too old to cite for AI ownership.
- **The ~1:100 AppSec-engineer-to-developer ratio.** I could not source this. arXiv returned **zero** results for "security champions"; OpenAlex returned zero for AppSec staffing ratios and irrelevant IoT surveys for the broader query; BSIMM16's public page does not give it. **Do not use the 1:100 figure in the chapter without a citation I have not been able to find.**

---

## 4. The centralized-security-scanning precedent

This is the strongest analogy available and it is well evidenced across thirteen years.

### 4.1 The original finding — and it was about false positives from the start

> **Johnson, B., Song, Y., Murphy-Hill, E., & Bowdidge, R.** "Why don't software developers use static analysis tools to find bugs?" *2013 35th International Conference on Software Engineering (ICSE)*. DOI: 10.1109/icse.2013.6606613. **529 citations.**

*Classification: peer-reviewed research.* Interviews with **20 developers**. All recognised the value of static analysis; the barriers to adoption were **false positives** and **how warnings are presented**. The paper calls for interactive mechanisms to help developers act on defects.

> **Christakis, M., & Bird, C.** "What developers want and need from program analysis: an empirical study." *ASE 2016* (31st IEEE/ACM International Conference on Automated Software Engineering). DOI: 10.1145/2970276.2970347. **221 citations.**

*Classification: peer-reviewed research.* Multi-method study at Microsoft — interviews, surveys, defect analysis — on what makes an analyser *"most attractive to developers."*

> **Sadowski, C., Aftandilian, E., Eagle, A., Miller-Cushon, L., & Jaspan, C.** "Lessons from building static analysis tools at Google." *Communications of the ACM* 61(4), 2018. DOI: 10.1145/3188720. **240 citations.**

*Classification: peer-reviewed / first-party industrial experience.* The one-line lesson, quoted by OpenAlex from the abstract: **"For a static analysis project to succeed, developers must feel they benefit from and enjoy using it."** For a chapter about who should own the check, this is the whole argument in a sentence — Google's own conclusion after years of central tooling is that *consent*, not *coverage*, is the success condition.

### 4.2 The 2026 data: it has not got better

> **Du, X., Feng, J., Zou, Y., Xu, W., Ma, J., Zhang, W., Liu, S., Peng, X., & Lou, Y.** "Reducing False Positives in Static Bug Detection with LLMs: An Empirical Study in Industry." arXiv:2601.18844, 26 January 2026.

*Classification: preprint, first-party industrial data (Tencent).* Enterprise-customized static analysis tools in Tencent's Advertising and Marketing Services software:

- **433 alarms: 328 false positives, 105 true positives — a 75.8% false-positive rate**
- **10–20 minutes of manual inspection per alarm**
- Hybrid LLM + static analysis *"eliminate 94-98% of false positives with high recall"* at **$0.0011–$0.12** and **2.1–109.5 seconds** per alarm

Read that as the chapter should: **a centrally mandated scanner was generating three false alarms for every real one, and the 2026 state of the art is to buy a second AI system to clean up after the first.** That is central tooling creating work rather than removing it, with a receipt.

Supporting 2026 figures on the same theme, all preprints: Rust memory-safety analysers Rudra and MirChecker *"suffer from high false positive rates, which diminish developer trust, increase manual review effort, and may obscure genuine vulnerabilities"* — precision improved from **25.6% to 59.0%** by an RL method (arXiv 2605.04000). A multi-agent Semgrep wrapper cut false positives **from 560 to 64 (88.6%)** for a 3.1% recall loss (arXiv 2605.01885). A survey of **72 security practitioners** found three SAST tools flagged 114 of 135 validated instances but agreed on CWE mapping only **6.42%** of the time (arXiv 2602.03470) — three central scanners, three different answers.

### 4.3 What I could not get from OWASP and NIST

The brief asks for OWASP Benchmark and NIST SATE results. Both are less usable than expected:

- **OWASP Benchmark** (owasp.org/www-project-benchmark, fetched 2026-09-20) describes test suites and scoring (Youden Index) but **publishes no per-tool TPR/FPR figures on the project page**. Java Benchmark is still **v1.2, released 2016**; Python is v0.1 with v1.0 planned for *"early 2026"* — a ten-year-old benchmark is weak evidence about 2026 tools.
- **NIST SATE** (nist.gov, fetched 2026-09-20) is explicitly *"a recurring non-competitive study"* — by design it does not rank tools or publish per-tool precision. The most recent edition is **SATE VI, September 2019**.

**Use the Tencent study instead.** It is recent, industrial, and gives a hard number.

---

## 5. Exit and lock-in

**I found almost no published evidence here, and I want to be blunt about it rather than pad the section.** No migration account, no cost-of-leaving study, no report of an internal platform team being disbanded turned up through the fetch-only method available. What follows is the small set of verified facts about the *shape* of the lock-in, not its cost.

**Verified facts:**

- **Seat definitions make cost scale with adoption, not with usage.** Greptile: a seat is *"any developer who has gotten a review done by Greptile in that billing period."* Baz charges *"$30 per active developer per month."* Under a central mandate that runs on every repository, **every developer becomes an active developer**, and the org loses the ability to shrink the bill by narrowing scope. This is the mechanism by which a mandate converts an opt-in tool's price into a headcount tax.
- **Review history is retained by the vendor, and no vendor I checked documents an export path.** CodeRabbit: *"After cancellation, review history and configuration are retained"* (docs.coderabbit.ai/getting-started/subscription-management, fetched 2026-09-20). Retained by whom, in what format, and exportable how, is not stated.
- **Self-hosting is gated by size.** CodeRabbit's self-hosted option requires *"500 or more user seats"* on Enterprise. The escape hatch from vendor dependency is available only to organizations already deeply committed.
- **Enablement is centrally enforceable and the opt-out is undocumented** (see §3.1). GitHub documents how an enterprise admin mandates Copilot review across organizations; it does not document how a single repository declines.
- **Portability varies by where comments live.** Copilot, CodeRabbit and Greptile post into the GitHub PR, so the *comments* survive a vendor change as ordinary PR history. Graphite and Baz operate their own review surfaces; Graphite's docs do not state whether AI review comments are mirrored to GitHub (graphite.com/docs/ai-reviews, fetched 2026-09-20). **The chapter can fairly say that the review conversation is portable where the tool writes into the forge and unverified where it does not.**

**Adjacent evidence on central platforms becoming the constraint** — the closest I could get:

> **Lertpongrujikorn, P., Nguyen, H. D., & Amini Salehi, M.** "Empirical Analysis of Cloud-Edge Infrastructure Complexity: Practitioner Pain Points and Architectural Directions." arXiv:2608.08400, 9 August 2026.

*Classification: preprint, independent, interview study.* **101 semi-structured interviews across 86 organizations.** *"deployment complexity (38.6%) and onboarding difficulty (35.6%)"* are the dominant operational bottlenecks; developers prioritise *"productivity (53.5%) and automation (44.6%)"*. The paper concludes that **infrastructural complexity, not execution performance, is the primary adoption barrier** for internal developer platforms. It is about infrastructure, not code review, and should be cited as an analogy at most.

---

## 6. Correlated blind spots

This thread turned out to be the best-evidenced of the six, and it is the one that most directly undermines the case for a single shared reviewer.

### 6.1 The foundational result

> **Panickssery, A., Bowman, S. R., & Feng, S.** "LLM Evaluators Recognize and Favor Their Own Generations." arXiv:2404.13076, 15 April 2024.

*Classification: peer-reviewed-track research (NeurIPS 2024); figures below from the full text via ar5iv, fetched 2026-09-20.*

Abstract, verbatim in part: *"One such bias is self-preference, where an LLM evaluator scores its own outputs higher than others' while human annotators consider them of equal quality… We discover that, out of the box, LLMs such as GPT-4 and Llama 2 have non-trivial accuracy at distinguishing themselves from other LLMs and humans. By fine-tuning LLMs, we discover a linear correlation between self-recognition capability and the strength of self-preference bias; using controlled experiments, we show that the causal explanation resists straightforward confounders."*

- **GPT-4: 73.5% accuracy** at distinguishing its own output in the pairwise setting; GPT-3.5 and Llama 2 above 50%
- After fine-tuning on **500 examples**, *"GPT-3.5 and Llama 2 both achieve over 90% accuracy at self-recognition"*
- Example-level **Kendall's τ between self-recognition and self-preference: 0.37 to 0.82**, depending on model and dataset
- Datasets: **XSUM** and **CNN/DailyMail**, 1,000 news articles each (500 train / 500 eval); models GPT-4, GPT-3.5 Turbo, Llama-2-7b-chat

Note the domain: **summarization, not code.** Cite it as the mechanism, not as evidence about code review.

### 6.2 The code-specific measurement, with numbers

> **Caridad, R.** "Models are worse at reviewing their own code." Greptile blog, **21 July 2026**. https://www.greptile.com/blog/model-inversion

*Classification: **vendor-published research** — Greptile sells the feature this study justifies. Method is disclosed; treat the numbers as directional and the conclusion as commercially motivated.*

Method: two datasets of **500 PRs each** (one Claude-authored, one Codex-authored), ~**1,500 ground-truth bug comments** total. Authors: Claude Opus 4.7 and Codex. Reviewers: Claude Opus 4.7 and GPT 5.5. Three review runs per PR; recall measured by matching against ground truth with an LLM judge; high-severity bugs only.

| Reviewer | Recall on **cross-family** PRs | Recall on **own-family** PRs | Gap |
|---|---|---|---|
| Claude Opus 4.7 | **62.0%** (Codex-authored) | **53.7%** (Claude-authored) | 8.3 pts |
| GPT 5.5 | **60.0%** (Claude-authored) | **50.5%** (Codex-authored) | 9.5 pts |

The stated mechanism: *"the types of bugs a model introduces most often are the same types it's more likely to miss."* Secondary findings: Opus spends **59.4%** of context in a breadth-first "Scope" phase, GPT **82.5%** in a depth-first "Investigate" phase; GPT was observed identifying bugs in its reasoning trace and omitting them from the final review.

**This is the number the chapter needs.** Standardising on one reviewer for every repository does not just risk a blind spot — it *guarantees* the blind spot is aligned with whatever model the organization's developers are generating code with, and costs roughly **8–10 points of recall on high-severity bugs** relative to picking a different family.

### 6.3 Self-review collapse

> **Song, X., Cai, Z., & Zhao, L.** "When AI Reviews Its Own Code: Recursive Self-Training Collapse in Code LLMs." arXiv:2606.28438, 26 June 2026. Status: under review.

*Classification: preprint, independent.* Three gatekeeping regimes compared: none, human-controlled filters (compilation, static analysis), and AI self-review (perplexity, self-scoring). Findings: *"no review collapses fastest"*; human filters *"slow but do not stop collapse"*; AI self-gating shows **"acceptance scores rise while benchmark correctness falls"**, with the binary self-gate entering a **"rubber-stamp regime."** Conclusion: *"stable recursive code LLM training requires exogenous verification rather than model-coupled self-review."*

The abstract does not give the numeric magnitude of the correctness drop; I did not retrieve the full text. **Cite the qualitative finding, not a number.**

### 6.4 Supporting

> **Zietsman, C.** "The Specification as Quality Gate: Three Hypotheses on AI-Assisted Code Review." arXiv:2603.25773, 26 March 2026.

*Classification: preprint, single author, explicitly directional.* Argues AI code review is *"structurally circular when executable specifications are absent"* because *"both the generating agent and the reviewing agent reason from the same artefact, share the same training distribution, and exhibit correlated failures"*, and that errors in homogeneous pipelines **"echo rather than cancel."** Tests span same-family (Claude reviewing Claude) and a cross-family panel of four models across three families. **The author states the experiments use a planted-bug corpus rather than natural defects and describes the evidence as directional, not controlled.** Useful for framing; do not present as a result.

> **Vargas, M. J. T.** "SLEAN: Simple Lightweight Ensemble Analysis Network." arXiv:2510.10010, 11 October 2025.

*Classification: preprint, small sample — 15 bugs, 69 AI propositions, 31.9% acceptance.* Reports that agreement between AI systems had *"weak correlation with fix quality"*, improving acceptance by only **2.4 percentage points**. Sample is too small to lean on, but it points the same way: **consensus between models is not evidence of correctness when the models share a prior.**

### 6.5 Volume, for context

> Greptile, "A statistical study of PRs opened on openclaw/openclaw," **8 May 2026**. https://www.greptile.com/blog/prs-on-openclaw

*Classification: vendor-published analysis of a public repository.* PR volume went from *"two pull requests a week"* in December to **3,400/week** in February. Merge rate fell from **~48% to "fewer than 9.3%."** One contributor opened **106 PRs in a single day, median three seconds apart.** First-time contributors merged at **8.2%**, 2–5 PR contributors at **10.3%**, 5+ at **18.6%**. Features merged at **9%**, refactors at **35%**. Four contributors independently submitted identical feature requests; six separately fixed the same bug, two with *"identical titles 94 minutes apart"*.

The duplicate-submission detail is the interesting one for this chapter: **independent AI contributors converged on the same work.** That is the same correlation as §6.2, observed on the generation side.

---

## What I could not verify

Listed so nothing below is mistaken for a gap in the evidence rather than a gap in my access.

**Method limitation, first.** The session's WebSearch budget was fully consumed before this task started. Everything here came from URLs I could guess or construct, plus the arXiv and OpenAlex APIs. I could not run discovery searches, so **absence of a finding below is not evidence of absence in the literature.**

1. **"Bosu et al. 2025" as cited in the brief does not exist.** The 4,335-PR / 73.8% / 5h52m→8h20m study is Cihan et al., arXiv 2412.18531, ICSE 2025 SEIP. Amiangshu Bosu's arXiv record (23 papers, checked 2026-09-20) contains nothing matching. Correct the citation before publishing.
2. **No published token or compute cost per self-hosted review, from any vendor.** Qodo's PR-Agent says only *"a single LLM call (~30 seconds, low cost)."* The Tencent per-alarm figures ($0.0011–$0.12) are for static-analysis triage, a different and smaller task.
3. **No 2026 DORA report.** dora.dev lists 2014–2025; `/research/2026/` is 404.
4. **No 2026 Stack Overflow Developer Survey** visible; the site index names 2025 as current, `/2026/` is 404.
5. **Atlassian State of DevEx 2026** — could not confirm it exists. Three URLs, all 404.
6. **Puppet/Perforce State of DevOps Platform Engineering Edition 2026** — referenced on puppet.com, link target 404. Only the 2023 edition was readable (400+ respondents), too old to use.
7. **The ~1:100 AppSec-engineer-to-developer ratio has no source I could find.** arXiv: zero results for "security champions". OpenAlex: nothing relevant. BSIMM16 (111 firms, January 2026) does not publish an SSG:developer ratio publicly. **Do not use this figure.**
8. **GitLab 2026 DevSecOps ownership breakdown** — the public landing page gives only three statistics (3,266 respondents; 34/37/29 code-origin split; 83% AI-in-SDLC). Ownership, trust and review-time figures are behind a form.
9. **DORA 2025 full report** — the PDF exceeded the fetch size limit. All DORA figures here come from the Google Cloud announcement blog and dora.dev landing pages, not the report body.
10. **Graphite "Diamond" does not appear to exist as a named product** in September 2026. AI Reviews are bundled into Graphite's $40/user/month Team tier.
11. **Cursor Bugbot's per-review price is not published.** Only *"usage-based billing"* and *"Bugbot first consumes your included usage, then bills additional reviews through on-demand spend."*
12. **OWASP Benchmark publishes no per-tool FP rates** on its project page, and its Java suite is v1.2 from 2016. **NIST SATE is non-competitive by design** and its most recent edition is SATE VI (September 2019). Neither yields a usable 2026 SAST false-positive number; the Tencent study does.
13. **Exit and lock-in is essentially unevidenced in public.** No migration account, no cost-of-switching study, no report of a central review platform being retired or a platform team disbanded. Section 5 documents the *shape* of the lock-in from vendor terms only.
14. **Whether Graphite or Baz mirror AI review comments into GitHub** is not stated in their public docs — so the portability of review history for those two tools is unknown, not confirmed absent.
15. **The magnitude of the correctness drop in "When AI Reviews Its Own Code"** is not in the abstract and I did not retrieve the full text. Cite qualitatively.
16. **Semantic Scholar's API returned HTTP 429 on every attempt** (four tries, spaced). The two classic SAST-adoption citations (Johnson 2013, Christakis & Bird 2016) were verified through OpenAlex instead, which supplied title, authors, year, venue, DOI and citation count but only a paraphrased abstract — so the Johnson and Christakis "abstracts" in §4.1 are OpenAlex summaries, not verbatim text. The one verbatim sentence I quote is from Sadowski et al. 2018.
