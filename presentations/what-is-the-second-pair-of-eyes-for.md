# What Is the Second Pair of Eyes For?

Presentation content derived from
[`_explorations/what-is-the-second-pair-of-eyes-for.md`](../_explorations/what-is-the-second-pair-of-eyes-for.md).

- **Audience:** the AI leadership team
- **Purpose:** introduce the question, show what the evidence says about code
  review now that AI writes code, and list what I would try before buying or
  building a review service. Collect reactions, especially disagreement.
  **This is not a decision meeting.** Nobody is being asked to approve or fund
  anything.
- **Length:** ~40 minutes for the main line, leaving the rest of the slot for
  discussion
- **Slides:** 30, of which 6 are chapter dividers, plus a 4-slide appendix
  held in reserve
- **What the audience should leave with:** the three jobs one pull request does,
  the one line that does not move, five things to try in order, a first week
  they can run in their own repository, and a clear sense of where the
  reasoning is thin
- **Rendering format:** two PowerPoint builds of this same content:
  `…-eyes-for.pptx` (neutral dark theme) and `…-eyes-for-vippsmobilepay.pptx`
  (Vipps MobilePay corporate design: Off White / Dark Blue surfaces, VM Orange
  and VM Blue balanced, Arial as the sanctioned substitute for the brand fonts)

**Five chapters and a conclusion**, each opened by a divider slide carrying the
chapter question and the slides inside it. The structure follows the exploration's
own chapters. Chapter 05 is the practical one: what a developer does in a single
repository, and it is the only chapter that names files and settings.

**One idea per slide.** Each slide carries one claim and one piece of evidence,
about 50 words. The reasoning behind it sits in the *Notes* block under each
slide here, and in the speaker notes of both PowerPoint files. The notes are the
leave-behind: a reader who was not in the room reads the slide and then the
notes, and gets the argument in full. The *Visual* line is guidance for
generation, not slide text.

**Draft status.** The exploration this deck is built from is unpublished, and
the deck inherits its open items. Two matter in the room: the claim that cheap
controls are available and unused has not been checked against our
repositories, and Prototype 0.1 of the author's check has not been used by any
team. Both are stated on the slides rather than smoothed over. Numbers follow
the exploration: percentages and prices exact, large counts rounded, European
number formatting.

**The appendix exists because the room may push on the evidence.** A1 lists
the peer examples in one table, A2 the regulatory detail, A3 how far to trust
each number, and A4 the names and terms. Jump to them; don't present them.

---

## Slide 1 — What Is the Second Pair of Eyes For?

One developer opens a pull request. Another reads it and approves it. We call that approval the second pair of eyes. Now the change may have been written by an AI, and since September 2026 an AI can count as the approver too.

**Where did it come from?**
Maintainer, reviewer, regulator.

**What changed?**
Writing became cheap. Approval became a setting.

**Who should own the check?**
And what I would try first.

An introduction to how far I got. I am looking for reactions and disagreement, not a decision.

**Notes:** Most code reviews happen in a pull request. A developer opens it, another developer reads and approves it, and the branch is merged. We use the pull request as a review tool and the approval as the second pair of eyes. Two things have changed. The change itself may now be written by an AI, and on 1 September 2026 GitHub shipped a setting that lets Copilot's review count toward a repository's required approvals. So the question in the title is no longer rhetorical. Nobody is being asked to approve or fund anything today. I want to hear where this reasoning breaks in your context.

**Visual:** Title slide. Three small cards name the chapters. The register line is the last thing on the slide and should be read aloud.

---

## Slide 2 — Chapter 01: Where did the second pair of eyes come from?

*Divider slide.*

Three people wanted a second reader, and each wanted something different from it. None of them designed the thing we use today.

- The pull request was a request to integrate
- Who lives with the change
- Defects, or understanding
- The regulator's pair of eyes
- One pull request does three jobs

**Notes:** Before asking who should own the check, it is worth asking what the check was ever for. Three separate answers, from three places, all from a time when changes were scarce. Nobody designed the pull request to carry all three at once, which is why it carries them badly now.

**Visual:** Chapter divider. Dark, the number large, the question next to it, and the five slides of this chapter listed underneath.

---

## Slide 3 — The pull request was a request to integrate

- **2002:** Kernel contributors publish a change and ask Linus to pull it
- **2008:** GitHub makes the pull request a feature
- **2010:** Pull requests between branches of one repository
- **2011–2017:** Merge button, protected branches, required reviews, code owners

> Writing a change and accepting it were separate acts from the start. That was how the work was divided, not a control. The approval rules came later, on top.

**Notes:** In 2002, Jeff Garzik wrote a short guide for developers who wanted their changes in the Linux kernel: publish the change in a repository Linus Torvalds can pull from, write a summary, list the files you changed. The rules existed to save Linus work. The contributor could not write to the maintainer's repository, so writing and accepting were two acts by two people from the beginning. GitHub made the pull request a feature in 2008. In 2010 it allowed pull requests between branches of the same repository, which changed the reason for opening one: inside a company everyone can already merge, so a team opens a pull request so that someone looks first. Required approvals and code owners arrived between 2011 and 2017. The pull request worked as a request to integrate for years without any of them.

**Visual:** Timeline strip across the middle, the quote below it. The 2010 step is the pivot from permission to review.

---

## Slide 4 — Who lives with the change

**The kernel**
Linus read the code and carried the consequences himself.

**A payment company**
One developer reads the change. The company answers for it, to customers and to its supervisor.

