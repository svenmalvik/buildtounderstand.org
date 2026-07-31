# Chapter 4 Findings: Where Should the Platform End?

**Date:** 2026-07-30

**Related material:** [full research dossier](./research.md) · [community research](./07-community.md) · [validation report](./validation.md)

## Short answer

The platform should not end at one universal architectural line. It should end at a different place for each capability, and “ownership” should be split into separate decisions about the contract, source of truth, policy, runtime operation, enforcement, on-call, funding, and exit.

For an organization that has **not demonstrated** large repeated runtime demand, a real pooled-capacity advantage, a need for globally consistent decisions, or a regulated-evidence benefit, the best starting hypothesis is a thin but firm shared spine:

- versioned contracts and compatibility tests;
- integration with existing identity and credential systems;
- minimum non-bypassable security and compliance controls;
- reusable evaluation and telemetry plumbing;
- catalogue ingestion and provenance;
- cost allocation, exception, and retirement rules;
- an executable exit test.

The workflow team should retain model and prompt choices, tool meaning, business authorization, domain evaluation, orchestration, release judgment, and responsibility for the product consequence. Existing IAM, CI/CD, observability, service-catalogue, cloud, security, and FinOps platforms should provide most of the generic machinery.

This is a **scoped, falsifiable starting hypothesis**, not an industry consensus or universal law. It should be rejected for a capability when evidence shows that broader central operation removes more total work and risk, or supplies capacity and consistency that distributed teams cannot provide at comparable reliability and cost. Uber's Michelangelo, Google's TFX, Borg, and Zanzibar are important counterexamples: broad integrated platforms can be the correct answer when repeated demand and shared-state economies are sufficiently large ([Uber](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/); [TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/); [Borg](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/); [Zanzibar](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)).

The stopping rule is therefore:

> Share the smallest mechanism that demonstrably retires repeated work or enforces a necessary guarantee. Stop before the shared layer takes over workflow meaning that it cannot evaluate, operate, or support better than the team carrying the outcome.

## Evidence quality and what is not known

The evidence is good enough to reject a simple checklist—“the AI platform owns models, tools, identity, evaluations, observability, and deployment”—but not good enough to prove one boundary for every organization.

The strongest sources establish different things:

