# Mechanism: deciding and operating the AI-platform boundary

Research date: 2026-07-30

## What I'm unpacking

The mechanism is how an organization repeatedly decides, encodes, enforces, operates, and later moves the boundary among an AI platform, an existing developer platform, workflow-owning product teams, control functions, vendors, and runtime systems.

The central finding is that “ownership” is too coarse a word for this decision. A useful boundary separates at least six rights and duties: defining policy, defining an interface, stewarding the source of truth, running the data path, enforcing a decision, and supporting failures. The CNCF platform guidance makes a similar separation implicitly: platform teams own user-facing interfaces and experiences while collaborating with the teams that implement infrastructure and supporting services; it also says platform capabilities should prioritize common use cases rather than one-team-specific needs ([CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/)).

## The walkthrough

1. **Start with an observed workflow constraint, not an inventory of attractive platform features.** The product team supplies a concrete workflow, risk tier, current lead time, failure history, duplicated work, and exit requirement; platform, security, SRE, data, and domain owners identify which parts recur across teams. The output is a problem statement and baseline measures, not a platform roadmap. It can fail when “AI platform” is assumed to be the solution before repeated demand exists. CNCF explicitly frames a platform as a product whose roadmap is learned from users and whose common cases take priority over capabilities needed by one team ([CNCF white paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/)); Fowler's “thinnest viable platform” treatment asks for the smallest helpful capability and an upgrade or migration path ([Fowler](https://martinfowler.com/articles/platform-prerequisites.html)).

2. **Decompose the candidate capability into ownership layers.** For model access, tools, identity, evaluation, observability, deployment, integrations, MCP, or catalogue data, the actors assign: policy authority; schema/API ownership; authoritative data stewardship; provisioning; runtime operation; enforcement; on-call and incident command; funding; and decommissioning. The input is the problem statement; the output is a responsibility map with one accountable owner for each layer. It fails when a platform team is labelled “owner” but a control function retains veto power, a vendor runs the service, and a product team still carries the business outcome.

