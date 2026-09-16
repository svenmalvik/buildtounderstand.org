# Machine approval, and the two responses to the queue

**Question this document answers:** Has anyone actually removed the human from the approval of a code change, and what did organisations under pressure do instead?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 02, "Restrict the Input, or Relax the Gate" and "The Approval Became a Setting"

**Last updated:** 2026-09-16

Scope: what the record shows about removing or keeping human approval. This complements the capacity and growth evidence in the `vce-context` worktree at `research/pull-request-origins/ai-pull-request-growth-and-review-capacity-2026.md`, which has a 14 September 2026 cutoff and covers volume, the three failure modes, and automated review evidence.

## Main findings

**Nobody found has publicly removed a mandatory human approval, but the platform removed the requirement that the approver be human.** On 1 September 2026, GitHub shipped a setting under which an automated reviewer's approval satisfies a repository's required-approvals rule. The question chapter 01 leaves open, whether the approving function must be a person, was answered in practice by a configuration toggle rather than by a policy decision.

**Every named organisation in the record kept the human approver.** Including one licensed bank. Where throughput improved, the published explanation is better preparation and queueing, not a removed approver.

**The precedent for merging without a human already existed, in dependency updates.** Auto-merge for machine-generated dependency changes is long-standing and openly documented, and the substitute control offered by the platform's own guidance is the test suite. No incident attributable to it was found.

## The setting, verified directly

The research agent that found this flagged its own quotes as needing confirmation, so both pages were fetched and read directly on 16 September 2026.

GitHub changelog, "Copilot code review can now approve pull requests", dated 1 September 2026:

> "Copilot can submit an approval that counts toward the repository's required-approvals rule."

> "By default, Copilot will not approve pull requests."

> "If new commits are pushed after Copilot approves, its approval is dismissed just like a human reviewer's, and you can request a new review from Copilot to get a fresh approval."

Admin control exists at three levels, enterprise, organisation, and repository, and a repository admin can "choose which file paths Copilot is allowed to approve".

The documentation carries it as two separate toggles:

> "Allow Copilot to approve pull requests: Toggle on to let Copilot submit approving reviews."

> "Allow Copilot approvals to count toward merge requirements: Toggle on so Copilot approvals can satisfy pull request approval requirements."

The enterprise-level default is "Disabled everywhere (default)", and the docs state: "Copilot approvals are in public preview and subject to change."

Two things neither page says. Neither states that human review is still required. And neither frames the change as a governance question.

One line in the changelog needs care before quoting: "An approval assessment alone does not count toward merge requirements." Read in context this appears to distinguish an assessment of whether Copilot would approve from an actual submitted approval, but the pages do not define the distinction. Do not quote that sentence without resolving what "approval assessment" means, because it reads as a contradiction of the headline quote.

`GitLab` is unclear by comparison. Its approval rules documentation says nothing about bots or service accounts approving. It does say that "Merge request authors do not count as eligible approvers on their own merge requests by default".

## Who kept the human approver

| Organisation | Date | Status | Evidence |
| --- | --- | --- | --- |
| Shopify | 2 Sep 2026 | RETAINED | "Owners supply product context, accept risk, review, and merge." |
| Monzo, a licensed UK bank | 13 Aug 2026 | RETAINED | "An engineer still reviews and merges, but the bottleneck moves from 'find an engineer with capacity' to 'find a reviewer'." |
| Ericsson | 14 Sep 2026 | RETAINED | Agent-generated issues "were then manually validated by the developers of the case company". |
| Atlassian (RovoDev) | Jan 2026 | RETAINED | Peer review described as mandatory in the studied environment. |
| Cloudflare | 20 Apr 2026 | RETAINED | Explicitly "not a replacement for human review". |
| Anthropic | 9 Mar 2026 | RETAINED | Human approval explicitly retained. |