- **Specifications and official documentation** define what MCP, A2A, OpenTelemetry, Backstage, IAM, and policy systems do and do not promise. For example, MCP standardizes context exchange and tool invocation, but its tool annotations are not trusted enforcement by themselves ([MCP tools](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)). Backstage explicitly describes its catalogue as a cache over authoritative sources, not the ultimate source of dynamic truth ([Backstage](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)).
- **Regulator and public-interest records** show why observed state, recovery, least privilege, switching, and legal-role allocation matter. The EU AI Act distributes obligations across providers and deployers rather than requiring one central gateway ([European Commission](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)). The UK Competition and Markets Authority documents technical and commercial cloud-switching barriers that an organization-wide platform can amplify ([UK CMA](https://www.gov.uk/cma-cases/cloud-services-market-investigation)).
- **Research and industry surveys** provide useful associations, not causal proof. DORA reports platform-associated improvements in individual productivity, team performance, and organizational performance, while also reporting lower throughput and change stability and an additional throughput penalty from exclusive platform use ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). The honest conclusion is that platform use can help and harm at the same time, depending on independence and implementation.
- **Company case studies** expose real mechanisms and scale, but the authors benefit from the architecture being seen as successful. Google, Uber, and Spotify generally do not publish full platform headcount, exception queues, abandoned use cases, product-team integration labor, or decommissioning cost.
- **Community material** provides operational texture—bugs, queues, stale metadata, compatibility work, and workarounds—but it is qualitative and self-selected. Hacker News, Reddit, and GitHub are not a representative poll of engineers. Issue trackers over-sample failure; public forums under-sample ordinary application engineers who quietly adapt; vendor participation is not always obvious.

The most important missing evidence is a longitudinal, multi-organization comparison of the same capability operated as contract-only, federated, central-runtime, and vendor-managed models, stratified by organization size and workflow risk. It would need to publish central and product-team labor, delivery outcomes, incidents, exception latency, audit findings, switching time, and retirement cost. No source found meets that standard.

The validation verdict must also remain explicit: it is **not PASS**. All 237 distinct source URLs from the substantive angle files are present in the [full dossier](./research.md), with zero missing and no duplicate receipt URL. The remaining validation note is organizational: **153 complete receipts remain in a catch-all section rather than being reclassified into provenance subgroups**. This affects receipt organization, not the substantive findings, but it is why the [validation report](./validation.md) remains `NEEDS_IMPROVEMENT`.

## The deeper answer: ownership has multiple layers

Asking whether “the platform owns identity” or “the platform owns MCP” compresses several independent responsibilities into one word. For every capability, the organization should name at least these layers:

1. **Contract or interface:** who defines the vocabulary, schema, API, versioning, and compatibility rules?
2. **Source of truth:** where does the authoritative fact live, and who repairs it when it is wrong?
3. **Policy:** who decides what should be allowed, required, or prohibited?
4. **Runtime operation:** who keeps the service or data path available?
5. **Enforcement:** which component makes the non-bypassable decision?
6. **On-call and incident command:** who diagnoses the failure and coordinates recovery?
7. **Funding:** who pays for build, operation, integration, exceptions, and migration?
8. **Exit:** who proves the capability can be replaced and pays to remove it?

These owners often differ. The identity team may issue a principal, the domain service may decide whether that principal can refund an invoice, a gateway may impose an organization-wide provider restriction, and the product team may remain accountable for the user outcome. A catalogue may display the owner without being authoritative for authorization. A vendor may operate a runtime without assuming responsibility for the customer's data, configuration, workflow, or law; this division is explicit in cloud shared-responsibility models ([AWS](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/shared-responsibility.html)).

This decomposition resolves much of the apparent central-versus-local conflict. A policy can be common while enforcement is distributed. An evaluation runner can be shared while evaluation meaning remains local. A platform can define how integrations are exposed without implementing and supporting every integration.

## Capability-by-capability boundary

The table below is the recommended starting allocation for an organization that has not yet proved the conditions for a broader central runtime.

| Capability | Shared AI platform should own | Existing platforms should provide | Workflow/product team retains | Trigger for broader centralization |
|---|---|---|---|---|
| **Model access and gateway** | Provider-neutral identity, cost, trace, failure, and extension contracts; approved-provider policy integration; credential brokerage; common quotas and usage attribution; portability tests | Enterprise IAM, secrets, network controls, procurement, cloud accounts, common telemetry, and incident processes | Model/provider selection for the use case, prompts, provider-specific features, quality/cost trade-offs, fallback meaning, and product outcome | Many teams repeatedly implement the same routing, quotas, redaction, failover, or regional controls; mandatory policy must mediate every call; pooled inference capacity produces measurable savings; the gateway can be staffed and dual-run |
| **MCP and tools** | Protocol profile, admission schema, provenance, ownership metadata, version rules, conformance tests, registry, common auth hooks, minimum sandbox/egress controls, and audit format | IAM and consent, secrets, resource APIs, network policy, software provenance, observability, vulnerability handling, and incident response | Tool meaning, inputs and outputs, business invariants, data scope, side effects, domain authorization, implementation, and support | The same tool semantics are reused broadly and remain stable; a shared host/sandbox materially reduces risk; the central operator can support downstream failures without becoming the owner of the entire long tail |
| **Identity and authorization** | AI-specific integration profile: agent identity metadata, delegated-user context, requested scopes, policy inputs, evidence and revocation hooks | Existing IAM/OAuth/OIDC, workload identity, token issuance, policy stores, HR ownership, credential rotation, and resource entitlements | The requested business action, contextual access decision, consent and approval requirements, and residual-risk acceptance | Global consistency, causal ordering, revocation, or audit completeness cannot be achieved through existing IAM plus resource-side enforcement; the scale resembles a shared authorization service rather than a new AI-only directory ([Zanzibar](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)) |
| **Evaluation** | Common runner, dataset/evaluator formats, scheduling, lineage, reproducibility, evidence storage, comparison UI, and baseline adversarial suites | CI/CD gates, artefact storage, data governance, access control, and risk systems | Representative cases, expected outcomes, domain harms, human-review rules, thresholds, release decision, and response to drift | Many workflows share stable evaluation primitives or regulatory evidence; one operated service removes substantial duplicate machinery without replacing domain judgment; results remain exportable and rerunnable elsewhere |
| **Observability** | AI semantic extensions, trace propagation requirements, model/tool/evaluation correlation, and minimum evidence profile | Existing OpenTelemetry SDKs/collectors/backends, logging, metrics, tracing, retention, access control, incident tooling, and privacy controls | Product SLOs, outcome annotations, alert thresholds, incident severity, domain dashboards, and interpretation | Repeated AI instrumentation and redaction work is genuinely common; a shared pipeline can meet privacy and cardinality constraints; central operation improves diagnosis without creating a sensitive, opaque surveillance store ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/)) |
| **Deployment and runtime** | AI artefact profile for models, prompts, tools, agent graphs, evaluation evidence, policy versions, and rollback references | Existing CI/CD, environments, provenance, approval, rollout, rollback, cloud/Kubernetes/serverless substrate, and runtime SLOs | Release timing, workload configuration, semantic health, rollback safety, capacity impact, and business continuity | AI execution introduces a genuinely different scheduling, isolation, state, latency, or evidence primitive; pooled capacity or specialist operations retire more work than a parallel runtime creates ([Borg](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/)) |
| **Integrations** | Exposure pattern, authentication, timeout, retry, idempotency, version, lifecycle, conformance, telemetry, and retirement requirements | API management, network and secrets, service catalogue, connector runtime, delivery, and security review | Domain mapping, correctness, reconciliation, side effects, downstream relationship, and support | Multiple teams need substantially the same stable semantics; a funded shared owner can diagnose the external system, carry the pager, maintain versions, and decommission credentials |
| **Catalogue metadata** | Agent-specific schema, validation, provenance, freshness rules, lifecycle, and links to observed evidence | Existing developer portal/catalogue ingestion, search, presentation, ownership systems, and repository integrations | Purpose, owner, docs, lifecycle intent, dependencies, disputed meaning, and changes near the code | Discovery volume justifies richer ingestion and graph operation; never centralize live authorization into the catalogue merely because the metadata is convenient. Backstage's own guidance supports catalogue-as-cache rather than catalogue-as-truth ([Backstage](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)) |
| **Governance, cost, and exceptions** | Risk tiers, mandatory floors, required evidence, cost tags, exception schema, review cadence, expiry, and retirement contract | Legal/risk registers, IAM, policy engines, FinOps allocation, procurement, audit stores, privacy systems, and incident management | Use-case value, residual-risk acceptance within limits, local control design, exception rationale, outcome monitoring, and remediation | A common evidence or control plane removes repeated regulatory work or closes material inconsistency; enforcement remains at the earliest correct non-bypassable boundary rather than defaulting to one central gateway |

