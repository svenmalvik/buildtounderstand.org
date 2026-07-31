---
title: What Is the Smallest (AI) Platform That Could Possibly Work?
date: 2026-07-27
excerpt: Under exploration.
published: true
---

# What Is the Smallest (AI) Platform That Could Possibly Work?

## Question

At Vipps, one of the most common requests I see is access to LLMs. Giving an engineer an API key is easy. It solves the immediate access problem. It does not help finance attribute the bill, compliance understand the data flow, or incident response observe the system.

The key is small. The work around it is not.

That difference made me ask two questions. When does recurring work justify a shared platform? If it does, what is the smallest form that platform could take?

I am using AI agents as the current case. By agents, I mean software built with LLMs, skills, and integrations with internal or external tools. This raises a broader question: When does a shared system create leverage, and when does it merely centralize work and reduce freedom?

## Exploration

### Chapter 1: What Problem Would a Platform Solve?

Organizations want engineers and non-engineers to build useful agents. As more people try, the same needs begin to appear. Developers need model access, evaluation tools, and a path to deployment. Finance needs cost attribution. Compliance needs control over data flows and audit evidence. Incident response needs a system it can observe.

None of these requests alone justifies an AI platform. One team asking for model access has an access problem. One finance department asking about a bill has an accounting problem. A collection of experiments does not become a platform problem just because the experiments use AI.

I start seeing a platform problem when teams repeatedly need the same access controls, cost attribution, evaluation, observability, or audit evidence. At that point, solving every use case separately creates more work, inconsistent controls, or unnecessary risk.

The number of agents is a poor threshold. A company may have one hundred experiments and no platform problem. The same company may have only two agents in production that handle sensitive data and already need strict controls. The difference is not the number of agents. It is whether a constraint repeats, what happens when it is ignored, and whether a shared capability would remove more work than it creates.

Even then, the answer may be to extend a platform that already exists. I would consider a dedicated AI platform only when existing systems cannot remove the repeated constraint without every team rebuilding the same AI-specific components.

I see a version of this with PR review agents. An engineer uses the most capable available model with extra-high reasoning effort. The agent solves an immediate and obvious problem for the team. It may still ignore the cost of each review, the rules that govern the review, and how another team could learn from the work or build upon it.

The first version works for the team. The organization becomes responsible for everything around it.

### Can a Platform Help People Build Agents?

An AI platform can help engineers and non-engineers build agents. I use the word "can" because its usefulness depends on the problem it removes, not on how complete the platform looks.

At Vipps, we created an agent template called AI Playground. A builder visits our internal developer portal, clicks a button, and gives the agent a name. This creates a repository with a working agent already deployed to the test environment. The builder also receives a starter prompt for a coding agent. The coding agent clones the repository and asks what to do next. From there, the builder can start shaping the agent instead of recreating the same setup.

Whether agent creation belongs to an AI platform is partly a matter of definition. The template solves one recurring problem. Non-engineers no longer need an engineer to recreate the same setup for every agent. Requirements from other stakeholders can also be included in the process, even when the builder does not know about them yet.

The value is not the button in the portal. It is the repeated work that the button removes.

### Chapter 2: When Does Shared Work Become a Platform?

### What Is Actually Repeating?

Repeating work does not always look the same. I have seen two examples often enough to be useful here.

Non-engineers such as analysts and product managers use Claude Code or Codex to build something useful, perhaps a dashboard. It works on their machine. Making it available to others means connecting it to company data and deploying it to the company runtime. At Vipps, services follow a contract that engineers receive through the internal developer portal. Using that contract still requires engineering experience, so the platform team helps each new builder through much of the same work.

The second example is simpler. Engineers build AI-powered Slack apps and ask for an API key to an LLM. The request takes little time, but handing out a key does not provide cost attribution, data controls, evaluation, or useful observability.

The work is not identical. The first example repeats deployment support. The second repeats access without the controls other stakeholders need. Both may be platform candidates.

I start by looking for repeated work. Repetition alone is not a reason to build.