3. **Select an operating model capability by capability.** The decision group compares contracts-only, central runtime, federated control, and vendor service against risk, reuse, latency, blast radius, local knowledge, support capacity, switching cost, and reversibility. The output is an architecture decision record with a review date and removal test. It fails when centralization is treated as maturity or when buying a managed service is mistaken for transferring accountability; AWS's Bedrock guidance says AWS secures the service infrastructure while customers remain responsible for their data sensitivity, requirements, laws, and service configuration ([AWS Bedrock security](https://docs.aws.amazon.com/bedrock/latest/userguide/security.html)).

   | Model | What the shared layer owns | What remains local | Best fit | Characteristic failure |
   |---|---|---|---|---|
   | **Contracts-only** | Vocabulary, schema, compatibility tests, discovery metadata | Runtime, provider calls, integrations, evaluation, deployment, support | Early or heterogeneous estate; low-cost coordination; exit matters | Declared metadata is mistaken for observed truth or runtime enforcement |
   | **Central runtime** | Gateway/runtime data path, credentials, routing, quotas, policy enforcement, common telemetry, on-call | Workflow semantics, domain evaluation, product outcome, some tool implementations | Repeated cross-cutting controls and sufficient operating capacity | Common-mode latency/outage, bottleneck, abstraction leakage |
   | **Federated control** | Central policy and contract, distributed policy engines/enforcement and domain runtimes | Local operation, domain policy, integrations, evaluation | Large or regulated estate needing global floors and local context | Policy-version skew, conflict, ambiguous incident ownership |
   | **Vendor service** | Vendor-operated infrastructure and the contracted managed features | Correct configuration, data, application logic, domain risk, portability, vendor incident handling | Commodity capability where vendor operation removes more work than integration creates | Lock-in, quota/region/API ceilings, opaque failure, responsibility gaps |

   This is not a once-for-the-whole-platform choice. OPA, for example, documents a federated pattern: policies and decision telemetry are centrally managed while lightweight policy engines run beside services for low-latency, highly available decisions ([OPA management architecture](https://www.openpolicyagent.org/docs/management-introduction)). A different capability in the same organization can remain a contract or use a vendor runtime.

4. **Publish the smallest enforceable contract at the system of record.** The contract owner supplies versioned schemas for identity, ownership, risk tier, model/tool requirements, evaluation evidence, telemetry fields, and deployment references. Product teams keep descriptors close to their code or authoritative domain system; CI validates syntax and compatibility; the existing developer platform ingests and presents the result. The output is discoverable, machine-readable metadata. It fails when annotations are treated as controls: JSON Schema distinguishes annotations from validation ([JSON Schema](https://json-schema.org/understanding-json-schema/reference/metadata)), and Backstage recommends treating its catalogue as a cache over authoritative sources rather than the ultimate source of truth ([Backstage catalogue graph](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)).

5. **Bind human, workload, and delegated-agent identity at the action boundary.** Identity teams establish authentication and credential lifecycle; product/domain owners define permitted business actions; the platform may provide common token exchange, secrets delivery, and policy-decision APIs; the service or tool that can cause the effect enforces the decision. Inputs are principal, delegated user, target resource, requested action, context, and risk; output is an allow, deny, or approval-required decision plus an audit record. It fails when identity is propagated without audience binding or when authentication is confused with authorization. The MCP authorization specification requires tokens bound to the intended resource and forbids passing an inbound token through to downstream APIs ([MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)).

6. **Insert shared runtime mediation only for controls that need the data path.** If model-provider credentials, quotas, provider routing, regional restrictions, or uniform request telemetry must be enforced on every call, the platform operates a model gateway or adopts a vendor service. Inputs are an authenticated request, model intent, budget, policy, provider health, and region; outputs are a routed request, response, usage record, and trace. It fails when the gateway becomes a reasoning/orchestration layer or when all providers are reduced to a leaky lowest-common-denominator API. Microsoft's reference architecture shows the concrete runtime duties—authentication, policy evaluation, routing with backend credentials, and OpenTelemetry emission—rather than “governance” as an abstract box ([Azure AI Gateway](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)).

7. **Expose tools and integrations without centralizing their domain semantics.** The domain team owns the downstream API, business invariants, tool implementation, input/output sanitization, and operational support. The platform can own the exposure contract, registry admission, client libraries, sandbox or egress controls, delegated-auth pattern, and audit format. Inputs are a tool descriptor, provenance, scopes, risk classification, test evidence, and support owner; output is an approved discovery record and callable endpoint. It fails when listing a tool is equated with approving it: MCP defines dynamic discovery and execution but says tool annotations are untrusted unless the server is trusted ([MCP architecture](https://modelcontextprotocol.io/docs/learn/architecture), [MCP tools](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)).

8. **Evaluate at both the shared component and complete-workflow levels.** The AI/platform team can maintain harnesses, dataset formats, evaluator infrastructure, baseline safety suites, and evidence storage. The workflow-owning team owns task-specific cases, acceptable error trade-offs, human review, and the release decision; risk or compliance owners set mandatory floors for high-impact uses. Inputs include a versioned application chain, representative data, expected outcomes, risk tolerance, and production feedback. Outputs are reproducible evidence and a named go/no-go decision. It fails when a model score substitutes for end-to-end behavior: Google Cloud says tightly coupled chains require end-to-end evaluation, complete-artifact versioning, component lineage, and continuous monitoring ([Google Cloud architecture](https://docs.cloud.google.com/architecture/deploy-operate-generative-ai-applications)); NIST places testing, evaluation, verification, validation, monitoring, incident response, override, and decommissioning across the lifecycle ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)).

9. **Deploy through the existing delivery platform unless AI changes the deployment primitive.** The developer platform owns generic build provenance, environment controls, secrets release, rollout mechanics, and rollback hooks. The AI capability contributes model/prompt/tool/evaluation artefacts and their checks; the product team owns configuration and production acceptance. Inputs are a versioned release, evaluation evidence, target environment, and approval policy; outputs are a staged deployment and observable revision. It fails through partial rollout, untested resource behavior, or unclear rollback semantics. GitHub environments demonstrate that approval, branch restrictions, external protection rules, and secret release can remain generic deployment capabilities ([GitHub deployment environments](https://docs.github.com/en/actions/reference/workflows-and-actions/deployments-and-environments)); Argo CD shows that even automated reconciliation keeps deletion, pruning, self-healing, retry, and rollback semantics as explicit choices ([Argo CD automated sync](https://argo-cd.readthedocs.io/en/latest/user-guide/auto_sync/)).

10. **Operate exceptions, incidents, and boundary changes as first-class flows.** Every mandatory control has an exception owner, expiry, compensating control, and observable bypass; every runtime dependency has an SLO, on-call owner, degraded mode, and incident interface; every capability has adoption, total-work, switching, and removal measures. Reviewers can move a layer inward, outward, to an existing platform, or to a vendor when evidence changes. The output is a boundary that can evolve rather than a permanent organizational claim. It fails when exceptions become invisible shadow paths or when a platform cannot be replaced. Fowler recommends voluntary adoption and explicitly treats internal platforms as capable of creating vendor-like lock-in ([Fowler](https://martinfowler.com/articles/platform-prerequisites.html)).

## Inputs and dependencies

| Input or dependency | Specific instance | Why the boundary depends on it | Owner that should remain visible |
|---|---|---|---|
| **Demand and workflow evidence** | User interviews, workflow traces, support tickets, incident history, duplicate adapters | Distinguishes a shared constraint from a one-team preference; platform guidance requires learning user needs ([CNCF](https://tag-app-delivery.cncf.io/whitepapers/platforms/)) | Product teams and internal platform product manager |
| **Contracts and compatibility tooling** | JSON Schema; OpenAPI | Encodes syntax and interface semantics, but schemas do not catch every specification violation ([OpenAPI](https://spec.openapis.org/oas/)) | Contract steward and every consumer |
| **Authoritative metadata** | Repository-owned Backstage entity descriptors; HR/IAM ownership records | Backstage ingests repository metadata and says owning teams maintain it through normal Git workflows ([Backstage catalogue](https://backstage.io/docs/features/software-catalog/)) | Domain owner for meaning; developer platform for ingestion |
| **Human and workload identity** | Organization identity provider, OAuth authorization server, workload credentials | Runtime actions need authenticated principals, audience-bound tokens, expiry, revocation, and delegation | Identity team plus resource owner |
| **Policy distribution and decision telemetry** | OPA bundles, status, discovery, decision logs | Allows common policies with distributed low-latency decisions; OPA does not provide the whole control plane automatically ([OPA](https://www.openpolicyagent.org/docs/management-introduction)) | Control function for policy; service team for enforcement |
| **Model supply** | Vendor model APIs or Kubernetes-hosted model servers and accelerators | Determines credentials, quotas, residency, capacity, routing, failure modes, and cost. Kubernetes' inference extension distinguishes gateways, schedulers, model servers, metrics, and accelerators ([Kubernetes Inference Extension](https://github.com/kubernetes-sigs/gateway-api-inference-extension)) | Vendor or model-serving team; gateway owner for mediation |
| **Tool and integration supply** | MCP hosts, clients, servers, downstream APIs | The protocol connects components but does not decide workflow authorization, sandboxing, or downstream invariants ([MCP architecture](https://modelcontextprotocol.io/docs/learn/architecture)) | Domain API/tool owner plus host/runtime owner |
| **Evaluation data and authority** | Representative cases, expected outcomes, safety suites, human review, risk tolerance | Generic infrastructure cannot define whether a domain result is acceptable; NIST calls for contextual knowledge and repeatable TEVV ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)) | Product/domain owner, affected stakeholders, control function |
| **Observability substrate** | OpenTelemetry traces, metrics, logs, baggage, Collector/exporter | Shared semantics can correlate a request across components; OpenTelemetry supports multiple signals and vendor-neutral exporters ([OpenTelemetry signals](https://opentelemetry.io/docs/concepts/signals/), [OpenTelemetry traces](https://opentelemetry.io/docs/concepts/signals/traces/)) | Existing observability platform; product team for domain signals |
| **Delivery and runtime infrastructure** | GitHub environments, Argo CD, Kubernetes control plane and worker nodes | Existing systems already supply approval, reconciliation, scheduling, secrets, and rollback-related controls; Kubernetes separates cluster state management from worker execution ([Kubernetes components](https://kubernetes.io/docs/concepts/overview/components/)) | Developer/cloud platform and workload team |
| **Capital and operating capacity** | Platform engineers, SRE/on-call, security review, cloud/model spend, vendor contract, migration budget | A runtime service creates availability and support obligations that a contract does not | Funding executive, platform product owner, FinOps/procurement |
| **Legal and regulatory permissions** | Data protection, sector obligations, records retention, provider terms, model licences | May require particular data paths, evidence, approvals, or locations; it does not by itself prove a central runtime is necessary | Legal/privacy/risk for requirements; engineering for implementation |
| **Exit mechanisms** | Portable descriptors, provider adapters, data export, dual-run plan, deprecation policy | Determines whether shared leverage preserves the freedom to replace a component | Capability owner and consuming teams |

## Internals where most coverage waves hands

### 1. Control plane and data plane are separate boundary decisions

A **control plane** stores desired state, policy, registrations, routing configuration, evaluation requirements, and deployment intent. A **data plane** handles live prompts, responses, tool calls, credentials, and effects. Kubernetes provides the familiar structural precedent: the API server, scheduler, controllers, and `etcd` manage cluster state while worker nodes execute workloads ([Kubernetes components](https://kubernetes.io/docs/concepts/overview/components/)). OPA provides a federation precedent: logically centralized policy management can distribute signed bundles to local policy engines that render decisions beside services ([OPA discovery](https://www.openpolicyagent.org/docs/management-discovery)).

This matters because “centralize governance” does not entail “send every model and tool call through one central process.” A contract-only design centralizes vocabulary but neither plane. A central-runtime design owns both configuration and traffic mediation. Federated control centralizes minimum policy and evidence while distributing decisions or enforcement. A vendor service may operate both planes but still leaves the customer accountable for configuration, application logic, and data ([AWS shared responsibility](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/shared-responsibility.html)).

Policy also has three distinct locations:

- **Design-time:** schema linting, approved providers, threat modelling, evaluation requirements.
- **Admission/deployment-time:** release evidence, environment approval, image/model provenance, configuration policy.
- **Runtime:** identity, rate limits, resource authorization, egress, content controls, human approval.

A policy belongs at the earliest boundary that can decide correctly, but a mandatory guarantee must ultimately be enforced where bypass cannot avoid it. Central policy with local enforcement needs version reporting, conflict rules, last-known-good behavior, and a declared fail-open or fail-closed mode. OPA's stack model makes one such conflict rule explicit: a global deny can override a bundle owner's allow ([OPA control-plane concepts](https://www.openpolicyagent.org/docs/ocp/concepts)).

### 2. A catalogue answers “what exists”; authorization answers “may this action happen?”

Backstage describes its software catalogue as a centralized view whose common source is YAML stored with and maintained by the owning codebase ([Backstage catalogue](https://backstage.io/docs/features/software-catalog/)). Its graph guidance says the catalogue is a caching mechanism, should not be the ultimate source of truth, and is not ideal for dynamic real-time relationships ([Backstage catalogue graph](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)). Therefore an agent catalogue can display an agent's owner, purpose, lifecycle, risk tier, models, tools, documentation, evaluation revision, and runtime links without becoming the authoritative store for live permissions, deployment health, or tool behavior.

The authorization path needs a trusted principal, target resource, action, delegated-user context, policy, and fresh domain state. Catalogue fields can help locate those inputs but should not silently become an allow decision. The same distinction applies to MCP: a server can advertise tools dynamically, yet the specification says annotations are only hints and must be considered untrusted unless their server is trusted ([MCP tool schema](https://modelcontextprotocol.io/specification/2025-11-25/schema)). Ownership is consequently split: the existing developer platform can own presentation and ingestion, the AI contract can define agent-specific metadata, and the resource-owning service must enforce live authorization.

### 3. A model gateway is a runtime product, not merely an API wrapper

Once all calls traverse a gateway, it owns an availability and latency dependency, provider credentials, request limits, routing semantics, retries, failure classification, usage attribution, telemetry, and often data-handling controls. Azure's reference implementation authenticates the caller, evaluates policies, chooses a backend with stored credentials, returns the response, and emits OpenTelemetry; its broader architecture adds token- and request-based quotas, content checks, regional routing, and retry behavior ([Azure AI Gateway](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview), [Azure gateway reference architecture](https://learn.microsoft.com/en-us/ai/playbook/solutions/genai-gateway/reference-architectures/apim-based)).

Self-hosted inference adds a different mechanism. The Kubernetes Gateway API Inference Extension separates the proxy, an endpoint picker/scheduler, body-based routing, model servers, and accelerator capacity; routing can depend on request cost, prefix-cache state, adapter availability, and service objectives ([Kubernetes Inference Extension](https://github.com/kubernetes-sigs/gateway-api-inference-extension)). That is materially more operational scope than a multi-provider HTTP adapter.

The boundary test is concrete: centralize only the duties whose consistent runtime mediation retires more duplicated work or unmanaged risk than the gateway's own on-call, migration, latency, blast radius, and abstraction cost create. Provider-specific features should remain reachable through explicit escape hatches or typed extensions if portability would otherwise mean losing capability.

### 4. MCP standardizes exchange, not integration ownership or safe execution

MCP defines hosts, per-server clients, servers, a JSON-RPC data layer, transports, lifecycle negotiation, and primitives for tools, resources, and prompts ([MCP architecture](https://modelcontextprotocol.io/docs/learn/architecture)). It explicitly says it focuses on context exchange and does not dictate how AI applications use models or manage supplied context. The protocol can therefore be part of an AI platform without making every MCP server or downstream integration a platform asset.

There are at least seven separable owners:

1. protocol and SDK evolution;
2. host/client runtime;
3. registry and admission metadata;
4. MCP server operation;
5. downstream API and business invariants;
6. delegated identity and user consent;
7. sandbox, egress, audit, and incident response.

The security boundary is especially easy to misplace. MCP warns about confused-deputy attacks, token passthrough, session hijacking, SSRF, and prompt injection, and requires per-client consent and audience-correct tokens in relevant flows ([MCP security best practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)). The tool schema itself cannot prove that a “read-only” hint is true. Network controls, resource-server authorization, sandboxing, scoped credentials, and human approval for consequential actions remain runtime duties, usually closest to the host or resource.

The practical split is: the platform can own a safe exposure and admission pattern; the domain team owns the integration's meaning and support; identity owns reusable credential mechanisms; security sets mandatory baselines; the host/runtime owns orchestration and approval UX. Central ownership of all tool code would discard domain knowledge and create an unbounded support queue.

### 5. Evaluation and observability require shared plumbing but local meaning

OpenTelemetry supplies reusable mechanics—traces, metrics, logs, baggage, context propagation, semantic conventions, SDKs, collectors, and exporters ([OpenTelemetry status](https://opentelemetry.io/docs/specs/status/)). It does not decide which workflow outcome was correct. Likewise, an evaluation platform can schedule runs, version datasets, store evidence, compare revisions, and supply baseline adversarial tests, but cannot choose a loan decision's tolerance, a medical workflow's escalation rule, or a code agent's acceptable destructive behavior without domain owners.

Generative systems also need lineage beyond a gateway's token count: application revision, model/provider revision, prompts, retrieved context, tool inputs and outputs, evaluator revision, policy decision, approval, cost, latency, and final business outcome. Google Cloud's operations guidance requires end-to-end chain evaluation and logs of inputs, outputs, intermediate states, and chain configuration, with continuous evaluation after deployment ([Google Cloud architecture](https://docs.cloud.google.com/architecture/deploy-operate-generative-ai-applications)).

Correlation has privacy and trust costs. OpenTelemetry warns that baggage is automatically propagated in network requests, may reach unintended third parties, and has no built-in integrity check ([OpenTelemetry baggage](https://opentelemetry.io/docs/concepts/signals/baggage/)). Thus the existing observability platform should own collection and retention mechanisms, while product and privacy owners decide which prompt, response, user, and domain fields may be captured. “Uniform telemetry” without data minimization can centralize sensitive content as efficiently as it centralizes debugging.

### 6. Deployment and integration ownership follow the changed primitive

Model aliases, prompts, tools, agent graphs, evaluation sets, and policy bundles are deployable artefacts, but that does not imply a second CI/CD platform. Existing delivery systems already implement environments, approval, protected branches, external readiness gates, secrets release, reconciliation, retry, and controlled deletion ([GitHub environments](https://docs.github.com/en/actions/reference/workflows-and-actions/deployments-and-environments), [Argo CD sync options](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-options/)). The AI layer should extend those contracts with AI-specific evidence and rollout semantics rather than duplicate the machinery.

Integration ownership should similarly follow change authority and incident knowledge:

- The platform owns a reusable adapter only when multiple teams need substantially the same semantics and the platform can support its downstream failure modes.
- A domain team owns a tool or connector when it changes with domain rules, carries business side effects, or requires workflow-specific incident judgment.
- The platform can still define exposure, authentication, telemetry, timeout, retry, and conformance requirements.
- Vendor-operated connectors do not remove the need for a named internal owner, because the customer still configures access and carries the product outcome under shared-responsibility models ([AWS Bedrock security](https://docs.aws.amazon.com/bedrock/latest/userguide/security.html)).

This gives a clean answer to “where should deployment and integrations live?”: generic mechanisms stay in the existing developer platform; AI-specific contracts and evidence plug into them; domain semantics stay with the team able to change and diagnose the workflow.

## Failure modes

1. **Configuration or deployment drift activates a path no one intended.** A partial rollout, stale instance, incompatible schema consumer, or hidden bypass makes declared state diverge from execution. On 2012-08-01, Knight Capital's router sent more than 4 million orders while trying to fill 212 customer orders; the SEC found that new code had not been deployed to one of eight servers, old functionality was reactivated, and the firm lost more than $460 million ([SEC order](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf)). **Boundary lesson:** the team owning deployment must also own observed version evidence, staged rollout, rollback, and alerts; catalogue state is insufficient.

2. **A centrally distributed control creates a global blast radius.** A fast control plane propagates one bad policy everywhere before local owners can react. On 2019-07-02, a Cloudflare WAF rule caused CPU exhaustion across the worldwide HTTP/HTTPS path; the rule passed the available tests but lacked resource-consumption testing and was deployed globally without staging ([Cloudflare postmortem](https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/)). **Boundary lesson:** global policies need canaries, resource limits, emergency isolation, and an independently reachable rollback path.

3. **The shared runtime becomes a common-mode dependency, including for recovery.** On 2017-02-28, an incorrect operational-command input removed more Amazon S3 servers than intended in `us-east-1`, affecting the index and placement subsystems and dependent AWS services; even the Service Health Dashboard's administration console depended on S3 ([AWS S3 incident](https://aws.amazon.com/message/41926/)). **Boundary lesson:** gateways, catalogues, identity, policy, and status systems need cells, degraded modes, and recovery paths that do not depend on the failed data plane.

4. **The source of truth or recovery story is weaker than the interface suggests.** On 2017-01-31, an accidental deletion on GitLab.com's primary database caused hours of unavailability and unrecoverable production-data loss; GitLab estimated effects on roughly 5,000 projects, 5,000 comments, and 700 new accounts ([GitLab postmortem](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)). **Boundary lesson:** a central catalogue, evaluation store, or policy repository creates no leverage if backup restoration, ownership history, and data reconciliation are untested.

5. **Delegated identity crosses integration boundaries with excessive reach.** On 2022-04-12, GitHub began investigating attackers' use of stolen OAuth user tokens belonging to Heroku and Travis CI integrations to download private repository data from dozens of organizations and search it for secrets ([GitHub security alert](https://github.blog/news-insights/company-news/security-alert-stolen-oauth-user-tokens/)). **Boundary lesson:** an integration registry must not substitute for audience restriction, least privilege, token lifecycle, per-client consent, and resource-side authorization.

6. **A shared integration becomes a software-supply-chain multiplier.** On 2021-04-01, Codecov was alerted that an attacker had modified its Bash Uploader in Google Cloud Storage; the malicious uploader reached users through the uploader, GitHub Action, CircleCI Orb, and Bitrise Step and extracted environment variables and repository URLs ([Codecov postmortem](https://about.codecov.io/apr-2021-post-mortem/)). **Boundary lesson:** centrally blessed tools need signed artefacts, immutable versions, provenance, isolation, rapid revocation, and explicit customer impact analysis.

7. **Generic testing passes while end-to-end safety ownership falls between teams.** The NTSB found that the Uber ATG automated-driving system involved in the fatal 2018-03-18 Tempe crash detected the pedestrian 5.6 seconds before impact but did not correctly classify or predict her path; the system design precluded emergency braking, and the investigation cited inadequate safety risk assessment and ineffective operator oversight ([NTSB investigation](https://www.ntsb.gov/investigations/Pages/HWY18MH010.aspx)). **Boundary lesson:** platform test harnesses cannot own the release judgment for a domain workflow; domain, human-factors, operational, and control owners must jointly define and accept end-to-end risk.

8. **The model works in isolation but the operating system around it hits economic or physical limits.** Zillow's annual report for the fiscal year ending 2023-12-31 says Zillow Offers was wound down after home-pricing unpredictability, capacity constraints, and operational challenges; the company had previously paused new contracts because renovation and closing work had backlogged ([Zillow annual report](https://investors.zillowgroup.com/files/doc_financials/2023/ar/zillow-group-inc-_annual_report_2023.pdf), [Zillow operational update](https://investors.zillowgroup.com/investors/news-and-events/news/news-details/2021/At-Operational-Capacity-Zillow-Offers-to-Focus-on-Signed-Customer-Contracts-and-Current-Inventory-Suspends-Signing-of-New-Contracts-Through-2021/default.aspx)). **Boundary lesson:** evaluation, quotas, and deployment gates must include downstream labor, inventory, support, and business capacity—not only model accuracy and API health.

9. **Policy exists only as metadata and produces false assurance.** JSON Schema annotations provide context but do not enforce validation, and MCP tool annotations are untrusted hints unless the server is trusted ([JSON Schema](https://json-schema.org/understanding-json-schema/reference/metadata), [MCP tools](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)). A real failure may remain invisible because the dashboard says an agent is “read-only” or “approved” while the execution path has broader credentials. **Historical analogue:** the Codecov uploader was a familiar approved integration surface, yet malicious code executed inside customer CI environments and read their environment variables ([Codecov](https://about.codecov.io/apr-2021-post-mortem/)). **Boundary lesson:** attach proofs and observed runtime evidence to claims; never turn descriptive fields directly into authorization.

## Constraints and ceilings

- **Correctness is contextual and partly irreducible.** A shared platform can standardize evaluation mechanics, but acceptable outcomes, edge cases, and human escalation depend on the workflow. NIST explicitly requires mapping the tasks and context, documenting generalization limits, and monitoring after deployment ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)).

- **Central capacity is typically smaller than aggregate product-team capacity.** In organizations with many product teams, the shared platform team usually has less engineering capacity than those teams combined. Fowler therefore warns that a design requiring the central team to implement every migration or integration cannot scale ([Fowler](https://martinfowler.com/articles/platform-teams-stuff-done.html)). Where that asymmetry exists, federation and internal contribution are operating necessities rather than merely cultural preferences.

- **Runtime mediation consumes latency and reliability budget.** Every synchronous gateway, authorization check, guardrail, evaluator, and telemetry exporter adds work or another dependency. Distributed decision engines can reduce network latency and preserve availability, which is why OPA recommends colocating engines with services while managing them centrally ([OPA](https://www.openpolicyagent.org/docs/management-introduction)).

- **Physical and provider capacity remain hard limits.** Hosted APIs expose request/token quotas and regions; self-hosted inference is bounded by accelerators, memory, cache locality, scheduling, and queueing. The Kubernetes inference architecture requires scheduler knowledge of request cost, endpoint capability, prefix cache, and adapters precisely because ordinary round-robin routing is not enough ([Kubernetes Inference Extension](https://github.com/kubernetes-sigs/gateway-api-inference-extension)).

- **A common contract cannot erase semantic diversity.** OpenAPI and JSON Schema describe interfaces and validation, not every business invariant; OpenAPI itself warns that its schemas do not catch every specification violation ([OpenAPI](https://spec.openapis.org/oas/)). Provider features, model behavior, tool side effects, and jurisdiction-specific constraints will continue to require extensions or escape routes.

- **Security cannot be delegated to model behavior.** MCP's own security material calls for conventional audience validation, consent, input validation, access controls, rate limits, output sanitization, timeouts, and auditing; tool descriptions and annotations are not enforcement ([MCP security](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices), [MCP tools](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)).

- **Observability competes with privacy, cost, and signal quality.** Full prompt, response, tool, and identity capture can improve diagnosis while creating a sensitive centralized dataset. OpenTelemetry baggage can unintentionally propagate to third parties and lacks integrity checks ([OpenTelemetry baggage](https://opentelemetry.io/docs/concepts/signals/baggage/)). Sampling, redaction, retention, and access design are part of the platform boundary.

- **Managed services move operation, not all responsibility.** Vendor services reduce infrastructure work but impose APIs, quotas, regions, supported models, commercial terms, and exit costs. AWS's shared-responsibility model makes the division explicit: provider and customer responsibilities vary by the chosen service, and customers retain application, data, IAM, and configuration duties ([AWS shared responsibility](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/shared-responsibility.html)).

- **Jurisdiction and control functions can force enforcement without dictating architecture.** A legal requirement can mandate retention, access control, approval, or residency; it does not automatically select a single central runtime. A federated design can distribute enforcement while reporting common evidence, but it must make policy versions and exceptions observable.

- **The boundary must be affordable to remove.** If consumers cannot bypass, dual-run, export, or replace the service, internal centralization produces vendor lock-in. The “thinnest viable platform” guidance recommends planning for realistic platform lifetimes and architectural seams for replacement ([Fowler](https://martinfowler.com/articles/platform-prerequisites.html)).

## Side effects

- **Authority moves toward whoever controls admission, credentials, and the data path.** A catalogue team controls discoverability; a gateway team controls availability and provider choice; a policy team controls permissible actions. These are materially different powers even if all are called “platform.”

- **The organization gains a new internal product and support surface.** Runtime ownership creates SLOs, incident response, capacity planning, migrations, documentation, user research, and exception queues. CNCF treats platform teams as product teams precisely because the platform must continuously learn and serve internal users ([CNCF](https://tag-app-delivery.cncf.io/whitepapers/platforms/)).

- **Centralization can reduce duplicated adapters while concentrating failure and security impact.** The AWS S3 and Cloudflare incidents show how broadly reused central paths can turn one operational or policy error into a multi-service event ([AWS](https://aws.amazon.com/message/41926/), [Cloudflare](https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/)).

- **Contracts create an ecosystem of consumers that makes schema evolution political.** Catalogue plugins, CI checks, gateways, evaluation stores, audit reports, and product repositories may all depend on fields that began as “just metadata.” Compatibility and deprecation work then become part of the platform's cost.

- **Federation preserves local operation but creates reconciliation work.** Policy conflict, version skew, evidence aggregation, exception expiry, and responsibility during cross-boundary incidents become recurring coordination duties. OPA's explicit conflict composition is evidence that federation needs defined precedence, not merely distributed agents ([OPA concepts](https://www.openpolicyagent.org/docs/ocp/concepts)).

- **Uniform telemetry can become both institutional memory and a surveillance or data-loss risk.** Correlated traces make debugging and evaluation reusable, but identity and content propagation can expose sensitive information outside the intended boundary ([OpenTelemetry baggage](https://opentelemetry.io/docs/concepts/signals/baggage/)).

- **Teams may lose skill and agency if the abstraction hides the system too completely.** Voluntary adoption, inspectable underlying systems, provider escape hatches, and a supported exception path keep the paved road from becoming a cage. Fowler argues voluntary adoption also pressures the platform to stay loosely coupled and replaceable ([Fowler](https://martinfowler.com/articles/platform-prerequisites.html)).

- **Vendor-specific internal contracts can multiply switching work across consuming teams.** The UK Competition and Markets Authority found technical and commercial barriers that make cloud switching and multi-cloud use harder ([CMA cloud-services market investigation](https://www.gov.uk/cma-cases/cloud-services-market-investigation)). The EU Data Act removes covered switching charges, including egress, from 2027-01-12, but does not remove schema conversion, re-evaluation, dual running, or support migration ([European Commission Data Act explanation](https://digital-strategy.ec.europa.eu/en/factpages/data-act-explained)). A nominally multi-model gateway can therefore remain costly to leave when identity, guardrail, evaluation, telemetry, or tool-registration conventions mirror one provider. Test portability with a real second implementation and measure the switching work rather than inferring it from an API-compatible HTTP shape.

## Plain-language analogy

Think of the organization as a region with a road authority. The authority should define shared signs, vehicle rules, maps, identity for licensed operators, and safety inspections; it may also build heavily reused roads and operate dangerous junctions. It should not own every vehicle, choose every destination, or employ every driver. Product teams are the transport operators who understand their passengers and routes; control functions set non-negotiable safety floors; vendors may run toll roads; the existing developer platform is the wider road network and map service. A contracts-only model publishes the road rules, a central runtime is a toll plaza through which every vehicle passes, federated control gives local roads their own enforcement under regional law, and a vendor service outsources a road while retaining the operator's duty to use it safely. The analogy breaks because AI requests are not passive vehicles: model outputs are probabilistic, tools can acquire delegated authority mid-journey, descriptions may be untrustworthy, and evaluating a journey can require examining the whole changing workflow rather than checking a vehicle once.

## Source receipts

### Primary

- [CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/)
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)
- [Model Context Protocol architecture](https://modelcontextprotocol.io/docs/learn/architecture)
- [Model Context Protocol authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)
- [Model Context Protocol tools specification](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)
- [Model Context Protocol security best practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)
- [OpenAPI Specification](https://spec.openapis.org/oas/)
- [JSON Schema annotations and metadata](https://json-schema.org/understanding-json-schema/reference/metadata)
- [NTSB investigation: Uber ATG automated-driving crash](https://www.ntsb.gov/investigations/Pages/HWY18MH010.aspx)

### Technical Docs

- [Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)
- [Backstage: Creating the Catalog Graph](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)
- [Open Policy Agent management architecture](https://www.openpolicyagent.org/docs/management-introduction)
- [Open Policy Agent discovery](https://www.openpolicyagent.org/docs/management-discovery)
- [Open Policy Agent control-plane concepts](https://www.openpolicyagent.org/docs/ocp/concepts)
- [OpenTelemetry signals](https://opentelemetry.io/docs/concepts/signals/)
- [OpenTelemetry traces](https://opentelemetry.io/docs/concepts/signals/traces/)
- [OpenTelemetry baggage](https://opentelemetry.io/docs/concepts/signals/baggage/)
- [Kubernetes components](https://kubernetes.io/docs/concepts/overview/components/)
- [Kubernetes Gateway API Inference Extension](https://github.com/kubernetes-sigs/gateway-api-inference-extension)
- [GitHub deployment environments](https://docs.github.com/en/actions/reference/workflows-and-actions/deployments-and-environments)
- [Argo CD automated sync](https://argo-cd.readthedocs.io/en/latest/user-guide/auto_sync/)
- [Argo CD sync options](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-options/)
- [Azure AI Gateway overview](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)
- [Azure GenAI gateway reference architecture](https://learn.microsoft.com/en-us/ai/playbook/solutions/genai-gateway/reference-architectures/apim-based)
- [Google Cloud: deploy and operate generative AI applications](https://docs.cloud.google.com/architecture/deploy-operate-generative-ai-applications)
- [AWS Bedrock security, guardrails, and observability](https://docs.aws.amazon.com/bedrock/latest/userguide/security.html)
- [AWS shared-responsibility model](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/shared-responsibility.html)

### Filings

- [SEC administrative order: Knight Capital Americas LLC](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf)
- [Zillow Group annual report for the fiscal year ending 2023-12-31](https://investors.zillowgroup.com/files/doc_financials/2023/ar/zillow-group-inc-_annual_report_2023.pdf)

### News

- [Amazon S3 service disruption in `us-east-1`](https://aws.amazon.com/message/41926/)
- [Cloudflare outage on 2019-07-02](https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/)
- [GitLab database outage postmortem](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)
- [GitHub stolen third-party OAuth token alert](https://github.blog/news-insights/company-news/security-alert-stolen-oauth-user-tokens/)
- [Codecov Bash Uploader postmortem](https://about.codecov.io/apr-2021-post-mortem/)
- [Zillow Offers operational-capacity update](https://investors.zillowgroup.com/investors/news-and-events/news/news-details/2021/At-Operational-Capacity-Zillow-Offers-to-Focus-on-Signed-Customer-Contracts-and-Current-Inventory-Suspends-Signing-of-New-Contracts-Through-2021/default.aspx)

### Practitioner Commentary

- [Mind the platform execution gap](https://martinfowler.com/articles/platform-prerequisites.html)
- [How platform teams get stuff done](https://martinfowler.com/articles/platform-teams-stuff-done.html)

### Snowball audit

Round one named and checked the load-bearing projects and institutions surfaced by the source and interpretation: MCP, Backstage, Open Policy Agent, OpenTelemetry, Kubernetes, CNCF, NIST, AWS, Microsoft Azure, Google Cloud, GitHub, and Argo CD. Round two followed the concrete failure and responsibility examples they exposed: Knight Capital and the SEC, Cloudflare, Amazon S3, GitLab, Heroku, Travis CI, Codecov, Uber ATG and the NTSB, and Zillow. No unresolved parent company, regulator, protocol owner, or runtime component remained load-bearing after the second pass.
