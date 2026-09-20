# Ownership and exit: source verification

Researcher: ownership-research agent. All fetches performed **2026-09-20**.

**Method note, read this first.** This document was written in two passes.

*Pass 1 (findings 1-11).* The session's WebSearch budget was fully spent
(200/200), so every result came from direct URL fetching (WebFetch, and `curl`
from Bash). Open-ended discovery worked only by downloading a site's
`sitemap.xml` or `llms.txt` and grepping it. Google, Bing, DuckDuckGo, Brave,
Startpage, Mojeek and every public SearXNG instance returned bot challenges,
403s or 429s. **Absence of a finding in pass 1 is weak evidence.**

*Pass 2 (findings 12-13, and revisions marked **[Pass 2]**).* The budget was
raised and WebSearch worked again. I re-ran Task 4 and Task 3 with search. Task
4 is now confirmed from multiple primary sources; Task 3 now has a clean
per-vendor verdict. Task 2 was re-searched and remains unanswered.

Browser automation was explicitly declined by the team lead and was not used.

---

## Main findings

### 1. The Adyen OpenRewrite post is real, and three details in the brief were wrong

**Source:** first-party company engineering account (Adyen tech blog).
**Canonical URL:** https://www.adyen.com/knowledge-hub/how-we-automated-code-modernization-with-openrewrite
Fetched 2026-09-20 (HTTP 200).

Corrections to the brief:

| Brief said | Actually |
|---|---|
| 22 August 2026 | **20 August 2026.** JSON-LD: `"datePublished":"2026-08-20T17:00:00.000+02:00"`. On-page byline: "August 20th, 2026 · 9 minutes" |
| (title not given) | **"Automating Code Modernization with OpenRewrite"** |
| "orchestrated by an agent" | Accurate, but "agent" means a container orchestrator, **not an LLM** — see finding 2 |

Author line verbatim, confirming the title in the brief:

> Stefano Dalla Palma · Development Tooling Engineer, Adyen

**All five quotes verify verbatim.** Corrections: none.

1. > After approving a dozen near-identical MRs, reviewers may start to pattern-match rather than scrutinize.
2. > a designated person walked through approved MRs before merging to double-check the changes
3. > over 4,000 automated MRs across the codebase, with a steady 70% merge rate, a median review turnaround under two hours
4. > more than 400 unique reviewers
5. > It produces small MRs touching fewer than five files on average.

**Sample/method for the numbers.** All first-party and self-reported; no
external audit, no baseline comparison, no control group. Critically, the brief
omits the time window — the full sentence is:

> In just our first two months, the system quietly produced over 4,000 automated
> MRs across the codebase, with a steady 70% merge rate, a median review
> turnaround under two hours, and a workload that spread naturally across more
> than 400 unique reviewers, so no single engineer was ever overloaded.

So 4,000 MRs / 70% / <2h median / 400+ reviewers are all **first-two-months**
figures. Scale context from the same post: Adyen runs "5,000+ modules."

### 2. The changes are deterministic OpenRewrite recipes, and the post says so explicitly

This is the load-bearing point and it is unusually well evidenced — the post
contains a passage whose entire subject is the deterministic/LLM distinction:

> One human-side footnote: some reviewers encountering our bot for the first
> time assumed it was an AI agent. We saw MRs sit for days because a reviewer
> asked a question and waited for a reply that was never coming. The quick fix
> is a templated response pointing back to a human owner. The broader
> observation is that the "leave a comment and someone will respond" expectation
> is now so deeply embedded in how engineers interact with tooling that a
> **deterministic bot** reads, at first glance, like a conversational one.

Three further confirmations:

- The "agent" is infrastructure, not a model: "The agent runs iteratively in the
  background using Podman on a dedicated VM."
- Recipes are code with ordinary bugs, not probabilistic output: "Recipes are
  code, and like any code they have edge cases." The worked example is a
  static-analysis false positive (`Text.hasText(str.getSomething())`), not a
  hallucination.
- LLM reviewers are named as *separate, third-party* tooling that had to be
  suppressed: "When OpenRewrite MRs triggered secondary AI reviewers or strict
  SonarQube rules on unrelated lines in the same file, reviews stalled. We
  decided to disable auxiliary tooling with specific labels."