### When Does Repeated Work Justify a Shared Solution?

Teams may repeat work because they are still learning. Centralizing it too early can turn useful experiments into a shared solution nobody needs. I would treat repetition as a meaningful constraint only when it blocks a valuable workflow and produces a visible consequence:

- **Incidents and Recovery:** Does the repeated constraint cause preventable incidents, or make incidents harder to detect, contain, and recover from?
- **Audit Effort:** Does every team have to reconstruct the same evidence differently, and how much effort does that require?
- **Cost:** What does the constraint cost through duplicated implementation, infrastructure use, waiting, support, and rework?
- **Reliability:** Do local solutions fail inconsistently, make failures difficult to observe, or make dependable recovery difficult?
- **Risk:** What are the consequences of getting this work wrong, and how widely could those consequences spread?

There is no useful universal threshold based on the number of teams, agents, models, or requests. Two production agents handling sensitive data may justify shared controls. One hundred experiments may not. The consequences are more important than the count.

### Could the Work Be Removed Instead?

Before I build a shared capability, I should ask whether the workflow or constraint should exist at all. The apparent platform problem may be unclear ownership, missing training, unnecessary variation, a poor procurement choice, or a workflow that should simply be removed.

Calling it a platform problem too early assumes a solution before the cause is understood. Platforms can standardize work that nobody needed.

### Could Documentation, Conventions, or Reusable Libraries Be Enough?

My next test is whether a simpler solution removes the constraint. The order is important: documentation, a convention, a template, a library, a CLI, and only then a narrow managed capability.

A small team may need no more than a repository template and a CLI. Expensive or risky concerns such as identity, policy, databases, or audit evidence are stronger candidates for a managed service. The goal is to use the simplest option that completes the work.

### When Does a Shared Capability Become a Platform?

A shared capability becomes platform-like when teams choose it as the standard option because it is easier and safer than solving the problem locally.

That choice is important. Adoption by mandate can make a platform common without making it useful.

I am interested in whether the capability removes enough repeated work to justify the work it creates. Someone still has to own and maintain it. If that costs more than the coordination and risk it removes, the platform has not created leverage. It has moved the work.

The first justified AI platform may therefore be a gateway, evaluation service, policy check, trace convention, cost-attribution layer, or deployment contract. It does not need to begin as one broad integrated product labelled as an AI platform.

### Who Does Not Need an AI Platform?

An AI platform is probably premature when there is only one team, few production workflows, or no valuable use case yet. It is also a poor answer when the real problem is skills, data access, or workflow design.

A team must first understand its work well enough to describe the workflow. Only then can it decide what should be automated and what, if anything, should be shared.

A dedicated AI platform also needs clear ownership, support, upgrades, and a way to replace or remove old versions. That requires ongoing work.

### When Does a Platform Create More Work Than It Removes?

I would worry when adoption depends on a mandate, users wait longer than before, or teams keep forking and bypassing the platform. These signs show that the standard option may be creating more work than it removes.

### How Would I Know the Platform Helped?

To understand whether a platform, or one capability within it, actually helped, I need to compare what happened without it with what happens after it is introduced. If I can measure that difference clearly, I have useful evidence.

Some effects are harder to measure. In those cases, I can ask the people using the platform whether it removed work or merely moved it.

### What Was the Baseline?

Before introducing a shared capability, I need to know how often the constraint occurs. Useful measures include workflow completion time, waiting time, duplicated implementations, incidents, audit effort, and cost per successful outcome.

### What Changed?

After introducing it, I can ask whether more common cases complete without extra help. Waiting time, incidents, audit effort, or cost should improve. Adoption alone tells me only that the capability is being used.

### What New Costs and Risks Did the Platform Introduce?

I also have to count platform staffing, support, maintenance, on-call load, the cost of moving away, and the risk that one failure affects everyone. The original problem may disappear or become less important. If the platform no longer removes enough work to justify its cost, I should be willing to remove it or the parts that no longer help.

A platform needs criteria for removing it as much as it needs a measure of success.

### Chapter 3: What Does "Smallest" Mean?

