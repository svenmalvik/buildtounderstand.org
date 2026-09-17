# Restrict the input, or relax the gate

**Question this document answers:** When review capacity ran out, what did projects and companies actually do about it?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 02, "Restrict the Input, or Relax the Gate"

**Last updated:** 2026-09-17

Scope: published responses only, verified at source. The European fintech evidence is tracked separately below because the author works at a Norwegian payment company and that audience is the one the piece is written for.

## Main findings

**Two opposite responses exist, and the split is not open source against companies.** Open-source projects restricted what may be submitted while keeping human approval. Meta relaxed the gate and merges low-risk changes automatically. But Shopify and Monzo faced the same pressure and kept the approver, finding their throughput elsewhere.

**The most important finding is that the shortage predated AI.** Two maintainers say so independently, in their own words. AI did not create the capacity problem. It removed the option of ignoring it.

**One project reversed its restriction, and the reason is instructive.** netbox banned machine-written contributions and undid it two days later, replacing a ban it could not enforce with a gate a bot can check. Across 92 tracked policy files it is the only loosening case; the rest tightened.

## The shortage was already there

This is the framing the section should adopt, because it comes from the people carrying the load.

Godot Foundation, "Changes to our Contribution Policies", 30 June 2026:

> "This reviewer shortage was already a problem, but it was one that we successfully ignored."

> "the number of qualified reviewers is small, reviewing PRs is demanding, and we can't keep up with everything"

Mike McQuaid of Homebrew, quoted by GitHub on 18 June 2026:

> "We've had problems on Homebrew for a while with enthusiastic users submitting many pull requests that need near identical review. AI further accelerated it."

Two independent projects, the same claim: the problem is older than the tools, and the tools made it unignorable.

## Restricting the input

### Godot: restrict contributions, keep the approver

"Changes to our Contribution Policies", 30 June 2026, `https://godotengine.org/article/contribution-policy-2026/`. **RESTRICTS INPUT.**

Four restrictions, quoted exactly:

> "No autonomous AI agent use or vibe coding"

> "No use of AI to generate substantial pieces of code"

> "If you do use AI in some capacity to author code, you must disclose it"

> "No AI-generated text in human-to-human communication"

Human approval is retained and made explicit: "All PRs must be reviewed and approved by a human before merging".

The policy distinguishes minor assistance from prohibited use. Code completion, regular-expression help and find-and-replace remain permitted. On translation: "Machine translations are still acceptable as long as the original content was written by a human".

This is the cleanest single source for the restriction side. It restricts input, keeps the gate, and says the capacity problem is older than AI.

### Rust: a numeric circuit breaker, inside a declared experiment

Inside Rust, "rust-lang/rust is adopting an LLM policy", 5 August 2026, and the Rust Forge LLM usage policy at `https://forge.rust-lang.org/policies/llm-usage.html`. **RESTRICTS INPUT.**

The circuit breaker, verbatim:

> "If more than half of PRs merged in a 6-week window are LLM-created, we disallow merging new LLM-created PRs until we go back below 50%, with a minimum cooldown of 10 days."

On self-review:

> "All review requirements in our existing review policy still apply. A review from a project member does not substitute for self-review."

Machine-written changes are permitted rather than banned:

> "Pre-arranged, non-critical, high-quality, well-tested, and well-reviewed code changes that are originally created by an LLM are allowed, with disclosure."

**Two corrections to earlier framing.** The circuit breaker is live policy, not a proposal. But the surrounding policy is explicitly time-boxed: "This experiment is meant to inform future non-experimental policy, not to serve as the perpetual LLM usage policy." So it is policy in force inside a self-declared experiment.

**Do not write that the circuit breaker has never tripped.** Neither document says either way, and absence of a statement is not evidence.

Scope is narrow: five teams, covering compiler, libs, types, rustdoc and bootstrap, across the repositories rust-lang/rust, rustlings, mdBook, cargo, rust-clippy and rustfmt. Not project-wide.

### GitHub: a cap on open pull requests

"How pull request limits are cutting down the noise", 18 June 2026. **RESTRICTS INPUT.**

The mechanism: a cap on how many open pull requests a user **without write access** may have in a repository. Draft pull requests do not count toward it. AI-generated pull requests do count. Trusted contributors can be placed on a bypass list. Repository admins configure it under interaction limits, and organisation-level limits followed on 6 August 2026.

Whether it is on by default is not stated in the post. Treat as unverified.

Maintainer quotes on submission pressure, all from that post:

> Nicholas Tindle, AutoGPT: "It's helped us want to review pull requests again. Knowing that someone hasn't just opened 5-10 pull requests that are slop makes it much easier to want to look."

> Vincent Koc, OpenClaw: "We get a huge volume of pull requests from the community and had to build our own bots for fighting spam."

The AutoGPT quote is the most human evidence in this research. The cost of the queue is not only time, it is the willingness to look at all.

### What the policies say across projects

Hora, Robbes and Zacchiroli, arXiv 2609.07542, 7 September 2026. Figures confirmed: 83.3 per cent permit or encourage AI in code contributions, 14.9 per cent forbid it, 67.3 per cent require substantial human involvement, 48.8 per cent require disclosure.

**Two corrections.** It is **281 policies, not 281 repositories.** Repositories were drawn from the SEART GitHub search engine, filtered to at least 100 commits, not forks, and at least one commit in 2026, taking the top 2,000 by stars plus 36 well-known organisations including Apache, the Linux kernel, OpenJDK, LLVM and Zig. Median star count 27.2K. That yielded 281 policies.

And it **extends an earlier paper by the same authors**, described in the paper as "our previous preliminary study", raising the analysed projects from 1,000 to 2,000 and the policies from 118 to 281. The earlier work reported 78 per cent allowing AI-assisted contributions. The two are therefore not independent confirmations. Cite the September paper only. For genuine independent corroboration, use Robles and German, arXiv 2609.07919, published the same day by different authors.

The defensible summary is conditional acceptance: most projects permit machine-written contributions, and most of those attach conditions.

### curl: restrict by removing the incentive

The strongest restriction story in this research, and a different strategy from the others. curl did not add a rule. It removed a reward.

Daniel Stenberg, "Death by a thousand slops", 14 July 2025, gives the volume: "about 20% of all submissions" were AI slop, against "about 5% of the submissions in 2025 had turned out to be genuine vulnerabilities". At that point nothing had changed: "we are not going to do anything rushed or in panic immediately".

Then, "The end of the curl bug-bounty", 26 January 2026. The programme stopped on 31 January 2026. The stated cause was an "explosion in AI slop reports combined with a lower quality even in the reports that were not obvious slop". The confirmation rate "plummeted to below 5%. Not even one in twenty was real". Lifetime totals were 87 confirmed vulnerabilities and over 100,000 US dollars paid. Reports are still accepted, without payment.

**RESTRICTS INPUT**, by removing an incentive rather than adding a prohibition. Useful for the section because it shows a third option beyond restricting and relaxing: change what the submission is worth.

### Outright bans, including one that predates the wave

QEMU declines contributions that "include or derive from AI generated content. This includes ChatGPT, Claude, Copilot, Llama and similar tools." It permits "other uses of AI, such as researching APIs or algorithms, static analysis, or debugging, provided their output is not included in contributions." So the line is drawn at output entering the contribution, not at tool use.

Gentoo, adopted 14 April 2024: "It is expressly forbidden to contribute to Gentoo any content that has been created with the assistance of Natural Language Processing artificial intelligence tools." Still in force, and it predates the 2026 wave by over a year, which supports the point that this concern is older than the current volume problem.

Both **RESTRICT INPUT.**

### The one reversal, and what it actually means

Found, and the turnaround was two days. Verified from raw commit data rather than a page summary.

netbox-community/netbox prohibited AI-generated issues on 5 May 2026, then on 7 May 2026 committed "Remove prohibition on AI-generated PRs and add guidance to AGENTS.md". The deleted text was:

> "Any contributions which include solely AI-generated content will be rejected. All PRs must be submitted by a human."

**Read carefully before using.** This is not a retreat from restriction. They replaced a ban they could not enforce with a gate a machine can verify: an open, self-assigned issue is now required before any pull request, waived only for maintainers. The issue-side restriction survived, and the guide still says AI-generated issues "may be rejected without further discussion".

So the lesson is about enforceability, not about restriction failing. The restriction that survived is the one a bot can check.

**Rarity is corroborated.** Across 92 tracked policy files in the policy study, revisions overwhelmingly tightened, and netbox is identified as the lone loosening case.

## Relaxing the gate

Covered in detail in [`machine-approval-and-two-responses.md`](./machine-approval-and-two-responses.md). In brief:

- **Meta** merges qualifying low-risk changes automatically after automated review, "has reviewed 535K+ diffs and landed 331K+", with the assurance standard set by a tunable risk percentile.
- **GitHub** made machine approval able to satisfy a required-approvals rule on 1 September 2026, defaulting to off and marked public preview.
- **Dependency auto-merge** has been the accepted precedent for years, with the test suite as the substitute control.

