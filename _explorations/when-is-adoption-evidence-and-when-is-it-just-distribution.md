---
title: When Is Adoption Evidence, and When Is It Just Distribution?
date: 2026-08-24
excerpt: Under exploration.
published: false
---

<!--
DRAFT. Prose written in the writing-style voice. Not published.

Follow-up to: what-is-the-smallest-ai-platform-that-could-possibly-work.md
Answers the question that piece ended on (:256): how a contract that nobody
asked for reaches its first team.

Open items before publishing:
1. AI Playground usage number. It is load-bearing in chapter 02. Get it, or
   keep the sentence that says it doesn't exist. The absence is a finding,
   but it can't be silent.
2. Confirm what may be said publicly about the centralized PR review
   discussion. Written here to the limit the record supports: a wish on the
   table, ownership unclear, not my decision, and I built the tool someone
   would centralize with.
3. Decide whether Prototype 0.3 runs before publishing. next-steps.md:157
   says no second experiment before 1 October. If it runs, the piece
   publishes with a number. If not, it publishes as a design.
4. The outreach in chapter 01 does not name the person. Keep it that way
   unless he agrees to be named.

Verified citation corrections to respect:
- Cross-product AI review is 18.2% of reviewed agent PRs (45,269/248,641).
  The 1.6% figure uses a much wider denominator. Do not bind them together.
- The ESEM study does not show same-vendor degradation. Do not cite it that way.
- A2A v1.0.1 was published 28 May 2026.
- GitLab's 85% is a Harris Poll of 1,528 respondents. Perception, not telemetry.

Research collected but deliberately kept out of the prose, to protect
readability. Available if a section needs more weight:
- Zhong et al. (14 July 2026), 1.02m PRs across 207 projects: agent
  involvement associated with faster decisions, not better review quality.
- Zhong et al. (16 March 2026): human suggestions adopted 39.9 percentage
  points more often than agent suggestions; 28.7% of unadopted AI
  suggestions were incorrect.
- Zahavi (1975), the handicap principle, behind the costly signal argument.
- Samuelson (1938), revealed preference, behind the same argument.
- Wang et al. (2026): SBOM cross-tool package detection consistency
  7.84% to 12.77%.
- EU AI Omnibus, Regulation (EU) 2026/1744, in force 27 July 2026. Annex III
  high risk moved to 2 December 2027, Annex I to 2 August 2028.
-->

<article class="exploration-article" markdown="1">

<header class="exploration-hero">
  <h1>When Is Adoption Evidence, and When Is It Just Distribution?</h1>
</header>

Three weeks ago I published an agent contract. It is one file with thirteen fields, checked into the repository next to the agent it describes. Since then, several people have read it and told me they like the idea.

No team uses it yet. That isn't a verdict. We simply haven't come that far, and we do intend to use it.

So I have two facts and no evidence. People like the idea, and nothing depends on it yet. I can read the praise as demand, or I can read the silence as disinterest, and today I can defend both readings equally well.

That is uncomfortable, because the last exploration ended by saying I no longer trust the sentence "teams need this" when I am the one saying it. It didn't ask the harder version of the question. Does the sentence become evidence when someone else says it?

What has to cost something before agreement means anything?

I am using the agent contract as the current case. The question is about declarations and shared services in general: service contracts, ADRs, model cards, CODEOWNERS files, internal platforms, anything a team is invited to adopt.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">01</span>
  <div>
    <h2 id="what-did-the-praise-actually-measure">What Did the Praise Actually Measure?</h2>
  </div>
</div>

Praise can measure several things. It can mean the reader understood the idea, that the idea sounds reasonable, or that they would like it to exist. None of those is the thing I need to know. I need to know whether the contract beat the work, the risk, and the coordination that a team already carries.

### What I Asked For, and What Came Back

I made the measurement worse myself. When I wrote to people about the contract, I sent the article and my question in the same message. I explained the idea, then asked what they thought of it. The answers came back using the words I had supplied.

My own note on it, written after I read the replies: counting a phrase I supplied as evidence that I was right is the Manifold error with better manners.