### Is the Smallest Platform the One With the Fewest Features?

It is tempting to measure the size of a platform by counting its features, services, or lines of configuration. By that measure, a YAML file is smaller than a gateway, and a gateway is smaller than a runtime.

A small central contract can force every team to build adapters, reconstruct audit evidence, and explain the same fields differently. A broad managed runtime may replace visible servers with a vendor invoice while creating one failure that affects every team, a permanent on-call responsibility, and a high cost to leave. Both may look small from the platform team's perspective.

I need a definition that counts the work done by the platform team and the teams using the platform:

> The smallest useful AI platform is the shared capability that creates the least total work, lets a defined group complete one valuable workflow, meets the minimum required controls, and remains cheaper to change or remove than the repeated work it removes.

This gives "smallest" four tests:

| Test | Question |
| --- | --- |
| Outcome | Does it remove the measured constraint and let the intended user complete the job? |
| Risk | Does it provide the minimum controls required by the data, authority, ability to reverse an action, and possible impact? |
| Total work | Does it reduce central and local integration, support, audit, incident, migration, and exception work? |
| Change and removal | Can its contracts, state, evidence, and users be changed or retired at an acceptable cost? |

"Smallest" in that sense is the simplest solution that passes all four tests for a particular workflow.

### What Is the Minimum Capability That Must Be Shared?

We already have an agent runtime and an AI portal, although nobody really asked for either. My current hypothesis is that the first useful shared capability is simpler: a versioned agent contract stored with the code.

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

This is already more than a catalogue entry. It connects the agent to decisions made by delivery, security, finance, compliance, and incident response. Every required field needs a named owner, a source responsible for the fact, a person or system that uses it, and a decision made from it.

Where a field comes from is also important. Some facts are **declared** by the team, some are **observed** by CI or the runtime, and some are **confirmed** by an independent owner. These are not interchangeable.

The contract needs checks against its schema, valid and invalid examples, compatibility tests for the systems that use it, and a policy for changing or removing fields. It also needs an owner.

The smallest AI-specific addition could be an `Agent` kind or attached metadata that an IDP such as Backstage displays. CI, observability, FinOps, and deployment systems would remain the sources for the facts they already know.

### How Should the Minimum Change With Risk?

The controls an agent needs should depend on the consequences of getting it wrong. An experiment using public data and taking no external action does not need the same controls as an agent that moves money or changes production infrastructure.

I find four working classes useful:

| Class | Example | Minimum shared capability |
| --- | --- | --- |
| Experiment | Local prototype using synthetic or public data | Owner, purpose, lifecycle, access guidance, and deletion date |
| Internal read-only | Search, summarization, or drafting with internal data | Data class, provider and region, evaluation reference, trace and cost correlation, and incident contact |
| Reversible action | Drafts tickets, code changes, or limited transactions for review | Tool permissions, identity for each run, approval rule, rollback, audit log, incident response instructions, and a way to disable the agent |
| High-impact action | Customer, financial, employment, safety, regulated, or privileged action | Accountable risk owner, formal evaluation threshold, isolation, ongoing monitoring, retained evidence, and independent approval |

This is an operating model I want to test. Each higher class requires more controls. Those controls can still be enforced without one central runtime.

Each control should be enforced by the last system that can still prevent harm. A missing description can produce a warning. An invalid owner reference can fail CI. Missing approval for a production agent can block deployment. A tool action with serious consequences must be authorized by the downstream system using the identity and authority of that run.

This is where a shared AI platform capability begins to make sense. It can define which controls apply, validate them consistently, and connect each control to the system that can still prevent harm. CI, deployment, and downstream systems may perform the enforcement, while the platform gives them a shared contract.

This distinction is important because contracts and enforcement do different jobs. A contract can define vocabulary, validate its structure, maintain compatibility, and support decisions about whether an agent may be deployed. But it cannot stop a running agent from using a credential with too much access.

### What Can Be Removed Without Preventing Users From Succeeding?

The useful sequence is:

> workflow documentation → template → contract → validation checks → deployment controls → gateway → shared runtime