## The third answer: move the review earlier

Added after a reader pointed out that the restrict-or-relax framing missed an option. It is the strongest finding of that follow-up.

### The same tool runs on both sides of the submission line

Timing verified from vendor documentation on 17 September 2026, not inferred.

| Tool | Side of the line | Evidence |
| --- | --- | --- |
| Codex CLI `/review` | Pre-submission | "Run a dedicated review against uncommitted changes, a commit, or a base branch." |
| Claude Code `/code-review` | Pre-submission | "reviews your branch's commits ahead of its upstream plus any uncommitted changes" |
| CodeRabbit CLI | Pre-submission | "Get AI code reviews directly in your CLI before you commit." |
| Cursor Bugbot `/review-bugbot` | Pre-submission | "reviews your branch changes: every change relative to the base branch" |
| Cursor Bugbot, default | Post-submission | "Runs automatic reviews on every PR update" |
| Anthropic Code Review | Post-submission | "reviews trigger when a PR opens, on every push, or when manually requested" |
| Claude Code GitHub Action | Post-submission | triggers on `pull_request` events |
| Gemini Code Assist on GitHub | Post-submission | "invoke Gemini Code Assist at any stage of the pull request to review the code" |

**The structural fact that matters.** Anthropic ships one review skill with two delivery paths, and its documentation points from the post-submission product to the pre-submission one, describing the latter as a way to "run `/code-review` in a local Claude Code session to check a diff before pushing". Cursor does the same. So pre-submission review is not a separate category of tool. It is a placement choice, and the vendors present it as the author's convenience rather than as a change to the review model.

**Why that is worth saying in the prose.** Where the reviewer runs decides whether anyone independent has seen the change. Chapter 01 establishes that the regulation asks for independence between the function that approves and the functions that request and implement. A reviewer the author runs on their own branch is the same function. So the earlier placement may be the better engineering practice and the weaker independence claim, and nobody in the tooling treats that as a governance question.

### The one team account

Anthropic, "How Anthropic secures its AI-native software development lifecycle", 21 July 2026. **MOVES REVIEW EARLIER, human reviewer retained only by risk tier.**

> "Our team started with a CLAUDE.md file that instructs the agent to run /security-review as a final step before opening a PR."

> "Some of our customers choose to integrate /security-review with a PreToolUse hook, which makes this step a harder gate."

Human review is retained selectively rather than per change: the post describes "reserving human review for regulated or truly critical code" and states that "Human accountability is still central for code that is reviewed and merged by Claude", with humans sampling automated approvals.

So in practice the third answer combines with the second. Moving the check earlier is what makes relaxing the gate defensible for lower tiers.

### Does the author's own machine review count as self-review? One project says no

This is the direct answer to whether moving the check earlier discharges the author's duty, and it comes from the Rust policy file announced 5 August 2026:

> "An LLM review does not substitute for self-review. Authors are expected to review their own code before posting and after each change."

The same file permits private pre-submission review, keeps bots non-blocking, and forbids substitution on the other side too: teams "may not have a policy that an LLM review substitutes for a human review."

No counter-example was found anywhere. No policy or engineering account treats a machine review the author ran as meeting a self-review obligation.

### Progressive delivery adds a control, it does not replace review

Scarlett Attensil, LaunchDarkly, 15 September 2026, argues runtime controls are a missing addition rather than a replacement, and that build-side gates including review remain necessary. Its framing line is the sharpest sentence found in this entire research:

> "Reviewers like AI code more than production does."

The data behind it is the New Relic 2026 report, 200 US technology decision-makers, **SELF-REPORTED**: 94 per cent rate AI-written code as higher quality at review, 78 per cent report more production incidents, and 82 per cent hit an AI-attributable failure within six months.

Carry the caveats: 200 respondents, decision-makers rather than reviewers, United States, self-reported, and the report is vendor-published. But the contrast between 94 and 78 is the cleanest available statement of the assurance failure, and it belongs in the chapter wherever outcomes are discussed.

### Stacked diffs: no AI claim

Graphite makes no AI-volume claim. Its one figure is a vendor-published customer result, Asana "saving up to 7 hours per week on code reviews", one company, with AI unmentioned. Meta's RADAR is the real result in this space, and it kept the diff while changing the approver.

### Is the pull request the wrong unit?

