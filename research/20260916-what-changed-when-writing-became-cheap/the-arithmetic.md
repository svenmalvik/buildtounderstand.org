# The arithmetic: arrivals, effort, and capacity

**Question this document answers:** Can anyone actually do the capacity calculation for code review, and what do the three terms in it look like?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 02, "The Arithmetic Nobody Escapes"

**Last updated:** 2026-09-19

Scope: the capacity relation is changes arriving, times the human effort each needs, against the qualified reviewer time available. This note takes each term separately and asks what is measured.

## Main findings

**Nobody has done this arithmetic in public for code review.** The three terms exist separately in the literature and have never been multiplied together. No organisation has published a calculation of the form "we have this many engineers, this many changes arrive, each takes this long, therefore".

**One term has never been measured at all.** There is no published figure for minutes of human attention per review. See the companion note on what a review costs.

**A second term is routinely overstated.** Reviewer capacity is not headcount. Across five large projects, 20 per cent of developers perform about 80 per cent of the reviews.

**No one has shown the queueing nonlinearity for code review.** Nothing models a review queue with utilisation, so the essay must not claim that waiting time rises steeply as capacity is approached. That claim is unsupported.

## Term 1: arrivals, the only term measured well

Meta, arXiv 2605.30208v2, is the clearest first-party statement that arrivals outran capacity:

> "Historically, at Meta, reviewer capacity and tooling improvements have been sufficient to keep review latency within acceptable bounds."

> "Together, these trends suggest that the rate of code creation is rising faster than human review capacity."

> "In some large groups, we observed thousands of pending diff reviews, illustrating the problem of review backlogs."

The first sentence is the useful one for the essay: it says the arithmetic used to work, and then stopped working. RADAR gives the direction of the share of diffs reviewed within 24 hours, never its value.

A similar account without numbers, and **not to be used until verified**: a Linux kernel mailing list message attributed to Linus Torvalds, 17 May 2026, saying "the continued flood of AI reports has basically made the security list almost entirely unmanageable, with enormous duplication". This reached the research secondhand through arXiv 2604.16754v2. Verify against the primary posting before quoting.

## The rate that preserves detection, now sourced

This closes the gap that previously forced the section to cite vendor marketing.

**Kemerer and Paulk**, IEEE Transactions on Software Engineering 35(4), July/August 2009, pp. 534-550, DOI 10.1109/TSE.2009.27. **PEER REVIEWED.** Sample, p. 538: "the resulting C data set has 371 observations for 153 developers and the C++ data set has 246 observations for 90 developers." Developers had up to 34 years of experience, median seven.

The threshold, section 4.5, p. 546:

> "The recommended preparation rate is less than or equal to 200 LOC/hour [27], [47]. A faster rate is considered ineffective and a reinspection is recommended."

The result, pp. 546-547:

> "In all four cases, reviewers who adhere to the recommended review rate find more defects than those who do not. For design defects, they find 66 and 57 percent, respectively, and 56 and 57 percent for code defects. Reviewers using a faster-than-recommended review rate find only 49 and 51 percent of design defects and 47 and 45 percent of code defects."

Abstract, p. 534: "The recommended review rate of 200 LOC/hour or less was found to be an effective rate for individual reviews, identifying nearly two-thirds of the defects in design reviews and more than half of the defects in code reviews."

**Three caveats that must travel with it.** The authors note the absolute effect "may be as few as one or two defects since the absolute numbers are not large". Slowing below 200 did not help measurably, with no significant difference between 0-100 and 100-200 lines an hour, so 200 is a ceiling rather than a target. But "defect removal effectiveness continues to decline as the review rate becomes faster."

**The strongest objection, and the limit to state openly.** In the Personal Software Process the reviewer wrote the code. These were course assignments with a median size around 120 lines, in C and C++, reviewed by their own author. A pull request is someone else's unfamiliar code. The paper anticipates the size objection in section 4.6 and argues the task sizes are comparable, and notes the developers had a median of seven years of experience. It cannot answer the familiarity objection.