I would start by documenting one valuable workflow and the controls it requires. For an internal read-only agent, the documentation could explain how to request model access, which data the agent may use, how to deploy and evaluate it, how to record its cost and traces, and who to contact if something goes wrong.

If teams can complete the workflow without repeated platform-team help, documentation may be enough. If the same questions or manual steps continue, I would add the next simplest capability. Each new capability should remove a specific repeated task or provide a required control.

This means reusing existing identity, deployment, observability, incident response, billing, and data-governance systems wherever they can do the job. I would add an AI-specific capability only when the existing system cannot provide it without several teams rebuilding the same controls for high-impact work.

When removing a central capability, I also have to count the work this creates for each team. Removing a central evaluation service is not a saving if every team now creates its own scripts.

I want to find the solution that produces the least total work but that still meets the required controls.

### Does the Smallest Platform Need a User Interface?

A platform needs an interface. It does not necessarily need its own graphical interface.

An engineer may need only reviewed YAML with editor and CI feedback. A common repository may need only a template or CLI. Another system needs an API or export, not a new portal page.

Other users have different jobs. A domain expert comparing agent outputs may need a review interface almost immediately. A risk owner may need evidence and approval controls in the existing system where the high-impact action happens. Finance, audit, and incident response may need a view of all agents in an IDP such as Backstage. Giving them raw records would only move the work of connecting those records to them.

The smallest interface is therefore specific to a user and a job:

| User and job | Likely first interface |
| --- | --- |
| Engineer registers or changes an agent | Versioned file with editor and CI feedback |
| Engineer creates a common repository | Template or CLI using the same schema |
| Occasional or non-engineer builder configures a workflow with limited actions | Existing form, low-code interface, chat, or generated pull request |
| Domain expert evaluates outputs | Review and annotation interface |
| Risk owner approves an action | Existing approval interface close to the downstream system |
| Finance, audit, or incident response inspects all agents | Existing portal or report using data from its original sources |
| Another system consumes metadata | API or export |

### Could the Smallest Platform Be a Contract?

Yes, but only if the contract removes real work.

A versioned agent descriptor, validated in CI and displayed through an IDP such as Backstage, could solve ownership, discovery, cost allocation, lifecycle, and evidence problems. Small integrations could send the relevant fields to observability, cost-management, and governance systems.

This is the simplest possible starting point I can see for the problems described in the first two chapters.

I still need to test this hypothesis. The contract fails the test if teams cannot complete the workflow without repeated help, if its data becomes outdated, if every consumer needs a custom adapter, or if a control for a high-impact action can only be applied at runtime. In those cases, the next simplest answer may be a generator, an authorization service, an ai gateway, or an evaluation service.

The contract also has to be removable. Its versions and consumers should be known. One agent record should be exportable and deletable without affecting the running agent. If catalogue metadata becomes required for execution without a decision, the catalogue has become a runtime dependency.

### What Should the Platform Not Provide?

The platform I am describing should not:

- define one agent framework, prompt pattern, memory system, or orchestration model
- own product prompts, domain tools, business evaluation rules, or the definition of acceptable harm
- authorize a tool just because it appears in a catalogue
- store prompt and tool payloads by default when metadata, sampling, or redaction is enough
- force experiments through controls designed for high-impact production actions
- run agents before repeated runtime problems justify the work required to operate them

These limits are intentional. I would add any one of these capabilities to the platform only after a measured constraint shows that leaving it outside creates more work or risk.

### When Should a Capability Be Reduced, Replaced, or Removed?

When I introduce a platform, I should also decide what would make me remove it. I need to understand this before deciding what to add next.

I would **reduce it** when a simpler option achieves the same outcome and risk result, most features have no active consumer, the number of exceptions and support requests does not decrease, or agents can run on the existing application platform while their contracts and evidence remain available.

I would **replace it** when an existing platform or supplier provides the capability at lower total cost, the replacement preserves identity and evidence, and a typical agent can move without rebuilding product logic or evaluation data. The comparison must include migration and running both systems during the move.

