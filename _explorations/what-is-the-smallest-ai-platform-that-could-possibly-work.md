---
title: What Is the Smallest (AI) Platform That Could Possibly Work?
date: 2026-07-27
excerpt: Under exploration.
published: false
---

# What Is the Smallest (AI) Platform That Could Possibly Work?

At Vipps, one of the most common requests I see is access to LLMs. Giving an engineer an API key is easy. It solves the immediate access problem. However, it doesn't show finance which team created the cost, help compliance understand where the data goes, or give incident response a way to observe the system.

There is always additional work that often comes later, sometimes weeks after the main work. So, when does recurring work justify a platform used by several teams? And if it does, what is the smallest platform that could possibly work?

I am using AI agents as the current case. By agents, I mean software built with LLMs, skills, and integrations with internal or external tools.

## Chapter 1: What Problem Would a Platform Solve?

Organizations want engineers and non-engineers to build useful agents to be either more productive or to create new products. As more people build agents in whatever form, the same needs appear. Developers need model access, evaluation tools, and a path to deployment. Finance needs to know which team created each cost. Compliance needs control over data flows and audit evidence. Incident response needs a system it can observe, and the list goes on.

None of these requests alone justifies an AI platform. One team asking for model access has an access problem. One finance department asking about a bill has an accounting problem. A collection of experiments doesn't become a platform problem just because the experiments use AI.

I start seeing a platform problem when teams repeatedly need the same access controls, a way to connect costs to the teams that created them, evaluation, observability, or audit evidence. At that point, solving every use case separately creates more work, inconsistent controls, or unnecessary risk.

A company may have many experiments and no platform problem. The same company may have only two agents in production that handle sensitive data and already need strict controls. The difference is whether the same problem keeps appearing, what happens when it is ignored, and whether solving it once for several teams would remove more work than it creates.

Even then, the answer may be to extend a platform that already exists. I would consider a dedicated AI platform only when existing systems can't solve the repeated problem without every team rebuilding the same AI-specific components.

### What Is Actually Repeating?

Repeating work doesn't always look the same. I have seen two examples often enough to be useful here.

Non-engineers such as analysts and product managers use Claude Code or Codex to build "something", perhaps a dashboard. It works on their machine. Making it available to others means connecting it to company data and deploying it to the company runtime environment. At Vipps, services follow a contract that engineers receive through the internal developer portal. Using that contract still requires engineering experience.

The second example is simpler. Engineers build AI-powered Slack apps and ask for an API key to an LLM. The request takes little time, but handing out a key doesn't show which team created each cost or provide data controls, evaluation, or useful observability.

The work is not identical. The first example repeats deployment support. The second repeats access without the controls other stakeholders need. Both are problems a platform might solve.

AI Playground removes part of the first problem. A (non-)engineer visits our internal developer portal, gives an agent a name, and receives a repository with a working agent deployed to the test environment. The (non-)engineer also receives a starter prompt for a coding agent. The value is the repeated setup that the template removes.

### When Should Several Teams Use the Same Service?

Teams may repeat work because they are still learning. Centralizing it too early can turn experiments into a service nobody needs. I would consider building one service only when repeated work blocks a useful workflow or creates visible cost, risk, incidents, or audit work.

Before I build a service for several teams, I should also ask whether the workflow is needed or whether the repeated work can be removed. The apparent platform problem may be unclear ownership, missing training, or a workflow that should simply be removed. Platform teams can standardize work that nobody needed.

My next test is whether a simpler solution solves the problem. The order is important: documentation, a convention, a template, a library, a CLI, and only then a concrete managed service.

A service starts to act like a platform when several teams choose it because it is easier and safer than solving the problem on their own. Adoption by mandate can make a platform common without making it useful.

Someone still has to own and maintain that service. If that costs more than the coordination and risk it removes, the platform has moved the work instead of creating leverage.

## Chapter 2: What Is the Smallest Platform, and Where Should It End?

It is tempting to measure the size of a platform by counting its features, services, or lines of configuration. By that measure, a YAML file is smaller than a gateway, and a gateway is smaller than a runtime.

A small central contract can still force every team to build adapters, reconstruct audit evidence, and explain the same fields differently. A broad managed runtime can hide servers behind a vendor invoice while creating a permanent on-call responsibility and a high cost to leave. Both may look small from the platform team's perspective.