**Implication for the essay:** the pattern-matching quote is evidence about
*review-fatigue under repetitive diffs*, and about the *weakest possible*
version of the problem. These diffs were deterministic, mechanically
reviewable, under five files, and 100% human-approved. If reviewers still went
slack here, the same quote cannot be used to argue that an LLM reviewer's
output would be scrutinized more carefully — it argues the opposite, a fortiori.

### 3. Full context around the pattern-matching quote

The quote sits inside "The case for staying small", as a *counter*-argument
against the author's own recommendation. Verbatim, complete paragraph:

> One counterintuitive risk of staying small I observed: the recurring shape of
> recipe-generated diffs can create false familiarity. After approving a dozen
> near-identical MRs, reviewers may start to pattern-match rather than
> scrutinize. The Text migration above is exactly the kind of change where that
> matters: the diff looks routine, but the decision underneath isn't. While
> running the first version of the AnnotateNullableParameter recipe, I saw a
> handful of legitimately faulty annotations slip through in otherwise clean
> batches. Our mitigation was a lightweight meta-review layer: while a recipe
> was still new to our context, a designated person walked through approved MRs
> before merging to double-check the changes. Once we were confident in the
> recipe's behavior, we relaxed that layer.

Four things the essay can use that the brief didn't ask for:

- **The failure was observed, not hypothesized.** "I saw a handful of
  legitimately faulty annotations slip through in otherwise clean batches."
  Faulty `@Nullable` annotations "silently alter the method's contract."
- **The meta-review layer was temporary and confidence-gated**, not permanent:
  "Once we were confident in the recipe's behavior, we relaxed that layer."
  A shared reviewer's human backstop is a *ramp*, not a standing cost.
- **The post ends on the ownership question, unresolved.** This is the single
  most quotable passage for the essay:

  > A few colleagues also raised the question of accountability in a high-stakes
  > engineering environment like ours. Every automated change is reviewed and
  > approved by a human before it merges, but when a bot opens an MR, who
  > actually owns the resulting commit? Is it the engineer who triggered the
  > run, the team that authored the recipe, or the system itself? Each option
  > shapes reviewer behavior and operational scalability differently. I don't
  > think there is a universal answer; it likely depends on the scope of the
  > change and the maturity of the recipe.

- **Centralizing created a new drift problem**, in the author's own words:
  "when a developer defers a suggestion to keep a feature moving, the module's
  compliance state can drift, so a later change to those files may surface a
  suggestion unrelated to that engineer's work — the very situation the system
  is meant to avoid. I don't have a clean answer yet."

### 4. Adyen's CTO: the bottleneck moved to code review, and AI code review is "incremental"

**Source:** first-party company account, and the highest-authority one I found.
**URL:** https://www.adyen.com/knowledge-hub/ai-in-our-development-lifecycle
**Author:** "Tom Adams · Chief Technology Officer, Adyen"
**Date:** on-page byline "September 3rd, 2026"; JSON-LD `datePublished`
`2026-09-04T00:00:00.000+02:00` (one-day discrepancy — cite as early Sept 2026).
Fetched 2026-09-20.

This post was published two weeks after the OpenRewrite one, from the same
company, and it is about exactly the essay's question.

- > Within our teams, the bottleneck has already shifted from code generation to
  > code reviews, as we see an increase in code review turnaround times and
  > pushback per review.
- > Specialized security models and AI code reviews offer nice incremental
  > gains, but a critical piece of the puzzle is still missing: the difference
  > between writing code and evolving systems.
- > Even before AI, review efforts are often not proportional to change risk. A
  > small change could be a typo fix, but could have an unobvious security
  > critical or high blast radius impact.
- **Their answer is not a shared reviewer — it's a shared risk router:**
  > To address this, we're currently piloting a risk tagging system. It uses AI
  > to evaluate change risk behind every merge request. It tags every request
  > with a classification (low, mid, high, unknown) based on explicit criteria
  > around fault likelihood, critical-flow impact, security, behaviour change,
  > reversibility, rollout safety, and other repository-specific criteria. This
  > informs both authors and reviewers, and helps engineers focus their time and
  > effort.
