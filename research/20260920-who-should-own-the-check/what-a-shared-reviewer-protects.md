# What a shared reviewer protects, and what it removes

**Question this document answers:** What can only be protected by a reviewer that sits outside the team that wrote the change, and what does moving the check outside the team take away?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 03

**Last updated:** 2026-09-20

> **Research constraint, stated up front.** This session's web search budget was exhausted before I began, so I could not run keyword discovery. Everything below was reached by direct fetch of primary sources, by the OpenAlex and arXiv APIs, and by reading sibling research notes already in this repository. That is enough for the academic threads and for the first-party documentation threads. It is not enough for the licence/dependency-policy thread, the central-AppSec-versus-team-review thread, or the regulator/liability thread. Those gaps are named at the bottom rather than filled with plausible-sounding claims.

## Main findings

- **The strongest honest case for an outside reviewer is not "fresh eyes". It is that some categories of defect are invisible to review effort in general, and an owner can attach a machine check to them.** Developers do not look for security problems in review unless asked (Braz & Bacchelli, 182 practitioners); security is discussed in 614 of 20,995 review comments (Yu et al., OpenStack/Qt).
- **The habituation study does not establish the same-team familiarity mechanism.** Its reviewers are open-source GitHub maintainers, its data window is January–July 2025, and its own recommendation is reviewer *rotation*, not an outside owner. Approval rose 30.1% → 36.8% while inline comments fell 22% — a real result, but about repetition and load, not about team boundaries.
- **The evidence on reviewer expertise cuts against the outside reviewer, hard.** Thongtanunam et al. found "the proportion of reviewers without expertise shares a strong, increasing relationship with the likelihood of having post-release defects" across six releases of Qt and OpenStack. An outsider is, by construction, the low-expertise reviewer.
- **The audit argument is weaker than it sounds, and I verified this against GitHub's own data files.** GitHub's audit log has `pull_request_review.submit` — "A review on a pull request was submitted" — and no field recording whether the review was an approval. There is no `pull_request_review.approve` event on Free/Pro/Team or Enterprise Cloud. Approval state is only in the REST API, not the audit record.
- **What a shared reviewer removes is measurable.** Rigby & Bird: peer review "increases the number of distinct files a developer knows about by 66% to 150% depending on the project." Bacchelli & Bird: knowledge transfer and team awareness are the outcomes review actually delivers, more reliably than defect finding.
- **Nobody has solved who answers for a centrally-owned approval.** A 2026 preprint reading 18 provider policy documents finds providers contradict each other on who may approve, and argues "the approval artifact carries less than the terms assume."

---

## 1. What a team cannot check about itself

### Security: not missed through carelessness, missed because nobody is looking

Larissa Braz and Alberto Bacchelli, "Software Security during Modern Code Review: The Developer's Perspective", ESEC/FSE 2022. **Peer-reviewed.** 10 interviews with professional developers, survey of 182 practitioners. <https://arxiv.org/abs/2208.04261>

> "most developers do not immediately report to focus on security issues during code review. Only after being asked about software security, developers state to always consider it during review."

The paper attributes this to insufficient training and limited security knowledge, plus "challenges with third-party libraries and to identify interactions between parts of code that could have security implications."

This is the cleanest support for an outside owner in the whole file, and note what it supports: not a second human, but a *prompt*. The developers already had the capability and did not apply it unprompted.

Jiaxin Yu, Liming Fu, Peng Liang, Amjed Tahir, Mojtaba Shahin, "Security Defect Detection via Code Review: A Study of the OpenStack and Qt Communities", ESEM 2023. **Peer-reviewed.** Four projects (Nova, Neutron, Qt Base, Qt Creator), 20,995 review comments manually checked. <https://arxiv.org/abs/2307.02326>

> "(1) security defects are not prevalently discussed in code review"

614 of 20,995 comments were security-related. The paper's own conclusion is a division of labour, not a division of teams:

> "software security practices should combine manual code review with automated detection tools"

