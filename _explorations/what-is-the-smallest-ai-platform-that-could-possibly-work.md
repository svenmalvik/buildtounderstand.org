---
title: What Is the Smallest (AI) Platform That Could Possibly Work?
date: 2026-07-27
excerpt: Under exploration.
published: false
---

# What Is the Smallest (AI) Platform That Could Possibly Work?

## Question

At Vipps, the most common request I see is access to LLMs. Giving an engineer an API key is easy. The key solves the engineer's problem. Finance gets a bill it cannot attribute, compliance gets a data flow it cannot see, and incident response gets a system it cannot observe. The key is small. The work around it is not.

This made me ask two questions. When does recurring work justify a shared platform? If it does, what is the smallest form that platform could take?

This exploration uses AI agents as the current case. By agents, I mean software built with LLMs, skills, and integrations with internal or external tools. Underneath the technology is a broader question: When does a shared system create leverage, and when does it merely centralize work and reduce freedom?

## Exploration

### What Problem Would a Platform Solve?

Organizations want engineers and non-engineers to build useful agents. This creates recurring demands. Developers need model access, evaluation tools, and a path to deployment. Finance wants cost attribution. Compliance wants control over data flows and audit evidence. Incident response needs something useful to observe.

None of these requests alone justifies an AI platform. One team asking for model access has an access problem. One finance department asking about a bill has an accounting problem. A collection of experiments does not become a platform problem just because the experiments use AI.

The threshold is crossed when teams repeatedly need the same access controls, cost attribution, evaluation, observability, or audit evidence. Solving each use case separately creates more work, inconsistent controls, or unnecessary risk.

The number of agents is therefore a poor threshold. A company may have one hundred experiments and no platform problem. The same company may have only two agents in production that handle sensitive data and already need strict controls. What matters is whether a constraint has repeated, whether its consequences matter, and whether a shared capability would remove more work than it creates.

Even then, the answer may be to extend an existing platform first. A dedicated AI platform becomes justified only when existing systems cannot remove the repeated constraint without every team rebuilding the same AI-specific machinery.

Here is an example I see again and again. An engineer builds a PR review agent using the best available frontier model with extra-high reasoning effort. The agent solves an immediate and obvious problem for the team. However, it neglects the cost-to-value ratio, the rules and constraints governing the review, and how other teams can learn from it or build their own PR review agents.

The first version works. The organization inherits the second version.

#### Can a Platform Help People Build Agents?

An AI platform can help engineers and non-engineers build agents. I use the word "can" because its usefulness depends on the platform's ambitions and the problems it is meant to solve. At Vipps, we created an agent template called AI Playground. You visit our internal developer portal (IDP), click a button, and give your new agent a name. The result is a repository with a functional agent shell already deployed to the test environment. As the agent engineer, you then receive a starter prompt for your coding agent. The coding agent clones the repository and asks what to do next. From there, you can start vibe coding. We are adding more capabilities to meet the needs of other stakeholders as well.

Whether this makes agent creation part of the AI platform is partly a matter of definition. It does solve one recurring problem. Non-engineers no longer need to ask engineers to rebuild the same foundation for every agent. They also start with the requirements of other stakeholders already included, even if they do not know about them. That, I think, is the point of an AI platform.

### When Does Shared Work Become a Platform?

#### What Is Actually Repeating?

Repeating work looks different from team to team. I have seen two examples often enough to be useful here.

Non-engineers such as analysts and product managers use Claude Code or Codex to build something useful, perhaps a dashboard. It works on their machine. Making it available to others means connecting it to company data and deploying it to the company runtime. At Vipps, services follow a contract that engineers receive through the internal developer portal. Using that contract still requires engineering experience, so the platform team helps each new builder through much of the same work.

The second example is simpler. Engineers build AI-powered Slack apps and ask for an API key to an LLM. The request takes little time, but handing out a key does not provide cost attribution, data controls, evaluation, or useful observability.

The work is not identical. The first example repeats deployment support. The second repeats access without the controls other stakeholders need. Both may be platform candidates. Repetition alone proves very little.

