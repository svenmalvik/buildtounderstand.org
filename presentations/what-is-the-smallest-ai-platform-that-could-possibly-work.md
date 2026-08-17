# What Is the Smallest (AI) Platform That Could Possibly Work?

Presentation content derived from
[`_explorations/what-is-the-smallest-ai-platform-that-could-possibly-work.md`](../_explorations/what-is-the-smallest-ai-platform-that-could-possibly-work.md).

- **Audience:** internal platform team and engineering leadership
- **Purpose:** agree on whether the repeated AI work justifies a platform, agree
  on the smallest version of it, and decide how it reaches its first team
- **Length:** ~25 minutes, plus discussion on the last slide
- **Slides:** 10
- **What the audience should leave with:** a decision on one of three adoption
  paths, and a named owner for it
- **Rendering format:** not chosen yet.

Each slide is written to stand on its own — readable without a presenter, and
usable as a document after the meeting. Content is denser than a talk-only deck
for that reason. The *Visual* line under each slide is guidance for generation,
not slide text.

**Image asset:** `assets/images/ai_platform.png` — the full AI platform
reference architecture. It appears twice: complete on slide 5, and marked up on
slide 8. Both uses are load-bearing; see the generation notes at the end.

---

## Slide 1 — The question

**What is the smallest (AI) platform that could possibly work?**

The most common AI request I see is access to an LLM. Giving an engineer an API
key takes minutes and solves exactly one problem.

What the key does not do:

- show finance which team created which cost
- help compliance understand where the data goes
- give incident response a system it can observe
- tell anyone whether the agent still works

That work arrives later — sometimes weeks after the part that felt like the job.
It lands on us, and it lands again with the next team.

Two questions for today:

1. Does that repeated work justify a platform used by several teams?
2. If it does, what is the smallest platform that could possibly work?

*Agent, throughout: software built with LLMs, skills, and integrations with
internal or external tools.*

**Visual:** title slide. "API key: 5 minutes" set against the four unanswered
items.

---

## Slide 2 — No single request is a platform problem

A collection of experiments does not become a platform problem just because the
experiments use AI.

- A team asking for model access has an **access problem**
- Finance asking about a bill has an **accounting problem**
- Neither one, on its own, justifies a platform

It becomes a platform problem when several teams repeatedly need the **same**
access controls, cost attribution, evaluation, observability, or audit evidence —
and solving each case separately creates more work, inconsistent controls, or
unnecessary risk.

The test is not how much AI activity we have. It is:

- Does the same problem keep appearing?
- What happens if we ignore it?
- Would solving it once for several teams remove more work than it creates?

One company can run many experiments and have no platform problem. Another can
have two production agents on sensitive data and already need strict controls.

And even when the answer is yes, the answer may be to **extend a platform we
already own**. A dedicated AI platform is justified only when our existing
systems cannot solve the repeated problem without every team rebuilding the same
AI-specific parts.

**Visual:** individual requests on the left (access, cost, data flow,
observability, audit) collapsing into one repeated shape on the right.

---

## Slide 3 — What is actually repeating for us

Two patterns, both real, both already costing us time.

**Deployment support repeats**

Analysts and product managers build something with a coding agent — often a
dashboard. It works on their machine. Making it available to others means the
company runtime and the service contract in the developer portal, which still
requires engineering experience. So we help. Manually. Again.

> Signal: the same setup and translation work returns with every new builder.

**Access without controls repeats**

Engineers build AI-powered Slack apps and ask for an LLM key. The request itself
is cheap. The key answers none of the operational questions from slide 1.

> Signal: easy access creates the same unanswered questions every time.

**Where we already stand**

The AI Playground removes part of the first pattern: a person names an agent in
the developer portal and receives a repository with a working agent deployed to
test, plus a starter prompt for a coding agent. What it removes is the repeated
setup, the allowed technologies, and the practices we want people to inherit as
skills.

