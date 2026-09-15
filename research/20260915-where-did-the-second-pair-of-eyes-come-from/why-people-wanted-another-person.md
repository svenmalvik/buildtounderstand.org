# Why People Wanted Another Person — verified primary-source facts

**Question this document answers:** What did people who introduced peer review, before and after pull requests, say the second person was for, and what did later empirical studies find about whether review actually delivers that?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 01, "Why People Wanted Another Person"

**Last updated:** 2026-09-15

Scope: primary-source verification only. All facts below were checked against the original paper, book, mailing-list post, or blog post, not against a summary, except where noted. This complements `pull-request-origins.md` in the `vce-context` research folder, which already establishes the historical timeline; this note goes deeper on the *reasons* developers gave.

## Main findings

Two different explanations for wanting a second person recur across fifty years, and they don't agree with each other.

The first is that people cannot see their own errors. Weinberg's 1971 concept of "egoless programming" states it directly: a programmer who sees code as an extension of self will not look hard for its errors. Fagan's 1976 inspection process, Wiegers's 2002 book, and Raymond's 1997 "Linus's Law" all restate the same claim in different words: another person sees what the author cannot.[^1][^2][^3][^4]

The second is that the empirical record does not support defect-finding as what review mostly does, once you look at what reviewers actually write. At Microsoft, defects were the top-ranked reason developers gave when asked why review exists, but only 14% of the comments they actually wrote were about defects; understanding the change was the stated main difficulty instead.[^5] At Google, the person who introduced review said the reason was to make code understandable to other engineers, not to catch bugs; bug-catching was a secondary benefit "recognized" afterward.[^6] At AMD, 87% of reviews recorded no defect at all.[^7]

So the two traditions point in different directions. The stated reason for wanting a second pair of eyes is usually defects. The reason review keeps existing, once you look at what it produces, looks more like understanding, consistency, and shared ownership.

## The claim that you cannot see your own errors

- Weinberg, *The Psychology of Computer Programming* (1971), ch. 4: "A programmer who truly sees his program as an extension of his own ego is not going to be trying to find all the errors in that program." He cites von Neumann as an early example of a programmer who "incessantly pushed his programs on other people to read for errors." (Verified only via a secondary quote collection citing the 2011 reissue; the original 1971 text was not reached.)[^1]
- Fagan 1976 gives the same idea an institutional form: inspections use a moderator "from an unrelated project" for objectivity, and the process is explicitly about *finding* errors, not fixing them: "the inspection is not intended to redesign, evaluate alternate design solutions, or to find solutions to errors; it is intended just to find errors!"[^2]
- Wiegers, *Peer Reviews in Software* (2002): "Finding my own errors is often hard because I am too close to the work." And in ch. 2: "Asking other people to point out errors in your work is a learned — not instinctive — behavior."[^3]
- Raymond's 1997 "Linus's Law", as corrected by Torvalds himself: "Somebody finds the problem, and somebody else understands it. And I'll go on record as saying that finding it is the bigger challenge." Raymond's own formal statement: "Given a large enough beta-tester and co-developer base, almost every problem will be characterized quickly and the fix obvious to someone."[^4]

## What formal inspection actually measured

Fagan's numbers are specific to one 1975 case study (eight COBOL modules, Aetna Life and Casualty) and should not be generalized past that:

- Design and code inspections found 82% of all errors eventually found in that program (38 of 46 per thousand lines of code); testing and six months of production use found the other 18%.[^2]
- The same case reported a 25% saving in programmer resources, because rework caught early is 10 to 100 times cheaper than rework caught late.[^2]
- Inspection efficiency drops after two hours, so sessions were capped near two hours.[^2]

These are the two headline numbers (82% and 25%) that later writing about inspections tends to repeat. Both come from one study, not from a industry-wide average.

## What later empirical studies found reviewers actually do

