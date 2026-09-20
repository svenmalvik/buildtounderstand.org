# Central review reversals, central vs team review, and the AppSec ratio

Research date: 2026-09-20. All sources below were fetched on 2026-09-20 unless noted.

**Method note / limitation up front.** The session's `WebSearch` budget (200 calls) was
already exhausted before this task started. All work below was done with `WebFetch`
against search-engine HTML and against primary documents. Most search engines blocked
the fetch (DuckDuckGo CAPTCHA, Mojeek 403, Startpage blocked, Ecosia 403, Bing RSS
returned navigational junk). Brave Search worked for roughly ten queries and then
rate-limited (HTTP 429) for the rest of the session. So the search surface here is
narrower than it should be, and GAP 1 in particular is **not** closed. A delayed retry
(4-minute backoff, then three queries 25s apart) still returned HTTP 429 on all three, so
Brave was unavailable for the remainder of the session. The arXiv and Hacker News Algolia
APIs were reachable and were used as substitutes; Semantic Scholar rate-limited after two
queries. See "What I could not verify".

---

## Main findings

- **BSIMM16 (Jan 2026, 111 firms, 223,700 developers) gives a real, primary-source
  number for the AppSec ratio.** Median SSG-members-per-100-developers is **1.8**
  across all firms, and **1.13** for firms with 650+ developers — i.e. roughly
  **1 security engineer per 88 developers** at larger firms. The commonly cited
  "1:100" is in the right ballpark but is almost never sourced to this.
- **The strongest firms have *smaller* central security teams, not bigger ones.**
  BSIMM16: bottom-20% firms average an SSG-to-developer ratio of **6.8**; top-20%
  firms average **2.7**. The top firms compensate with champions (**12.3** vs **4.6**
  per 100 developers). BSIMM's own authors say they cannot tell cause from effect.
- **BSIMM16 states the "push the check into the team" argument explicitly**: having
  champions do the work "removes SSG members from the engineering-critical path and
  empowers engineering teams to own their software security deliverables."
- **Cloudflare (Apr 2026) is a live, first-party example of exactly the shared-reviewer
  design the essay is about**, with numbers: one company-wide AI reviewer, 131,246
  review runs / 48,095 merge requests / 5,169 repositories in 30 days, median review
  3m39s, ~1.2 findings per review, and a break-glass override used **288 times (0.6%
  of merge requests)**. It blocks merges. Teams customise via `AGENTS.md`.
- **Postman (Apr 2026) is a documented *narrowing* of a central security gate**, with
  numbers: 25% of releases auto-unblocked, ~2 business days removed from average
  per-review closure time, 3 business weeks of AppSec capacity freed per half-year.
  They did not abolish the gate — they made it risk-adaptive.
- **Peer-reviewed evidence says no single reviewer is sufficient, and expertise does
  not predict who finds what.** Edmundson et al. (ESSoS 2013, 30 reviewers, 7 known
  vulnerabilities): no reviewer found all seven; the best found five; 20% found none;
  average 2.33; years of security experience had **no** statistically significant
  correlation with effectiveness. ~10 independent reviewers ≈ 80% chance of finding
  everything; ~15 ≈ 95%.
- **Review *coverage* affects security bugs; review *participation* (depth, more
  commenters) does not.** Thompson & Wagner (PROMISE'17, 3,126 GitHub projects,
  382,771 PRs): halving unreviewed PRs predicts ~6% fewer security bugs, but the
  average number of commenters per PR had no significant relationship with security
  bugs.
- **A single shared AI reviewer is a single point of attack, and the asymmetry favours the
  attacker.** Preprint (arXiv 2603.18740v3, Mar 2026) evaluating 33 CVEs across 20 projects
  against Claude Code and CodeRabbit review pipelines: an iterative "refinement attack" that
  crafts PR metadata to bias the reviewer succeeded in **32/33 (97%)** cases, because
  "attackers can iteratively refine attacks against a local clone of the review pipeline,
  while defenders have only one chance to detect them."
