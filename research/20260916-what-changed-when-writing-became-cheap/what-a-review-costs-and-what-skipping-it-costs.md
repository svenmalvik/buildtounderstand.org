# What a review costs, and what skipping it costs

**Question this document answers:** How much human effort does a code review actually take, and has anyone measured what happens to code that skipped one?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 02, "The Queue Is Real" and "The Arithmetic Nobody Escapes"

**Last updated:** 2026-09-16

Scope: measurements only, with effort, elapsed time, and outcome kept strictly apart. Conflating them is the main way this subject gets misreported. Nearly every 2026 source below is an arXiv preprint with no venue acceptance shown, which is stated per item rather than assumed.

## Main findings

**Nobody has measured how many minutes a single review takes.** The only effort figures available are self-reported hours per week. The chapter's arithmetic therefore has to be built on a stated assumption, not a measured constant, and should say so.

**Someone has now measured what happens after the merge, which earlier research assumed nobody had.** A July 2026 longitudinal study of 182 repositories found that each 10 percentage-point increase in a project's no-review rate is associated with roughly a 6 per cent increase in agentic maintenance burden. That is the closest thing in the record to a measured cost of skipping the second pair of eyes.

**The outcome evidence is mixed, and the strongest counter-finding comes from Google.** Across 3.52 million changes, AI-generated code had a consistently *lower* revert rate than human-written code. Any honest account has to carry that alongside the negative findings.

## Effort: what a review costs a person

**Hours per week, self-reported.** Bosu and Carver, ESEM 2013, surveyed open-source reviewers and report an "Average number of hours per week spent in reviewing other contributors' code (Mean= 6.4 hours, σ = 7.1)". The distribution: 30 per cent under two hours, 32 per cent three to five, 26 per cent six to ten, 12 per cent over ten. Sample: 287 completed responses from 433 starts. **EFFORT.**

**A provenance trap worth recording.** Czerwonka, Greiler and Tilford, ICSE-SEIP 2015, a Microsoft experience report, states: "Developers spend on average six hours a week reviewing changes of others [6]." Reference [6] is Bosu and Carver above, the open-source survey. The sentence reads like Microsoft telemetry and is not. Do not cite it as a Microsoft measurement. The same paper cites elapsed time separately: "The median time from a review being requested to receiving all necessary sign-offs is about 24 hours, with many lasting days if not weeks", itself citing Rigby and Bird. **ELAPSED.**

**Bacchelli and Bird 2013 contains no effort figure.** Checked against the full text. Its minute figures all concern research logistics, such as interviews and observation sessions. This is worth recording because the paper is the obvious place to look and the number is not there.

**No per-review effort measurement exists.** Full-text searches for "minutes per review", "minutes per pull request", and "reviewer minutes" returned nothing relevant.

## Effort against change size

**The widely repeated figures are vendor guidance, not primary research, and their provenance does not survive checking.** They come from a SmartBear marketing page describing the company's own unpublished study: "developers should review no more than 200 to 400 lines of code (LOC) at a time"; "a review of 200-400 LOC over 60 to 90 minutes should yield 70-90% defect discovery"; "SmartBear research shows a significant drop in defect density at rates faster than 500 LOC per hour"; "performance starts dropping off after about 60 minutes". The page credits only "a SmartBear study of a Cisco Systems programming team" and gives no sample size. The figures usually quoted alongside it, 2,500 reviews and 3.2 million lines, appear only in the company's gated ebook, which could not be reached. Attribute as vendor guidance if used at all.

**One unverified peer-reviewed candidate, worth a manual download.** Kemerer and Paulk 2009, IEEE Transactions on Software Engineering, DOI 10.1109/tse.2009.27, is the strongest candidate for a research-grade figure on review rate and defect detection. The open access copy sits behind a bot challenge and could not be fetched, and Fagan 1976 failed at three mirrors during the same pass. If the chapter wants a citable rate claim rather than vendor guidance, this is the paper to retrieve by hand.

**One real measurement from Microsoft data,** in the same Czerwonka paper: "the more files there are in a single review, the lower the overall rate of useful feedback. The decrease however only starts to be noticeable for reviews with 20 or more changed files." This is a usable substitute for the vendor figures and has actual telemetry behind it.

Fagan 1976 independently capped inspection sessions at about two hours, on the grounds that detection efficiency falls away after that. See the chapter 01 research note.

## Volume, and how much of it is attributable to agents