> A required approval puts a developer at the gate. It does not say what they should do there.

**Notes:** In the kernel every change passed through Linus because only he could pull it, and he would live with every change he pulled. Inside a company the second person disappears, because everyone on the team can merge. A required approval brings that person back: one more person has to say yes. But there is no Linus at the keyboard. At a payment company the one who lives with the change is the company. When a change moves money the wrong way, the company answers to its customers and to its supervisor. That is not ownership of an asset. It is exposure to an outcome, and it sits nowhere near the merge button. The company never reads the change. What it is exposed to depends entirely on the one developer who does.

**Visual:** Two panels: one person reads and carries, versus one reads and another carries. The quote is the question the whole deck answers.

---

## Slide 5 — Why people wanted another person

- **82%** of errors caught by inspection in Fagan's 1976 case study
- **14%** of Microsoft review comments that pointed at a defect
- **29%** suggested improvements to code that already worked

Google's reason was different from the start: review exists so that other developers can **understand** the code. Two questions, one approval. Does it work, and will the next person understand it?

**Notes:** Ask developers why review exists and the answer is to catch mistakes. Michael Fagan's 1976 paper on inspections found one case where inspection caught 82% of the errors eventually found. But look at what reviewers actually write. At Microsoft, developers ranked finding defects as their top reason for reviewing. Researchers then read the comments. Only 14% pointed at a defect. The largest group, 29%, were suggestions to improve code that already worked. At Google, the person credited with introducing review gave a different reason from the start: to force developers to write code that other developers could understand. So a review answers two questions. A one-line configuration fix needs the first. A change to how payments are calculated needs both, and needs someone who understands payments to answer the second. Both go through the same pull request and get the same single approval.

**Visual:** Three stat tiles, then one sentence. The two questions in bold are the problem statement for chapter 02.

---

## Slide 6 — The regulator's pair of eyes

> "The independence of the functions that approve changes and the functions responsible for requesting and implementing those changes."

**Functions, not persons**
A function is a role. Nothing says the approver must be a person.

**Risk-based**
A config change and a change that moves money need not get the same scrutiny.

**Silent on AI**
No supervisor has written that an AI may or may not approve a change.

**Notes:** At Vipps MobilePay there is a third reason for a second pair of eyes: the law requires one. Four eyes in banking means three different things. Two persons must direct the business, which is where the German Vier-Augen-Prinzip comes from. A second person must check a sensitive manual action, such as lowering a customer's money-laundering risk level. And since July 2025, under the EU's Digital Operational Resilience Act and its technical standard, the function that approves a change must be independent of the function that requests and implements it. The rule says functions, and everywhere else the law uses that word it means a role, not a human. The policy must be risk-based. Where the rules require source code review they define it as static and dynamic testing, a tool rather than a person. And the European supervisors' July 2026 statement on frontier AI never used the words approval, human, or four eyes. The rule asks neither of the developer questions from the previous slide. It never asks whether the approver understood the change. Detail in appendix A2.

**Visual:** The rule verbatim as the opening quote, three short cards under it. Appendix A2 carries the full regulatory detail.

---

## Slide 7 — One pull request does three jobs

**The reading**
The comments prove someone read it.

**The gate**
The approval is what the change has to pass.

**The record**
The pull request stays behind as evidence.

The weak point is the gate. The approver is usually a colleague on the same team. And nobody asked what happens when the changes outnumber the people who can read them.

**Notes:** The second pair of eyes came from three places. Fagan wanted defects found early. Linus wanted to choose what went into his own code. The regulator wants an independent function to approve, a record of it, and more care where the risk is higher. Today one pull request does all three jobs. The comments are the reading, the approval is the gate, the pull request is the record. The problem is the approval. The approver is usually another developer on the same team with the same manager. The rule never says whether that is independent enough or whether the approver must sit outside the team. That question stays open for the whole deck. And all three roots come from a time when changes were scarce. An inspection needed a meeting. Linus read what he pulled. Nobody asked what happens when the changes outnumber the readers.

**Visual:** Three cards. Reading, gate, record are the load-bearing words for the rest of the deck.

---

## Slide 8 — Chapter 02: What changed when writing became cheap?

*Divider slide.*

More code arrives than anyone can read. The reader adapted, and the approval became a setting.

- Writing became cheap
- Familiarity replaced reading
- Three failures that look like one
- The numbers stopped adding up
- Four ways out
- The approval became a setting

**Notes:** This chapter is the evidence. It is the part where I expect the most disagreement, so stop me on any number. Every figure has a caveat and they are collected in appendix A3.

**Visual:** Chapter divider, same treatment as chapter 01. Six items, so the list is the tightest of the four.

---

## Slide 9 — Writing became cheap

- **+51%** changes per developer in one year at Meta
- **25m → 90m** merged pull requests a month on GitHub, 2023 to 2026
- **16 h vs 3 h** wait before an AI-written pull request is picked up
- **400 vs 157** lines in an AI-written pull request, decided in less time

> Bigger changes, decided faster. Probably not read.

**Notes:** Meta reports 51% more changes per developer in one year, with agents causing over 80% of that growth. On GitHub, merged pull requests went from about 25 million a month in January 2023 to over 90 million by June 2026, which is platform growth rather than the AI share. A pull request written with AI waits more than 16 hours to be picked up against about 3 for a human-written one. Once picked up it reaches a decision in about 194 minutes against 252, which sounds like reviewing got faster. But those changes are over 400 lines against 157, and nobody measured how many of the minutes were spent reading. A change nearly three times the size, decided in less time, is probably not really read. Meta now scores each change for risk and merges the low-risk ones with no human approval. More than 331.000 changes reached production that way.

