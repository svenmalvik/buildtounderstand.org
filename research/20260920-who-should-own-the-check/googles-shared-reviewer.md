# Google's shared reviewer: readability and Tricorder

**Question this document answers:** Google runs the two longest-running examples of a *shared* reviewer — readability (a central pool of certified humans who must approve every change in their language) and Tricorder (a central static analysis platform whose findings appear in every code review). What does each one protect, and what does each one cost?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 03

**Last updated:** 2026-09-20

---

## Main findings

- **Google separates the check from the checker by splitting approval into three independent bits** — correctness (LGTM), ownership, and readability — and then notes that most reviews collapse all three into one person. The machinery is central; the decision usually stays local.
- **Readability is the human shared reviewer, and Google publishes its costs in its own words.** Around 1–2% of engineers are readability reviewers; around 20% of engineers are in the process at any time. Google calls it "a heavyweight process," names three concrete costs, and records the internal criticism: "an unnecessary bureaucratic hurdle and a poor use of engineer time," and, in a second chapter, "an archaic hazing process."
- **Google's own study of readability reports direction but publishes no magnitude.** "CLs by authors with readability take statistically significantly less time to review and submit." No effect size, no sample size, no added-latency figure for a change that needs an outside readability reviewer has been published. This is the single biggest gap in the record.
- **Readability's central trade-off is stated explicitly and is about scaling, not quality:** centralizing "is limited to scaling linearly rather than sublinearly with organization growth, but it makes it easier to enforce consistency, avoid islands, and avoid ... drifting from established norms."
- **Tricorder is the strongest published case for centralizing machinery, and it is a case built on three failures.** Google tried a bug dashboard (ignored), manual bug filing (a company-wide Fixit reviewed 3,954 warnings and fixed only 640), and only succeeded once findings appeared inside the review. The governing rule is a hard 10% effective-false-positive ceiling enforced by click data.
- **Counter-evidence is strong and specific:** at Microsoft, 91% of 873 developers said unfamiliar files take longer to review, and 82% said familiar reviewers give *different* — deeper, more conceptual — feedback. A reviewer pulled from a central pool is by construction the unfamiliar case.

---

## 1. Google's readability process

### What it certifies and who grants it

> "Google defines a concept called *readability*, which was introduced very early on to ensure consistent code style and norms within the codebase. Developers can gain readability certification in a particular language. To apply for readability, a developer sends changes to a set of readability reviewers; once those reviewers are confident the developer understands the code style and best practices for a language, the developer is granted readability for that language. **Every change must be either authored or reviewed by someone with a readability certification for the language(s) used.**"
>
> — Sadowski, Söderberg, Church, Sipko, Bacchelli, "Modern Code Review: A Case Study at Google," ICSE-SEIP '18, Gothenburg, 27 May–3 June 2018, §5.1 "Describing The Review Process." Peer-reviewed conference paper (industry track). https://storage.googleapis.com/gweb-research2023-media/pubtools/4476.pdf
>
> *(Note on sourcing: page 5 of that PDF does not extract as text. This passage was read from a 150 dpi render of page 5.)*

The same section defines the other half of the pair:

> "**Ownership.** The Google codebase is arranged in a tree structure, where each directory is explicitly *owned* by a set of people. Although any developer can propose a change to any part of the codebase, an owner of the directory in question (or a parent directory) must review and approve the change before it is committed; even directory owners are expected to have their code reviewed before committing."
>
> — same paper, §5.1

### The three approval bits

> "There are three aspects of review that require 'approval' for any given change at Google:
>
> - A correctness and comprehension check from another engineer that the code is appropriate and does what the author claims it does. This is often a team member, though it does not need to be. This is reflected in the LGTM permissions 'bit' ...
> - Approval from one of the code owners that the code is appropriate for this particular part of the codebase ... Owners act as gatekeepers for their particular directories.
> - Approval from someone with language 'readability' that the code conforms to the language's style and best practices, checking whether the code is written in the manner we expect. This approval, again, might be implicit if the author has such readability. **These engineers are pulled from a company-wide pool of engineers who have been granted readability in that programming language.**"
>
> — Winters, Manshreck, Wright (eds.), *Software Engineering at Google*, O'Reilly, 2020, Ch. 9 "Code Review," §"Code Review at Google." Book, published by Google engineers, free online. https://abseil.io/resources/swe-book/html/ch09.html

Why the split exists — this is the chapter's own answer, and it is the "centralize the machinery, not the decision" argument stated from the inside:

> "Although this level of control sounds onerous—and, admittedly, it sometimes is—most reviews have one person assuming all three roles, which speeds up the process quite a bit."

> "If all three of these types of reviews can be handled by one reviewer, why not just have those types of reviewers handle all code reviews? **The short answer is scale.** Separating the three roles adds flexibility to the code review process."

> "Most code reviews at Google are reviewed by precisely one reviewer. Because the code review process allows the bits on code correctness, owner acceptance, and language readability to be handled by one individual, the code review process scales quite well across an organization the size of Google."
>
> — all three from *SWE at Google*, Ch. 9

### Who grants it, and how many people are involved

> "Around 1 to 2% of Google engineers are readability reviewers. All reviewers are volunteers, and anyone with readability is welcome to self-nominate to become a readability reviewer. Readability reviewers are held to the highest standards because they are expected not just to have deep language expertise, but also an aptitude for teaching through code review. **They are expected to treat readability as first and foremost a mentoring and cooperative process, not a gatekeeping or adversarial one.**"

> "Today, around 20% of Google engineers are participating in the readability process at any given time, as either reviewers or code authors."

> "Engineers with readability have demonstrated that they consistently write clear, idiomatic, and maintainable code ... They do this by submitting CLs through the readability process, during which **a centralized group of readability reviewers** review the CLs and give feedback on how much it demonstrates the various areas of mastery. **As authors internalize the readability guidelines, they receive fewer and fewer comments on their CLs until they eventually graduate from the process and formally receive readability.**"
>
> — *Software Engineering at Google*, Ch. 3 "Knowledge Sharing," case study "Readability: Standardized Mentorship Through Code Review." https://abseil.io/resources/swe-book/html/ch03.html

Note what "how long it takes to obtain" means here: the process has **no fixed duration**. Graduation is a judgement by reviewers that comment volume has fallen far enough. No published figure gives a median time-to-readability. See "What I could not verify."

### The centralization trade-off, stated explicitly