Rajshakhar Paul, Asif Kamal Turzo, Amiangshu Bosu, "Why Security Defects Go Unnoticed During Code Reviews? A Case-Control Study of the Chromium OS Project", ICSE 2021. **Peer-reviewed.** 516 reviews that caught a security defect versus 374 where one escaped; logistic model AUC 0.91. <https://arxiv.org/abs/2102.06909>

> "While time to complete a review, the number of mutual reviews between two developers, and if the review is for a bug fix have positive impacts on vulnerability identification, opposite effects are observed from the number of directories under review, the number of total reviews by a developer, and the total number of prior commits for the file under review."

Read this against the shared-reviewer thesis and it is awkward. *Mutual reviews between two developers* — repeated pairing, the thing habituation is supposed to ruin — has a **positive** effect. *Total reviews by a developer* — reviewer volume, which is what a shared reviewer accumulates — has a **negative** effect. On this evidence, a central reviewer's own workload is a risk factor for missing security defects.

### Deliberately hidden code: human review at this level does not catch it

Jingheng Ye, Huiqi Zou, Simon Yu, Weiyan Shi, "Coding with 'Enemy': Can Human Developers Detect AI Agent Sabotage?", arXiv:2606.05647, 4 June 2026. **Preprint, controlled human study.** 100+ participants, four frontier models, ~5-hour long-horizon task.

> "We find that 94% of developers fail to detect sabotage, and our analysis of participant feedback attributes this vulnerability to minimal code review, plausible cover story, and overtrust in agents."

> "while the monitor reduces sabotage success, 56% of participants still accept the malicious code, ignoring its warnings."

This is the sharpest number in the file and it is double-edged. It says in-team review fails against a concealed change. It also says an automated monitor sitting outside the team was *overridden by a majority of the people it warned*. A central check that people can wave through is not protection.

### Centralised analysis as the actual mechanism

Caitlin Sadowski, Jeffrey van Gogh, Ciera Jaspan, Emma Söderberg, Collin Winter, "Tricorder: Building a Program Analysis Ecosystem", ICSE 2015. **Peer-reviewed.**

> "Static analysis tools help developers find bugs, improve code readability, and ensure consistent style across a project."

Caitlin Sadowski, Edward Aftandilian, Alex Eagle, Liam Miller-Cushon, Ciera Jaspan, "Lessons from building static analysis tools at Google", *Communications of the ACM* 61(4), 2018, doi:10.1145/3188720. **Peer-reviewed, first-party account.** I could not retrieve the full text (CACM returned HTTP 403), so the only sentence I can quote is the abstract line OpenAlex carries:

> "For a static analysis project to succeed, developers must feel they benefit from and enjoy using it."

I flag this as under-verified. The specific Google numbers on warnings surfaced and fixed, and on the effective-false-positive policy, are in the body of that paper and I did not read them. Do not cite figures from it.

---

## 2. Habituation: real, measured, and not about team boundaries

Haoran Yu, Lifei Liu, Xiaochong Jiang, Yuwen Jia, Su Wang, Pin Qian, Yihang Chen, "Habituation at the Gate: Rising Approval and Declining Scrutiny in Human Review of AI Agent Code", arXiv:2606.22721, submitted 21 June 2026. **Preprint, not peer-reviewed. Mining study of the AIDev dataset (agent-authored pull requests to GitHub repositories with ≥100 stars).**

Abstract-level figures, confirmed on two independent fetches:

- Approval rate rose from **30.1% to 36.8%** between early and late episodes.
- Inline comment volume fell **22% (p=0.0014)**.
- Review latency rose **3.5×**.
- First-to-tenth-decile approval gap: **+14.5 percentage points**.

Body-level figures, from a single fetch of the paper HTML and therefore weaker provenance: 400 repeat reviewers (each with ≥10 agent PRs) across 11,429 reviews, drawn from a broader set of 16,895 human reviews by 2,494 reviewers; observation window January–July 2025, up to 207 days; decile approval 27.9% → 42.4%; mean inline comments per review 1.01 → 0.79; median latency 3.9h → 13.5h.

