---
title: What Is the Smallest (AI) Platform That Could Possibly Work?
date: 2026-07-27
excerpt: Under exploration.
published: false
---

# What Is the Smallest (AI) Platform That Could Possibly Work?

## Question

At Vipps, one of the most common requests I see is access to LLMs. Giving an engineer an API key is easy. It solves the immediate access problem. It does not help finance attribute the bill, compliance understand the data flow, or incident response observe the system.

The key is small. The work around it is not.

That difference made me ask two questions. When does recurring work justify a shared platform? If it does, what is the smallest form that platform could take?

I am using AI agents as the current case. By agents, I mean software built with LLMs, skills, and integrations with internal or external tools. The technology is current, but the question underneath it is not: When does a shared system create leverage, and when does it merely centralize work and reduce freedom?

## Exploration

### Chapter 1: What Problem Would a Platform Solve?

Organizations want engineers and non-engineers to build useful agents. As more people try, the same needs begin to appear. Developers need model access, evaluation tools, and a path to deployment. Finance needs cost attribution. Compliance needs control over data flows and audit evidence. Incident response needs a system it can observe.

None of these requests alone justifies an AI platform. One team asking for model access has an access problem. One finance department asking about a bill has an accounting problem. A collection of experiments does not become a platform problem just because the experiments use AI.

I start seeing a platform problem when teams repeatedly need the same access controls, cost attribution, evaluation, observability, or audit evidence. At that point, solving every use case separately creates more work, inconsistent controls, or unnecessary risk.

The number of agents is a poor threshold. A company may have one hundred experiments and no platform problem. The same company may have only two agents in production that handle sensitive data and already need strict controls. The difference is not the number of agents. It is whether a constraint repeats, what happens when it is ignored, and whether a shared capability would remove more work than it creates.

Even then, the answer may be to extend a platform that already exists. I would consider a dedicated AI platform only when existing systems cannot remove the repeated constraint without every team rebuilding the same AI-specific machinery.

I see a version of this with PR review agents. An engineer uses the best available frontier model with extra-high reasoning effort. The agent solves an immediate and obvious problem for the team. It may still ignore the cost of each review, the rules that govern the review, and how another team could learn from the work or build upon it.

The first version works. The organization inherits the second version.

### Can a Platform Help People Build Agents?

An AI platform can help engineers and non-engineers build agents. I use the word "can" because its usefulness depends on the problem it removes, not on how complete the platform looks.

At Vipps, we created an agent template called AI Playground. A builder visits our internal developer portal, clicks a button, and gives the agent a name. This creates a repository with a working agent shell already deployed to the test environment. The builder also receives a starter prompt for a coding agent. The coding agent clones the repository and asks what to do next. From there, the builder can start shaping the agent instead of rebuilding its foundation.

Whether agent creation belongs to an AI platform is partly a matter of definition. The template solves one recurring problem. Non-engineers no longer need an engineer to recreate the same foundation for every agent. Requirements from other stakeholders can also be included in the path, even when the builder does not know about them yet.

The value is not the button in the portal. It is the repeated work that the button removes.

### Chapter 2: When Does Shared Work Become a Platform?

### What Is Actually Repeating?

Repeating work does not always look the same. I have seen two examples often enough to be useful here.

Non-engineers such as analysts and product managers use Claude Code or Codex to build something useful, perhaps a dashboard. It works on their machine. Making it available to others means connecting it to company data and deploying it to the company runtime. At Vipps, services follow a contract that engineers receive through the internal developer portal. Using that contract still requires engineering experience, so the platform team helps each new builder through much of the same work.

The second example is simpler. Engineers build AI-powered Slack apps and ask for an API key to an LLM. The request takes little time, but handing out a key does not provide cost attribution, data controls, evaluation, or useful observability.

The work is not identical. The first example repeats deployment support. The second repeats access without the controls other stakeholders need. Both may be platform candidates.

Repetition is where I start looking. It is not yet a reason to build.

### When Does Repeated Work Justify a Shared Solution?

Teams may repeat work because they are still learning. Centralizing it too early can turn useful experiments into a shared solution nobody needs. I would treat repetition as a meaningful constraint only when it blocks a valuable workflow and produces a visible consequence:

- **Incidents and Recovery:** Does the repeated constraint cause preventable incidents, or make incidents harder to detect, contain, and recover from?
- **Audit Effort:** Does every team have to reconstruct the same evidence differently, and how much effort does that require?
- **Cost:** What does the constraint cost through duplicated implementation, infrastructure consumption, waiting, support, and rework?
- **Reliability:** Do local solutions fail inconsistently, create operational blind spots, or make dependable recovery difficult?
- **Risk:** What are the consequences of getting this work wrong, and how widely could those consequences spread?

