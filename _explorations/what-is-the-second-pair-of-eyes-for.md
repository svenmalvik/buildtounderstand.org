---
title: What Is the Second Pair of Eyes For?
date: 2026-09-14
excerpt: Under exploration.
published: false
---

<!--
DRAFT. Prose written in the writing-style voice. Not published.

Built from the research in vce-context/research/pull-request-origins/
(four documents, all dated 14 September 2026). Follows the format of
what-is-the-smallest-ai-platform-that-could-possibly-work.md.

Open items before publishing:
1. The mistake. RESOLVED 17 Sep 2026, confirmed by Sven: he approved a
   change because the tests were green, without reading it. Placed with
   the assurance failure in "Three Failures That Look Like One", because
   the green check stood in for a judgement and the recorded approval
   recorded confidence in the tests rather than a reading of the change.
   The other two candidates (a PR opened from agent output he couldn't
   explain; a review rule people bypassed) are NOT his experience and
   must not be written.
2. The centralized AI review wish at work (chapter 03). RESOLVED 20 Sep
   2026, corrected by Sven: there is no such wish. Nobody at work asked for
   a centralized reviewer. Earlier drafts wrote "people keep asking" and
   "a wish exists", and both were invented. The section now presents the
   managed service as one option the author would reach for first, and says
   plainly that nobody asked for it. Do not reintroduce a claim about
   colleagues wanting this. The conflict-of-interest line stands, because
   he did build the tool such a service would run on.
3. "Most of the cheap controls are available to us and unused" is copied
   from the adoption draft, where it is also unverified. Either check which
   branch protections are switched on across our repositories before
   publishing, or keep the sentence that admits I haven't looked.
4. Prototype 0.1 has not been used by any team. The text says so. Decide
   whether to run it on one repository first so the piece publishes with a
   result instead of a design.
5. The adoption exploration (when-is-adoption-evidence-...) is unpublished.
   This draft leans on its conclusion once, in chapter 03, without linking.
   If that piece publishes first, add the link. If not, the sentence stands
   alone.
6. Two things are called DORA. The parked sources below cite Google's
   DevOps Research and Assessment (verification tax). Chapter 01 now also
   cites the EU Digital Operational Resilience Act. Name which one every
   time. The adoption draft's line "whoever implements a change and whoever
   approves it" should read "the functions that approve and the functions
   that implement", which is what RTS 2024/1774 art. 17(1)(b) says.
7. IKT-forskriften change management was § 9, not § 10 (§ 10 was repealed
   in 2015). Verify the art. 17 wording against EUR-Lex before print; the
   note relies on two secondary reproductions that agree.

Sources kept out of the prose to protect readability. All accessed
14 September 2026; details and caveats in the research folder.
- Fagan 1976, IBM Systems Journal: formal inspections; four roles, moderator
  from an unrelated project. 1976 is a publication landmark, not a start.
- Saltzer & Schroeder 1975: separation of privilege. Concept, not the
  etymology of "four eyes".
- Garzik, BK Kernel Hacking HOWTO, 21 Feb 2002; bk pull request 16 Apr 2003.
- git-request-pull-script, Ryan Anderson, authored 26 Jul 2005, committed
  27 Jul 2005 by Junio C Hamano (ab421d2c).
- Launchpad merge proposals 22 Feb 2008; GitHub PRs 23 Feb 2008 (shipped
  the night before). Parallel activity, not a race.
- GitHub Pull Requests 2.0, 31 Aug 2010: "our take on code review".
  Merge button 2011; protected branches 2015; required reviews 2016;
  CODEOWNERS 2017; draft PRs 2019.
- Bacchelli & Bird 2013 (Microsoft): 17 developers, 570 comments, surveys of
  165 managers and 873 programmers.
- Sadowski et al. 2018 (Google): understandability as the origin; 9m
  reviewed changes in the logs.
- Smith 2014 (Atlassian ordering system): domain knowledge motive.
- Gousios et al. 2014: correct code can still be unwanted.
- GitHub, 18 Jun 2026: ~25m to >90m monthly merged PRs, Jan 2023 to Jun 2026.
  Platform growth, not the AI-attributable fraction.
- He et al., 2 Jul 2026: 802 developers, 196,212 PRs, throughput 2.09x,
  reviewer load roughly doubled. One AI-forward enterprise, non-randomized.
- Duma et al., 4 May 2026 (EASE 2026): 61.38% of 33,596 agent PRs had no
  recorded review; same-repository comparison 30.1% vs 30.8%.
- Zhong et al., 14 Jul 2026: faster decisions, no consistent quality gain.
  Quality measures are process smells, not escaped defects.
- Hora, Robbes & Zacchiroli, 7 Sep 2026: 281 policies; 83.3% permit AI,
  67.3% require substantial human involvement, 48.8% require disclosure.
- Godot Foundation, 30 Jun 2026; Inside Rust, 5 Aug 2026; Rust Forge LLM
  policy (living).
- r/ExperiencedDevs 27 May 2026 (u/Evgenii42, u/vooglie quote).
  r/TechLeader 12 Sep 2026 (40 to 110 weekly PRs, four approvers).
- RovoDev (Atlassian), 3 Jan 2026: cycle time 14.35h vs 20.73h; mandatory
  peer review retained. Cloudflare, 20 Apr 2026: 131,246 review runs,
  explicitly not a replacement for human review. Anthropic, 9 Mar 2026:
  substantive comments 16% to 54%; human approval retained.
- DORA, 10 Mar 2026: the verification tax. DORA, teams empowered to choose
  tools. Spotify, 3 Jun 2026: checks per component type. Atlassian,
  29 Aug 2025: shared CI, team customization. Anjum 2026, Frontiers:
  limited causal evidence on platform engineering.
-->

<article class="exploration-article" markdown="1">

<header class="exploration-hero">
  <h1>What Is the Second Pair of Eyes For?</h1>