Used carefully, this strengthens rather than weakens the essay's calculation: if 200 lines an hour is the ceiling for reviewing code you wrote yourself, reviewing a stranger's code is not faster. Treat it as an upper bound and say why.

**Where 200 comes from**, p. 547: "the recommended rate is about 100 LOC/hour (maximum of 200 LOC/hour), and the recommended length of an inspection meeting that the developer would prepare for is 2 hours, the typical size of work product we might expect to see in an industry inspection would be about 200 LOC." So the recommended rate is nearer 100, with 200 as the maximum, and 200 lines is roughly what fits a two-hour session.

**Two independent sources cap the session rather than the rate.** Fagan limits inspection sessions to two hours because detection efficiency dwindles after that. NASA-GB-A302, the Software Formal Inspections Guidebook of August 1993, specifies no rate at all but states that "Inspection meetings are limited to two hours" and that the product "should be of an appropriate size that it can be inspected during a two hour meeting."

**The 400-line figure has no research behind it.** 200 does. Do not treat the vendor's 200 to 400 range as equivalent evidence.

**Gilb could not be retrieved as a primary source**, and the widely repeated claim that each defect found saves nine hours remains unverified. If a Gilb rate is needed, cite the peer-reviewed secondary, Kemerer and Paulk p. 536: "Gilb and Graham, for example, suggest a preparation rate of 0.5 to 1.5 pages per hour; they also suggest that rates as slow as 0.1 page per hour may be profitable for critical documents."

**No modern replication exists.** No post-2015 study tests rate in lines per hour against detection. Of 99 papers citing Kemerer and Paulk since 2015, none does. That rests on citation-graph traversal rather than a full search.

**Fagan 1976 states rates too**, IBM Systems Journal 15(3), Table 3, original p. 190. For systems programming: design preparation 100 and inspection 130 lines an hour; code preparation 125 and inspection 150. The table footnote says these "apply to systems programming and are conservative. Comparable rates for applications programming are much higher", and Table 2 gives far faster applications rates from the Aetna COBOL project, preparation 898 and 709 lines an hour.

So the defensible statement is a range, not a constant: somewhere between about 130 and 200 lines an hour for careful review of systems-style code, with applications code potentially faster.

## Term 2: effort per review, never measured

Covered in [`what-a-review-costs-and-what-skipping-it-costs.md`](./what-a-review-costs-and-what-skipping-it-costs.md). In short: no study anywhere reports minutes of human attention per review. The only effort figures are self-reported weekly averages, about 6.4 hours in open source and about 3.2 hours at Google, and neither divides by the number of reviews.

The nearest thing to a service time is a vendor model rather than a measurement. LinearB's gitStream, 18 November 2022, predicts review time from change size, file types and repository familiarity and buckets it into "a useful time range (e.g. 15-30 minutes)". **SERVICE TIME, modelled, not measured.** No distribution is published.

Google sets a service level without any arithmetic behind it: "One business day is the maximum time it should take to respond to a code review request." That is a target, not a capacity calculation.

## Term 3: capacity, much smaller than headcount

This is the finding that does the most work in the section.

Rigby et al., "Factoring Expertise, Workload, and Turnover into Code Review Recommendation", arXiv 2312.17236v1, 28 December 2023. Five projects: CoreFX, CoreCLR, Roslyn, Rust and Kubernetes.

> "We see that review effort is highly concentrated with 20% of the developers performing around 80% of the reviews."

> "On the Rust project, 20% of the developers do 84% of the reviews."

Method: a Gini coefficient over an inverted Lorenz curve of review workload.

| Project | Reviewed PRs | Years | Developers |
| --- | --- | --- | --- |
| Rust | 17,499 | 9 | 2,720 |
| Kubernetes | 32,400 | 5 | 2,617 |
| CoreFX | 13,499 | 5 | 985 |
| CoreCLR | 10,250 | 4 | 698 |
| Roslyn | 8,646 | 5 | 469 |