The repeated pattern is deliberate: the AI layer should usually define the AI-specific contract and evidence, existing platforms should provide mature generic machinery, and the workflow team should retain contextual judgment. Broader centralization is a result to earn with measured demand, risk, consistency, or capacity—not a maturity level to assume.

## Explicit answers to every Chapter 4 question

### 1. Are model access, tools, identity, evaluation, observability, and deployment all platform responsibilities?

They are all **platform concerns**, but not all end-to-end platform possessions.

- Model access benefits from shared credentials, provider policy, cost attribution, and trace contracts; workflow teams retain model and fallback choices.
- Tools benefit from admission, provenance, auth patterns, sandboxing, and audit; domain teams retain the tool's meaning and support.
- Identity should extend the enterprise identity platform; an AI team should not create a second identity authority.
- Evaluation benefits from a shared runner and evidence format; domain owners decide what good and harmful mean.
- Observability should extend the existing telemetry platform; product teams own SLOs and incident meaning.
- Deployment should extend existing delivery and runtime platforms unless AI introduces a genuinely different execution primitive.

### 2. Which capabilities are necessary from the beginning?

Begin with the minimum needed to make one real workflow accountable and replaceable:

1. a versioned contract with owner, purpose, lifecycle, risk, interface, and dependency metadata;
2. integration with existing identity, credential, and resource-side authorization;
3. explicit tool/model provenance and requested scopes;
4. references to evaluation evidence and the domain owner who sets acceptance;
5. trace context, cost attribution, redaction, and retention rules;
6. deployment revision, runtime owner, rollback, and incident runbook references;
7. an exception and deprecation process;
8. an exit test against a second implementation.

A mandatory gateway, new catalogue, separate CI/CD system, central agent runtime, universal evaluation service, or platform-owned integration estate is not automatically necessary on day one.

### 3. Should the platform own integrations, or only define how integrations are exposed?

Define exposure by default. Own an integration only when its semantics are genuinely shared, its reuse is measured, and the platform has the funding, downstream knowledge, versioning capacity, and on-call commitment to support it.

The domain team should own a connector when it changes with business rules or when failures require domain judgment. A platform-owned connector to “invoices” is not reusable if every consumer means something different by invoice, approval, reconciliation, or reversal.

### 4. Are MCP-related tools part of an AI platform?

MCP is part of the platform's **interoperability and governance surface**, but it does not make every MCP server a platform asset. The shared layer can own a supported protocol profile, registry, conformance, admission, provenance, common client/host components, auth hooks, audit format, and minimum sandbox controls. The tool and downstream service stay with the team that understands their side effects and can repair them.

MCP discovery is not authorization. A server description or `readOnly` annotation cannot prove safety; the resource must enforce the business action with fresh identity and state ([MCP security guidance](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)).