</header>

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">01</span>
  <div>
    <h2 id="where-did-the-second-pair-of-eyes-come-from">Where Did the Second Pair of Eyes Come From?</h2>
  </div>
</div>

### The Pull Request Was a Request to Integrate

Most code reviews today happen in a pull request. A developer opens a PR, another developer reads it and approves it, and then the branch is merged. We use the pull request as a review tool, and the approval as the second pair of eyes. But where did the pull request come from? And is it still worth having when the change was written by an AI?

In February 2002, the Linux kernel developer Jeff Garzik wrote a short guide for other developers who wanted their changes in the kernel. A change only became part of the kernel when Linus Torvalds pulled it into his repository. The guide said: publish your changes in a repository on the internet that Linus can pull from, write a summary, and also add a diffstat, which lists the files you changed and how much. These rules existed to save Linus a lot of work.

The word "pull" is what the maintainer does. The contributor pushes the change to a repository they own and then asks the maintainer to pull it. The contributor had no permission to write to the maintainer's repository. So from the beginning, writing a change and accepting it were two seperate acts. It wasn't meant as a control; it was just how the work was split.

Notice what the guide asked of the contributor. Publish the change, write a summary, list the files that changed. The preparation is understanding by reading. So there were two readings, the contributor's first and the maintainer's second. GitHub made this a feature in 2008: Review. Required approvals, and code owners were all added later, between 2010 and 2017. The pull request had worked as a request to integrate for years without any of them. They are rules placed on top of it.

In 2010, GitHub also allowed pull requests between branches of the same repository. That changed the reason for opening one. In the kernel, a developer opened a pull request because they couldn't write to Linus's repository. It was the only way to get a change in. Inside a company, everyone on the team can write to the shared repository. A team opens a pull request anyway, so that someone looks at the change before it goes in. When a team opens a pull request against its own master branch (now most call it the main branch), it doesn't need permission to integrate because it had already the permission.

The pull request never required a second pair of eyes. Linus as the maintainer would live with every change he pulled, so he wanted to decide what came in. In the kernel workflow, every change passed through a second person before it was merged, because only the maintainer (Linus) could pull it. Inside a company, that second person disappears because everyone on the team can merge. The rules that came later bring the second person back. A required approval or a code owner's review says: one more person has to say yes before this change goes in.

But in a company repository, there is no Linus at the keyboard. Someone still lives with every change, and at a payment company that someone is the company itself. It owns the code, but that is not the point. When a change moves money the wrong way or stops a payment going through, the company answers for it, to its customers and to its supervisor. That is not ownership of an asset. It is exposure to an outcome, and it sits nowhere near the merge button.

Linus read the code and carried that exposure himself. Here the two are split: one developer reads the change, and the company carries what follows. The company never reads the change, so what it is exposed to depends entirely on that one developer. A required approval puts that developer there, but it doesn't say what they should do. So what is the second pair of eyes for?

### Why People Wanted Another Person

When asking developers why review exists, the answers are almost always the same: to catch mistakes before they are shiped. Michael Fagan's 1976 paper on formal inspections was built around this, and one of his case studies found that inspection caught 82% of the errors eventually found in a program. Eric Raymond's 1997 line about open source, "given enough eyeballs, all bugs are shallow", says the same in one sentence.

But that is not what a second person mostly does once you look at what they write during a review. At Microsoft, developers ranked finding defects as their top reason for reviewing code. Then researchers read the comments those developers actually wrote. Only 14% pointed at a defect. The largest category, at 29%, was suggestions to improve the code that already worked. The developers said one thing about why they reviewed and did something else once they were reviewing.

At Google, the person credited with introducing code review gave a different reason from the start. Review existed "to force developers to write code that other developers could understand." Catching bugs was welcome, but it was not why the practice began. This changes of course what the second person is checking. A reviewer looking for a bug reads the code once and asks whether it works. A reviewer checking for understanding reads the code the way the next engineer will, months later.

So a review can answer two different questions. Does this code work? And will the next person understand why it's written this way? A one-line configuration fix mostly needs someone to answer whether it works. A change to how payments get calculated needs someone to check that it works, and someone who understands payments to check that it will still make sense later. Both changes go through the same pull request, and get the same single approval.

This is also where the four-eyes principle in banking regulation and the four-eyes principle in software have grown apart. A financial regulator asks whether the function approving a change is independent from the function that requested it. But it does not ask whether the code works or whether anyone will understand it later. Those are exactly the two things developers want from a second pair of eyes. A passing check and a signed-off approval can satisfy the regulator. However, they do not answer whether the code works or whether anyone will understand it.

### The Regulator's Pair of Eyes
<!-- Third root, for a regulated fintech. Two meanings of "four eyes" in
     finance: two directors (CRD art. 13, Vier-Augen-Prinzip) and dual
     control on sensitive manual actions (Basel; Finanstilsynet
     «fire øyne»-kontroll). Neither is code review. Code review inherits
     the second through change management: IKT-forskriften § 9 until
     30 June 2025, then DORA (EU 2022/2554) art. 9(4)(e) and RTS 2024/1774
     art. 17(1)(b): independence of the *functions* that approve from the
     functions that request and implement. Functions, not persons.
     Risk-based. Research: research/20260915-where-did-the-second-pair-of-eyes-come-from/ -->

At Vipps MobilePay, a regulated payment company, there is a third reason for a second pair of eyes: the law requires one.

"Four eyes" in banking means two different things. The first is about who runs the company. European banking law grants a licence only where "at least two persons effectively direct the business". That rule is where the German term Vier-Augen-Prinzip comes from, and the English phrase four eyes is a translation of it. Those two people are accountable for everything the company does, including its software, but they approve no individual change.

The second meaning is about a single sensitive action. One person does it, another checks it, before taking effect. When the Norwegian supervisor fined a savings bank in 2023, one finding was that no four-eyes check existed when an employee manually lowered a customer's money-laundering risk level.