- **Finding a security problem in review is not the same as fixing it.** Peer-reviewed study
  of **135,560 code review comments** in OpenSSL and PHP: reviewers raised security concerns
  in 35 of 40 coding-weakness categories, but only **39-41%** of raised concerns were
  addressed; **30-36%** were "merely acknowledged" and **18-20%** went unfixed due to
  disagreement about the solution. Whoever owns the check does not necessarily own the fix.
- **I did NOT find a clean, documented case of a company building a central code
  review / AppSec / architecture review function and then dismantling it.** The
  closest verified case is Postman narrowing a gate. See "What I could not verify".

---

## GAP 3 — The AppSec-engineer-to-developer ratio

### Primary source: BSIMM16 report (2026)

- **Type:** vendor-published industry study, but based on structured first-party
  assessments of named participating firms; the closest thing to a census that exists.
  Published by Black Duck (formerly Synopsys). Not peer-reviewed.
- **URL:** https://www.blackduck.com/content/dam/black-duck/en-us/reports/bsimm-report.pdf
  (redirects to https://assets.blackduck.com/image/upload/bsimm-report.pdf)
- **Fetched:** 2026-09-20. PDF downloaded and text-extracted locally with `pdftotext`.
- **Published:** January 2026 (the landing page says "The BSIMM16 report, published in
  January 2026"). Report cover reads "BSIMM16 REPORT 2026".

**Sample and method (verbatim):**

> "Unique in the software security industry, the BSIMM project has grown from nine
> participating companies in 2008 to 111 in 2026, with approximately 3,700 software
> security group (SSG) members and 6,500 security champions. The average age of
> participants' SSIs is 5.6 years, but the BSIMM project shows consistent growth even
> as participants enter and leave over time—we added 16 firms for BSIMM16 and dropped
> 26 others whose data hadn't been refreshed."

> "The BSIMM trends and insights we've identified are a distillation of software
> security lessons learned across 111 organizations that collectively have 10,200
> security professionals helping about 223,700 developers do good security work on
> about 91,200 applications."

Method: BSIMM is an observational assessment — assessors interview a firm and record
which of ~125 activities they observe. Participation is voluntary and self-selecting
(firms that pay for or agree to a maturity assessment). **This is not a random sample
of the industry**; it skews toward firms that already have a software security group.

**Table 6, "THE SOFTWARE SECURITY GROUP" (BSIMM16 p.41), verbatim rows:**

| Statistic | Average | Median | Largest | Smallest | Notes (verbatim) |
|---|---|---|---|---|---|
| SSG Size | 33.5 | 10 | 892 | 1 | "Average drops to 25.7 (one outlier)" |
| Number of Developers | 2,038.3 | 650 | 30,000 | 1 | |
| Number of Applications | 820.5 | 100 | 15,000 | 1 | "Average drops to 691.6 (one outlier)" |
| SSG Age | 5.6 | 4.5 | 23 | 0.1 | |
| **SSG Members-to-Developer Ratio (per 100 Developers)** | **5.6** | **1.8** | 100 | 0.02 | "Average drops to 4.8 (one outlier)" |
| **SSG-to-Developer Ratio (650+ Developers) - 56 Firms** | **1.79** | **1.13** | 14.87 | 0.02 | |
| SSG-to-Developer Ratio (less than 650 Developers) - 55 Firms | 9.54 | 3.33 | 100 | 0.33 | |
| **Champions-to-Developer Ratio (per 100 Developers)** | **5.9** | **1.2** | 102.2 | 0 | "Average drops to 4.8 (two outliers)" |
| Champions-to-Developer Ratio (650+ Developers) - 41 Firms | 5.81 | 3 | 25.63 | 0.03 | "Only includes firms with champions" |
| Champions-to-Developer Ratio (less than 650 Developers) - 24 Firms | 17.5 | 6.43 | 102.2 | 0.2 | "Only includes firms with champions" |

Table caption, verbatim:

> "Table 6. THE SOFTWARE SECURITY GROUP. We calculated the ratio of full-time SSG
> members and champions to developers and applications for the entire data pool by
> averaging the individual ratio for each participating firm. In the 'Notes' column,
> we show the impact of removing outliers in the data."

**What this means for the "1:100" claim.** BSIMM16 does not print "1:100" anywhere.
The number closest to it is the **median SSG-to-developer ratio for firms with 650+
developers: 1.13 per 100 developers, i.e. about 1 security engineer per 88
developers.** The all-firms median is 1.8 per 100 (≈1:56), and the all-firms *average*
is 5.6 per 100 (≈1:18) — but the average is badly skewed by small firms (firms with
<650 developers average 9.54 per 100). **Use the median, and say which cut you are
using.** Averages and medians differ by a factor of three here.

Note the whole-pool arithmetic as a cross-check: 3,700 SSG members ÷ 223,700
developers = 1.65 per 100 (≈1:60). This is a pool-level ratio, not the average of
per-firm ratios, and differs from Table 6's figures for that reason.

### Where the "1:100" folk number actually comes from — traceable but weakly

- **BSIMM8 (2017)** is the origin of a widely-repeated "1.6 per 100 developers" figure.
  BSIMM8 PDF fetched 2026-09-20 from
  https://apothecaryshed.com/wp-content/uploads/2025/09/bsimm8.pdf (a third-party
  mirror; the report is CC BY-SA 3.0 licensed, which is why mirrors exist).
  Verbatim from BSIMM8: "We present the BSIMM8 model as built directly out of data
  observed in 109 software security initiatives."
  Secondary sources give the totals as 1,268 SSG members + 3,501 satellite for
  290,582 developers.
- **Secure Code Warrior** (vendor blog, Matias Madou, 2017-10-09,
  https://www.securecodewarrior.com/article/what-security-practices-do-300-000-developers-really-do,
  fetched 2026-09-20) states verbatim: **"BSIMM8 reports that this number is even
  less, now at 1.6 per 100 developers."** Note 1,268 ÷ 290,582 = 0.44 per 100, while
  (1,268 + 3,501) ÷ 290,582 = 1.64 per 100 — so the "1.6" almost certainly counts
  **SSG + satellite combined**, not security engineers alone. Vendor blogs that repeat
  "1.6 per 100" as an AppSec-headcount ratio are misreading it.
- **Practitioner restatements of "1:100" are unsourced.** Example:
  https://dev.to/instasla/how-to-build-a-security-champions-program-driven-by-alert-accountability-2872
  (dev.to, vendor-authored), snippet: "The staffing gap varies, but the number cited
  most consistently across the industry lands around one AppSec professional for every
  100 developers." No citation given. Treat "1:100" as folklore that **happens** to
  land close to BSIMM16's large-firm median (1.13 per 100) — say that, rather than
  citing "1:100" as if it had a source.

---

## GAP 2 — Central security review vs team review

### 2a. BSIMM16 on central teams vs champions — the single most useful finding

Verbatim, BSIMM16 "DATA ANALYSIS: SECURITY CHAMPIONS" (p.83):

> "In Figure 23, the orange line shows that firms can achieve higher scores even with a
> lower ratio of SSG to developers (e.g., the bottom 20% have an average SSG-to-developer
> ratio of 6.8 while the top 20% have an average SSG-to-developer ratio of 2.7). One way
> these firms are able to scale is by increasing the ratio of champions to developers, as
> shown by the teal bars (e.g., the bottom 20% have an average champions-to-developer
> ratio of 4.6 while the top 20% have an average champions-to-developer ratio of 12.3)."

> "While the presence of a champions program doesn't guarantee a high number of activity
> observations, there is a correlation that appears when grouping BSIMM firms by scores.
> Nearly 96% of firms in the highest-scoring group have a champions program as compared to
> 30% in the lowest-scoring group. Figure 24 shows the score increases from an average of
> 22.4 activities in the lowest-scoring group (shown on the orange line), up to an average
> of 76.9 activities in the highest-scoring group (shown here as the top 20%)."

**BSIMM's own caveat, verbatim (Figure 24 caption) — quote this if you use the finding:**

> "Presence of a champions program and average score (scale on the right) appear to be
> correlated, but we don't have enough data to say which is the cause and which is the
> effect."

**A second caveat the essay must carry:** the BSIMM "score" is a count of observed
activities out of ~125, not a measure of defects found, vulnerabilities escaped, or
breaches avoided. A higher score means "does more of the things BSIMM tracks". It is
**not** evidence that distributed review catches more bugs than central review. It is
evidence that mature programmes are structured with a small centre and a wide edge.

Also verbatim, BSIMM16 "SECURITY CHAMPIONS" (p.42) — this is the argument for pushing
the check back into the team, stated by a mainstream industry source:

> "Champions can enable an SSI to scale its efforts while reducing dependency on the SSG
> team, and there appears to be a correlation between a higher BSIMM score and the presence
> of champions, as shown in Figure 13. Having security champions carry out software security
> activities removes SSG members from the engineering-critical path and empowers engineering
> teams to own their software security deliverables and share responsibility for software
> security objectives."

Distribution of champions programmes, verbatim (BSIMM16 p.82):

> "Many firms with no champions continue to exist in the data pool, which causes the overall
> median champions size to be nine (46 of 111 firms had no champions at the time of their
> current assessment). The median champion size is 45 for the firms with champions programs"

> "For the 65 BSIMM16 firms with champions at their last assessment time, the average
> champions size was 100, with a median of 45."

Figure 13, verbatim: bottom 20% — "30% of the bottom 20% of firms have champions";
middle 60% — "55%"; top 20% — "96% of the top 20% of firms have champions".

### 2b. No single reviewer finds everything, and expertise does not predict who does

**Edmundson, Holtkamp, Rivera, Finifter, Mettler, Wagner, "An Empirical Study on the
Effectiveness of Security Code Review."**

- **Type:** peer-reviewed conference paper, ESSoS 2013 (International Symposium on
  Engineering Secure Software and Systems). Springer LNCS.
- **URL:** https://people.eecs.berkeley.edu/~daw/papers/coderev-essos13.pdf
- **Fetched:** 2026-09-20 (PDF, text-extracted locally).

Method, verbatim from the abstract:

> "We hired 30 developers to conduct a manual code review of a small web application. The
> web application supplied to developers had seven known vulnerabilities, including three
> different types: Cross-Site Scripting, Cross-Site Request Forgery, and SQL Injection. Our
> findings include: (1) none of the subjects found all confirmed vulnerabilities, (2) more
> experience does not necessarily mean that the reviewer will be more accurate or effective,
> and (3) reports of false vulnerabilities were significantly correlated with reports of
> valid vulnerabilities."

Results, verbatim:

> "The average number of correct vulnerabilities found was 2.33 with a standard deviation of
> 1.67."

> "Twenty percent of the reviewers in our sample found no true vulnerabilities, and no
> developer found more than five out of the seven known vulnerabilities."

> "only 17% of the reviewers found the lack of Cross-Site Request Forgery protection"

On how many reviewers you need, verbatim:

> "In order to determine the optimal number of reviewers, we simulated hiring various numbers
> of reviewers. In each simulation, we randomly chose X reviewers, where 0 ≤ X ≤ 30, and
> combined all reports from these X reviewers. This is representative of hiring X independent
> reviewers. For a single trial within the simulation, if this combination of reports found
> all seven vulnerabilities, then the trial was considered a success; if not, it was
> considered a failure. We conducted 1000 trials for a single simulation and counted the
> fraction of successes; this estimates the probability of finding all vulnerabilities with X
> reviewers. Figure 4 shows the probability of finding all vulnerabilities based on the
> number of developers hired. For example, 10 reviewers have approximately an 80% chance of
> finding all vulnerabilities, 15 reviewers have approximately a 95% chance of finding all
> vulnerabilities, and it is probably a waste of money to hire more than 20 reviewers."

On expertise, verbatim:

> "Our results did not indicate any correlations between self-reported demographic information
> and reviewer effectiveness. None of the characteristics listed in Appendix A had a
> statistically significant correlation with the number of correct vulnerabilities reported."

> "Typical hiring practices include evaluation of a candidate based on his education,
> experience, and certifications, but according to this data it does not have a significant
> impact on the effectiveness of the developer's review."

> "Our results revealed that years of experience and education were not useful in predicting
> how well a subject was able to complete the code review. We also found that the subject's
> own opinion of how well they performed showed no correlation with how effective their report
> was."

**Limits — state these if you use it.** n=30, freelancers hired via a labour-outsourcing
site, one small PHP application (Anchor CMS), seven vulnerabilities of three types, 2013.
The paper does **not** compare a central security function against an implementing team;
it compares individual reviewers against each other. What it supports is narrower and
more interesting: **a single designated reviewer — however expert — is the wrong unit,
because the variance between reviewers is large and is not predicted by expertise.** That
argues against "one reviewer for the whole company" as a *quality* claim, while leaving
the *consistency* claim untouched.

### 2c. Coverage beats depth, for security specifically

**Thompson & Wagner, "A Large-Scale Study of Modern Code Review and Security in Open
Source Projects."**

- **Type:** peer-reviewed conference paper, PROMISE'17, November 8, 2017, Toronto.
- **URL:** https://people.eecs.berkeley.edu/~daw/papers/coderev-promise17.pdf
- **Fetched:** 2026-09-20 (PDF, text-extracted locally).

Method, verbatim:

> "We gather a very large dataset from GitHub (3,126 projects in 149 languages, with 489,038
> issues and 382,771 pull requests), and use a combination of quantification techniques and
> multiple regression modeling to study the relationship between code review coverage and
> participation and software quality and security."

