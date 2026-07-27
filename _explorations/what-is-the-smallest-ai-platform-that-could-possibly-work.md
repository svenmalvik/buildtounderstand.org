---
title: What Is the Smallest AI Platform That Could Possibly Work?
date: 2026-07-27
excerpt: Under exploration.
published: false
---

# What Is the Smallest AI Platform That Could Possibly Work?

## Chapter 1: What Problem Would a Platform Solve?

### What problem is an AI platform actually solving?

Today, many organizations run one form of an Ai adoption initiative with the goal of working more efficient using Ai but also to create better or new products with Ai. The consequence is more people consume external Ai services, create Ai agents using LLMs, using skills, or integrating internal and external MCP servers. To make it simple I label all these as Ai agents or just agents.

Here are the recurring areas where I see an increase in questions and demand because of Ai adoption initiatives:

- Developers ask for LLMs for their agents
- Finance want to know the spendings of these Ai agents by area, team, and product or agent
- Compliance wants to be in control of the data flow and asks for governance and audit evidences

These are only some of the most obvious points I have see. Other less obvious but still recurring works are:

- Developers ask for Ai evaluation and tesing tooling
- The incident and response teams ask for observing Ai agents.
- Leaders asks for better coordination of who build what agent to avoid many special agents

### What becomes difficult when teams build agents without an AI platform?

The most requested work is access providing access to LLMs. While it's easy to hand-over API keys and make engineers happy immediatly, most of the important demands from other units in the organization are not met. Finance doesn't know who is using what model and why. They just get a bill. Compliance doesn't know what data is flowing where. Nobody tells them. In case of an incident the incidet respond teams can't help simply because they are blind. There is nothing really to be observed.

An example I see again and again. An engineer build a PR review agent using the best Ai frontier model with extra high reasoning effort. Such an agent solves an immediate and obvious issue. However, it neglects others such as what is the cost/value ratio, what rules and constraints is the PR review being done with this one team or agent, and how can other teams use or learn and also have a PR review agent.

A central Ai platform must therefore do its best to take all necessary dimensions such as finance, compliance, procurement, governance, auditing, etc. into account in a way that it takes some or all of these burdens from the people.

### Does an AI platform actually help engineers and non-engineers build agents faster and more consistently?

An Ai platform can help engineers and non-engineers to build agents. i say can because it depends on the ambitions of the Ai platform and what problems do you want it to solve. At Vipps for example we created an agent builder. You visit our internal developer portal (IDP), click a button and give the agent a name. The result is a repository with an agent shell that is being deployed in the test environment. For you as the agent engineer, you are left with a starter prompt for your coding agent. It clones the repo, then asks for next steps for vibe coding. We are currently building more into it to address the other qyestions as well: costs, auditing, observability, etc.

You can argue that creating agents for non-engineers is a recurring problem that Vipps has been addressed and it therefore is a part of the Ai platform. The final answer to this depends on your organizational demands. For us it answered 3 principles, see Home page:

1. Build to Understand
1. Preserve Engineering Freedom
1. Design for Agency

> TODO: read findings.md

## Chapter 2: When Does Shared Work Become a Platform?

- When does repeated work justify a shared platform?
- Could documentation, conventions, and reusable libraries solve the problem instead?
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