- > we continue to believe in human–in-the-loop, and human focus remains
  > critical for quality control. More code changes will lead to more context
  > switching and less discussions in code reviews. This is a net increase in risk.

**Numbers** (all first-party, self-reported, no external audit):
~1,400 developers; ~57 million lines of code; "AI adoption is effectively 100%
across engineering"; "Merge requests per developer are up 48%"; "Self-reported
time savings, measured via DX surveys, are 15%"; "heavy AI users produce 2x more
merge requests than other engineers of the same seniority level" — which Adyen
itself flags: "This is a noisy and perhaps distracting proxy metric."

Note the honesty worth mirroring: MRs per developer up 48%, but time saved only
15%, self-reported. Adyen does not claim the 48% is value.

### 5. Ownership evidence: a central DX team plus a federated champions network

Same CTO post. This is the only explicit statement of *who owns it* that I could
verify anywhere:

> To scale this expertise, we formed an AI Champions group of 40 expert users
> across our organization. They translate general AI capabilities into concrete
> workflows tailored to their product areas, while closing the feedback loop
> with our **AI-focused developer experience team** by surfacing friction.

So Adyen's model is neither "each team" nor "one central function" — it is a
central platform/DX team plus 40 embedded translators. The OpenRewrite work sits
in the same place: the author "joined Adyen's internal developer platform team",
and the acknowledgments credit "the Build Optimization and Automated Testing
(BOAT) team" and "the CI/CD team".

Also an exit data point hiding in this post: Adyen **built and then moved off**
its own internal AI reviewer.

> We built Codyen, an IDE extension that assisted with explaining code, writing
> tests, code reviews, and doc writing, powered by our internal GenAI inference
> infrastructure. This work was pre-agents [...] Since then, we have switched to
> using a combination of buy, build, and open-source tooling.

And a governance-cost finding that bears directly on "what a shared thing costs":

> Initially, having monorepos made discovering and sharing resources (like
> skills, subagents, hooks, commands, etc) easy. This helped kickstart and adopt
> these patterns. Later on, this turned into a pollution problem of too many
> resources being shared with little governance. This slowed down workflows and
> wasted tokens. To address this we built an Agent Marketplace [...]

### 6. GitHub: there is NO repository-level opt-out from an org or enterprise ruleset (Task 4)

**Answer: No.** **[Pass 2: re-verified with search. The answer holds.]**

The lead's draft sentence — "It doesn't document how a single repository turns
it off" — is **accurate as written**. Keep it.

**Source:** vendor documentation (GitHub Docs). Fetched 2026-09-20.
- https://docs.github.com/en/copilot/how-tos/agents/copilot-code-review/configure-automatic-review
- https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets

Automatic Copilot review is enabled by a branch ruleset rule, "Automatically
request Copilot code review", which can be created at repository, organization,
or enterprise level. The docs describe **no mechanism for a repository to
decline** an org- or enterprise-level ruleset. The governing quote is the rule
layering rule:

> A ruleset does not have a priority. Instead, if multiple rulesets target the
> same branch or tag in a repository, the rules in each of these rulesets are
> aggregated. If the same rule is defined in different ways across the
> aggregated rulesets, the most restrictive version of the rule applies.

Aggregation plus most-restrictive-wins means a repo cannot subtract a rule its
org imposed. The only escapes both belong to **whoever writes the ruleset**, not
to the repo:

- **Exclusion patterns**, set by the org admin: "Under 'Target repositories,'
  click Add target and choose either Include by pattern or Exclude by pattern
  [...] Exclusion patterns are applied after inclusion patterns."
- **Bypass permissions**, granted by the ruleset author: "When you create a
  ruleset, you can allow certain users to bypass the rules in the ruleset."

Note the asymmetry the essay can use: GitHub gives repos granular control over
whether Copilot's *approval* counts ("Let repositories decide"), but gives them
**no equivalent control over whether Copilot reviews at all**. Delegation exists
for the approval, not for the check.

**[Pass 2] Three further confirmations, all fetched 2026-09-20:**