> "One of the primary advantages of the readability program is that it exposes engineers to more than just their own team's tribal knowledge. To earn readability in a given language, engineers must send CLs through a centralized set of readability reviewers who review code across the entire company. **Centralizing the process makes a significant trade-off: the program is limited to scaling linearly rather than sublinearly with organization growth, but it makes it easier to enforce consistency, avoid islands, and avoid (often unintentional) drifting from established norms.**"
>
> — *SWE at Google*, Ch. 3

### The costs, in Google's own list

> "These benefits come with some costs: **readability is a heavyweight process** compared to other mediums like documentation and classes because it is mandatory and enforced by Google tooling ... These costs are nontrivial and include the following:
>
> - Increased friction for teams that do not have any team members with readability, because they need to find reviewers from outside their team to give readability approval on CLs.
> - Potential for additional rounds of code review for authors who need readability review.
> - Scaling disadvantages of being a human-driven process. Limited to scaling linearly to organization growth because it depends on human reviewers doing specialized code reviews."

> "The program makes a deliberate trade-off of **increased short-term code-review latency and upfront costs** for the long-term payoffs of higher-quality code, repository-wide code consistency, and increased engineer expertise. The longer timescale of the benefits comes with the expectation that code is written with a potential lifetime of years, if not decades."
>
> — *SWE at Google*, Ch. 3

The first bullet is the one that matters for the chapter: the cost lands unevenly. A team with no certified member pays a tax that a team with one does not.

### Published criticism

Two Google-authored passages record the internal complaint:

> "But aspirations aren't enough. **Readability is a controversial program: some engineers complain that it's an unnecessary bureaucratic hurdle and a poor use of engineer time.** Are readability's trade-offs worthwhile? For the answer, we turned to our trusty Engineering Productivity Research (EPR) team."
>
> — *SWE at Google*, Ch. 3

> "The readability process was put in place in the early days of Google, before automatic formatters ... and linters that block submission were commonplace. **The process itself is expensive to run because it requires hundreds of engineers performing readability reviews for other engineers in order to grant readability to them. Some engineers viewed it as an archaic hazing process that no longer held utility, and it was a favorite topic to argue about around the lunch table.** The concrete question from the language teams was this: is the time spent on the readability process worthwhile?"

> "People were certain the costs had been worth the benefits at one point in time, but **with the advent of autoformatters and static analysis tools, no one was entirely certain. There was a growing belief that the process now served as a hazing ritual.**"

> "It committed that, **if our analysis showed that the costs either outweighed the benefit or the benefits were negligible, the team would kill the process.** As different programming languages have different levels of maturity in formatters and static analyses, this evaluation would happen on a per-language basis."
>
> — *SWE at Google*, Ch. 7 "Measuring Engineering Productivity," §"Triage: Is It Even Worth Measuring?" https://abseil.io/resources/swe-book/html/ch07.html

This is the sharpest framing available for the chapter: **Google itself argued that once the machinery got good enough, the human shared reviewer might no longer be needed** — and set up a study designed to be able to kill the program.

### How Google justifies the cost

> "The EPR team performed in-depth studies of readability, including but not limited to whether people were hindered by the process, learned anything, or changed their behavior after graduating. These studies showed that readability has a net positive impact on engineering velocity. **CLs by authors with readability take statistically significantly less time to review and submit than CLs by authors who do not have readability.** Self-reported engineer satisfaction with their code quality—lacking more objective measures for code quality—is higher among engineers who have readability versus those who do not. A significant majority of engineers who complete the program report satisfaction with the process and find it worthwhile."
>
> Footnote 22: "This includes controlling for a variety of factors, including tenure at Google and the fact that CLs for authors who do not have readability typically need additional rounds of review compared to authors who already have readability."
>
> — *SWE at Google*, Ch. 3

> "For readability, our study showed that it was overall worthwhile: engineers who had achieved readability were satisfied with the process and felt they learned from it. **Our logs showed that they also had their code reviewed faster and submitted it faster, even accounting for no longer needing as many reviewers.** Our study also showed places for improvement with the process: engineers identified pain points that would have made the process faster or more pleasant."
>
> — *SWE at Google*, Ch. 7, §"Taking Action and Tracking Results"

**Caveat worth carrying into the chapter:** the measured benefit is a comparison between *people who have graduated* and *people who have not*. It is not a measurement of the program's cost — it is a measurement of the state after paying it. The obvious confound (engineers who have readability are, on average, more experienced) is partly controlled via tenure per footnote 22, but the published account gives no effect size and no sample size.

Google also names the direction of travel — machinery replacing the human check:

> "Some of the costs can be mitigated with tooling. **A number of readability comments address issues that could be detected statically and commented on automatically by static analysis tooling.** As we continue to invest in static analysis, readability reviewers can increasingly focus on higher-order areas, like whether a particular block of code is understandable by outside readers who are not intimately familiar with the codebase instead of automatable detections like whether a line has trailing whitespace."
>
> — *SWE at Google*, Ch. 3

And an exemption that is itself an argument about when a shared reviewer is worth it:

> Footnote 21: "For this reason, code that is known to have a short time span is exempt from readability requirements. Examples include the experimental/ directory ... and the Area 120 program."
>
> — *SWE at Google*, Ch. 3

---

## 2. The 2018 paper's numbers

All from Sadowski, Söderberg, Church, Sipko, Bacchelli, "Modern Code Review: A Case Study at Google," ICSE-SEIP '18. Peer-reviewed conference paper. https://storage.googleapis.com/gweb-research2023-media/pubtools/4476.pdf

### Stated purpose of code review at Google

> "E explained that **the main impetus behind the introduction of code review was to force developers to write code that other developers could understand**; this was deemed important since code must act as a teacher for future developers. E stated that the introduction of code review at Google signaled the transition from a research codebase, which is optimized towards quick prototyping, to a production codebase, where it is critical to think about future engineers reading source code. Code review was also perceived as capable of ensuring that more than one person would be familiar with each piece of code, thus increasing the chances of knowledge staying within the company."

> "E reiterated on the concept that, **although it is great if reviewers find bugs, the foremost reason for introducing code review at Google was to improve code understandability and maintainability.**"
>
> — §4.1 "How it All Started." "E" is one of Google's first employees, interviewed by the first author. n = 1 for this claim; it is oral history, not measurement.

### The four properties

Careful here — the paper has **two** different lists of four/five, and they are easy to conflate.