Results, verbatim:

> "Halving the number of unreviewed pull requests we would expect to see 6% fewer security
> bugs."

> "We do not find a significant relationship between the average number of commenters on pull
> requests and the number of security bugs. This result is in contrast with that found by
> Meneely et al."

Conclusion, verbatim:

> "Our results indicate that code review coverage has a small but significant effect on both
> the total number of issues a project has and the number of security bugs. Additionally, our
> results indicate that code review participation has a small but significant effect on the
> total number of issues a project has, but it does not appear to have an effect on the number
> of security bugs. Overall, code review appears to reduce the number of bugs and number of
> security bugs."

**Limits, in the authors' words:** "sampling from GitHub limits us to open source software
projects. Commercial or closed source projects may exhibit different characteristics." They
also note weak ground truth: "We used one coder, and there is some grey area in our
definition." Effect sizes are explicitly described as "small but significant".

**Why this matters for the essay.** If coverage is what moves security outcomes and depth
of human participation is not, then the argument for a shared reviewer is a **coverage**
argument, not a **quality** argument. A cheap reviewer that looks at 100% of changes is
supported by this evidence; an expensive central board that looks at 10% deeply is not.

---

## GAP 1 — Documented reversals of central review

### 1a. Postman: a central security gate narrowed, with numbers (CLOSEST MATCH FOUND)

