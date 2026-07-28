# Findings: When Does Shared Work Become a Platform?

**Last updated:** 2026-07-28
**Full synthesis:** [research.md](research.md)
**Community evidence:** [07-community.md](07-community.md)
**Validation:** [validation.md](validation.md)

## Short answer

Repeated work becomes a platform candidate when all of these are true:

1. A valuable, owned workflow is repeatedly blocked by the same constraint.
2. The constraint is consequential enough to measure in waiting time, duplicated work, incidents, audit effort, cost, reliability, or risk.
3. Documentation, clearer ownership, conventions, templates, libraries, CLIs, or a narrow managed service cannot remove it adequately.
4. A shared capability can complete the common path end to end rather than merely create a ticket for another team.
5. Engineers choose the shared path because it is easier and safer, while supported exceptions remain possible.
6. The capability removes more coordination, cognitive load, and risk than its ownership, maintenance, coupling, and failure domain introduce.
7. The result remains positive when reviewed later. A platform needs an expiry test as well as a creation threshold.

There is no defensible universal threshold based on the number of teams, agents, models, or repeated tasks.

## What research shows

The empirical evidence is much thinner than the market language suggests.

- DORA’s 2024 survey associates internal-platform use with higher perceived individual, team, and organizational performance. The same analysis associates platform use with lower delivery throughput and change stability, and exclusive mandatory use with a further throughput penalty. These are correlations, not causal estimates.
- A 2026 multivocal literature review found that only 2 of 88 included sources were tier-one publications primarily about platform engineering. It found no peer-reviewed empirical evidence for the effectiveness of IDP scorecards.
- A randomized trial of AI-assisted development with 96 Google engineers found a time benefit for one coding task. It supports the claim that AI can change engineering work; it does not establish that a broad AI platform causes better outcomes.
- Public research did not reveal a controlled or matched longitudinal comparison of four relevant choices: documentation/training, templates or reusable libraries, a narrow managed capability, and a broad internal AI platform.

The evidence supports recurring lifecycle, governance, evaluation, observability, cost, and authority problems. It does not establish that integrating them into one dedicated AI platform creates a general business-value premium.

## What AI-platform vendors say

Vendor positions are more nuanced than a simple “buy a platform,” but all have commercial incentives to expand the shared surface.

- Google Cloud argues for self-service golden paths that reduce cognitive load and explicitly says there is no one-size-fits-all platform.
- AWS distinguishes Bedrock from SageMaker based on workload needs, implying that scope should follow the work rather than a universal architecture.
- Scale AI recommends buying the common foundation while building differentiated workflows and feedback loops.
- Spotify presents Backstage as a mature human-and-agent interface built on ownership, catalogue, and action metadata.
- PlatformEngineering.org frames platforms as a growing enterprise operating model and an answer both for AI-assisted platform work and AI workloads.

The useful part of the vendor consensus is:

> Centralize common, non-differentiating capabilities; retain workflow-specific logic and differentiation locally.

The unsupported leap is:

> Therefore the common capabilities should be one broad, integrated AI platform.

Vendor case studies frequently omit non-users, abandoned implementations, internal staffing, exception handling, upgrades, migration, and exit costs. Their material is valuable for product capabilities and market positioning, but weak as independent proof of net value.

## What engineers experience

The community sample is purposive, not representative. It is useful for finding concrete mechanisms and failure modes.

### What works

- A small CLI that makes deployments reproducible and predictable.
- Templates that bootstrap projects with common infrastructure while letting teams remain independent.
- Shared services for expensive or risky concerns such as databases, messaging, DNS, identity, and policy.
- Catalogues that expose ownership and dependencies.
- Golden paths designed with continuous feedback from their users.
- Capabilities that both humans and agents can invoke and verify through stable, machine-readable interfaces.

### What fails

- A “self-service” portal that submits the same ticket to the same operators.
- Wrappers and internal frameworks mandated across the company without counting upgrade and support work.
- A platform designed from leadership’s desired architecture rather than engineers’ actual workflow.
- Hard validation that blocks users when the system cannot represent incomplete or exceptional states.
- A portal mistaken for execution.
- Broad adoption treated as proof of value.

### The most useful practitioner test

A shared capability is platform-like when it:

1. accepts the user’s intent;
2. applies the required checks;
3. performs the common operation without bespoke human work; and
4. returns a usable, observable result.

If it only changes how the request enters a queue, it has not removed the constraint.

### What scale changes

Small teams often report that documentation, repository templates, libraries, and a CLI are sufficient. One large Backstage practitioner reported thousands of weekly users and a dedicated team of 20. The same investment can be rational at that scale and absurd for a small organization.

The relevant ratio is not simply users per platform engineer. It is:

> consequential repeated constraints removed per unit of ongoing ownership.

## The central counterargument

