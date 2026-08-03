---
title: What Should an AI Agent Leave Behind After Completing a Task?
date: 2026-08-02
excerpt: Under exploration.
published: false
---

<article class="exploration-article" markdown="1">

<header class="exploration-hero">
  <h1>What Should an AI Agent Leave Behind After Completing a Task?</h1>
</header>

In the previous exploration, I proposed an agent contract that describes what should be known before an agent runs: its purpose, owner, risk, permissions, evaluation, and operational references.

That leaves the other side of the task unexplored. What should remain after the agent has finished? Is a successful result enough, or should another person be able to understand what happened, verify what changed, and challenge or reverse the work?

I want to find the smallest useful record that makes completed work understandable without creating more ownership, surveillance, or storage work than it removes.

<!--
Research dossier:
research/20260802-214243-what-should-an-ai-agent-leave-behind/research.md
-->

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">01</span>
  <div>
    <h2 id="who-needs-to-understand-the-work">Who Needs to Understand the Work?</h2>
  </div>
</div>

Before deciding what an agent should leave behind, I need to understand who will use the record and what they need to learn from it.

I first thought I could answer this by listing roles. Engineers need traces. Auditors need approvals. People affected by a decision need an explanation. The list is useful, but the boundaries are too simple.

The same person can move between several roles. An engineer may operate the agent during the day, respond to its failure that night, and review its evidence later. Research on explainable AI reaches a similar conclusion. A [CHI framework for interpretability stakeholders](https://vis.csail.mit.edu/pubs/beyond-expertise-roles/) argues that a person's role and technical knowledge don't determine by themselves what the person needs to understand. The need also depends on the goal, the kind of information required, and how the person plans to use it.

A small interview study of 18 experienced AI and autonomous-system practitioners found that every participant wore at least two professional "hats." Only about half wanted explanations, while others preferred access to trusted engineers, examples, data, limitations, or a way to explore the system. They wanted to know how a system fails and misleads as much as how it works ([Hoffman and others, 2023](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2023.1117848/full)). The sample is too small to describe all practitioners, but it exposes a useful distinction: a record shouldn't begin with an assumed audience. It should begin with a decision someone needs to make.

### Which Questions Return After the Task?

Nobody needs evidence only because evidence exists. They return to the task because something remains uncertain. Should this result be accepted? Which action caused the failure? What must be stopped? Were the rules followed? Can the decision be challenged? Will the work still be understandable after the original runtime is gone?

These decisions require different views of the same task:

| Person | Decision after the task | The view must answer | Likely source of evidence |
| --- | --- | --- | --- |
| Engineer | Can I accept the work, or must I investigate it? | Which input, decision, or action first diverged from what was expected? | Runtime, trace, tool, test, and domain records |
| Incident responder | What must I contain, repair, or reverse? | Which identity acted, what was attempted, what committed, and which resources are still exposed? | Identity, policy, gateway, and domain systems |
| Reviewer or auditor | Can I accept the claim that the required process was followed? | Which authority, policy, approval, check, exception, and evidence applied at the time? | Identity, policy, approval, evaluation, and evidence systems |
| Person affected by the result | Can I understand, correct, or challenge this outcome? | Which facts and rules shaped it, who is responsible, and what procedure can change it? | Decision owner, domain record, case record, and challenge process |
| Future maintainer | Can I still reconstruct the work after replacing part of the system? | Which meanings, identifiers, versions, and verification material must survive? | Schema, evidence store, domain records, and verification bundle |

The role still helps, but the decision defines the minimum. An engineer diagnosing a failure needs a path through intermediate state. An auditor sampling policy compliance needs the policy and approval that applied at execution time. A person challenging an outcome needs understandable reasons and a procedure with a responsible owner. A raw trace doesn't become useful to that person merely because it is complete.

Research on algorithmic contestability makes this boundary clearer. People affected by a decision need more than a description of a model or a list of inputs. They need information and procedures that let them identify an error, present other evidence, reach a human reviewer, and obtain a correction or remedy. Interviews with 21 people reasoning about a public-sector enforcement scenario describe contestability as cooperative work, supported by personalised explanations and places in the process where a decision can actually be challenged ([Yurrita and others, 2025](https://doi.org/10.1145/3757415)). An evidence record may support that work. It can't replace the work or the responsible institution.

This suggests that one artifact shouldn't be presented to every person directly. A machine-readable record could connect the authoritative evidence, while different views reveal only what a decision requires. That avoids copying every fact into several systems, but it creates another requirement: every view must make missing, expired, or inaccessible evidence visible instead of turning absence into confidence.

### What Do Engineers Actually Use?

Public engineering discussions are much more concrete than the language of accountability. Engineers ask for a navigable sequence of model calls, retrievals, tool calls, state changes, errors, latency, and cost. They want to find the first meaningful divergence, not read an agent's story about itself.

They disagree about how much infrastructure this requires. In one [Hacker News discussion](https://news.ycombinator.com/item?id=39371297), some participants described LLM observability as ordinary service telemetry with new names, while another connected it to an existing Jaeger and Prometheus setup and reported that it worked well. In an [r/MachineLearning discussion](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/), one practitioner called complete interaction history invaluable for debugging and evaluation. Others said they built a small rules-based or internal solution because a product would add cost and integration work.

The disagreement is useful. It suggests that the valuable part isn't a new observability category. It is the evidence that answers a recurring engineering question at lower total cost than reconstructing it later.

Older systems research shows why the choice of evidence is important. A study of 250 failures across five large software systems found that more than half couldn't be diagnosed well from the existing logs. The researchers' logging tool added evidence around common failure paths, and a controlled user study reported a 60.7% reduction in diagnosis time ([Yuan and others, 2012](https://www.usenix.org/conference/osdi12/technical-sessions/presentation/yuan)). The result doesn't tell me which fields an agent needs, but it shows that useful evidence is selected for a diagnosis. More logging and better logging are different things.

The same limit appears in newer agent research. [AgentDebugX](https://arxiv.org/abs/2607.18754), a 2026 preprint, starts from the observation that replaying a trace often doesn't identify the step that caused the visible failure. Its best automated method reached 28.8% exact agent-and-step attribution on one benchmark, and its advantage was concentrated in traces longer than 40 events. This isn't a study of human engineers, and it doesn't validate an evidence manifest. It is still a warning against treating a complete trace as a completed diagnosis.

The implementation problems are ordinary and easy to underestimate. OpenTelemetry maintainers note that a payload may be enriched, redacted, truncated, or replaced by a reference before it reaches storage ([issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)). An OpenAI Agents SDK user found that disabling one exporter also disabled a local MLflow tracer ([issue #1387](https://github.com/openai/openai-agents-python/issues/1387)). Langfuse operators have had to add deletion and storage-cleanup controls for old traces ([issue #8834](https://github.com/langfuse/langfuse/issues/8834)). Capturing evidence creates its own failure paths.

Across these discussions and studies, four needs return:

1. A timeline that helps locate the first important divergence.
2. A distinction between what the agent attempted and what another system confirms actually changed.
3. Visible gaps when evidence was dropped, transformed, deleted, or never captured.
4. Enough context to act without retaining every prompt, document, and tool result forever.

The public discussions are self-selected. They overrepresent tool builders, vendors, and engineers already interested in AI infrastructure. I found no representative survey of what engineers want from post-task agent records, and no controlled comparison showing that a receipt reduces review or incident time. These sources provide design hypotheses, not a vote.

### Who Is the First Reader?

The prototype needs a narrower boundary than "everyone who may care later." I will start with the engineer responsible for the system in which an agent completed a task.

That engineer must decide whether to accept the completed task or investigate it. To make that decision, the engineer needs to identify the task and agent revision, understand the purpose and exercised authority, distinguish attempted actions from committed effects, find any affected resource versions, inspect the relevant trace, and see which checks passed or which evidence is missing. An investigation may then lead to repair or reversal.

The first prototype doesn't need to explain the result to every possible audience. It needs to support this one decision without preventing other views from being built later. The affected person, auditor, and future maintainer remain part of the design because their evidence must not be destroyed or made inaccessible. They are not the first interface.

This gives me a concrete test for the next chapter: can an engineer use the record to decide whether one completed task should be accepted or investigated, while distinguishing the agent's claims from facts confirmed by the systems it used?

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">02</span>
  <div>
    <h2 id="what-can-the-record-actually-prove">What Can the Record Actually Prove?</h2>
  </div>
</div>

Logs, traces, provenance, attestations, domain records, explanations, and receipts are often treated as different names for the same evidence. They answer different questions.

### What Already Exists?

| Artifact | What it can show | What it doesn't establish alone |
| --- | --- | --- |
| Result | What the agent returned | How it was produced or whether it is correct |
| Log | Events selected by one system | A complete causal path |
| Trace | How one execution moved through several systems | Whether an external effect actually committed |
| Provenance record | Which entities, activities, and actors contributed | Whether their claims are true |
| Attestation | Who signed a claim about a subject | That the signed claim is complete or correct |
| Domain record | What changed in the system that owns the action | The full context of the agent task |
| Explanation | Why an outcome is understandable to one audience | Complete operational evidence |
| Receipt or evidence manifest | A small index connecting the records | The truth of every record it references |

Use [W3C PROV](https://www.w3.org/TR/prov-dm/), [W3C Trace Context](https://www.w3.org/TR/trace-context/), [in-toto attestations](https://github.com/in-toto/attestation/blob/main/spec/README.md), and the [IETF SCITT architecture](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html) to develop these distinctions.

The name is part of the exploration. A receipt may imply stronger proof than the artifact can provide. Evidence manifest may describe a small set of references more accurately.

### Can the Agent Be Its Own Evidence?

Explore the difference between an agent describing its work and another system confirming what happened.

An agent can say that it called a tool, followed a policy, changed a resource, or passed an evaluation. The useful evidence may need to come from the identity system, policy engine, tool gateway, domain system, evaluator, and billing system instead.

Signing the agent's record can show who produced it and whether it changed later. It can't establish that every claim inside it is true.

### Which System Owns Each Fact?

| Kind of fact | Examples | Possible source |
| --- | --- | --- |
| Declared for the task | Purpose, agent revision, expected data class | Receipt or agent contract |
| Observed during execution | Timing, tool calls, errors, cost | Runtime, trace, gateway, and billing systems |
| Decided before an action | Delegated authority, policy result, approval | Identity and policy systems |
| Confirmed after an action | Resource version, transaction, deployment, rollback | The domain system that owns the action |
| Verified independently | Evaluation result, audit decision, accepted exception | Evaluator or decision system |
| Protected for later use | Digest, signature, timestamp, retention state | Evidence and transparency systems |

The record should connect these facts. It shouldn't replace the systems that produced them. This is the central trust boundary for the prototype.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">03</span>
  <div>
    <h2 id="what-is-the-smallest-useful-record">What Is the Smallest Useful Record, and Where Should It End?</h2>
  </div>
</div>

A possible test for the smallest useful record is:

> The smallest useful post-task record is the artifact that lets a defined person understand and verify one completed task, exposes missing evidence, creates the least total work, and remains usable after its original systems are changed or removed.

This gives the record four tests:

<div class="test-grid">
  <div class="test-card">
    <p class="test-card__number">01</p>
    <h4>Understanding</h4>
    <p>Can the intended person understand what happened and what changed?</p>
  </div>
  <div class="test-card">
    <p class="test-card__number">02</p>
    <h4>Evidence</h4>
    <p>Can the person distinguish the agent's claims from facts confirmed by other systems?</p>
  </div>
  <div class="test-card">
    <p class="test-card__number">03</p>
    <h4>Total work</h4>
    <p>Does the record remove more review, incident, audit, and migration work than it creates?</p>
  </div>
  <div class="test-card">
    <p class="test-card__number">04</p>
    <h4>Change and removal</h4>
    <p>Can the record survive a change of runtime, trace backend, verifier, or evidence location?</p>
  </div>
</div>

### The Smallest Record I Can Justify as a Prototype

Start with an evidence manifest that holds stable declarations and typed references to facts produced elsewhere.

<div class="prototype" markdown="1">
<p class="prototype__label">Prototype 0.2 · agent-receipt.yaml</p>

```yaml
receipt:
  schema: agent-receipt/0.2
  id: receipt-123
  started_at: 2026-08-02T12:00:00Z
  completed_at: 2026-08-02T12:00:04Z
  status: completed

task:
  purpose: explain settlement deviation
  requested_by: user:sven

agent:
  identity: agent:settlement-explainer
  revision: a8c21f4

authority:
  delegation_ref: identity://delegations/9821
  policy_ref: policy://settlement-read/17

execution:
  trace_ref: trace://settlement-explainer/trace-123
  attempted_tools:
    - settlement-reader

effects:
  - type: read
    record_ref: settlement://8472/version/4
    status: confirmed

verification:
  verifier: eval:settlement-explanations
  criteria_ref: eval://settlement-explanations/12
  result: passed

lifecycle:
  data_class: internal
  retention_until: 2026-11-02

integrity:
  issuer: runtime:application-platform
  signature_ref: sigstore://bundle/receipt-123
```

<p class="prototype__caption">The manifest describes the task and points to the systems that can confirm its authority, execution, effects, verification, and integrity.</p>
</div>

The prototype is a hypothesis, not the proposed answer. The exploration should remove every field that doesn't help a reviewer and add a field only when its absence prevents understanding or verification.

### Where Should the Record End?

The evidence manifest should not become:

- a copy of the complete trace
- a second source for facts owned by another system
- a permanent archive of every prompt and tool result
- the policy engine that decides whether an action is allowed
- the explanation shown directly to every possible audience
- proof that a signed claim is true

The smallest record may be a versioned index with enough stable meaning to connect these systems. The prototype should test whether even that additional index is necessary.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">04</span>
  <div>
    <h2 id="how-should-evidence-change-with-risk">How Should Evidence Change With Risk?</h2>
  </div>
</div>

An internal read-only task doesn't create the same need for evidence as an agent that moves money, changes production infrastructure, or affects a person's access to something important.

The minimum may need to grow with authority, impact, sensitivity, and reversibility. More evidence can also create more privacy, review, and retention work.

### How Should the Minimum Change?

| Task | Candidate minimum |
| --- | --- |
| Read-only task with internal data | Identity, version, data class, result, trace reference, cost, and evaluation reference |
| Task that changes another system | The read-only fields plus delegated authority, policy decision, attempted calls, committed effects, and reversal instructions |
| High-impact or difficult-to-reverse task | The previous fields plus approval, independent verification, evidence custody, retention, explanation, and challenge path |

The prototype should test whether these additions help. More fields can still create a record nobody can review or afford to maintain.

### What Should the Record Leave Out?

Explore the cost and risk of retaining prompts, retrieved documents, tool arguments, tool results, and internal reasoning.

Identifiers, digests, classifications, and controlled references may be enough. References can also expire, access can change, and lawful deletion can remove the evidence. A digest can show that something changed. It can't make deleted evidence available again.

The [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689) and [GDPR](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679) provide a useful tension between evidence duties and data minimisation. Keeping more information isn't automatically the safer option.

### Who Must Be Able to Challenge the Result?

Operational evidence for engineers and an explanation for an affected person are different products. The exploration should ask how the receipt leads to a responsible owner, understandable reason, correction process, and remedy without exposing raw traces or protected data.

This section should also ask who is allowed to inspect the record, who can correct it, and what happens when the record itself is incomplete or wrong.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">05</span>
  <div>
    <h2 id="how-would-i-test-the-record">How Would I Test the Record?</h2>
  </div>
</div>

The prototype should test the value of the record, not only whether the YAML can be generated.

### Compare Three Forms of Evidence

Produce the same completed task in three forms:

1. The result alone.
2. The result with its complete trace.
3. The result with a small evidence manifest that points to the trace and authoritative records.

Reviewers shouldn't be told which option is expected to work best. They should answer the same questions with each artifact.

### Test More Than the Successful Path

Use successful and hostile cases:

- a successful read-only task
- stale or incomplete source data
- a tool call that fails before changing anything
- a partial task where one effect commits and another fails
- an attempted action outside the agent's authority
- evidence that has expired or become inaccessible
- a receipt that disagrees with the source system
- replacement of the trace backend, verifier, and agent runtime

A receipt that works only when every component behaves correctly doesn't provide much additional trust.

### Measure Total Work and False Confidence

| Test | Possible measure |
| --- | --- |
| Understanding | Can a reviewer correctly reconstruct what happened? |
| Verification | Can the reviewer distinguish attempted actions from committed effects? |
| Time | How long does the review take? |
| Missing evidence | Does the artifact reveal gaps instead of hiding them? |
| False confidence | Does the reviewer accept an incomplete or false receipt? |
| Privacy | How much sensitive content is copied or exposed? |
| Ownership | How much generation, storage, review, migration, and deletion work is created? |
| Portability | Can the task still be understood after replacing the supporting systems? |

The experiment may show that the evidence manifest is useful. It may also show that a trace and the domain records already provide enough evidence.

<div class="chapter-heading chapter-heading--compact">
  <span class="chapter-heading__number" aria-hidden="true">06</span>
  <div>
    <h2 id="can-the-record-create-leverage-without-reducing-freedom">Can the Record Create Leverage Without Reducing Freedom?</h2>
  </div>
</div>

A record can help teams understand and change an agent. It can also make the original runtime, tracing product, storage system, and verifier harder to leave.

The value of the record should continue after the original task. Engineers should be able to use it during reviews, incidents, audits, migrations, and later changes. That value must exceed the continuing work of capture, storage, access control, schema changes, broken references, review, and deletion.

### Where Would the Leverage Come From?

The record could remove repeated work by giving several people a shared way to find the authoritative evidence. It could make an incident easier to reconstruct, an audit easier to sample, and a migration less dependent on the original vendor's interface.

Count the work the record creates as well:

- instrumenting every participating system
- defining and changing the schema
- protecting and reviewing access
- repairing broken references
- preserving old verification keys and policy versions
- answering access and correction requests
- migrating and eventually deleting the evidence

The record creates leverage only when the repeated work it removes exceeds this continuing ownership cost.

### How Can Teams Leave the Evidence System?

Syntax alone doesn't create portability. Another implementation must understand what each field means, verify old signatures, resolve evidence references, and retain the information needed to reconstruct the task.

The prototype should therefore be tested after changing:

- the agent runtime
- the trace backend
- the identity or policy system
- the evidence location
- the verifier

If the record works only inside the original vendor's dashboard, it doesn't preserve engineering freedom.

### When Should the Record Be Reduced or Removed?

Explore the full lifecycle of the evidence:

- when a field should become a reference instead of copied content
- when sensitive evidence should be redacted or deleted
- how broken references become visible
- what must remain after a provider or verifier disappears
- when the original task no longer justifies the ownership cost

Removal is part of the prototype. A record that can only be created and retained is incomplete.

## Conclusion

Under exploration.

The conclusion should answer:

- Is the useful artifact a receipt, an evidence manifest, or only a view over existing records?
- Which facts must come from systems independent of the acting agent?
- How should the minimum change with authority, impact, and reversibility?
- Does the artifact reduce total review, incident, audit, and migration work?
- Can teams replace the runtime, storage, identity, and verifier without losing operational history?

The prototype may show that a portable record creates useful leverage. It may show that it is justified only for higher-impact tasks. It may also show that better traces and domain records are enough.
</article>