The Monzo sentence is the most useful in the set for the chapter. A regulated bank reports that automation moved the bottleneck onto review rather than removing it, which is the capacity argument stated by a practitioner rather than by a vendor.

The Shopify account is useful for a different reason. Its reported gains, an open-issue backlog down about 70 per cent in eleven days and security changes merging at about 80 per cent where previously about 10 per cent did, are attributed to preparation and a freshness-gated merge queue. That is evidence that large throughput gains are available without touching the approver, which weakens any argument that the approver is the only thing standing in the way.

## The existing precedent: dependency auto-merge

Renovate's configuration documentation:

> "By default, Renovate raises PRs but leaves them to someone or something else to merge them. By configuring this setting, you allow Renovate to automerge PRs or even branches."

Its stated risk concerns tests rather than the absent human: "If you don't select any status check, and you use platform automerge, then GitHub might automerge PRs with failing tests!"

GitHub's own Dependabot guidance shows a worked auto-merge example scoped to patch updates and advises enabling required status checks. It gives no warning about merging without human review and no recommendation to require review for major version changes. So the substitute control published by the platform is the test suite.

The OpenSSF npm best practices guide assumes review without requiring it: "These tools submit merge requests that you may review and merge into the default branch."

This matters for the chapter because it shows the second pair of eyes was already optional for a whole class of machine-generated changes, years before the approval toggle existed, and that the industry treated the test suite as the compensating control.

## What was not found

Stated as absences, with the method's limit attached. The research pass had no web search budget left and worked by direct fetches of named primary sources, so these are "not found by direct fetch", not proof of non-existence.

- **No named organisation publicly removing a mandatory human approval.** Nothing found for Netflix, Stripe, Uber, Google, Meta, Amazon, Spotify, Booking, Klarna, Revolut, or Wise. Google's public code review guide mandates nothing about approval and never mentions AI or agents.
- **No published account of anyone switching on the new approval toggles.** The capability is documented; adoption is not. Do not imply anyone is using it.
- **No reversal.** No organisation found restoring human review after removing it. Given no adoption announcement exists either, this absence carries little information.
- **Nothing from Nordic or European banks and payment firms** on approving AI-generated code, beyond Monzo in the UK. Nothing from DNB, Nordea, Klarna, Revolut, or Wise.
- **No incident attributable to dependency auto-merge.**

## A source to avoid

A Hacker News submission dated 7 April 2026, titled "58% of PRs in our largest monorepo merge without human review", points to a Vercel blog URL that returns HTTP 404. The submission had 2 points. Either the post never existed or it was withdrawn. This is exactly the headline the chapter would want and exactly the kind it cannot use. Recorded here so it does not get picked up later from a search snippet.

## Confidence and gaps

| Claim | Assessment |
| --- | --- |
| Machine approval can satisfy a required-approvals rule as of 1 Sep 2026 | High. Changelog and documentation both read directly on 16 Sep 2026. |
| The feature defaults to off and is in public preview | High. Quoted from the documentation. |
| Anyone is actually using it | Unknown. No published account found. |
| Every named organisation in the record retained human approval | High for the organisations listed, which is not a sample of the industry. |
| No organisation has removed mandatory human approval | Weak as a negative. Direct-fetch method with no search budget; absence of evidence. |
| Dependency auto-merge is an accepted practice without human review | High. Vendor and platform documentation describe and support it. |
| The "58%" monorepo claim | Unusable. Target URL returns 404. |
| What "approval assessment" means in the changelog | Unresolved. Resolve before quoting that sentence. |

## Related documents

- `ai-pull-request-growth-and-review-capacity-2026.md` in the `vce-context` worktree, for volume, capacity, and the three failure modes.
- [`../20260915-where-did-the-second-pair-of-eyes-come-from/functions-versus-persons.md`](../20260915-where-did-the-second-pair-of-eyes-come-from/functions-versus-persons.md), which establishes that no rule found requires a human approver. Read together with this note, the regulation left the door open and the platform walked through it.