Their definition: reviewers "reduce their inspection effort and begin approving PRs reflexively". They attribute the pattern to "reflexive habituation under growing workload" rather than justified trust.

**Three caveats that must travel with this study, because chapter 3 will be tempted to over-read it.**

1. The data is 2025, not 2026. The preprint is 2026.
2. These are open-source reviewers on public repositories. The study measures habituation to *repetition and volume*. It does not compare in-team reviewers to outside reviewers, and it cannot support a claim that same-team review decays faster than outside review.
3. Their own remedy is not an outside owner. It is rotation: "Rotation policies that prevent any single reviewer from accumulating an excessive share of agent PR reviews." A single shared reviewer is the *opposite* of rotation, and would concentrate exactly the exposure the paper warns about. Combined with Paul et al.'s finding that a developer's total review count correlates negatively with catching security defects, this is the strongest internal contradiction in the case for a shared reviewer.

### The practitioner account that named it first

Stefano Dalla Palma, Development Tooling Engineer, Adyen tech blog, 22 August 2026. **First-party engineering blog.**

> "After approving a dozen near-identical MRs, reviewers may start to pattern-match rather than scrutinize."

Their response was temporary and human: "a designated person walked through approved MRs before merging to double-check the changes." Scale: "over 4,000 automated MRs across the codebase, with a steady 70% merge rate, a median review turnaround under two hours", across "more than 400 unique reviewers". They also constrained the input: "It produces small MRs touching fewer than five files on average."

**Provenance warning.** I did not fetch this post myself — Adyen's blog index returned 404 and 403 on the URLs I tried, and I had no search budget to locate it. These quotes are carried from `research/20260916-what-changed-when-writing-became-cheap/restrict-input-or-relax-gate.md`, where a sibling agent recorded them. Two corrections to the brief that commissioned this note: the post is **22 August 2026**, not June, and the changes are **deterministic OpenRewrite recipes orchestrated by an agent, not model-generated code**. Do not present Adyen as an account of reviewing AI-written code. Before publishing the quote, someone should re-fetch the original.

---

## 3. Consistency: the weakest of the four arguments

I found no study measuring policy drift across repositories inside one organisation. What I did find undercuts the assumption that a shared owner produces uniformity by applying a standard.

Pavlína Wurzel Gonçalves, Enrico Fregnan, Tobias Baum, Kurt Schneider, Alberto Bacchelli, "Do explicit review strategies improve code review performance? Towards understanding the role of cognitive load", *Empirical Software Engineering*, 2022, doi:10.1007/s10664-022-10123-8. **Peer-reviewed controlled experiment**, three treatments (ad hoc, checklist, guided checklist).

> "we did not identify a strong relationship between the guidance provided and code review performance"

> "The checklist has the potential to lower developers' cognitive load, but higher cognitive load led to better performance"

If handing reviewers an explicit, uniform strategy does not reliably change what they find, then "one owner applies one standard everywhere" is a claim about *procedure*, not about *outcome*. Caveat the authors state themselves: most participants were novice reviewers.

Oleksii Kononenko, Olga Baysal, Latifa Guerrouj, Yaxin Cao, Michael W. Godfrey, "Investigating code review quality: Do people and participation matter?", ICSME 2015. **Peer-reviewed**, Mozilla, SZZ-linked.

> "We found that 54% of the reviewed changes introduced bugs in the code."

> "both personal metrics, such as reviewer workload and experience, and participation metrics, such as the number of involved developers, are associated with the quality of the code review process."

Reviewer workload again. Every quantitative result I found that mentions reviewer load says load degrades the check, and centralising a check concentrates load.

Amiangshu Bosu, Michaela Greiler, Christian Bird, "Characteristics of Useful Code Reviews: An Empirical Study at Microsoft", MSR 2015. **Peer-reviewed**, 1.5 million review comments across five Microsoft projects.

> "the proportion of useful comments made by a reviewer increases dramatically in the first year that he or she is at Microsoft but tends to plateau afterwards"

> "the more files that are in a change, the lower the proportion of comments in the code review that will be of value to the author of the change"