**Meta, RADAR** (arXiv 2605.30208v2, 28 May 2026, PACMSE). First-party and specific: "significant lines of code per human-landed diff grew by 105.9% year over year and per-developer diff volume rose 51%, with agentic AI responsible for over 80% of that growth." On the queue: "the percentage of diffs reviewed within 24 hours is dropping", and "In some large groups, we observed thousands of pending diff reviews". **VOLUME and ELAPSED.**

This is better evidence for the chapter's opening than the platform-wide merged-pull-request count, because it attributes the growth to agents rather than leaving the AI share unknown.

**Author inexperience shows up as reviewer load** (arXiv 2602.23905v1, 27 Feb 2026). Across 22,953 pull requests from 1,719 authors using AI heavily, those of lower-experience authors "receive 4.52x more review comments, and have 31% lower acceptance rates, and remain open 5.16x longer". Comment count is an effort proxy, not measured effort. This is the ownership failure appearing in data rather than in anecdote.

**Automated review did not shorten the pipeline in one industrial study** (arXiv 2412.18531v2). Across 4,335 pull requests, 1,568 auto-reviewed, "average pull request closure duration increased from five hours 52 minutes to eight hours 20 minutes". **ELAPSED.** It cuts against the assumption that an automated first pass necessarily speeds things up.

**Atlassian RovoDev** (arXiv 2601.01129v2) reports "reducing the number of human-written comments by 35.6%" and "decreasing the PR cycle time by 30.8%" over a year of deployment. Comment reduction is an effort proxy; cycle time is elapsed.

**Perceived effort** (arXiv 2510.24265v2): a survey of 415 practitioners reports generation gains "offset by increased code review burden". Self-reported.

## Outcomes: what happened to code that shipped

This is the section earlier research treated as empty. It is not empty any more.

**The finding closest to this exploration's question.** Xia and Miller, "Do These Violent Delights Have Violent Ends? Measuring the Post-Merge Fate of Agentic Code", arXiv 2607.09902v1, 10 July 2026, 182 repositories, longitudinal. Verified directly against the abstract on 16 September 2026.

> "While the overall maintenance rates are similar, agentic contributions require significantly higher rates of corrective maintenance and introduce more security weaknesses and dependency vulnerabilities."

> "each 10 percentage-point increase in a project's no-review rate is associated with roughly a 6% increase in agentic maintenance burden on average."

**OUTCOME.** Caveats that must travel with it: this is an association between repository characteristics, not a causal estimate; a project that skips review may differ in many other ways; and the arXiv page shows no venue acceptance.

**The strongest counter-finding, from Google.** arXiv 2608.06640v1, 6 August 2026, 3.52 million changes over twelve months, authors affiliated with Google. Mixed results, and the favourable half is credible: build failures "remained above parity (with a median ratio of roughly 1.3x)", but "AI-generated code demonstrated a consistently lower revert rate than human-written code", median about 0.9x. **OUTCOME.** Any fair account of this subject has to include it.

**Meta RADAR outcomes, which need care.** "The revert rate for RADAR-reviewed diffs is 1/3 that of non-RADAR diffs, and the Production Incident (PI) rate is 1/50 that of non-RADAR diffs." The comparison is gated low-risk diffs selected for automation against everything else, and the authors state "this is not a causal estimate". They also name the remaining gap themselves: "Future work should study longer-term effects on review backlogs, defect escape rates".

**Shallow review and exposure duration.** "AI Code in the Wild", arXiv 2512.18567v1, 21 December 2025, covering the top 1,000 repositories plus "7,000+ recent CVE-linked code changes": "when review is shallow, AI-introduced defects persist longer, remain exposed on network-accessible surfaces, and spread to more files and repositories." Artifacts were promised but not released at the time of checking.

**A measured review-escape rate.** "Security debt of coding agents", arXiv 2607.12428v2, 14 July 2026, 16,112 file changes across 4,022 agent pull requests: "existing automated and human review processes fail to detect 81.1% of these credentials prior to integration", and "38.9% of agent-generated PRs contain at least one security smell". The same paper attributes 67.6 per cent of genuine leaked secrets to human collaborators, which should be quoted alongside so the finding is not read as an agent-only problem.