There is no useful universal threshold based on the number of teams, agents, models, or requests. Two production agents handling sensitive data may justify shared controls. One hundred experiments may not. The consequences are more important than the count.

### Could the Work Be Removed Instead?

Before I build a shared capability, I should ask whether the workflow or constraint should exist at all. The apparent platform problem may be unclear ownership, missing training, unnecessary variation, a poor procurement choice, or a workflow that should simply be removed.

Calling it a platform problem too early gives the solution a shape before the cause is understood. Platforms are quite capable of standardizing work that nobody needed.

### Could Documentation, Conventions, or Reusable Libraries Be Enough?

My next test is whether a lighter solution removes the constraint. The order is important: documentation, a convention, a template, a library, a CLI, and only then a narrow managed capability.

A small team may need no more than a repository template and a CLI. Expensive or risky concerns such as identity, policy, databases, or audit evidence are stronger candidates for a managed service. The goal is not to build the smallest possible platform department. It is to use the lightest option that completes the work.

### When Does a Shared Capability Become a Platform?

A shared capability becomes platform-like when teams choose it as the common path because it is easier and safer than solving the problem locally.

That choice is important. Adoption by mandate can make a platform common without making it useful.

I am interested in whether the capability removes enough repeated work to justify the work it creates. Someone still has to own and maintain it. If that costs more than the coordination and risk it removes, the platform has not created leverage. It has moved the work.

The first justified AI platform may therefore be a gateway, evaluation service, policy check, trace convention, cost-attribution layer, or deployment contract. It does not need to begin as one broad integrated product labelled as an AI platform.

### Who Does Not Need an AI Platform?

An AI platform is probably premature when there is only one team, few production workflows, or no valuable use case yet. It is also a poor answer when the real problem is skills, data access, or workflow design.

A team must first understand its work well enough to describe the workflow. Only then can it decide what should be automated and what, if anything, should be shared.

A dedicated AI platform also needs clear ownership, support, upgrades, and deprecation. That is an investment, not a side effect.

### When Does a Platform Create More Friction Than It Removes?

I would worry when adoption depends on a mandate, users wait longer than before, or teams keep forking and bypassing the platform. These are not signs that teams need more persuasion. They are signs that the common path may be creating more friction than it removes.

### How Would I Know the Platform Helped?

To understand whether a platform, or one capability within it, actually helped, I need to compare what happened without it with what happens after it is introduced. If I can measure that difference clearly, I have useful evidence.

Some effects are harder to measure. In those cases, I can ask the people using the platform whether it removed work or merely moved it.

### What Was the Baseline?

Before introducing a shared capability, I need to know how often the constraint occurs. Useful measures include workflow completion time, waiting time, duplicated implementations, incidents, audit effort, and cost per successful outcome.

### What Changed?

After introducing it, I can ask whether more common cases complete without extra help. Waiting time, incidents, audit effort, or cost should improve. Adoption alone tells me only that the capability is being used.

### What New Costs and Risks Did the Platform Introduce?

I also have to count platform staffing, support, maintenance, on-call load, switching cost, and common failure risk. The original problem may disappear or become less important. If the platform no longer removes enough work to justify its cost, I should be willing to remove it or the parts that no longer help.

A platform needs a removal condition as much as it needs a success measure.

### Chapter 3: What Does "Smallest" Mean?

### Is the Smallest Platform the One With the Fewest Features?

It is tempting to measure the size of a platform by counting its features, services, or lines of configuration. By that measure, a YAML file is smaller than a gateway, and a gateway is smaller than a runtime.

A small central contract can force every team to build adapters, reconstruct audit evidence, and explain the same fields differently. A broad managed runtime can hide its servers behind a vendor invoice while creating a common failure domain, a permanent on-call dependency, and an expensive exit. Both may look small from the platform team's perspective.

I need a definition that counts the whole system, including the work that appears outside the platform boundary:

> The smallest useful AI platform is the lowest-total-work shared capability that lets a defined group complete one valuable workflow, meets that workflow's risk floor, and remains cheaper to change or remove than the work it displaces.

This gives "smallest" four tests:

| Test | Question |
| --- | --- |
| Outcome | Does it remove the measured constraint and let the intended user complete the job? |
| Risk | Does it provide the minimum controls required by the data, authority, reversibility, and impact involved? |
| Total work | Does it reduce central and local integration, support, audit, incident, migration, and exception work? |
| Reversibility | Can its contracts, state, evidence, and consumers be changed or retired at an acceptable cost? |