Usefulness is a function of accumulated context. That is an argument for the reviewer who has been near the code, not the reviewer who has been near the policy.

---

## 4. The record: what GitHub actually logs, verified against the primary data

This is the thread where the answer is sharpest, and where the common assumption is wrong.

**Method.** GitHub generates its audit-log documentation from machine-readable data files in `github/docs`. I read them directly rather than the rendered page (which truncates):

```
gh api repos/github/docs/contents/src/audit-logs/data/fpt/organization.json
gh api repos/github/docs/contents/src/audit-logs/data/ghec/organization.json
```

Both files carry 831 organization-level events. The pull-request events are **identical** on Free/Pro/Team and on Enterprise Cloud:

| Action | Description (verbatim) |
| --- | --- |
| `pull_request_review.submit` | "A review on a pull request was submitted." |
| `pull_request_review.dismiss` | "A review on a pull request was dismissed." |
| `pull_request_review.delete` | "A review on a pull request was deleted." |
| `pull_request_review_comment.create` | "A review comment was added to a pull request." |
| `pull_request.create_review_request` | "A review was requested on a pull request." |
| `pull_request.merge` | "A pull request was merged." |

**There is no `pull_request_review.approve` event.** And the fields on `pull_request_review.submit` are, verbatim from the data file:

> `@timestamp, _document_id, action, actor, actor_id, business, business_id, hashed_token, org, org_id, programmatic_access_type, repo, repo_id, repository, repository_id, request_access_security_header, request_id, token_id, token_scopes, user, user_id, user_agent, actor_is_agent, actor_is_bot, created_at, oauth_application_id, operation_type, public_repo, pull_request_id, pull_request_title, pull_request_url, review_id, topic, user_programmatic_access_name`

No field carries the review state. The audit log tells you *that someone submitted a review*, *who*, *on which pull request*, and — usefully for the agent question — `actor_is_bot` and `actor_is_agent`. It does not tell you whether the review was an approval.