**Visual:** Four stat tiles and a five-word quote. The fourth tile is the one that looks like good news and isn't.

---

## Slide 10 — Familiarity replaced reading

- **30,1% →
36,8%** approval rate as reviewers saw more agent-written code
- **−22%** inline comments over the same seven months
- **96%** of developers do not fully trust AI output
- **48%** always verify it before committing

> Reviewers approve what has become familiar. Authors submit what they doubt.

**Notes:** Researchers followed 400 reviewers through more than 11.000 reviews of agent-written code over seven months. As each reviewer saw more of it, their approval rate rose from 30,1% to 36,8% and their inline comments fell by 22%. The changes stayed the same size and waiting times got longer, not shorter. The code did not get better. It got familiar. Authors are no more careful. Sonar asked about 1.150 developers: 96% said they do not fully trust that AI output is correct, but only 48% said they always verify it before committing. Google reviewed code so that the next developer could understand it. Now half of the authors do not check their own.

**Visual:** Two pairs of tiles: reviewers on the left, authors on the right. The quote names the pattern before the next slide splits it.

---

## Slide 11 — Three failures that look like one

**1 · The reading is overwhelmed**
More code arrives than people can read.

**2 · The first reading never happened**
The author skims 400 generated lines and opens the pull request. Nothing checks for that.

**3 · The record lies**
Approved, when nobody read it.

> I approved a change because the tests were green, without reading it. The record shows my approval. What it recorded was confidence in the tests.

**Notes:** There are three problems, not one. The first overwhelms the reading: more arrives than anyone can read. The third breaks the record, which now says a change was approved when nobody read it. I have done the third one. I approved a change because the tests were green, without reading it. The green check stood in for my judgement, and the recorded approval recorded confidence in the tests rather than a reading of the change. The second failure is different. An agent writes 400 lines, the author skims them and opens the pull request. The understanding that used to come with writing the change never happens. The tests still pass and the approval still shows a name, but nothing on a pull request shows whether anyone understood the change. Nobody built a check for that, because the first reading used to come free with the work. It is the failure I want to design for at the end.

**Visual:** Three short cards, then the mistake as a first-person aside. It sits with the third failure because that is the one it illustrates. The second failure returns on slide 21.

---

## Slide 12 — The numbers stopped adding up

- **200 lines / h** beyond this, reviewers find about half the defects
- **1 in 4** AI-written pull requests has more than 400 lines
- **2 hours** of one person's attention for that one change
- **3,2 h / week** spent reviewing by Google developers before AI

Nobody can review everything properly anymore. Most teams have already stopped reviewing some changes. **Did anyone choose which ones?**

**Notes:** In 2009, Kemerer and Paulk measured what happens as a reviewer speeds up. Up to 200 lines an hour people found most of the defects. Faster than that, about half. One in four AI-written pull requests has over 400 lines, so at 200 lines an hour that is two hours of one person's attention for a single change. Before AI, developers spent about 3,2 hours a week reviewing at Google and about 6,4 in open source. That is one to three changes a week read properly, against 51% more changes per developer. One caution: nobody publishes how many minutes a reviewer actually spends on a change, so the 200 lines an hour is an assumption from one 2009 study. Treat the arithmetic as a shape, not a measurement. The point survives the caution. Nobody can review everything properly anymore, so most teams have already stopped reviewing some changes. The question is whether anyone chose which ones.

**Visual:** Four tiles as a left-to-right chain of arithmetic. The bold question closes the slide. The caution about the 2009 assumption is in the notes and in appendix A3.

---

## Slide 13 — Four ways out

**Have fewer pull requests**
Godot banned AI-generated code and kept the human approver.

**Approve some without a human**
Zalando auto-approves 33% as low-risk. None of these companies is regulated.

**Check before you open it**
Coding agents review your branch first. Rust: not a substitute for self-review.

**Make each one simpler to approve**
Adyen: under five files, a human approves, a designated person re-reads.

**Notes:** The Godot Foundation said in June 2026 that the reviewer shortage was already a problem, and one they had ignored. Four kinds of answer are in use. Open source mostly restricts the input: Godot banned AI-generated code, five Rust teams run a circuit breaker on the share of AI-written merges, curl ended its bug bounty over slop. Companies mostly relax the gate: Meta, Zalando and Spotify auto-approve what they judge low-risk, and none of the three is a regulated financial company. A third answer moves the check earlier: Claude Code, Codex and Cursor run a review on your branch before you open a pull request, and Rust's policy says that does not substitute for self-review. The fourth makes each change easier to approve. Adyen, the only regulated payment company here, runs over 4.000 automated merge requests with a human approving each, and added a designated person who re-reads approved changes because reviewers had started to pattern-match. Two caveats: Adyen's changes came from a deterministic bot, not a model. And whether a classifier that approves low-risk changes counts as an independent function under DORA, nobody has written down. Full list in appendix A1.

**Visual:** Four cards, one example each. Everything else about the peers is in appendix A1 and the notes.

---

## Slide 14 — The approval became a setting

**Copilot, the author**
Blocked from approving, like any author.

**Copilot, the reviewer**
A second identity. It can approve what the first one wrote, and the audit log has no event for it.

> Someone has to decide which repositories have it on, which changes are exempt, and who answers when it goes wrong. On most teams nobody has that job.