Both rules limit which decisions one person may make alone: running the company, or lowering a customer's risk level. The second person is there because the first one can make a mistake or cheat. However, neither rule ensures that the second person actually understood the work.

Until June 2025 in Norway, the rule said only that a firm must have procedures for handling changes, and must follow them. It never asked for an approver at all. Each firm wrote its own procedure and decided for itself whether a second person was involved. However, since July 2025, payment and e-money institutions follow DORA instead, along with a second regulation that spells out what DORA's requirements mean in practice. Those detailed rules require "the independence of the functions that approve changes and the functions responsible for requesting and implementing those changes.". "The European rulebook it replaced asked for the same six steps, that every change be recorded, tested, assessed, approved, implemented and verified, but never asked the approver to be independent of the implementer.

Two words I want to highlight here are "functions" and "independence", which the law doesn't define. But everywhere else the law talks about a function, it means a part of the organisation: risk management, controls, internal audit. So a function is a role rather than a human being. What independence between two such roles requires, well, it never says. So the rule doesn't say who, or what, does the approving. Basel leaves similar room when it defines dual control, calling it two or more separate "entities (usually persons)" acting in concert. In short, whatever approves has to be separate from whatever implements. Nothing says it must be a person.

Together these rules don't ask the questions a developer would ask, which are whether the code works and whether the next person will understand it. They require every change to be recorded, tested, assessed, approved, implemented and verified in a controlled manner. Again, these rules never ask whether the approver understood a change. The reason they give for wanting independence is objectivity and avoiding conflicts of interest, not finding defects. And where the detailed rules do require "source code reviews", they define them as static and dynamic testing, which is a scanner rather than a person.

How carefully a change is checked can also depend on its risk. The policy has to be "based on a risk assessment approach". A reversible configuration change and a change to how money moves don't have to receive the same scrutiny.

When the European supervisors wrote about the risks of frontier AI models in July 2026, the statement never used the words approval, human, segregation, or four eyes. What it asked for was more automation in development and deployment. Nobody has written that AI may or may not approve a change.

| Four eyes in | What must be separate |
| --- | --- |
| Running a bank | Two persons who direct the business |
| A sensitive action | A second person, for one decision |
| A software change | The function that approves from the one that implements |

So the second pair of eyes came from three places. Fagan wanted defects found early. Linus wanted to choose what went into his own code. The regulator wants an independent function to approve the change, a record of it, and more care when the risk is higher.

Today one pull request does all three jobs.

- The comments are the reading.
- The approval is the gate.
- The pull request is the record.

The problem is the approval. The approver is usually another developer on the same team, with the same manager. It's a second person, but within the same part of the company. In other rules for banks, a function is independent only if its people don't do the work they check, and if they sit outside the team that does it. But those rules are written for risk management and internal audit, whose job is to watch the business. The change rule never says the approver has to be one of those. So the question stays open: is it enough that the approver didn't write this change, or must they sit outside the team that did?

Fagan, Linus, and the regulator all come from a time when changes were scarce. An inspection needed a meeting and a prepared reader. Linus read what he pulled. The regulator wants six steps on every single change. But there was never the question about what happens when the changes start to outnumber the people who can read them.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">02</span>
  <div>
    <h2 id="what-changed-when-writing-became-cheap">What Changed When Writing Became Cheap?</h2>
  </div>
</div>

### Three Failures That Look Like One
<!-- Merged section: the volume and scrutiny evidence, then the taxonomy
     it conceals. Research:
     research/20260916-what-changed-when-writing-became-cheap/
     Volume: Meta RADAR arXiv 2605.30208v2. Pickup and review times:
     LinearB 4 May 2026, 8.1m PRs. Habituation: arXiv 2606.22721,
     400 reviewers, 11,429 reviews, KDD 2026 workshop, three controls.
     Ownership: Sonar 1,149 respondents; do NOT cite 68% or 60% from
     that page, its counters render in JavaScript.
     The mistake is confirmed by Sven and sits with assurance.
     NOTE: this study's 30.1% is unrelated to the 30.1% in the May 2026
     recorded-review paper. Never place them near each other. -->

We create more code than ever before. Meta reports 51% more changes per developer in one year, with agents causing over 80% of that growth. On GitHub, merged PRs went from about 25 million a month in January 2023 to over 90 million by June 2026. A PR written with AI waits more than 16 hours before it gets picked up. A PR written without AI waits about 3 hours.

But once someone picks it up, the AI-written PR reaches a decision in about 194 minutes against 252. Sounds like reviewing got faster. Nobody measured how many of those minutes a reviewer spent reading. And those PRs are a lot bigger, over 400 lines against 157. A bigger PR decided in less time is probably not really read.

Someone measured this directly. Researchers followed 400 reviewers through 11429 reviews of agent-written code over seven months. As each reviewer saw more agent-written code, their approval rate rose from 30.1% to 36.8%, and their inline comments fell by 22%. The changes stayed the same size, the waiting time got longer rather than shorter, and approval of human-written code fell in the same months. Developers approved more because agent-written code had become familiar.

Authors are no more careful with their own work. Sonar asked 1149 developers. 96% said they don't fully trust that AI output is correct. But only 48% said they always verify it before committing. So people doubt their code but submit it anyway.

Google reviewed code so the next developer could understand it. Now half of them don't check their own.

Meta now scores each PR for risk and merges the low-risk ones automatically. No human approves them. That is how more than 331000 PRs reached production. A company like Meta wouldn't have built this if it wasn't a major issue for them.

There seem to be three problems:

- More code arrives than people can read.
- Developers submit code they don't understand themselves.
- An approval gets recorded with no real check.

A pull request does three jobs: the comments are the reading, the approval is the gate, and the pull request is the record. The first failure overwhelms the reading, because more arrives than anyone can read. The third breaks the record, which now says a change was approved when nobody read it.