- **Type:** first-party company engineering blog.
- **URL:** https://blog.postman.com/how-we-scaled-security-reviews-without-slowing-down-engineering/
- **Author / date:** Anurag Mewar, **2026-04-22**. Fetched 2026-09-20.

The old model: a mandatory VAPT (Vulnerability Assessment & Penetration Testing) Jira
ticket plus a security test plan for qualifying releases. Problems they name:

> "Late architectural and implementation questions on certain releases"
> "Compressed timelines for meaningful manual security review"
> "Crunch mode for the AppSec team"
> "Major security findings surfacing as release blockers, impacting delivery schedules"

Measured results after the change:

> "25% of Releases Auto-Unblocked: 1 in 4 service releases now move from staging to
> production"
> "Removed 2 business days of average per-VAPT closure time for qualifying releases"
> "22 developer and security work-hours per quarter saved in reduced context switching"
> "3 full business weeks of AppSec team capacity freed up every half-year"

**Important: this is a narrowing, not a reversal.** They kept the gate and made it
risk-adaptive: low-risk releases auto-close when triage shows no sensitive change;
high-criticality services still require mandatory manual review. The post gives no
absolute AppSec headcount, no engineering headcount, and no pre-change blocking rate,
so the percentages have no denominator you can check. Self-reported, not independently
measured.