**Notes:** On 1 September 2026, GitHub shipped a setting that lets Copilot's review count toward a repository's required-approvals rule. It is off by default for enterprises and in public preview, and I have not found anyone using it. The rule that authors cannot approve their own pull request works on identities, and Copilot has two: one that writes and one that reviews. The writing identity is blocked. The reviewing identity is free to approve. If I ask Copilot to make a change, GitHub will not let me approve it, because it knows I am too close. Copilot's reviewer has no such limit. GitHub's own documentation says the agent gets a second opinion on its code with Copilot code review, which is a second opinion from itself. Nothing in the documentation mentions segregation of duties or independence. The approval shows on the pull request under Copilot's name, but the organisation audit log has no event for it. To find what Copilot approved last quarter you would open every pull request. The approval is a setting now, and on most teams nobody has been given the job of deciding how it is set.

**Visual:** Two identity cards, the author greyed and the reviewer lit. The quote names the job nobody holds, which is chapter 03's question.

---

## Slide 15 — Chapter 03: Who should own the check?

*Divider slide.*

One shared reviewer for everyone is the obvious answer. It is better at two jobs out of three.

- One answer: a centralized AI reviewer
- What it would cost
- Centralize the machinery, keep the decision local

**Notes:** Nobody at work asked for a centralized reviewer. This was my own first instinct, and this chapter is me arguing against it. If you think the argument is wrong, this is the chapter to interrupt.

**Visual:** Chapter divider. Only three items, so the list sits higher and lighter than the previous two.

---

## Slide 16 — One answer: a centralized AI reviewer

**"An outsider sees more"**
The research measures context, not reading.

**"AI never gets tired"**
The people reading its reviews do.

**"Nobody looks for security"**
Because nobody asked them to.

> Better at coverage. Possibly better at the record. Not better at the approval.

**Notes:** One answer: our developer experience team runs one AI reviewer for every repository, approving low-risk changes without a human. Three reasons are usually given. An outsider sees more: but the research measures whether the reviewer has context, such as why a workaround exists and what the team already decided. Nine out of ten Microsoft developers said a change takes longer to review when they do not know the code, and a first read of a diff never supplies that, however fast. AI never gets tired: but the people reading its reviews do, and one person facing every change will at some point just trust and approve. Nobody on the team looks for security: true, 614 of almost 21.000 review comments in two open source projects touched it. But asked directly, the same developers said they always think about it. Nobody had asked them to, and asking is cheaper than a service. What a managed reviewer does do better is coverage. It reads every change, and projects with fewer unreviewed pull requests had fewer security bugs. It could also keep a better record than GitHub's audit log, which only notes that a review happened and reaches back 180 days. What it has not managed to do better is the approval.

**Visual:** Three claim cards, the claim in quotation marks and the rebuttal in one line. The quote maps back to reading, gate, record.

---

## Slide 17 — What it would cost

- **$43.000 to
$260.000** a year in licences for about 300 engineers
- **>90%** of the riskiest changes approved by the FCA's 23 firms' change boards
- **2,6×** more likely to be a worst performer with outside approvers
- **32 of 33** planted vulnerabilities passed two AI reviewers

> A service that reads every change stops being a check. And every repository misses the same bugs.

**Notes:** A managed review service costs $12 to $72 per developer per month, so $43.000 to $260.000 a year for us, paid whether or not the queue gets shorter. That is the smallest cost. The first real cost is what happens to a check when one function reviews for everyone. Google's central readability review certifies 1 to 2% of engineers, so most teams go outside for every review. Google's DORA research, the DevOps Research and Assessment programme, found companies with outside approvers 2,6 times more likely to be in the worst-performing group. The UK's FCA looked at 23 firms and over a million changes: their change boards approved more than 90% of the riskiest changes, some every single one. The second cost is that engineers who hand their reviews to a service stop understanding their own code, and that is the part they cannot buy back. The third is a shared blind spot. In a vendor study, Claude caught 62% of Codex's serious bugs but only 53,7% of its own; GPT caught 60% of Claude's but 50,5% of Codex's. Researchers re-planted 33 known vulnerabilities and rewrote the descriptions until the reviewer stopped objecting; 32 got past Claude Code and CodeRabbit. Two more: at one company, turning a reviewer on raised pull request close time from under six hours to over eight. And the lock-in is not the comments, which you own, but the context the tool learns about your code, which none of six vendors lets you export.

**Visual:** Four tiles, licence first so the room sees it is the smallest number. Caveats on each figure are in appendix A3.

---

## Slide 18 — Centralize the machinery, keep the decision local

**Mechanically verifiable**
Formatting, known bug patterns, secrets, dependencies. Google applies 3.000 automated fixes a day at under 5% false positives.

**Needs a person**
Is the change wanted? Norms, gatekeeping, education. Correct code can still be unwanted.

Atlassian replaced 20 CI/CD servers with one platform and cut lead time from 2 days to 90 minutes. Cloudflare runs one reviewer with per-team config and a logged break-glass. **Shared tools, local approval.**