That is worth naming as evidence: pattern one was real, and a **template** was
the right size of answer for it. Pattern two is the one still open — and it is
the one producing the questions from finance, compliance, and incident response.

**Visual:** two cards side by side, each with its signal line. First card marked
partially solved; second card marked open.

---

## Slide 4 — Build less than you think you need

> **The order matters.** Documentation → convention → template, library, or CLI →
> managed service. Build the service only when the simpler interventions cannot
> remove the repeated work.

Teams also repeat work because they are still learning. Centralizing too early
turns experiments into a service nobody needs.

Before building a shared service, ask whether the repeated work can be
**removed** rather than served. The apparent platform problem may be unclear
ownership, missing training, or a workflow that should not exist.

**I have paid for getting this wrong — though not with a platform.**

Manifold was an AI coding IDE for individual developers. I spent six months of
evenings on it, convinced someone needed it. Nobody did. The software was not
the problem. The problem was that I treated my own conviction as evidence that
the demand existed.

An internal platform fails the same way, but more quietly. A team that stops
using a platform rarely says so — it routes around the platform and keeps
working. We keep the mandate and lose the users, so the mandate stops being
evidence that anyone needs the thing.

> That is why I no longer trust the sentence "teams need this" when I am the one
> saying it. Everything after this slide argues for building less than I think is
> necessary.

A service starts to behave like a platform when several teams choose it because
it is easier and safer than solving the problem themselves.

**Visual:** the four-step escalation as a staircase, managed service at the top
and marked expensive. The Manifold block set apart as a first-person aside.

---

## Slide 5 — What a complete AI platform looks like

![Full AI platform reference architecture: nine horizontal layers between users and a trust column](../assets/images/ai_platform.png)

This is the picture most of us have in mind when someone says "AI platform."
**Build · Run · Govern · Trust.**

Nine layers, serving employees, developer tools, AI agents, business
applications, and external partners:

| Layer | What it provides |
| --- | --- |
| **Experience** | Chat/UI, playground, workflows, SDKs and APIs |
| **Agent** | Agent framework, tool use, multi-agent collaboration, task orchestration |
| **Context** | RAG/retrieval, vector DB, data connections, MCP and tool servers |
| **Model & inference** | Model gateway and routing, model selection and fallback, caching, cost and latency optimization |
| **Models** | OpenAI, Anthropic, Google, Meta, our own hosted or fine-tuned models |
| **Evaluation** | Quality metrics, automated evaluations, human feedback, experiments and A/B testing |
| **Governance & security** | Identity and access management, policies and guardrails, data privacy, audit logs and compliance |
| **Observability & operations** | Monitoring and alerting, tracing and logging, usage/quotas/billing, reliability and SLOs |
| **Infrastructure** | Cloud, Kubernetes, GPU/CPU compute, networking, storage |

And running down the right side, the reason any of it matters — the **trust
layer**: transparency (what happened and why), explainability (why this answer),
verifiability (is it correct), accountability (who did what), safety and control
(is it safe and compliant), reliability (can we depend on it).

> A trustworthy AI platform gives humans confidence to delegate work to AI: the
> right result, for the right reason, in a safe and reliable way, with full
> visibility and control.

**Nothing on this diagram is wrong.** Every box is a real capability that someone
has to provide. That is exactly what makes it dangerous as a plan: it is roughly
forty capabilities, it reads as a roadmap, and a roadmap is not evidence that we
should own any particular box.

So the question is not *which layers exist*. It is:

- Which of these do we already have, under a different name?
- Which belong to the team building the agent, not to us?
- Which are not needed yet for the workflow in front of us?
- And what is the cheapest thing that makes the trust column answerable **per
  agent**, starting today?

**Visual:** the diagram full-bleed, as large as the format allows. This is the
one slide where the image is the content — put the layer table on a second panel
or a build step if it does not fit alongside. Keep the trust column readable; it
sets up slide 8.

---