#### When Does Repeated Work Justify a Shared Solution?

Teams may repeat work because they are still learning. Centralizing it too early can turn useful experiments into a shared solution nobody needs. Repetition becomes a meaningful constraint when it blocks a valuable workflow and produces a visible consequence:

- **Incidents and Recovery:** Does the repeated constraint cause preventable incidents, or make incidents harder to detect, contain, and recover from?
- **Audit Effort:** Does every team have to reconstruct the same evidence differently, and how much effort does that require?
- **Cost:** What does the constraint cost through duplicated implementation, infrastructure consumption, waiting, support, and rework?
- **Reliability:** Do local solutions fail inconsistently, create operational blind spots, or make dependable recovery difficult?
- **Risk:** What are the consequences of getting this work wrong, and how widely could those consequences spread?

There is no useful universal threshold based on the number of teams, agents, models, or requests. Two production agents handling sensitive data may justify shared controls. One hundred experiments may not.

#### Could the Work Be Removed Instead?

Before building a shared capability, I should ask whether the workflow or constraint should exist at all. The apparent platform problem may be unclear ownership, missing training, unnecessary variation, a poor procurement choice, or a workflow that should simply be removed.

Calling it a platform problem too early gives the solution a shape before the cause is understood. Platforms are quite capable of standardizing work that nobody needed.

#### Could Documentation, Conventions, or Reusable Libraries Be Enough?

The next test is whether a lighter solution removes the constraint. The order matters: documentation, a convention, a template, a library, a CLI, and only then a narrow managed capability.

Small teams may need no more than a repository template and a CLI. Expensive or risky concerns such as identity, policy, databases, or audit evidence are stronger candidates for a managed service. The goal is not to build the smallest possible platform department. It is to use the lightest option that completes the work.

#### When Does a Shared Capability Become a Platform?

A shared capability becomes platform-like when teams choose it as the common path because it is easier and safer than solving the problem locally.

I am interested in whether the capability removes enough repeated work to justify the work it creates. Someone still has to own and maintain it. If that costs more than the coordination and risk it removes, we have built a new and maybe even larger problem.

The first justified AI platform may therefore be a gateway, evaluation service, policy check, trace convention, cost-attribution layer, or deployment contract. It does not need to begin as one broad integrated product labelled as an AI platform.

#### Who Does Not Need an AI Platform?

An AI platform is probably premature when there is only one team, few production workflows, or no valuable use case yet. It is also a poor answer when the real problems are skills, data access, or workflow design. A team must first understand its work well enough to describe the workflow. Only then can it decide what should be automated.

A dedicated AI platform also needs clear ownership, support, upgrades, and deprecation. That is an investment, not a side effect.

#### When Does a Platform Create More Friction Than It Removes?

Warning signs include adoption by mandate, long waits for users, and teams forking or bypassing the platform.

#### How Would We Know the Platform Helped?

##### What Was the Baseline?

Before introducing a shared capability, ask how often the constraint occurred. Measure workflow completion time, waiting time, duplicated implementations, incidents, audit effort, and cost per successful outcome.

##### What Changed?

Did more common cases complete without extra help? Did waiting, incidents, audit effort, or cost improve?

##### What New Costs and Risks Did the Platform Introduce?

Count platform staffing, support, maintenance, on-call load, switching cost, and common failure risk. We should also decide what would make us remove it again. The original problem may disappear or become less important. If the platform no longer removes enough work to justify its cost, we should remove it or the parts that no longer help.

### What Does "Smallest" Mean?

#### Is the Smallest Platform the One With the Fewest Features?

It is tempting to measure the size of a platform by counting its features, services, or lines of configuration. By that measure, a YAML file is smaller than a gateway, and a gateway is smaller than a runtime.

This leaves out most of the work.

A small central contract can force every team to build adapters, reconstruct audit evidence, and explain the same fields differently. A broad managed runtime can hide its servers behind a vendor invoice while creating a common failure domain, a permanent on-call dependency, and an expensive exit. Both may look small from the platform team's side of the fence. The fence is doing quite a lot of work.