- **Bacchelli & Bird, Microsoft, 2013** (17 developers observed, 570 review comments classified, 165 managers and 873 programmers surveyed): finding defects was the top-ranked motivation for 44% of programmers, but in the comments they actually wrote, "code improvement" was the largest category (29%) and defects were fourth (14%). "Many interviewees eventually acknowledged that understanding is their main challenge when doing code reviews."[^5]
- **Sadowski et al., Google, 2018** (12 interviews, 44-respondent survey, logs of 9 million reviewed changes): the early employee who introduced review said its purpose was "to force developers to write code that other developers could understand," adding that "although it is great if reviewers find bugs, the foremost reason for introducing code review at Google was to improve code understandability and maintainability." Median reviewer count is 1; median full review latency is under 4 hours.[^6]
- **Rigby & Bird, 2013**, across Microsoft, AMD, Google-led, and open-source projects: the convergent, cross-organization number of active reviewers (beyond the author) is 2, not more. Review has shifted, in their words, "from a defect finding activity to a group problem solving activity." At AMD, 87% of reviews recorded no defect.[^7]
- **McIntosh et al., 2014** (Qt, VTK, ITK): low review coverage and low reviewer participation are statistically associated with more post-release defects, up to two and five additional defects per component respectively, though the coverage effect was significant in only two of the four releases studied. This is the strongest defect-outcome evidence in the set, and it is still narrow: three open-source C++ projects, not a general claim.[^8]
- **Gousios et al., 2014** (166,884 GitHub pull requests, 291 projects): among unmerged pull requests, only 13% were rejected for a technical reason. 53% were closed for reasons tied to the distributed, asynchronous nature of the process itself (the change went stale, conflicted, or was superseded).[^9]

## The organizational account: shared understanding, not a rule from above

Steve Smith's 2014 account of Atlassian's order-management system is useful because it describes review starting *without* a mandate: "We did this organically, with no mandate from higher-ups and no internal discussion. It just happened," after the team moved to Git and Bitbucket in 2011. His stated reasons: the system had grown too large for one person to understand fully, the team was adding new members, and "we were all aware that mistakes on our part could cost the company dearly." He contrasts this with a prior employer's Fagan-style inspections, which were "mandated by management, and largely regarded as an inconvenience," and were "the first casualty" whenever the schedule slipped. His closing point: "shared responsibility is not the same as abdicated responsibility." Note: no specific bug caught by a domain-expert reviewer is described in the post; the account only says he "felt a lot better" after adding two reviewers to a pricing change.[^10]

## Documenting review as a distinct act from authorizing a change

The Linux kernel's own tag history separates two things that a pull-request approval today often collapses into one click:

- `Signed-off-by:` was introduced by Torvalds in May 2004, during the SCO lawsuit, and is explicitly about provenance, not review: "This is not about proving authorship — it's about documenting the process." It certifies where a patch came from, not that anyone examined it.[^11]
- `Reviewed-by:` is a separate, later tag, proposed by Jonathan Corbet in October 2007 and merged into kernel documentation in April 2008. Its statement of oversight: "I have carried out a technical review of this patch to evaluate its appropriateness and readiness for inclusion into the mainline kernel," and it is explicitly "a statement of opinion," with the reviewer disclaiming "any warranties or guarantees." Uptake was partial: 123 uses in the 2.6.27 cycle, with LWN noting "most reviewers do not offer the associated tag, so their contribution goes unrecorded."[^12]

This is direct evidence that even in the community that produced the modern pull request, "someone signed off on this" and "someone reviewed this" were kept as two different, separately optional statements.

## Confidence and gaps

| Claim | Assessment |
| --- | --- |
| Fagan's 82% error-detection figure and 25% resource saving | High confidence for the one 1975 Aetna case; not a general industry figure. |
| Weinberg's exact wording on egoless programming | Medium confidence; sourced from a quote collection citing the 2011 reissue, not the 1971 original. |
| Bacchelli & Bird's ranked motivations and comment classification | High confidence; read from the full ICSE 2013 paper. |
| Google's stated original reason for review (understandability) | High confidence, from Sadowski et al. 2018 section 4.1, a retrospective account by one early employee, not a controlled study. |
| Gousios et al.'s 13%/53% rejection-reason split | High confidence; read from Table 3 of the ICSE 2014 paper. |
| The Atlassian post contains a documented bug caught by a domain reviewer | Not supported; the post does not describe one. |
| Reviewed-by originated with Linus Torvalds | Not supported; it originated with Jonathan Corbet after the 2007 Kernel Summit. Signed-off-by is the Torvalds tag, and it is about provenance, not review. |

## Sources

Sources accessed 15 September 2026, verified from primary PDF, HTML, or archived text by two independent research passes.