The second failure is different. An agent writes 400 lines, the author skims them and opens the pull request, and the understanding that used to come with writing the change never happens because of AI. The tests still show a green check, the approval still shows a name, the record still shows who approved. However, nothing on a pull request shows whether anyone understood the change. Nobody ever built a check for that, because the first reading used to come with the work. That is the check I try to build at the end of this article: the author's half of four eyes.

### The Numbers Stopped Adding Up
<!-- The honest version: nobody has measured minutes per review, so the
     arithmetic rests on a stated assumption, not a constant. Say so.
     Only effort figure available is ~6.4 h/week self-reported (Bosu &
     Carver 2013, 287 responses). The Microsoft 2015 paper's "six hours
     a week" cites that same OSS survey, so do NOT call it Microsoft
     telemetry. Bacchelli & Bird has no per-review figure.
     The 200-400 lines / 60-90 minutes limits are vendor guidance, not
     research. Usable substitute with real telemetry (Czerwonka 2015):
     useful feedback declines with more files, noticeable past 20.
     Outcome evidence now exists, both ways. Xia & Miller
     (arXiv 2607.09902v1, 10 Jul 2026, 182 repos): each 10pp increase in
     a project's no-review rate is associated with ~6% more agentic
     maintenance burden. Association, not causation. Counter-finding at
     Google scale (arXiv 2608.06640v1, 3.52m changes): AI code reverted
     LESS, ~0.9x, while build failures ran ~1.3x. Carry both. -->

In 2009, Kemerer and Paulk measured what happens to a reviewer as they review faster. Up to 200 lines an hour, people found most of the defects. Faster than that, they found about half.

Here is the thing. One in four PRs written with AI has over 400 lines. At 200 lines an hour, that is 2 hours of one person's attention for one single change.

Almost nobody has two spare hours for a single PR. Before AI, developers spent about 3.2 hours a week reviewing at Google, and about 6.4 in open source. So one to three changes a week, against the 51% more changes per developer that Meta now reports.

I should be careful with that number. Nobody publishes how many minutes a reviewer actually spends on a change, so 200 lines an hour is an assumption from a 2009 study.

The point is that nobody can review everything properly anymore. Most teams have therefore already stopped reviewing some changes. The important question now is whether developers chose consciously what they stopped reviewing.

### Restrict, Relax, or Move It Earlier
<!-- The contrast, not just the maintainers. Open source regulated the
     input and kept human approval: Godot 30 Jun 2026 (restricted AI
     contributions, reviewer shortage predated AI), Rust Forge (circuit
     breaker at half of merges in six weeks), GitHub per-contributor PR
     limits Jun 2026. Companies relaxed the gate instead: r/TechLeader
     12 Sep 2026 (two reviews to one, none for some PRs). Shopify
     2 Sep 2026 got throughput from preparation and a freshness-gated
     merge queue while keeping the approver, backlog down ~70% in 11
     days, security merges ~10% to 80%. Monzo 13 Aug 2026 kept the
     approver: "An engineer still reviews and merges, but the bottleneck
     moves from 'find an engineer with capacity' to 'find a reviewer'."
     Adyen verified 20 Sep 2026 at
     adyen.com/knowledge-hub/how-we-automated-code-modernization-with-openrewrite,
     published 20 Aug 2026, "Stefano Dalla Palma - Development Tooling
     Engineer, Adyen". All quotes verbatim. Caveat that must travel: these
     are deterministic OpenRewrite recipes, and the post calls it "a
     deterministic bot". Adyen is NOT an account of reviewing
     model-written code. The review-capacity shape is the same; the
     provenance is not. Say so if this paragraph grows. Note also that this
     makes the pattern-matching quote an a fortiori argument: the diffs were
     mechanical, under five files, and 100% human-approved, and reviewers
     still went slack. It cannot be used to suggest that an LLM reviewer's
     output would get more scrutiny than this did. The meta-review layer was
     temporary, not standing: "Once we were confident in the recipe's
     behavior, we relaxed that layer." The 4000 MRs, 70% merge rate, <2h
     median and 400+ reviewers are all first-two-months figures.
     Research: research/20260916-what-changed-when-writing-became-cheap/ -->

The Godot Foundation said this in June 2026: "This reviewer shortage was already a problem, but it was one that we ignored." Homebrew's maintainer said something similar. They had this problem for a while already. AI only accelerated it. So having too many PRs to review is an old problem that just became more urgent.

There are four main options to address this:

1. Have fewer PRs.
1. Approve some PRs without a human.
1. Check PRs yourself before you open them.
1. Make each PR simpler to approve.

Here are a few examples for each option:

**1. Have fewer PRs.** This is mostly open source.

- The Godot Foundation banned AI-generated code and kept the human: "All PRs must be reviewed and approved by a human before merging."
- Five teams inside the Rust project limited how much of their code Ai may write. If Ai write more than half the merged changes in six weeks, Ai changes stop being merged for at least ten days.
- GitHub shipped a project setting that limits how many PRs one person can have open.
- curl removed the payment. About 20% of its security submissions were slop, fewer than one in twenty reports was a real vulnerability. It endet its Bug Bounty programm in January 2026.

**2. Approve some PRs without a human.** This is what many companies do.

- Meta scores each change for risk and merges the low-risk ones automatically without any human in the loop.
- Zalando also runs a classifier similar to Meta when the PR opens. "33% of our PRs are low-risk and are auto-approved by the bot." The author then merges their own change. Medium and high risk PRs still need a human.
- Spotify had 76% more PRs to review and started auto-merging the ones it judged safe.

None of these three is a regulated financial company. The European rules want an approving function that is independent of the function implementing the change, and they never say that function has to be a person. A classifier that approves low-risk changes might satisfy the rule on paper. Whether it does depends on whether a classifier counts as a function, who owns it, and whether its decision lands somewhere an auditor can read. I haven't found anyone who has written that down.

**3. Check PRs yourself before you open them.** Ai harnesses like Claude Code have this already.