**Two things make this valuable.** It predates the AI period, so it is a baseline rather than a symptom of the current volume. And the concentration is movable: a workload-aware recommender brought it to "20% of the developers doing 59% of the reviews". So capacity is partly a routing problem, not only a headcount problem.

**Reviewer-to-author ratio: not found.** No source publishes qualified reviewers against submitting authors. The developer counts above are not reviewer-eligibility counts.

This is also the measured value that the LinearB reviewer-imbalance metric defines but never publishes.

## Queueing: what exists and what does not

**Applied to code review, once, and not for utilisation.** Fatima Ali et al., "Group versus Individual Review Requests: Tradeoffs in Speed and Quality at Mozilla Firefox", arXiv 2601.01514v1, 4 January 2026, ICSE-SEIP 2026, 66,318 Firefox revisions:

> "In the context of code review, a group review request is equivalent to a shared queue and individual requests to individual queues."

Its finding is that group requests associate with fewer regressions and have "negligible association with review velocity". It models pooled against dedicated servers, citing management science rather than Little's Law.

**The nonlinearity is not found for code review.** No paper, preprint or engineering post in the searched sources models a review queue as M/M/1, computes utilisation, or shows waiting time rising steeply as utilisation approaches one. **The essay must not claim it.**

**The closest formal model is in another domain, and it does not support the claim either.** Kwon et al., "Publish and Perish", arXiv 2604.05714v1, 7 April 2026, models scientific peer review as a queue under the theory of constraints. Its critical condition compares arrival rate against service capacity in the form the essay needs. But it produces unbounded divergence once arrivals exceed capacity, which is linear overload, not a steep rise below capacity. Do not cite it as evidence for the nonlinearity.

Its statement of the constraint is the plainest found anywhere, and it is the authors' own wording, appearing twice in their model exposition without a citation marker:

> "reviewer capacity is fixed, which is physically correct for peer review (unlike enzyme kinetics, more substrate does not produce faster processing)"

If used, attribute it to scientific peer review rather than code review.

## Work-in-progress limits

One shipped mechanism, no published effect. GitHub, 18 June 2026: "A pull request limit sets the maximum number of pull requests a user without write access can have open at once in your repository." Drafts are excluded, a bypass list exists, no default value is stated, and no before-and-after measurement is published.

Note what it does: it caps **arrival**, not work in progress inside review. No Kanban-style limit on changes under review appears anywhere in the searched sources. Zalando's size cap is socially agreed rather than enforced, since "Hard enforcement through pre-commit hooks is less popular."

## The strongest claim that the arithmetic does not bind

Meta's, and its authors hedge it themselves:

> "An important implication is that automation can absorb a portion of routine diff volume without requiring a proportional increase in human reviewer capacity."

Stated fairly: if a definable share of arrivals can be served by machine at near-zero marginal cost, the constraint moves from total volume to the residual that cannot be stratified. Note the wording concedes the limit. It says "a portion", not any arrival rate. The same paper calls its outcome comparison non-causal and names review backlogs as future work.

## Confidence and gaps

| Claim | Assessment |
| --- | --- |
| Arrivals are rising faster than review capacity | High as a first-party statement from Meta; not a general measurement. |
| Effort per review has never been measured | High. Confirmed across two research passes. |
| 20 per cent of developers do about 80 per cent of reviews | High. Five projects, stated method, pre-AI baseline. |
| Concentration is movable by routing | Medium-high. Same paper, reporting its own recommender's effect. |
| Waiting time rises steeply as capacity is approached | Not established for code review. Do not claim it. |
| Anyone has published a capacity calculation | Not found. |
| A work-in-progress limit on review has been tried and measured | Not found. The GitHub limit caps arrivals and publishes no effect. |
| Automation removes the constraint | No. The strongest claim concedes it absorbs a portion. |
| The Torvalds quote on the security list | Unverified, secondhand. Check the primary posting first. |

## Method limit

The pass ran without web search, using the arXiv, Crossref, OpenAlex and Semantic Scholar interfaces plus direct fetches. The honest claim is that these sources contain no such arithmetic, not that none exists anywhere.