1. **The docs page has no "disabling" section at all.** Its table of contents is
   four entries, every one about enabling: "Configuring automatic code review
   for your own pull requests / for a repository / for repositories in an
   organization / for an enterprise". The only occurrences of "Disabled" on the
   page are `Disabled everywhere`, and both refer to Copilot **approvals**, not
   reviews. Verified across all three URL aliases GitHub serves for this page
   (`/how-tos/agents/copilot-code-review/configure-automatic-review`,
   `/how-tos/copilot-on-github/set-up-copilot/configure-automatic-review`,
   `/how-tos/copilot-on-github/set-up-copilot/configure-code-review` — byte-identical, 23,909 bytes each).

2. **Policy inheritance is explicitly one-directional and most-restrictive.**
   From https://docs.github.com/en/copilot/concepts/agents/code-review :
   > Once this policy is set at the enterprise level, it becomes visible, but
   > not editable at the organization level.
   >
   > The policy is most restrictive. Copilot code review is only available in
   > repositories under an organization where you have explicitly enabled the policy.

   Note this cuts one way only: the enterprise can switch it *off* for everyone
   below, but nobody below can switch it off for themselves.

3. **Practitioners cannot find an opt-out either**, which is circumstantial but
   consistent. GitHub Community discussion #202544 (21 July 2026): "I'd like to
   disable Copilot for this repository but can't figure out how. There's
   documentation on how to enable automatic Copilot reviews for a repo but I
   can't figure out how to disable them for a repo." A responder suggested
   "Repository Settings → Copilot → Code Review"; **the questioner confirmed
   that setting did not exist**, and the thread closed with no definitive
   answer. Source: forum discussion, not documentation — use as colour, not
   proof. https://github.com/orgs/community/discussions/202544

**Bonus, same page, relevant to approval mechanics:**

> Require an additional approval for unattributed Copilot pull requests is
> enabled by default, for both new and existing rulesets. When Copilot opens a
> pull request that isn't attributed to a person, the ruleset requires one more
> approval than the number you configured.
>
> — https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets

### 7. Opt-out contrast: Cursor Bugbot documents a per-engineer override, GitHub does not

**Source:** vendor documentation. https://cursor.com/docs/bugbot.md, fetched 2026-09-20.

Under "Enterprise", after stating that an admin enables Bugbot per repository and
"Bugbot runs for all contributors to enabled repositories, regardless of team
membership":

> **Personal settings**
> Enterprise users can override settings for their own PRs:
> - Run **only when mentioned** by commenting `cursor review` or `bugbot run`
> - Run **only once** per PR, skipping subsequent commits
> - **Enable reviews on draft PRs** to include draft pull requests in automatic reviews

So an individual engineer under a centrally-mandated Bugbot can demote it from
automatic to on-demand for their own PRs. This is the closest thing I found to a
documented opt-out from a central reviewer, and it is the direct counterexample
to GitHub's ruleset model. Two vendors, two opposite answers to "can the person
being checked turn the check off?"

Also note Bugbot's check is **advisory by default**: "Requiring the status alone
does not block merges on findings because findings default to `neutral`."

### 8. Exit (Task 3): no vendor exports the review comments. Six checked, six No's

**CodeRabbit** is the only vendor of the six with a documented, first-class
export — and it is worth reading closely, because it exports two *different*
things with very different portability.

*Metrics export* — https://docs.coderabbit.ai/guides/data-export.md (fetched 2026-09-20):
Dashboard CSV, per-PR rows, date range capped at "Custom range (within the last
1 year)", **"Maximum rows | 10,000"**, with larger exports requiring the
Enterprise-only Metrics Data API. Fields are counts, not comment text:
`total_coderabbit_comments_posted`, `total_coderabbit_comments_accepted`,
severity and category breakdowns, `first_human_review_at`, `merged_at`,
`estimated_review_minutes`. Note the retention floor: "Severity and category
data is only available for pull requests reviewed on or after October 10, 2025."

*Learned-context export* — https://docs.coderabbit.ai/knowledge-base/learnings.md
(fetched 2026-09-20). This is the lock-in surface, and CodeRabbit addresses it
head-on under a heading literally called "Export and transfer learnings":

> You can export your organization's learnings and import them into another
> CodeRabbit account. This is useful when migrating accounts or consolidating
> organizations.

> The CSV file contains all your learnings with their associated metadata,
> including the repository, file path, usage count, last date edited, last date
> used, date created, and learning text.