I would **remove it** when the original constraint has disappeared, no risk obligation or critical consumer remains, usage data shows that no remaining users depend on it, and every real user job has a tested alternative or intentionally no replacement.

Removal is still a product change. It needs retention decisions, migration support, rollback, communication, and money.

That is the standard I want to use here. A small AI platform must count the central work, local work, required controls, and cost of leaving.

### Chapter 4: Where Should the Platform End?

The contract gives the platform a possible beginning. However, it does not tell where the platform should end. Model access, tools, identity, evaluation, observability, and deployment all affect the platform. However, they do not necessarily belong always to the platform team.

| Capability | What could be shared | What should remain elsewhere |
| --- | --- | --- |
| Model access | Credentials, quotas, cost attribution, trace correlation, and a common interface | Existing identity and secret systems; the workflow team's model choice, prompts, fallback behavior, and product outcome |
| Tools | Common rules for making tools available to agents, information about origin and ownership, authentication, and audit fields | Business rules, data access, side effects, authorization, support, and repair |
| Identity | Agent identity metadata, delegated-user context, requested permissions, and a way to revoke access | The existing identity platform issues identities and credentials; the resource owner decides whether a business action is allowed |
| Evaluation | A common runner, formats, scheduling, history, and reusable evidence | The domain team defines representative cases, possible harm, acceptance levels, and whether a release is good enough |
| Observability | Shared trace fields that connect models, tools, evaluations, cost, and workflows | An existing observability platform handles the data; the product team defines service levels, alerts, and the meaning of a failure |
| Deployment | A common description of the agent, its model, tools, evaluation evidence, running revision, and rollback | The existing delivery platform deploys and runs it; the product team decides when to release and whether a rollback is safe |

The AI platform can define the common parts and connect them to systems the organization already uses. But decisions that depend on the workflow should stay with the team that understands it.

### What Is Necessary From the Beginning?

The first version needs enough information and control to make one real workflow accountable and replaceable. The contract from Chapter 3 already describes the owner, purpose, lifecycle, risk, interfaces, dependencies, requested access, evaluation evidence, traces, cost, deployed revision, rollback, incident contact, exceptions, and a way to leave.

The first version does not need to provide all the systems behind that information. Existing identity systems can issue access. The downstream service can authorize a business action. The observability platform can collect its traces. The developer portal can display information from those systems.

An ai gateway or a common evaluation service do not become necessary because the workflow uses an LLM. I would add those when it removes measured repeated work or provides a required control that the contract and existing systems cannot yet provide.

### When Is a Contract Not Enough?

A contract can be small and still create a large amount of work. Every team may still need to build an adapter, collect evidence, understand errors, and fix outdated information. The contract then describes the work in the same way for every team. It does not remove the work.

To remove work, the contract needs a working implementation, compatibility checks, and information about where each fact came from. It also needs to compare what a team declared with what the systems observed. An agent can say which revision is deployed or which evaluation it passed. The delivery and evaluation systems must confirm it.

I would move beyond the contract when teams still need the same help, when they keep rebuilding the same components, or when a required control can only work while the agent is running. The next capability could be a generator, evaluation service, (ai) gateway, authorization service, or dedicated runtime. The kind of repeated work should decide the priority.

### Where Should Mandatory Controls Be Enforced?

A shared policy and shared enforcement are different choices. Each control should be enforced by a system that cannot be bypassed.

A gateway can enforce which model providers and regions are allowed because it controls that connection. A deployment system can require evaluation evidence before releasing an agent.

The AI platform can connect these controls without making decisions it doesn't understand. A contract or catalogue entry can describe the required authority. However, it can't prove that a running action is allowed.

### Should the Platform Own Integrations?

I would start by defining how integrations are exposed. Owning them comes later. A common pattern can describe authentication, timeouts, retries, duplicate requests, versions, traces, ownership, and retirement.

I would move an integration into the platform when several teams need the same stable behavior and someone has the knowledge and time to support it. That owner must be able to diagnose failures in the downstream system, support new versions, respond to incidents, and remove the integration later.

