# Futures and second-order effects: Where Should the Platform End?

Research cut-off: 2026-07-30.

The strongest forward-looking conclusion is not that the AI platform should be
central or local. It is that its boundary should be drawn between **portable
cross-cutting evidence and control** and **workflow-specific judgment and
execution**. The protocols are becoming more interoperable, but that does not
make the systems built around them portable. Identity state, authorization
policy, evaluation datasets, trace content, catalogue semantics, runtime state,
and exception processes remain the places where dependency accumulates.

## Forward calendar

Skipped per research plan: this is an evergreen boundary question with no
triggering event, named organization, contract window, launch, or fixed decision
date.

## Second-order effects map

### 1. Open protocols commoditize connections, so vendors compete to own the control plane

**First-order effect:** MCP standardizes access to tools and context, while A2A
standardizes agent discovery and coordination. MCP's 2026-07-28 specification
made the core stateless, added per-request capability negotiation, and put
specialized behavior into opt-in extensions. A2A 1.0 includes Agent Cards,
multiple security schemes, task lifecycle operations, and signed-card support.
Those are meaningful interoperability gains, not merely marketing vocabulary.
([MCP specification, 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28);
[MCP changelog, 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28/changelog);
[A2A specification](https://a2a-protocol.org/latest/specification/))

**Second-order effects:**

1. The connection layer becomes less differentiating. Vendor competition moves
   upward into identity, policy, memory, evaluation, registry, semantic tool
   search, managed runtime, and evidence retention. That bundling is already
   visible: AWS describes AgentCore as Gateway, Identity, Runtime, Memory,
   Evaluations, Policy, and Observability; Microsoft Foundry combines runtime,
   per-agent Entra identity, MCP/A2A endpoints, tools, tracing, and publishing;
   Google presents Gemini Enterprise Agent Platform as an end-to-end environment
   for building, orchestrating, and governing agents.
   ([AWS AgentCore overview](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/);
   [Microsoft Foundry Agent Service](https://learn.microsoft.com/en-gb/azure/ai-foundry/agents/overview?context=%2Fazure%2Fai-studio%2Fcontext%2Fcontext&view=foundry-classic);
   [Google Gemini Enterprise Agent Platform, 2026-04-22](https://cloud.google.com/blog/products/ai-machine-learning/the-new-gemini-enterprise-one-platform-for-agent-development))
2. Nominal protocol portability can coexist with operational lock-in. A team may
   move an MCP server yet still be unable to move its credentials, policy model,
   evaluation history, trace semantics, memory, or approval workflow. The
   protocol boundary is therefore a socket, not an exit plan. MCP itself states
   that it cannot enforce consent, authorization, privacy, or tool safety at the
   protocol level.
   ([MCP security guidance](https://modelcontextprotocol.io/specification/2026-07-28))
3. Open standards may reduce point-to-point integration work while increasing
   demand for gateways and registries. MCP's own 2026 roadmap lists audit trails,
   SSO-integrated authorization, gateway behavior, and configuration portability
   as production problems, and the Linux Foundation reports broad cloud support
   for A2A. The likely market is not “open protocol instead of platform,” but
   “open protocol inside several competing platforms.”
   ([MCP 2026 roadmap, 2026-03-09](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/);
   [Linux Foundation A2A update, 2026-04-09](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year))

**Boundary implication:** centrally own the protocol profile, conformance tests,
identity integration, minimum audit envelope, and portability test. Do not infer
from that ownership that the same team should own tool semantics, workflow
orchestration, memory, or domain evaluation.

### 2. A shared gateway reduces duplicated security work, then attracts workflow logic

**First-order effect:** a gateway is a natural place for ingress and egress
authentication, credential exchange, rate limiting, routing, tool admission,
telemetry propagation, and emergency revocation. AWS explicitly markets its
gateway as a single trusted entry point for credential management, secure
connectivity, observability, and delegated OAuth.
([AWS AgentCore Gateway, 2026-06-01](https://aws.amazon.com/blogs/machine-learning/extending-mcp-support-for-amazon-bedrock-agentcore-gateway-2/))

**Second-order effects:**

1. Because every request passes through it, the gateway attracts retries,
   provider-specific fallbacks, tool filtering, budgets, policy decisions, and
   eventually workflow state. It then ceases to be replaceable plumbing and
   becomes an orchestration product with a larger failure domain.
2. A central enforcement point makes audit and revocation easier, but also
   enlarges the blast radius of a defect, outage, or mistaken policy. Teams with
   exceptional needs either wait for a central exception or build shadow paths.
3. The platform team's role shifts from enabling team to policy intermediary.
   This concentrates decision rights even when the technical API remains open.
   DORA warns that rigid “ivory tower” platforms produce workarounds and that
   internal platforms can reduce throughput and change stability when poorly
   implemented; it recommends extensibility, clear feedback, task-success
   measures, and developer independence.
   ([DORA platform engineering, updated 2026-01-12](https://dora.dev/capabilities/platform-engineering/);
   [2024 DORA report](https://dora.dev/research/2024/dora-report/))

**What ordinary engineers are saying:** the small, self-selected practitioner
sample is divided on implementation but unusually consistent on the boundary.
One engineer operating roughly two million requests per month across 150–200
teams said they would centralize access to internal and sensitive MCP servers,
but leave generic local tools outside the proxy. Another thread distinguishes
tool servers from the long-lived work of token refresh, rate limits, audit, and
policy. A third reports building a custom gateway because integrated suites were
too inflexible, while another discussion describes the debugging cost after
routing and policy moved into the gateway. These are anecdotes, and several
participants disclose vendor interests, but they illuminate the practical
trade-off better than adoption counts do.
([gateway-boundary discussion](https://www.reddit.com/r/mcp/comments/1uhelfu/where_do_you_draw_the_line_with_litellms_mcp/);
[build-versus-buy discussion](https://www.reddit.com/r/mcp/comments/1uokcud/build_vs_buy_on_mcp_gatewaytool_servers/);
[custom gateway discussion](https://www.reddit.com/r/mcp/comments/1rhavm1/anyone_else_building_a_centralized_mcp_gateway_to/))

**Boundary implication:** make the gateway mandatory only for controls that must
be universal. Keep workflow state, domain routing, retry meaning, and product
fallback behavior on the workflow side. Treat every new gateway feature as a
change in organizational authority, not just an implementation convenience.

### 3. Per-agent identity creates a new lifecycle, not merely a new credential

**First-order effect:** cloud platforms are introducing identities for individual
agents. Microsoft gives each hosted agent a dedicated Entra identity; Google
offers per-agent IAM identity in preview; A2A supports signed Agent Cards and
several authentication schemes.
([Microsoft hosted agents](https://learn.microsoft.com/en-us/azure/foundry/agents/concepts/hosted-agents);
[Google Agent Engine identity](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/set-up);
[A2A specification](https://a2a-protocol.org/latest/specification/))

**Second-order effects:**

1. Least privilege becomes more feasible, but lifecycle work multiplies:
   issuance, ownership, delegation, rotation, revocation, dormant-agent cleanup,
   and reconciliation with the human or service on whose behalf the agent acts.
2. Identity metadata becomes part of the product's behavior. The answer to “who
   acted?” may require a chain connecting a human, an agent version, a runtime,
   delegated authority, a tool, and an approval. NIST's current concept paper
   treats identification, authorization, auditing, non-repudiation,
   human-agent binding, and prompt-injection mitigation as open design problems,
   not solved infrastructure.
   ([NIST/NCCoE agent identity concept paper, 2026-02-05](https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents))
3. A single central identity service can improve revocation and audit while
   making provider-specific identity objects the deepest source of lock-in.
   Signed Agent Cards prove integrity of a description; they do not by themselves
   prove that the described agent is authorized for a particular business action.

**Boundary implication:** the existing enterprise identity team should own trust
anchors and lifecycle rules; the platform should integrate them and expose a
standard delegation envelope; workflow owners should define the authority
needed for each business action and remain accountable for it.

### 4. Standard telemetry and evaluation make evidence portable—while making privacy and interpretation harder

**First-order effect:** MCP now documents W3C trace-context propagation.
OpenTelemetry's GenAI conventions cover models, token use, agents, workflows,
tool execution, and evaluation events. NIST is developing benchmark practices
and in-workflow evaluation probes that produce machine-readable audit trails.
([MCP changelog](https://modelcontextprotocol.io/specification/2026-07-28/changelog);
[OpenTelemetry GenAI observability, 2026-05-14](https://opentelemetry.io/blog/2026/genai-observability/);
[NIST AI 800-2 draft announcement, 2026-01-30](https://www.nist.gov/news-events/news/2026/01/towards-best-practices-automated-benchmark-evaluations);
[NIST evaluation probes, updated 2026-05-05](https://www.nist.gov/programs-projects/building-evaluation-probes-agentic-ai))

**Second-order effects:**

1. A common trace envelope can make runtime and model comparison cheaper, so
   platform teams can centralize evidence without centralizing execution.
2. Full prompts, tool arguments, results, and model responses are also sensitive
   payloads. OpenTelemetry disables content capture by default in its example and
   warns about size and sensitivity. More observability can therefore create more
   privacy, retention, access-control, and data-residency work.
3. Shared evaluators can eliminate duplicated harnesses, but a universal score can
   erase domain meaning. NIST describes evaluation practice as still emerging and
   distinguishes objectives, benchmark selection, execution, analysis, and
   reporting. The platform can own the harness and evidence schema; the workflow
   owner still needs to own what “good,” “safe,” and “complete” mean.
4. Once evaluation gates deployment, evaluator changes become production changes.
   They need versioning, reproducibility, appeal paths, and observed post-release
   checks—not just a centrally published benchmark.

**Boundary implication:** centralize trace propagation, redaction, evidence
retention, evaluator interfaces, and reproducibility. Federate datasets,
rubrics, risk acceptance, and outcome interpretation to domain owners.

### 5. Regulation and sovereignty pull routing and evidence inward, but not necessarily into a new AI platform

**First-order effect:** EU governance is moving from principles toward
enforcement and operational evidence. The AI Act is broadly applicable from
2026-08-02; Commission enforcement of general-purpose-model obligations begins
then, while the 2026 AI Omnibus moved high-risk-system deadlines to 2027-12-02
and product-embedded systems to 2028-08-02. The EDPB says whether an AI model is
anonymous must be assessed case by case and addresses lawful bases for
development and deployment.
([EU AI Act, Article 113](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689);
[AI Omnibus, 2026-07-27](https://digital-strategy.ec.europa.eu/en/news/ai-omnibus-enters-force);
[GPAI provider guidance](https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers);
[EDPB Opinion 28/2024, 2024-12-18](https://www.edpb.europa.eu/news/edpb-opinion-on-ai-models-gdpr-principles-support-responsible-ai_en))

**Second-order effects:**

1. Organizations will need model/version inventories, region-aware routing,
   provenance, retention, and evidence export across a chain of providers and
   deployers. Those requirements favor shared capabilities.
2. The same requirements can fragment deployments by jurisdiction and risk tier.
   A universal global runtime becomes less attractive than a portable control
   contract implemented by regional or sector-specific runtimes.
3. Sovereignty shifts from “where does compute run?” to “can we access, choose,
   control, audit, and replace the model and its surrounding evidence system?”
   The EU AI Office's 2026 expert work explicitly frames sovereignty around
   access, choice, control, and benefit.
   ([EU AI Office frontier-AI findings, 2026-07-15](https://digital-strategy.ec.europa.eu/en/library/ai-office-publishes-frontier-ai-expert-findings-eu-competitiveness-sovereignty-and-security))
4. Compliance pressure can accidentally justify an all-encompassing platform even
   where existing identity, data-governance, records-management, security, and
   observability systems already own the relevant controls.

**Boundary implication:** map obligations to existing accountable systems first.
The AI platform should compose and evidence those controls, not silently become
the new system of record for identity, privacy, records, or legal interpretation.

### 6. Agents turn the existing developer platform into reusable context, then move the bottleneck to human decisions

**First-order effect:** an existing service catalogue and paved roads can serve
both people and agents. Spotify exposes Backstage capabilities through MCP and
CLI tools, while keeping fleet orchestration and its coding-agent harness as
distinct systems.
([Spotify Engineering, 2026-06-03](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint))

**Second-order effects:**

1. Existing ownership, documentation, standards, and component metadata gain a
   second consumer without requiring a separate agent catalogue. This is
   leverage if metadata remains authoritative and reusable.
2. Agent performance becomes coupled to platform consistency and metadata
   quality. Stale ownership or ambiguous golden paths can now mislead automated
   actors at machine speed.
3. Faster code production moves constraint and cost downstream. Spotify reports
   higher pull-request frequency and then identifies review and human
   decision-making as the new bottleneck. A platform measured only on agent
   invocations or generated changes can therefore look successful while total
   work increases.
4. Standardization improves agent performance but can reduce legitimate
   diversity. The platform must distinguish “common enough to teach and
   automate” from “mandatory because the platform cannot model alternatives.”

**Boundary implication:** prefer agent-specific metadata in the existing
developer platform when the underlying facts already live there. Create a
separate agent catalogue only for genuinely agent-specific lifecycle,
authority, or evidence that has no authoritative home elsewhere.

### Synthesis: the likely durable split

| Shared spine | Federated/domain-owned edge |
|---|---|
| Protocol profiles and conformance | Tool meaning and business semantics |
| Enterprise identity integration and revocation | Requested authority and risk acceptance |
| Credential brokerage and minimum mandatory policy | Workflow orchestration and fallback meaning |
| Trace propagation, redaction, retention, and export | Domain evaluation datasets and rubrics |
| Catalogue schema, ownership links, and discovery | Implementation, deployment choice, and local support |
| Portability tests and exit evidence | Product outcomes and incident accountability |

This is a hypothesis to test, not a universal blueprint. High-impact,
irreversible workflows may justify a thicker mandatory boundary; low-risk,
read-only experiments may justify almost none.

## Four scenarios

The scenarios are mutually exclusive descriptions of the dominant pattern by
2027-07-30. Percentages are subjective estimates, sum to 100%, and are included
to expose the assumptions rather than simulate precision.

### Base — The thin federated spine wins

**Headline:** Most organizations extend their existing developer, identity,
security, and observability platforms with a small agent-specific contract and
gateway profile. Product teams own tools, workflows, deployment, and domain
evaluation; the shared layer owns discovery, identity integration, minimum
policy, trace propagation, and portability tests.

**Falsifiable triggers:**

- By 2027-07-30, at least two of AWS, Microsoft, and Google support current MCP,
  A2A, and OpenTelemetry interchange while continuing to differentiate on
  managed identity, policy, memory, evaluation, and runtime.
- Published enterprise cases more often describe an existing service catalogue
  plus agent metadata than a separate authoritative agent catalogue.
- Platform scorecards include task success, exception time, and switching cost,
  not only adoption or request volume.

**Leading indicators over the next 6–12 months:** MCP client/server conformance
coverage; A2A signed-card use; OpenTelemetry evaluation-event support; evidence
export formats; Backstage/service-catalogue integrations; documented escape
paths; and teams completing cross-runtime portability drills.

**Probability:** **Likely — 50%.** Standards are converging at the connection and
telemetry layers, while DORA and practitioner evidence favor extensible paved
roads over comprehensive mandates. The uncertainty is whether vendor bundles
make the thin boundary economically or operationally unattractive.

**Downstream consequences:** platform teams become stewards of contracts and
cross-cutting controls rather than owners of every runtime. Domain teams retain
judgment but must supply metadata, evidence, and on-call ownership. Vendors still
sell integrated suites, but protocol and evidence portability constrain some
switching costs.

**Evidence base:** [MCP 2026 roadmap](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/),
[A2A 1.0 adoption](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year),
[DORA platform guidance](https://dora.dev/capabilities/platform-engineering/),
and [Spotify's reuse of Backstage](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint).

### Upside — Open evidence makes exit routine

**Headline:** Protocol conformance expands into portable identity assertions,
policy inputs, evaluation records, and trace bundles. Switching a workflow
between model providers or runtimes becomes an ordinary tested operation rather
than a migration project.

**Falsifiable triggers:**

- By 2027-07-30, three major cloud or agent platforms can import and export the
  same agent identity metadata, trace context, and evaluation-result envelope
  without proprietary translation in domain code.
- At least two public enterprise case studies demonstrate moving a production
  workflow across runtimes while preserving authorization scope and audit
  continuity.
- Procurement begins requiring executable portability and evidence tests rather
  than check-box support for MCP or A2A.

**Leading indicators over the next 6–12 months:** stable GenAI semantic
conventions; MCP conformance scenarios; cross-vendor A2A interoperability tests;
signed provenance; provider-neutral evaluation records; contract tests in CI;
and procurement language requiring export and deletion guarantees.

**Probability:** **Plausible but not probable — 20%.** The technical ingredients
exist, including MCP trace propagation, A2A signed cards, and OpenTelemetry
evaluation events, but identity authority and policy semantics remain immature.
NIST still describes identity and evaluation practices as active research and
draft guidance.

**Downstream consequences:** the platform can remain thin because assurance
travels with the workflow. Smaller vendors and internal teams gain bargaining
power. Migration work falls, but conformance, signing, schema governance, and
evidence verification become important shared disciplines.

**Evidence base:** [MCP changelog](https://modelcontextprotocol.io/specification/2026-07-28/changelog),
[A2A specification](https://a2a-protocol.org/latest/specification/),
[OpenTelemetry GenAI conventions](https://opentelemetry.io/blog/2026/genai-observability/),
and [NIST's AI Agent Standards Initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure).

### Downside — The gateway becomes the platform, then the bottleneck

**Headline:** Security and compliance urgency turns the shared gateway into the
mandatory home for routing, tools, policy, memory, evaluation, workflow state,
and deployment. Integrated cloud suites make this convenient initially; later,
provider semantics, exception queues, and common-mode failure dominate.

**Falsifiable triggers:**

- By 2027-07-30, most new vendor features require proprietary gateway, identity,
  memory, or evaluation resources even when MCP or A2A is exposed at the edge.
- Internal platform teams cannot migrate one representative workflow or grant a
  non-standard exception within an agreed service level without vendor or
  central-team intervention.
- Adoption rises while developer task success, throughput, change stability, or
  satisfaction falls, and shadow gateways or local bypasses increase.

**Leading indicators over the next 6–12 months:** proprietary extensions;
gateway-held workflow state; non-exportable evaluation history; rising exception
lead time; platform on-call growth; local API keys and side gateways; forced
catalogue dependencies; and outages affecting otherwise independent workflows.

**Probability:** **Plausible — 25%.** All three major clouds already bundle most
agent lifecycle capabilities, and central gateways naturally attract more
logic. DORA's platform warnings and current practitioner discussions show the
organizational failure mode, but they do not establish its prevalence.

**Downstream consequences:** audit coverage may improve at first, but engineering
freedom and local learning decline. Platform teams inherit domain support,
product teams lose debugging context, vendors gain pricing power, and a future
exit requires coordinated migration of policy, identity, evidence, memory, and
runtime—not just endpoints.

**Evidence base:** [AWS AgentCore Gateway](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway.html),
[Microsoft Foundry Agent Service](https://learn.microsoft.com/en-gb/azure/ai-foundry/agents/overview?context=%2Fazure%2Fai-studio%2Fcontext%2Fcontext&view=foundry-classic),
[Google Gemini Enterprise Agent Platform](https://cloud.google.com/blog/products/ai-machine-learning/the-new-gemini-enterprise-one-platform-for-agent-development),
[DORA](https://dora.dev/capabilities/platform-engineering/), and the
[practitioner gateway-boundary thread](https://www.reddit.com/r/mcp/comments/1uhelfu/where_do_you_draw_the_line_with_litellms_mcp/).

### Wildcard — Verifiable delegated authority becomes the real platform boundary

**Headline:** A serious agent incident, procurement rule, or standards
breakthrough makes cryptographically verifiable delegated authority and action
receipts the non-negotiable control. The organizational boundary moves away from
model access and runtime toward an identity-and-evidence plane spanning humans,
agents, tools, and providers.

**Falsifiable triggers:**

- By 2027-07-30, a regulator, major public procurer, or cross-industry standard
  requires machine-verifiable binding among the human principal, agent version,
  delegated scope, tool action, and retained evidence.
- Signed A2A Agent Cards are supplemented in widespread implementations by
  interoperable proof of authority and revocation, not merely signed discovery
  metadata.
- NIST or another recognized standards body publishes implementable guidance
  adopted by at least two major identity platforms.

**Leading indicators over the next 6–12 months:** NIST identity deliverables;
tamper-evident action receipts; agent-aware OAuth/OIDC profiles; human-on-behalf-
of delegation; non-repudiation requirements; signed evaluation trails; and
identity vendors, rather than model vendors, leading enterprise agent
architecture.

**Probability:** **Low — 5%.** NIST asks exactly these questions and A2A has a
cryptographic foothold, but the mechanisms are not yet mature or broadly
implemented. The wildcard is the speed at which one high-impact incident or
procurement mandate could change the priority.

**Downstream consequences:** existing identity and security teams gain the
central role. Runtime and model choice become more replaceable if authority and
evidence remain portable. Conversely, one proprietary identity plane could
become an even deeper lock-in point than today's model gateways.

**Evidence base:** [NIST/NCCoE identity concept paper](https://www.nccoe.nist.gov/publications/other/accelerating-adoption-software-and-ai-agent-identity-and-authorization-concept),
[NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative),
[A2A specification](https://a2a-protocol.org/latest/specification/), and
[NIST evaluation probes](https://www.nist.gov/programs-projects/building-evaluation-probes-agentic-ai).

## The single 90-day signal

**Run one exit drill by 2026-10-28.**

Move one representative, non-trivial workflow between two model/runtime stacks
while keeping the same domain tool implementations. Preserve its least-privilege
identity, approval behavior, MCP/A2A interfaces where applicable, evaluation
dataset, and end-to-end OpenTelemetry evidence.

Record only one composite signal: **the percentage of the workflow's operational
contract that survived unchanged**. The contract comprises tool schemas,
identity/delegation scope, policy inputs, evaluation cases and results, trace
fields, ownership metadata, and incident runbook.

- **Thin-boundary signal:** at least 80% survives unchanged, domain code changes
  by no more than 20%, and the move takes no more than five engineer-days.
- **Thick-boundary signal:** credentials, policies, evaluation history, trace
  meaning, approval flow, or catalogue state must be reconstructed manually,
  regardless of whether the MCP endpoint itself still works.

This test is more informative than feature inventories because it measures exit,
not advertised compatibility. The thresholds are proposed decision criteria, not
industry benchmarks.

## What current coverage is most under-pricing

The under-priced effect is **the transfer of decision rights and future option
value**.

Most platform coverage prices the visible work: connectors avoided, credentials
centralized, deployments automated, or dashboards added. It rarely prices what
happens after the boundary is established:

- Every schema owner gains the ability to decide what the organization can
  express. Every admission controller gains the ability to decide what may run.
  Every gateway gains the ability to decide what may be reached.
- Exception, appeal, migration, dual-running, incident coordination, metadata
  repair, and decommissioning are not edge cases. They are the recurring cost of
  keeping a shared capability honest.
- Local skill can atrophy when a platform hides failure mechanics. The cost
  appears later, during an incident, a vendor exit, or a workflow the paved road
  cannot represent.
- An open protocol does not guarantee an open system. Policy semantics, identity
  objects, memory, evaluation evidence, and operational history can be
  proprietary even when every connection is MCP or A2A.
- Central consistency may improve agent performance while transferring review
  and prioritization work to humans downstream. Spotify's case makes this
  constraint shift unusually explicit.
- The absence of a platform also has a cost: duplicated identity integrations,
  token refresh, audit gaps, fragmented state, and fault diagnosis. Interviews
  with 20 practitioners across eight companies found value in cross-system
  collaboration and reuse but continued fragmentation, coordination, distributed
  state, and diagnosis problems. The paper is a 2026 preprint with a small,
  sector-limited sample, so it is directional rather than definitive.
  ([enterprise MCP interview study, 2026-06-08](https://arxiv.org/abs/2606.09182))

The practical accounting unit should therefore be **total work per successful,
governed, replaceable workflow**, not platform adoption, server count, gateway
traffic, or feature coverage. Engineering freedom is not the absence of shared
constraints; it is the retained ability to understand, change, extend, bypass
with accountability, replace, and leave them.

## Watch list

1. **MCP conformance coverage:** watch which clients, SDKs, servers, and gateways
   pass scenarios for the 2026-07-28 specification, not merely claim “MCP
   support.” This indicates whether the protocol is a real portability layer.
2. **MCP enterprise-work completion:** watch audit, SSO, gateway behavior, and
   configuration-portability work from the 2026 roadmap. These determine how
   much bespoke platform scaffolding remains.
3. **MCP extension sprawl:** watch whether Tasks, Skills over MCP, and MCP Apps
   remain optional and composable or become incompatible vendor profiles.
4. **MCP registry trust signals:** watch provenance, ownership verification,
   vulnerability handling, versioning, abandonment, and revocation—not only
   published-server counts.
5. **A2A signed Agent Cards:** watch production verification, key rotation,
   revocation, and multi-tenant use. A signature without lifecycle operations is
   discovery integrity, not delegated authority.
6. **A2A/MCP boundary clarity:** watch whether implementations keep agent
   coordination, tool access, and workflow orchestration distinct or hide all
   three behind one proprietary runtime.
7. **NIST agent-identity deliverables:** watch for implementable profiles covering
   human-agent binding, on-behalf-of delegation, least privilege, audit, and
   non-repudiation.
8. **Evaluation standard maturity:** watch revisions to NIST AI 800-2 and the
   evaluation-probes project for reproducible, machine-readable evidence that can
   travel across platforms.
9. **OpenTelemetry GenAI stability:** watch the stability status of agent,
   workflow, tool, and evaluation conventions, plus compatibility across
   instrumentations and backends.
10. **Sensitive telemetry practice:** watch default redaction, content opt-in,
    regional storage, retention, and access controls. Trace portability that
    leaks prompts or tool results is not useful leverage.
11. **EU enforcement evidence:** watch how the AI Office enforces GPAI obligations
    from 2026-08-02 and what evidence deployers ask model providers to export.
12. **EU high-risk implementation:** watch harmonized standards and guidance
    before 2027-12-02. Evidence requirements may pull capability into shared
    controls even when execution stays local.
13. **Cloud-suite coupling:** watch whether AWS AgentCore, Microsoft Foundry, and
    Google Gemini Enterprise permit independent use and export of identity,
    gateway, evaluation, memory, policy, and observability components.
14. **Existing developer-platform integration:** watch Backstage and comparable
    catalogues for agent identity, authority, evaluation, and runtime metadata.
    This tests whether a separate agent catalogue is necessary.
15. **Gateway scope creep:** watch the share of routing, retry, workflow state,
    approval logic, and domain policy moving into gateways; also watch exception
    lead time and common-mode incidents.
16. **Practitioner build-versus-buy reports:** watch for fully loaded staffing,
    on-call, token-lifecycle, upgrade, support, migration, and decommissioning
    costs. Current public discussion has anecdotes but little comparable cost
    evidence.
17. **Tool-discovery scaling:** watch searchable or dynamically filtered tool
    catalogues versus loading every schema into context. Engineers already report
    context and collision problems at large tool counts.
    ([practitioner discussion](https://www.reddit.com/r/mcp/comments/1t73igk/how_to_connect_100_mcp_servers_without_the/))
18. **Outcome-aware platform scorecards:** watch task success, time for standard
    and exceptional work, post-agent review load, incident recovery, voluntary
    retention, bypasses, and switching time. Adoption alone cannot distinguish a
    paved road from a golden cage.

## Source receipts

### Calendar

- **Skipped intentionally.** The source chapter names no actor-specific launch,
  contract, vote, hearing, or deadline that would justify a forward calendar.
  Regulatory dates above are context for second-order effects, not a claim that
  this chapter has become an event-driven story.

### Forecasts, roadmaps, and standards

- [MCP 2026 roadmap](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/)
  — 2026-03-09. Primary roadmap; useful for acknowledged production gaps.
  Maintainer-authored and therefore optimistic about MCP's trajectory.
- [MCP specification 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28)
  and [changelog](https://modelcontextprotocol.io/specification/2026-07-28/changelog)
  — authoritative protocol requirements and breaking changes; say nothing by
  themselves about implementation quality or adoption.
- [A2A specification](https://a2a-protocol.org/latest/specification/) — current
  normative source for discovery, tasks, security schemes, and Agent Card
  signing.
- [Linux Foundation A2A update](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year)
  — 2026-04-09. First-party adoption announcement; ecosystem counts and production
  claims were not independently audited here.
- [Linux Foundation Agentic AI Foundation announcement](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation?hs_amp=true)
  — 2025-12-09. Establishes common governance for MCP, goose, and AGENTS.md and
  names major industry participants; it is an institutional launch statement.
- [OpenTelemetry GenAI observability](https://opentelemetry.io/blog/2026/genai-observability/)
  — 2026-05-14. Primary practitioner documentation for GenAI telemetry and
  sensitive-content defaults; conventions remain under active development.

### Regulation, public research, and filings

- [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)
  and [2026 AI Omnibus summary](https://digital-strategy.ec.europa.eu/en/news/ai-omnibus-enters-force)
  — primary legal text plus Commission implementation update. The Commission
  summary was used for amended dates; this research is not legal advice.
- [European Commission GPAI guidance](https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers)
  — current enforcement and provider timeline; applies to model providers, not
  automatically to every internal agent platform.
- [EDPB Opinion 28/2024 summary](https://www.edpb.europa.eu/news/edpb-opinion-on-ai-models-gdpr-principles-support-responsible-ai_en)
  — 2024-12-18. Primary regulator interpretation on anonymity and lawful bases;
  case-specific application remains necessary.
- [NIST agent identity concept paper](https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents)
  — 2026-02-05. Primary public-research agenda; it identifies unresolved
  questions rather than prescribing a finished architecture.
- [NIST AI Agent Standards Initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)
  — 2026-02-17. Primary program announcement; future deliverables were not assumed
  to exist.
- [NIST AI 800-2 draft announcement](https://www.nist.gov/news-events/news/2026/01/towards-best-practices-automated-benchmark-evaluations)
  — 2026-01-30. Primary source showing evaluation practices are still emerging.
- [NIST evaluation probes](https://www.nist.gov/programs-projects/building-evaluation-probes-agentic-ai)
  — updated 2026-05-05. Ongoing public research into machine-readable audit trails,
  not evidence of widespread production use.
- [EU AI Office frontier-AI findings](https://digital-strategy.ec.europa.eu/en/library/ai-office-publishes-frontier-ai-expert-findings-eu-competitiveness-sovereignty-and-security)
  — 2026-07-15. Expert-forum synthesis useful for the sovereignty frame; the page
  states that the findings are not an official Commission position.

### Vendor, analyst, and practitioner material

- [AWS AgentCore overview](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/)
  and [Gateway documentation](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway.html)
  — current product documentation demonstrating lifecycle bundling. Capability
  claims are vendor-authored and do not establish customer outcomes.
- [Microsoft Foundry Agent Service](https://learn.microsoft.com/en-gb/azure/ai-foundry/agents/overview?context=%2Fazure%2Fai-studio%2Fcontext%2Fcontext&view=foundry-classic)
  and [hosted-agent identity](https://learn.microsoft.com/en-us/azure/foundry/agents/concepts/hosted-agents)
  — current product documentation for per-agent identity, managed runtime,
  MCP/A2A endpoints, and observability; some features are previews.
- [Google Gemini Enterprise Agent Platform](https://cloud.google.com/blog/products/ai-machine-learning/the-new-gemini-enterprise-one-platform-for-agent-development)
  and [Agent Engine identity setup](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/set-up)
  — 2026 product framing plus technical identity documentation; the per-agent
  identity feature is marked preview.
- [DORA platform-engineering capability](https://dora.dev/capabilities/platform-engineering/)
  and [2024 DORA report](https://dora.dev/research/2024/dora-report/) — research-
  informed guidance that records both productivity benefits and stability or
  throughput risks. DORA is run by Google Cloud.
- [Spotify Engineering](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint)
  — 2026-06-03. Detailed first-party case on Backstage, agents, fleet automation,
  and shifted bottlenecks; self-reported metrics were not independently verified.
- [Enterprise MCP interview study](https://arxiv.org/abs/2606.09182) —
  2026-06-08 preprint based on 20 practitioners at eight Internet and financial
  companies. Useful early qualitative evidence; small, sector-limited, and not
  treated as population-level prevalence.
- [Production MCP: A Practitioner's Guide](https://davidgolverdingen.nl/en/insights/production-mcp-practitioners-guide)
  — 2026-03-26. One engineer's account after nine production servers. Valuable
  operational detail, but a single organization and a deliberately narrow
  mid-market thesis.

### Community

- [Where do you draw the line with LiteLLM's MCP Gateway?](https://www.reddit.com/r/mcp/comments/1uhelfu/where_do_you_draw_the_line_with_litellms_mcp/)
  — 2026 community thread containing a reported large internal deployment and
  direct debate over gateway versus orchestration scope.
- [Build vs buy on MCP gateway/tool servers](https://www.reddit.com/r/mcp/comments/1uokcud/build_vs_buy_on_mcp_gatewaytool_servers/)
  — 2026 community thread surfacing maintenance, token lifecycle, audit, policy,
  and staffing concerns; several replies are vendor-affiliated.
- [Centralized MCP gateway for permissions](https://www.reddit.com/r/mcp/comments/1rhavm1/anyone_else_building_a_centralized_mcp_gateway_to/)
  — 2026 community thread showing demand for a narrow, pluggable gateway and
  dissatisfaction with all-in-one suites.
- [Connecting 100 MCP servers](https://www.reddit.com/r/mcp/comments/1t73igk/how_to_connect_100_mcp_servers_without_the/)
  — 2026 community discussion about schema volume, dynamic discovery, filtering,
  permissions, and context cost.

Community material is evidence of concerns, vocabulary, and lived design choices,
not a representative sentiment poll. The threads are self-selected, may contain
promotion, and cannot establish how common any architecture is.

### Proper-noun snowball audit and evidence gaps

The first pass identified MCP/AAIF, A2A/Linux Foundation, NIST/NCCoE/CAISI,
OpenTelemetry, the European Commission/AI Office/EDPB, AWS, Microsoft, Google,
DORA, Spotify, and Backstage. The second pass searched those entities against
identity, authorization, evaluation, observability, sovereignty, and
interoperability. OAuth/OIDC, W3C Trace Context, cloud IAM products, registries,
and several commercial gateways appeared as dependencies; they were kept as
background unless a primary source made them load-bearing.

What remains missing is as important as what was found:

- no matched comparison of central, federated, and local ownership models;
- no reliable public distribution of fully loaded build-versus-buy costs;
- no population-level survey of ordinary product engineers on AI-platform scope;
- little evidence on decommissioning, vendor exit, exception latency, or
  catalogue staleness;
- few independently verified production case studies that preserve both
  compliance outcomes and developer freedom.

Those gaps make any universal boundary claim premature. They also make the
90-day exit drill the most useful next piece of evidence this chapter could
produce itself.