Manifold was the six months I spent building an AI coding IDE that nobody needed, because I treated my own conviction as evidence of demand. This is the same error wearing a costume. I didn't supply the conviction this time. I supplied the vocabulary, and then read the vocabulary coming back as agreement.

That is worse for me than being wrong. If the replies had said the idea was useless, I would have learned something. Instead I built a question that couldn't return bad news, and then felt encouraged by it.

### Why Stated Preference Is Weak, Not False

The people who answered me weren't wrong or careless. They answered the question I asked, and the question was cheap.

This is measured, and the size of the gap is useful. A meta-analysis of 28 studies (Murphy et al., 2005) found hypothetical valuations ran about 1.35 times higher than real ones, with a long tail of much worse cases. A review of intention research (Sheeran, 2002) found that stated intentions explain roughly 28% of what people later do. Both numbers say the same thing. Stated preference is a weak signal, not a false one.

Rob Fitzpatrick's *The Mom Test* turns this into a practical rule: ask about past behaviour, existing workarounds, and money already spent, and never ask whether someone likes the idea. I asked whether people liked the idea.

### What the Praise Could Not Tell Me

There are two separate failures here, and I want to keep them apart. The first is that I ran a bad experiment. The second is that the contract may be unwanted. The first one prevents me from concluding the second.

So the honest position at the end of this chapter is not that the contract failed. It is that I have no usable evidence in either direction, which is a worse place to be than being refuted.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">02</span>
  <div>
    <h2 id="is-non-use-a-verdict-or-a-cost">Is Non-Use a Verdict, or a Cost?</h2>
  </div>
</div>

The obvious correction is to stop listening to what people say and watch what they do. I want to be careful with that correction, because it can be wrong in a specific way.

Bernheim and Rangel (2008) describe when observed choice stops describing real preference. It happens under complexity, under passive choice, and when people have little experience with the thing. All three apply to an agent contract that arrived in an article. So "nobody used it" can also mean that using it was expensive, or that nobody was ever in a position to choose.

Expensive how, and for whom? That question turns out to be more productive than the first one.

### What Happens to Small Declarations

The contract is a small, versioned, declarative file that a team is asked to keep true. There are older examples of exactly that shape, and their record is not encouraging.

Architecture decision records are the closest analogue. A study of ADR use in practice (Buchgeher et al., 2023) found low adoption, and that about half of the repositories that did adopt them hold only one to five records. They were tried with real interest, and then left.

Model cards show the same curve at larger scale. A study of Hugging Face (Oreamuno et al., 2024) found documentation present for about 40% of models and under 30% of datasets, with limitations and evaluation the least completed sections. Software bills of materials repeat it again: of 25,882 Java SBOMs examined by JBomAudit (2025), 7,907 omitted direct dependencies they should have listed.

One pattern runs through all three. The fields closest to accountability are the hardest to keep true. Purpose and name survive. Ownership, evaluation, and limitations decay.

My contract has thirteen fields. I'll predict now which ones rot first, so the prediction can be checked later: `owner`, `incident_contact`, and `disable`. They are the three fields that create an obligation for a named human.

### Two Systems I Built, One Chosen

I have two of my own systems that speak to this, and they disagree.

Vippsi was a Slack app I built in about two weeks. It grew to roughly 250 daily active users and deferred a seven-figure purchase in NOK for about a year. Nobody was told to use it.

The AI Playground was delivered through the internal developer portal and made available to everyone. I can't produce a usage number for it. Not a low number: no number.

Same builder, same organization, same year, opposite outcomes. I can't explain the difference with software quality, and I can't explain it with promotion, because the Playground was the better promoted of the two. I'll come back to it.

### Which Numbers Describe Distribution?

It helps to separate the numbers I can produce from the numbers I would need.

Distribution numbers count how far something was pushed: licences, installations, catalog entries, training attendance, teams covered by a mandate. Chosen-use numbers count what happened after that: activation among eligible teams, repeat use once a mandate is removed, workflows completed without help from the platform team, and how often teams route around the thing.

The industry mostly reports the first kind. DORA's 2024 report found 89% of respondents had an internal developer platform, while also finding that throughput and stability can get worse when a platform is imposed across the delivery lifecycle. That is an association in survey data, not a causal claim, but it does show that coverage and value are different measurements.