The same reviewer that comments on your PR will also run on your branch before you open one. Anthropic ships one review skill as well as Codex and Cursor. Anthropic's own team told the agent to run a security review "as a final step before opening a PR". Some customers put that into a hook so it can't be skipped. Human review is still important, but only for "regulated or truly critical code".

Rust's policy says an LLM review **does not substitute for self-review**. Running a machine over your own branch is not the same as having understood the code.

**4. Make each PR simpler to approve.**

- Shopify cleared about 70% of its security backlog in 11 days. Their system writes the fix, explains why it is needed, and keeps it ready to merge by a human developer.
- Adyen runs more than 4000 automated merge requests and keeps a human approving. Each change touches fewer than five files on average, which makes it "fast to review, easy to approve".

Adyen also wrote this: "After approving a dozen near-identical MRs, reviewers may start to pattern-match rather than scrutinize." Their answer was a designated person walking through approved changes before they merged.

Adyen is the only regulated payment company in these four options, and the only one that treated the empty approval as something to fix rather than a cost to accept. The designated person is a third pair of eyes, added because the second pair had stopped reading.

### The Approval Became a Setting
<!-- New section. On 1 September 2026 GitHub shipped machine approval
     that satisfies the rule: "Copilot can submit an approval that counts
     toward the repository's required-approvals rule." Two toggles,
     enterprise default disabled, public preview. Verified directly
     against the changelog and docs on 16 Sep 2026.
     Ties to chapter 01: the regulation says functions, not persons, and
     no rule found requires a human approver. The precedent already
     existed in dependency auto-merge, where the substitute control is
     the test suite. Nobody found using the toggles yet; adoption
     unverified, so do not claim it. -->

On 1 September 2026, GitHub added a new setting that let Copilot also approve PRs. I wondered about that. The rule is that authors cannot approve their own PRs. But the rule works on identities, and Copilot has two. One that writes code and one that reviews code. The identity for writing is blocked while the reviewing one is free to approve.

It goes further. If I ask Copilot to make a change, GitHub will not let me approve it. It knows I am too close to it. However, Copilot's reviewing identity has no such limit.

GitHub's own documentation says that the agent "gets a second opinion on its code with Copilot code review", which is a second opinion from itself, on its own work.

Nothing in the documentation mentions segregation of duties, conflicts of interest, or independence. There is one line saying human review should be added on top. But that is an advice, not a control.

For a European finance regulated company, this part is worrying. You can see the approval on the PR, under Copilot's name. But the audit log has no event for it. To find out what Copilot approved last quarter, you would have to walk through every PR and collect it yourself.

So the approval is a setting now. Someone has to decide which repositories have it switched on, which changes are exempt from it, and who answers when an AI-approved change causes harm. On most teams nobody has been given that job. That is what I want to work out next.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">03</span>
  <div>
    <h2 id="who-should-own-the-check">Who Should Own the Check?</h2>
  </div>
</div>