### 1b. Cloudflare: a company-wide shared AI reviewer, running now, with numbers

This is not a reversal — it is the strongest available data point on what a shared
reviewer actually costs and does at scale, which the section needs regardless.

- **Type:** first-party company engineering blog.
- **URL:** https://blog.cloudflare.com/ai-code-review/
- **Author / date:** Ryan Skidmore, **2026-04-20**. Fetched 2026-09-20.

Verbatim:

> "In the first 30 days, the system completed 131,246 review runs across 48,095 merge
> requests in 5,169 repositories."

> "the median review completes in 3 minutes and 39 seconds."

> "That is about 1.2 findings per review on average, which is deliberately low."

> "engineers have only needed to 'break glass' 288 times (0.6% of merge requests)."

> "It approves clean code, flags real bugs with impressive accuracy, and actively blocks
> merges when it finds genuine, serious problems or security vulnerabilities."

> "teams can opt to provide a URL to an AGENTS.md template that gets injected into all agent
> prompts to ensure their standard conventions apply across all of their repositories without
> needing to keep multiple AGENTS.md files up to date."

**Why this is load-bearing.** It is a shared reviewer that (a) is genuinely central —
one system, 5,169 repositories; (b) genuinely blocks; (c) has a documented local escape
hatch; and (d) publishes the escape-hatch usage rate. 0.6% is the number to argue with:
either it shows the shared reviewer is almost always right, or it shows the override is
socially expensive and under-used. The post does not distinguish these. It also does not
report false-negative rate, cost, or how many of the 1.2 findings per review were acted
on — so "impressive accuracy" is the author's assessment, not a measurement.