Here is the uncomfortable part. Every number I have about my own systems is a distribution number.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">03</span>
  <div>
    <h2 id="what-would-make-agreement-informative">What Would Make Agreement Informative?</h2>
  </div>
</div>

If cheap agreement carries little information, then the fix isn't to collect more agreement. It is to make agreeing cost something.

### What Makes a Signal Costly

This is old ground in economics. Spence (1973) showed that a signal carries information when it's expensive enough that someone without the underlying quality wouldn't send it. Chaudhry and Wald (2022) give the working criteria: a signal is informative when it's difficult to fake, verifiable, and costly to the sender.

Translated to an internal platform, that means three things. The cost has to be paid by the team that would adopt, not by me. It has to be tied to the behaviour I'm claiming exists. And it has to be visible to someone other than the person making the claim.

This rules out most of what I would naturally count. A mandatory field filled in by a junior engineer is not a costly signal from the leader who said the contract was a good idea.

### The Path That Already Exists

The mechanism I had missed is visible in a file most engineers already use. A CODEOWNERS file routes review requests automatically. On its own it changes nothing that anyone has to obey. It becomes consequential only when branch protection makes that approval a condition for merging.

So the declaration isn't what creates the obligation. The path does. A declaration becomes consequential when it sits in a path that people already have to walk.

That explains my two systems without appealing to quality or promotion. `VippsService.yaml` is also a declarative contract, kept accurate by roughly 250 engineers, because deployment went through it. Nobody adopted it out of interest. They kept it true because their deployment failed if they didn't.

Vippsi sat in a conversation people were already having in Slack. The AI Playground sat next to their work, and nothing they already did required passing through it.

My agent contract gates nothing. Nothing depends on it being true, so nothing tells anyone when it isn't.

This changes what I wrote at the end of the last exploration. I ended it on three options for getting the contract to a first team: put it in the template, wait for the pull, or don't build it. All three are ways of moving a file toward teams.

Distribution was never the thing in short supply. I had a distribution plan for a problem that wasn't distribution.

It also changes how I count the value that continues after the initial work. A declaration that gates something keeps producing value, because every team that passes through it leaves accurate information behind. It also keeps producing work, because every team that passes through it can be blocked by it.

The first is the reason to build it. The second is the reason to keep it small, and the reason a team must be able to leave.

### The Live Example: Should Review Be Centralized?

I have a live case, and I want to describe my position in it accurately. At work there is a wish to centralize AI code review using the models we already offer. Ownership of that work is currently unclear, and the decision isn't mine. What I own is that I built the tool someone would centralize with.

The pressure behind the wish is real. A GitLab survey run by Harris Poll in June 2026 (1,528 respondents, so perception rather than telemetry) reported 85% saying review has become the bottleneck. That matches what I see. Generating a change is now cheap, and understanding one is not.

The strongest argument against centralizing isn't cost. Bacchelli and Bird (2013) found that code review at Microsoft delivered less defect finding than teams expected, and much more understanding, knowledge transfer, and awareness of what was changing. Thongtanunam et al. (2016) found that reviewers without domain expertise correlate with post-release defects. When the Godot project stopped accepting autonomous agent contributions in June 2026, it made the practitioner version of the same argument: feedback absorbed by a machine doesn't turn anyone into a future maintainer.

So centralizing review optimizes the part that is visibly slow and quietly removes the part that makes teams capable. That is a risk worth testing, and I want to be careful not to overstate it. No study I found shows that a centrally owned AI reviewer produces worse outcomes than team-chosen tools.

There are two more things I would want on the table before anyone builds it.

The first is a measurement. In an industrial study of 4,335 pull requests (Bosu et al., 2025), AI review comments were resolved 73.8% of the time, while average closure time rose from 5 hours 52 minutes to 8 hours 20 minutes. A tool bought for speed made the pipeline slower.

The second is that one central model is the wrong shape even if centralizing is right. Kang et al. (ICML 2025) found model pairs agreed about 60% of the time when both were wrong, and LLM judges prefer their own output. One reviewer for everything buys consistency, and consistency isn't independence.

