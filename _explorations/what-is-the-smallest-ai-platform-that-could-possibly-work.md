---
title: What Is the Smallest AI Platform That Could Possibly Work?
date: 2026-07-27
excerpt: Under exploration.
published: false
---

# What Is the Smallest AI Platform That Could Possibly Work?

## Chapter 1: What Problem Would a Platform Solve?

### What problem is an AI platform actually solving?

Today, many organizations run some form of AI adoption initiative to work more efficiently and create better or entirely new products with AI. As a result, more people use external AI services and build AI agents with LLMs, skills, and integrations with internal and external MCP servers. For simplicity, I refer to all of these as AI agents, or just agents.

These initiatives create recurring questions and demands:

- Developers ask for access to LLMs for their agents
- Finance wants to know how much these AI agents cost by area, team, product, or agent
- Compliance wants control over data flows and asks for governance and audit evidence

These are some of the most obvious ones I have seen. Other less obvious but still recurring areas of work include:

- Developers ask for AI evaluation and testing tools
- Incident response teams ask for observability for AI agents
- Leaders ask how their teams are doing with AI adoption

None of these requests alone justifies an AI platform. One team asking for model access has an access problem. One finance department asking about a bill has an accounting problem. A collection of experiments does not become a platform problem just because the experiments use AI.

The threshold is crossed when teams repeatedly need the same access controls, cost attribution, evaluation, observability, or audit evidence. Solving each use case separately creates more work, inconsistent controls, or unnecessary risk.

The number of agents is therefore a poor threshold. A company may have one hundred experiments and no platform problem. The same company may have only two agents in production that handle sensitive data and already need strict controls. What matters is whether a constraint has repeated, whether its consequences matter, and whether a shared capability would remove more work than it creates.

Even then, the answer may be to extend an existing platform first. A dedicated AI platform becomes justified only when existing systems cannot remove the repeated constraint without every team rebuilding the same AI-specific machinery.

### What becomes difficult when teams build agents without an AI platform?

The most common request I see is access to LLMs. It is easy to hand over API keys and make engineers happy immediately, but this does not meet the needs of other parts of the organization. Finance does not know who is using which model or why. They just get a bill. Compliance does not know what data is flowing where. Nobody tells them. During an incident, the response teams cannot help because they are blind. There is nothing useful to observe.

Here is an example I see again and again. An engineer builds a PR review agent using the best available frontier model with extra-high reasoning effort. The agent solves an immediate and obvious problem for the team. However, it neglects the cost-to-value ratio, the rules and constraints governing the review, and how other teams can learn from it or build their own PR review agents.

A central AI platform must therefore account for the needs of finance, compliance, procurement, governance, and audit teams.

### Does an AI platform actually help engineers and non-engineers build agents faster and more consistently?

An AI platform can help engineers and non-engineers build agents. I use the word "can" because its usefulness depends on the platform's ambitions and the problems it is meant to solve. At Vipps, we created an agent template called AI Playground. You visit our internal developer portal (IDP), click a button, and give your new agent a name. The result is a repository with a functional agent shell already deployed to the test environment. As the agent engineer, you then receive a starter prompt for your coding agent. The coding agent clones the repository and asks what to do next. From there, you can start vibe coding. We are adding more capabilities to meet the needs of other stakeholders as well.

Whether this makes agent creation part of the AI platform is partly a matter of definition. It does solve one recurring problem. Non-engineers no longer need to ask engineers to rebuild the same foundation for every agent. They also start with the requirements of other stakeholders already included, even if they do not know about them. That, I think, is the point of an AI platform.

## Chapter 2: When Does Shared Work Become a Platform?

### What Is Actually Repeating?

Repeating work looks different from team to team. I have seen two examples often enough to be useful here.

Non-engineers such as analysts and product managers use Claude Code or Codex to build something useful, perhaps a dashboard. It works on their machine. Making it available to others means connecting it to company data and deploying it to the company runtime. At Vipps, services follow a contract that engineers receive through the internal developer portal. Using that contract still requires engineering experience, so the platform team helps each new builder through much of the same work.

The second example is simpler. Engineers build AI-powered Slack apps and ask for an API key to an LLM. The request takes little time, but handing out a key does not provide cost attribution, data controls, evaluation, or useful observability.

The work is not identical. The first example repeats deployment support. The second repeats access without the controls other stakeholders need. Both may be platform candidates, but repetition alone proves very little.

### When Does Repeated Work Justify a Shared Solution?

Teams may repeat work because they are still learning. Centralizing it too early can turn useful experiments into a shared solution nobody needs. Repetition becomes a meaningful constraint when it blocks a valuable workflow and produces a visible consequence:

- **Incidents and Recovery:** Does the repeated constraint cause preventable incidents, or make incidents harder to detect, contain, and recover from?
- **Audit Effort:** Does every team have to reconstruct the same evidence differently, and how much effort does that require?
- **Cost:** What does the constraint cost through duplicated implementation, infrastructure consumption, waiting, support, and rework?
- **Reliability:** Do local solutions fail inconsistently, create operational blind spots, or make dependable recovery difficult?
- **Risk:** What are the consequences of getting this work wrong, and how widely could those consequences spread?