**Survey-level delivery outcomes.** The DevOps Research and Assessment program, 2024 report, nearly 3,000 respondents: a 25 per cent increase in AI adoption was associated with delivery throughput down 1.5 per cent and delivery stability down 7.2 per cent. Its 2025 report, 4,867 respondents: "AI adoption now improves software delivery throughput, a key shift from last year. However, it still increases delivery instability." Instability combines change fail rate and rework, rework being unplanned deployments caused by a production incident. Self-reported survey data, and no 2026 report was listed at the time of checking. Note the name collision: this is the DevOps program, not the EU regulation discussed in chapter 01.

## Verified platform figures, and one vendor to avoid

**GitHub's volume figure, confirmed.** "How pull request limits are cutting down the noise", GitHub Blog, 18 June 2026: "In January 2023, developers merged about 25 million pull requests a month across GitHub. Today that number tops 90 million—a roughly 3.6x increase." **VOLUME.** The metric is merged pull requests per month. GitHub does not attribute the growth to AI in that passage, and the post is about maintainer-facing rate limits.

The same post makes an effort claim with no measurement behind it: "Reviewing one still takes a human about as long as it ever did." **EFFORT, unmeasured.** Usable in the prose precisely because it is an assertion rather than a finding, and it can be quoted alongside the observation that nobody has counted.

Related, from "Agent pull requests are everywhere. Here's how to review them", 7 May 2026: "GitHub Copilot code review has processed over 60 million reviews, growing 10x in less than a year" and "More than one in five code reviews on GitHub now involve an agent." Both **VOLUME.**

**The strain sits in pickup, not in reviewing.** LinearB data shows that once review begins, AI-assisted pull requests are reviewed faster than unassisted ones, about 194 minutes against 252 at the median. **ELAPSED TIME.** This refines the capacity argument: the scarce resource is reviewer attention and scheduling, not reading speed. Sample size and article date still to be confirmed.

**Faros AI: verified, corrected, and best left out.** Its figures are real and the report exists, "The AI Engineering Report 2026: The Acceleration Whiplash", covering "two years of telemetry data from 22,000 developers and more than 4,000 teams", comparing each organisation's lowest and highest AI-adoption periods. Quotes: "Median time to first PR review is up 156.6%", "Median time in review is up 441.5%", "Pull requests merged without any review, human or agentic, are up 31.3%".

Three problems:

1. **The 31.3% is a relative increase, not a share.** It does not mean 31.3 per cent of pull requests merge unreviewed. The baseline rate is unpublished, so it cannot be converted into a share. Writing "31% of pull requests merge without review" would be simply wrong.
2. **Three different review-time figures circulate from one dataset.** A November 2025 post gives a 91 per cent increase in review time, a May 2026 post gives 199.6 per cent for the average, and the report gives 441.5 per cent for the median. Any use has to name which cut it is.
3. **The design confounds adoption with calendar time,** because a given organisation's high-adoption periods are also its later periods. Faros claims statistical association, not causation.

Decision recorded: do not cite this vendor in the prose. The numbers are attackable on provenance even where they are accurate, and better-sourced figures exist for every point they support.

## The strongest case that the queue is not real

Stated fairly, because the section has to answer it rather than ignore it.

**Merging is the end of a review, not a backlog.** Merged pull request volume rose about 3.6 times, but a merge is what happens when review completes. A number that grows while still clearing describes throughput, not blockage. If review were truly binding, those changes would not be merging.

**The growth is concentrated, not general.** The doubling belongs to the heaviest users of these tools, while non-users are flat. So the aggregate is not a description of everyone's condition.

**Reviewing itself did not get slower.** Once a reviewer starts, AI-assisted changes clear faster than unassisted ones.

**Where teams actually hold work may be downstream.** Steve Fenton argued in The New Stack on 16 July 2026 that if review were the binding constraint, deployment batches would not be where most teams accumulate work.

**What survives the objection.** Two things. Pickup delay, and the rise in merges with no review at all. Both support the narrower claim: the queue is real for the people standing in it, even where the totals clear. That formulation is the honest version and is what the prose now says.

## Pickup versus reviewing

LinearB, 4 May 2026, 8.1 million pull requests across 4,800 teams in 42 countries. Both **ELAPSED TIME**.

| Stage | AI-assisted | Unassisted |
| --- | --- | --- |
| Wait before pickup | about 16 hours | about 200 minutes |
| Review once started | about 194 minutes | about 252 minutes |

The contrast is the useful part. The wait before anyone starts is roughly five times longer for AI-assisted changes, while the reviewing itself is faster. This is the clearest available evidence that the scarce resource is reviewer attention rather than reading speed.

## Was the volume rise an artifact of splitting work?