**Notes:** Where the rules require source code review they mean static and dynamic testing, and Google has drawn that line in writing for a decade. Static analysis exists so that human review can focus on issues that are not mechanically verifiable. One Java hash-code bug was flagged, fixed 31 times, then made a compiler error. Developers apply about 3.000 automated fixes a day and click not useful about 250 times, a false-positive rate just below 5%. What remains on the other side is judgment: whether the code is wanted, norms where the style guide is silent, gatekeeping, education. The dividing line is not AI versus human or vendor versus self-built. It is mechanically verifiable versus not, and everything on the first side can be centralized without controversy. Google's DORA research supports shared platforms, since teams that choose their own tools deliver better but unconstrained choice fragments. That argues for a shared platform, not a shared approver. Atlassian replaced more than 20 CI/CD servers with one platform: build time from 6 hours to 90 minutes, lead time from 2 days to 90 minutes, $4 million a year saved by one team, and teams still choose what runs. Cloudflare shows the shape for review: one reviewer company-wide, a config file per team, and a break-glass override logged every time. Caveat: no study has shown platform engineering causes such gains rather than strong teams building platforms.

**Visual:** Two cards split the slide: left mechanical, right judgment. The closing sentence carries the two examples and the bold verdict.

---

## Slide 19 — Chapter 04: What would I try first?

*Divider slide.*

Five things, cheapest first. Four of them exist today. The fifth is mine and unproven.

- What I would try before building a review service
- The author's half of four eyes

**Notes:** Nothing in this chapter is a proposal for funding. It is the order I would try things in, and I want to know which one you would start with and which one you think is a waste of time.

**Visual:** Chapter divider. Two items only. The lead line carries more weight here than the list.

---

## Slide 20 — What I would try before building a review service

1. **Turn on what already exists.** Required reviews, status checks, secret and dependency scanning. I have not checked what is on today.
2. **Tier repositories by what they touch.** More from the ones that move money, less from the internal chatbot.
3. **Centralize the machinery.** Formatters, linters, scanners, once for the company.
4. **Pair models across vendors.** A different model family reviews what the first one wrote.
5. **The author's half of four eyes.** The one new idea. Next slide.

**Notes:** In roughly the order I would try them, cheapest and most certain first. The first four are available today, proven at scale by someone else, and outsource no judgment. First, turn on what already exists: required reviews, required status checks, no direct pushes to protected branches, stale approvals dismissed on new commits, secret and dependency scanning. I have not checked which of these are on across our repositories, and that check is the actual first step. Second, tier repositories by what they touch. A payment repository and an internal chatbot are not the same bet even when a change to each looks equally small. Spotify's Soundcheck runs different tracks of checks per kind of component on one platform. Third, centralize the machinery the way Atlassian did, and keep the approval local. Fourth, pair models across vendors in CI. It fixes exactly one evidenced blind spot for the cost of an API call, which is what Greptile sells as the independent code validator. Fifth is the one idea in this deck that is genuinely new, and the one with the least evidence. Cost and exit for each item: the first three have nothing to leave. GitHub's security add-ons would be about $176.400 a year for 300 active committers, and swapping the scanner takes nothing with it. The real risk is that platform initiatives fail to show impact 60 to 70% of the time and close to half are disbanded within 18 months.

**Visual:** A numbered list of five, one line each. Items 1 to 4 tagged 'available today', item 5 tagged 'unproven'. Nothing here should look like a roadmap.

---

## Slide 21 — The author's half of four eyes

Before opening a pull request, the author explains the change in their own words.

**Why**
Explaining something yourself measurably deepens your understanding.

**Limit**
Across 80.000 pull requests, descriptions rarely changed the review. Except when they explained and asked.

**Risk**
A required field decays into "N/A".

**Status:** Prototype 0.1 is a design. No team has used it.

**Notes:** The second failure from slide 11 was never about volume. Authors stopped understanding what they submit, and nothing on a pull request looks for that, because the first reading used to come free with writing the change. The check I want to design asks the author to explain the change in their own words before opening the pull request. The cognitive-science case is old and solid: prompting someone to explain something in their own words deepens their understanding of it. GitHub already recommends self-review. But a 2026 study of 80.000 pull requests across 156 projects found that descriptions mostly make a negligible difference to review outcomes, with one exception: a description that explains the code and asks for a specific kind of feedback. About a third of pull requests have no description at all. The risk is easy to name. Making an explanation mandatory is trivial, and a required field decays into N/A, which satisfies the check without the understanding it was meant to prove. That is the same empty ritual as the third failure. Prototype 0.1 exists as a design. No team has used it, so I am not presenting results. The whole design problem is making it the second reading, not the ritual.

**Visual:** The idea in one sentence at the top, three one-line cards, the status line as a plain admission at the bottom.

---

## Slide 22 — Chapter 05: What would I do in one repository?

*Divider slide.*

Chapter 04 was the order for the company. This is the same order in one repository, with the file each step lives in.

- First, decide what this repository touches
- Make the mechanical checks unskippable
- Two decisions that follow from the tier
- Ask the author for what no check can see
- The first week

**Notes:** Everything so far has been a decision somebody else makes. This chapter is for the developer who agrees with the argument and wants to do something on Monday. Nothing in it needs a platform team, a budget, or a vendor. Every item is a file in the repository or a setting on it.

**Visual:** Chapter divider, same treatment as the others. This is the practical chapter, so the items read as actions rather than questions.

---

## Slide 23 — First, decide what this repository touches

Chapter 04 tiered repositories and never said who does the tiering. This repository has to answer for itself, because the answer sets how strict everything after it should be.

- Does it move money, hold customer data, or neither?
- Write the answer in the README, under a short "Review rules" heading
- Say what follows: how many reviewers, whether a machine may approve, whether a security review is mandatory
- Revisit it when the repository starts touching something new

> One sentence in the README that a new joiner can find is more than most repositories have today.