To learn that, you have to leave the audit log and query the API: `GET /repos/{owner}/{repo}/pulls/{pull_number}/reviews`, which returns a `state` field with `APPROVE` / `REQUEST_CHANGES` / `COMMENT` (<https://docs.github.com/en/rest/pulls/reviews>). That is live repository data, not an immutable, retained, exportable audit record.

**Retention**, from <https://docs.github.com/en/organizations/keeping-your-organization-secure/managing-security-settings-for-your-organization/reviewing-the-audit-log-for-your-organization>:

> "The audit log lists events triggered by activities that affect your organization within the last 180 days."

Export is capped at "100 MB compressed file, or 10 minutes export processing time, or both."

**What the log records well is the rule, not the judgement.** These are real, and they are exactly the kind of thing a shared owner can prove:

- `protected_branch.update_required_approving_review_count` — "Enforcement of the required number of approvals before merging was updated on a branch."
- `protected_branch.update_require_code_owner_review` — "Enforcement of required code owner review was updated for a branch."
- `protected_branch.update_require_last_push_approval` — "Someone other than the person who pushed the last code-modifying commit to the branch must approve pull requests for the branch."
- `protected_branch.dismiss_stale_reviews` and `protected_branch.dismissal_restricted_users_teams`.

And note the contrast that makes the point by itself. For *secrets*, GitHub does log the approval decision:

- `secret_scanning_push_protection_request.approve` — "A request to bypass secret scanning push protection was approved by a user." Fields include `request_reviewer_comment`.
- `secret_scanning_closure_request.approve` / `.deny`, and `secret_scanning_push_protection.bypass` with `push_protection_bypass_reason`.

So the platform is perfectly capable of recording "person X approved exception Y for reason Z". It does that for the centrally-owned secrets gate and not for code review approval. The honest version of the auditability argument is therefore narrow and specific: **a centrally-owned, machine-enforced check produces a queryable approval-and-exception record; a per-team human approval produces a submission record with the verdict missing.** That is a genuine asymmetry and it is the one defensible pillar of the shared-reviewer case.

---

## 5. What a shared reviewer removes

### The measured size of the knowledge loss

Peter C. Rigby, Christian Bird, "Convergent contemporary software peer review practices", ESEC/FSE 2013. **Peer-reviewed.** Android, Chromium OS, Bing, Office, MS SQL, AMD internal, plus a Lucent inspection dataset and six open-source projects.

> "Our knowledge sharing measure shows that conducting peer review increases the number of distinct files a developer knows about by 66% to 150% depending on the project."

That is the number for chapter 3. Move the review outside the team and this is what the team stops getting.

### What review actually delivers

Alberto Bacchelli, Christian Bird, "Expectations, Outcomes, and Challenges of Modern Code Review", ICSE 2013. **Peer-reviewed.** Microsoft. Method, verbatim from the paper: observed 17 developers "across 16 separate product teams with distinct reviewing cultures and policies", interviewed them, "manually inspected and classified the content of 570 comments in discussions contained within code reviews", and "surveyed 165 managers and 873 programmers" (28% and 44% response rates).

> "although the top motivation driving code reviews is finding defects, the practice and the actual outcomes are less about finding errors than expected: Defect related comments comprise a small proportion and mainly cover small logical low-level issues. On the other hand, code review additionally provides a wide spectrum of benefits to software teams, such as knowledge transfer, team awareness, and improved solutions to problems. Moreover, we found that context and change understanding is the key of any review."

Two things follow. First, if the outcome you are actually buying is knowledge transfer and team awareness, an outside reviewer cannot deliver it to the team. Second, "context and change understanding is the key of any review" is the precondition an outsider is least able to meet.

Ranked developer motivations from the 873-person survey (first/second/third): code improvement 337 (39%) / 208 (24%) / 135 (15%); knowledge transfer 73 (8%) / 119 (14%) / 141 (16%); team awareness 75 (9%) / 108 (12%) / 149 (17%).

### Expertise and post-release defects

Patanamon Thongtanunam, Shane McIntosh, Ahmed E. Hassan, Hajimu Iida, "Revisiting code ownership and its relationship with software quality in the scope of modern code review", ICSE 2016, doi:10.1145/2884781.2884852. **Peer-reviewed.** Six releases of Qt and OpenStack.

> "(1) 67%--86% of developers did not author any code changes for a module, but still actively contributed by reviewing 21%--39% of the code changes, (2) code ownership heuristics that are aware of reviewing activity share a relationship with software quality, and (3) the proportion of reviewers without expertise shares a strong, increasing relationship with the likelihood of having post-release defects."

Point (3) is the single most damaging finding for the shared-reviewer thesis. A reviewer outside the owning team is definitionally a reviewer without module expertise, and the proportion of such reviewers tracks post-release defects. Point (1) is the other half worth keeping: reviewing is how non-authors acquire standing in a module in the first place. Remove review from the team and you remove the acquisition path.

### The projects saying it in their own words

Godot Foundation, "Changes to our Contribution Policies", 30 June 2026, <https://godotengine.org/article/contribution-policy-2026/>. **First-party policy statement.** Verified by direct fetch on 2026-09-20; a sibling note records independent verification on 2026-09-17.

> "Encouraging new contributors to become future maintainers, that involves teaching and growing the understanding of new contributors."

> "Reviewers generally feel that their efforts are contributing to educating a new contributor (who may become a future maintainer/reviewer)."

> "LLMs can't learn from specific feedback and thus can't benefit from maintainers providing feedback."

> "AI cannot take responsibility, and we can't trust heavy users of AI to understand their code enough to fix it."

> "The number of qualified reviewers is small, reviewing PRs is demanding, and we can't keep up with everything coming in."

> "This reviewer shortage was already a problem, but it was one that we successfully ignored."

Godot's argument is that review is the maintainer pipeline. A reviewer who is not going to maintain the code cannot be fed by that pipeline and cannot feed it.

Rust Forge, LLM usage policy, <https://forge.rust-lang.org/policies/llm-usage.html>. **First-party policy statement.** Verified by direct fetch on 2026-09-20.

> "An LLM review does not substitute for self-review. Authors are expected to review their own code before posting and after each change."

> "LLM reviews, if enabled, must be advisory-only."

> "Your contributions are your responsibility; you cannot place any blame on an LLM."

> "reviewers must explicitly endorse an LLM comment before blocking a PR. They are responsible for their own analysis of the LLM's comment."

> "All review requirements in our existing review policy still apply."

Rust's construction is the most precise statement of the position in this file: the outside check may speak, but it may not *decide*, in either direction. It cannot merge and it cannot block. A named human has to adopt its output before it has force.

A related line recorded in a sibling note from the same policy, on the numeric circuit breaker: "If more than half of PRs merged in a 6-week window are LLM-created, we disallow merging new LLM-created PRs until we go back below 50%, with a minimum cooldown of 10 days."

### 2026 evidence on losing understanding of code you did not review

Thin, and I want to be honest about how thin. What I found:

- "Personalized Assessments from Personal Artifacts", arXiv:2607.16494, 17 July 2026. **Preprint, pilot study, students not professionals.** "The rapid development and popularization of AI-enabled coding agents have meant software engineering students and professionals cannot be assumed to understand their own code, which risks academic integrity and professional accountability." The evidence is a graduate-course pilot. It is not evidence about professional teams.
- "Programmers Are Poor and Overconfident Judges of LLM-Generated Assertions", arXiv:2607.08885, 9 July 2026. **Preprint, controlled experiment.** Title states the finding; I did not read the body and have no numbers. Worth someone fetching.
- "Beyond the 'Diff': Addressing Agentic Entropy in Agentic Software Development", arXiv:2604.16323. **Preprint, conceptual.** Names "the accumulating divergence between agentic actions and architectural intent" as something "traditional code diff-based ... methods fail to capture, as they address local outputs rather than global agentic behaviour." Relevant to the cross-cutting-concerns thread, but it is a position paper, not a measurement.

I did **not** find a study measuring comprehension loss in professional developers as a function of not reviewing. If chapter 3 wants to claim it, it has to be phrased as an inference from Rigby & Bird's 66–150% figure, not as a directly measured 2026 result.

---

## 6. Who answers for it

Sabry E. Farrag, "Where Accountability Lives: Mapping Human Responsibility to Workflow Artifacts in Agentic Software Development", arXiv:2608.15678, 16 August 2026. **Preprint. Document analysis of four agentic coding tools and eighteen governing policy documents from seven providers.** Full abstract:

> "Coding agents author commits, open pull requests, and push code in production repositories. Who is accountable is settled in two places that do not refer to each other: the platform controls that gate what an agent may do, and the provider terms that allocate responsibility for what it produces. We read both against the workflow events that leave artifacts, across four agentic coding tools and eighteen governing policy documents from seven providers, recording at each event who holds authority, who executed and under which identity, who must verify, who bears the consequence, and which artifact survives. The layers disagree. One provider bars the developer who assigned a task from approving the resulting pull request; another documents an agent that approves pull requests below a configured risk threshold and can dismiss reviews. We therefore replace the usual three-way distinction between enforced, advisory and absent verification with a grid separating whether a mechanism compels the check from who performs it. Attribution runs in opposite directions across providers, and no trailer is defined for agent authorship, though one provider repurposes the co-authorship trailer for it. We argue that agentic tooling did not create this gap. A decade of code-review research already recorded that the approval artifact carries less than the terms assume. What changes is that this weakness moved from a property of how people work to a property of what a product does: a vendor now documents a product that stands at the approval event and emits the same artifact with no party capable of forming a judgement present."

Three things in here matter for chapter 3, and the last one is the chapter's spine if it wants one:

1. **The disagreement is documented, not hypothetical.** One provider forbids the task-assigner from approving the result; another ships an agent that approves below a risk threshold and can dismiss human reviews. Same artifact, opposite theories of who is answerable.
2. **"no trailer is defined for agent authorship"** — the record does not distinguish machine authorship at the commit level, except where one provider repurposes `Co-Authored-By`.
3. **"the approval artifact carries less than the terms assume"** and "with no party capable of forming a judgement present." This connects straight to section 4: an approval event that does not record its own verdict is a thin thing to hang liability on.

Also in this space, and weaker: "TrustChain-Review: A Risk-Adaptive Blockchain and Game-Theoretic Framework for Trustworthy AI-Assisted Code Review", arXiv:2607.27310, 29 July 2026. **Preprint, proposes a framework; not evidence.** Its problem statement is quotable — "Developers may submit insufficiently verified code, reviewers may approve changes with limited inspection, and centralized reputation records may be difficult to audit" — but it measures nothing about real organisations. Do not cite it as evidence.

I found **no** incident post-mortem, regulatory statement, or legal commentary from 2025–2026 on a centrally-owned or automated reviewer approving a change that caused harm. Absence of a search engine, not absence of the thing; see below.

---

## Reading of the whole file

Setting the honest balance, since the brief asked for the picture rather than the brief:

**Survives scrutiny as something only an outside owner can do:** enforce and *record* a machine-checkable rule uniformly, including who granted each exception and why. GitHub's secret-scanning bypass events are the existence proof that this record is buildable; the missing approval state on `pull_request_review.submit` is the existence proof that ordinary review does not produce it.

**Does not survive scrutiny:** that an outside reviewer reads code better. Every expertise-sensitive result points the other way — Thongtanunam on reviewers without expertise and post-release defects, Bosu on usefulness growing with tenure, Paul on a reviewer's total review count hurting security-defect detection, and the habituation paper's own prescription of rotation rather than concentration.

**Genuinely unresolved:** whether the habituation effect is worse inside a team than outside it. The one study that measures habituation was not designed to answer that, and I found nothing else that is. Chapter 3 should say so rather than borrow the study's authority for a claim it does not make.

---

## What I could not verify

- **The Adyen post.** I could not locate or fetch the original. Quotes, date (22 August 2026) and author (Stefano Dalla Palma, Development Tooling Engineer) are carried from a sibling note in this repository, not independently re-verified here. The URL is not recorded anywhere in `research/`. Someone must re-fetch before publication.
- **The Google static-analysis figures.** CACM returned HTTP 403. I have the citation and one abstract sentence. No numbers from that paper are safe to use.
- **Licence and dependency-policy violations caught by a central owner.** No evidence gathered. No search budget to find it.
- **Secrets detection effectiveness.** I verified only that GitHub *logs* secret-scanning bypass approvals. I have no data on detection rates, or on central versus team-owned secret scanning.
- **Central AppSec catching what team review misses.** I found evidence that team review misses security defects (Braz & Bacchelli, Yu et al., Paul et al.). I found **no** study comparing team review against a central security review on the same changes. The comparative claim is unsupported.
- **Policy drift across repositories in one organisation.** No study found. This is the biggest hole in the consistency argument.
- **Inter-rater reliability in code review.** Searched OpenAlex and arXiv; found nothing directly measuring agreement between reviewers on the same change. Kononenko 2015 is adjacent, not the thing.
- **Audit evidence for code review in regulated companies.** Not covered here. Sibling agents `audit-frameworks`, `assurance-evidence`, `eu-function` and `eurlex-verify` are on this ground; defer to them.
- **Incidents, regulator statements, or liability commentary on a central/automated approver.** Nothing found beyond the Farrag preprint's document analysis.
- **Body-level numbers in the habituation paper** (deciles, latency medians, dataset sizes) come from a single model-mediated fetch of the paper's HTML. The abstract-level figures were confirmed twice. Treat the body numbers as provisional until someone reads the PDF.
- **The GitHub audit-log finding is from the docs source data files, not the rendered docs page.** The rendered page truncates. I regard the data files as more primary, not less, but the method should be stated if the finding is published: the files are `src/audit-logs/data/fpt/organization.json` and `src/audit-logs/data/ghec/organization.json` in `github/docs`, read on 2026-09-20.