Two constraints the essay should not miss. First, the import path is
**CodeRabbit-to-CodeRabbit only** — the documented procedure is to commit the
CSV to a branch, open a PR, and comment
`@coderabbitai import file my_learnings.csv as Learnings data for future use`.
There is no documented path into a competitor. Second, the export is lossy by
design: "Exported learning text reflects any applied redaction markers rather
than the original secrets."

**[Pass 2] Per-vendor verdict.** The lead asked for a clear yes/no per vendor on
whether **AI review comment history** is exportable. All docs fetched
2026-09-20. All are vendor documentation unless noted.

| Vendor | Comment history exportable? | What exists instead |
|---|---|---|
| **CodeRabbit** | **No** — metrics only | Dashboard CSV of per-PR *counts* (comments posted/accepted by severity and category), capped at 10,000 rows and 1 year. Plus a separate CSV export of "learnings", importable only back into CodeRabbit |
| **Greptile** | **No** | Analytics dashboard only: "Click **Export** to download the current analytics data." Format unstated. Covers PRs reviewed, merge time, addressed rate, critical bugs, upvote/downvote. The learned memory and auto-generated rules have **no documented export at all** |
| **Cursor Bugbot** | **No** — metrics only | Enterprise API `GET /analytics/team/bugbot-reviews`, `read:*` scope: "the reviewed commit, findings count, billed cost, and per-finding resolution data" |
| **Graphite** | **No** | Nothing. The Insights page documents filters and time periods but no export control. No export/portability page anywhere in the docs index |
| **Qodo** | **No** — and arguably nothing to export | Qodo advertises zero data retention for hosted Qodo Merge: code and PR data are not stored. If true, there is no retained review history on the vendor side to take with you. *Not independently verified beyond Qodo's own materials — treat as a vendor claim* |
| **GitHub Copilot** | **No** — telemetry only | Copilot usage metrics API returns downloadable NDJSON reports via signed URLs, including `used_copilot_code_review_active` / `_passive` per user per day, and repo-level reports with "one record per repository with pull request activity for the day, including pull requests created by Copilot cloud agent and reviewed by Copilot code review." Engagement telemetry, not comment text |

Sources, in order: docs.coderabbit.ai/guides/data-export.md and
/knowledge-base/learnings.md; greptile.com/docs/analytics.md and
/docs/how-greptile-works/memory-and-learning.md; cursor.com/docs/bugbot.md;
graphite.dev/docs/insights.md and /docs/ai-privacy-and-security.md;
docs.qodo.ai/llms.txt and qodo-merge-docs.qodo.ai;
docs.github.com/en/copilot/reference/copilot-usage-metrics/copilot-usage-metrics.

**So: six vendors, six No's.** Not one of them documents a way to export the
review comments themselves. Every export on offer is a metrics or telemetry
by-product.

One sharp detail for the essay. Greptile markets a page titled "The independent
code validator" (greptile.com/independence.md, vendor marketing) — but
"independence" there means independence *from coding agents and model
providers*: "Agent agnostic. Some devs like Codex, some Cursor, others Claude."
It says nothing about the customer's independence from Greptile. The word is
doing the opposite of the work a buyer would hope.