**Notes:** Chapter 04 said to tier repositories by what they touch, and never said who does the tiering. A developer with one repository in front of them has to settle it, because the answer decides how strict every step after this one should be: how many reviewers, whether a machine may approve, whether a security review is mandatory. A payment repository and an internal dashboard are not the same bet, even when a change to each looks equally small. Chapter 01 found the regulation asking for exactly this, a policy based on a risk assessment approach, and it never said the assessment had to be elaborate. One sentence in the README, dated, that a new joiner can find, is more than most repositories have today. The date matters because the answer expires: a repository that starts handling customer data has changed tier whether or not anybody wrote it down.

**Visual:** The question as the body, the three answers left deliberately plain. This is a ten-minute decision, and the slide should look like one.

---

## Slide 24 — Make the mechanical checks unskippable

**Run the checks**
Format, lint, test and static analysis in a workflow file. Dependency and secret scanning switched on.

**Require the checks**
Require each check by name. Require a pull request. Stop direct pushes to the default branch.

**Keep approvals current**
Dismiss stale approvals when new commits land, so the approval refers to the code that actually merges.

> A check that runs is a suggestion. A check that blocks a merge is a control.

**Notes:** This is chapter 03's dividing line applied to one repository. Everything mechanically verifiable runs before a person looks at the change. Formatting, linting, the test suite and a static analysis pass go in a workflow file under .github/workflows. Dependency scanning is a dependabot.yml. Secret scanning is a toggle in the repository settings. Google's reason is the one from chapter 03: static analysis exists so that human review can focus on what is not mechanically verifiable. The second step is the one people skip. A check that merely runs is advice. In branch protection or a ruleset, require those status checks by name, require a pull request before merging, and stop direct pushes to the default branch. Then dismiss stale approvals when new commits land. Dismissing stale approvals is the cheapest defence in this whole deck against the third failure, where the record says approved and nobody read the version that shipped.

**Visual:** Three cards in the order they get done: run, require, keep honest. The quote is the sentence to say out loud.

---

## Slide 25 — Two decisions that follow from the tier

**Who reviews the paths that carry risk**
A CODEOWNERS file requires a named reviewer for the code that moves money or touches customer data. The rest of the repository stays on the lighter default.

**Whether a machine may approve here**
Off by default today. A payment repository and an internal dashboard may answer differently. Neither should answer by accident.

> Write it in the README next to the tier, with the reason. The setting has nowhere to hold one, and nothing logs a machine approval.

**Notes:** Step 1 settled what the whole repository touches. Both decisions here follow from that answer. A CODEOWNERS file requires a named reviewer for the paths that move money or hold customer data, and leaves the rest on the lighter default. That is the risk-based approach the regulation asks for, written as a file rather than a policy nobody reads. It also answers something the approval rule leaves open: not just that someone approved, but that someone who knows this code did. The second decision comes from chapter 02. Whether Copilot's review counts toward this repository's required approvals is a per-repository choice, currently off by default. Write the answer into the README under the same Review rules heading step 1 started, with the reason. The setting has nowhere to hold a reason, and chapter 02 found GitHub's organisation audit log records no event at all when a machine approves, so the README is the only place the decision survives. Both repositories are allowed to answer differently. What neither should do is answer by accident, which is what happens when nobody decides.

**Visual:** Two cards, deliberately only two. The quote is the point: the second decision is the one nobody currently owns.

---

## Slide 26 — Ask the author for what no check can see

One pull request template. The same questions in front of every change.

- What changed, and why it belongs here
- What you want looked at, specifically
- How to undo it
- Which parts an agent wrote

> Across 80.000 pull requests, descriptions rarely changed the review. The exception was one that explains the code and asks for a specific kind of feedback. So ask for both.

**Notes:** This is the author's half of four eyes, in the one place a repository can host it. A pull_request_template.md in the .github folder puts the same questions in front of every pull request. The wording matters more than the existence. Chapter 04 cited a 2026 study of 80.000 pull requests across 156 projects where description elements made largely negligible difference to review outcomes, with one exception: a description that explains the code and asks for a specific kind of feedback. So the template asks for both. A template that only asks for a summary is asking for the thing the study found does not matter. One honest limit: a template is a prompt, not a control. GitHub prefills it and nothing stops someone deleting it. Enforcing it takes a CI check, and an enforced field is exactly where N/A appears.

**Visual:** The four questions as the body of the slide, because they are the deliverable. The quote carries the one finding that shapes the wording.

---

## Slide 27 — The first week

| When | Do | Where it lives |
| --- | --- | --- |
| Day 1 | Write down what this repository touches, and what follows from it | README, under "Review rules" |
| Day 1 | Format, lint, test, static analysis on every change | .github/workflows/ |
| Day 1 | Dependency and secret scanning | .github/dependabot.yml, repository settings |
| Day 2 | Require those checks, require a pull request, stop direct pushes | Branch protection, or a ruleset |
| Day 2 | Dismiss stale approvals when new commits land | The same place |
| Day 3 | A named reviewer for the paths that carry risk | .github/CODEOWNERS |
| Day 3 | Whether a machine may approve here, and why | README, under "Review rules" |
| Day 4 | The template that explains and asks | .github/pull_request_template.md |
| Ongoing | Read a sample of already-approved changes | A calendar entry, not a tool |

Every line is a file or a setting, copied to the next repository in minutes and reverted by deleting a line. **I have not checked which of these are already on in ours.**