### 1c. Netflix "paved road" — the model is advisory, but I could not verify the primary text

The Netflix AppSec "paved road" is the canonical reference for optional-rather-than-
mandatory central security tooling. I was **unable to fetch the primary sources**:
`netflixtechblog.com/scaling-appsec-at-netflix-6a13d7ab6043` returned HTTP 403, the
Medium mirror returned 403, and a reader-proxy attempt hit a CAPTCHA. A Brave search
snippet for a SlideShare deck ("The Paved Road at Netflix") read: "The Paved Road
provides integrated, supported tools and services to help engineers focus on delivering
business value. It is not mandatory for teams to use." **I did not fetch that deck and
cannot confirm the quote, its date, or its author.** Do not cite this until verified.

---

## Additional evidence found via the arXiv API (search engines were blocked)

### The monoculture cost of one shared reviewer

**"Measuring and Exploiting Contextual Bias in LLM-Assisted Security Code Review."**

- **Type:** preprint, NOT peer-reviewed. arXiv 2603.18740v3.
- **URL:** http://arxiv.org/abs/2603.18740v3
- **Date:** submitted 2026-03-19 (v3). Retrieved via the arXiv API on 2026-09-20.

Abstract, verbatim in the load-bearing parts:

> "we first conduct a large-scale exploratory study across 6 LLMs under five framing
> conditions, establishing the framing effect as a systematic and widespread phenomenon in
> LLM-based vulnerability detection. We then design a realistic and controlled experimental
> environment, evaluating 33 CVEs across 20 real-world projects and two popular ACR pipelines
> (Claude Code and CodeRabbit), to assess the susceptibility of real-world ACR pipelines to
> vulnerability re-introduction attacks."

> "We find that template-based attacks are ineffective and may even backfire, as direct
> biasing attempts raise suspicions. Our refinement attack, on the other hand, is successful
> in 32/33 (97%) cases, exploiting a fundamental asymmetry: attackers can iteratively refine
> attacks against a local clone of the review pipeline, while defenders have only one chance
> to detect them."

> "Overall, our findings highlight the dangers of over-relying on ACR and stress the
> importance of human oversight and contributor trust in the development process."

**Why this is load-bearing for the essay.** This is the sharpest available argument against
one reviewer for the whole company, and it is not an efficiency argument — it is a
correlated-failure argument. A single shared reviewer is a *known, clonable* reviewer. An
attacker can rehearse against it offline until it passes. Thirty teams reviewing their own
code have thirty different blind spots; one shared reviewer has one blind spot, in front of
every change in the company. Note that Cloudflare's 0.6% break-glass rate (1b) should be read
against this: low override usage is only reassuring if the reviewer is not the thing being
gamed.