### What a Managed Review Service Would Do for You
<!-- Chapter 03, section 1 of 4. Research:
     research/20260920-who-should-own-the-check/ (six notes:
     what-a-shared-reviewer-protects, cost-of-a-shared-ai-reviewer,
     external-approval-and-independence, googles-shared-reviewer,
     central-review-reversals, ownership-and-exit).
     PARAPHRASE WARNING, added when chapter 03 was rewritten for a
     non-native reader at roughly grade 6. Most of the long academic
     quotations were turned into plain paraphrase, because the quoted
     wording was what held the reading level up. The exact wording of
     every one of them is in the research notes listed above. Before
     publishing, check each paraphrased claim back against the note, and
     restore the quotation wherever the paraphrase drifts. Still verbatim
     in this chapter: 'a heavyweight process', 'an archaic hazing
     process', the Greptile seat definition, and 'which is deliberately
     low'. Everything else is my wording, not the source's.
     Large counts are also rounded in the prose for readability: 20995
     review comments reads as 'almost 21,000', 382771 pull requests as
     'nearly 400,000', and Cloudflare's 131246 / 48095 / 5169 as 'more
     than 131,000' / '48,000' / 'over 5,000'. Percentages, prices and the
     small counts stay exact. Exact figures are in the research notes.
     Cautions:
     - BSIMM16, published Jan 2026, 111 firms and 223700 developers. Median
       1.8 security-group members per 100 developers; 1.13 at firms with
       650+ developers. Top-quintile firms 2.7, bottom-quintile 6.8;
       champions 12.3 vs 4.6 per 100 developers. BSIMM's authors state they
       cannot separate cause from effect, and the text says so. The widely
       repeated "1 AppSec engineer per 100 developers" has no traceable
       source; use BSIMM or nothing.
     - BSIMM's score counts observed activities out of ~125. It is not a
       measure of defects caught or breaches avoided. Do not let the text
       imply it is.
     - The 30-reviewer / 7-vulnerability study is Edmundson et al., ESSoS
       2013. Best reviewer found five, 20% found none, mean 2.33, and years
       of security experience showed no significant correlation. Freelance
       reviewers, one small PHP application, 2013, so transferability is
       medium at best. It is kept in deliberately because it weakens this
       section's own expertise argument. Do not remove it to tidy the case.
     - The coverage result is Thompson & Wagner, PROMISE 2017, peer
       reviewed, 3126 GitHub projects and 382771 pull requests. The authors
       call the effect sizes "small but significant" and the data is open
       source only. It is the strongest positive case for a managed reviewer
       in this chapter and it is a coverage claim, never a quality claim.
     - The missing comparative study is stated in the text as a finding.
       Nobody has compared what a central security function finds against
       what the implementing team finds on the same changes. If someone
       later finds that study, this paragraph has to change.
     - Refused sources, recorded so nobody picks them up: an uncited SEO
       claim that champions catch "3x more logic-level security bugs" than
       centralized review; the ProjectDiscovery State of AppSec 2026 blog
       (all figures gated); and the Netflix "paved road is not mandatory"
       phrasing, which returned 403 on every route to a primary source and
       does not appear in the 2018 TechBlog post that is usually cited.
     - DORA in this chapter is Google's DevOps Research and Assessment,
       not the EU Digital Operational Resilience Act of chapter 01.
     - Google readability: the internal velocity claim compares people who
       finished the programme with people who have not, with no effect size
       and no sample size published. Used here only for the costs and the
       criticism, which are Google's own words.
     - The habituation study (arXiv 2606.22721) measures repetition and
       load, not team boundaries. It must never carry a same-team claim.
     - GitHub audit-log finding read from src/audit-logs/data/fpt/ and
       ghec/organization.json in github/docs on 20 Sep 2026. The rendered
       docs page truncates; the data files are the primary source.
     - The two-identities argument in the opening is built from chapter 02
       (GitHub ships one Copilot identity that writes and one that reviews;
       only the writing one is blocked from approving) plus the Greptile
       model-inversion study later in this chapter. The bridge claim, that
       the two identities may run the same model, is NOT verified. GitHub
       does not document which model backs each identity, and Copilot lets
       a customer pick models, so it may differ per install. The text says
       "GitHub does not say ... and from the outside there is no way to
       check", which is the most that can be supported. Never assert that
       they are the same model.
     - The opening leans on chapter 01 for the EU wording, so the two must
       stay consistent. The claim that no regulator statement and no
       incident report exists about an automated approver comes from
       what-a-shared-reviewer-protects.md, which records it as "absence of
       a search engine, not absence of the thing". The text says "I went
       looking ... and I found neither", which is all I can support. Do not
       upgrade it to "none exists".
     - Cut on request: the line saying no study settles the central-versus-
       team question. The gap itself is real and worth keeping somewhere,
       because nobody has compared what a central security team finds with
       what the product team finds on the same changes. It is no longer
       stated anywhere in the prose. Consider it for "What I Don't Know
       Yet" at the end of the piece.
     - Do not name a target level for unreviewed pull requests. The
       finding (Thompson & Wagner, PROMISE 2017) is proportional: halving
       the number of unreviewed pull requests predicts about 6% fewer
       security bugs, from whatever level you start at. Writing "get it
       down to one in ten" makes the claim false for a project already
       there, and for one at one in two. It is also an association across
       3126 projects, not a measured intervention, so keep "you would
       expect" and never say the change causes the drop.
     - The security claim is security-only in the evidence. Braz &
       Bacchelli (182 practitioners) and Yu et al. (614 of 20995 comments)
       both measure security and nothing else. The licence and dependency
       thread and the cross-cutting-architecture thread were never
       evidenced: what-a-shared-reviewer-protects.md records "No evidence
       gathered" for the first, and only a position paper for the second.
       The text therefore states the generalisation as a guess and says so.
       Do not turn it into a claim, and do not widen the bold line back to
       "certain things" to cover it.
     - Vocabulary rule, now that two kinds of team are named: never write
       "the team" unqualified in this chapter. It is either the product
       team (the one that wrote the change) or the central team (devex).
       An unqualified "team" sends the reader back to work out which.
     - Org shape, given by Sven on 20 Sep 2026 and new to this draft: one
       developer experience team and twenty to thirty product teams. The
       piece already names Vipps MobilePay in chapter 01, so this adds team
       structure to what is public. Include it in the manager clearance the
       strategy note asks for, alongside the internal system already named.
       Do not invent what the devex team owns beyond this.
     - There is no wish at work. Corrected by Sven on 20 Sep 2026: nobody
       asked for a centralized reviewer, and earlier drafts that said
       "people keep asking" invented it. The managed service is presented
       as the author's own first instinct, and the text says nobody asked
       for it. The only first-hand claim left in this section is that he
       built the tool such a service would run on. -->

Chapter 02 ended with a setting. Copilot can now approve a pull request, and somebody has to decide which repositories have that switched on.

At a payment company that is not only our decision. The European rules say an approval has to come from a function that is independent of the function doing the work, and chapter 01 showed they never say that function has to be a person. So on paper a setting could satisfy the rule.

Look closer though. Chapter 02 showed that Copilot has two identities, one that writes code and one that reviews it, and only the writing one is blocked from approving. GitHub does not say whether the two run the same model, and from the outside there is no way to check. If they do, then the rule is being met by a name rather than by a difference. There is a measurement later in this chapter that makes the doubt concrete: a model is reliably worse at finding bugs in code from its own family than in anyone else's. Independence that disappears when you measure it is not independence.

Chapter 01 left the same question in an older form. Is it enough that the approver did not write the change, or do they have to sit outside the team that did?

One possible answer is to give the job to our developer experience team. They would build an AI reviewer and make it to the product teams. It would look like the other things a developer experience team runs, where one group owns it and everyone else uses it. It is the option I would reach for first.

The attraction is easy to see. The work happens once, and every team gets the result. But only if the service does something a product team cannot already do for itself. Three claims are usually made, and two fall apart.

**An outsider sees more.** The research says the opposite. Microsoft asked 873 developers, and nine out of ten said a change takes longer to review when they do not know the files. The less reviewers know the code, the more bugs survive to production.

**A machine never gets tired.** But the people reading what it writes do, and one reviewer in front of every change piles that reading into one place. Every study says load makes a check worse. The study in chapter 02 asks for the opposite: spread reviews around.

**Nobody in the product team is looking for security.** True. Of almost 21000 review comments in two open source projects, only 614 touched security. But asked directly, the same developers said they always think about it. They knew how to do it. Nobody had asked them to.

The useful claim is not that a managed reviewer reads better. It is that it reads everything. That is exactly what chapter 02 said a busy team can no longer do, because more changes now arrive than anyone has time to read.