No, and this closes an obvious objection. At the 75th percentile, "AI-assisted pull requests contain over 400 lines of code compared to 157 lines for unassisted work", with agentic pull requests near 290 lines. **VOLUME.** Changes got bigger, so the rise in count is not an accounting effect of dividing the same work into smaller pieces.

Caveat: this is vendor data, and its corroborating source was dropped for the provenance problems recorded above, so it now stands alone. No source measures what share of the rise is genuinely new work.

## Reviewer concentration: a metric, not a measurement

LinearB, 9 September 2026, over 8.1 million pull requests, defines the idea but never publishes a value: "An average review count across your organization can look healthy while most of the reviewing sits with a handful of people." Its reviewer-imbalance metric "reports how many more reviews your top 20% of reviewers complete than everyone else".

This supports a claim about missing measurement, not a claim that concentration worsened. Do not write that reviewing became more concentrated. Nobody published the number.

## What nobody appears to have measured

**Human attention per review, in minutes, at any company, in any decade.** The entire effort literature reduces to two self-reported weekly averages: 6.4 hours in open source and 3.2 hours at Google. Neither divides by the number of reviews.

**Effort per review under AI.** Meta shows supply roughly doubling and timely review falling, but publishes no denominator in reviewer time. Every 2026 figure available is volume, latency, comment count, or perception.

**A skipped review causally linked to a production incident.** The post-merge study comes closest, and only as a correlation, in open-source repositories.

**One organisation answering both halves of the question.** This is the sharpest way to state the gap. Google measured reverts segmented by AI authorship but not incidents. Meta measured incidents but only for the gated low-risk diffs it had chosen to automate. The two companies with the telemetry to settle this each answered half, and neither segmented outcomes by how much review a change actually received.

**Whether an automated approval that satisfies a merge rule produces different outcomes than a human one.** This became a configuration option on 1 September 2026 and has no evidence either way.

## Confidence and gaps

| Claim | Assessment |
| --- | --- |
| Reviewers spend roughly six hours a week reviewing | Medium. One 2013 open-source survey, 287 responses, self-reported, high variance. |
| That six-hour figure is Microsoft telemetry | False. The Microsoft paper is citing the open-source survey. |
| Bacchelli & Bird contains a per-review time figure | False. Checked against full text. |
| The 200-400 line and 60-90 minute limits are research findings | No. Vendor material. Attribute as vendor guidance. |
| Useful feedback declines with more files, noticeably past 20 | Medium-high. Microsoft data in a peer-reviewed venue. |
| Agentic AI drove most of Meta's diff-volume growth | Medium-high. First-party, specific, preprint. |
| Higher no-review rate is associated with more agentic maintenance burden | Medium. Verified quote, 182 repositories, association not causation, no venue shown. |
| AI-generated code is reverted more often | Contradicted at Google scale, where revert rate was lower at about 0.9x. |
| Review escapes are measurable and large for secrets | Medium. 81.1 per cent undetected pre-integration, single preprint, and most genuine leaks were attributed to humans. |
| AI adoption harms delivery stability | Medium. Two survey waves agree on instability while reversing on throughput. Self-reported. |
| The 2,500 reviews and 3.2 million lines behind the vendor figures | Unverifiable. Gated ebook, not reachable. |
| Kemerer & Paulk 2009 supports a review-rate claim | Unknown. Not retrieved; behind a bot challenge. Worth one manual download. |
| The queue is a general condition across the industry | No. The growth is concentrated among the heaviest tool users; non-users are flat. |
| Reviewing got slower | No. Once started, AI-assisted changes clear faster, about 194 against 252 minutes. |
| The volume rise is an artifact of splitting work smaller | No. Changes got bigger, over 400 lines against 157 at the 75th percentile. Vendor data, now uncorroborated. |
| Reviewing became more concentrated among fewer people | Not established. The metric is defined but no value was published. |
| METR revised its productivity findings in 2026 | Not found. Eight 2026 posts, none on that trial. |
| Cursor's 39 per cent merged-pull-request figure | Unusable. Cited secondhand; the primary URL returns 404. |
| GitHub's 90 million excludes bot pull requests | Unknown. Not stated in the source. |

## Related documents

- [`machine-approval-and-two-responses.md`](./machine-approval-and-two-responses.md), on the 1 September 2026 approval setting and who kept the human approver.
- `ai-pull-request-growth-and-review-capacity-2026.md` in the `vce-context` worktree, for the three failure modes and the automated-review evidence.