**Caveats:** preprint, not peer-reviewed; n=33 CVEs; tests two specific commercial pipelines;
the attack assumes the adversary can submit a PR and knows which review pipeline is in use.
I read the abstract via the arXiv API, not the full paper.

### Finding a defect is not the same as fixing it

**"Toward Effective Secure Code Reviews: An Empirical Study of Security-Related Coding
Weaknesses."**

- **Type:** peer-reviewed. Published in *Empirical Software Engineering* (Springer),
  2024-06-08, DOI 10.1007/s10664-024-10496-y. Preprint at arXiv 2311.16396v2 (2023-11-28).
- **URL:** https://link.springer.com/article/10.1007/s10664-024-10496-y ;
  preprint http://arxiv.org/abs/2311.16396v2
- **Retrieved:** abstract via the arXiv API on 2026-09-20. I did not fetch the full text.

Abstract, verbatim:

> "we conducted an empirical case study in two large open-source projects, OpenSSL and PHP.
> Based on 135,560 code review comments, we found that reviewers raised security concerns in
> 35 out of 40 coding weakness categories. Surprisingly, some coding weaknesses related to
> past vulnerabilities, such as memory errors and resource management, were discussed less
> often than the vulnerabilities. Developers attempted to address raised security concerns in
> many cases (39%-41%), but a substantial portion was merely acknowledged (30%-36%), and some
> went unfixed due to disagreements about solutions (18%-20%). This highlights that coding
> weaknesses can slip through code review even when identified."

**Why this matters for "who should own the check".** The failure mode here is not detection,
it is follow-through. Roughly a third of raised security concerns were acknowledged and
dropped, and a fifth died in disagreement. A central reviewer with no authority over the fix
inherits exactly this failure mode, and at higher volume. Any claim that a shared reviewer
improves security has to show that its findings get *fixed*, not just *filed* — and none of
the first-party accounts in this file (Cloudflare, Postman) report a fix-through rate.

**Caveats:** two open-source C projects with unusual security cultures; percentages are
ranges across the two projects; open-source review dynamics differ from an employer's.

### A named position, not evidence

**"The End of Code Review: Coding Agents Supersede Human Inspection."**

- **Type:** preprint position paper, NOT peer-reviewed, NOT empirical. arXiv 2606.13175.
- **URL:** http://arxiv.org/abs/2606.13175 . Published 2026-06-11. Abstract retrieved
  2026-09-20 via the arXiv API.

Verbatim:

> "We argue that coding agents have crossed a threshold of capability at which traditional
> human code review is no longer a necessary component of a software quality pipeline. Our
> argument rests on two claims: every stated goal of code review can be served by agents at
> lower cost and higher throughput; the naive integration in which agents write code and
> humans remain the mandatory reviewers is a dead end because it neither provides meaningful
> assurance nor scales with AI-assisted throughput."

Useful only as a citable statement of the strong position the essay is arguing with. The
authors present no data. Do not use it as evidence for anything.

---

## What I could not verify

**GAP 1 is not closed.** I did not find a single published, dated, first-party account of
an organisation that built a central code review function, central AppSec review gate,
central architecture review board, or centrally mandated scanner/AI reviewer and then
**dismantled** it or **made it advisory**, with queue depth, staffing cost, or wait-time
numbers attached.

What I found instead, and why each falls short:

- **Postman (1a)** — real numbers, but a narrowing of a gate, not a reversal.
- **Architecture review boards** — a Brave search for `"architecture review board"
  disbanded OR "made advisory" bottleneck` returned ~14 results, all of which were
  consultant, vendor, or opinion content (Medium, LinkedIn Pulse, Okoone, Sogeti Labs,
  InfoWorld, LeanIX, AWS Architecture Blog, Hava, Sparx, a Substack, Reddit). Several
  assert that ARBs "can become a bottleneck", none reports a specific organisation that
  retired one, and none carries numbers. I did not fetch these individually because the
  snippets made clear they were generic advice, not case reports. **A Bing query for the
  exact phrases `"architecture review board" "we disbanded"` and `"we abolished"`
  returned zero matching documents** (Bing fell back to generic "architecture" results),
  which is weak evidence that no such account is indexed under those words.