**The structural point that matters more than any of these.** Every one of these
tools posts its findings as native pull-request review comments in the git host.
GitHub's REST API exposes those independently of the vendor — "List review
comments in a repository [...] Lists review comments for all pull requests in a
repository"
(https://docs.github.com/en/rest/pulls/comments, fetched 2026-09-20). So the
*comment history* is not where lock-in lives; it is already in your own
forge and you can walk with it. Lock-in lives in the accumulated, tool-specific
learned context — CodeRabbit's "learnings", the thing it exports only to itself.
That reframes the exit cost in the essay: you do not lose the record, you lose
the tuning.

### 9. Closest comparable: Grab, central team, model-generated MRs across the fleet

**Source:** first-party company account.
**URL:** https://engineering.grab.com/scaling-out-distroless-adoption-with-ai
Date: sitemap `lastmod` 2026-06-22; **no publication date or byline was visible
on the page itself** — treat the date as approximate.

Useful as the LLM-based mirror image of Adyen's deterministic system: a central
team driving automated MRs across many repos, but with model-generated changes.

> Human-in-the-loop: Every MR is a draft: a human reviews before anything
> merges. Humans also decide which learnings become permanent knowledge. The
> agent proposes; people approve.

And the honest non-number, which is worth contrasting against Adyen's specificity:

> The campaign moved the needle across our service fleet: overall distroless
> adoption within our scope has grown substantially since we began using AI to
> drive the work.

No baseline, no percentage, no time window.

### 10. Dropbox: agents produce 1 in 12 PRs, and the bottleneck moved downstream

**Source:** first-party company account.
**URL:** https://dropbox.tech/culture/beyond-code-generation-rethinking-engineering-productivity-in-the-age-of-ai-agents
**Author:** Kazuaki Okumura. **Date:** May 28, 2026. Fetched 2026-09-20.

> Nova is already producing meaningful output, accounting for roughly 1 in 12
> pull requests at Dropbox today, with adoption continuing to grow.

> As code generation accelerates, the constraints shift downstream into review,
> validation, testing, release coordination, and production operations.

> We track signals such as code review turnaround time, first-run test pass
> rate, defect ratio, and rework rate to understand whether increased output is
> holding up under real-world conditions.

Independent corroboration of Adyen's "the bottleneck moved to review" claim,
from a different company, different stack, three months earlier. Both
first-party and self-reported; neither is measured by a third party.

### 11. Stack Overflow 2025: developers distrust AI output more than they trust it

**Source:** survey. https://survey.stackoverflow.co/2025/ai, fetched 2026-09-20.
**Sample and method:** "49,009 responses from 177 countries are used in these
survey results", fielded May 29 – June 23, 2025. **Self-selected, not
probability-sampled** — respondents "were recruited primarily through channels
owned by Stack Overflow", which the methodology page concedes biases toward
highly-engaged Stack Overflow users. Treat as directional only.
(https://survey.stackoverflow.co/2025/methodology)

> More developers actively distrust the accuracy of AI tools (46%) than trust it
> (33%), and only a fraction (3%) report "highly trusting" the output.
> Experienced developers are the most cautious, with the lowest "highly trust"
> rate (2.6%) and the highest "highly distrust" rate (20%), indicating a
> widespread need for human verification for those in roles with accountability.

This survey contains **no ownership breakdown** — nothing on which function owns
an AI reviewer. It measures trust, not org design.

### 12. [Pass 2] No first-party account of switching or switching off — searched properly, still not found

With search restored I ran targeted queries for organisations switching AI code
review vendors, turning one off, or being unable to opt out of a mandated one.
**Every result was vendor marketing or SEO content, not a first-party account.**
Queries run 2026-09-20: `"we switched from" CodeRabbit OR Greptile OR "Copilot
code review" to another AI code review tool engineering blog experience`;
`"turned off" OR "disabled" AI code review tool "too noisy" engineering team
rollout retrospective 2026`; `site:news.ycombinator.com AI code review tool we
disabled it team opt out mandated`.

What came back was comparison-bait ("Greptile vs CodeRabbit", "Best AI Code
Review Tools 2026") from getpanto.ai, levelop.dev, wetheflywheel.com,
macroscope.com, codeant.ai and similar. **I am not citing any of it.** None is
a first-party account; several are published by competing vendors about each
other.

The one thing worth recording, clearly labelled: Greptile — a vendor in this
category — published a post titled **"There is an AI code review bubble"**
(https://www.greptile.com/blog/ai-code-review-bubble, **vendor blog**). The
Hacker News thread on it (https://news.ycombinator.com/item?id=46766961) carries
practitioner comments, of which the most relevant is `zmmmmm`: "I'm mostly using
this selectively so far, and I wouldn't want it turned on by default for every
PR." **Anonymous forum comment — weak evidence, usable only as colour.** I could
not reliably establish the thread's date; the page reported roughly seven months
before 2026-09-20, so approximately February 2026, but I did not confirm this.

### 13. [Pass 2] Qodo documents per-scope review exclusion

Relevant to the opt-out question, alongside GitHub (no opt-out, finding 6) and
Cursor (per-engineer opt-out, finding 7). From the Qodo code review
documentation (https://qodo-merge-docs.qodo.ai/, fetched 2026-09-20), listed
among review controls:

> Ignore content from analysis: Exclude files, branches, or PRs from review.

So three vendors, three different answers to "who may decline the check": GitHub
— nobody below the ruleset author; Cursor — any individual engineer, for their
own PRs; Qodo — anyone who can edit the config, at file, branch or PR
granularity. The question the essay asks has no settled industry answer, and
that is itself the finding.

---

## What I could not verify

**No survey anywhere states which function owns the AI code reviewer.** This was
Task 2's core ask and I could not satisfy it, in either pass. **[Pass 2]** I
re-searched with `platform team owns AI code review rollout "developer
productivity team" enterprise who owns 2026` and got only vendor blogs
(qodo.ai, pensero.ai, codeant.ai, nimbalyst.com) and dev.to SEO posts. Nothing
citable. The only verified ownership statement I have anywhere is Adyen's, in
finding 5 — a single company, first-party, n=1. Specifically:

- **GitLab 2026 Global DevSecOps Survey** — the landing page
  (https://about.gitlab.com/developer-survey/, fetched 2026-09-20) confirms the
  survey exists and gives the sample: "surveying 3,266 DevSecOps professionals
  across the world and various industries", 9th annual. **The report itself is
  gated behind a lead-capture form and I could not retrieve it.** I grepped
  GitLab's full blog sitemap (`https://about.gitlab.com/blog.xml`) for every
  survey/report post and read the two candidates
  (`gitlab-global-devsecops-ai-report`, `devsecops-survey-released`); neither
  contains an ownership breakdown. **I cannot confirm the report contains one.**
  Getting this needs either a form submission or a search engine.
- **DORA 2025** — the landing page loads
  (https://dora.dev/research/2025/dora-report/) but the report is a PDF gated at
  `cloud.google.com/resources/content/dora-roi-of-ai-assisted-software-development`.
  No PDF link is present in the page HTML. Not retrieved.
- **Stack Overflow 2025** — retrieved and read; contains no ownership data (see
  finding 11).
- **LeadDev, InfoQ, Gartner, Forrester, Atlassian, Pluralsight, platform
  engineering community reports** — not attempted. Each needs a search engine to
  locate the relevant article, and none has a greppable sitemap I could guess at.

**No account of any organisation switching AI code review vendors or turning one
off.** Not found, and **[Pass 2]** still not found with search working — see
finding 12 for the exact queries and why I rejected everything they returned.
Task 3's central question is unanswered. I searched: the six vendors' full
documentation indexes (`llms.txt` / sitemap) for migration and offboarding
content; the engineering blog sitemaps listed below; and three targeted web
searches. My read is that this account may simply not exist in public yet — the
category is young enough that few organisations have completed a full
adopt-then-leave cycle, and those that have have no incentive to publish it.
**Do not let the essay imply such an account exists.**

**No account of a team being unable to opt out of a mandated reviewer.** I
established the *mechanism* for both outcomes (GitHub: no opt-out, finding 6;
Cursor: documented opt-out, finding 7), but found no first-hand account of
anyone living with either.

**Engineering blogs checked and found empty** on org-wide AI code reviewer
rollouts: Shopify, Zalando, Klarna, Dropbox, Canva, Grab, Nubank — sitemaps
downloaded and grepped for code-review and AI terms on 2026-09-20. Blogs I
could not reach at all: **Monzo** (404 on sitemap), **Spotify** (404),
**Booking** (404), **Delivery Hero** (403), **Wise** (Medium, 403), **Revolut**
(403), **Uber** (406). **N26** not attempted. Absence here is especially weak
evidence — several of these were unreachable rather than searched.

**Greptile's docs host** (`docs.greptile.com`) did not resolve; I used
`www.greptile.com/llms.txt` instead, which indexes the same content. If Greptile
keeps an export page off that index, I would have missed it.

**Adyen's OpenRewrite post: the figures are unaudited.** Every number in
findings 1 and 4 is self-reported by Adyen with no external verification, no
control group, and no pre/post baseline. The 70% merge rate in particular has no
stated comparison — we do not know Adyen's merge rate for ordinary human MRs, so
"70%" cannot be read as good or bad.
