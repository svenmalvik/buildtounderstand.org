---
title: What Is the Smallest (AI) Platform That Could Possibly Work?
date: 2026-07-27
excerpt: Under exploration.
published: true
---

# What Is the Smallest (AI) Platform That Could Possibly Work?

At Vipps, one of the most common requests I see is access to LLMs. Giving an engineer an API key is easy. It solves the immediate access problem. However, it doesn't show finance which team created the cost, help compliance understand where the data goes, or give incident response a way to observe the system.

The difference between giving someone access and handling everything around it made me ask two questions. When does recurring work justify a shared platform? And if it does, what is the smallest platform that could possibly work?

I am using AI agents as the current case. By agents, I mean software built with LLMs, skills, and integrations with internal or external tools.

## Chapter 1: What Problem Would a Platform Solve?

Organizations want engineers and non-engineers to build useful agents. As more people try, the same needs begin to appear. Developers need model access, evaluation tools, and a path to deployment. Finance needs cost attribution. Compliance needs control over data flows and audit evidence. Incident response needs a system it can observe.

None of these requests alone justifies an AI platform. One team asking for model access has an access problem. One finance department asking about a bill has an accounting problem. A collection of experiments doesn't become a platform problem just because the experiments use AI.

I start seeing a platform problem when teams repeatedly need the same access controls, cost attribution, evaluation, observability, or audit evidence. At that point, solving every use case separately creates more work, inconsistent controls, or unnecessary risk.

The number of agents is a poor threshold. A company may have one hundred experiments and no platform problem. The same company may have only two agents in production that handle sensitive data and already need strict controls. The difference is whether a constraint repeats, what happens when it is ignored, and whether a shared capability would remove more work than it creates.

Even then, the answer may be to extend a platform that already exists. I would consider a dedicated AI platform only when existing systems can't remove the repeated constraint without every team rebuilding the same AI-specific components.

### What Is Actually Repeating?

Repeating work doesn't always look the same. I have seen two examples often enough to be useful here.

Non-engineers such as analysts and product managers use Claude Code or Codex to build something useful, perhaps a dashboard. It works on their machine. Making it available to others means connecting it to company data and deploying it to the company runtime. At Vipps, services follow a contract that engineers receive through the internal developer portal. Using that contract still requires engineering experience, so the platform team helps each new builder through much of the same work.

The second example is simpler. Engineers build AI-powered Slack apps and ask for an API key to an LLM. The request takes little time, but handing out a key doesn't provide cost attribution, data controls, evaluation, or useful observability.

The work is not identical. The first example repeats deployment support. The second repeats access without the controls other stakeholders need. Both may be platform candidates.

AI Playground removes part of the first problem. A builder visits our internal developer portal, gives an agent a name, and receives a repository with a working agent deployed to the test environment. The builder also receives a starter prompt for a coding agent. The value is not the button in the portal. It is the repeated setup that the template removes.

### When Does Repeated Work Justify a Shared Solution?

Teams may repeat work because they are still learning. Centralizing it too early can turn useful experiments into a shared solution nobody needs. I would treat repetition as a meaningful constraint only when it blocks a valuable workflow and produces a visible consequence:

- **Incidents and recovery:** Does the repeated constraint cause preventable incidents, or make incidents harder to detect, contain, and recover from?
- **Audit effort:** Does every team have to reconstruct the same evidence differently, and how much effort does that require?
- **Cost:** What does the constraint cost through duplicated implementation, infrastructure use, waiting, support, and rework?
- **Reliability:** Do local solutions fail inconsistently, make failures difficult to observe, or make dependable recovery difficult?
- **Risk:** What are the consequences of getting this work wrong, and how widely could those consequences spread?

Before I build a shared capability, I should also ask whether the workflow or constraint should exist at all. The apparent platform problem may be unclear ownership, missing training, unnecessary variation, a poor procurement choice, or a workflow that should simply be removed. Platforms can standardize work that nobody needed.

My next test is whether a simpler solution removes the constraint. The order is important: documentation, a convention, a template, a library, a CLI, and only then a narrow managed capability.

A shared capability becomes platform-like when teams choose it as the standard option because it is easier and safer than solving the problem locally. Adoption by mandate can make a platform common without making it useful.

Someone still has to own and maintain the shared capability. If that costs more than the coordination and risk it removes, the platform has moved the work instead of creating leverage.

## Chapter 2: What Does "Smallest" Mean?

