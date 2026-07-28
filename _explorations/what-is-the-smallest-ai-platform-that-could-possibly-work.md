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

I believe that repeating work can be very different from company to company. Below are 2 examples that I see repeatedly.

Non-engineers such as analysts or PMs start to use Claude Code or Codex in the desktop app and vibe code something that they find useful. It might be a dashboard of some sort. Then comes the next step where they typically ask someone for help to connect their service to a data source. That's not unusual even for engineers. What's unusual is the next step. Until now their solution runs on their local machine. But what they want is to make it available to others meaning that the solution must run on the company's runtime environment, so they reach out to the platform team. That's where the work really begins. All services run on Kubernetes in a certain way. We call our applications for VippsServices since they follow a certain contract that engineers get through the IDP as a self service. Knowing how to follow the contract requires some engineering experience. The platform team typically engages with these people and tries to help them.

Another recurring work that is done by engineers we see is the rise of new Ai-powered Slack apps. Those engineers typically ask for no more then an API key to an LLM which is quickly done.

All other requests related to Ai haven't so far been recurring even though I may not remember or have seen all of them.

### When Does Repetition Become a Meaningful Constraint?

Teams including the platform teams may repeat work simply for the sake of learning and gaining experience. Centralizing those work too early may result in solutions nobody really need. Repetition becomes first meaningful when several valuable workflows show similar obstacles or when solving those locally produces no meaningful new understanding, and the consequences are visible. Those consequences may appear in incidents, audit effort, cost, reliability, or risk.

#### Incidents and Recovery

Does the repeated constraint cause preventable incidents, or make incidents harder to detect, contain, and recover from?

#### Audit Effort

Does every team have to reconstruct the same evidence differently, and how much effort does that require?

#### Cost

What does the constraint cost through duplicated implementation, infrastructure consumption, waiting, support, and rework?

#### Reliability

Do local solutions fail inconsistently, create operational blind spots, or make dependable recovery difficult?

#### Risk

What are the consequences of getting this work wrong, and how widely could those consequences spread?

### Could the Work Be Removed Instead?

### Could Documentation, Conventions, or Reusable Libraries Be Enough?

### Does the Shared Capability Remove the Work or Merely Move It?

### When Does a Shared Capability Become a Platform?

### Who Does Not Need an AI Platform?

### When Does a Platform Create More Friction Than It Removes?

### How Would We Know the Platform Helped?

#### What Was the Baseline?

Before introducing a shared capability, how often did the constraint occur, what consequences did it have, and how much work did it create?

#### What Changed?

Did incidents, containment time, audit effort, cost per successful outcome, reliability, or risk improve after introducing the shared capability?

#### What New Costs and Risks Did the Platform Introduce?

How much platform staffing, support, maintenance, exception handling, coupling, and common failure risk did the shared capability create?

### What Is the Decision Rule?

## Chapter 3: What Does "Smallest" Mean?

- What is the minimum capability that must be shared?
- What can be removed without preventing users from succeeding?
- When should a platform capability be shrunk, replaced, or removed?
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