**(a) The four *expectations* Google developers have of review** (this is the paper's own finding, from coding 12 interviews, validated on 44 survey responses):

> "By coding our interview data, we identified **four key themes for what Google developers expect from code reviews: education, maintaining norms, gatekeeping, and accident prevention.** Education regards either teaching or learning from a code review and is in line with the initial reasons for introducing code review; norms refer to an organization preference for a discretionary choice (e.g., formatting or API usage patterns); gatekeeping concerns the establishment and maintenance of boundaries around source code, design choices or another artifact; and accidents refer to the introduction of bugs, defects or other quality related issues."
>
> — §4.2 "Current expectations." A fifth, retrospective use is added: "code review is also used *retrospectively* for **tracking history**."

> "**Finding 1.** Expectations for code review at Google do not center around problem solving. Reviewing was introduced at Google to ensure code readability and maintainability. Today's developers also perceive this educational aspect, in addition to maintaining norms, tracking history, gatekeeping, and accident prevention. Defect finding is welcomed but not the only focus."

> "**Finding 2.** Expectations about a specific code review at Google depend on the work relationship between the author and reviewers."

**(b) The five *convergent practices* (CP1–CP5)** — these are Rigby & Bird's, which the Google paper is testing against, not Google's own:

> | id | Convergent Practice |
> |---|---|
> | CP1 | Contemporary peer review follows a lightweight, flexible process |
> | CP2 | Reviews happen early (before a change is committed), quickly, and frequently |
> | CP3 | Change sizes are small |
> | CP4 | Two reviewers find an optimal number of defects |
> | CP5 | Review has changed from a defect finding activity to a group problem solving activity |
>
> — §2.2, Table 1. Source: Rigby & Bird, "Convergent contemporary software peer review practices," ESEC/FSE 2013.

Google matches CP1–CP3, diverges on CP4 (one reviewer, not two) and CP5 (education, not group problem solving).

### Sample size

> "Our final dataset includes the **approximately 9 million changes created by more than 25,000 authors and reviewers from January 2014 until July 2016** that meet these criteria, and about 13 million comments collected from all changes between September 2014 and July 2016."

> "On an average workday at Google, about 20,000 changes are committed that meet the filter criteria described above."

Filters applied: no changes without reviewers, robot-authored changes filtered by name heuristic (kept only if they had a human reviewer), main codebase only, uncommitted changes excluded, zero-source-line diffs excluded. Qualitative side: **12 interviews** and **44 valid survey responses out of 98 sent (45% response rate)**.

### Reviewers per change

> "At Google, by contrast, **fewer than 25% of changes have more than one reviewer, and over 99% have at most five reviewers with a median reviewer count of 1.** Larger changes tend to have more reviewers on average. However, even very large changes on average require fewer than two reviewers."
>
> Footnote 1: "30% of changes have comments by more than one commenter, meaning that about 5% of changes have additional comments from someone that did not act as an approver for the change."

> "**Usually, only one reviewer is required to satisfy the aforementioned requirements of ownership and readability.**"

> "**Finding 4.** Code review at Google has converged to a process with markedly quicker reviews and smaller changes, compared to the other projects previously investigated. Moreover, one reviewer is often deemed as sufficient, compared to two in the other projects."

### Latency

> "In terms of speed, we find that **developers have to wait for initial feedback on their change a median time of under an hour for small changes and about 5 hours for very large changes. The overall (all code sizes) median latency for the entire review process is under 4 hours.** This is significantly lower than the median time to approval reported by Rigby and Bird, which is 17.5 hours for AMD, 15.7 hours for Chrome OS and 14.7, 19.8, and 18.9 hours for the three Microsoft projects. Another study found the median time to approval at Microsoft to be 24 hours."

> "During the week, **70% of changes are committed less than 24 hours after they are mailed out for an initial review.**"
>
> — §8 Conclusion

### Other numbers worth having

- Frequency: "the median developer authors about 3 changes a week, and 80 percent of authors make fewer than 7 changes a week ... the median for changes reviewed by developers per week is 4, and 80 percent of reviewers review fewer than 10 changes a week."
- Size: "about 90% modify fewer than 10 files. Over 10% of changes modify only a single line of code, and **the median number of lines modified is 24.**"
- Iterations: "**over 80% of all changes involve at most one iteration of resolving comments.**"
- Reviewer time: "developers spend an average of 3.2 (median 2.6 hours a week) reviewing changes. This is low compared to the 6.4 hours/week of self-reported time for OSS projects." (measured over five weeks starting October 2016, from interaction logs)
- Satisfaction: "all respondents agreed with the statement that code review is valuable" (n=44); "97% of developers are satisfied with it" (internal Critique survey, sample size not given).
- **Only 2 of 44 survey respondents said the comments had found a bug**; "8 respondents described the comments as not being helpful."

### Reviewer selection — the machinery around the human

> "To identify the best person to review a change, Critique relies on a tool that analyzes the change and suggests possible reviewers. **This tool identifies the smallest set of reviewers needed to fulfill the review requirements for all files in a change.** Note that often only one reviewer is required since changes are often authored by someone with ownership and/or readability for the files in question. This tool prioritizes reviewers that have recently edited and/or reviewed the included files. **New team members are explicitly added as reviewers since they have not yet built up reviewing/editing history.** ... **Tool support for finding reviewers is typically only necessary for changes to files beyond those for a particular team. Within a team, developers know who to send changes to.**"
>
> — §5.1

That last sentence is the chapter's point in one line: the shared reviewer is a *fallback for crossing a boundary*, not the default path.

### Knowledge spreading — the measured educational effect

> "As developers build experience working at Google, the average number of comments on their changes decreases (Figure 2). **Developers at Google who have started within the past year typically have more than twice as many comments per change.** ... Also, we can see that the number of distinct files edited and reviewed by engineers at Google, and the union of those two sets, increase with seniority (Figure 3) and **the total number of files seen is clearly larger than the number of files edited.**"
>
> — §7.3

---

## 3. Tricorder

Three primary sources, three vintages. Numbers differ because the dates differ; keep them separate.

- **[T15]** Sadowski, van Gogh, Jaspan, Söderberg, Winter, "Tricorder: Building a Program Analysis Ecosystem," ICSE 2015. Peer-reviewed. Data from 2014. https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43322.pdf
- **[T18]** Sadowski, Aftandilian, Eagle, Miller-Cushon, Jaspan, "Lessons from Building Static Analysis Tools at Google," *Communications of the ACM* 61(4), April 2018, 58–66. Invited magazine article, peer-reviewed venue. Data "as of January 2018." https://storage.googleapis.com/gweb-research2023-media/pubtools/4365.pdf (DOI 10.1145/3188720)
- **[T20]** *Software Engineering at Google*, Ch. 20 "Static Analysis," 2020. https://abseil.io/resources/swe-book/html/ch20.html

### The 10% rule

> "**Produce less than 10% effective false positives. Developers should feel the check is pointing out an actual issue at least 90% of the time.** To measure this, we run analyzers on existing code and manually check a statistically sound sample size of the results."
>
> Footnote 5: "**This 10% false positive threshold matches that used by other analysis platforms such as Coverity.**"
>
> — [T15] §IV-C, criterion 2 of 4 for admitting a new analyzer

The full four criteria [T15]: (1) "The warning should be easy to understand and the fix should be clear ... For example, cyclomatic complexity or location-based fault prediction does not meet this bar." (2) the 10% rule. (3) "The warning should be for something that has the potential for significant impact ... language-focused analyzers are vetted by language experts." (4) "The warning should occur with a small but noticeable frequency ... if a warning occurs too frequently, it's likely that it's not causing any real problems."

The definition that makes the rule enforceable is the *effective* false positive:

> "To an analysis writer, a false positive is an incorrect report produced by their analysis tool. However, to a developer, **a false positive is any report that they did not want to see**. We prefer to use the term *effective false positive* ... **We define an effective false positive as any report from the tool where a user chooses not to take action to resolve the report.**"

> "In contrast, we have found that if an analysis incorrectly reports a bug, but making the suggested fix would improve code readability, this is not considered a false positive."

> "**The bottom line is that developers will decide whether an analysis tool has high impact, and what a false positive is.**"
>
> — [T15] §III-A "No false positives"

Different bar for build-breaking checks:

> "These analyses break the build when they find an issue, so **the effective false positive rate must be essentially zero.** They also cannot significantly slow down compiles, so must have < 5% overhead."
>
> — [T15] §III-D

### "Please Fix" / "Not useful" and the enforcement mechanism

> "In order to respond quickly to issues with analyzers, we have built in a feedback mechanism that tracks how developers interact with the robocomments TRICORDER generates in code reviews ... there are four links that developers can click:
> - **NOT USEFUL** gives the developers the opportunity to file a bug about the robocomment.
> - **PLEASE FIX** creates a review comment asking the author to fix the robocomment and is only available to reviewers.
> - **PREVIEW FIX** ... shows a diff view of the suggested fix ...
> - **APPLY FIX** ... applies the suggested fix to the code and is available only to authors ...
>
> We define the 'not-useful rate' of an analyzer as:
> **NOTUSEFUL/(NOTUSEFUL + PLEASEFIX + APPLYFIX)**
>
> Analysis writers are expected to check these numbers through a dashboard we provide. **A rate ≥ 10% puts the analyzer on probation, and the analysis writer must show progress toward addressing the issue. If the rate goes above 25%, we may decide to turn the analyzer off immediately.** In practice, we typically work with the analyzer writers to fix the problem instead of immediately disabling an analyzer ... **Nonetheless, having a policy in place has proven invaluable in making expectations clear with analyzer writers.**"
>
> — [T15] §IV-E

The 2018 version states the threshold more bluntly (note the slight discrepancy with [T15]'s two-tier probation/disable):

> "The Tricorder team tracks such not-useful clicks, computing the ratio of 'Please fix' vs. 'Not useful' clicks. **If the ratio for an analyzer goes above 10%, the Tricorder team disables the analyzer until the author(s) improve it.** While the Tricorder team has rarely had to permanently disable an analyzer, it has disabled an analyzer (on several occasions) while the analyzer author is removing and revising subchecks that were particularly noisy."
>
> — [T18] §"Iterate on feedback from users"

And the contract with contributors [T15] §III-B: "we reserve the right to disable analyzers if: • No one is fixing bugs filed against the analyzer. • Resource usage ... is affecting TRICORDER performance ... • The analyzer results are annoying developers." Followed by: "**Our experience is that pride-in-work combined with the threat of disabling an analyzer makes the authors highly motivated to fix problems in their analyzers.**"

### Measured click data

**2014 [T15] §V:**
> "On an average day we run TRICORDER on **31K snapshots**, each with an average size of 12 files ... In total for one day, we report an average of **93K findings for around 30 categories**. TRICORDER also runs close to 5K builds per day. **Each day, reviewers click PLEASE FIX on an average of 716 findings (416 from the Linters), but only 48 findings get a not-useful click. An average CL has two please-fix clicks and no not-useful clicks.** Even though we are producing considerably more findings than are clicked on, most are not actually shown in the review as they appear on unchanged lines."

> "Figure 5 shows the week-over-week across all of the TRICORDER analyzers; **in recent months it is typically at around 5%. When we remove analyzers that are on probation, the number goes down to under 4%.**"

> "the Linter has received PLEASE FIX clicks from **over 18K users in 2014**. The number of people who have ever clicked NOT USEFUL is substantially lower across all categories."

> "**reviewers click PLEASE FIX an average of 5117 times each week**" — [T15] §VII

**January 2018 [T18] §"Scale of Tricorder":**
> "As of January 2018, Tricorder had analyzed approximately **50,000 code review changes per day**. During peak hours, there were **three analysis runs per second**. Reviewers clicked 'Please Fix' **more than 5,000 times per day**, and authors applied the automated fixes **approximately 3,000 times per day**. And Tricorder analyzers received 'Not useful' clicks **250 times per day**."

**2020 [T20]:**
> "Tricorder analyzes **more than 50,000 code review changes per day** and is often running several analyses per second."
> "Tricorder includes **more than 100 analyzers**, with most being contributed from outside the Tricorder team. **Seven of these analyzers are themselves plug-in systems that have hundreds of additional checks**, again contributed from developers across Google. **The overall effective false-positive rate is just below 5%.**"
> "Reviewers click 'Please Fix' thousands of times per day, and authors apply the automated fixes approximately 3,000 times per day. And Tricorder analyzers received 'Not useful' clicks 250 times per day."

The intermediate figure from the code-review paper (data Jan 2014–Jul 2016):
> "Currently, Tricorder includes **110 analyzers, 5 of which are plugin systems for hundreds of additional checks, in total analyzing more than 30 languages.**" — Sadowski et al. ICSE-SEIP 2018, §5.1

Ratio check for January 2018: ~250 not-useful vs. >5,000 please-fix plus ~3,000 applied fixes ≈ 3% not-useful rate against a 10% ceiling.

### Why they abandoned the dashboard

This is the single best-documented passage in the whole file for "centralize the machinery, not the decision," because it is three failures with numbers:

> "**Attempt 1. Bug dashboard.** Initially, in 2006, FindBugs was integrated as a centralized tool that ran nightly over the entire Google codebase, producing a database of findings engineers could examine through a dashboard. **Although FindBugs found hundreds of bugs in Google's Java codebase, the dashboard saw little use because a bug dashboard was outside the developers' usual workflow, and distinguishing between new and existing static-analysis issues was distracting.**
>
> **Attempt 2. Filing bugs.** The BugBot team then began to manually triage new issues found by each nightly FindBugs run, filing bug reports for the most important ones. In May 2009, hundreds of Google engineers participated in a companywide 'Fixit' week, focusing on addressing FindBugs warnings. **They reviewed a total of 3,954 such warnings (42% of 9,473 total), but only 16% (640) were actually fixed, despite the fact that 44% of reviewed issues (1,746) resulted in a bug report being filed.** Although the Fixit validated that many issues found by FindBugs were actual bugs, a significant fraction were not important enough to fix in practice. **Manually triaging issues and filing bug reports is not sustainable at a large scale.**
>
> **Attempt 3. Code review integration.** The BugBot team then implemented a system in which FindBugs automatically ran when a proposed change was sent for review, posting results as comments on the code-review thread ... Such integration was discontinued when the code-review tool was replaced in 2011 for two main reasons: **the presence of effective false positives caused developers to lose confidence in the tool, and developer customization resulted in an inconsistent view of analysis results.**"
>
> — [T18] §"What We Learned from FindBugs"

Restated as a lesson:

> "**Most developers will not go out of their way to use static analysis tools.** Following in the footsteps of many commercial tools, Google's initial implementation of FindBugs relied on engineers choosing to visit a central dashboard to see the issues found in their projects, **though few of them actually made such a visit. Finding bugs in checked-in code (that may already be deployed and running without user-visible problems) is too late.** To ensure that most or all engineers see static-analysis warnings, **analysis tools must be integrated into the workflow and enabled by default for everyone. Instead of providing bug dashboards**, projects like Error Prone extend the compiler with additional checks, and surface analysis results in code review."
>
> — [T18] §"Lessons Learned"

And the earlier statement of the same finding:

> "**We have repeatedly found that when developers have to navigate to a dashboard or run a standalone command line tool, analysis usage drops off.**"

> "the command-line tool was used by **only 35 developers in 2014 (and by 20 of those only once)**."
>
> — [T15] §II-B

Why the review is the right place:

> "TRICORDER introduces an effective place to show warnings. Given that all developers at Google use code review tools before submitting changes, TRICORDER's primary use is to provide analysis results at code review time. **This has the added benefit of enabling peer accountability, where the reviewer will see if the author chose to ignore analysis results.**"

> "The mean time for a review of more than one line is greater than 1 hour; **we typically expect analyses to complete in less than 5 − 10 minutes** (ideally much less), as developers may be waiting for results."
>
> — [T15] §III-D

> "The success of code-review analysis suggests it occupies a **'sweet spot'** in the developer workflow at Google. ... **After the review and code are checked in, the friction confronting developers for making changes increases.** Developers are thus hesitant to make additional changes to code that has already been tested and released, and lower severity and less-important issues are unlikely to be addressed."
>
> — [T18]

> "Code review is a sweet spot for analysis results" — because developers are already in a change-focused mindset, have context-switching time while awaiting reviews, and experience peer pressure to address issues. — [T20], paraphrased by the chapter

### Contribution by any engineer

> "In a company using a diverse set of languages and custom APIs, **no single team has the domain knowledge to write all needed analyses.** Relevant expertise and motivation exists among developers throughout the company, and we want to leverage this existing knowledge by empowering developers to contribute their own analyses ... **while these contributors are experts in their domains, they may not have the knowledge, or skill set, to effectively integrate their analyses into the developer workflow. Ideally, workflow integration and the boilerplate needed to get an analysis up and running should not be the concern of the analysis writer.**"
>
> — [T15] §III-B "Empower users to contribute"

> "**13 of the 16 analyzers in this table** (all except Formatter, BuildDeprecation, Builder) **were contributed by members of more than 10 other teams.** Many additional developers contributed plug-ins to analyzers such as ErrorProne, ClangTidy, or the Linter."

> "**the majority of all analyses running in TRICORDER are analyses contributed by developers outside the team managing TRICORDER itself.**"
>
> — [T15] §V(c) and §VII

> "**A small team of 2-3 people maintain TRICORDER and the ecosystem around it**, in addition to working on an open-source version of the platform."
>
> — [T15] §I

That last figure is the leverage claim in its cleanest form: 2–3 people maintain a platform that in 2018 touched 50,000 changes a day.

> "There are many domain experts at Google whose knowledge could improve code produced. **Static analysis is an opportunity to leverage expertise and apply it at scale by having domain experts write new analysis tools or individual checks within a tool.** ... We have focused on developing simple APIs that can be used by engineers throughout Google—not just analysis or language experts—to create analyses."
>
> — [T20]

### Project customization, not user customization

Directly relevant to "who owns the check":

> "Past experiences at Google showed that **allowing user-specific customization caused discrepancies within and across teams, and resulted in declining usage of tools.** We observed teams where a developer abandons a tool they were initially using after discovering teammates were committing new instances of code containing warnings flagged by the tool ... **To achieve this, we got rid of all priority or severity ratings for analysis results.** ... **Instead of having developers filter out analyzer results, we started getting bug reports about broken analyzers.**"

> "We do allow limited customization, but **the customization is project-based rather than user based.**"
>
> — [T15] §III-E

> "**In short, user customization resulted in hidden bugs and suppressing feedback.**"
>
> — [T20]

### The three lessons

> "**Focus on developer happiness.** We have invested considerable effort in building feedback channels between analysis users and analysis writers in our tools, and aggressively tune analyses to reduce the number of false positives.
> **Make static analysis part of the core developer workflow.** ... [enabled by default for everyone]
> **Empower users to contribute.** We can scale the work we do building and maintaining analysis tools and platforms by leveraging the expertise of domain experts."
>
> — [T20] "TL;DR"

> "**At Google, there is typically no mandate from management that engineers use static analysis tools. Engineers working on static analysis must demonstrate impact through hard data. For a static analysis project to succeed, developers must feel they benefit from and enjoy using it.**"
>
> — [T18]

Note the asymmetry with readability, and it is the chapter's whole argument: the *machinery* is adopted without a mandate and justified by click data; the *human shared reviewer* is mandatory and justified by a study whose numbers were never published.

---

## 4. Comparable shared reviewers elsewhere

### Microsoft — CodeFlow

Centrally owned: the tool, and nothing about who reviews.

> "Over the past two years, a common tool for code review at Microsoft has achieved wide-spread adoption. As it represents a common and growing solution for code review (**over 40,000 developers used it so far**), we focused on developers using this tool for code review—CodeFlow."

> "Each team has its own development culture and code review policies."
>
> — Bacchelli & Bird, "Expectations, Outcomes, and Challenges of Modern Code Review," ICSE 2013, §III. Peer-reviewed. https://sback.it/publications/icse2013.pdf

And, from Rigby & Bird as quoted in the Google paper:

> "Microsoft uses CodeFlow, which tracks the state of each person (author or reviewer) and where they are in the process (signed off, waiting, reviewing); **CodeFlow does not prevent authors from submitting changes without approval** and supports chats in comment threads."
>
> — Sadowski et al. ICSE-SEIP 2018, §2.1

**What is centrally owned:** the review tool and its state model. **What stays with the team:** the policy, the reviewer choice, and even whether approval is required at all. This is the *weakest* form of centralization of the four and a useful contrast to Google.

### Meta — reviewer recommender, Nudgebot, and the metrics

> "We track a metric that we call '**Time In Review**,' which is a measure of how long a diff is waiting on review across all of its individual review cycles. We only account for the time when the diff is waiting on reviewer action."

> "When we looked at the data in early 2021, our **median (P50) hours in review for a diff was only a few hours** ... However, looking at **P75** (i.e., the slowest 25 percent of reviews) we saw diff review time **increase by as much as a day**."

> "**The longer someone's slowest 25 percent of diffs take to review, the less satisfied they were by their code review process.** We now had our north star metric: P75 Time In Review."

> "However, simply optimizing for the speed of review could lead to negative side effects, like **encouraging rubber-stamp reviewing.** We needed a guardrail metric ... We settled on '**Eyeball Time**' – the total amount of time reviewers spent looking at a diff. An increase in rubber-stamping would lead to a decrease in Eyeball Time."

> "Historically, Meta's reviewer recommender looked at a limited set of data to make recommendations, leading to problems with new files and staleness as engineers changed teams. We built a new reviewer recommendation system, incorporating work hours awareness and file ownership information ... The result? A **1.5 percent increase in diffs reviewed within 24 hours** and an increase in top three recommendation accuracy (how often the actual reviewer is one of the top three suggested) **from below 60 percent to nearly 75 percent.**"

> "**Next Reviewable Diff** ... we found that this feature resulted in a **17 percent overall increase in review actions per day** ... and that engineers that use this flow perform **44 percent more review actions** than the average reviewer!"

> "we built **Nudgebot**, which was inspired by research done at Microsoft ... The average Time In Review for all diffs dropped **7 percent** (adjusted to exclude weekends) and the proportion of diffs that waited longer than three days for review dropped **12 percent**!"
>
> — "Move faster, wait less: Improving code review time at Meta," Engineering at Meta, 16 November 2022. Company engineering blog (not peer-reviewed; no sample sizes given for the experiments). https://engineering.fb.com/2022/11/16/culture/meta-code-review-time-improving/

**What is centrally owned:** the metric definitions (Time In Review, Eyeball Time), the recommender model, the nudging bot, the queueing UI. **What stays with the team:** who actually reviews — the recommender *suggests*, file ownership constrains, and the author picks. Meta centralized the routing and the measurement, never the approval.

Meta's Diff Authoring Time work (engineering.fb.com posts of 25 October 2024 and 16 January 2025) is about measuring how long authoring takes, not about who reviews. The 2024 post is a podcast episode summary with no data in the text; I did not find quotable numbers. Treat DAT as out of scope for this chapter unless the chapter needs a measurement-ownership example.

### Spotify — Golden Paths

The clearest primary statement anywhere of "opinionated default, opt-out permitted, support withdrawn":

> "[During Hack Week] eight top engineers gathered their forces and created a tutorial on the recommended way of using our services; it was named 'The Golden Path'. This is the way we support an easy and streamlined way of working. **If you are an adventurer you can of course leave the Golden Path and do your own thing, but then you will not have the same support.**"

> "The Golden Path — as we define it today — is the '**opinionated and supported**' path to 'build something' ... The '**blessed**' tools — those on the Golden Path — are visualized in the Explore section of our internal developer portal, Backstage."

> "**The idea behind having Golden Paths is not to limit or stifle engineers, or set standards for the sake of it.** With Golden Paths in place, teams don't have to reinvent the wheel, have fewer decisions to make, and can use their productivity and creativity for higher objectives."

> "Recently we have been exploring around the concept of what we call a **Golden State**. A Golden State is **a list of checks that engineers can use to know if their systems are following the Golden Path.** The ambitious end goal of Golden State is to get most of our engineering organisation to be on the Golden Path."
>
> — Gary Niemen, "How We Use Golden Paths to Solve Fragmentation in Our Software Ecosystem," Spotify Engineering, 17 August 2020. Company blog. https://engineering.atspotify.com/2020/08/how-we-use-golden-paths-to-solve-fragmentation-in-our-software-ecosystem/

Also worth noting for the leverage/freedom argument, because it is an admitted cost of the centralized model:

> "We used to have one technical writer per tutorial. But this didn't really scale ... So we ditched the technical writer model and went for a more centralized model to solve some of these larger issues. And, of course, what happens? **We created a second-order problem.** Because each tutorial covers the Golden Path for a particular engineering discipline, **we needed to distribute content ownership across a wide number of teams** ... but then we miss coordination at the level of the tutorial."

**What is centrally owned:** the blessed tool list, the tutorial, the Backstage surface, and (aspirationally) the Golden State checks. **What stays with the team:** the choice to leave, at the price of support. Note that "Golden State" is the point where Spotify's paved road starts to become a *check* — which is exactly the transition the chapter is about. I found no published evidence on whether Golden State checks ever became blocking.

### Netflix — the paved road

Primary source, verbatim:

> "Tooling and automation help to scale expertise, but no tool will solve every problem in the developer productivity and operations space. **Netflix has a 'paved road' set of tools and practices that are formally supported by centralized teams. We don't mandate adoption of those paved roads but encourage adoption by ensuring that development and operations using those technologies is a far better experience than not using them.** The downside of our approach is that the ideal of 'every team using every feature in every tool for their most important needs' is near impossible to achieve. **Realizing the returns on investment for our centralized teams' solutions requires effort, alignment, and ongoing adaptations.**"
>
> — Philip Fisher-Ogden, Greg Burrell, Dianne Marsh, "Full Cycle Developers at Netflix — Operate What You Build," Netflix TechBlog, 17 May 2018. Company blog. https://netflixtechblog.com/full-cycle-developers-at-netflix-a08c31f83249 (the live URL returns 403 to automated fetches; this text was read from the Internet Archive snapshot of that URL)

**Important correction to the brief:** the formulation "you are free to go off the paved road, but you own the consequences" does **not** appear in this post, and I could not locate it in any primary Netflix source. What Netflix actually published is weaker and more interesting — no mandate at all, adoption won by making the paved road better, and an explicit admission that this leaves coverage incomplete. Use the verbatim quote above; do not attribute the "own the consequences" phrasing to Netflix. See "What I could not verify."

**What is centrally owned:** the tools and practices, maintained by centralized platform teams. **What stays with the team:** everything, including the decision not to use them. Netflix is the extreme end of the spectrum — pure machinery, zero mandated check.

### The spectrum, for the chapter

| | Machinery centrally owned | Check mandatory | Who decides |
|---|---|---|---|
| Netflix paved road | yes | no | team |
| Spotify Golden Path | yes | no ("you will not have the same support") | team |
| Microsoft CodeFlow | tool only | no (tool does not block) | team policy |
| Meta recommender/Nudgebot | yes (routing + metrics) | review yes, *reviewer* no | author + file owners |
| Google Tricorder | yes | findings shown always; fixing is not forced | reviewer ("Please fix") |
| Google readability | yes | **yes** | central pool if no local certificate holder |

Readability is the only one on this list where a *person outside the team* must say yes.

---

## 5. Counter-evidence: what is lost when review moves away from the team

### Bacchelli & Bird 2013 — expectations vs. outcomes at Microsoft

Method and samples: "(1) observed 17 industrial developers performing code review, (2) interviewed [them], (3) surveyed **165 managers** (600 sent, **28% response rate**), and (4) surveyed **873 programmers and testers** (44% response rate), and (5) card-sorted **200 review threads corresponding to 570 comments** recorded by CodeFlow."

**The headline gap:**

> "Our results show that, although the top motivation driving code reviews is finding defects, **the actual outcomes are less about finding errors than expected**: Defect [finding] ... context and change understanding is the key of any review."

> "finding defects is the first motivation for code review for **383 of the programmers (44%)**, second motivation for 204 (23%), and third for 96 (11%)."

> "**Code Improvements:** The most frequent category, with **165 (29%)** comments, is code improvements ... **Defect Finding:** Although defect finding is the top motivation and expected outcome of code review for many practitioners, the category defect is only the fourth most frequent, out of nine items, with **78 (14%)** comments. Among defect comments, 65 are on logical issues ..., 6 on high-level issues, 5 on security, and 3 on wrong exception handling."

> "**Review comments about defects are few, comprising one-eighth of the total in our sample, and mostly address 'micro' level and superficial concerns; while programmers and managers would expect more insightful remarks on conceptual and design level issues.**"

**The findings that bear directly on a shared/outside reviewer — these are the strongest counter-evidence in the file:**

> "Participants explained that **when they own or are very familiar with the files being changed, they have a better context and it is easier for them to understand the change submitted**: 'when doing code review I start with things I am familiar with, so it is easier to see what is going on.' When they are file owners, they often do not need to read the description ... On the contrary, when they do not own files, or have to review new files, they need more information."

> "**Most of the respondents (798, i.e., 91%) answered positively** to the first question [whether it takes longer to review files they are not familiar with], motivating it with the fact that it takes time to familiarize with the code and 'learn enough about the files being modified to understand their purpose, invariants, APIs, etc.,' because 'big-picture impact analysis requires contextual understanding. **When reviewing a small, unfamiliar change, it is often necessary to read through much more code than that being reviewed.**'"

> "**the answer to the second question is positive in 716 (82%) cases. The main difference with file owner comments is that they are substantially deeper, more detailed and insightful.** A respondent explained: 'Comments reflect their deeper understanding – more likely to find subtle defects, feedback is more conceptual (better ideas, approaches) instead of superficial (naming, mechanical style, etc.)' another tried to boldly summarize the concept: '**Difference between algorithmic analysis and comments on coding style. The difference is big.**'"

> "Many interviewees eventually acknowledged that **understanding is their main challenge when doing code reviews** ... 'understanding the code takes most of the reviewing time.'"

> "The most difficult task from the understanding perspective is finding defects, immediately followed by alternative solutions."

> Warning about what a low-context reviewer produces: "'I've seen quite a few code reviews where someone commented on formatting while missing the fact that there were security issues or data model issues.'"

**Read against Google:** readability approval is, by definition, the low-familiarity case when no team member holds the certificate. Bacchelli & Bird's 91%/82% pair predicts exactly what Google's chapter 3 cost list names — more time, extra rounds, shallower comments. And it predicts the direction of the "hazing" complaint: a reviewer without file context can only reliably comment on style, which is precisely the category that autoformatters and Tricorder later took over.

Source: Alberto Bacchelli, Christian Bird, "Expectations, Outcomes, and Challenges of Modern Code Review," ICSE 2013, pp. 712–721. Peer-reviewed conference paper. https://sback.it/publications/icse2013.pdf

### Thongtanunam, McIntosh, Hassan, Iida 2016 — reviewing *is* ownership

> "Through a case study of **six releases of the large Qt and OpenStack systems**, we find that: (1) **67%-86% of developers did not author any code changes for a module, but still actively contributed by reviewing 21%-39% of the code changes**, (2) code ownership heuristics that are aware of reviewing activity share a relationship with software quality, and (3) **the proportion of reviewers without expertise shares a strong, increasing relationship with the likelihood of having post-release defects.**"
>
> — abstract

> "– 67%-86% of developers only contribute to a module by reviewing code changes. **18%-50% of these review-only contributors are documented core developers** of the studied systems.
> – **13%-58% of developers who are flagged as minor contributors by traditional code ownership heuristics are actually major contributors when their code review activity is considered.**
> – When traditional code ownership heuristics are refined by code review activity, we find that **modules without post-release defects tend to have a higher rate of developers in the minor author & major reviewer category, but a lower rate of developers in the minor author & minor reviewer category** than modules with post-release defects do.
> – Even when we control for several factors that are known to have an impact on software quality, **the proportion of developers in the minor author & minor reviewer category shares a strong, increasing relationship with the likelihood of having post-release defects in a module.**"
>
> — §8 Conclusions

Sample size: six releases; modules with 100% review coverage per release were 328, 438, 241, 326, 515, 499; modules with defects per release were 70 (21%), 77 (18%), 70 (29%), 123 (37%), 128 (25%), 198 (40%). Open-source systems (Qt, OpenStack), Gerrit-based, not industrial-proprietary.

**Why this matters for the chapter:** the defect signal is attached to *minor author **and** minor reviewer*. Repeated reviewing builds the same kind of ownership as repeated authoring. A shared reviewer who reviews a module once and never again is, by this measure, a minor reviewer — they do not accumulate the thing that correlates with fewer defects. Centralizing the reviewer doesn't just cost latency; on this evidence it forgoes the accumulation.

Source: Patanamon Thongtanunam, Shane McIntosh, Ahmed E. Hassan, Hajimu Iida, "Revisiting Code Ownership and its Relationship with Software Quality in the Scope of Modern Code Review," ICSE 2016. Peer-reviewed conference paper. PDF mirror: https://rebels.cs.uwaterloo.ca/papers/icse2016_thongtanunam.pdf (DOI 10.1145/2884781.2884852)

### Knowledge transfer and onboarding value of review

Google's own measurements, which cut *for* the educational argument and therefore for keeping review close to people who will keep working on the code:

> "In an attempt to measure knowledge transfer due to code review, [Rigby and Bird] built off of prior work that measured expertise in terms of the number of files changed, by measuring the number of distinct files changed, reviewed, and the union of those two sets. **They find that developers know about more files due to code review.**"

> "**Developers at Google who have started within the past year typically have more than twice as many comments per change.** ... We postulate that this decrease in commenting is a result of reviewers needing to ask fewer questions as they build familiarity with the codebase and **corroborates the hypothesis that the educational aspect of code review may pay off over time.**"

> "the number of distinct files edited and reviewed by engineers at Google, and the union of those two sets, increase with seniority (Figure 3) and **the total number of files seen is clearly larger than the number of files edited.**"
>
> — Sadowski et al. ICSE-SEIP 2018, §7.3 "Knowledge spreading"

And from Bacchelli & Bird, knowledge transfer is *expected* but barely *observed*:

> "Concerning the other expected outcomes of code reviews, we did not expect to find evidence about them, because of their more 'social'–thus harder to quantify—nature. Nevertheless, we found **some (12) comments specifically about knowledge transfer**, where the reviewers were directing the code change author to external resources."

12 of 570 comments. Use this carefully: it is a measurement of *explicit* knowledge-transfer comments, not of knowledge transferred, and the authors say so.

Also directly on point for readability's defenders, from Google's own discussion:

> "previous research has shown that typically one reviewer for a change will take on the task of checking whether code matches conventions; **readability makes this process more explicit.**"

> "a study of code ownership at Microsoft found that **changes made by minor contributors should be received with more scrutiny to improve code quality**; we found that this concept is enforced at Google through the requirement of an approval from an owner."
>
> — Sadowski et al. ICSE-SEIP 2018, §7.2. The Microsoft study referenced is Bird, Nagappan, Murphy, Gall, Devanbu, "Don't Touch My Code! Examining the Effects of Ownership on Software Quality," FSE 2011. https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/bird2011dtm.pdf

---

## What I could not verify

- **The measured added latency for a change that needs an outside readability approval.** No published Google source gives it. Chapter 3 names it qualitatively ("increased short-term code-review latency," "potential for additional rounds of code review"); Chapter 7 says logs showed certified authors "had their code reviewed faster and submitted it faster." Neither gives an effect size, a confidence interval, or a sample size. **Do not state a number for this in the chapter.**
- **How long it takes to obtain readability.** No published median, mean, or range. The process ends by reviewer judgement, not after a fixed number of CLs, so a single number may not exist.
- **What fraction of changes require an *external* readability reviewer.** The 2018 paper says "often only one reviewer is required since changes are often authored by someone with ownership and/or readability" and "fewer than 25% of changes have more than one reviewer," but neither figure isolates readability as the cause.
- **The Netflix "you are free to go off the paved road, but you own the consequences" wording.** Not present in "Full Cycle Developers at Netflix" and not found in any other primary Netflix source I could reach. The verified Netflix sentence is "We don't mandate adoption of those paved roads but encourage adoption by ensuring that development and operations using those technologies is a far better experience than not using them." Treat the "own the consequences" version as folklore unless someone locates the original.
- **Spotify Soundcheck.** Not covered here. I have no primary Spotify source describing Soundcheck's checks or their enforcement; the Golden Paths post mentions "Golden State" checks as an *exploration*, not a shipped mandatory gate. Do not assert that Spotify enforces checks.
- **Meta's Diff Authoring Time posts.** Both URLs verified live (25 Oct 2024; 16 Jan 2025) but the 2024 page body is a podcast summary with no extractable figures. No DAT numbers are quoted here.
- **The CACM article's own HTML.** cacm.acm.org returned 403; all [T18] quotes were taken from Google's hosted author PDF of the same article (https://storage.googleapis.com/gweb-research2023-media/pubtools/4365.pdf, DOI 10.1145/3188720). Text should be identical, but page numbers are from the PDF.
- **A discrepancy between Tricorder sources, unresolved.** ICSE 2015 §IV-E: "A rate ≥ 10% puts the analyzer on probation ... If the rate goes above 25%, we may decide to turn the analyzer off immediately." CACM 2018: "If the ratio for an analyzer goes above 10%, the Tricorder team disables the analyzer until the author(s) improve it." Either the policy tightened between 2015 and 2018 or the CACM article compressed it. If the chapter quotes the rule, quote the 2015 two-tier version, which is the more precise one.
- **Published *external* criticism of readability.** Everything critical quoted above is Google criticising itself, in a book Google published. I found no peer-reviewed study and no independent published complaint. This is a real limitation: the cost side of the readability story rests entirely on Google's own self-report.
- **Page 5 of the 2018 ICSE-SEIP PDF** does not extract as text (the text layer is missing for that page in the Ghostscript-produced file). The §4.2 and §5.1 quotes above, including the readability definition and Findings 1 and 2, were transcribed from a 150 dpi page render. They should be re-checked against the ACM DL version before publication.