It is tempting to measure the size of a platform by counting its features, services, or lines of configuration. By that measure, a YAML file is smaller than a gateway, and a gateway is smaller than a runtime.

A small central contract can still force every team to build adapters, reconstruct audit evidence, and explain the same fields differently. A broad managed runtime can hide servers behind a vendor invoice while creating a permanent on-call responsibility and a high cost to leave. Both may look small from the platform team's perspective.

I need a definition that counts the work done by the platform team and the teams using the platform:

> The smallest useful AI platform is the shared capability that creates the least total work, lets a defined group complete one valuable workflow, meets the minimum required controls, and remains cheaper to change or remove than the repeated work it removes.

This gives "smallest" four tests:

| Test | Question |
| --- | --- |
| Outcome | Does it remove the measured constraint and let the intended user complete the job? |
| Risk | Does it provide the minimum controls required by the data, authority, reversibility, and possible impact? |
| Total work | Does it reduce central and local integration, support, audit, incident, migration, and exception work? |
| Change and removal | Can its contracts, state, evidence, and users be changed or retired at an acceptable cost? |

"Smallest" in that sense is the simplest solution that passes all four tests for a particular workflow.

### Could the Smallest Platform Begin With a Contract?

My current candidate is a narrow platform capability built around a versioned agent contract. The contract alone is not the platform. The candidate also includes validation in CI, connections to the systems that own operational facts, and a view in the developer portal.

The first workflow I want to test is an internal, read-only agent. Its contract would declare only the information needed to make that workflow accountable and observable:

- the agent's identity, purpose, owner, and lifecycle
- its risk class and the kind of data it may use
- references to approved model access and the application runtime
- identifiers that connect its runs to cost and traces
- an evaluation reference
- an incident contact and instructions for disabling the agent

This is smaller than a general contract for every kind of agent. High-impact actions, tool approvals, accepted exceptions, and retained evidence can be added when a workflow requires them. They don't need to be part of the first test.

### Which System Owns Each Fact?

The contract shouldn't become a second source for facts that another system already knows. It should declare stable information and point to operational facts where they are produced.

| Kind of fact | Examples | Source |
| --- | --- | --- |
| Declared with the code | Purpose, owner, lifecycle, risk class, allowed data, model-access reference, incident contact | Agent contract |
| Observed while building or running | Deployed revision, evaluation result, traces, cost | CI, delivery, evaluation, observability, and billing systems |
| Confirmed by an accountable owner | Approval, accepted exception, review decision, expiry | The system where that decision is made |

The developer portal can combine these facts into one view without copying all of them into the repository. The contract can contain identifiers and requirements. The original systems remain responsible for the current state.

This separation is important. A team can declare which revision it expects to run. Only the delivery system can show which revision is running. A team can reference an evaluation. Only the evaluation system can show whether the current revision passed it.

### How Should the Minimum Change With Risk?

The controls an agent needs should depend on the consequences of getting it wrong. An experiment using public data and taking no external action doesn't need the same controls as an agent that moves money or changes production infrastructure.

I find four working classes useful. The controls are cumulative. Each class adds to the controls required by the classes above it.

| Class | Example | Additional shared controls |
| --- | --- | --- |
| Experiment | Local prototype using synthetic or public data | Owner, purpose, lifecycle, access guidance, and deletion date |
| Internal read-only | Search, summarization, or drafting with internal data | Data class, provider and region, evaluation reference, trace and cost correlation, and incident contact |
| Reviewed action | Drafts a ticket, code change, or transaction for approval | Tool permissions, identity for each run, approval rule, audit log, rollback where possible, incident instructions, and a way to disable the agent |
| High-impact action | Customer, financial, employment, safety, regulated, or privileged action | Accountable risk owner, formal evaluation threshold, isolation, ongoing monitoring, retained evidence, and independent approval |

Reversibility is a separate property. An action can require review and still be difficult to reverse. That consequence should affect its risk class and the controls applied to it.

### Who Defines and Enforces a Control?

A shared control has four different responsibilities:

| Responsibility | Owner |
| --- | --- |
| Decide which outcome is required | The person accountable for the harm or obligation |
| Define representative cases and evidence | The team that understands the workflow |
| Encode and validate the shared rule | The platform capability |
| Prevent a disallowed action | A system that has the context and authority to stop it |

The enforcement point must be one the workflow cannot bypass and must have enough context and authority to prevent the harm. A gateway can enforce allowed model providers and processing regions if direct provider access is unavailable. A deployment system can require evaluation evidence before releasing an agent. A downstream service must authorize a business action using the identity and authority of that run.

