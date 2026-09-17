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
1. The mistake. CLAUDE.md asks for a mistake from the same domain, placed
   where it carries the argument. Chapter 02 has a marked slot for it. The
   record doesn't establish one about review, so nothing is written there.
   Candidates to confirm or reject: a change I approved without reading
   because the tests were green; a PR I opened from agent output I couldn't
   explain; a review rule I introduced that people bypassed. If none is
   true, the section stands on the Rust and Reddit evidence and says so.
2. The centralized AI review wish at work (chapter 03). Written to the same
   limit as the adoption draft: a wish exists, ownership is unclear, the
   decision isn't mine, I built the tool someone would centralize with.
   Confirm what may be said publicly.
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

Most code reviews today happen inside a pull request. Someone opens a change, someone else reads it and approves it, and then the branch is merged. The pull request has become the review tool, and the approval has become the second pair of eyes. But where did the pull request come from? And is it still worth having when the change was written by an AI?

In February 2002, the Linux kernel developer Jeff Garzik wrote a short guide for other developers who wanted their changes in the kernel. A change only became part of the kernel when Linus Torvalds pulled it into his repository. The guide said: publish your changes in a repository on the internet that Linus can pull from, write a summary, and also add a diffstat, which lists the files you changed and how much. These rules existed to save Linus work.

The word "pull" describes what the maintainer does. The contributor pushes the change to a repository they own and then asks the maintainer to pull it. The contributor had no permission to write to the maintainer's repository. So from the beginning, writing a change and accepting it were two acts, done by two different people. It wasn't meant as a control; it was just how the work was split.

GitHub made this a feature in 2008. Review, required approvals, and code owners were all added later, between 2010 and 2017. The pull request had worked as a request to integrate for years without any of them. They are rules placed on top of it.

In 2010, GitHub also allowed pull requests between branches of the same repository. That changed the reason for opening one. In the kernel, a developer opened a pull request because they couldn't write to Linus's repository. It was the only way to get a change in. Inside a company, everyone on the team can write to the shared repository. A team opens a pull request anyway, so that someone looks at the change before it goes in. When a team opens a pull request against its own master branch (now most call it the main branch), it doesn't need permission to integrate because it had already that permission.

The pull request never required a second pair of eyes. Linus as the maintainer would live with every change he pulled, so he wanted to decide what came in. In the kernel workflow, every change passed through a second person before it went in, because only the maintainer (Linus) could pull it. Inside a company, that second person disappears because everyone on the team can merge. The rules that came later bring the second person back. A required approval or a code owner's review says: one more person has to say yes before this change goes in. But in a company repository, there is no Linus. Nobody owns the code the way he owned the kernel. So whether these rules work depends on something else: why people wanted another person to look at their change in the first place.

### Why People Wanted Another Person

When asking developers why review exists, the answers are almost always the same: to catch mistakes before they are shiped. Michael Fagan's 1976 paper on formal inspections was built around this, and one of his case studies found that inspection caught 82% of the errors eventually found in a program. Eric Raymond's 1997 line about open source, "given enough eyeballs, all bugs are shallow", says the same in one sentence.

But that is not what a second person mostly does once you look at what they write during a review. At Microsoft, developers ranked finding defects as their top reason for reviewing code. When researchers then read the comments those same developers actually left, only 14% were about a defect. The largest category, at 29%, was suggestions to improve the code that already worked. The developers said one thing about why they reviewed and did something else once they were reviewing.

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

The second borrows the same phrase for something else: a control on single sensitive actions. When the Norwegian supervisor fined a savings bank in 2023, one finding was that no four-eyes check existed when an employee manually lowered a customer's money-laundering risk level.

Both rules limit which decisions one person may make alone: running the company, or lowering a customer's risk level. The second person is there because the first one can make a mistake or cheat. However, neither rule ensures that the second person actually understood the work.

Until June 2025 in Norway, a system could not go live before the responsible one had approved it. The rule never said who that was, and each firm decided for itself. However, since July 2025, payment and e-money institutions follow DORA instead, along with a second regulation that spells out what DORA's requirements mean in practice. Those detailed rules require "the independence of the functions that approve changes and the functions responsible for requesting and implementing those changes.". "The European rulebook it replaced asked for the same six steps, that every change be recorded, tested, assessed, approved, implemented and verified, and never asked the approver to be independent of the implementer.

Two words I want to highlight here are "functions" and "independence", which the law doesn't define. But everywhere else the law talks about a function, it means a part of the organisation: risk management, controls, internal audit. So a function is a role rather than a human being. What independence between two such roles requires, well, it never says. So the rule doesn't say who, or what, does the approving. Basel leaves similar room when it defines dual control, calling it two or more separate "entities (usually persons)" acting in concert.