## Slide 6 — What "smallest" has to mean

After a diagram with forty boxes, the tempting measure is subtraction: fewer
features, fewer services, fewer lines of configuration. By that measure a config
file looks smaller than a gateway. Convenient, but not the measure that matters.

> The smallest useful AI platform is the system that creates the least total
> work, lets a defined group complete one valuable workflow, meets the minimum
> required controls, and remains cheaper to change or remove than the repeated
> work it removes.

That gives "smallest" four tests:

| Test | Question |
| --- | --- |
| **Outcome** | Does it solve the measured problem and let the intended user finish the job? |
| **Risk** | Does it provide the minimum controls required by the data, authority, reversibility, and possible impact? |
| **Total work** | Does it reduce central *and* local integration, support, audit, incident, migration, and exception work? |
| **Change and removal** | Can its contracts, state, evidence, and users be changed or retired at an acceptable cost? |

Two consequences worth stating:

- Total work includes the work we push onto the teams using the platform, not
  just the work we do ourselves
- "Smallest" is the simplest thing that passes all four tests **for one
  particular workflow** — so it changes when the workflow changes

**Visual:** the definition as a pull quote; the four tests as a 2×2 grid.
Optionally the previous slide's diagram greyed out behind it.

---

## Slide 7 — The proposal: a versioned agent contract

The smallest platform I can justify is a narrow service built around a
**versioned agent contract**: a configuration file stored with the code that
describes the agent and the systems it uses.

The contract alone is not the platform. The contract **and** the service are: CI
validation, connections to the systems that own operational facts, and a view in
the developer portal.

Scope for version 0.1: one simple, internal, read-only agent. Not a general
contract for every kind of agent.

```yaml
agent:
  name: settlement-explainer
  owner: payments
  purpose: explain settlement deviations
  lifecycle: experimental
  risk: internal-read-only
  allowed_data: internal
  model_access: approved-eu-provider
  runtime: application-platform
  cost_id: payments-settlement
  trace_id: settlement-explainer
  evaluation: evals/settlement.yaml
  incident_contact: payments-on-call
  disable: runbooks/disable-agent.md
```

Every field exists to make one internal, read-only workflow accountable and
observable: who owns it and why it exists, what data and models it may use,
where its runs connect to cost and traces, how it is evaluated, who to call, and
how to switch it off. If a field cannot be justified for *this* workflow, it does
not go in yet.

**It must not become a second source of truth.** It declares stable information
and points to operational facts where they are produced:

| Kind of fact | Examples | Source |
| --- | --- | --- |
| Declared with the code | Purpose, owner, lifecycle, risk class, allowed data, model-access reference, incident contact | Agent contract |
| Observed while building or running | Deployed revision, evaluation result, traces, cost | CI, delivery, evaluation, observability, billing |
| Confirmed by an accountable owner | Approval, accepted exception, review decision, expiry | The system where that decision is made |

How it works:

1. An engineer creates or changes the agent and its contract in the same repository
2. CI validates identity, ownership, risk, data class, operational references,
   incident contact, and disable instructions
3. Delivery, evaluation, observability, and billing systems continue to produce
   and own their operational facts
4. The developer portal brings declarations, current facts, and links to their
   sources into one view
5. The agent keeps running on the existing application runtime

**No new runtime, no AI gateway, no evaluation service, no new GUI to start.**
High-impact actions, tool approvals, accepted exceptions, and retained evidence
get added when a workflow requires them.

**Visual:** YAML as the centrepiece; the five steps as a left-to-right flow
beneath it; the fact-ownership table as a second panel or build step.

---

## Slide 8 — Where the platform ends: the same picture, marked up

Same diagram as slide 5. Four colors, one question per layer: **who owns this,
and do we need it yet?**