### 5. Should the AI platform own the agent catalogue?

Usually no. It should define and validate agent-specific metadata, then publish it into the existing developer platform. Authoritative fields should remain near the workflow or in the system that already owns them: repository for version and intent, IAM/HR for identity and ownership, delivery system for deployed revision, risk system for decisions, and telemetry for observed behavior.

The catalogue should ingest, index, display provenance, and show freshness. It should not become the live authorization path. A separate AI catalogue is justified only if the existing developer platform cannot represent required agent lifecycle or evidence after a measured extension attempt.

### 6. Which capabilities should be centralized, and which should remain with teams?

Centralize stable, repeated, cross-cutting mechanisms and mandatory organization-wide floors: identity integration, credential brokerage, common interfaces, baseline policy, reusable telemetry and evaluation plumbing, cost allocation, provenance, conformance, and evidence retention.

Keep contextual and rapidly changing meaning with teams: prompts, model suitability, tool behavior, business permissions, domain test cases, orchestration, product SLOs, release judgment, incident interpretation, and end-user consequences.

Centralize runtime operation only when one of four conditions is demonstrated: repeated demand at material scale, pooled-capacity advantage, required global consistency, or a shared regulated-evidence/control benefit.

## Research and precedents

The history does not point in one direction. It shows boundaries moving as scale, technology, and ownership economics change.