"Smallest" in that sense is the lightest arrangement that passes all four tests for a particular workflow.

### What Is the Minimum Capability That Must Be Shared?

My current hypothesis is that the first useful shared capability is not an agent runtime or a new AI portal, even though we have both already even though nobody really asked. It is a versioned agent contract beside the code.

The contract would describe at least:

- who the agent is, why it exists, who owns it, and whether it is experimental, active, or retired
- what harm it could cause and what kinds of data it handles
- where it runs and which revision is deployed
- which model providers, models, and processing regions it may use
- which tools it may call, what access each tool requires, and whose authority or identity it uses
- how the agent is evaluated, which evaluation version applies, who owns it, and whether it currently passes
- how to respond when something goes wrong, whom to contact, and how to disable the agent
- how to connect each run to its traces, cost, product, and workflow
- when the agent was last reviewed, when approval expires, and which exceptions were accepted

This is already more than a catalogue entry. It connects the agent to decisions made by delivery, security, finance, compliance, and incident response. Every required field needs a named owner, an authoritative source, a consumer, and a decision that the consumer makes from it.

Where a field comes from is also important. Some facts are **declared** by the team, some are **observed** by CI or the runtime, and some are **attested** by an independent owner. These are not interchangeable.

The contract needs schema checks, valid and invalid examples, compatibility tests for its consumers, and a deprecation policy. It also needs an owner.

The smallest AI-specific addition could be an `Agent` kind or attached metadata that an IDP such as Backstage renders while CI, observability, FinOps, and deployment systems remain authoritative for the facts they already know.

### How Should the Minimum Change With Risk?

The controls an agent needs should depend on the consequences of getting it wrong. An experiment using public data and taking no external action does not need the same controls as an agent that moves money or changes production infrastructure.

I find four working classes useful:

| Class | Example | Minimum shared capability |
| --- | --- | --- |
| Experiment | Local prototype using synthetic or public data | Owner, purpose, lifecycle, access guidance, and deletion date |
| Internal read-only | Search, summarization, or drafting with internal data | Data class, provider and region, evaluation reference, trace and cost correlation, and incident contact |
| Reversible action | Drafts tickets, code changes, or bounded transactions for review | Tool scopes, per-run identity, approval rule, rollback, audit log, runbook, and kill switch |
| High-impact action | Customer, financial, employment, safety, regulated, or privileged action | Accountable risk owner, formal evaluation threshold, isolation, ongoing monitoring, retained evidence, and independent approval |

This is an operating model I want to test. A higher class raises the control floor. It does not automatically require one central runtime.

The control should be enforced at the latest boundary where harm can still be prevented. A missing description can produce a warning. An invalid owner reference can fail CI. Missing approval for a production agent can block deployment. A consequential tool action must be authorized by the downstream system using the identity and authority of that run.

This is where a shared AI platform capability begins to make sense. It can define which controls apply, validate them consistently, and connect each control to the boundary where it can still prevent harm. CI, deployment, and downstream systems may perform the enforcement, while the platform gives them a shared contract.

A green catalogue entry is not permission to transfer money.

This distinction is important because contracts and enforcement do different jobs. A contract can define vocabulary, validate shape, maintain compatibility, and support admission decisions. But it cannot stop a running agent from using an overpowered credential.

### What Can Be Removed Without Preventing Users From Succeeding?

The useful sequence is:

> documentation → template → contract → conformance checks → admission control → gateway → shared runtime

I would start at the left and keep the first rung that lets the intended user complete the workflow while meeting the risk floor. There is no reason to continue climbing because the architecture diagram still has room.

This means reusing existing identity, deployment, observability, incident response, billing, and data-governance systems wherever they can do the job. I would add an AI-specific capability only when the existing system cannot provide it without several teams rebuilding the same consequential machinery.