| Layer in the diagram | Status for version 0.1 |
| --- | --- |
| **Experience** | *Already have it.* The Playground covers the entry point; the product surface belongs to the team |
| **Agent** | *Team owns it.* Framework, tool use, orchestration. The contract only declares identity, purpose, owner, and lifecycle |
| **Context** | *Team owns it.* Retrieval, vector stores, data connections. The contract declares the allowed data class, not the wiring |
| **Model & inference** | *Declared reference + deferred.* The contract points at approved model access. Gateway, routing, fallback, and caching wait for a signal — model choice, prompts, and fallback behavior stay with the team |
| **Models** | *External.* Approved provider and region are a declared reference, not something we build |
| **Evaluation** | *Reference now, runner later.* The contract carries an evaluation reference; the domain team defines the cases, the possible harm, and what is good enough to release |
| **Governance & security** | *Existing systems + contract.* Our identity platform issues identities; the resource owner authorizes business actions. The contract declares risk class, allowed data, incident contact, and how to disable. CI validates that they are there |
| **Observability & operations** | *Existing systems + identifiers.* Observability and billing own the data. The contract carries the trace and cost identifiers that connect a run to it |
| **Infrastructure** | *Untouched.* The existing application runtime and cloud. We introduce no new runtime |

That is the whole boundary: **one file, CI validation, and a portal view.** The
other eight layers are already owned, belong to the team, or are waiting.

**The contract connects decisions. It does not enforce them.** Every shared
control splits into four responsibilities:

| Responsibility | Owner |
| --- | --- |
| Decide which outcome is required | The person accountable for the harm or obligation |
| Define representative cases and evidence | The team that understands the workflow |
| Encode and validate the rule | The platform team |
| Prevent a disallowed action | A system with the context and authority to stop it |

A gateway can enforce allowed models. A deployment system can require evaluation
evidence before release. A downstream service must authorize the business action.
A YAML file cannot stop an agent from using a credential with too much access.

**It also gives the trust column an answer per agent** — which is what the
diagram promises and a key alone never delivers:

| Trust property | What makes it answerable | Who answers it |
| --- | --- | --- |
| Transparency | Declared purpose, model access, data class, runtime | Contract |
| Accountability | Declared owner and lifecycle; approvals and exceptions | Contract + the deciding system |
| Verifiability | Evaluation reference | Contract + evaluation system |
| Safety & control | Risk class, allowed data, incident contact, disable instructions | Contract + enforcing systems |
| Reliability | Trace and cost identifiers | Contract + observability and billing |
| Explainability | Sources and reasoning steps | The team's product, not the platform |

**When the contract stops being enough:** teams still need the same manual help;
the declared information becomes unreliable; every system needs a custom adapter.
Then the next box we light up — generator, gateway, authorization service,
evaluation service, or dedicated runtime — is a response to a signal, not a
roadmap item. An AI gateway does not become necessary because a workflow uses an
LLM.

**Visual:** the diagram again, with each layer tinted by status — *already have
it* / *team owns it* / *deferred* / *contract declares it*. Dim everything the
contract does not touch so the lit area reads as small. The three tables follow
as build steps; do not show all four elements at once.

---

## Slide 9 — Teams have to be able to leave

A useful platform gives teams an easier way to work. It becomes a problem when
that is the only practical way.

If a team loses model access, deployment, observability, support, and cost
attribution the moment it chooses something else, it has to rebuild what already
exists — and we made that choice for it.

> Freedom needs a usable path forward.

If only the standard path receives normal support and audit recognition, an
alternative implementation is not a real option.

Leaving always creates work: prompts, tool schemas, evaluations, configuration,
state, logs, and retained evidence may need to move or be recreated; old access
must be revoked; both paths may run in parallel during migration. The point is
not that leaving should be free. The point is that it should be **visible,
supported, and possible**.

A practical alternative path needs:

- access to the existing identity, deployment, observability, incident response,
  and cost systems
- a way to show that required controls still work
- an export or reconstruction plan for state and evidence
- a named owner and budget for migration and temporary parallel operation
- a way to revoke the old path and return if the replacement fails