[^1]: Gerald M. Weinberg, *The Psychology of Computer Programming*, Van Nostrand Reinhold, 1971, ch. 4, "Programming as a Social Activity." Quoted via a collection citing the Silver Anniversary edition (Dorset House, 1998 / dotted reissue 2011); the 1971 text itself was not reached (Internet Archive copy access-restricted).

[^2]: Michael E. Fagan, ["Design and Code Inspections to Reduce Errors in Program Development"](https://www.ida.liu.se/~TDDC90/literature/lab-papers/fagan76.pdf), *IBM Systems Journal* 15(3), 182–211, 1976. pp.185–186 on rework cost; p.189, Table 1, on the Aetna error-detection figures; pp.190–191 on roles and the two-hour session limit; p.193 on "find errors, don't fix them."

[^3]: Karl E. Wiegers, *Peer Reviews in Software: A Practical Guide*, Addison-Wesley, 2002, [Preface](https://www.processimpact.com/karls_books/reviews_book/preface.pdf) p.P-1 and ch.2 p.2-1. Also Wiegers, ["Seven Truths About Peer Reviews"](https://www.processimpact.com/articles/seven_truths.pdf), *Cutter IT Journal*, July 2002, p.3–4, citing Tom Gilb on hours saved per defect found.

[^4]: Eric S. Raymond, *The Cathedral and the Bazaar*, version 3.0, section "Release Early, Release Often." First presented at Linux Kongress, Würzburg, May 1997 (exact day unresolved between sources).

[^5]: Alberto Bacchelli and Christian Bird, ["Expectations, Outcomes, and Challenges of Modern Code Review"](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/ICSE202013-codereview.pdf), ICSE 2013. Section III (methods), Section IV (Figure 3, ranked motivations), Section V (Figure 4, comment classification), Section VI.A ("Code Review is Understanding").

[^6]: Caitlin Sadowski, Emma Söderberg, Luke Church, Michal Sipko, Alberto Bacchelli, ["Modern Code Review: A Case Study at Google"](https://storage.googleapis.com/gweb-research2023-media/pubtools/4476.pdf), ICSE-SEIP 2018. Section 4.1 ("How it All Started"), Section 5.2 (quantitative review metrics).

[^7]: Peter C. Rigby and Christian Bird, "Convergent Contemporary Software Peer Review Practices", FSE 2013. Table 1 (projects); convergent practices CP1–CP5; AMD defect-recording figure.

[^8]: Shane McIntosh, Yasutaka Kamei, Bram Adams, Ahmed E. Hassan, "The Impact of Code Review Coverage and Code Review Participation on Software Quality", MSR 2014. Abstract and RQ1/RQ2 findings on Qt, VTK, ITK.

[^9]: Georgios Gousios, Martin Pinzger, Arie van Deursen, ["An Exploratory Study of the Pull-Based Software Development Model"](https://pinzger.github.io/papers/Gousios2014-pullbasedmodel.pdf), ICSE 2014. Section 8, Table 3 (350 manually classified unmerged pull requests).

[^10]: Steve Smith, ["Organic code reviews for a billion-dollar order system"](https://web.archive.org/web/2015/https://www.atlassian.com/blog/archives/organic-code-reviews-billion-dollar-order-system), Atlassian Blog, 27 October 2014. Retrieved via Wayback Machine; the live URL now redirects.

[^11]: Linus Torvalds, ["[RFD] Explicitly documenting patch submission"](https://lkml.iu.edu/hypermail/linux/kernel/0405.2/1301.html), LKML, 23 May 2004. Introduces `Signed-off-by:` and the Developer's Certificate of Origin in response to the SCO litigation.

[^12]: Jonathan Corbet, ["RFC: reviewer's statement of oversight"](https://lkml.iu.edu/hypermail/linux/kernel/0710.1/index.html), LKML, 8 October 2007, following discussion at the 2007 Kernel Summit. Merged into `Documentation/SubmittingPatches` by commit `ef40203a0982`, 28 March 2008, released in Linux 2.6.25, 17 April 2008. Uptake figure (123 tags in the 2.6.27 cycle) from Jonathan Corbet, ["Kernel development"](https://lwn.net/Articles/306169/), LWN, 11 November 2008.

## Related documents

- `pull-request-origins.md` (in the `vce-context` worktree, `research/pull-request-origins/`), for the historical timeline this note assumes.
- [`four-eyes-regulation.md`](./four-eyes-regulation.md), the regulatory root that chapter 01 also draws on.