**Notes:** The last row is the one nothing else covers. Everything above it decays quietly, and only a person re-reading approved changes notices. That is Adyen's fix from chapter 02, the one regulated payment company in this deck, whose reviewers said they had started to pattern-match after a dozen near-identical changes. At one-repository scale it is a recurring calendar entry rather than a tool: read a sample of merged pull requests and ask whether the approvals on them meant anything. On leverage and freedom: the workflow file and the template are copied to the next repository in minutes, so the second repository costs a fraction of the first. Each item is reverted by deleting a line, with no vendor to ask. What the list cannot do is the job chapter 01 found underneath all three: decide whether the change is wanted. Days 1 to 3 make that decision cheaper to reach, day 4 gives the decider something to read, and the last row checks that the decision is still being made. None of them makes it. And I owe this argument the check in the last line: I do not know how many of these settings are already on in our repositories.

**Visual:** The table takes the width and is the takeaway slide, the one worth photographing. The closing line keeps the unverified claim visible instead of letting the table look like a finished audit.

---

## Slide 28 — Conclusion

*Divider slide.*

What moves, what doesn't, and what I still don't know.

**Notes:** Two slides. The first is the answer to the title question. The second is where I hand it back to you.

**Visual:** Finale divider. No number, an accent rule instead, matching the exploration's own finale heading treatment.

---

## Slide 29 — What moves, and what doesn't

**Shorter queue**
Turn on what is there. Centralize the mechanical. Log it. Tier by risk.

**Higher quality, with evidence**
A different model family reviews the change. Two more are design problems, not results.

**Set aside**
Restricting AI use. Open source defends against strangers. We employ our authors.

> The approval stays with a human who is independent of whoever implemented the change. That is the one line that does not move.

**Notes:** The queue gets shorter by turning on what is already there, centralizing everything mechanical, giving that machinery its own log of approved, rejected and why, the way secret scanning already logs it, and tiering by what the repository touches with a logged break-glass rather than an org-wide switch nobody downstream can turn off. Quality goes up with real evidence in exactly one place: a different model family reviews the change. It might go up in two more, the author's half of four eyes and Adyen's periodic look at already-approved changes to catch the gate going stale, but both are design problems here, not results. Restricting how much AI our engineers may use is set aside, not rejected: Godot, Rust and curl defend against low-trust external contributors, which is a different problem from employed engineers using a tool they were given. The approval itself stays with a human who is independent of whoever implemented the change, including when the change was written by an AI. Two honest notes. The rules are silent on AI approval, not against it, so this is the cautious reading of that silence and not the only one allowed. And whether same-team approval is independent enough is a question this deck raised on slide 7 and never answered.

**Visual:** Three short cards, then the quote as the largest text on the slide. The two hedges live in the notes and return as open questions on the next slide.

---

## Slide 30 — What I don't know yet

**Same team, or outside it?**
Everything here assumes same-team approval is enough. The regulation does not say.

**Does a classifier count as a function?**
Meta and Zalando auto-approve. Nobody has written down whether DORA allows it.

**What is switched on today?**
A day of checking I have not done.

**Does the author's check survive a team?**
Nobody has used it.

**What would help me most:** A review decision you made and had to undo. What did it cost?

**What would change my mind:** A regulated company whose auditor accepted a machine's approval.

**Notes:** Four things I do not know. Whether the approver must sit outside the team that shipped the change, which slides 6 and 7 raised and everything since has assumed away. Whether a classifier that auto-approves low-risk changes counts as an independent function under DORA, which depends on who owns it and whether its decision lands where an auditor can read it, and which nobody has written down. Which branch protections and scanners are on across our repositories today, which is a day of work I have not done and the cheapest item on my list rests on it. And whether the author's check survives contact with a real team, or becomes the ritual. What would help me most is a review decision you have already made and had to undo: a rule people bypassed, a gate you loosened, a reviewer you switched off, and what it cost. What would change my mind is a regulated company that let a machine approve changes and had an auditor accept the record, or evidence that a managed reviewer improved the gate itself rather than the coverage.

**Visual:** Four open questions as cards, not ranked. Two reply cards at the bottom. Nothing on this slide should look like a recommendation waiting for approval.

---

# Appendix

Not presented. Each of these answers one likely question in more detail than
the main line needs.

## A1 — Who did what about the queue

*Use when someone asks for the full list behind slide 13.*

| Who | What they did | Human approver? | Regulated? |
| --- | --- | --- | --- |
| Meta | Risk score per change, low-risk merged automatically. 331.000+ to production. | No, for low risk | No |
| Zalando | Classifier on open. 33% auto-approved as low-risk, author merges. | No, for low risk | No |
| Spotify | 76% more pull requests. Auto-merges what it judges safe. Soundcheck tiers checks per component type. | No, for safe | No |
| Shopify | System writes and explains security fixes, freshness-gated merge queue. Backlog down ~70% in 11 days. | Yes | No |
| Adyen | 4.000+ automated merge requests from a deterministic bot, under five files each. Designated person re-reads approved changes. | Yes | Yes |
| Monzo | "An engineer still reviews and merges, but the bottleneck moves from 'find an engineer with capacity' to 'find a reviewer'." | Yes | Yes |
| Cloudflare | 131.000+ review runs in 30 days across 5.000+ repositories. Per-team config, break-glass used 0,6% of the time. Explicitly not a replacement for human review. | Yes | No |
| Godot | Banned AI-generated contributions. "All PRs must be reviewed and approved by a human before merging." | Yes | No |
| Rust (five teams) | Circuit breaker: AI over half of merges in six weeks, AI changes stop for ten days. | Yes | No |
| curl | Ended its bug bounty in January 2026. About 20% of security submissions were slop. | Yes | No |
| GitHub | Per-contributor limit on open pull requests. Copilot approval can count toward required approvals since 1 Sep 2026. | Setting | No |