The second thing a product team cannot give itself is a record. GitHub keeps an audit log of what happens in your repositories, and when somebody reviews a pull request it notes that a review was submitted. It does not note whether that review approved the change or rejected it. There is no approval event at all, the decision survives only in the repository, and the log reaches back 180 days. For secret scanning GitHub does record the approval, the refusal, and the reason the person typed. So a central owner can show months later who allowed what and why, and a product team cannot.

Chapter 01 said a pull request does three jobs at once. The comments are the reading, the approval is the gate, and the pull request is the record. A managed service is better at two of them. It reads everything, and it keeps a record worth showing an auditor. The one job it has no advantage in is the gate.

### What a Managed Review Service Would Cost
<!-- Chapter 03, section 2 of 4. Same research folder as the previous
     section.
     PARAPHRASE WARNING, added when chapter 03 was rewritten for a
     non-native reader at roughly grade 6. Most of the long academic
     quotations were turned into plain paraphrase, because the quoted
     wording was what held the reading level up. The exact wording of
     every one of them is in the research notes listed above. Before
     publishing, check each paraphrased claim back against the note, and
     restore the quotation wherever the paraphrase drifts. Still verbatim
     in this chapter: 'a heavyweight process', 'an archaic hazing
     process', the Greptile seat definition, and 'which is deliberately
     low'. Everything else is my wording, not the source's.
     Large counts are also rounded in the prose for readability: 20995
     review comments reads as 'almost 21,000', 382771 pull requests as
     'nearly 400,000', and Cloudflare's 131246 / 48095 / 5169 as 'more
     than 131,000' / '48,000' / 'over 5,000'. Percentages, prices and the
     small counts stay exact. Exact figures are in the research notes.
     Cautions:
     - Tricorder vintages: the 10% admission bar and the probation/25%
       disable policy are ICSE 2015 (2014 data); "just below 5%" overall is
       SWE at Google ch. 20 (2020). Keep them straight.
     - Greptile's model-inversion study (21 Jul 2026, 2 x 500 PRs) is vendor
       research selling the feature. Directional only. Same for the 43%
       acceptance figure.
     - The triage arithmetic is mine and is labelled as mine in the text.
       Do not present it as a measurement.
     - The 4335-PR study is Cihan et al., arXiv 2412.18531, ICSE 2025 SEIP.
       An earlier brief attributed it to "Bosu et al. 2025", which does not
       exist. Do not reintroduce that citation.
     - FCA multi-firm review, 5 Feb 2021: lead with the 90% approval rate.
       The 3.8% vs 1.6% failure rate is context, not proof, because major
       changes are selected into CAB review for being risky.
     - DORA here is Google's DevOps Research and Assessment.
     - The refinement-attack figure (32 of 33) is arXiv 2603.18740v3,
       Mar 2026, 33 CVEs across 20 projects against Claude Code and
       CodeRabbit pipelines. Preprint, not peer-reviewed. Keep the
       mechanism (attacker iterates against a local clone, defender gets
       one attempt); it is the part that does not depend on the number.
     - Cloudflare figures are first-party, 20 Apr 2026: 131246 review runs,
       48095 merge requests, 5169 repositories, 30 days, median 3m39s,
       ~1.2 findings per review, break-glass used 288 times (0.6%). Self-
       reported, no baseline. Kept because it is the fair counter to this
       section's freedom argument and should not be dropped.
     - Exit was reframed on 20 Sep 2026 and the draft was wrong twice
       before landing here. These tools post findings as native pull
       request comments, which GitHub's REST API exports independently of
       any vendor, so the reading is portable. The lock-in is the learned
       context. CodeRabbit (docs.coderabbit.ai/knowledge-base/learnings) is
       the only one of six with a documented learnings export, and it
       imports CodeRabbit-to-CodeRabbit only. Greptile, Graphite and Qodo
       have no export page; Bugbot exposes counts, not comment text.
     - Verified again on 20 Sep 2026 with web search working: no first-party
       account exists of any organisation switching AI code review vendors,
       turning one off, or being blocked from opting out. The category is
       young. Never let the draft imply such an account exists.
     - Exporting the review comments: six vendors checked, six no's. None
       documents an export of the comment text. It does not matter, because
       the comments are native pull request comments in the customer's own
       forge. Keep the argument on the tuning, not the record.
     - Unused, kept for a later section: Greptile markets itself as "the
       independent code validator", where independence means independence
       from coding agents and model providers, not the customer's
       independence from Greptile.
     - Cloudflare reports no false-negative rate and no cost, and does not
       separate the two readings of 0.6%. The text says so. Do not let the
       number stand as evidence the reviewer is accurate.
     - GitHub ruleset behaviour verified 20 Sep 2026: rules aggregate, most
       restrictive wins, and no repository-level opt-out from an org or
       enterprise ruleset is documented. Repos can decide whether Copilot's
       approval counts, not whether the review runs. Cursor Bugbot's
       per-engineer "only when mentioned" setting is the counterexample.
     - Gap, still open: no documented case found of an organisation building
       a central code review, AppSec or architecture review function and
       then dismantling it. Postman narrowing a gate (Apr 2026, 25% of
       releases auto-unblocked, ~2 business days off per-review closure,
       self-reported with no denominator) is the nearest verified thing.
       Do not write a reversal that isn't sourced. The search surface here
       is thin rather than exhausted: the obvious companies were never
       tried because the session ran out of web search, and UK GDS service
       assessment devolution is an untested lead. Worth one more pass. -->

Google has run a service like this for most of its life, and it publishes what the service costs.

Google calls its version readability. Every change has to be written or reviewed by an engineer certified in that language, and the certificates come from a central pool of about one to two percent of Google's engineers. Google calls it "a heavyweight process", made compulsory by its own tooling. The first cost on its own list is the friction for a team with nobody certified, because that team has to go outside itself to get anything reviewed. Then come extra rounds of review, and a programme that can only grow by hiring more reviewers. Google even publishes the complaint its engineers make. Some call readability "an archaic hazing process", an old ritual that lost its purpose years ago. Google ran a study and promised in advance to kill the programme if the costs won. It survived. But it is worth noticing why anyone asked. Formatters and scanners had got good enough that nobody was sure the human reviewers were still earning their keep.

