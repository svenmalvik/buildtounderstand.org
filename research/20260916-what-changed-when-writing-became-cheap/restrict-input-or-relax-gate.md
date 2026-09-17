# Restrict the input, or relax the gate

**Question this document answers:** When review capacity ran out, what did projects and companies actually do about it?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 02, "Restrict the Input, or Relax the Gate"

**Last updated:** 2026-09-17

Scope: published responses only, verified at source. The European fintech evidence is tracked separately below because the author works at a Norwegian payment company and that audience is the one the piece is written for.

## Main findings

**Two opposite responses exist, and the split is not open source against companies.** Open-source projects restricted what may be submitted while keeping human approval. Meta relaxed the gate and merges low-risk changes automatically. But Shopify and Monzo faced the same pressure and kept the approver, finding their throughput elsewhere.

**The most important finding is that the shortage predated AI.** Two maintainers say so independently, in their own words. AI did not create the capacity problem. It removed the option of ignoring it.

**Nobody restricting input has reported reversing it.** That absence is weak evidence, since the policies are recent.

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

## The counter-pattern: same pressure, kept the gate

This complicates any neat open-source-versus-companies story, and the section should say so.

- **Shopify**, 2 September 2026: "Owners supply product context, accept risk, review, and merge." Its reported gains, an open-issue backlog down about 70 per cent in eleven days and security changes merging at about 80 per cent where about 10 per cent did before, are attributed to preparation and a freshness-gated merge queue rather than to removing the approver.
- **Monzo**, a licensed UK bank, 13 August 2026: "An engineer still reviews and merges, but the bottleneck moves from 'find an engineer with capacity' to 'find a reviewer'."

So large throughput gains are available without touching the approver, which weakens the argument that the approver is the thing standing in the way.

## European fintech evidence

Tracked separately, because the piece is written for engineering leaders in regulated European companies and that is where the evidence is thinnest. An earlier direct-fetch pass found nothing published by DNB, Nordea, Klarna, Revolut or Wise. Monzo is the only European financial institution found with a published position, and it retained the approver.

A dedicated search is in progress. If it confirms the gap, the section should say plainly that European financial firms have published almost nothing, which is itself worth reporting to that audience.

**Note on the author's employer.** Anything found about Vipps MobilePay is to be reported separately and cleared by the author before use, per the confidentiality constraint in his strategy document.

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