**Visual:** One dense table. Not presented. Regulated column is the one to point at if someone asks who our actual peers are: Adyen and Monzo.

## A2 — The regulatory detail

*Use when someone wants the rule read out rather than summarised.*

- **Two persons direct the business.** European banking law (CRD art. 13) grants a licence only where "at least two persons effectively direct the business". That is the origin of Vier-Augen-Prinzip and the English phrase four eyes. They approve no individual change.
- **Dual control on a sensitive action.** Basel defines it as two or more separate "entities (usually persons)" acting in concert. The Norwegian supervisor fined a savings bank in 2023 partly because no four-eyes check existed when an employee manually lowered a customer's money-laundering risk level.
- **Change management before July 2025.** IKT-forskriften § 9 required procedures for handling changes, and that they be followed. It never asked for an approver.
- **Change management since July 2025.** DORA (EU 2022/2554) art. 9(4)(e), with RTS 2024/1774 art. 17(1)(b): "the independence of the functions that approve changes and the functions responsible for requesting and implementing those changes". Every change recorded, tested, assessed, approved, implemented and verified. Policy "based on a risk assessment approach". Source code reviews defined as static and dynamic testing.
- **Not defined:** function, independence. Elsewhere in the rulebook a function is a part of the organisation. Whether the approver must sit outside the implementing team is not stated.

*The art. 17 wording relies on two secondary reproductions that agree. Verify against EUR-Lex before anything is quoted externally. Two things in this deck are called DORA: the EU act here, and Google's DevOps Research and Assessment on slides 17 and 18.*

**Visual:** Bullets, one per rule. The note at the bottom is a real caveat, not decoration: the wording has not been checked against the primary source.

## A3 — How far to trust each number

*Use when someone pushes on a figure. Every number in the main line has a caveat, and these are them.*

| Number | Where it comes from | How far it carries |
| --- | --- | --- |
| 30,1% → 36,8% approval, comments −22% | 400 reviewers, 11.429 reviews, seven months, three controls. KDD 2026 workshop paper. | Measures repetition and load, not team boundaries. |
| 96% distrust, 48% always verify | Sonar survey, about 1.150 respondents. | Self-reported. |
| 200 lines an hour | Kemerer & Paulk, 2009. | One study. The 2-hour arithmetic is mine and rests on it. |
| 3,2 h and 6,4 h a week reviewing | Google telemetry; open-source survey of 287 respondents. | The open-source figure is self-reported. |
| 62% vs 53,7%; 60% vs 50,5% | Greptile, two sets of 500 pull requests, July 2026. | Vendor research selling the feature. Directional only. |
| 32 of 33 vulnerabilities passed review | Preprint, March 2026, 33 CVEs across 20 projects. | Not peer-reviewed. The mechanism carries even if the number moves. |
| Fewer unreviewed PRs, fewer security bugs | 3.126 projects, nearly 400.000 pull requests, PROMISE 2017. | Association, open source only. Effect called small but significant. |
| 2,6× more likely worst performers | Google's DORA (DevOps Research and Assessment), 2019. | Correlation across survey respondents. |
| >90% of riskiest changes approved | UK FCA multi-firm review, 23 firms, over a million changes, 2021. | Major changes are selected into board review for being risky. |
| Close time 6 h → 8 h after turning a reviewer on | One company, 4.335 pull requests, ICSE 2025 industry track. | One company. |
| Atlassian 75% / 96% / $4 million | Atlassian engineering blog, August 2025. | First-party. A 2026 review finds no proof platforms cause such gains. |
| 60 to 70% of platform initiatives fail | Conference reporting in The New Stack, October 2025. | Industry reporting, not a study. About platforms in general, not review. |

**Visual:** Dense table, not presented. Its job is to be there when a number is challenged, so that the answer is on a slide and not improvised.

## A4 — Names and terms

*Use if the room mixes people who live in the tooling with people who don't.*

| Term | Meaning in this deck |
| --- | --- |
| Four eyes | Three different rules: two persons run a bank, a second person checks a sensitive action, the approving function is independent of the implementing one. |
| DORA (EU) | Digital Operational Resilience Act, EU 2022/2554. Applies to payment institutions since July 2025. |
| DORA (Google) | DevOps Research and Assessment. Google Cloud's research programme on software delivery. Coined "the verification tax" in 2026. |
| RTS | Regulatory Technical Standard. The detailed rules under DORA (EU). 2024/1774 art. 17 is the change-management one. |
| Required approvals, code owners | GitHub branch-protection rules from 2016 and 2017. One more person has to say yes before a merge. |
| Break-glass | A logged override that lets a team bypass a check in an emergency. Cloudflare's reviewer has one; GitHub's org-wide rulesets do not. |
| Tricorder | Google's static-analysis platform. Runs on every change before a human reviewer sees it. |
| Soundcheck | Spotify's platform for running different tiers of checks per kind of component. |
| Self-review | The author reading their own change as a critic would before asking anyone else to. GitHub recommends it. Rust's policy says an LLM review is not a substitute. |
| The author's half of four eyes | My name for a check that asks the author to explain the change in their own words before opening a pull request. A design, not yet a result. |

**Visual:** Glossary table. Not presented.