I need a definition that counts the work done by the platform team and the teams using the platform:

> The smallest useful AI platform is the system that creates the least total work, lets a defined group complete one valuable workflow, meets the minimum required controls, and remains cheaper to change or remove than the repeated work it removes.

This gives "smallest" four tests:

| Test | Question |
| --- | --- |
| Outcome | Does it solve the measured problem and let the intended user complete the job? |
| Risk | Does it provide the minimum controls required by the data, authority, reversibility, and possible impact? |
| Total work | Does it reduce central and local integration, support, audit, incident, migration, and exception work? |
| Change and removal | Can its contracts, state, evidence, and users be changed or retired at an acceptable cost? |

"Smallest" in that sense is the simplest solution that passes all four tests for a particular workflow.

### The Smallest Platform I Can Justify

The smallest platform I can justify is a narrow service built around a versioned agent contract. The contract alone is not the platform. The service also includes validation in CI, connections to the systems that own operational facts, and a view in the developer portal.

I use an internal, read-only agent to define the initial scope. Its contract declares only the information needed to make that workflow accountable and observable:

- the agent's identity, purpose, owner, and lifecycle
- its risk class and the kind of data it may use
- references to approved model access and the application runtime
- identifiers that connect its runs to cost and traces
- an evaluation reference
- an incident contact and instructions for disabling the agent

This is smaller than a general contract for every kind of agent. High-impact actions, tool approvals, accepted exceptions, and retained evidence can be added when a workflow requires them. They don't need to be part of the initial scope.

### Which System Owns Each Fact?

The contract shouldn't become a second source for facts that another system already knows. It should declare stable information and point to operational facts where they are produced.

| Kind of fact | Examples | Source |
| --- | --- | --- |
| Declared with the code | Purpose, owner, lifecycle, risk class, allowed data, model-access reference, incident contact | Agent contract |
| Observed while building or running | Deployed revision, evaluation result, traces, cost | CI, delivery, evaluation, observability, and billing systems |
| Confirmed by an accountable owner | Approval, accepted exception, review decision, expiry | The system where that decision is made |

The developer portal can combine these facts into one view without copying all of them into the repository. The contract can contain identifiers and requirements. The original systems remain responsible for the current state.

This separation is important. A team can declare which revision it expects to run. Only the delivery system can show which revision is running. A team can reference an evaluation. Only the evaluation system can show whether the current revision passed it.

### How Would This Platform Work?

1. An engineer creates or changes the agent and its contract in a repository.
2. CI validates its identity, owner, purpose, lifecycle, risk class, data class, model-access reference, runtime reference, cost and trace identifiers, evaluation reference, incident contact, and disable instructions.
3. Delivery, evaluation, observability, and billing systems provide the facts they observe.
4. The existing developer portal combines the declarations, current facts, and links to their sources.
5. The agent continues to run on the existing application platform.

### How Should the Minimum Change With Risk?

The controls an agent needs should depend on the consequences of getting it wrong. An experiment using public data and taking no external action doesn't need the same controls as an agent that moves money or changes production infrastructure.

The internal, read-only agent in the initial scope needs a data class, approved provider and region, an evaluation reference, a way to connect each run to its traces and cost, and an incident contact. An agent that takes action may also need tool permissions, identity for each run, approval, an audit log, and a way to disable or reverse the action. The greater the possible harm, and the harder the action is to reverse, the more controls the workflow needs.

### Who Defines and Enforces a Control?

A control used by several teams has four different responsibilities:

| Responsibility | Owner |
| --- | --- |
| Decide which outcome is required | The person accountable for the harm or obligation |
| Define representative cases and evidence | The team that understands the workflow |
| Encode and validate the rule | The platform |
| Prevent a disallowed action | A system that has the context and authority to stop it |

The enforcement point must be one the workflow cannot bypass and must have enough context and authority to prevent the harm. A gateway can enforce allowed model providers and processing regions if direct provider access is unavailable. A deployment system can require evaluation evidence before releasing an agent. A downstream service must authorize a business action using the identity and authority of that run.

The contract connects these decisions. It doesn't replace enforcement. It can't stop a running agent from using a credential with too much access.

### Where Should the Platform End?

The contract gives the platform a possible beginning. It doesn't decide which parts the platform team should own.