Together these rules don't ask the questions a developer would ask, which are whether the code works and whether the next person will understand it. They require every change to be recorded, tested, assessed, approved, implemented and verified in a controlled manner. Again, these rules never ask whether the approver understood a change. The reason they give for wanting independence is objectivity and avoiding conflicts of interest, not finding defects. And where the detailed rules do require "source code reviews", they define them as static and dynamic testing, which is a scanner rather than a person.

How carefully a change is checked can also depend on its risk. The policy has to be "based on a risk assessment approach". A reversible configuration change and a change to how money moves don't have to receive the same scrutiny.

When the European supervisors wrote about the risks of frontier AI models in July 2026, the statement never used the words approval, human, segregation, or four eyes. What it asked for was more automation in development and deployment. Nobody has written that a machine may or may not approve a change.

So three different rules are called four eyes, and each one separates something different.

| Four eyes in | What must be separate |
| --- | --- |
| Running a bank | Two persons who direct the business |
| A sensitive action | A second person, for one decision |
| A software change | The function that approves from the one that implements |

Only the third one reaches a pull request, and it is the only one of the three that is new.

So the second pair of eyes came from three places. Fagan wanted defects found early. Linus wanted to choose what went into his own code. The regulator wants an independent function to approve the change, a record of it, and more care when the risk is higher.

Today one pull request does all three jobs.

- The comments are the inspection.
- The approval is the gate.
- The pull request is the record.

The problem is the approval. The approver is usually another developer on the same team, with the same manager. It's a second person, but within the same part of the company. In other rules for banks, a function is independent only if its people don't do the work they check, and if they sit outside the team that does it. But those rules are written for risk management and internal audit, whose job is to watch the business. The change rule never says the approver has to be one of those. So the question stays open: is it enough that the approver didn't write this change, or must they sit outside the team that did?


<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">02</span>
  <div>
    <h2 id="what-changed-when-writing-became-cheap">What Changed When Writing Became Cheap?</h2>
  </div>
</div>

### The Queue Is Real
<!-- Better than the platform-wide merged-PR count: Meta RADAR
     (arXiv 2605.30208v2, 28 May 2026) attributes the growth to agents.
     Lines per human-landed diff +105.9% YoY, per-developer diff volume
     +51%, "with agentic AI responsible for over 80% of that growth".
     Also "the percentage of diffs reviewed within 24 hours is dropping"
     and "In some large groups, we observed thousands of pending diff
     reviews". Research:
     research/20260916-what-changed-when-writing-became-cheap/ -->

We create more code than ever before. Meta reports 51% more changes per developer in one year, with agents causing over 80% of that growth. On GitHub, merged pull requests went from about 25 million a month in January 2023 to over 90 million by June 2026. And reviewing a PR, in GitHub's words, "still takes a human about as long as it ever did."

A change written with AI waits about 16 hours before anyone picks it up. A change written without it waits about three. Once a reviewer starts, the AI-written change is done faster, about 194 minutes against 252. So the scarce thing is attention, not reading speed. The queue is real for the people standing in it, even when the totals look fine.

The strongest evidence isn't a percentage, though. It is what Meta built next. They now run a funnel that scores each change for risk, checks it automatically, and merges the ones that qualify. No human approves those. By the time they published, it had reviewed more than 535,000 changes and merged more than 331,000 of them. A company doesn't build that to solve a problem it doesn't have.

What I still can't tell you is how big the queue is. Nobody has measured how many minutes a review takes, at any company, in any decade. GitHub says the cost hasn't changed, but gives no number for it. The whole research on review effort comes down to two self-reported weekly averages, about six hours a week in open source and about three at Google, and neither divides by the number of reviews. So when someone says we are out of review capacity, they are talking about an amount nobody has counted.

The numbers we do have are easy to misread. One study found that 61% of pull requests written by agents had no recorded review. That sounds like nobody is checking anymore. But in the same repositories, human participation was almost the same for agent and human changes, 30.1% against 30.8%. The difference was in the record, not in the checking. A maintainer who reads a change and merges it leaves no trace.

So this is weaker than a crisis and stronger than a feeling. Writing got cheaper and reading didn't. The companies with the most data answered by building machines to get around their own queues. And the one number that would tell us how much review we can afford has never been collected.

### Three Failures That Look Like One
<!-- Capacity, ownership, assurance. The ownership failure now has data,
     not just the Reddit anecdote: arXiv 2602.23905v1 (27 Feb 2026),
     22,953 PRs from 1,719 heavy AI users, lower-experience authors'
     PRs get 4.52x more review comments, 31% lower acceptance, open
     5.16x longer.
     The mistake slot (CLAUDE.md, open item 1) belongs here, in the
     ownership failure. Nothing written until the record supports one. -->

### Restrict the Input, or Relax the Gate
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
     Research: research/20260916-what-changed-when-writing-became-cheap/ -->

### The Arithmetic Nobody Escapes
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

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">03</span>
  <div>
    <h2 id="who-should-own-the-check">Who Should Own the Check?</h2>
  </div>
</div>

### What a Shared Reviewer Would Protect, and What It Would Cost

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