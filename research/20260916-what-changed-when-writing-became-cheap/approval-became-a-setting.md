# The approval became a setting

**Question this document answers:** What exactly changed on 1 September 2026 when a machine's approval became able to satisfy a required-approvals rule, and what does the change leave unanswered?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 02, "The Approval Became a Setting"

**Last updated:** 2026-09-19

Scope: platform mechanics and public reaction. The regulatory half is in the chapter 01 note on functions versus persons, which established that no rule found requires the approver to be a person.

## Main findings

**Every rule about who may approve is about role in the change, never about being human.** GitHub bars the author. GitLab bars the author, anyone who added commits, and code owners who contributed. None of them bars a machine. The assumption that a second pair of eyes belongs to a person was never written down by regulators or by vendors.

**The author-cannot-approve rule binds an identity, and the writing agent and the reviewing bot are two different identities.** The cloud agent that opens pull requests is explicitly barred from approving. The reviewer bot is not barred from approving what that agent wrote.

**A human who assigned the work is held to a stricter standard than the machine.** GitHub bars a person from approving a pull request they asked Copilot to produce. No equivalent restriction exists for the machine reviewer.

**There is no audit log event for a machine approval.** You can prove when the setting was enabled. You cannot prove which merges it unblocked.

**Nobody argued about it.** The changelog reached one upvote and no comments.

## What shipped

GitHub changelog, 1 September 2026, "Copilot code review can now approve pull requests":

> "When enabled, Copilot can submit an approval that counts toward the repository's required-approvals rule."

> "By default, Copilot will not approve pull requests."

Documentation:

> "When Copilot approvals are enabled in repository, organization, and enterprise settings, Copilot can submit an approving review that satisfies your repository's required-approval rule the same way a teammate's approval would."

Control exists at enterprise, organisation and repository level, with the enterprise default "Disabled everywhere (default)". Repository admins can "choose which file paths Copilot is allowed to approve". Approvals dismiss on new commits, "just like a human reviewer's". The feature is public preview.

## The ambiguity, resolved

An earlier pass flagged one changelog sentence as unquotable until its meaning was settled. It is now settled, and the distinction is worth the prose.

An **approval assessment** is an opinion written in prose, and it ships with every review whether or not approvals are enabled:

> "Every Copilot code review includes an approval assessment in the overview comment, indicating whether Copilot has determined the pull request ready to approve after reviewing it"

> "On its own, this assessment does not count toward merge requirements."

An **approval** is a submitted review event that satisfies the rule. So the changelog sentence means the opinion in the comment is not a vote. What shipped on 1 September is the vote.

No formal glossary entry or enumerated states list exists. The distinction is drawn only in running prose across several pages.

## Identity, not function

This is the finding the section is built on.

The base rule: "Pull request authors cannot approve their own pull requests."

The rule reaches one hop into humans who delegated the work: "You will also not be able to approve a pull request that was raised by GitHub Copilot if it was you who assigned Copilot to the issue…"

The writing agent is barred from approving: "Copilot cloud agent cannot mark its pull requests as 'Ready for review' and cannot approve or merge a pull request."

But two distinct identities are involved. The reviewer is the bot account `copilot-pull-request-reviewer[bot]`. The author is the cloud agent, which opens pull requests "under its own app identity instead of on behalf of a person". The author-cannot-approve rule binds an identity, and these are not the same identity.

**So the asymmetry is:** a person who told Copilot to do the work cannot approve the result. The machine reviewer has no such restriction. Independence is enforced more strictly against people than against machines.

**One partial mitigation, and it does not close the loop.** A ruleset option, on by default: "When Copilot opens a pull request that isn't attributed to a person, the ruleset requires one more approval than the number you configured." It raises the count. Nothing in the text says the additional approval must come from a human.

**Not verified:** whether the reviewer bot is technically blocked from approving cloud-agent pull requests. The documentation does not say either way, which is itself the finding.

## GitHub's own framing

The cloud agent documentation describes the reviewer as internal to the agent:

> it "gets a second opinion on its code with Copilot code review"

A second opinion on its own code, from the same system. This is the vendor's own description, and it collides directly with the title of the exploration.

## This was already possible, with two caveats

Bot approval is roughly a decade old. The reviews endpoint has accepted three actions since the API entered preview on 14 December 2016: "The review actions include: APPROVE, REQUEST_CHANGES, or COMMENT." Posting a review sits under write access on the repository "Pull requests" permission, which is exactly what a GitHub App installation token carries.

**Caveat one.** A bot cannot satisfy a code owner requirement. The code owners reference lists only users, teams and email addresses, and requires that "Users and teams must have explicit `write` access to the repository." Apps are not eligible owners.

**Caveat two.** No GitHub sentence confirms that an app approval counts toward a numeric required-approvals rule. Branch protection documentation says: "You can require approving reviews from people with write permissions in the repository or from a designated code owner." That says people.

So the honest reading: teams could already wire a bot to approve, but the platform's own language framed required approvals as coming from people. September made it explicit, first-party, and configurable.

## The audit trail: visible live, thin afterwards

**Live**, the approval is identifiable. The API review object carries `user`, documented as "required, any of: **null** or **Simple User**", plus a required `author_association`. The reviewer resolves to the bot login. In the interface, the reviewers sidebar groups approvals by permission level, separating those that count toward merge from those that do not.