### Where Does MCP Belong?

MCP changes how a tool is exposed but doesn't change who understands the tool.

The platform can define which parts of MCP it supports, how servers are registered, how identity is passed, which evidence is recorded, which minimum isolation applies, and how compatibility is tested. The team that understands the tool's inputs, side effects, permissions, and failures should still own the tool and the system behind it.

The same boundary should apply to an MCP tool and an ordinary API integration. Finding a tool through MCP does not grant access to it. The downstream system still needs to check the current identity, permission, approval, and state before performing an action.

### Should the AI Platform Own the Agent Catalogue?

I do not see a reason to build a separate AI catalogue yet. The AI platform can define and validate agent-specific metadata, then publish it into the existing developer platform such as Backstage.

I would try to extend the developer platform people already use and measure what remains missing. A separate AI catalogue may become useful if the existing platform cannot represent the agent lifecycle or the evidence people need.

### Chapter 5: How Can the Platform Preserve Freedom?

Even a useful standard option can become a constraint. If teams cannot change, extend, replace, or stop using it, the platform may remove repeated work by removing agency. That is not the kind of leverage I want to build.

These questions remain open:

- How can teams stop using the platform when their needs differ?
- Could the platform slow teams down?
- Who operates it, and what ongoing cost does that create?
- How does it let teams change models, vendors, or agent frameworks?
- How can mandatory safety and governance controls still leave room to choose a different path?

## Prototype

### Chapter 6: Can a Prototype Show Whether the Smallest Platform Works?

### Can a Contract Be Enough?

A definition is useful, but it does not show whether the platform really removes work. I need to build the smallest version and measure the work it removes and creates.

My current hypothesis is a versioned agent contract stored with the code, validated in CI and displayed through systems the organization already operates. It should not require a new portal or a shared agent runtime.

I will test this with one internal, read-only agent and one end-to-end workflow:

1. An engineer creates or changes the agent from a repository.
2. CI validates its identity, owner, purpose, lifecycle, risk class, model access, evaluation reference, runtime reference, cost identifier, trace identifier, incident response instructions, and a way to disable it.
3. The existing developer portal displays the contract and links to the systems that contain the runtime, evaluation, cost, trace, and incident information.
4. The agent continues to run on the existing application platform.

The prototype succeeds only if the engineer can complete the standard workflow without repeated platform-team help, finance can attribute the cost, and an incident responder can find the owner, running revision, traces, incident response instructions, and a way to disable the agent without reconstructing them by hand.

Before building it, I need a baseline:

- time from repository creation to a registered and observable deployment
- number of manual platform-team interactions
- time needed to attribute the agent's model cost
- time needed to identify the running revision, owner, and incident procedure
- local adapters or duplicate records required outside the contract

The contract is not the answer merely because it is small. It fails if its data becomes outdated, every consumer needs a custom adapter, teams still need repeated help, or controls for high-impact actions can only be enforced at runtime. In those cases, the next simplest answer may be a generator, a narrow authorization service, a gateway, or an evaluation service.

I should also be able to delete the contract without stopping the agent. If I cannot, it is a runtime dependency rather than only metadata.

## Conclusion

My answer is not final until I test the prototype with an actual workflow.

For now, the smallest AI platform that could possibly work is not a smaller copy of a broad platform. It is a versioned contract for one repeated and valuable workflow, connected to systems the organization already operates, with only the controls that the workflow requires.

The smallest platform is not the one with the fewest features. It is the shared capability that removes more total work than it creates and remains affordable to change or leave.

A contract may satisfy that definition. Building it may prove that it does not.

The AI-specific parts of this answer will change. Four questions are likely to remain useful for longer: Does the platform produce the outcome? Does it meet the minimum required controls? Does it reduce total work? Can people still change it or leave?

## Emerging Principle

> Build a platform only when it removes more total work than it creates.

A platform creates leverage when a capability built once removes work repeatedly. It preserves engineering freedom when people can still change it, extend it, replace it, or leave.

A useful platform needs both.