Moving approval outside the team that writes the code has been tried more widely. In 2019 DORA studied companies that required approval from an outside body, and found them 2.6 times more likely to end up in the worst performing group, with no sign that the approval prevented failures. The UK financial regulator read more than a million production changes across 23 firms, and looked closely at change advisory boards, the committees that meet to approve releases. Those boards approved more than nine out of ten of the big changes they saw, and some firms had not turned down a single change all year. So the problem was never that a second reviewer existed. The problem was a second reviewer who approved everything, which is what a check turns into when it sits far from the work and has to look at all of it. That is chapter 02's empty approval, arriving from a different direction.

The money is the easy part. Published prices run from about $12 to $72 per developer per month, so a thousand developers cost a few hundred thousand dollars a year. An extra review costs between fifty cents and about $1.70. Notice what no price list charges you for: a review that turns out to be wrong.

The reading is the real cost, and it never appears on an invoice. The largest independent study read more than 31,000 AI review comments across 239 repositories and checked what developers did with each one. They acted on 36% and rejected 56%. The biggest vendor reports much the same from its own side, with 43% accepted. So between half and three fifths of what the service says has to be read by a person and thrown away.

Google has a rule for this. Its code scanning platform, Tricorder, only lets a new check in if developers act on more than nine findings out of ten, and across the platform the rate of ignored findings sits just under 5%. Above 10% a check goes on probation, and above 25% Google can switch it off the same day. A managed AI reviewer today runs at 56%.

Put rough numbers on it. Twenty thousand reviews a month with three comments each is sixty thousand comments, of which about thirty-four thousand get rejected. At two minutes each that is more than a thousand engineer hours in a month, against a licence that might cost thirty thousand dollars. The reading costs more than the tool, and it lands somewhere else. The licence comes out of the owner's budget, and the reading comes out of every product team. So does the waiting. After one company switched a reviewer on, the time to close a pull request rose from just under six hours to more than eight. Chapter 02 called this the first failure, where more arrives than anyone can read. A managed reviewer does not remove it. It moves it, and adds to it.

There is a quieter cost as well. Rigby and Bird found that people who review code end up familiar with 66% to 150% more of the files in their project. Chapter 01 said Google started reviewing so that other developers would understand the code. A managed reviewer reads the change and keeps that understanding to itself, which is chapter 02's second failure seen from the other side.

Then the blind spot. Greptile had Claude and Codex review 500 pull requests written by each, and both models did worse on code from their own family. Claude caught 62% of the serious bugs in Codex's code but only 53.7% in Claude's. GPT caught 60% in Claude's code but only 50.5% in Codex's. Greptile sells the feature, so I treat this as a direction rather than a measurement, and the direction is enough. One reviewer for the whole company is one blind spot for the whole company, lined up with whatever model everyone writes with. It is also one thing for an attacker to learn. Researchers rewrote the pull requests around 33 known security holes until the reviewer waved them through, and thirty-two got past both Claude Code and CodeRabbit. An attacker can practise against a copy of the pipeline, and the defender gets one attempt.

Leaving is harder than it looks. Greptile counts a seat as "any developer who has gotten a review done by Greptile in that billing period", so once the reviewer runs everywhere every developer counts, and nobody can shrink the bill by using it less. The comments themselves are safe, which I had wrong at first, because these tools post findings as ordinary pull request comments that live in your own repository. What you cannot take with you is the tuning. Of six vendors, only CodeRabbit documents an export, and it only loads into another CodeRabbit account.

The last cost is about who gets to say no. On GitHub a single rule turns Copilot review on for every repository in the company, and once it is set at the top an organisation below can see the policy but not change it. A repository may decide whether Copilot's approval counts toward the number it needs. It may not decide whether the review happens. Cursor built the opposite, letting an engineer ask for review only when they want it, and Qodo lets anyone who can edit the configuration leave files or branches out. Three vendors, three answers to whether the person being checked may decline.

Cloudflare shows the way out can be designed in. Its reviewer runs across the whole company, and in one month it completed more than 131,000 review runs across 48,000 merge requests in over 5,000 repositories. It blocks merges. Each team shapes it with a file in its own repository, and when a team has to get past it there is an emergency override that Cloudflare calls break glass. Engineers used it on 0.6% of merge requests, and every use leaves a record. That number reads two ways though, and Cloudflare does not say which. Either the reviewer is almost always right, or nobody wants to be the engineer who broke the glass. Cloudflare also reports about 1.2 findings per review and calls that "deliberately low", which is less than half of what my rough numbers assumed. The cost of all that reading is a design choice as much as anything else.

So the cost list is long, and against it stand only the reading and the record. Everything else a second pair of eyes was ever for, finding the bug, understanding the change, leaving the product team knowing more than it did before, gets weaker the further the reader sits from the code.

Google's own complaints may hold the answer. A great deal of what its reviewers wrote about were things a program could have found on its own. Which is the next question. How much of what we call review needs a person at all?

### Most Checks Don't Need Judgment

### Centralize the Machinery, Not the Decision

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">04</span>
  <div>
    <h2 id="what-would-i-try-first">What Would I Try First?</h2>
  </div>
</div>

### What I Would Try Before Building a Review Service

<div class="prototype" markdown="1">
<p class="prototype__label">Prototype 0.1 · the author's half of four eyes</p>

<p class="prototype__caption"></p>
</div>

### What It Would Cost, and How to Leave It

## Conclusion

### What I Don't Know Yet

---

You can write to me at [sven@malvik.de](mailto:sven@malvik.de) or find me on [LinkedIn](https://www.linkedin.com/in/svenmalvik/).
</article>