| Area | What the platform could provide | What should remain elsewhere |
| --- | --- | --- |
| Model access | Credentials, quotas, a way to connect model usage, costs, and traces to each team, and a common interface | Existing identity and secret systems; the workflow team's model choice, prompts, fallback behavior, and product outcome |
| Tools | Common rules for exposing tools, origin and ownership information, authentication patterns, and audit fields | Business rules, data access, side effects, authorization, support, and repair |
| Identity | Agent identity metadata, delegated-user context, requested permissions, and a way to revoke access | The existing identity platform issues identities and credentials; the resource owner decides whether a business action is allowed |
| Evaluation | A common runner, formats, scheduling, history, and reusable evidence | The domain team defines representative cases, possible harm, acceptance levels, and whether a release is good enough |
| Observability | Standard trace fields that connect models, tools, evaluations, cost, and workflows | The existing observability platform handles the data; the product team defines service levels, alerts, and the meaning of a failure |
| Deployment | A common description of the agent, its dependencies, evaluation evidence, and rollback reference | The existing delivery platform deploys and runs it; the product team decides when to release and whether a rollback is safe |

The AI platform can define common parts and connect them to systems the organization already uses. Decisions that depend on the workflow should stay with the team that understands it.

An AI gateway or common evaluation service doesn't become necessary because the workflow uses an LLM. I would add one when it removes measured repeated work or provides a required control that the contract and existing systems can't provide.

The contract is no longer enough when teams still need the same help, its information becomes unreliable, every system needs a custom adapter, or an important control can only work while the agent is running. The next addition could then be a generator, AI gateway, authorization service, evaluation service, or dedicated runtime. The repeated work should decide which one comes next.

### What Should the Platform Not Provide?

The platform shouldn't define one agent framework, prompt pattern, memory system, or orchestration model. It also shouldn't store prompt and tool payloads by default or force experiments through controls designed for high-impact actions. I would change these limits only after evidence shows that doing so removes more work or risk.

## Chapter 3: How Can the Platform Preserve Freedom?

A useful platform gives teams an easier way to work. It becomes a problem when that way is the only practical option.

A team may depend on the platform for model access, deployment, observability, support, and a way to identify its own model costs. If the team loses these when it chooses something else, it must rebuild the surrounding work first. The freedom to leave exists, but the path may be too expensive to use.

Freedom needs a usable path forward.

Teams should be able to improve the platform, provide the required outcomes through another implementation, or leave. If only the standard platform receives normal support and audit recognition, another implementation isn't a real option.

### How Can Teams Leave or Remove the Platform?

Leaving still creates work. Prompts, tool schemas, evaluations, configuration, state, logs, and retained evidence may need to move or be recreated. Old access needs to be revoked. The team may need to run both options during migration.

The platform preserves freedom by making this work visible, supported, and possible. A practical alternative path needs:

- access to the existing identity, deployment, observability, incident response, and cost systems
- a way to show that required controls still work
- an export or reconstruction plan for state and evidence
- a named owner and budget for migration and temporary parallel operation
- a way to revoke the old path and return if the replacement fails

The same standard applies to the platform itself. I would reduce it when a simpler option achieves the same outcome and risk result. I would replace it when another option does the same work at lower total cost and preserves the information needed to move. I would remove it when the original problem has disappeared and every remaining user has a tested alternative or intentionally needs no replacement.

Removal is still a product change. It needs retention decisions, migration support, rollback, communication, and a budget. The cost of leaving is part of the cost of the platform.

## Conclusion

For the scope explored here, the smallest AI platform I can justify is a narrow service built around a versioned agent contract.

The contract lives with the code and describes the agent's purpose, owner, risk, allowed data, model access, incident response, and how its runs connect to evaluation, traces, and cost. CI validates what the team declares. Delivery, evaluation, observability, and billing systems remain responsible for the facts they already know. The existing developer portal brings those facts together.

This platform doesn't need its own agent runtime, AI gateway, evaluation service, or graphical interface from the beginning. Those parts should be added only when several teams would otherwise repeat the same work or when an important control can't be provided by an existing system.

Its leverage comes from removing repeated setup, coordination, and evidence work. It preserves engineering freedom by leaving product decisions with the teams that understand the workflow and by allowing another implementation to provide the same required outcomes.

The smallest platform is therefore not the one with the fewest features. It is the one that removes the most repeated work while creating the least new ownership and remaining possible to change, replace, or remove.

## Emerging Principle

> Build a platform only when it removes more total work than it creates.