- **EC2, 2006-08-24:** AWS placed capacity, virtualization, metering, and an API behind a managed boundary while customers kept images and applications. This is the clean narrow-service precedent: centralize an expensive repeated primitive, not product logic ([AWS](https://aws.amazon.com/about-aws/whats-new/2006/08/24/announcing-amazon-elastic-compute-cloud-amazon-ec2---beta/)).
- **Michelangelo, 2017-09-05:** Uber described teams repeatedly building bespoke training and serving systems, then centralized data, training, evaluation, deployment, serving, and monitoring. Uber now reports about 400 active ML projects, more than 20,000 monthly training jobs, more than 5,000 production models, and 10 million peak predictions per second. This is serious evidence that integrated lifecycle ownership can pay at Uber-like scale, though it remains operator-authored and omits fully loaded cost ([Uber](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/)).
- **TFX, 2019-05-20:** Google's peer-reviewed case reports one deployment moving from months to weeks and coinciding with a 2% increase in Google Play installs. It supports shared lifecycle machinery, not the claim that every organization needs Google's perimeter ([TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/)).
- **Borg and Zanzibar:** Borg demonstrates pooled scheduling and utilization economies; Zanzibar demonstrates globally consistent authorization at extreme scale. They falsify any rule that thinness is always more liberating. A mature central capability can create freedom from toil that local teams could not reproduce ([Borg](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/); [Zanzibar](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)).
- **Backstage, 2020-03-16:** Spotify separated catalogue and developer experience from the systems being presented. This supports using an existing portal as an index while sources and runtimes remain distributed. Spotify's productivity figures are observational and lack a non-user control, so they are evidence of association rather than causation ([methodology](https://backstage.spotify.com/discover/blog/how-spotify-measures-the-value-of-backstage)).
- **Kubernetes dockershim, 2022-05-03:** Kubernetes retained the Container Runtime Interface and removed the bundled Docker adapter. This is a direct precedent for keeping the contract while externalizing a vendor-specific implementation and lifecycle ([Kubernetes](https://kubernetes.io/blog/2022/05/03/kubernetes-1-24-release-announcement/)).
- **GOV.UK PaaS, 2022-07-12:** GDS chose to decommission a platform rather than fund a major rewrite after the surrounding cloud market and departmental capabilities changed. Platform scope is not permanent; a capability that once created leverage can later create more ownership cost than value ([GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)).

The common lesson is not “thin wins.” It is that platform boundaries must have admission, operating, and retirement criteria. The contract is valuable when it preserves an architectural seam. It is theatre when consumers mistake declared metadata for observed truth or when no implementation can prove conformance.

## What the communities say

The sampled conversation lives mainly on Hacker News, Reddit, GitHub, practitioner blogs, and platform conferences. The texture differs by venue:

- Hacker News is most suspicious of abstraction tax, renamed silos, YAML over YAML, and security products built after connectivity.
- Reddit provides more organization-size, build-versus-buy, support, and Backstage/gateway operating detail, but also contains vendors participating in practitioner threads.
- GitHub issues reveal concrete seams—deletion, freshness, configuration portability, authorization, and provider compatibility—but say nothing reliable about prevalence.
- Practitioner writing is more favorable to platforms, provided they are treated as products with self-service, feedback, support, and escape paths.
- Conference material is useful for strategic frames but overrepresents programs that survived and people selling platform expertise.

This evidence is **qualitative and self-selected**. It can reveal failure mechanisms and recurring concerns; it cannot establish what “engineers” as a population believe.

### What ordinary and hands-on engineers say

The strongest ordinary-engineer theme is conditional support: centralize a burden they can name, but do not replace an understandable system with an opaque queue.

> “Bad platforms narrow possibilities.”
>
> — `BlackFly`, platform-team engineer, [Hacker News, 2023-06-25](https://news.ycombinator.com/item?id=36465932)

> “another tool getting in between the devs and the work”
>
> — `NormalUserThirty`, on Backstage, [Reddit, 2023-07-28](https://www.reddit.com/r/devops/comments/15bke0w/comment/jtrqo04/)

> “it has many bugs and it's really over-complicated”
>
> — `sammcj`, describing gateway use with clients, [Reddit, 2025-05-14](https://www.reddit.com/r/LocalLLaMA/comments/1kmragz/comment/msdwh8r/)

> “treating MCP manifests like deploy artifacts, not config”
>
> — `jake_that_dude`, on production MCP governance, [Reddit, 2026-06-02](https://www.reddit.com/r/ClaudeAI/comments/1tuqqpn/comment/opcznh0/)

There is also an ordinary-practitioner case for breadth:

> “80% of this stuff is common between solutions - so put that shit behind a button.”
>
> — `lucidguppy`, [Reddit, 2023-12-11](https://www.reddit.com/r/devops/comments/18fshs8/comment/kcwc1nx/)

The disagreement is not really about reuse. It is about whether the shared layer removes the repeated work or merely relocates it into platform configuration, compatibility bugs, tickets, and exceptions.

### What maintainers and direct implementers say

Maintainers focus less on the platform slogan and more on lifecycle work:

> “Configuration of the collector is a major barrier to entry for users.”
>
> — `djaglowski`, OpenTelemetry maintainer, [GitHub, 2023-09-06](https://github.com/open-telemetry/opentelemetry-collector/issues/8372)

> “Today every MCP client invents its own format for server configuration”
>
> — `BobDickinson`, MCP contributor, [GitHub, 2026-04-22](https://github.com/modelcontextprotocol/modelcontextprotocol/pull/2633)

> “Taking too long for the registered entity to show up in the catalog. sometimes from hours to days to never.”
>
> — `dayadev`, Backstage adopter, [GitHub, 2022-09-23](https://github.com/backstage/backstage/issues/13834)

These comments show what the platform actually owns after launch: templates, compatibility, freshness, migration, permissions, deletion, diagnostics, and repair.

### What executives, consultants, founders, and vendors say

These voices are useful but have different stakes from ordinary users:

> “platforms must be compelling to use, they cannot stand on a mandate alone”
>
> — Evan Bottcher, independent technology leader, [2018-03-05](https://martinfowler.com/articles/talk-about-platforms.html)

> “all engineers run the code they write—but we divide the areas of responsibility by layer or function”
>
> — Charity Majors, Honeycomb co-founder, [2022-09-30](https://charity.wtf/p/the-future-of-ops-is-platform-engineering)

> “every dollar spent on a platform engineer is a dollar you can't spend on delivering features”
>
> — Brian Guthrie, then Orgspace co-founder and CTO, [2022-06-10](https://2022.platformcon.com/talk/is-the-optimal-size-of-a-platform-team-zero)

Cloud and AI vendors increasingly bundle gateway, identity, memory, policy, evaluation, observability, deployment, and support. Their product maps are evidence that these functions require operation; they are not evidence that one vendor or one internal team should own all of them.

### Where engineers disagree

1. **Framework or product:** some teams want a malleable framework such as Backstage; others expected an installable, supported portal and see framework ownership as an unexpected product-development commitment.
2. **Gateway scope:** some engineers value one place for credentials, quotas, audit, and fallback; others experience provider-compatibility translation as a permanent new failure surface.
3. **Local freedom or duplicated toil:** application teams value control and fast exceptions; platform teams report inheriting locally built infrastructure after owners leave.
4. **Federation or ownership vacuum:** contribution can preserve local knowledge, but shared components decay when no team is funded to support other users.
5. **Optionality:** advocates see voluntary paved roads as a quality pressure; control functions worry that optional paths make mandatory evidence and security inconsistent.
6. **What “self-service” means:** executing without a ticket is not enough if only the platform team can interpret the error or repair the abstraction.

## The strongest counterarguments

The thin starting hypothesis survives only if it engages the strongest case against it.

### A contract can become coordination theatre

A schema cannot ensure current state, correct implementation, or runtime enforcement. OpenAPI notes that schemas do not catch every specification violation; Backstage says its catalogue is a cache; MCP says annotations are not trusted guarantees. A contract must therefore include conformance tests, provenance, observed-state evidence, error behavior, and a real implementation. Otherwise the organization has standardized descriptions while leaving duplicated adapters and inconsistent controls untouched.

### Integrated lifecycle machinery can remove more work

Michelangelo and TFX show why data, training, evaluation, deployment, serving, and monitoring may compound when operated together. At sufficient scale, the local alternative is not freedom; it is many fragile copies. The correct response is to measure the scale threshold and full cost, not to dismiss broad integration because it is broad.

### Central runtime can increase practical engineering freedom

Borg's pooled scheduling and Zanzibar's consistency show that central capability can free product teams from machinery they could technically own but could not operate efficiently or safely. Freedom to replace the service and freedom from infrastructure toil are both real. The design must preserve an exit without pretending local reimplementation is costless.

### Global controls and regulatory evidence may need shared operation

Identity, revocation, policy consistency, and audit evidence can fail when every team interprets them differently. Regulation does not mandate one gateway, but repeated evidence collection and lifecycle controls can create a genuine shared-service economy. A federated model—central policy and evidence with distributed enforcement—may be a better answer than either extreme.

### Federation has incentive failures

Local teams optimize for their product. They may not fund documentation, compatibility, support, and migration for other consumers. A shared contract does not create a maintainer. Any federated design needs contribution rules, support commitments, funding, and a way to retire abandoned components.

These arguments make the conclusion contingent: broad integration may be right at Uber or Google scale, for a globally consistent authorization service, for pooled inference capacity, or for regulated evidence. The chapter should present those as falsifiers of a thin boundary, not footnotes.

## Total work and power effects

Platform scope should be evaluated against **total work per successful, governed, replaceable workflow**, not the platform team's feature count or adoption number.

Count at least:

- central build and roadmap capacity;
- 24/7 staffing, pager load, incident command, and capacity planning;
- product-team adapters, metadata, evaluation sets, onboarding, and diagnosis;
- security, privacy, legal, risk, audit, procurement, and FinOps work;
- tickets, exception queues, training, documentation, and rework;
- vendor, model, cloud, network, storage, telemetry, and support spend;
- policy and metadata reconciliation;
- migration, dual running, re-evaluation, data export, and decommissioning;
- lost local skill and the time required to understand an abstraction during failure.

Google SRE's operating guidance makes clear that runtime ownership implies staffing, toil limits, readiness, and the ability to hand a service back—not merely a box on an architecture diagram ([Google SRE](https://sre.google/sre-book/evolving-sre-engagement-model/)). FinOps guidance similarly makes allocation necessary: an opaque central bill cannot show cost per product outcome ([FinOps](https://www.finops.org/wg/cloud-cost-allocation/)).

The boundary also redistributes power:

- the gateway owner controls reachability, provider choice, quotas, and possibly the data path;
- the catalogue owner controls discoverability, not necessarily truth;
- the identity team controls principals and credentials;
- the policy owner controls what is permissible;
- the resource owner controls the business action;
- the platform operator controls incident priority and exception latency;
- procurement controls commercial commitment and switching terms;
- the workflow owner carries the product consequence.

Calling all of these actors “the platform” hides the real governance design. Every central capability should therefore publish not only an API but its decision rights, vetoes, service level, support boundary, funding model, and reversal condition.

## Practical responsibility model

| Layer | Primary accountable actor | What that actor must provide | What it must not silently assume |
|---|---|---|---|
| **Contract/interface** | AI contract steward with consumers | Versioned schema, compatibility policy, extensions, examples, conformance suite, deprecation | That schema compliance proves runtime safety or business correctness |
| **Source of truth** | Existing authoritative system or workflow owner | Provenance, update path, reconciliation, freshness, deletion, ownership repair | That the catalogue copy is authoritative because it is convenient |
| **Policy** | Resource/domain owner for business policy; security/legal/risk for mandatory floors | Explicit decisions, inputs, versioning, exceptions, review and expiry | That the operator of an enforcement point owns the policy judgment |
| **Runtime operation** | Existing platform, qualified shared team, or vendor named per capability | SLO, capacity, telemetry, degraded mode, change management, incident response | That operating infrastructure transfers product accountability |
| **Enforcement** | Earliest correct non-bypassable boundary, usually gateway for global provider rules and resource service for business actions | Fresh identity and state, least privilege, auditable decision, fail behavior, revocation | That descriptive metadata, a catalogue listing, or model behavior enforces policy |
| **On-call** | Team with diagnostic access and authority to repair its layer | Pager, runbook, escalation, incident command, handback criteria | That a product team can own a black-box platform failure or that platform SRE can judge domain impact alone |
| **Funding** | Beneficiary and control owner through explicit central funding plus allocation | Build, run, support, integration, exception, migration, and retirement budgets | That work performed by product teams or OSS maintainers is free |
| **Exit** | Platform product owner and consuming owners jointly | Export, second implementation, dual-run plan, evidence continuity, credential revocation, deletion and decommission | That an open API makes policy, identity, state, evidence, and operating knowledge portable |

## Decision rules and scorecard

Use the thin shared spine as the starting hypothesis only while the organization has not proved one of the broadening conditions. For each capability:

1. **Observed constraint:** identify a real workflow delay, repeated implementation, incident pattern, capacity problem, or obligation. Do not start with the desired platform feature.
2. **Repeated-demand test:** show that several teams face substantially the same problem, or that one mandatory control applies across the organization. Define “several” locally.
3. **Net-work test:** estimate work retired minus central operation, exported team work, support, exceptions, migration, and exit. A transfer of work is not leverage.
4. **Stable-semantics test:** centralize only the part whose meaning is sufficiently common. Rapidly changing domain meaning remains local.
5. **Guarantee test:** if a requirement is mandatory, name the non-bypassable enforcement point. A contract or catalogue entry is not an enforcement mechanism.
6. **Authority test:** separately name policy owner, source-of-truth owner, operator, enforcer, on-call, risk acceptor, funder, and exit owner.
7. **Self-service and diagnostic test:** the normal path requires no ticket, and a consuming team can understand a failure without privileged platform access.
8. **Exception test:** a legitimate exception has a named decider, service level, compensating control, expiry, and observable queue.
9. **Existing-platform test:** first test whether IAM, CI/CD, observability, catalogue, security, cloud, data, and FinOps platforms can be extended.
10. **Operations test:** do not centralize runtime without funded SLO, capacity, telemetry, incident, pager, and handback commitments.
11. **Exit test:** a second implementation consumes the contract; configuration and evidence export; dual running works; removal is funded.
12. **Review test:** set an ADR review date and a threshold for moving the boundary inward or outward.

The scorecard should combine:

- task success for common and exceptional workflows;
- lead time and waiting time;
- throughput and change stability;
- incident frequency, blast radius, detection, and recovery;
- platform-team and exported product-team labor;
- support volume and exception latency;
- voluntary retention, bypasses, and local workarounds;
- cost per successful governed outcome;
- audit completeness and policy drift;
- time and work to switch, dual-run, and decommission.

Adoption, entities registered, gateway calls, or capabilities shipped are diagnostic inputs, not success by themselves. DORA's simultaneous positive and negative findings are the warning: a platform can improve perceived productivity while harming throughput and stability ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)).

## Prototype implications for the proposed agent contract

The site should build the contract as a testable seam, not as a miniature platform.

### What the first contract should contain

| Field group | Minimum content | Why |
|---|---|---|
| **Identity and lifecycle** | Stable agent ID, version, owner, repository, status, created/updated timestamps, deprecation date | Makes ownership and removal machine-readable without inventing a new identity authority |
| **Purpose and risk** | Intended outcome, users, prohibited uses, risk tier, data classes, jurisdictions | Prevents a generic agent record from concealing materially different workflows |
| **Interfaces** | Input/output schemas, model requirements, tool references, events, protocol/version, supported extensions | Creates compatibility seams while keeping provider-specific capability visible |
| **Authority** | Requested scopes, delegated-user requirements, approval points, resource and policy references, revocation method | Describes requested authority without turning metadata into permission |
| **Evaluation evidence** | Dataset and evaluator references, versions, domain owner, required baseline, latest run, release decision | Separates shared evidence mechanics from contextual judgment |
| **Observability and privacy** | Trace fields, correlation ID, content-capture rules, redaction, retention, access, region | Makes diagnosis portable without assuming full prompt capture is safe |
| **Deployment and operation** | Artefact revision, runtime reference, environments, current observed revision, SLO, on-call, runbook, rollback | Connects declared metadata to observed operation |
| **Cost and funding** | Cost centre, usage tags, budget owner, relevant quotas, support allocation | Makes hidden central and local work visible |
| **Exit and retirement** | Export format, alternate implementation, dual-run procedure, dependency and credential removal, evidence retention/deletion | Makes engineering freedom executable rather than rhetorical |
| **Provenance and freshness** | Authoritative source for each referenced fact, last observation, freshness limit, reconciliation status | Prevents the catalogue from becoming stale truth |

### How it should work

1. Keep the descriptor beside the agent or workflow code. Reference IAM, risk, evaluation, deployment, and telemetry records instead of copying their truth.
2. Validate syntax, compatibility, ownership, required evidence, and deprecation in CI.
3. Publish the descriptor to the existing developer catalogue. Show provenance, freshness, observed deployment state, and unresolved differences.
4. Keep runtime authorization out of the catalogue. The gateway may enforce provider and credential floors; the resource service enforces the business action.
5. Provide a compatibility diff and deprecation tool so a contract change exposes affected consumers before release.
6. Add one representative MCP tool and one non-MCP integration. Apply the same ownership fields to both, testing whether MCP is an exchange profile rather than a special ownership category.
7. Add a small evaluation envelope and trace envelope that can be exported and rerun through two implementations.
8. Do not build a new gateway, runtime, evaluation service, or catalogue until prototype measurements show repeated work or a guarantee the contract and existing platforms cannot supply.

### Prototype acceptance criteria

The prototype succeeds if:

- a second workflow can adopt the contract without copying workflow-specific semantics;
- the catalogue can be rebuilt from authoritative sources;
- a stale or orphaned record is visible rather than silently trusted;
- a tool cannot gain authority merely by changing metadata;
- an engineer can trace model, tool, policy, evaluation, deployment, owner, and incident references for one execution;
- a second runtime can consume most of the same operational contract;
- removal revokes credentials, retires discovery, preserves required evidence, and leaves no hidden platform dependency.

The prototype fails usefully if it reveals that the contract needs a runtime guarantee. That is the point of building it: to discover the boundary rather than encode an opinion.

## The 90-day exit drill

By **2026-10-28**, move one representative, non-trivial workflow between two model/runtime stacks while keeping the domain tool implementations unchanged.

Preserve:

- least-privilege identity and delegated scope;
- approval behavior and resource-side authorization;
- MCP/A2A interfaces where used;
- evaluation cases, evaluator versions, raw results, and release evidence;
- OpenTelemetry trace meaning and redaction;
- ownership metadata, runbook, and cost attribution.

Measure the percentage of the operational contract that survives unchanged. Use these as proposed local criteria, **not industry benchmarks**:

- thin-boundary signal: at least 80% survives, domain-code changes stay at or below 20%, and the move takes no more than five engineer-days;
- thick-boundary signal: credentials, policies, evaluation history, trace meaning, approval flow, or catalogue state must be manually reconstructed even though the endpoint remains “compatible.”

The drill matters because portability is broader than an API. It includes identity, policy, evidence, state, operations, and the ability to leave.

## Open questions and missing evidence

1. At what number of similar teams, requests, models, or tools does shared runtime operation repay its support and blast-radius cost?
2. Which guarantees truly require synchronous central mediation, and which can use admission plus distributed enforcement?
3. How should total work be measured across central budgets, product teams, control functions, vendors, and maintainers?
4. Which provider differences should a gateway expose rather than normalize?
5. How should a human principal, agent version, delegated scope, approval, resource action, and revocation be bound into one auditable event? NIST still treats agent identity and authority as an active standards problem ([NIST](https://www.nccoe.nist.gov/publications/other/accelerating-adoption-software-and-ai-agent-identity-and-authorization-concept)).
6. Which evaluation suites are reusable without turning domain validity into a generic score?
7. What prompt, tool, identity, and evaluation content may be retained, in which region, for how long, and with whose access?
8. What is an acceptable exception response time, and when do bypasses prove that the paved road is the wrong shape?
9. Can the proposed on-call owner actually diagnose both platform and domain failure at 03:00?
10. What would it cost to retire the capability, including dual running, re-evaluation, credential removal, training, and lost operational knowledge?
11. What do ordinary application engineers, regulated-industry teams, quiet non-adopters, and teams that abandoned platforms say in a structured, representative study?
12. Can an independent comparison reproduce the claimed benefits of Michelangelo, TFX, Zanzibar, or Backstage at ordinary organizational scale?

## Conclusion

The platform should end where shared value stops exceeding shared ownership cost.

That boundary is not a list of AI features. It is a capability-by-capability allocation of contracts, truth, policy, operation, enforcement, on-call, funding, and exit. Start with a contract and existing enterprise platforms only as a scoped hypothesis for an organization that has not proved the case for broader operation. Centralize further when repeated demand, pooled capacity, global consistency, or regulated evidence makes the broader service measurably better.

The principle for Chapter 4 is therefore:

> A platform creates leverage when it removes more total work and risk than it creates, while leaving the people who understand the workflow able to change it, diagnose it, replace it, and carry its consequences.