I need a definition that counts the whole system:

> The smallest useful AI platform is the lowest-total-work shared capability that lets a defined group complete one valuable workflow, meets that workflow's risk floor, and remains cheaper to change or remove than the work it displaces.

This gives "smallest" four tests:

| Test | Question |
| --- | --- |
| Outcome | Does it remove the measured constraint and let the intended user complete the job? |
| Risk | Does it provide the minimum controls required by the data, authority, reversibility, and impact involved? |
| Total work | Does it reduce central and local integration, support, audit, incident, migration, and exception work? |
| Reversibility | Can its contracts, state, evidence, and consumers be changed or retired at an acceptable cost? |

The smallest platform is therefore not a fixed product category. It is the lowest rung that passes all four tests for a particular workflow.

#### What Is the Minimum Capability That Must Be Shared?

My current hypothesis is that the first useful shared capability is not an agent runtime or a new AI portal. It is a versioned agent contract beside the code, backed by validation and consumed by systems the organization already operates.

The contract would describe at least:

- identity, purpose, ownership, and lifecycle
- the risk class and data classifications
- runtime and deployment references
- model providers, allowed models, and regions
- tools, required scopes, and authorization mode
- evaluation suite, version, owner, and latest result
- runbook, incident contact, and a way to disable the agent
- trace, cost, and product or workflow identifiers
- review, expiry, and exception evidence

This is already more than a catalogue entry. It connects the agent to decisions made by delivery, security, finance, compliance, and incident response. Every required field needs a named owner, an authoritative source, a consumer, and a decision that the consumer makes from it. A field with no consumer is decoration. Enough decorative fields and we have built a questionnaire.

The source of a field matters as well. Some facts are **declared** by the team, some are **observed** by CI or the runtime, and some are **attested** by an independent owner. These are not interchangeable. A repository can declare that an agent is approved or that a particular revision is running. This does not make either claim true.

The contract therefore needs schema checks, valid and invalid examples, compatibility tests for its consumers, and a deprecation policy. It also needs an owner. A contract without this machinery is documentation with better punctuation.