The strongest formulation is a vision paper with no data, arXiv 2605.17548, 17 May 2026, in which "reviewers transition from manual inspectors into supervisory operators of agents". Against it, the synthesis of 3,100 coded documents surfaces no practitioner proposal to abandon the pull request and concludes that "review is the control point through which a coding agent's effect on software is decided."

### Pairing and segregation of duties

**Not found** in any audit, banking, or ISO source. The DevOps Research and Assessment program's capability page of 30 October 2025 settles it by implication: segregation of duties "states that changes must be approved by someone other than the author". Two people co-writing a change produce no such approver and no captured record. Name which DORA when using this: the DevOps programme, not the EU regulation of chapter 01.

### The verdict on the third option

Mostly advocacy. Everyone found with real systems and real numbers kept the pull request and changed who approves it.

### Nobody has measured it

Essentially no data. No vendor publishes review-time, rework, or acceptance-rate effects. CodeRabbit's CLI documentation makes no quantified claim of any kind. Cursor's Bugbot documentation has no effectiveness metrics, only per-review pricing. Gemini Code Assist claims "speeding up reviews" with nothing behind it.

## The option nobody took

Worth reporting as an absence, because it makes the three-way choice honest.

**Dropping the pull request.** The mechanism exists and is well described, but from 2021 and not AI-motivated: Rouan Wilsenach, "Ship/Show/Ask", 8 September 2021, "You make your change on a branch, you open a Pull Request, then you merge it without waiting for anyone". Nobody found has revived it citing AI volume. **MOVES REVIEW LATER.**

**Trunk-based development does not support the claim either.** Its community site puts review before the merge: "the PR should be on a short-lived feature branch and processed very quickly by reviews towards merging back to trunk/main." Committing straight to trunk is framed as a small-team choice with no AI rationale, and it recommends self-verification "optimally with a pair-programming partner".

**Pair programming: no adopters found.** No 2025-2026 account of a team adopting or expanding human pairing because AI made review the bottleneck. The nearest Thoughtworks source argues the opposite and predates the question, Birgitta Böckeler, "Coding assistants do not replace pair programming", 10 August 2023. Notably, the one 2026 memo in that series about human-agent working arrangements does not discuss pull requests or review at all.

**And the counter-evidence is sharp.** "(Im)Paired Programming: Coding Agents Improve Productivity but Harm Understanding", arXiv 2607.26375, 29 July 2026, finds agents "boost task completion but reduce code comprehension". The Extreme Programming argument for pairing instead of review depends on the human understanding what was written, so this turns the proposed remedy into another instance of the ownership failure.

Note also that in the current literature "pair programming" increasingly means two agents rather than a human avoiding review.

**Post-merge measurement is active; post-merge review is not.** Three 2026 papers argue merge success is the wrong endpoint, including Xia and Miller on 182 repositories, one on 1,210 merged agent pull requests, and one on 37,623 pull requests. None proposes that review should move after the merge.

## The counter-pattern: same pressure, kept the gate

This complicates any neat open-source-versus-companies story, and the section should say so.

- **Shopify**, 2 September 2026: "Owners supply product context, accept risk, review, and merge." Its reported gains, an open-issue backlog down about 70 per cent in eleven days and security changes merging at about 80 per cent where about 10 per cent did before, are attributed to preparation and a freshness-gated merge queue rather than to removing the approver.
- **Monzo**, a licensed UK bank, 13 August 2026: "An engineer still reviews and merges, but the bottleneck moves from 'find an engineer with capacity' to 'find a reviewer'."

So large throughput gains are available without touching the approver, which weakens the argument that the approver is the thing standing in the way.

## European fintech evidence

The headline result is an absence. European banks and fintechs have published essentially nothing on reviewing AI-generated code. That is worth reporting to this audience rather than hiding.

**Checked individually and found nothing:** ING, Klarna, Wise, N26, Checkout.com, Starling, SumUp, Mollie, Revolut, bunq, Danske Bank, Nordea, SEB, Swedbank, DNB, Santander, BBVA, Deutsche Bank, Nexi, Worldline, Trustly, Tink, Zettle, Schibsted, Adevinta. Qonto publishes heavily on AI, but about product agents and customer-facing review, not code review.

**Vipps MobilePay has published nothing.** The developer portal is API documentation only. No engineering blog, no AI development post, no AI language in public contribution guidelines. So there is nothing to clear and no confidentiality exposure from this direction.

### Adyen, the only European payment company on the record

Stefano Dalla Palma, Development Tooling Engineer, Adyen tech blog, 22 August 2026. **RETAINED, and it restricts input at the same time.**