“When does work become a platform?” may already be a platform-shaped question.

The apparent platform problem may instead be:

- unclear ownership;
- weak product discovery;
- missing training or documentation;
- unnecessary variation between teams;
- a poor procurement choice;
- a workflow that should be removed;
- a narrow control or managed-service problem.

Calling the situation a platform problem can encourage scope growth before the cause is understood.

## A sharper decision rule

Use this sequence for each candidate capability:

| Step | Question | Possible outcome |
|---|---|---|
| 1. Workflow | Is this workflow valuable, used, and owned? | If not, stop. |
| 2. Constraint | What repeatedly blocks it, and what is the measured consequence? | If no meaningful constraint is visible, observe rather than build. |
| 3. Cause | Is the cause technical, organizational, educational, contractual, or regulatory? | Fix the cause, not its most visible symptom. |
| 4. Substitute | Can removal, documentation, a convention, template, library, CLI, or narrow vendor service solve it? | Use the lightest option that works. |
| 5. Shared capability | Can a shared service remove the common constraint end to end? | Build or buy one bounded capability. |
| 6. Escape | Can unusual workloads leave the path safely? | Add an explicit exception path before mandating anything. |
| 7. Measurement | Does it improve the workflow after all operating costs are included? | Expand, hold, shrink, replace, or delete. |

## When an AI platform is probably justified

- Several valuable production workflows need the same model-access, identity, evaluation, observability, evidence, deployment, or cost capability.
- The same control must be implemented consistently because mistakes are costly or legally consequential.
- Local implementations create measurable duplication, incompatible evidence, or incident-response blindness.
- Existing developer, data, identity, security, and observability platforms cannot absorb the AI-specific need cleanly.
- A staffed owner can operate the capability as a product.
- The organization can preserve export, portability, and exception paths.

The first justified capability may be only a gateway, evaluation service, trace convention, policy check, cost-attribution layer, or deployment contract.

## Who probably does not need one

- A small organization or one team with few production AI workflows.
- Teams still searching for a valuable use case.
- Organizations whose binding problems are data ownership, skills, incentives, or workflow design.
- Teams whose existing platforms can be extended with a template, library, policy, or telemetry convention.
- Organizations unable to fund product ownership, support, on-call, upgrades, and deprecation.
- Cases where the proposed platform mainly improves management visibility without completing engineers’ work.
- Environments changing so quickly that a centralized abstraction would harden assumptions before they are understood.

## When the platform creates more friction than it removes

Watch for these signals:

- adoption requires mandate rather than preference;
- the common path still contains a human ticket queue;
- exception waiting time rises;
- teams fork, bypass, or duplicate the platform;
- platform-specific concepts take longer to learn than the underlying systems;
- upgrades and integrations dominate the roadmap;
- delivery throughput or stability worsens;
- a growing share of budget pays for coordination inside the platform team;
- vendor switching requires rebuilding identity, policy, evaluation, lineage, or audit evidence;
- the platform has no sunset criteria.

## Measures that make the rule falsifiable

- baseline and post-change workflow completion time;
- median and 95th-percentile waiting and exception time;
- duplicate implementations retired;
- percentage of common cases completed without human intervention;
- incidents, containment time, and blast radius;
- audit reconstruction time;
- evaluation coverage and escaped failures;
- cost per successful workflow outcome;
- platform staffing, support, and on-call load;
- voluntary adoption, abandonment, bypass, and satisfaction;
- provider or model switching time;
- time and cost to export or retire the capability.

## The missing evidence

The highest-value study would be an independent, preregistered, longitudinal comparison of teams facing the same repeated AI constraint and using:

1. documentation and training;
2. a template, library, or CLI;
3. a narrow managed or internal capability; and
4. a broad internal AI platform.

It should measure customer outcomes, delivery, reliability, compliance, developer experience, fully loaded ownership, exception handling, migration, switching, and exit. That result would either validate the smallest-capability rule or show where integration effects justify a broader platform.

## The 90-day signal

By **2026-10-26**, classify material AI-governance additions in a fixed public sample—Azure AI Gateway, AWS Bedrock/SageMaker, Google Vertex/Agent Platform, OpenTelemetry GenAI conventions, and Backstage—as:

- independently consumable primitives with APIs and export paths; or
- suite-only capabilities.

Portable primitives would support the view that the smallest useful AI platform is a thin portfolio of contracts and services. Suite-bound controls and evidence would indicate that vendors are successfully pulling the platform boundary outward.

## Bottom line

Shared work becomes a platform when advice and local reuse no longer remove a consequential repeated constraint, and one owned shared capability can remove it with lower total coordination and risk.

The smallest AI platform should therefore not begin as a portal, product category, or reference architecture. It should begin as evidence that one valuable workflow is blocked in the same way more than once.