In a fintech there is also a rule that outranks the engineering discussion. The DORA delegated regulation requires independence between whoever implements a change and whoever approves it. An agent that writes and an agent that approves is a question compliance will ask before the platform team does.

And there is a number I can finally compute, after two explorations that defined "smallest" partly by total work and never calculated one. Managed AI review is priced around 15 to 25 US dollars per review. At a thousand reviews a month that is 15,000 to 25,000 dollars, before re-runs on every push, and before the people who triage the false positives.

### What I Would Try Before Owning a Review Service

The last exploration proposed an order and never tested it: start with documentation, then a convention, then a template, then a library or a CLI, and build a managed service only when the simpler options can't remove the repeated work. This is the first real decision I can test it against.

For review capacity, the cheaper options are ordinary:

- require disclosure when a change was written by an agent
- limit pull request size
- use CODEOWNERS with required approval, so review lands on people who know the code
- add required checks
- add a merge queue

Most of those are already available to us and unused. That is the cheapest evidence in this whole article, and I haven't collected it. Before I argue about a service nobody owns yet, I should find out whether the options we already have are switched on.

<div class="prototype" markdown="1">
<p class="prototype__label">Prototype 0.3 · counting what agreement turns into</p>

Not another YAML file. The last two prototypes were files nobody had used, which is the kind of evidence I said I no longer trust. This one is a count.

Five steps, each costing the participant more than the one before:

1. reads the article
2. names a real agent they run today
3. generates a contract for it
4. commits that contract to their own repository
5. the contract is still there, and still accurate, after 14 days

Only steps four and five cost anything. The first three are distribution wearing the clothes of adoption.

I want the disconfirming result written down before I run it. With 20 eligible participants, zero completions puts the 95% upper bound near 14%, which is low enough for me to stop. Fewer than 10 participants isn't a result, it's a story.

The test can also fail in its own ways. A participant may not run a suitable agent, or may not have permission to commit to the repository. Both need screening, or I'll be measuring authority instead of demand.

It can also only measure my readers, who selected themselves by reading me. It can't tell me anything about teams at Vipps.

<p class="prototype__caption">The test measures what agreement turns into, not whether people agree.</p>
</div>

## Conclusion

> Agreement becomes evidence at the point where it costs the person something. A declaration earns that cost only when something people already do depends on it being true.

That reframes my own question. I had been asking how to get the contract to a first team, which is a distribution problem. The better question is which existing path the contract could sit in, so that a team keeps it accurate because their own work depends on it.

The smallest honest next step is not to distribute the contract more widely. It is to put one field of it into a path that already exists, and find out whether anyone keeps that one field true.

### What I Don't Know Yet

I don't know whether the AI Playground has users. I built it, I distributed it, and I can't answer the question I'm asking other people to answer.

I don't know whether a declaration that gates something is adopted or merely obeyed, or whether I would be able to tell the difference from inside the team that owns the gate. Compliance is easy to mistake for demand, and I've already made one measurement error in this direction.

And the decision in front of me is still open. I can put one field of the contract into the deployment path we already have, which is cheap and immediate, but the resulting number may only tell me that people follow gates. I can run the counting test on my readers first, which produces a cleaner signal about real demand, but it measures an audience that isn't the organization I work in. Or I can collect the free evidence first and find out which review controls we already own and don't use, which costs almost nothing but answers a smaller question than the one I started with.

The third option is the cheapest and the least interesting, and I notice I want to skip it. Last time I wanted the option that would have produced good numbers that meant nothing, and wanting it was the reason I didn't pick it. I haven't decided yet.

---

If you have introduced a declaration that teams were asked to keep true, whether that's a service contract, a CODEOWNERS file, an ADR, or a model card, I want to know whether anything depended on it being true, and what it cost your teams to keep it true.

What would change my mind is a declaration that gated nothing and stayed accurate anyway. If you have one of those, I would like to know what held it up.

You can write to me at [sven@malvik.de](mailto:sven@malvik.de) or find me on [LinkedIn](https://www.linkedin.com/in/svenmalvik/).
</article>