There is no useful universal threshold based on the number of teams, agents, models, or requests. Two production agents handling sensitive data may justify shared controls. One hundred experiments may not.

### Could the Work Be Removed Instead?

Before building a shared capability, I should ask whether the workflow or constraint should exist at all. The apparent platform problem may be unclear ownership, missing training, unnecessary variation, a poor procurement choice, or a workflow that should simply be removed.

Calling it a platform problem too early gives the solution a shape before the cause is understood. Platforms are quite capable of standardizing work that nobody needed.

### Could Documentation, Conventions, or Reusable Libraries Be Enough?

The next test is whether a lighter solution removes the constraint. The order matters: documentation, a convention, a template, a library, a CLI, and only then a narrow managed capability.

Small teams may need no more than a repository template and a CLI. Expensive or risky concerns such as identity, policy, databases, or audit evidence are stronger candidates for a managed service. The goal is not to build the smallest possible platform department. It is to use the lightest option that completes the work. We can always optimize our solutions later when they have been proved to be valuable.

### When Does a Shared Capability Become a Platform?

A shared capability becomes platform-like when teams choose it as the common path because it is easier and safer than solving the problem locally.

I am interested in whether the capability removes enough repeated work to justify the work it creates. Someone still has to own and maintain it. If that costs more than the coordination and risk it removes, we have built a new and maybe even larger problem.

The first justified AI platform may therefore be a gateway, evaluation service, policy check, trace convention, cost-attribution layer, or deployment contract. It does not need to begin as one broad integrated product and label it Ai platform.

### Who Does Not Need an AI Platform?

An AI platform is probably premature when there is only one team, few production workflows, or no valuable use case yet. It is also a poor answer when the real problems are skills, data access, or workflow design. By workflow design I am primarily thinking of non-technical teams who haven't yet identified how their work can be described as workflows which must clearly come first so you know what you may want to automate later.

A dedicated AI platform also needs clear ownership, support, upgrades, and deprecation workflows. That means an investment you must be comfortable with.

### When Does a Platform Create More Friction Than It Removes?

Warning signs include adoption by mandate, long waiting time for the users, and teams forking or bypassing the platform.

### How Would We Know the Platform Helped?

#### What Was the Baseline?

Before introducing a shared capability, ask, how often did the constraint occur? Measure workflow completion time, waiting time, duplicated implementations, incidents, audit effort, and cost per successful outcome.

#### What Changed?

Did more common cases complete without extra help? Did waiting, incidents, audit effort, or cost improve?

#### What New Costs and Risks Did the Platform Introduce?

Count platform staffing, support, maintenance, on-call load, switching cost, and common failure risk. We should also decide what would make us remove it again. The original problem may disappear or become less important. But ff the platform no longer removes enough work to justify the cost, we need to consider to remove it or parts.

### What Is the Decision Rule?

For each proposed capability:

1. **Workflow:** Is the workflow valuable, used, and owned? If not, stop.
2. **Constraint:** What repeatedly blocks it, and what is the measured consequence?
3. **Cause:** Is the cause technical, organizational, educational, contractual, or regulatory?
4. **Substitute:** Can removal, documentation, a convention, template, library, CLI, or narrow service solve it?
5. **Shared capability:** Can one bounded capability remove the common constraint end to end?
6. **Escape:** Can unusual workloads leave the common path safely?
7. **Measurement:** Does the result remain positive after all operating costs are included?

Shared work becomes a platform when advice and local reuse no longer remove a consequential repeated constraint, and one owned capability can remove it with lower total coordination and risk.

## Chapter 3: What Does "Smallest" Mean?

- What is the minimum capability that must be shared?
- What can be removed without preventing users from succeeding?
- When should a platform capability be shrunk, replaced, or removed?
- Does the smallest platform need a user interface?
- Does it need to run agents, or only help teams build them?
- Could the smallest platform be a set of contracts rather than a deployed system, such as an agent metadata contract consumed by Backstage?
- What should the platform deliberately not provide?

## Chapter 4: Where Should the Platform End?

- Are model access, tools, identity, evaluation, observability, and deployment all platform responsibilities?
- Which of those capabilities are necessary from the beginning?
- Should the platform own integrations, or only define how integrations are exposed?
- Are MCP-related tools part of an AI platform?
- Should the AI platform own the agent catalogue, or only define and publish the agent-specific metadata that the existing developer platform displays?
- Which capabilities should be centralized, and which should remain with individual teams?

## Chapter 5: How Can the Platform Preserve Freedom?

- How can teams escape the platform when their needs differ?
- Could the platform become a bottleneck?
- Who operates it, and what ongoing cost does that create?
- How does it avoid locking teams into one model, vendor, or agent framework?
- Should safety and governance be built into the path or enforced around it?

## Chapter 6: Can the Smallest Platform Survive Contact With a Prototype?

- What is the thinnest end-to-end path from an idea to a running agent?
- What evidence would make us abandon the platform entirely?