**The same standard applies to this platform.** Reduce it when something simpler
achieves the same outcome and risk result. Replace it when something cheaper does
the same work and preserves the information needed to move. Remove it when the
original problem is gone and every remaining user has a tested alternative.

Removal is a product change: retention decisions, migration support, rollback,
communication, budget. The cost of leaving is part of the cost of the platform.

> If we cannot describe the exit, we have not finished designing the platform.

Worth noticing against slide 5: a one-file contract on the existing runtime is
close to the cheapest thing on that diagram to walk away from. Most of the boxes
are not.

**Visual:** the five exit requirements as a checklist, each with the owning
system named.

---

## Slide 10 — The decision I need from this room

Prototype 0.1 has one problem worth stating directly: **no team has used it.**
It is a file I wrote to find out whether the idea holds together — which is the
same kind of evidence I said on slide 4 that I no longer trust.

So the open question is not what the contract should contain. It is how a
contract nobody asked for reaches its first team. I see three ways and I do not
know which is right.

| Path | What it buys | What it costs |
| --- | --- | --- |
| **Put it in the template** | Fastest adoption. Every agent generated through the internal template gets a contract by default; teams receive it without asking | Nobody chose it. The adoption numbers would look good and mean nothing — the exact failure mode from slide 4 |
| **Wait for the pull** | Real demand. We build when a team asks for something it enables: cost attribution, audit evidence, or a way to disable an agent during an incident | The request arrives after agents are already in production — the most expensive moment to introduce a contract, and the least likely to get engineering time |
| **Don't build it** | Cheapest. Add the fields to the service contract the developer portal already uses. No new system to own, nothing to leave | Puts AI-specific facts into a system that was not designed for them. Unclear whether that is reuse or a problem that grows slowly |

> The first option is the one I want to pick, and wanting it is the reason I have
> not.

**What I am asking for:** pick one path, name the owner, and state what evidence
would make us switch.

**What would change my mind:** a team that was handed a contract by default and
actually used it. If anyone here has been further along on this before — which
path did you choose, and what did it cost?

**Visual:** three columns with the cost line emphasized over the benefit line.
Do not visually rank them.

---

## Notes for whoever generates the deck

**The image**

- Source: `assets/images/ai_platform.png` (repo root). From this folder:
  `../assets/images/ai_platform.png`.
- Slide 5 shows it complete and unmodified. Slide 8 shows it again with layers
  tinted by status. Showing the *same* image twice is the argument — a second,
  differently drawn diagram breaks it.
- Alt text: "AI platform reference architecture. Nine layers from experience down
  to infrastructure, between a column of users and applications on the left and a
  trust layer on the right."
- The diagram is dense. If it cannot be rendered legibly at slide size, crop to
  the nine layer bands and their headers rather than scaling the whole thing down;
  the per-layer capability names are already written out in the slide 5 table.
- The diagram is dark-background. Match the deck to it rather than placing it on
  white.

**Structure**

- Slide 4 and slide 10 carry the argument. The Manifold mistake is the reason the
  proposal is small, and slide 10 is the reason the meeting exists. Do not
  compress either to make room for the diagram.
- Slide 5 → 6 → 7 → 8 is one movement: the full picture, the measure, the
  proposal, the marked-up picture. Keep them adjacent and in that order.
- Slides 5, 7, and 8 are heavy. Use build steps rather than cutting reasoning —
  the reasoning is the content. Slide 8 has four elements; reveal them one at a
  time.
- Several slides use tables. If tables render badly, split slide 8 first — the
  four tests on slide 6 and the three paths on slide 10 must each stay together
  to be comparable.
- Do not add a summary slide after slide 10. Ending on the open decision is the
  point; restating the conclusion turns it back into an essay.
- The tone is first person and provisional: "the smallest platform I can
  justify," not "the recommended architecture." Keep the hedges — they are the
  argument, not padding.