[Backstage's catalogue format](https://backstage.io/docs/features/software-catalog/descriptor-format/) already provides a useful versioned envelope and a source-controlled ownership workflow. The smallest AI-specific addition could be an `Agent` kind or attached metadata that Backstage renders while CI, observability, FinOps, and deployment systems remain authoritative for the facts they already know.

#### How Should the Minimum Change With Risk?

The minimum follows consequence, not the word "agent." An experiment using public data and taking no external action does not need the same controls as an agent that moves money or changes production infrastructure.

I find four working classes useful:

| Class | Example | Minimum shared capability |
| --- | --- | --- |
| Experiment | Local prototype using synthetic or public data | Owner, purpose, lifecycle, access guidance, and deletion date |
| Internal read-only | Search, summarization, or drafting with internal data | Data class, provider and region, evaluation reference, trace and cost correlation, and incident contact |
| Reversible action | Drafts tickets, code changes, or bounded transactions for review | Tool scopes, per-run identity, approval rule, rollback, audit log, runbook, and kill switch |
| High-impact action | Customer, financial, employment, safety, regulated, or privileged action | Accountable risk owner, formal evaluation threshold, isolation, ongoing monitoring, retained evidence, and independent approval |

This is an operating model to test, not a universal taxonomy. The important point is that a higher class raises the control floor. It does not automatically require one central runtime.

The control should be enforced at the latest boundary where harm can still be prevented. A missing description can produce a warning. An invalid owner reference can fail CI. Missing approval for a production agent can block deployment. A consequential tool action must be authorized by the downstream system using the identity and authority of that run. A green catalogue entry is not permission to transfer money.

This distinction matters because contracts and enforcement do different jobs. A contract can define vocabulary, validate shape, maintain compatibility, and support admission decisions. It cannot stop a running agent from using an overpowered credential. [NIST's work on agent hijacking](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations) and [OWASP's guidance on excessive agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html) both point toward downstream authorization for consequential actions.

#### What Can Be Removed Without Preventing Users From Succeeding?

The useful sequence is:

> documentation → template → contract → conformance checks → admission control → gateway → shared runtime

Start at the left. Keep the first rung that lets the intended user complete the workflow and meets the risk floor. Do not continue climbing because the architecture diagram still has room.

This means reusing existing identity, deployment, observability, incident response, billing, and data-governance systems wherever they can do the job. The AI platform should add an AI-specific capability only when the existing system cannot provide it without several teams rebuilding the same consequential machinery.

Subtraction also has to include local work. Removing a central evaluation service is not a saving if every team now creates its own scripts, spreadsheets, review interface, and evidence store. Google illustrated this problem in its paper on [hidden technical debt in machine learning systems](https://research.google/pubs/hidden-technical-debt-in-machine-learning-systems/): model code can be a small part of a production ML system while the surrounding glue carries most of the weight.

The better question is not "How little can the platform team own?" It is "Which arrangement produces the least total work per successful, governed outcome?"

#### Does the Smallest Platform Need a User Interface?

It needs an interface. It does not necessarily need its own graphical interface.

An engineer may be well served by reviewed YAML with editor and CI feedback. A common repository may need only a template or CLI. Another system needs an API or export, not a portal page that it can admire during office hours.

Other users have different jobs. A domain expert comparing agent outputs may need a purpose-built review interface almost immediately. A risk owner may need evidence and approval controls in the existing system where the consequential action happens. Finance, audit, and incident response may need a fleet view in Backstage or another existing portal because raw records make them repeat the same reconciliation.

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

[Google's definition of an internal developer platform](https://cloud.google.com/solutions/platform-engineering) explicitly allows for a platform with or without a portal. That seems right. Building a portal before finding the user job mostly gives the platform a homepage.

#### Does the Smallest Platform Need to Run Agents?

Helping teams build agents and running those agents are different commitments.

A build-enabling platform can provide approved access patterns, metadata, repository templates, evaluation hooks, telemetry conventions, deployment hooks, and discovery. Execution can remain on the existing application platform.

A shared runtime must additionally own per-run identity, tool authorization, queues, retries, timeouts, idempotency, cancellation, streaming, quotas, isolation, state, recovery, human approvals, capacity, SLOs, on-call, incident response, evidence retention, and decommissioning. That is not one more feature. It is an operating model.

Several teams building agents does not prove that the platform should run them. The boundary should move only when several teams repeatedly rebuild the same runtime responsibility, the consequence matters, and central ownership reduces total work or risk after support, migration, and common failure costs are counted.

[Anthropic's guidance on building effective agents](https://www.anthropic.com/engineering/building-effective-agents) recommends simpler workflows when they are sufficient. The platform should preserve that choice. It should not require an agent runtime for software that did not need to become an agent in the first place.

#### Could the Smallest Platform Be a Contract?

Yes, but only if the contract removes real work.

A versioned agent descriptor, validated in CI and displayed through Backstage, could solve ownership, discovery, cost allocation, lifecycle, and evidence problems while agents continue to run on the existing platform. Thin adapters could send the relevant fields to observability, FinOps, and governance systems. This is the smallest credible starting point I can see for the problems described in the first two chapters.

It remains a hypothesis. The contract fails the test if teams cannot complete the workflow without repeated help, if its data goes stale, if every consumer needs a custom adapter, or if a consequential control can only be applied at runtime. In those cases the next smallest answer may be a generator, a narrow authorization service, a model gateway, or an evaluation service.

The contract also has to be removable. Its versions and consumers should be known. One agent record should be exportable and deletable without affecting the running agent. If catalogue metadata becomes required for execution without a deliberate decision, the catalogue has quietly become a runtime dependency. Quiet dependencies are still dependencies.

#### What Should the Platform Deliberately Not Provide?

The initial platform should not:

- define one agent framework, prompt pattern, memory system, or orchestration model
- own product prompts, domain tools, business evaluation rules, or the definition of acceptable harm
- replace existing identity, deployment, observability, incident, billing, or data-governance systems
- build a new portal when Git, Backstage, a template, an existing approval interface, or an API serves the job
- treat self-declared metadata as runtime evidence
- authorize a tool merely because it appears in a catalogue
- store prompt and tool payloads by default when metadata, sampling, or redaction is enough
- force experiments through controls designed for high-impact production actions
- promise indefinite compatibility for unused fields
- mandate adoption to hide an unhelpful path
- run agents before repeated runtime constraints justify the operational burden

These are boundaries, not unfinished roadmap items. Each one should enter the platform only after a measured constraint proves that leaving it outside creates more work or risk.

#### When Should a Capability Be Shrunk, Replaced, or Removed?

Platforms are usually designed as if adoption were a one-way door. A smallest platform needs an exit before it needs a roadmap.

**Shrink it** when a lower rung achieves the same outcome and risk result, most features have no active consumer, exceptions and support do not decline, or execution can return to existing compute while contracts and evidence remain.

**Replace it** when an existing platform or supplier now provides the capability at lower total cost, the replacement preserves identity and evidence, and a representative workload can move without rebuilding product logic or evaluation data. The comparison must include migration and running both systems during the move.

**Remove it** when the original constraint has disappeared, no risk obligation or critical consumer remains, actual usage confirms the long tail is gone, and every real user job has a tested alternative or intentionally no replacement.

Removal is still a product change. It needs retention decisions, migration support, rollback, communication, and money. When the UK Government Digital Service decided to [decommission GOV.UK PaaS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/), it gave users 18 months to migrate. The service was reliable and well liked. It had simply lost its comparative advantage.

That is the standard I want to use here. The smallest AI platform is not a miniature version of a broad one. It is the lightest owned arrangement that produces a successful, governed outcome after central work, local work, risk, and exit are all counted.

## Prototype

### Can a Contract Be Enough?

My current hypothesis is that the smallest useful starting point is a versioned agent contract beside the code, validated in CI and displayed through systems the organization already operates. It should not require a new portal or a shared agent runtime.

I will test this with one internal, read-only agent and one end-to-end workflow:

1. An engineer creates or changes the agent from a repository.
2. CI validates its identity, owner, purpose, lifecycle, risk class, model access, evaluation reference, runtime reference, cost identifier, trace identifier, runbook, and disable mechanism.
3. The existing developer portal displays the contract and links to the authoritative runtime, evaluation, cost, trace, and incident information.
4. The agent continues to run on the existing application platform.

The prototype succeeds only if the engineer can complete the common path without repeated platform-team help, finance can attribute its cost, and an incident responder can find the owner, running revision, traces, runbook, and disable mechanism without reconstructing them by hand.

Before building it, I need a baseline:

- time from repository creation to a registered and observable deployment
- number of manual platform-team interactions
- time needed to attribute the agent's model cost
- time needed to identify the running revision, owner, and incident procedure
- local adapters or duplicate records required outside the contract

The contract is not the answer if its data becomes stale, every consumer needs a custom adapter, teams still need repeated help, or the consequential controls can only be enforced at runtime. In those cases, the next smallest answer may be a generator, a narrow authorization service, a gateway, or an evaluation service.

I should also be able to delete the contract without stopping the agent. If I cannot, I have built a runtime dependency while calling it metadata.

## Conclusion

My answer is provisional until the prototype has survived contact with an actual workflow.

For now, the smallest AI platform that could possibly work is not a miniature version of a broad platform. It is a versioned contract for one repeated and valuable workflow, connected to systems the organization already operates, plus only the enforcement that the workflow's risk requires.

The smallest platform is not the one with the fewest features. It is the shared capability that removes more total work than it creates and remains affordable to change or leave. A contract may satisfy that definition. The prototype may prove that it does not.

The AI-specific parts of this answer will change. The four tests should last longer: Does the platform produce the outcome, meet the risk floor, reduce total work, and preserve a reasonable exit?

## Emerging Principle

> Build a platform only when it removes more total work than it creates.

A platform creates leverage when a capability built once removes work repeatedly. It preserves freedom when people can still change it, extend it, or leave it. A useful platform needs both.