> "Every automated change is reviewed and approved by a human before it merges"

Scale and load: "over 4,000 automated MRs across the codebase, with a steady 70% merge rate, a median review turnaround under two hours", spread across "more than 400 unique reviewers".

The input constraint, which is the interesting half: "It produces small MRs touching fewer than five files on average. These are fast to review, easy to approve".

And they named habituation from experience, independently of the study that measured it:

> "After approving a dozen near-identical MRs, reviewers may start to pattern-match rather than scrutinize."

Their countermeasure was temporary: "a designated person walked through approved MRs before merging to double-check the changes".

**Caveat that must travel with this.** These are deterministic OpenRewrite recipes orchestrated by an agent, not model-generated code. The review-capacity shape is the same; the provenance is not. Do not present Adyen as an example of reviewing AI-written code.

### The clearest European accounts are not financial firms

**Zalando**, Germany, e-commerce. Bartosz Ocytko, Executive Principal Engineer, 14 August 2026. **REMOVED for a defined subset.** "33% of our PRs are low-risk and are auto-approved by the bot." A risk classifier runs at pull request creation and scores rollout risk low, medium or high; the author may then merge their own low-risk change, cutting lead time 20 to 40 per cent. Medium and high still require a human. On size: "Teams who found large PRs to be a problem, have reached internal agreements that they will limit PR sizes to a fixed size", with enforcement social rather than mechanical, since "Hard enforcement through pre-commit hooks is less popular."

**Spotify**, Sweden. Tyson Singer, SVP, 16 September 2026. **REDUCED.** The only European source found that segments incident data by AI authorship:

> "we did not identify AI-authored code as a material direct contributor"

> "the volume of change increased faster than some of our verification controls could adapt"

It is watching two signals: "code complexity and PR size are both creeping up". Separately, Niklas Gustavsson, Chief Architect and VP of Engineering, 3 June 2026: "we now have 76% more PRs to review", with the response being "auto-merging what's safe, focusing review where it matters most". Attribution caution: those words are Spotify Engineering's write-up of his talk, not quoted directly as his.

**Booking.com**, Netherlands, 3 July 2025. **RETAINED**, but one engineer's post rather than policy: "You must be the ultimate gatekeeper, reviewing every line before it enters your codebase."

### No European financial institution restricting input, and no regulator statement

Not found for either. A GitHub search for AI-disclosure language in contribution guidelines across nine European fintech organisations returned zero hits. No European regulator or industry body statement beyond DORA and its technical standards was found, though that absence is weaker than the others: the European Banking Authority's search interface is JavaScript-rendered and returned nothing extractable.

**Method limits to carry into the piece.** This pass ran without web search, using direct blog fetches, RSS feeds and the GitHub API. Medium feeds expose only ten recent posts, so older posts from Klarna, Wise or N26 could exist unseen. Conference talks and podcasts were not searchable, which is precisely where European fintech engineers are most likely to have spoken without publishing. So the honest claim is that this sector has published little, not that it has said nothing.

## Confidence and gaps

| Claim | Assessment |
| --- | --- |
| Godot restricted AI contributions and kept human approval | High. Quoted from the announcement. |
| The reviewer shortage predated AI | High. Two independent projects say so in their own words. |
| Rust's circuit breaker is live policy | High, with the caveat that the whole policy is a declared time-boxed experiment. |
| Rust's circuit breaker has been triggered | Unknown. Neither document says. Do not claim either way. |
| Rust bans machine-written contributions | No. They are permitted with disclosure, under conditions. |
| The policy study covers 281 repositories | Wrong. 281 policies, from 2,000 top-starred projects plus 36 named organisations. |
| The policy study independently confirms an earlier one | No. It extends the authors' own earlier study. |
| Pull request limits are on by default | Unverified. Not stated in the source. |
| Any project reversed an input restriction | One found, netbox, two days after adopting it. But it swapped an unenforceable ban for a machine-checkable gate, so it is not evidence that restriction failed. |
| Policy revisions generally loosen over time | No. Across 92 tracked policy files, revisions overwhelmingly tightened; netbox is the lone loosening case. |
| curl's bug bounty ended because of AI submissions | High. The maintainer states the cause and the confirmation rate falling below 5 per cent. |
| Concern about machine-written contributions began in 2026 | No. Gentoo's ban was adopted 14 April 2024. |
| The Godot quotes are exact | Verified directly on 17 September 2026, including the framing line about the shortage being successfully ignored. |
| European financial firms have published on this | Almost nothing found so far, beyond Monzo. |