- **Change Advisory Boards** — search returned Wikipedia, Octopus Deploy, Harness,
  TeamDynamix, monday.com and similar, all restating the *Accelerate*/DORA external-
  approval finding the team already has. No new primary case, no new numbers.
- **Named companies** — I ran out of search budget before I could try Microsoft, Amazon,
  Shopify, Spotify, Etsy, Slack, Stripe, Atlassian, Booking.com, Zalando, Monzo, Adyen or
  Klarna individually. **These are untried, not exhausted.**
- **UK GDS service assessments** (my own candidate: a central assessment panel that was
  devolved to departments) — the Brave query 429'd, and `gov.uk/service-manual/
  service-assessments` returned only a link index with no content on who runs assessments.
  **Untested lead, worth one more search.**
- **Uber's RFC process** — fetched https://blog.pragmaticengineer.com/scaling-engineering-teams-via-writing-things-down-rfcs/
  (Gergely Orosz, published 2018-10-03, updated 2022-09-21). It contains **nothing** about
  a central approval body, bottlenecks, or a move from central approval to team ownership.
  Ruled out.

**Other things I could not verify:**

- **Netflix AppSec primary sources** — 403 on every route (see 1c). The "paved road is not
  mandatory" quote is unconfirmed.
- **Any study comparing defects found by a central security function against defects found
  by the implementing team's own review, on the same changes.** I did not find one. The
  academic literature I did find (Edmundson; Thompson & Wagner; and the citation trails
  through Paul et al. ICSE 2021, Di Biase et al. SCAM 2016 on Chromium, Braz et al. 2022)
  compares reviewers to each other or measures coverage effects — none of it sets a central
  function against a team on the same diffs. **If this study exists I did not find it; if it
  does not exist, that absence is itself worth stating in the essay.**
- **Queue times and coverage percentages for central AppSec teams.** A Brave search on this
  returned 429. The one concrete queue number I have is Postman's "2 business days of
  average per-VAPT closure time" removed — which is a delta, not a queue depth.
- **ProjectDiscovery "State of AppSec 2026"** (vendor survey, blog dated 2026-01-28,
  https://projectdiscovery.io/blog/new-report-state-of-appsec-2026-security-at-engineering-speed).
  The blog contains no sample size, no ratio, no queue times — all data is gated behind a
  whitepaper download I did not retrieve. **Do not cite the blog as a source of numbers.**
- **Security champions measured effect, independent of BSIMM.** Search returned only vendor
  and consultancy content. One result (securecodinghub.com) claimed champions programmes
  "resolve vulnerabilities 40% faster and catch 3x more logic-level security bugs during
  code review compared to teams relying solely on centralized security review" — this is
  **exactly** the comparison GAP 2 asked for, but it is an uncited claim on an SEO blog. **I
  did not fetch it and I would not cite it. If you want this claim, it needs a real source
  or it needs to be dropped.**
- **BSIMM15 "4.5 per 100 developers"** — appeared in a Brave snippet attributed to Codific
  via a Google Translate URL. Not fetched, not verified. BSIMM16's own figures above
  supersede it; do not use the BSIMM15 number.
- **The `katilyst.com` BSIMM16 champions post** (Sammy Migues, a BSIMM co-author) restated
  the 2.7 / 6.8 / 12.3 / 4.6 figures and added "Out of these 111 firms, 46 had no security
  champions, while 65 had built programs totaling 6,498 champions" and champion-to-dev
  ratios of "1:6" (<650 devs) and "1:17" (650+ devs). I verified the 2.7/6.8/12.3/4.6 and
  the 46/65 split **directly against the BSIMM16 PDF**. The "1:6" and "1:17" framings and
  the "6,498" total I did **not** find in the report text and have not verified; the report
  says "approximately ... 6,500 security champions". Its publication year was not stated on
  the page.
