---
title: What Is the Smallest AI Platform That Could Possibly Work?
date: 2026-07-27
excerpt: Under exploration.
published: false
---

# What Is the Smallest AI Platform That Could Possibly Work?

## Chapter 1: What Problem Would a Platform Solve?

### What problem is an AI platform actually solving?

Today, many organizations run some form of AI adoption initiative with the goals of working more efficiently and creating better or entirely new products with AI. As a result, more people consume external AI services and create AI agents that use LLMs, skills, or integrations with internal and external MCP servers. For simplicity, I refer to all of these as AI agents, or just agents.

Here are the recurring areas where I see an increase in questions and demand because of such AI adoption initiatives:

- Developers ask for access to LLMs for their agents
- Finance wants to know how much these AI agents cost by area, team, product, or agent
- Compliance wants control over data flows and asks for governance and audit evidence

These are only some of the most obvious points I have seen. Other less obvious but still recurring areas of work include:

- Developers ask for AI evaluation and testing tools
- Incident response teams ask for observability into AI agents
- Leaders ask how their teams are doing with AI adoption

None of these requests alone justifies an AI platform. One team asking for model access has an access problem. One finance department asking about a bill has an accounting problem. A collection of experiments does not become a platform problem just because the experiments use AI.

The threshold is crossed when teams repeatedly need the same access controls, cost attribution, evaluation, observability, or audit evidence. Solving each use case separately would creates more work, inconsistent controls, or unnecessary risk.

The number of agents is therefore a poor threshold. A company may have one hundred experiments and no platform problem. The same company may have only two agents in production that handle sensitive data and already need strict controls. What matters is whether a constraint has repeated, whether its consequences matter, and whether a shared capability would retire more work than it creates.

Even then, the answer may be to extend the existing platform to a degree. A dedicated AI platform becomes justified only when those systems cannot remove the repeated constraint without every team rebuilding the same AI-specific machinery.

### What becomes difficult when teams build agents without an AI platform?

The most common request I see is access to LLMs. While it is easy to hand over API keys and make engineers happy immediately, this does not meet most of the important demands from other parts of the organization. Finance does not know who is using which model or why. They just get a bill. Compliance does not know what data is flowing where. Nobody tells them. In the event of an incident, the incident response teams cannot help because they are blind. There is nothing useful to observe.

Here is an example I see again and again. An engineer builds a PR review agent using the best AI frontier model with extra-high reasoning effort. Such an agent solves an immediate and obvious problem for the team. However, it neglects other dimensions and stakeholders, including the cost-to-value ratio, the rules and constraints governing the review, and how other teams can learn from it or build their own PR review agents.

A central AI platform must therefore account for important or all stakeholders such as finance, compliance, procurement, governance, and auditing.

### Does an AI platform actually help engineers and non-engineers build agents faster and more consistently?

An AI platform can help engineers and non-engineers build agents. I use the word "can" because its usefulness depends on the platform's ambitions and the problems it is meant to solve. At Vipps, we created an agent builder and called it Ai playground. You visit our internal developer portal (IDP), click a button, and give your new agent a name. The result is a repository with a functional agent shell that is deployed to the test environment. As the agent engineer, you then receive a starter prompt for your coding agent. The coding agent clones the repository and asks what to do next. From there, you can start vibe coding. We are adding more capabilities to meet the demands from the other stakeholders as well.

You could argue that enabling non-engineers to create agents is a recurring problem that Vipps has addressed and is therefore part of the AI platform. However you may think about it, it solves at least one recurring work. And that is the point of an Ai platform I'd argue. Non-engineers don't need to bother engineers to repeatedly build the foundation of agents with all of the stakeholder's demands; they probably wouldn't know about those anyway.

## Chapter 2: When Does Shared Work Become a Platform?

- When does repeated work justify a shared platform?
- Could documentation, conventions, and reusable libraries solve the problem instead?
- central counterargument
- A sharper decision rule: identify the repeated constraint blocking a valuable workflow, then add the smallest shared capability that removes it.
- Who does not need an AI platform?
- When would an AI platform create more friction than it removes?

## Chapter 3: What Does "Smallest" Mean?

- What is the minimum capability that must be shared?
- What can be removed without preventing users from succeeding?
- Does the smallest platform need a user interface?
- Does it need to run agents, or only help teams build them?
- Could the smallest platform be a set of contracts rather than a deployed system?
- What should the platform deliberately not provide?

## Chapter 4: Where Should the Platform End?

- Are model access, tools, identity, evaluation, observability, and deployment all platform responsibilities?
- Which of those capabilities are necessary from the beginning?
- Should the platform own integrations, or only define how integrations are exposed?
- Are MCP-related tools part of an AI platform?
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