Subtraction also has to include local work. Removing a central evaluation service is not a saving if every team now creates its own scripts, spreadsheets, review interface, and evidence store. Google illustrated this problem in its paper on [hidden technical debt in machine learning systems](https://research.google/pubs/hidden-technical-debt-in-machine-learning-systems/): model code can be a small part of a production ML system while the surrounding glue carries most of the weight.

The question is not "How little can the platform team own?" It is "Which arrangement produces the least total work per successful, governed outcome?"

### Does the Smallest Platform Need a User Interface?

A platform needs an interface. It does not necessarily need its own graphical interface.

An engineer may be well served by reviewed YAML with editor and CI feedback. A common repository may need only a template or CLI. Another system needs an API or export, not a new portal page.

Other users have different jobs. A domain expert comparing agent outputs may need a purpose-built review interface almost immediately. A risk owner may need evidence and approval controls in the existing system where the consequential action happens. Finance, audit, and incident response may need a fleet view in an IDP such as Backstage. Giving them raw records would only move the reconciliation work to them.

The smallest interface is therefore specific to a user and a job:

| User and job | Likely first interface |
| --- | --- |
| Engineer registers or changes an agent | Versioned file with editor and CI feedback |
| Engineer creates a common repository | Template or CLI using the same schema |
| Occasional or non-engineer builder configures a bounded workflow | Existing form, low-code surface, chat, or generated pull request |
| Domain expert evaluates outputs | Review and annotation interface |
| Risk owner approves an action | Existing approval interface close to the downstream system |
| Finance, audit, or incident response inspects the fleet | Existing portal or report over authoritative data |
| Another system consumes metadata | API or export |

[Google's definition of an internal developer platform](https://cloud.google.com/solutions/platform-engineering) explicitly allows for a platform with or without a portal. That distinction seems right to me. A portal is useful when it helps someone complete a job. Before that, it mostly gives the platform a homepage.

### Does the Smallest Platform Need to Run Agents?

Helping teams build agents and running those agents are different commitments. The first shapes a path. The second owns an operating model.

A build-enabling platform can provide approved access patterns, metadata, repository templates, evaluation hooks, telemetry conventions, deployment hooks, and discovery. Execution can remain on the existing application platform.

A shared runtime must additionally own per-run identity, tool authorization, queues, retries, timeouts, idempotency, cancellation, streaming, quotas, isolation, state, recovery, human approvals, capacity, SLOs, on-call, incident response, evidence retention, and decommissioning. That is not one more feature. It is an operating model.

Several teams building agents does not prove that the platform should run them. I would move that boundary only when several teams repeatedly rebuild the same runtime responsibility, getting it wrong creates meaningful risk, and central ownership reduces total work or risk after support, migration, and common failure costs are counted.

[Anthropic's guidance on building effective agents](https://www.anthropic.com/engineering/building-effective-agents) recommends simpler workflows when they are sufficient. The platform should preserve that choice. It should not require an agent runtime for software that did not need to become an agent in the first place.

### Could the Smallest Platform Be a Contract?

Yes, but only if the contract removes real work.

A versioned agent descriptor, validated in CI and displayed through an IDP such as Backstage, could solve ownership, discovery, cost allocation, lifecycle, and evidence problems while agents continue to run on the existing platform. Thin adapters could send the relevant fields to observability, FinOps, and governance systems.

This is the smallest credible starting point I can see for the problems described in the first two chapters.

It remains a hypothesis. The contract fails the test if teams cannot complete the workflow without repeated help, if its data goes stale, if every consumer needs a custom adapter, or if a consequential control can only be applied at runtime. In those cases the next smallest answer may be a generator, a narrow authorization service, a model gateway, or an evaluation service.

The contract also has to be removable. Its versions and consumers should be known. One agent record should be exportable and deletable without affecting the running agent. If catalogue metadata becomes required for execution without a deliberate decision, the catalogue has quietly become a runtime dependency.

Quiet dependencies are still dependencies.

### What Should the Platform Deliberately Not Provide?

The boundaries are as important as the capability itself. The platform I am describing should not:

- define one agent framework, prompt pattern, memory system, or orchestration model
- own product prompts, domain tools, business evaluation rules, or the definition of acceptable harm
- replace existing identity, deployment, observability, incident, billing, or data-governance systems
- build a new portal when Git, an IDP such as Backstage, a template, an existing approval interface, or an API serves the job
- treat self-declared metadata as runtime evidence
- authorize a tool merely because it appears in a catalogue
- store prompt and tool payloads by default when metadata, sampling, or redaction is enough
- force experiments through controls designed for high-impact production actions
- promise indefinite compatibility for unused fields
- mandate adoption to hide an unhelpful path
- run agents before repeated runtime constraints justify the operational burden

These are boundaries, not unfinished roadmap items. I would move any one of them into the platform only after a measured constraint shows that leaving it outside creates more work or risk.

### When Should a Capability Be Shrunk, Replaced, or Removed?

Platforms are often designed as if adoption were a one-way door. A smallest platform needs an exit before it needs a roadmap.

I would **shrink it** when a lower rung achieves the same outcome and risk result, most features have no active consumer, exceptions and support do not decline, or execution can return to existing compute while contracts and evidence remain.

I would **replace it** when an existing platform or supplier provides the capability at lower total cost, the replacement preserves identity and evidence, and a representative workload can move without rebuilding product logic or evaluation data. The comparison must include migration and running both systems during the move.

I would **remove it** when the original constraint has disappeared, no risk obligation or critical consumer remains, actual usage confirms the long tail is gone, and every real user job has a tested alternative or intentionally no replacement.

Removal is still a product change. It needs retention decisions, migration support, rollback, communication, and money. When the UK Government Digital Service decided to [decommission GOV.UK PaaS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/), it gave users 18 months to migrate. The service was reliable and well liked. It had simply lost its comparative advantage.

That is the standard I want to use here. The smallest AI platform is not a miniature version of a broad one. It is the lightest owned arrangement that produces a successful, governed outcome after central work, local work, risk, and exit are all counted.

### Chapter 4: Where Should the Platform End?

The contract gives the platform a possible beginning. It does not yet tell me where the platform should end. I still need to understand which responsibilities create value when shared and which ones need to remain close to the team that understands the workflow.

- Are model access, tools, identity, evaluation, observability, and deployment all platform responsibilities?
- Which of those capabilities are necessary from the beginning?
- Should the platform own integrations, or only define how integrations are exposed?
- Are MCP-related tools part of an AI platform?
- Should the AI platform own the agent catalogue, or only define and publish the agent-specific metadata that the existing developer platform displays?
- Which capabilities should be centralized, and which should remain with individual teams?

### Chapter 5: How Can the Platform Preserve Freedom?

Even a useful common path can become a constraint. If teams cannot change, extend, replace, or leave it, the platform may remove repeated work by removing agency. That is not the kind of leverage I want to build.

These questions remain open:

- How can teams escape the platform when their needs differ?
- Could the platform become a bottleneck?
- Who operates it, and what ongoing cost does that create?
- How does it avoid locking teams into one model, vendor, or agent framework?
- Should safety and governance be built into the path or enforced around it?

## Prototype

### Chapter 6: Can the Smallest Platform Survive Contact With a Prototype?

### Can a Contract Be Enough?

A definition is useful, but it does not show whether the work really disappears. I need to build the smallest version and observe what happens around it.

My current hypothesis is a versioned agent contract beside the code, validated in CI and displayed through systems the organization already operates. It should not require a new portal or a shared agent runtime.

I will test this with one internal, read-only agent and one end-to-end workflow:

1. An engineer creates or changes the agent from a repository.
2. CI validates its identity, owner, purpose, lifecycle, risk class, model access, evaluation reference, runtime reference, cost identifier, trace identifier, runbook, and disable mechanism.
3. The existing developer portal displays the contract and links to the authoritative runtime, evaluation, cost, trace, and incident information.
4. The agent continues to run on the existing application platform.

The prototype succeeds only if the engineer can complete the common path without repeated platform-team help, finance can attribute the cost, and an incident responder can find the owner, running revision, traces, runbook, and disable mechanism without reconstructing them by hand.

Before building it, I need a baseline:

- time from repository creation to a registered and observable deployment
- number of manual platform-team interactions
- time needed to attribute the agent's model cost
- time needed to identify the running revision, owner, and incident procedure
- local adapters or duplicate records required outside the contract

The contract is not the answer merely because it is small. It fails if its data becomes stale, every consumer needs a custom adapter, teams still need repeated help, or consequential controls can only be enforced at runtime. In those cases, the next smallest answer may be a generator, a narrow authorization service, a gateway, or an evaluation service.

I should also be able to delete the contract without stopping the agent. If I cannot, I have built a runtime dependency while calling it metadata.

## Conclusion

My answer remains provisional until the prototype has survived contact with an actual workflow.

For now, the smallest AI platform that could possibly work is not a miniature version of a broad platform. It is a versioned contract for one repeated and valuable workflow, connected to systems the organization already operates, with only the enforcement that the workflow's risk requires.

The smallest platform is not the one with the fewest features. It is the shared capability that removes more total work than it creates and remains affordable to change or leave.

A contract may satisfy that definition. Building it may prove that it does not.

The AI-specific parts of this answer will change. Four questions should last longer: Does the platform produce the outcome? Does it meet the risk floor? Does it reduce total work? Can people still change it or leave?

## Emerging Principle

> Build a platform only when it removes more total work than it creates.

A platform creates leverage when a capability built once removes work repeatedly. It preserves engineering freedom when people can still change it, extend it, replace it, or leave.

A useful platform needs both.