**Afterwards, it is not.** No audit log event exists for a Copilot approval. The full enterprise event list contains no approval event for it and no `pull_request_review` family. Only configuration changes are recorded, such as `copilot.cfb_org_settings_changed`.

> You can prove when the toggle was flipped. You cannot prove which merges it unblocked.

**Why this matters for the audience.** Chapter 01 establishes that the change management rules require changes to be recorded and approved, and require independence between approving and implementing functions. A control whose operation leaves no event in the audit log is difficult to evidence to a supervisor, whatever view that supervisor eventually takes of machine approval.

## No independence language anywhere

Not found, and searched for directly. The configuration page documents two toggles, file path globs, and a public preview note. There is no segregation of duties language, no conflict of interest language, no statement about independence.

The nearest thing is advice rather than a control: "Copilot code review should be supplemented with careful human code review."

No GitHub statement about compliance or regulated use of the feature was found, in either direction.

## The documentation contradicts itself

The required-reviews page still carries pre-September wording: "Approvals by GitHub Copilot also appear in this section even though GitHub Copilot reviews do not count toward those requirements."

That contradicts the 1 September changelog. Three weeks after the change, the documentation still tells readers the opposite. Treat that page as partly stale, and note that a team checking the docs rather than the changelog would conclude the feature does not exist.

## Nobody argued about it

The changelog was submitted to Hacker News on 1 September 2026 at 22:48 UTC. **One point, zero comments.**

A search of the full Hacker News comment corpus since that date for "copilot approve", "required approvals" and "bot approval" returns no comment discussing the change. GitHub's own community discussions search returns nothing on it, and the changelog carries no linked discussion thread, which GitHub often attaches to announcements.

**No objection found and no defence found, because no public argument appears to have taken place.**

Scope this claim carefully when writing. The researcher could not run open-web discovery, so the defensible sentence is that nobody argued about it in the venues that could be checked, not that nobody anywhere noticed.

## Every platform restricts by role, not by species

Verified across four platforms. Each disqualifies an approver for their role in the change, never for being a machine.

**GitLab.** Three prohibitions, and that is the complete list: it "Prevents the author of a merge request from approving it", it "Prevents users who add commits to a merge request from also approving it", and "Code owners who commit to a merge request cannot approve it, if the merge request affects files they own." Bot users created for project access tokens "are members of the project" and "are granted permissions that correspond with the role and scope of the associated access token". They are members with roles, and no documented rule excludes them. Permitted by omission, and never discussed. GitLab Duo's merge request documentation makes no claim that it can approve.

**Bitbucket Cloud.** "The author of the pull request (PR) can approve their own PR, but that approval does not count towards the number of approvals needed for the merge check to pass." Nothing about apps or bots. Permitted by omission.

**Azure DevOps**, page dated 15 July 2026. The only identity limits are the author and the last pusher, and the setting names the compliance concept directly: "Select **Prohibit the most recent pusher from approving their own changes** to enforce segregation of duties." Nothing about service accounts or build identities. Permitted by omission.

**Gerrit.** "The label values that a given user is allowed to set are defined according to the access controls". Gerrit assumes machine voting exists, noting that "Some CI tools expect to use the Verified label to vote on a change after running", but that is the Verified label rather than Code-Review. Nothing restricts a Code-Review approval to humans. Permitted by access control, not by species.

The Azure DevOps wording is the most useful for the chapter, because it uses the exact compliance term from chapter 01 and then defines it entirely by role in the change.

This matches what chapter 01 found in the regulation, which speaks of functions rather than persons. Neither the regulators nor the vendors ever wrote down that the second pair of eyes had to be human.

## Confidence and gaps

| Claim | Assessment |
| --- | --- |
| Machine approval can satisfy a required-approvals rule since 1 Sep 2026 | High. Changelog and documentation read directly. |
| An assessment is an opinion and an approval is a vote | High. Both quoted from documentation. |
| The writing agent cannot approve; the reviewing bot is a different identity | High for both halves. Whether the reviewer is technically blocked on agent-authored PRs is **not stated**. |
| A human who assigned the work is barred, the machine is not | High. Quoted from the required-reviews page. |
| Bot approval was already possible via the API | High, roughly a decade. |
| A bot can satisfy a code owner requirement | No. Apps are not eligible code owners. |
| An app approval counts toward a numeric rule | Not stated by GitHub. Branch protection language says "people". |
| No audit log event records a machine approval | High. Full enterprise event list checked. |
| Any independence or segregation guidance exists for the feature | Not found. |
| Nobody publicly objected | Found nothing in Hacker News and GitHub discussions. Could not run open-web discovery, so scope the claim. |
| Any organisation has enabled it publicly | Unverified. Do not imply adoption. |
| Any auditor or regulator has commented | Not found. |

## Related documents

- [`../20260915-where-did-the-second-pair-of-eyes-come-from/functions-versus-persons.md`](../20260915-where-did-the-second-pair-of-eyes-come-from/functions-versus-persons.md), which establishes that no rule found requires a human approver.
- [`machine-approval-and-two-responses.md`](./machine-approval-and-two-responses.md), for the organisations that removed or kept the human approver.
