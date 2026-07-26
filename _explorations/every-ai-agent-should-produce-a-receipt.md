---
title: What If Every AI Agent Produced a Receipt?
date: 2026-07-26
excerpt: Coming soon.
---

# What If Every AI Agent Produced a Receipt?

<!--
AUTHOR OUTLINE

QUESTION
- Start with a real moment when an agent said it had completed a task but left
  you unsure what had actually happened.
- Ask what should exist between the agent's final answer and blind trust.
- Frame the central question: what if every agent had to produce a receipt?
- Define the receipt narrowly. It is not chain-of-thought or a complete log.

EXPLORATION
- Compare an agent receipt with an ordinary purchase receipt: a compact record
  of a transaction that another person or system can inspect.
- Distinguish four things: the answer, the conversation, the execution trace,
  and the receipt.
- Explore the minimum useful contents:
  - accepted task and constraints
  - agent, parent agent, model, gateway, and tool provenance
  - success, partial success, or failure
  - actions and changed targets
  - evidence for important claims
  - time, token, compute, and financial cost
  - uncertainties and work not verified
- Separate outcome claims from evidence. "Tests pass" is a claim; the command,
  exit code, timestamp, and retained output are evidence.
- Decide which facts the agent can report and which must come from the parent
  agent, gateway, or tool runtime.
- Consider delegation. A parent receipt could reference child receipts instead
  of hiding their work in one summary.
- Examine limits: misleading receipts, forged evidence, privacy, secrets,
  access control, and the fact that a receipt cannot prove the goal was right.

PROTOTYPE
- Build the smallest receipt you can use on one real agent task.
- Prefer a machine-readable format such as YAML or JSON.
- Include stable identifiers and references to evidence rather than copying
  large logs into the receipt.
- Use null for information that was not observed. Do not turn unknown cost
  into zero cost.
- Produce the same shape for successful, partial, and failed tasks.
- Record what surprised you when you used the prototype. This is the most
  important material for the article because it turns the idea into an
  exploration.
- Leave signing and tamper-resistant storage for a later version unless the
  prototype shows that they are already necessary.

CONCLUSION
- Answer the opening question using what the prototype taught you.
- State where responsibility belongs: the agent returns the receipt, while
  surrounding systems add facts only they can observe.
- Be clear about the limit. A receipt does not make autonomous work correct;
  it makes the work easier to inspect.
- End with the strongest unresolved question rather than a call to action.

PRINCIPLE, IF THE EXPLORATION EARNS ONE
- Possible direction: delegated work should remain inspectable.
- Explain how the principle changes the design of agents, gateways, and tool
  runtimes.
- Promote it to the site's Principles only after the prototype provides enough
  evidence to support it.

PERSONAL MATERIAL TO BRING
- The specific agent task that made you ask this question.
- What information you wished you had at the time.
- The actual receipt produced by your prototype.
- One failed or partial run, not only the successful example.
- The detail that changed your mind or made the original idea less simple.
-->