The contract connects these decisions. It doesn't replace enforcement. It can't stop a running agent from using a credential with too much access.

### Which Interface Is Smallest?

A platform needs an interface. It doesn't necessarily need its own graphical interface.

| User and job | Likely first interface |
| --- | --- |
| Engineer registers or changes an agent | Versioned file with editor and CI feedback |
| Engineer creates a standard repository | Template or CLI using the same schema |
| Occasional or non-engineer builder configures a limited workflow | Existing form, low-code interface, chat, or generated pull request |
| Domain expert evaluates outputs | Review and annotation interface |
| Risk owner approves an action | Existing approval interface close to the downstream system |
| Finance, audit, or incident response inspects agents | Existing portal or report using data from the original sources |
| Another system consumes metadata | API or export |

The interface depends on the user and the job. Giving finance or incident response raw records would only move the work of connecting those records to them.

## Chapter 3: Where Should the Platform End?

The contract gives the candidate a possible beginning. It doesn't decide which capabilities the platform team should own.

| Capability | What could be shared | What should remain elsewhere |
| --- | --- | --- |
| Model access | Credentials, quotas, cost attribution, trace correlation, and a common interface | Existing identity and secret systems; the workflow team's model choice, prompts, fallback behavior, and product outcome |
| Tools | Common rules for exposing tools, origin and ownership information, authentication patterns, and audit fields | Business rules, data access, side effects, authorization, support, and repair |
| Identity | Agent identity metadata, delegated-user context, requested permissions, and a way to revoke access | The existing identity platform issues identities and credentials; the resource owner decides whether a business action is allowed |
| Evaluation | A common runner, formats, scheduling, history, and reusable evidence | The domain team defines representative cases, possible harm, acceptance levels, and whether a release is good enough |
| Observability | Shared trace fields that connect models, tools, evaluations, cost, and workflows | The existing observability platform handles the data; the product team defines service levels, alerts, and the meaning of a failure |
| Deployment | A common description of the agent, its dependencies, evaluation evidence, and rollback reference | The existing delivery platform deploys and runs it; the product team decides when to release and whether a rollback is safe |

The AI platform can define common parts and connect them to systems the organization already uses. Decisions that depend on the workflow should stay with the team that understands it.

An AI gateway or common evaluation service doesn't become necessary because the workflow uses an LLM. I would add one when it removes measured repeated work or provides a required control that the contract and existing systems can't provide.

### When Is a Contract Not Enough?

A contract can be small and still create a large amount of work. Every team may still need to build an adapter, collect evidence, understand errors, and fix outdated information. The contract then describes the work in the same way for every team. It doesn't remove the work.

I would move beyond the contract when teams still need the same help, keep rebuilding the same components, or need a control that only works while the agent is running. The next capability could be a generator, evaluation service, AI gateway, authorization service, or dedicated runtime. The repeated work should decide the priority.

### Should the Platform Own Integrations?

I would start by defining how integrations are exposed. Owning them comes later. A common pattern can describe authentication, timeouts, retries, duplicate requests, versions, traces, ownership, and retirement.

I would move an integration into the platform when several teams need the same stable behavior and someone has the knowledge and time to support it. That owner must be able to diagnose failures in the downstream system, support new versions, respond to incidents, and remove the integration later.

### What Should the Platform Not Provide?

The candidate I am describing should not:

- define one agent framework, prompt pattern, memory system, or orchestration model
- own product prompts, domain tools, business evaluation rules, or the definition of acceptable harm
- authorize a tool just because it appears in a catalogue
- store prompt and tool payloads by default when metadata, sampling, or redaction is enough
- force experiments through controls designed for high-impact production actions
- run agents before repeated runtime problems justify the work required to operate them

These limits are intentional. I would add one of these capabilities only after a measured constraint shows that leaving it outside creates more work or risk.

## Chapter 4: How Can the Platform Preserve Freedom?

A useful platform gives teams an easier way to work. It becomes a problem when that way is the only practical option.

A team may depend on the platform for model access, deployment, observability, support, and cost attribution. If the team loses these when it chooses something else, it must rebuild the surrounding work first. The freedom to leave exists, but the path may be too expensive to use.

Freedom needs a usable path forward.

### How Can Teams Change or Extend the Platform?

I would want three paths for a need the platform doesn't yet support:

| Path | When it fits |
| --- | --- |
| Local extension | One workflow needs a provider-specific field, adapter, or check that doesn't change the shared contract |
| Shared contribution | Several teams need the same capability and someone can maintain it as part of the platform |
| Alternative implementation | The need doesn't fit the platform's direction, but the workflow can still provide the required outcomes |

The shared contract needs versioning and compatibility rules so that one contribution doesn't break every consumer. Local extensions should be visible and namespaced. A shared contribution needs an owner, support expectations, tests, and a way to remove it later.

The platform team may still reject a contribution because it creates too much support work, weakens a boundary, or serves only one workflow. The team proposing it should still have a supported way forward when the required controls can be met another way.

Freedom includes the ability to leave. It also includes the ability to improve the system people still choose to use.

### How Can Teams Stop Using the Platform?

Leaving still creates work. Prompts, tool schemas, evaluations, configuration, state, logs, and retained evidence may need to move or be recreated. Old access needs to be revoked. The team may need to run both options during migration.

The platform preserves freedom by making this work visible, supported, and possible. A practical alternative path needs:

- access to the existing identity, deployment, observability, incident response, and cost systems
- a way to show that required controls still work
- an export or reconstruction plan for state and evidence
- a named owner and budget for migration and temporary parallel operation
- a way to revoke the old path and return if the replacement fails

An exception shouldn't mean that a team is left alone. If only the standard platform receives normal support and audit recognition, using another implementation is not a real choice.

### When Should a Capability Be Removed?

I would reduce a capability when a simpler option achieves the same outcome and risk result. I would replace it when another option provides the capability at lower total cost and preserves the information needed to move. I would remove it when the original constraint has disappeared and every remaining user has a tested alternative or intentionally needs no replacement.

Removal is still a product change. It needs retention decisions, migration support, rollback, communication, and a budget. The cost of leaving is part of the cost of the platform.

## Chapter 5: Can a Prototype Show Whether the Candidate Works?

My current candidate is a versioned agent contract stored with the code, validated in CI, connected to the systems that own operational facts, and displayed through the existing developer portal. I want to test it with one internal, read-only agent and one end-to-end workflow:

1. An engineer creates or changes the agent from a repository.
2. CI validates its declared identity, owner, purpose, lifecycle, risk class, data class, model-access reference, runtime reference, cost identifier, trace identifier, evaluation reference, incident contact, and disable instructions.
3. Delivery, evaluation, observability, and billing systems provide the facts they observe.
4. The existing developer portal combines the declarations, current facts, and links to their sources.
5. The agent continues to run on the existing application platform.

The candidate succeeds only if the engineer can complete the standard workflow without repeated platform-team help, finance can attribute the cost, and an incident responder can find the owner, running revision, traces, incident instructions, and a way to disable the agent without reconstructing them by hand.

Before building it, I need a baseline for the work it is meant to remove:

- time from repository creation to a registered and observable deployment
- waiting time and number of manual platform-team interactions
- time needed to attribute the agent's model cost
- time needed to identify the running revision, owner, and incident procedure

I also need to measure the work the candidate creates:

- time spent building, maintaining, supporting, and operating the shared capability
- local integration, adapter, evidence, and exception work for each team
- number of stale or conflicting facts and the time needed to correct them
- ongoing infrastructure and supplier cost per registered agent
- number of bypasses, forks, and unsupported workflows
- estimated work required to export, replace, or remove the capability

The candidate fails if documentation or a template would remove the same work, if its data becomes unreliable, if every consumer needs a custom adapter, if teams still need repeated help, or if it creates more total work than it removes. It also fails for a workflow whose required controls can only be enforced while the agent is running.

The result may show that the candidate is too broad. It may also show that a contract isn't enough and that the next useful capability is a generator, AI gateway, authorization service, or evaluation service.

## Conclusion

I don't know the answer until I test the candidate with an actual workflow.

My current candidate is not a smaller copy of a broad AI platform. It is a narrow shared capability built around a versioned contract, connected to systems the organization already operates, with only the controls required by the first workflow.

The prototype should be able to prove this candidate wrong. That is how I can learn whether it is a platform that removes repeated work, a contract that only describes the work, or more capability than the workflow needs.

## Emerging Principle

> Build a platform only when it removes more total work than it creates.

A platform creates leverage when a capability built once removes work repeatedly. It preserves engineering freedom when people can still change it, extend it, replace it, or leave.

A useful platform needs both.
