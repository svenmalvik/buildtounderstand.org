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

Most code reviews today happen inside a pull request. Someone opens a change, someone else reads it and approves it, and then the branch is merged. The pull request has"" become the review tool, and the approval has become the second pair of eyes. But where did the pull request come from? And is it still worth having when the change was written by an AI?

In February 2002, the Linux kernel developer Jeff Garzik wrote a short guide for other developers who wanted their changes in the kernel. A change only became part of the kernel when Linus Torvalds pulled it into his repository. The guide said: publish your changes in a repository on the internet that Linus can pull from, write a summary, and also add a diffstat, which lists the files you changed and how much. These rules existed to save Linus work. Many developers sent him changes, and he had to read and sort all of them himself.

The word "pull" describes what the maintainer does. The contributor pushes the change to a repository they own and then asks the maintainer to pull it. The contributor had no permission to write to the maintainer's repository. So from the beginning, writing a change and accepting it were two acts, done by two different people. It wasn't ment as a control; it was just how the work was split.

GitHub made this a feature in 2008. Review, required approvals, and code owners were all added later, between 2010 and 2017. The pull request had worked as a request to integrate for years without any of them. They are rules placed on top of it.

In 2010, GitHub also allowed pull requests between branches of the same repository. That changed the reason for opening one. In the kernel, a developer opened a pull request because they couldn't write to Linus's repository. It was the only way to get a change in. Inside a company, everyone on the team can write to the shared repository. A team opens a pull request anyway, so that someone looks at the change before it goes in. When a team opens a pull request against its own master branch (now most call it the main branch), it doesn't need permission to integrate because it had already that permission.

The pull request never required a second pair of eyes. Linus as the maintainer would live with every change he pulled, so he wanted to decide what came in. In the kernel workflow, every change passed through a second person before it went in, because only the maintainer (Linus) could pull it. Inside a company, that second person disappears because everyone on the team can merge. The rules that came later bring the second person back. A required approval or a code owner's review says: one more person has to say yes before this change goes in. But in a company repository, there is no Linus. Nobody owns the code the way he owned the kernel. So whether these rules work depends on something else: why people wanted another person to look at their change in the first place.

### Why People Wanted Another Person

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

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">02</span>
  <div>
    <h2 id="what-changed-when-writing-became-cheap">What Changed When Writing Became Cheap?</h2>
  </div>
</div>

### The Queue Is Real

### Three Failures That Look Like One

### What the Maintainers Did

### The Arithmetic Nobody Escapes

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
