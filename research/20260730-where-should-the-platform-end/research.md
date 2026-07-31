# Where the AI Platform Should End — Research Dossier

**Question this dossier answers:** For each AI capability, what should a shared platform own, what should an existing enterprise platform expose, and what should remain with the team that understands and carries the workflow?

**Last updated:** 2026-07-30

## The Story in One Paragraph

There is no evidence-based universal perimeter for an “AI platform.” The strongest provisional answer is a thin but firm shared spine: common contracts, identity integration, credential brokerage, minimum mandatory controls, trace and evaluation evidence, catalogue ingestion, and portability tests; workflow teams retain tool meaning, business authorization, orchestration, domain evaluation, release judgment, and product consequences. That answer changes when repeated work, pooled capacity, global consistency, or regulatory evidence crosses a real scale or risk threshold: Uber's Michelangelo, Google's TFX, Borg, and Zanzibar show that broad integrated machinery can create substantial leverage, while DORA finds that internal platforms can improve perceived productivity and organizational performance yet reduce throughput and change stability, especially when independence is lost ([Uber](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/); [TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/); [Borg](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/); [Zanzibar](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/); [DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). The real boundary is therefore not “central versus local”; it is where a shared mechanism stops retiring more total work and risk than its support, coordination, latency, blast radius, lock-in, and loss of local judgment create.

## Evidence Quality and Limits

The evidence is strong enough to reject a feature checklist and weak enough to reject a universal blueprint.

| Evidence class | What it can establish | Principal limits |
|---|---|---|
| **Primary specifications and law** — MCP, A2A, OpenTelemetry, Backstage, NIST, EU law | What a protocol, catalogue, control, or legal role actually promises; what it explicitly does not enforce | Specifications do not prove adoption, implementation quality, net value, or organizational fit |
| **Independent/public-interest records** — SEC, NTSB, UK CMA, EDPB | Failure mechanisms, legal duties, switching barriers, and regulator findings | Usually adjacent to AI-platform design rather than direct comparisons of platform boundaries |
| **Industry research** — DORA, Stack Overflow, FinOps Foundation, CNCF | Cross-organization associations, adoption, reported pain, and operating guidance | Mostly self-selected, observational, and institutionally situated; causality and platform breadth are not isolated |
| **Primary company case studies** — Google, Uber, Spotify, AWS, Microsoft | Concrete architectures, operating mechanisms, and reported scale | Companies publish successes more readily than failures; platform headcount, non-users, exception queues, and full cost are usually absent |
| **Academic research** — TFX, Borg, Zanzibar, MLOps mapping, enterprise MCP interviews | Reproducible mechanisms, measured cases, or structured qualitative evidence | Much of the strongest work comes from unusually large organizations; the 2026 MCP interview preprint covers only 20 practitioners at eight companies |
| **Vendor documentation and pricing** | Current capabilities, meters, regions, and contractual responsibility boundaries | Commercially interested; feature availability does not establish realized customer value |
| **Community evidence** — Hacker News, Reddit, GitHub, practitioner blogs | Failure texture, support burdens, confusions, workarounds, and questions practitioners consider consequential | Qualitative and self-selected; issue trackers over-sample failure, forum identities are often unverifiable, and vendor participation can be hard to distinguish |

No source found a matched comparison of contract-only, central-runtime, federated, and vendor-managed AI capabilities. No public source prices the fully loaded annual platform cost—including central and product-team labor, exceptions, incidents, dual running, migration, and decommissioning—for Michelangelo, TFX, Zanzibar, Backstage, or a comparable AI-agent platform. No population-level survey asks ordinary product engineers where each AI-platform responsibility should sit. These gaps are why this dossier proposes an organizational experiment and stopping test instead of declaring an industry law.

## Cast

| Role or named entity | Stake and recent material action |
|---|---|
| **Application and product engineers** | Build and debug the workflows and remain accountable to users. In Stack Overflow's survey published 2025-07-29, 84% used or planned to use AI tools, but 46% distrusted output accuracy and 33% trusted it—evidence that verification and understandable fallback matter more than access alone ([survey](https://survey.stackoverflow.co/2025/ai)). |
| **Platform engineers and Google DORA** | Build shared paths and measure their effects. DORA's 2024 report found both platform-associated productivity gains and throughput/stability penalties; its guidance emphasizes independence, extensibility, feedback, and task success ([report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf); [guidance](https://dora.dev/capabilities/platform-engineering/)). |
| **Google Site Reliability Engineering** | Supplies a concrete precedent for conditional operational ownership: readiness, staffing, toil limits, SLOs, progressive transfer, and the ability to hand a service back ([engagement model](https://sre.google/sre-book/evolving-sre-engagement-model/); [team lifecycles](https://sre.google/workbook/team-lifecycles/)). |
| **NIST, NCCoE, and CAISI** | Separate development, deployment, operation, domain expertise, evaluation, identity, authorization, auditing, and non-repudiation roles. In 2026 they were still treating agent identity and evaluation practice as open standardization and research work, not solved platform features ([AI RMF](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/); [agent identity, 2026-02-05](https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents); [evaluation, 2026-01-30](https://www.nist.gov/news-events/news/2026/01/towards-best-practices-automated-benchmark-evaluations)). |
| **European Commission, EU AI Office, EDPB, and national authorities** | Allocate legal obligations across model providers, system providers, and deployers. GPAI obligations began on 2025-08-02, Commission enforcement begins 2026-08-02, and EDPB analysis of personal data remains use-case specific ([GPAI guidance](https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers); [AI Act navigation](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act); [EDPB Opinion 28/2024](https://www.edpb.europa.eu/documents/opinion-of-the-board-art-64/opinion-282024-on-certain-data-protection-aspects-related-to_en)). |
| **FinOps Foundation practitioners** | Allocate cloud, SaaS, data-centre, and AI spend. In the 2025 report, 63% of respondents managed AI spend, up from 31% in the previous edition, making allocation and unit economics part of platform ownership ([2025 State of FinOps](https://data.finops.org/2025-report/)). |
| **AWS, Microsoft, Google, OpenAI, and Anthropic** | Sell models, gateways, identity, policy, runtime, evaluation, observability, and support. AWS AgentCore, Microsoft Foundry, and Google's Gemini Enterprise Agent Platform demonstrate that vendors are bundling the whole lifecycle even as they support MCP, A2A, and OpenTelemetry ([AWS](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/); [Microsoft](https://learn.microsoft.com/en-gb/azure/ai-foundry/agents/overview?context=%2Fazure%2Fai-studio%2Fcontext%2Fcontext&view=foundry-classic); [Google](https://cloud.google.com/blog/products/ai-machine-learning/the-new-gemini-enterprise-one-platform-for-agent-development)). |
| **MCP maintainers and the Linux Foundation's Agentic AI Foundation** | Govern the upstream connection protocol; they do not decide which internal tool is trusted or which business action is authorized. MCP joined AAIF on 2025-12-09, and the 2026-07-28 specification made its core stateless and moved specialized behavior to opt-in extensions ([AAIF announcement](https://blog.modelcontextprotocol.io/posts/2025-12-09-mcp-joins-agentic-ai-foundation/); [specification](https://modelcontextprotocol.io/specification/2026-07-28)). |
| **A2A project and Linux Foundation** | Define agent discovery and coordination separately from tool access. A2A 1.0 includes Agent Cards, signatures, security schemes, and task operations; the Foundation reported more than 150 supporting organizations on 2026-04-09 ([specification](https://a2a-protocol.org/latest/specification/); [adoption announcement](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year)). |
| **Backstage maintainers and Spotify** | Provide an existing developer catalogue that can display agent metadata. Backstage says its catalogue is a cache over authoritative sources, and Spotify now exposes catalogue capabilities to agents through MCP and CLI tools rather than creating a wholly separate source of truth ([Backstage](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/); [Spotify, 2026-06-03](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint)). |
| **UK Competition and Markets Authority** | Investigated cloud switching, interoperability, egress, committed spend, and market concentration, closing its inquiry on 2025-07-31. Its findings make vendor choice and exit an architectural power question, not only procurement ([case record](https://www.gov.uk/cma-cases/cloud-services-market-investigation)). |
| **Open-source maintainers** | Carry security, compatibility, review, and support work for catalogues, protocols, gateways, policy engines, and telemetry. Census II found widely used FOSS often depends on very few contributors; a zero licence fee does not erase operating ownership ([Census II](https://lish.harvard.edu/publications/census-ii-free-and-open-source-software-%E2%80%94-application-libraries)). |

## Timeline

| Date | Precedent and what it teaches about the boundary |
|---|---|
| **2006-08-24** | AWS opened the EC2 beta: AWS owned capacity, virtualization, metering, and an API; customers retained images and applications. A narrow managed capability can remove repeated work without owning product logic ([AWS](https://aws.amazon.com/about-aws/whats-new/2006/08/24/announcing-amazon-elastic-compute-cloud-amazon-ec2---beta/)). |
| **2012-08-01** | Knight Capital's incomplete deployment reactivated old code on one of eight servers; the SEC says more than 4 million orders were sent while trying to fill 212 customer orders, contributing to a loss above $460 million. Declared configuration is not observed runtime truth ([SEC order](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf)). |
| **2017-01-31** | An accidental primary-database deletion caused GitLab.com data loss; GitLab estimated effects on roughly 5,000 projects, 5,000 comments, and 700 new accounts. A central source of truth has value only if restoration and reconciliation work ([GitLab](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)). |
| **2017-02-28** | An incorrect operational command removed more S3 servers than intended in `us-east-1`, affecting dependent services and even the dashboard administration path. Central dependencies need cells, degraded modes, and independent recovery paths ([AWS](https://aws.amazon.com/message/41926/)). |
| **2017-09-05** | Uber described Michelangelo, a broad internal platform spanning data, training, evaluation, deployment, serving, and monitoring after teams had repeatedly built bespoke systems. Integrated scope can repay its cost at substantial scale ([Uber](https://www.uber.com/gb/en/blog/michelangelo-machine-learning-platform/)). |
| **2019-05-20** | Google presented continuous training in TFX. A reported Google Play deployment moved from months to weeks and coincided with a 2% increase in installs, showing that shared lifecycle machinery can affect delivery and business outcomes ([TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/)). |
| **2020-03-16** | Spotify open-sourced Backstage, separating catalogue and developer experience from the independently operated systems it presents. The portal can own ingestion and display without owning every runtime ([Backstage](https://backstage.io/blog/2020/03/18/what-is-backstage/)). |
| **2022-05-03** | Kubernetes 1.24 removed the in-tree `dockershim` adapter after CRI became the runtime contract. The project retained the interface and externalized the vendor-specific implementation and lifecycle ([Kubernetes](https://kubernetes.io/blog/2022/05/03/kubernetes-1-24-release-announcement/)). |
| **2022-07-12** | GDS announced the retirement of GOV.UK PaaS rather than fund a major rewrite as cloud offerings and departmental capability improved. A platform that once created leverage can later fall below its economic threshold ([GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). |
| **2023-04-11** | CNCF published platform guidance defining reusable capabilities and developer autonomy rather than a fixed product or feature list ([CNCF](https://www.cncf.io/blog/2023/04/11/announcing-a-white-paper-on-platforms-for-cloud-native-computing/)). |
| **2024-06-28** | A systematic mapping study identified 35 MLOps components and several architecture variants across 43 primary studies. “MLOps” was already a design space, not one inevitable perimeter ([study](https://arxiv.org/abs/2406.19847)). |
| **2024-10-22** | DORA published its tenth report, associating platform use with productivity and organizational gains as well as lower throughput and change stability. Platform adoption and delivery outcome can diverge ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). |
| **2024-11-25** | Anthropic introduced MCP as an open connection standard. Its architecture separated hosts, clients, and servers; protocol discovery did not become business authorization ([Anthropic](https://www.anthropic.com/news/model-context-protocol)). |
| **2025-12-09** | MCP moved into AAIF governance. Upstream protocol stewardship became more neutral, while enterprise admission, identity, runtime, and support remained local decisions ([MCP/AAIF](https://blog.modelcontextprotocol.io/posts/2025-12-09-mcp-joins-agentic-ai-foundation/)). |
| **2026-07-28** | MCP's largest revision made the core stateless, added per-request capabilities and trace propagation, formalized extensions, strengthened authorization details, and introduced a deprecation policy. Production connectivity became easier, but MCP still says it cannot enforce consent, authorization, privacy, or tool safety itself ([specification](https://modelcontextprotocol.io/specification/2026-07-28); [changelog](https://modelcontextprotocol.io/specification/2026-07-28/changelog)). |

## Geography and Jurisdiction

Chapter 4 names no organization, customer, contract, corporate seat, or deployment region, so no specific jurisdictional answer is possible. The available evidence nevertheless establishes six boundary inputs:

| Layer | What must be resolved before centralizing |
|---|---|
| **EU provider versus deployer roles** | The AI Act allocates duties across the value chain; a platform may collect evidence but cannot absorb a deployer's monitoring, human-oversight, and incident duties ([Commission guidance](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)). |
| **Personal data** | Prompts, evaluation sets, traces, tool arguments, model development, and deployment can be distinct processing activities; EDPB Opinion 28/2024 calls for case-by-case analysis ([EDPB](https://www.edpb.europa.eu/documents/opinion-of-the-board-art-64/opinion-282024-on-certain-data-protection-aspects-related-to_en)). |
| **Data at rest versus inference and support access** | Microsoft distinguishes stored data in a selected Geo from “Global” inference processing and some remote support access. A regional storage label does not fully describe the data path ([Microsoft residency](https://azure.microsoft.com/en-us/explore/global-infrastructure/data-residency/)). |
| **Compelled access** | Physical residency and legal control are separate; the US CLOUD Act can reach data in a covered provider's possession, custody, or control, including some data stored abroad ([US DOJ](https://www.justice.gov/archives/opa/press-release/file/1153446/dl?inline=)). |
| **Switching law** | The EU Data Act removes covered switching charges, including egress, from 2027-01-12, but not schema conversion, re-evaluation, dual running, or support migration ([EU Data Act](https://digital-strategy.ec.europa.eu/en/factpages/data-act-explained)). |
| **Market concentration** | The UK CMA found technical and commercial barriers that make switching and multi-cloud use harder. A provider-specific shared layer can multiply that barrier across every consuming team ([CMA](https://www.gov.uk/cma-cases/cloud-services-market-investigation)). |

The asymmetry is between where data sits, which provider and support workforce can reach it, which legal actor owes the duty, and which technical component supplies evidence or enforcement. A central gateway may make regional routing easier while simultaneously becoming the cross-border data path and an organization-wide supplier dependency.

## By the Numbers

These are decision inputs, not a universal ROI model. Survey figures are associations or self-reports; vendor figures are list prices or first-party scale claims.

| Sourced fact | Category | What it means |
|---|---|---|
| Internal-platform users reported **8% higher individual productivity**, **10% higher team performance**, and platform-using organizations **6% higher software-delivery and operations performance** in DORA's report published 2024-10-22 ([DORA, pp. 50–51](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). | Productivity/performance | Shared capabilities can create value, but observational association does not identify which capabilities caused it. |
| The same report associated platform use with about **8% lower throughput** and **14% lower change stability**; exclusive use carried a further **6% throughput decrease** ([DORA, pp. 52–53](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). | Delivery trade-off | Adoption can rise while delivery outcomes worsen; mandatory fit is itself a measurable risk. |
| Developer independence was associated with a **5% productivity improvement** at individual and team levels ([DORA](https://dora.dev/capabilities/platform-engineering/)). | Developer agency | Ticket-free completion and transparent failure are boundary metrics, not “soft” preferences. |
| DORA's updated summary says **90% of organizations** used an internal platform and **76%** had dedicated platform teams ([DORA, updated 2026-01-12](https://dora.dev/capabilities/platform-engineering/)). | Adoption | Prevalence does not establish the correct scope; it increases the risk of adopting a fashionable perimeter without a local problem. |
| Google caps SRE operational work at **50%**; survey averages were near **33%**, with individual reports from **0% to 80%** ([Google SRE](https://sre.google/sre-book/eliminating-toil/)). | Labor/capacity | Runtime ownership consumes measurable engineering capacity. |
| A single-site two-person 24/7 rotation needs at least **8 engineers** under Google's 25% on-call rule, and its workbook recommends **9** for resilience ([Google SRE](https://sre.google/workbook/on-call/)). | Staffing | “The platform owns runtime” is a funding and staffing claim, not a box on an architecture diagram. |
| The 2025 State of FinOps had **861 respondents** representing about **$69 billion** in public-cloud spend; **63%** managed AI spend, up from **31%** in the prior edition ([FinOps Foundation](https://data.finops.org/2025-report/)). | Spend/adoption | AI cost spans models, cloud, SaaS, and private infrastructure; gateway token counts are incomplete unit economics. |
| UK customers spent **£9 billion** on public-cloud infrastructure in the year ending 2023-12-31, growing more than **30% annually**; AWS and Microsoft each held up to **40%** of customer spend ([CMA provisional findings, 2025-01-28](https://www.gov.uk/government/news/cma-independent-inquiry-group-publishes-provisional-findings-in-cloud-services-market-investigation)). | Market structure | Consolidation can improve buying power while turning one provider choice into an organization-wide exit problem. |
| MCP maintainers reported more than **97 million monthly SDK downloads** and **10,000 active servers** on 2025-12-09 ([MCP/AAIF](https://blog.modelcontextprotocol.io/posts/2025-12-09-mcp-joins-agentic-ai-foundation/)). | Ecosystem scale | No internal platform team can operate or certify the ecosystem; admission, provenance, and support must be bounded. |
| Stack Overflow's 2025 survey received more than **49,000 responses**; **84%** used or planned AI tools, **46%** distrusted output accuracy, **33%** trusted it, and **3%** highly trusted it ([survey](https://survey.stackoverflow.co/2025/ai)). | Practitioner adoption/trust | Access is common; verification and judgment remain scarce. |
| Uber reports about **400 active ML projects**, more than **20,000 monthly training jobs**, more than **5,000 production models**, and **10 million peak predictions per second** ([Uber](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/)). | Platform scale | Broad lifecycle integration is more defensible when divided by this repeated demand, but Uber does not publish full platform cost. |
| Zanzibar reports **trillions of ACLs**, **millions of authorization checks per second**, less than **10 ms** 95th-percentile latency, and more than **99.999%** availability over three years ([Google Research](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)). | Consistency/scale | Some shared mechanisms create economies no per-team implementation can reproduce; Google scale is not a default build recommendation. |

## How It Actually Works

The platform boundary is an operating process, not a diagram.

1. **Start with an observed workflow constraint.** A product team supplies the workflow, risk tier, lead time, failure history, duplicated work, and exit requirement. Platform, security, SRE, data, and domain owners identify what genuinely repeats. The output is a measured problem statement, not a feature roadmap. CNCF treats platforms as products learned from users; Fowler's thinnest-viable-platform guidance starts with the smallest helpful capability ([CNCF](https://tag-app-delivery.cncf.io/whitepapers/platforms/); [Fowler](https://martinfowler.com/articles/platform-prerequisites.html)).
2. **Decompose “ownership.”** For each candidate capability, assign contract/interface, source of truth, runtime operation, domain decision, enforcement, on-call, funding, and exit. “Platform owns identity” is meaningless if enterprise IAM issues credentials, a vendor runs the service, a resource team decides entitlement, and a product team carries the incident.
3. **Choose an operating model per capability.** Compare contract-only, central runtime, federated control, existing-platform extension, and vendor service against reuse, risk, latency, blast radius, support capacity, switching cost, and reversibility. The same organization may centralize a gateway, federate policy enforcement, reuse its existing observability system, and leave evaluation semantics local.
4. **Publish the smallest contract at the authoritative source.** Version schemas for ownership, risk, identity, tool/model requirements, evaluation evidence, telemetry, and deployment references. Validate in CI; let the existing catalogue ingest them. Backstage explicitly treats its catalogue as a cache rather than the ultimate truth ([Backstage](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)).
5. **Put enforcement at the action boundary.** Identity teams establish authentication and credential lifecycle; resource and domain owners define permitted business actions; the resource or tool that causes the effect enforces the decision. MCP requires audience/resource-bound tokens and forbids unsafe token passthrough, but protocol authorization does not determine business permission ([MCP authorization](https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization)).
6. **Insert runtime mediation only when the guarantee needs the data path.** A gateway is justified for credentials, provider allowlists, quotas, regional routing, cost attribution, uniform telemetry, or emergency revocation that must apply to every call. Once used, it becomes a runtime product with latency, availability, retry, compatibility, and on-call obligations—not merely an API wrapper ([Azure AI Gateway](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)).
7. **Separate tool exposure from tool meaning.** The platform can own registry admission, provenance, delegated-auth patterns, sandbox/egress controls, audit format, and reusable clients. The downstream owner should retain business invariants, implementation, data entitlement, and incident support. MCP tool annotations are untrusted hints unless the server itself is trusted ([MCP tools](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)).
8. **Share evaluation plumbing, not universal judgment.** A central service can run jobs, version datasets, store evidence, provide baseline suites, and support independent assessment. Workflow owners define representative cases, harms, thresholds, human review, and release acceptance. NIST connects evaluation to deployment context and domain expertise ([NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)).
9. **Extend existing delivery and observability platforms.** Prompts, model aliases, tools, agent graphs, evaluation sets, and policy bundles are new artefacts; they do not automatically justify new CI/CD or telemetry systems. Existing environments already provide approvals, provenance, rollout, rollback, and retention primitives ([GitHub environments](https://docs.github.com/en/actions/reference/workflows-and-actions/deployments-and-environments); [OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/)).
10. **Operate exceptions, incidents, and removal.** Every mandatory path needs an exception owner, expiry, compensating control, and observable bypass. Every runtime needs an SLO, degraded mode, incident interface, and funded on-call. Every capability needs a handback or decommissioning path.

### The internals most architecture summaries blur

- **Control plane is not data plane.** Desired state, policies, registrations, routing configuration, and evidence requirements may be central while decisions and execution remain distributed. OPA documents centrally managed policies with local low-latency engines ([OPA](https://www.openpolicyagent.org/docs/management-introduction)).
- **Catalogue is not authorization.** A catalogue answers what exists and who appears responsible. Fresh resource state, a principal, delegated context, action, and resource-side policy answer whether an action may happen.
- **Gateway is not provider independence.** It centralizes access but inherits every provider's evolving streaming, tool, auth, retry, and capability semantics. A lowest-common denominator may destroy capability; a rich abstraction creates a permanent compatibility team.
- **MCP is not an integration owner.** Protocol/SDK evolution, host runtime, registry, server operation, downstream API, identity, sandbox, and incident response are seven separable responsibilities.
- **Evaluation is not observability.** Telemetry records what happened; evaluation applies a contextual judgment. OpenTelemetry can make evidence portable, but full prompts and tool results create privacy, retention, and access-control work ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/)).
- **Declared state is not observed state.** Knight Capital, GitLab, S3, Cloudflare, OAuth integration compromise, and Codecov show failure through drift, common-mode control, weak recovery, excessive delegated reach, and trusted integration paths ([SEC](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf); [Cloudflare](https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/); [GitHub OAuth alert](https://github.blog/news-insights/company-news/security-alert-stolen-oauth-user-tokens/); [Codecov](https://about.codecov.io/apr-2021-post-mortem/)).

## Capability-by-Capability Boundary Matrix

This is a provisional allocation pattern. “Shared” may mean a narrow AI-platform capability, an existing enterprise platform, or a vendor-operated service; it does not mean one team should build every component.

| Capability | Contract / interface | Source of truth | Runtime operation | Domain decisions | Enforcement | On-call | Funding | Exit |
|---|---|---|---|---|---|---|---|---|
| **Model access / gateway** | AI platform defines provider-neutral request, identity, cost, trace, failure, and extension contracts | Approved providers/regions in policy system; workflow config with product team | Central or vendor gateway only for controls requiring every request; approved direct path remains possible | Product team chooses model, prompts, quality/cost trade-off, fallback meaning | Gateway enforces organization-wide provider, quota, region, and credential controls; product enforces workflow behavior | Gateway operator owns gateway SLO; product team owns outcome and provider-specific failure | Shared fixed cost plus usage allocated to consuming product | Second provider adapter, exportable usage/policy data, dual-run and bypass test; heterogeneous vendor prices and regions make real switching essential ([AWS pricing](https://aws.amazon.com/bedrock/pricing/); [DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)) |
| **MCP and tooling** | Platform owns admission schema, protocol profile, provenance, auth hooks, versioning, telemetry, and conformance | Tool descriptor near code or authoritative domain repository; registry is an index/cache | Domain team or qualified vendor runs server; platform may run shared sandbox, registry, or gateway | Domain owner defines tool meaning, inputs, side effects, data scope, and correctness | Resource service enforces business authorization; platform enforces admission, egress, sandbox, minimum scopes, revocation | Tool/server owner carries domain failure; shared gateway/registry owner carries its layer | Domain funds tool; shared platform funds reusable clients, conformance, security, and registry | Portable MCP interface plus source, tests, credentials migration, replacement owner, revocation and removal plan; MCP itself cannot enforce tool safety ([MCP specification](https://modelcontextprotocol.io/specification/2026-07-28)) |
| **Identity and authorization** | Enterprise identity team defines principals, delegation, token, policy-input, audit, and revocation contracts; AI platform integrates | Enterprise IAM is authoritative for people/workloads; resource system for entitlements; product for requested delegated scope | Existing IAM/policy services or vendor; do not create a parallel “AI identity” authority | Resource/domain owner decides permitted action and risk; user grants consent where required | Enforce at resource/action boundary; gateway can add a mandatory outer floor | IAM owner for issuance/revocation; resource owner for entitlement and action failure | Enterprise control budget plus per-product integration | Standard OAuth/OIDC/resource-bound credentials, exportable policy, revocation drill, no dependence on catalogue owner fields; NIST still treats agent identity as an open problem ([NIST](https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents)) |
| **Evaluations** | Shared team defines runner, dataset/evaluator format, lineage, evidence, reproducibility, and baseline suites | Domain team owns representative cases and expected outcomes; evidence store owns immutable run records | Central service can schedule and store runs; product pipeline invokes it | Domain experts define harms, thresholds, human review, and release acceptance; risk sets mandatory floors | CI/admission gate enforces evidence presence and minimum policy; accountable deployer makes go/no-go judgment | Evaluation service owner for harness; product owner for bad decision and production drift | Shared harness funded centrally; domain dataset, review, and remediation funded by product/risk owner | Export cases, evaluator versions, raw results, lineage, and decision records; rerun on a second harness ([NIST AI 800-2](https://www.nist.gov/news-events/news/2026/01/towards-best-practices-automated-benchmark-evaluations)) |
| **Observability** | Existing observability platform plus AI extension defines semantic fields, trace propagation, redaction, retention, access, and export | Runtime emits observed facts; product owns domain SLOs and outcome annotations; audit store retains evidence | Existing collectors/backends; avoid a separate AI-only telemetry island | Product/SRE define what signals mean, alert thresholds, user impact, and incident severity; privacy decides capturable content | Instrumentation and collectors enforce redaction/routing; access system enforces visibility | Telemetry platform for pipeline; each service for its alerts and incident meaning | Shared telemetry cost allocated by usage; product funds high-cardinality/domain data | OTLP/export, documented sampling/redaction, portable semantic fields, retention/deletion plan; content is opt-in because it can be sensitive ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/)) |
| **Deployment / runtime** | Existing developer platform owns environment, provenance, approval, rollout, rollback, and evidence contracts; AI profile adds model/prompt/tool/eval artefacts | Product repository and artefact stores; deployment system records observed revision | Existing cloud/Kubernetes/serverless platform or vendor; separate AI runtime only when execution primitive materially differs | Product decides release timing, config, semantic health, rollback safety, and SLO | Delivery platform enforces provenance and mandatory gates; runtime enforces isolation and resource policy | Runtime platform for substrate; product team for workload and business outcome | Platform funds substrate; product funds workload consumption and support share | Versioned artefacts, infrastructure portability, state export, dual run, rollback, and owner handback; Google SRE makes transfer conditional ([Google SRE](https://sre.google/sre-book/evolving-sre-engagement-model/)) |
| **Integrations** | Platform defines exposure, auth, timeout, retry, idempotency, version, telemetry, and retirement patterns | External/domain system owns business data; connector code and mapping live with accountable owner | Domain team owns long tail; platform owns only high-reuse adapters with stable semantics and funded support; vendor connectors need internal owner | Domain team decides mapping, side effects, reconciliation, and failure recovery | Downstream resource enforces business rules; platform applies network and minimum security policy | The team able to diagnose the external system owns the pager; shared adapter team owns common layer | Benefiting products fund domain connector; platform funds measured reusable core | Replace connector behind contract; export mappings/config; document provider API dependency and decommission downstream credentials ([DORA extensibility](https://dora.dev/capabilities/platform-engineering/)) |
| **Catalogue metadata** | AI platform defines agent-specific schema, validation, provenance, freshness, and observed-status links; existing developer platform owns presentation | Metadata beside agent/workflow or in authoritative product/IAM/risk systems; catalogue remains cache | Existing catalogue ingests and indexes; no catalogue in the live authorization path | Owning team defines purpose, lifecycle, owner, docs, and disputed meaning | CI rejects invalid metadata; catalogue never grants runtime permission | Catalogue team for ingestion/search; domain owner for inaccurate content | Existing developer-platform budget plus contribution from metadata consumers | Standard descriptors, export/search API, stale/orphan lifecycle, no runtime hard dependency; Backstage explicitly recommends this split ([Backstage](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)) |
| **Governance, cost, and exceptions** | Central governance defines risk tiers, mandatory floors, evidence, cost tags, exception, review, and retirement contracts | Legal/risk owns obligations and appetite; FinOps owns allocation model; product owns outcome/value; exception register records decisions | Policy/evidence systems may be central; enforcement can be distributed | Accountable use-case owner accepts residual risk and value trade-off within formal limits | Enforce each guarantee at earliest correct and non-bypassable boundary; record policy version and exception | Control-plane owner for availability; product for use-case incident; explicit joint incident command | Central control budget plus showback/chargeback; no unfunded transfer | Expiring exceptions, removal criteria, exportable policy/evidence, vendor and platform exit drill; cost must include migrated and exported local work ([FinOps](https://www.finops.org/wg/cloud-cost-allocation/); [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)) |

## Second-Order Effects

The boundary choice changes the surrounding organization and market, not merely the location of code.

1. **Open connection protocols commoditize access and move competition upward.** If MCP and A2A make tools and agents easier to connect, vendors have more reason to differentiate through managed identity, memory, policy, evaluation, orchestration, and evidence. An open edge can therefore coexist with a proprietary centre ([MCP roadmap](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/); [A2A](https://a2a-protocol.org/latest/specification/)).
2. **A mandatory gateway attracts adjacent authority.** Once every request passes through it, routing, quotas, retries, caching, policy, evaluation, prompt management, memory, and orchestration are each locally rational additions. The resulting gateway becomes harder to bypass, fund, operate, and replace, even if its original contract was thin.
3. **Per-agent identity creates a lifecycle institution.** Giving agents principals, delegated scopes, certificates, approval chains, and revocation creates ongoing issuance, recertification, incident, and decommissioning work. NIST's 2026 concept paper shows that the relevant trust chain is still an open design problem, not a single platform feature ([NIST](https://www.nccoe.nist.gov/publications/other/accelerating-adoption-software-and-ai-agent-identity-and-authorization-concept)).
4. **Portable evidence can increase both freedom and surveillance.** Standard trace and evaluation records can make assurance move across runtimes, but prompts, tool arguments, outputs, identities, and judgments can become a sensitive central dataset. Better portability therefore increases the need for redaction, purpose limitation, retention, regional storage, access control, and deletion ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/); [EDPB](https://www.edpb.europa.eu/documents/opinion-of-the-board-art-64/opinion-282024-on-certain-data-protection-aspects-related-to_en)).
5. **Reusing the developer platform moves the bottleneck to decisions.** Extending IAM, CI/CD, observability, and Backstage avoids duplicate substrate, but makes ownership, exception latency, release judgment, and domain evaluation the scarce resources. Agent-facing APIs can expose existing systems without resolving who is accountable for their meaning ([Spotify](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint); [Backstage](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)).
6. **Centralization redistributes skill and bargaining power.** Product teams may lose operational fluency while a central team and a small number of vendors accumulate knowledge, credentials, and budget authority. Procurement leverage can improve through aggregation, yet switching becomes harder if identity, policy, evidence, and workflow state travel with the supplier rather than with the contract ([UK CMA](https://www.gov.uk/cma-cases/cloud-services-market-investigation)).

## Money, Power, and Stakeholder Impact

### Money flows and total ownership cost

The chapter names no organization or procurement, so actual amounts are unknown. The necessary flows are still identifiable:

| From → To | What flows and why it matters |
|---|---|
| Product cost centre → model/cloud vendor | Tokens, throughput, compute, storage, network, logs, evaluation jobs, and support; allocate them to product and outcome, not an opaque platform total ([vendor meters](https://openai.com/api/)). |
| Organization → platform/SRE workforce | Salary, training, pager compensation, tools, incident response, and support; a real 24/7 service needs funded rotation capacity ([Google SRE](https://sre.google/workbook/on-call/)). |
| Product/domain teams → shared platform | Integration code, metadata, evaluation sets, documentation, exception work, incident diagnosis, and migration effort; this is often unbooked labor rather than an invoice. |
| Shared platform → product teams | Self-service workflows, reusable adapters, identity, telemetry, policy, consultation, and incident support; a ticket or privileged intervention is a cost even if the central budget absorbs it. |
| Organization → platform vendors and OSS ecosystem | Licences, ingestion, support, consulting, employee contribution time, patching, upgrades, security review, and forks; “open” moves the price, not the ownership duty ([Census II](https://lish.harvard.edu/publications/census-ii-free-and-open-source-software-%E2%80%94-application-libraries)). |
| Old platform/vendor → new platform/vendor | Export, adapter rewrite, re-evaluation, retraining, dual running, documentation, rehearsal, and decommissioning; removal of egress fees does not remove this work ([EU Data Act](https://digital-strategy.ec.europa.eu/en/factpages/data-act-explained)). |
| Platform cost centre → business units | Showback or chargeback for model, cluster, telemetry, licence, and support costs; without allocation, centralization hides unit economics ([FinOps](https://www.finops.org/wg/cloud-cost-allocation/)). |
| Organization → auditors, regulators, legal, privacy, and insurers | Assessment, documentation, legal review, incident, and enforcement work; shared evidence can reduce repetition, but accountability follows the legal actor and use case ([NIST](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)). |

Full TCO must count platform roadmap capacity, support/on-call, product-team onboarding and exceptions, vendor and infrastructure spend, control-function work, migration, dual running, re-validation, and decommissioning. A platform creates leverage only when repeated value exceeds all of those recurring costs.

### What current coverage under-prices

Most public platform stories price the shared machinery and report adoption, not the work moved to its edges. The undercounted items are product-team adapter and metadata work; domain-expert evaluation and incident time; exception queues; 24/7 staffing; policy reconciliation across catalogue, IAM, gateway, and resource; privacy review of retained prompts and tool results; dual-run and re-validation during migration; decommissioning; and the decay of local operating skill. Open protocols reduce interface conversion, but they do not make credentials, authorization semantics, state, evidence, support ownership, or contractual exit portable. These are not incidental costs: they determine whether “leverage” is repeated value creation or merely a transfer of labor and decision rights.

### Who decides

| Decision | Formal authority and veto | Reversal condition |
|---|---|---|
| Add, expand, or retire a shared capability | Platform product owner and accountable consumer class; finance/procurement controls spend; legal/security/risk veto only where obligation or appetite is breached | Repeated work removed falls below shared plus exported local work; task success, exception time, stability, or exit time crosses the agreed threshold |
| Approve a model/tool for one workflow | Accountable use-case owner accepts outcome risk; domain, privacy, security, legal, and independent assessment participate as risk requires | Model/tool/data/scope change, drift, incident, material regression, or law change |
| Authorize a tool action | Resource owner defines allowed action; IAM operates identity; user/principal supplies authority; resource enforces | Scope expansion, code/ownership change, compromise, anomaly, policy change, or failed recertification |
| Transfer production on-call | Platform/SRE and product owner jointly agree after readiness, SLO, staffing, and training; either can refuse an unsafe handoff | Service cannot run within toil/SLO limits, or no longer warrants specialist support ([Google SRE](https://sre.google/workbook/team-lifecycles/)) |
| Select a vendor or committed-spend arrangement | Procurement/finance owns commercial commitment; product/technology owns fitness and migration; legal/security/privacy own terms and risk | Price/SKU change, concentration threshold, regulation, missed SLA, provider failure, or failed exit test ([CMA](https://www.gov.uk/cma-cases/cloud-services-market-investigation)) |

The team that supplies an enforcement point does not automatically own the policy decision. The workflow team that owns context cannot waive an organization-wide legal or security floor. The catalogue team controls discoverability; the gateway team controls reachability and provider choice; the policy team controls permissible actions. Calling all three “platform” conceals materially different power.

### Stakeholder impact

| Stakeholder | Direction under a thin federated boundary | Mechanism |
|---|---|---|
| Application/product engineers | **Mixed, leaning positive** | Shared setup and controls remove toil; tickets, opaque errors, and mandatory fit reverse the benefit ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). |
| Platform engineers | **Mixed** | A bounded internal product compounds reusable work; an unbounded integration/runtime estate becomes support operations and loses roadmap capacity. |
| SRE/on-call responders | **Mixed to materially exposed** | Central expertise can improve reliability while central paths concentrate blast radius and pager load; handback and toil limits are essential. |
| ML/AI engineers | **Positive if composable; negative if flattened** | Shared evaluation, serving, and evidence reduce plumbing; lowest-common-denominator gateways block provider-specific capability. |
| Security/privacy/legal/risk | **Positive with common-mode exposure** | Shared identity and evidence retire duplicate work; a catalogue façade or central runtime defect can produce organization-wide false assurance. |
| Domain experts and affected users | **Positive only if decision authority remains real** | Contextual evaluation and human oversight preserve validity; generic central scores can erase harms. |
| Finance/FinOps/procurement | **Positive if allocated; exposed if merely centralized** | Consolidation improves negotiation and metering; an unallocated bill hides cost and subsidizes low-value workflows. |
| Existing developer, identity, delivery, and observability platform teams | **Positive under reuse; negative under duplication** | Agent-specific contracts can extend prior systems; a parallel AI stack creates competing truth and migration work. |
| Cloud/model vendors | **Positive** | Organization-wide integration, commitments, and proprietary policy/evidence semantics increase supplier leverage; tested portability limits it. |
| OSS maintainers | **Mixed and often underfunded** | Adoption and contribution increase alongside compatibility, security, and enterprise support demand. |
| Regulators/auditors | **Positive but susceptible to façade compliance** | Common inventories and evidence help; declared metadata without runtime reconciliation misleads. |
| Exceptional, small-scale, or non-AI teams | **Positive under optionality; negative under mandate** | They can reuse what helps; fixed platform and exception costs may exceed avoided work. |

The quiet winner may be the existing developer platform, which gains agent-aware metadata and machine interfaces without inheriting the runtime. The quiet losers are product engineers and domain experts whose work is relocated rather than retired: they write adapters, clean metadata, build evaluations, explain incidents, and wait for exceptions while an adoption dashboard counts them as users. Vendors win when an internal “neutral” contract mirrors one supplier's identity, policy, deployment, or evidence semantics.

## Counter-Narratives

The chapter's tentative thin-contract direction is a hypothesis. Four serious alternatives compete with it.

| Working frame | Counter-narrative and evidence | What would falsify the counter | Current read |
|---|---|---|---|
| **Start with a contract; runtime can remain local.** | A contract without authoritative state, conformance evidence, or runtime enforcement can become coordination theatre. OpenAPI says schemas do not catch every specification violation; Backstage says its catalogue is a cache; users report entities taking “hours to days to never” to appear ([OpenAPI](https://spec.openapis.org/oas/); [Backstage](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/); [issue #13834](https://github.com/backstage/backstage/issues/13834)). | A comparative pilot where contract-only teams retire as much duplicate integration/control work as runtime-backed teams, with fresher observed state and lower total cost | Counter leads for authorization and deployment guarantees; contract remains credible for vocabulary and discovery |
| **Workflow knowledge means evaluation, integration, deployment, and observability should stay local.** | Domain knowledge is necessary, but local ownership of the whole machinery duplicates pipelines, serving, evidence, and monitoring. Uber and TFX report large benefits from integrated lifecycle platforms ([Uber](https://www.uber.com/gb/en/blog/michelangelo-machine-learning-platform/); [TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/)). | At comparable scale, workflow-owned stacks deliver equal reliability and lower total labor without duplicated machinery | Counter leads at very large scale; unknown for small or heterogeneous estates |
| **Thinness preserves engineering freedom.** | A reliable central runtime can create freedom from infrastructure work teams cannot staff safely. Borg and Zanzibar show pooled scheduling and consistent authorization economies that independent teams cannot reproduce ([Borg](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/); [Zanzibar](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)). | Matched evidence that broader local control yields better delivery, recovery, and total cost than a mature shared capability | Roughly even: centralization can expand practical agency while reducing exit freedom |
| **A distinct AI platform is the right unit of analysis.** | Most named capabilities already have owners: IAM, CI/CD, observability, data, cloud, service catalogue, security, and FinOps. The AI-specific work may be a contract and adapters across existing platforms, not a new perimeter. Backstage and Spotify show agent capabilities extending an existing catalogue; DORA warns about added systems and handoffs ([Spotify](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint); [DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). | Repeated AI-specific state and failure modes that existing owners cannot support, plus evidence that one new product removes more cross-platform work than it adds | Strong for catalogue, deployment, IAM, and telemetry; less certain for gateways and agent evaluation |

The interests are symmetric. Thinness serves product-team autonomy, small central teams, open-source and point-solution suppliers, and a philosophy that values reversibility. Breadth serves cloud/AI vendors, central platform and control functions, consultants, and organizations with genuine economies of scope. Uber, Google, Spotify, AWS, Microsoft, and Google Cloud provide valuable architectural receipts while also benefiting when their platform approach is emulated or purchased. The advocate's title cannot decide the boundary.

Two contradictions must remain visible:

- Spotify reports strong associations between frequent Backstage use and activity, cycle time, deployment frequency, and deployment duration, but says high adoption made a non-user control group impossible. The evidence is association, not causal proof ([Spotify methodology](https://backstage.spotify.com/discover/blog/how-spotify-measures-the-value-of-backstage)).
- DORA finds both platform benefit and platform harm. A reader cannot cite its productivity figures while ignoring its throughput, stability, exclusivity, and independence findings.

## Community Pulse

This is a qualitative sample, not a sentiment poll. Hacker News was openly adversarial; Reddit supplied role-specific operational detail but included vendor replies; GitHub exposed concrete schema, lifecycle, and compatibility seams while over-sampling failures; practitioner blogs and conferences were more favorable but more likely to come from people whose platform survived or whose business serves platform teams. X, LinkedIn, YouTube comments, public Slack, and Discord did not yield stable, complete, date-reliable public corpora, so they are not used for load-bearing claims.

### Where the conversation lives

| Venue | Sampled activity | Dominant frame |
|---|---|---|
| Hacker News | Active; seven retrieved threads and roughly 120 top-level comments | Abstraction tax, organizational bottlenecks, category skepticism, and MCP security |
| Reddit | Heavy; more than ten threads across DevOps, SRE, platform, LocalLLaMA, and Claude communities | Build versus buy, Backstage TCO, “Spotify-sized” fit, gateway complexity, and promised versus actual self-service |
| GitHub | Active; more than a dozen issues/proposals | Deletion, ownership, auth, discovery, configuration portability, provider compatibility, and telemetry complexity |
| Practitioner blogs | Active but selective | Platform as product, escape paths, responsibility by layer, adoption, and support cost |
| Conference/video pages | Active and advocacy-heavy | Economic proof, standards versus autonomy, minimum viable scope, and platform-as-product |

### Ordinary and hands-on engineers

These comments carry the most direct operating texture, but their authors and experiences are not independently representative.

> “Bad platforms narrow possibilities.”
>
> — `BlackFly`, platform-team engineer, [Hacker News, 2023-06-25](https://news.ycombinator.com/item?id=36465932)

> “another tool getting in between the devs and the work”
>
> — `NormalUserThirty`, [Reddit, 2023-07-28](https://www.reddit.com/r/devops/comments/15bke0w/anyone_considered_backstageio_but_decided/)

> “it has many bugs and it's really over-complicated”
>
> — `sammcj`, describing gateway use with clients, [Reddit, 2025-05-14](https://www.reddit.com/r/LocalLLaMA/comments/1kmragz/are_you_using_ai_gateway_in_your_genai_stack/)

> “treating MCP manifests like deploy artifacts, not config”
>
> — `jake_that_dude`, [Reddit, 2026-06-02](https://www.reddit.com/r/ClaudeAI/comments/1tuqqpn/i_ship_ai_agents_in_production_the_mess_is_mcp/)

> “Most of the implementations, including my toy ones, do not have any auditing or metrics”
>
> — `neomantra`, [Hacker News, 2025-04-06](https://news.ycombinator.com/item?id=43600927)

The sampled range runs from strong support for self-service APIs, through a large skeptical-but-engaged cluster, to a loud minority hostile to “platform engineering” as a renamed silo. Confusion is frequent: “platform,” “portal,” “gateway,” “control plane,” “IDP,” and “MCP server” are often treated as if the noun already settled ownership.

### Maintainers and direct implementers

> “Configuration of the collector is a major barrier to entry for users.”
>
> — `djaglowski`, OpenTelemetry maintainer, [GitHub, 2023-09-06](https://github.com/open-telemetry/opentelemetry-collector/issues/8372)

> “Today every MCP client invents its own format for server configuration”
>
> — `BobDickinson`, MCP contributor, [GitHub, 2026-04-22](https://github.com/modelcontextprotocol/modelcontextprotocol/pull/2633)

> “Taking too long for the registered entity to show up in the catalog. sometimes from hours to days to never.”
>
> — `dayadev`, Backstage adopter, [GitHub, 2022-09-23](https://github.com/backstage/backstage/issues/13834)

These voices identify the platform's real product: templates, compatibility, lifecycle, authorization, freshness, migration, and repair—not the initial API.

### Executives, consultants, founders, and vendors

Their advice is useful but carries a stake distinct from ordinary users.

> “platforms must be compelling to use, they cannot stand on a mandate alone”
>
> — Evan Bottcher, independent technology leader, [2018-03-05](https://martinfowler.com/articles/talk-about-platforms.html)

> “all engineers run the code they write—but we divide the areas of responsibility by layer or function”
>
> — Charity Majors, Honeycomb co-founder, [2022-09-30](https://charity.wtf/p/the-future-of-ops-is-platform-engineering)

> “every dollar spent on a platform engineer is a dollar you can't spend on delivering features”
>
> — Brian Guthrie, then Orgspace co-founder and CTO, [2022-06-10](https://2022.platformcon.com/talk/is-the-optimal-size-of-a-platform-team-zero)

### Jokes, confusions, and silence

The dominant joke is recursive abstraction: “Just one more YAML bro I swear trust me bro” (`peterldowns`, [2025-04-10](https://news.ycombinator.com/item?id=43646930)). MCP security is summarized with “stolen from IoT” (`867-5309`, [2025-04-06](https://news.ycombinator.com/item?id=43600421)). The jokes encode two beliefs: platforms often add a configuration layer instead of retiring one, and agent connectivity is outrunning trust.

The most consequential misreadings are:

- Backstage is a framework for building a portal, not an install-and-forget portal.
- A portal can present links without owning delivery; a platform can own delivery without a portal.
- Self-service means the user can execute, not that support disappears.
- An MCP server runs code and shares model context; it is not harmless metadata plumbing.
- A gateway centralizes access but does not make provider APIs semantically interchangeable.

Conspicuously underrepresented are ordinary application engineers who use but did not choose the platform, regulated-industry engineers able to discuss audit and segregation of duties, teams that quietly abandoned a platform, finance/procurement/support owners, and maintainers of abandoned third-party plugins and MCP servers. Their absence likely biases public evidence toward polished success and visible failure, while daily accommodation work remains private.

## Scenarios

The scenarios describe the dominant organizational pattern by 2027-07-30. The percentages are subjective, sum to 100%, and expose assumptions rather than simulate precision.

### Base — The thin federated spine wins

**Probability:** **Plausible — 50%.**

**Trigger conditions:** By 2027-07-30, at least two of AWS, Microsoft, and Google support current MCP, A2A, and OpenTelemetry interchange while differentiating on managed identity, memory, policy, evaluation, and runtime; published enterprise cases more often extend existing catalogues than create separate authoritative agent catalogues; platform scorecards add task success, exception time, and switching cost.

**Leading indicators:** MCP conformance coverage, A2A signed-card use, stable OpenTelemetry evaluation fields, evidence export, Backstage integrations, documented escape paths, and completed portability drills.

**Rationale and effects:** Connection and telemetry standards are converging, while DORA and practitioner evidence favor extensible paved roads over comprehensive mandates. Platform teams become stewards of contracts and cross-cutting controls; domain teams retain judgment and on-call accountability. Vendor suites remain important but cannot fully dictate the internal contract ([MCP roadmap](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/); [DORA](https://dora.dev/capabilities/platform-engineering/)).

### Upside — Open evidence makes exit routine

**Probability:** **Modest — 20%.**

**Trigger conditions:** By 2027-07-30, three major platforms import and export the same agent identity metadata, trace context, and evaluation envelope without proprietary changes to domain code; two public production cases preserve authorization and audit continuity across runtime moves; procurement requires executable portability tests rather than check-box MCP/A2A support.

**Leading indicators:** Stable GenAI semantic conventions, cross-vendor A2A tests, signed provenance, provider-neutral evaluation records, contract tests in CI, and procurement clauses for export and deletion.

**Rationale and effects:** MCP trace propagation, A2A signed cards, and OpenTelemetry evaluation events provide ingredients, but identity authority and policy semantics are immature. If they mature, smaller suppliers and internal teams gain bargaining power, and the platform can stay thin because assurance travels with the workflow ([A2A](https://a2a-protocol.org/latest/specification/); [OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/); [NIST standards initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)).

### Downside — The gateway becomes the platform, then the bottleneck

**Probability:** **Modest — 25%.**

**Trigger conditions:** By 2027-07-30, proprietary gateway, identity, memory, or evaluation resources become prerequisites for important vendor features; one representative workflow cannot migrate or receive an exception without central/vendor intervention; adoption grows while task success, throughput, stability, or satisfaction falls and bypasses increase.

**Leading indicators:** Proprietary extensions, gateway-held workflow state, non-exportable evaluation history, growing exception lead time, platform on-call growth, local side gateways, and common-mode incidents.

**Rationale and effects:** All three major clouds already bundle most agent-lifecycle capabilities, and a gateway naturally attracts routing, retries, policy, memory, and orchestration. Audit coverage may improve first; later, product teams lose debugging context, central support expands, and exit requires migrating identity, evidence, policy, memory, and runtime—not just endpoints ([AWS AgentCore](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway.html); [Microsoft Foundry](https://learn.microsoft.com/en-gb/azure/ai-foundry/agents/overview?context=%2Fazure%2Fai-studio%2Fcontext%2Fcontext&view=foundry-classic); [Google](https://cloud.google.com/blog/products/ai-machine-learning/the-new-gemini-enterprise-one-platform-for-agent-development)).

### Wildcard — Verifiable delegated authority becomes the real boundary

**Probability:** **Low — 5%.**

**Trigger conditions:** By 2027-07-30, a regulator, major procurer, or cross-industry standard requires a machine-verifiable binding among human principal, agent version, delegated scope, tool action, and retained evidence; signed Agent Cards gain interoperable authority and revocation; NIST or another body publishes a profile adopted by two major identity platforms.

**Leading indicators:** NIST identity deliverables, tamper-evident action receipts, agent-aware OAuth/OIDC profiles, on-behalf-of delegation, signed evaluation trails, and identity vendors leading agent architecture.

**Rationale and effects:** NIST asks these questions and A2A has a cryptographic foothold, but implementation is early. A high-impact incident or procurement mandate could rapidly move the platform's centre of gravity from model/runtime to identity and evidence—either increasing portability or creating an even deeper proprietary lock-in ([NIST concept paper](https://www.nccoe.nist.gov/publications/other/accelerating-adoption-software-and-ai-agent-identity-and-authorization-concept); [A2A](https://a2a-protocol.org/latest/specification/)).

## The 90-Day Signal

Run one exit drill by **2026-10-28**.

Move a representative, non-trivial workflow between two model/runtime stacks while retaining the same domain tool implementations. Preserve least-privilege identity, approval behavior, MCP/A2A interfaces where applicable, the evaluation dataset, and end-to-end OpenTelemetry evidence.

Measure one composite signal: **the percentage of the workflow's operational contract that survives unchanged**—tool schemas, identity/delegation scope, policy inputs, evaluation cases/results, trace fields, ownership metadata, and incident runbook.

- **Thin-boundary signal:** at least 80% survives unchanged, domain code changes no more than 20%, and the move takes no more than five engineer-days.
- **Thick-boundary signal:** credentials, policies, evaluation history, trace meaning, approval flow, or catalogue state must be reconstructed manually, even if the MCP endpoint still works.

These are proposed organizational thresholds, not industry benchmarks. The drill is more informative than a feature inventory because it measures exit rather than advertised compatibility.

## Watch List

These are the observable developments most likely to move the proposed boundary:

1. **MCP core conformance:** independent results showing which clients, servers, gateways, and extensions actually interoperate against the current specification—not SDK download counts alone ([MCP specification](https://modelcontextprotocol.io/specification/2026-07-28)).
2. **MCP enterprise operation:** portable server configuration, identity, audit, revocation, and telemetry practices that remove the current client-by-client and gateway-by-gateway variation ([MCP roadmap](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/)).
3. **Protocol extension sprawl:** growth in provider-specific MCP or A2A extensions that makes nominal interoperability depend on one host or cloud.
4. **Registry trust:** provenance, publisher verification, ownership transfer, vulnerability handling, freshness, and removal behavior in public and private tool registries.
5. **A2A authority:** production use of signed Agent Cards, delegated scopes, revocation, and verifiable task history rather than discovery-only cards ([A2A](https://a2a-protocol.org/latest/specification/)).
6. **The A2A/MCP seam:** stable practice for deciding when an actor is an agent with task lifecycle versus a tool with a callable capability, including who carries authorization and on-call.
7. **Agent identity standards:** NIST profiles, OAuth/OIDC work, or procurement requirements that bind human principal, agent version, delegated authority, resource, and action ([NIST initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)).
8. **Evaluation portability:** NIST AI 800-2 and independent cases showing datasets, evaluator versions, lineage, raw results, and release decisions moving between harnesses ([NIST](https://www.nist.gov/news-events/news/2026/01/towards-best-practices-automated-benchmark-evaluations)).
9. **OpenTelemetry stability:** stable GenAI and evaluation semantic conventions with demonstrated cross-vendor export and manageable cardinality ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/)).
10. **Evidence privacy:** incident reports, regulator guidance, or engineering patterns for redacting, regionally storing, retaining, and deleting prompt and tool telemetry.
11. **EU enforcement:** how Commission enforcement of GPAI obligations from 2026-08-02 allocates evidence duties in real provider/deployer arrangements ([European Commission](https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers)).
12. **Existing-platform integration:** production cases in which agent metadata and machine interfaces extend IAM, delivery, observability, and catalogues without creating a second source of truth.
13. **Gateway scope creep:** rising counts of stateful workflow, memory, policy, evaluation, or orchestration features—and the corresponding exception and on-call load—in gateway products.
14. **Build-versus-buy TCO:** published cases that include central headcount, exported product-team labor, support, incidents, committed spend, migration, dual-run, and retirement, not only infrastructure price.
15. **Tool-discovery scaling:** evidence that catalogues improve correct tool selection without putting stale declarations in the authorization path.
16. **Outcome scorecards:** platform teams reporting task success, lead time, exception latency, throughput, change stability, incidents, total labor, voluntary retention, and switching time alongside adoption.

## Tensions and Open Questions

1. **Scale threshold:** How many genuinely similar teams, workflows, or controls justify shared runtime ownership rather than a shared contract? Uber and Google prove the threshold can exist; they do not locate it for a normal organization.
2. **Risk threshold:** Which actions require a mandatory, non-bypassable enforcement point, and which can rely on admission-time evidence plus local operation?
3. **Total work:** Can the organization measure central labor, exported product-team labor, support, exceptions, rework, incidents, migration, and exit in one model?
4. **Authority versus operation:** Who sets policy, who supplies the enforcement point, who accepts residual risk, and who can reverse the decision?
5. **Truth versus display:** Which facts belong near the workflow, in IAM, in a risk register, or in observed telemetry—and which are merely cached in a catalogue?
6. **Gateway semantics:** Which provider differences must remain explicit rather than normalized away? How quickly does compatibility work grow as providers change?
7. **Identity chain:** How are human principal, agent version, delegated scope, resource action, approval, and revocation bound into one auditable event?
8. **Evaluation ownership:** Which baseline suites can be shared without converting contextual judgment into a generic score?
9. **Privacy of evidence:** What prompts, tool arguments, results, and identities may be captured, in which regions, for how long, and by whom?
10. **Exception economics:** How long does an exceptional team wait, how often are exceptions renewed, and when does a paved road become a gate?
11. **On-call fit:** Can the proposed owner meet SLO, staffing, diagnostic access, and toil constraints, and can it hand the service back?
12. **Exit credibility:** Can the organization migrate the operational contract—not only the API—without reconstructing policy, identity, evaluation, and evidence?

The single evidence item that would most change this dossier is a multi-organization, longitudinal matched comparison of contract-only, central-runtime, federated, and vendor-managed implementations, stratified by scale and risk, publishing both platform and product-team labor, delivery outcomes, incidents, exception latency, audit findings, switching time, and decommissioning cost. Nothing in the current public record meets that bar.

## Decision Rules and Proposed Stopping Test

For an organization that has **not yet demonstrated** enough repeated runtime demand, pooled-capacity advantage, global-consistency need, or regulated-evidence benefit, use a thin contract plus existing enterprise platforms as a **starting hypothesis**, not a universal default. The hypothesis is falsifiable capability by capability: broaden shared implementation when a measured pilot shows that central operation retires more total work and risk, or supplies capacity, consistency, or evidence that distributed owners cannot provide at comparable reliability and cost. Uber's Michelangelo, Google's TFX, Borg, and Zanzibar are scale counterexamples to indiscriminate thinness; they show that broad integration can be correct when repeated demand, pooled infrastructure, or globally consistent control is real and large enough ([Uber](https://www.uber.com/gb/en/blog/michelangelo-machine-learning-platform/); [TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/); [Borg](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/); [Zanzibar](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)). They do not establish that every organization has crossed those thresholds.

For organizations still inside that scoped hypothesis, add a shared implementation only when the evidence for that capability passes all of these tests:

1. **Repeated constraint:** at least several teams face substantially the same problem, or one organization-wide obligation must be enforced. “Several” is an internal pilot threshold to define, not an industry constant.
2. **Net-work test:** the repeated work and unmanaged risk retired exceed platform build, operation, product-team integration, support, exception, migration, and exit work.
3. **Stable-semantics test:** the shared part is actually common. Domain meaning that changes with one workflow remains local.
4. **Authority test:** policy owner, schema owner, source of truth, enforcement point, operator, support owner, risk acceptor, and funding owner are separately named.
5. **Action-boundary test:** any mandatory guarantee is enforced where a bypass cannot avoid it; metadata and catalogue fields are not treated as proof.
6. **Self-service test:** the consuming team can complete and diagnose the normal path without a ticket or privileged meeting.
7. **Exception test:** a legitimate exception has a named decider, service level, compensating control, expiry, and observable path.
8. **Operations test:** the proposed owner accepts the SLO, telemetry, staffing, pager, incident command, and handback rule. Google SRE's 50% toil cap is a useful external warning line, not a universal local policy ([Google SRE](https://sre.google/sre-book/eliminating-toil/)).
9. **Existing-system test:** the capability cannot be supplied more cheaply by extending IAM, CI/CD, observability, catalogue, data, security, or FinOps systems already in place.
10. **Exit test:** a second implementation can consume the contract; evidence and configuration export; dual running is possible; deprecation and removal are funded.

**Within that scope, stop expanding the shared layer at the first test it fails; when the scale, consistency, capacity, or evidence conditions are demonstrated, expansion may be the correct result.** Move inward when a guarantee requires shared runtime mediation, and move outward again when measured value no longer exceeds ownership cost. A useful scorecard combines task success, lead time for normal and exceptional work, throughput, change stability, incidents, platform and exported labor, voluntary retention, local bypasses, cost per governed outcome, and switching time. Adoption, entity count, gateway traffic, or feature count alone cannot distinguish a paved road from a golden cage.

## Receipts

### Primary specifications, standards, law, and regulator records

- [MCP specification 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28)
- [MCP 2026-07-28 changelog](https://modelcontextprotocol.io/specification/2026-07-28/changelog)
- [MCP authorization specification 2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization)
- [MCP tool specification](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)
- [A2A specification](https://a2a-protocol.org/latest/specification/)
- [OpenTelemetry GenAI observability](https://opentelemetry.io/blog/2026/genai-observability/)
- [Backstage Software Catalogue](https://backstage.io/docs/features/software-catalog/)
- [Backstage catalogue graph and source-of-truth guidance](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)
- [Open Policy Agent management architecture](https://www.openpolicyagent.org/docs/management-introduction)
- [OpenAPI Specification](https://spec.openapis.org/oas/)
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)
- [NIST agent identity concept paper](https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents)
- [NCCoE agent identity and authorization concept paper](https://www.nccoe.nist.gov/publications/other/accelerating-adoption-software-and-ai-agent-identity-and-authorization-concept)
- [NIST AI Agent Standards Initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)
- [NIST automated benchmark evaluation draft announcement](https://www.nist.gov/news-events/news/2026/01/towards-best-practices-automated-benchmark-evaluations)
- [Regulation (EU) 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)
- [European Commission AI Act navigation](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)
- [European Commission GPAI provider guidance](https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers)
- [EDPB Opinion 28/2024](https://www.edpb.europa.eu/documents/opinion-of-the-board-art-64/opinion-282024-on-certain-data-protection-aspects-related-to_en)
- [EU Data Act explanation](https://digital-strategy.ec.europa.eu/en/factpages/data-act-explained)
- [UK CMA cloud-services market investigation](https://www.gov.uk/cma-cases/cloud-services-market-investigation)
- [UK CMA provisional findings, 2025-01-28](https://www.gov.uk/government/news/cma-independent-inquiry-group-publishes-provisional-findings-in-cloud-services-market-investigation)
- [US DOJ CLOUD Act white paper](https://www.justice.gov/archives/opa/press-release/file/1153446/dl?inline=)
- [SEC Knight Capital order](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf)

### Research and industry studies

- [2024 DORA report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)
- [DORA platform-engineering guidance](https://dora.dev/capabilities/platform-engineering/)
- [MLOps architecture systematic mapping study](https://arxiv.org/abs/2406.19847)
- [TFX production-scale ML platform paper](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/)
- [Borg cluster-management paper](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/)
- [Zanzibar global authorization paper](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)
- [Enterprise MCP interview preprint](https://arxiv.org/abs/2606.09182)
- [2025 State of FinOps](https://data.finops.org/2025-report/)
- [FinOps shared-cost allocation](https://www.finops.org/wg/cloud-cost-allocation/)
- [2025 Stack Overflow AI survey](https://survey.stackoverflow.co/2025/ai)
- [Census II of Free and Open Source Software](https://lish.harvard.edu/publications/census-ii-free-and-open-source-software-%E2%80%94-application-libraries)

### Primary company cases and incident records

- [AWS EC2 beta announcement, 2006-08-24](https://aws.amazon.com/about-aws/whats-new/2006/08/24/announcing-amazon-elastic-compute-cloud-amazon-ec2---beta/)
- [Uber Michelangelo](https://www.uber.com/gb/en/blog/michelangelo-machine-learning-platform/)
- [Uber's current AI platform](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/)
- [Spotify opens Backstage](https://backstage.io/blog/2020/03/18/what-is-backstage/)
- [Spotify: coding is no longer the constraint, 2026-06-03](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint)
- [Spotify Backstage measurement methodology](https://backstage.spotify.com/discover/blog/how-spotify-measures-the-value-of-backstage)
- [Kubernetes 1.24 dockershim removal](https://kubernetes.io/blog/2022/05/03/kubernetes-1-24-release-announcement/)
- [GOV.UK PaaS decommissioning decision, 2022-07-12](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)
- [CNCF platforms white paper announcement, 2023-04-11](https://www.cncf.io/blog/2023/04/11/announcing-a-white-paper-on-platforms-for-cloud-native-computing/)
- [MCP launch, 2024-11-25](https://www.anthropic.com/news/model-context-protocol)
- [MCP joins AAIF, 2025-12-09](https://blog.modelcontextprotocol.io/posts/2025-12-09-mcp-joins-agentic-ai-foundation/)
- [Linux Foundation A2A adoption announcement, 2026-04-09](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year)
- [MCP 2026 roadmap](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/)
- [GitLab database outage](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)
- [Amazon S3 service disruption](https://aws.amazon.com/message/41926/)
- [Cloudflare outage on 2019-07-02](https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/)
- [GitHub stolen OAuth token alert](https://github.blog/news-insights/company-news/security-alert-stolen-oauth-user-tokens/)
- [Codecov Bash Uploader postmortem](https://about.codecov.io/apr-2021-post-mortem/)

### Expert and practitioner guidance

- [CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/)
- [Mind the platform execution gap](https://martinfowler.com/articles/platform-prerequisites.html)
- [What I Talk About When I Talk About Platforms](https://martinfowler.com/articles/talk-about-platforms.html)
- [How platform teams get stuff done](https://martinfowler.com/articles/platform-teams-stuff-done.html)
- [Google SRE: Eliminating Toil](https://sre.google/sre-book/eliminating-toil/)
- [Google SRE workbook: On-Call](https://sre.google/workbook/on-call/)
- [Google SRE: Evolving Engagement Model](https://sre.google/sre-book/evolving-sre-engagement-model/)
- [Google SRE workbook: Team Lifecycles](https://sre.google/workbook/team-lifecycles/)
- [The Future of Ops is Platform Engineering](https://charity.wtf/p/the-future-of-ops-is-platform-engineering)
- [PlatformCon: Is the optimal size of a platform team zero?](https://2022.platformcon.com/talk/is-the-optimal-size-of-a-platform-team-zero)

### Community and issue trackers

- [Hacker News: How platform engineering works](https://news.ycombinator.com/item?id=36465220)
- [Hacker News comment: “Bad platforms narrow possibilities”](https://news.ycombinator.com/item?id=36465932)
- [Hacker News: MCP security](https://news.ycombinator.com/item?id=43600192)
- [Hacker News comment: MCP compared with IoT](https://news.ycombinator.com/item?id=43600421)
- [Hacker News comment: MCP auditing and metrics](https://news.ycombinator.com/item?id=43600927)
- [Hacker News comment: “Just one more YAML”](https://news.ycombinator.com/item?id=43646930)
- [Reddit: Backstage considered and rejected/adopted](https://www.reddit.com/r/devops/comments/15bke0w/anyone_considered_backstageio_but_decided/)
- [Reddit: AI gateway use](https://www.reddit.com/r/LocalLLaMA/comments/1kmragz/are_you_using_ai_gateway_in_your_genai_stack/)
- [Reddit: production MCP governance](https://www.reddit.com/r/ClaudeAI/comments/1tuqqpn/i_ship_ai_agents_in_production_the_mess_is_mcp/)
- [Backstage issue #13834](https://github.com/backstage/backstage/issues/13834)
- [OpenTelemetry Collector issue #8372](https://github.com/open-telemetry/opentelemetry-collector/issues/8372)
- [MCP client-configuration proposal](https://github.com/modelcontextprotocol/modelcontextprotocol/pull/2633)

### Vendor and background material

- [AWS AgentCore overview](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/)
- [AWS AgentCore Gateway](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway.html)
- [Microsoft Foundry Agent Service](https://learn.microsoft.com/en-gb/azure/ai-foundry/agents/overview?context=%2Fazure%2Fai-studio%2Fcontext%2Fcontext&view=foundry-classic)
- [Google Gemini Enterprise Agent Platform](https://cloud.google.com/blog/products/ai-machine-learning/the-new-gemini-enterprise-one-platform-for-agent-development)
- [Azure AI Gateway](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)
- [AWS Bedrock pricing](https://aws.amazon.com/bedrock/pricing/)
- [OpenAI API pricing](https://openai.com/api/)
- [Microsoft Azure data residency](https://azure.microsoft.com/en-us/explore/global-infrastructure/data-residency/)
- [GitHub deployment environments](https://docs.github.com/en/actions/reference/workflows-and-actions/deployments-and-environments)

### Additional complete angle receipts

The following receipts complete the unique URL union from the history, mechanism, stakeholder, contrarian, futures, and community research files. They are ordered by source host; the analytically central sources remain classified above.

- [PlatformCon: Don't build a platform, be a platform](https://2025.platformcon.com/sessions/don-t-build-a-platform-be-a-platform)
- [PlatformCon: Standards spare your sanity](https://2025.platformcon.com/sessions/standards-spare-your-sanity)
- [NIST AI RMF actor tasks](https://airc.nist.gov/airmf-resources/airmf/appendices/app-a-descriptions-of-ai-actor-tasks/)
- [Argo CD automated sync](https://argo-cd.readthedocs.io/en/latest/user-guide/auto_sync/)
- [Argo CD sync options](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-options/)
- [Tidelift State of the Open Source Maintainer report](https://assets-eu-01.kc-usercontent.com/ef593040-b591-0198-9506-ed88b30bc023/d325a56f-05be-4379-bfd1-ee4776fcad41/2024-tidelift-state-of-the-open-source-maintainer-report-.pdf)
- [AWS AgentCore Gateway MCP support, 2026-06-01](https://aws.amazon.com/blogs/machine-learning/extending-mcp-support-for-amazon-bedrock-agentcore-gateway-2/)
- [AWS digital-sovereignty controls](https://aws.amazon.com/compliance/digital-sovereignty/)
- [Azure OpenAI pricing](https://azure.microsoft.com/en-us/pricing/details/azure-openai/)
- [Backstage source-code audit](https://backstage.io/assets/files/X41-Backstage-Audit-2024-eb8535297d6f2542b0d61bf73c87f7fc.pdf)
- [Backstage backend system alpha](https://backstage.io/blog/2023/02/15/backend-system-alpha/)
- [Backstage ADR002 default catalogue file format](https://backstage.io/docs/architecture-decisions/adrs-adr002/)
- [Backstage external integrations](https://backstage.io/docs/features/software-catalog/external-integrations/)
- [Backstage entity lifecycle](https://backstage.io/docs/features/software-catalog/life-of-an-entity/)
- [Backstage descriptor format](https://backstage.io/docs/next/features/software-catalog/descriptor-format/)
- [Google Cloud Golden Paths](https://cloud.google.com/blog/products/application-development/golden-paths-for-engineering-execution-consistency)
- [Google platform-engineering control taxonomy](https://cloud.google.com/blog/products/application-modernization/platform-engineering-control-mechanisms)
- [Google Cloud 2024 DORA report announcement](https://cloud.google.com/blog/products/devops-sre/announcing-the-2024-dora-report?hl=en)
- [Google Cloud platform engineering](https://cloud.google.com/solutions/platform-engineering)
- [Google Vertex AI pricing](https://cloud.google.com/vertex-ai/generative-ai/pricing)
- [Production MCP: A Practitioner's Guide](https://davidgolverdingen.nl/en/insights/production-mcp-practitioners-guide)
- [DEV Community: What are Golden Paths in platform engineering?](https://dev.to/cyclops-ui/what-are-golden-paths-in-platform-engineering-3m20)
- [DEV Community: Pave Golden Paths with platform engineering](https://dev.to/mia-platform/pave-golden-paths-with-platform-engineering-33g1)
- [European Commission GPAI fact page](https://digital-strategy.ec.europa.eu/en/factpages/general-purpose-ai-obligations-under-ai-act)
- [EU AI Office frontier-AI findings, 2026-07-15](https://digital-strategy.ec.europa.eu/en/library/ai-office-publishes-frontier-ai-expert-findings-eu-competitiveness-sovereignty-and-security)
- [AI Omnibus, 2026-07-27](https://digital-strategy.ec.europa.eu/en/news/ai-omnibus-enters-force)
- [European Commission Article 50 guidance](https://digital-strategy.ec.europa.eu/lt/node/17077)
- [AWS Bedrock security](https://docs.aws.amazon.com/bedrock/latest/userguide/security.html)
- [AWS shared-responsibility model](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/shared-responsibility.html)
- [Google Cloud architecture for deploying and operating generative-AI applications](https://docs.cloud.google.com/architecture/deploy-operate-generative-ai-applications)
- [Google Assured Workloads data residency](https://docs.cloud.google.com/assured-workloads/docs/data-residency)
- [Google Agent Engine identity](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/set-up)
- [DORA 2024 report page](https://dora.dev/research/2024/dora-report/)
- [Spotify Golden Paths](https://engineering.atspotify.com/2020/08/how-we-use-golden-paths-to-solve-fragmentation-in-our-software-ecosystem)
- [Spotify technology migrations](https://engineering.atspotify.com/2020/6/tech-migrations-the-spotify-way)
- [Spotify DevOps productivity](https://engineering.atspotify.com/2020/8/how-we-improved-developer-productivity-for-our-devops-teams)
- [Spotify: Backstage grows up](https://engineering.atspotify.com/2021/03/happy-birthday-backstage-spotifys-biggest-open-source-project-grows-up-fast)
- [Spotify: five years of Backstage](https://engineering.atspotify.com/2025/04/celebrating-five-years-of-backstage)
- [EUR-Lex Data Act Article 29](https://eur-lex.europa.eu/legal-content/EN/TXT/?qid=1717081446388&uri=CELEX%3A32023R2854)
- [Backstage issue #13891](https://github.com/backstage/backstage/issues/13891)
- [Backstage issue #25622](https://github.com/backstage/backstage/issues/25622)
- [Backstage: modelling MCP servers in the catalogue](https://github.com/backstage/backstage/issues/32062)
- [Backstage issue #3750](https://github.com/backstage/backstage/issues/3750)
- [Backstage issue #3750 comment, 2021-03-18](https://github.com/backstage/backstage/issues/3750#issuecomment-802257555)
- [LiteLLM issue #26476, 2026-04-25](https://github.com/BerriAI/litellm/issues/26476)
- [LiteLLM issue #32031, 2026-07-03](https://github.com/BerriAI/litellm/issues/32031)
- [LiteLLM MCP permission re-grant issue](https://github.com/BerriAI/litellm/issues/33397)
- [Kubernetes Inference Extension](https://github.com/kubernetes-sigs/gateway-api-inference-extension)
- [MCP pre-auth resource discovery issue](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/540)
- [MCP pre-auth resource discovery comment, 2025-05-20](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/540#issuecomment-2895776478)
- [Flexera 2025 State of the Cloud report page](https://info.flexera.com/CM-REPORT-State-of-the-Cloud-AWS)
- [Zillow 2023 annual report](https://investors.zillowgroup.com/files/doc_financials/2023/ar/zillow-group-inc-_annual_report_2023.pdf)
- [Zillow operational update](https://investors.zillowgroup.com/investors/news-and-events/news/news-details/2021/At-Operational-Capacity-Zillow-Offers-to-Focus-on-Signed-Customer-Contracts-and-Current-Inventory-Suspends-Signing-of-New-Contracts-Through-2021/default.aspx)
- [JSON Schema metadata](https://json-schema.org/understanding-json-schema/reference/metadata)
- [Kubernetes dockershim FAQ](https://kubernetes.io/blog/2022/02/17/dockershim-faq/)
- [Kubernetes dockershim history](https://kubernetes.io/blog/2022/05/03/dockershim-historical-context/)
- [Kubernetes cloud-provider integration changes](https://kubernetes.io/blog/2023/12/14/cloud-provider-integration-changes/)
- [Kubernetes components](https://kubernetes.io/docs/concepts/overview/components/)
- [Kubernetes cloud-controller administration](https://kubernetes.io/docs/tasks/administer-cluster/running-cloud-controller/)
- [Azure gateway reference architecture](https://learn.microsoft.com/en-us/ai/playbook/solutions/genai-gateway/reference-architectures/apim-based)
- [Microsoft hosted agents](https://learn.microsoft.com/en-us/azure/foundry/agents/concepts/hosted-agents)
- [MCP governance](https://modelcontextprotocol.io/community/governance)
- [MCP architecture documentation](https://modelcontextprotocol.io/docs/learn/architecture)
- [MCP security best practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)
- [MCP 2025-06-18 architecture](https://modelcontextprotocol.io/specification/2025-06-18/architecture/index)
- [MCP 2025-06-18 authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)
- [MCP 2025-11-25 tool schema](https://modelcontextprotocol.io/specification/2025-11-25/schema)
- [Hacker News: Backstage discussion](https://news.ycombinator.com/item?id=26935504)
- [Hacker News: Backstage comment #26939387](https://news.ycombinator.com/item?id=26939387)
- [Hacker News: Backstage comment #26939491](https://news.ycombinator.com/item?id=26939491)
- [Hacker News: DevOps, SRE, and Platform Engineering](https://news.ycombinator.com/item?id=28137852)
- [Hacker News platform-engineering comment, 2021-08-11](https://news.ycombinator.com/item?id=28138594)
- [Hacker News platform-engineering comment #36465591, 2023-06-25](https://news.ycombinator.com/item?id=36465591)
- [Hacker News platform-engineering comment #36465746, 2023-06-25](https://news.ycombinator.com/item?id=36465746)
- [Hacker News platform-engineering comment #36467011, 2023-06-25](https://news.ycombinator.com/item?id=36467011)
- [Hacker News: Myths about platform engineering](https://news.ycombinator.com/item?id=40531258)
- [Hacker News platform-engineering comment #40532587, 2024-05-31](https://news.ycombinator.com/item?id=40532587)
- [Hacker News platform-engineering comment #40533670, 2024-05-31](https://news.ycombinator.com/item?id=40533670)
- [Hacker News MCP comment #43600428, 2025-04-06](https://news.ycombinator.com/item?id=43600428)
- [Hacker News MCP comment #43600527, 2025-04-06](https://news.ycombinator.com/item?id=43600527)
- [Hacker News: Show HN Koreo](https://news.ycombinator.com/item?id=43644351)
- [Hacker News Koreo comment #43647021, 2025-04-10](https://news.ycombinator.com/item?id=43647021)
- [Hacker News: Show HN MCP-Shield](https://news.ycombinator.com/item?id=43689178)
- [Hacker News: Show HN MCP Security Suite](https://news.ycombinator.com/item?id=44904974)
- [NIST AI RMF 1.0](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf)
- [OpenTelemetry AI-agent observability](https://opentelemetry.io/blog/2025/ai-agent-observability/)
- [OpenTelemetry signals](https://opentelemetry.io/docs/concepts/signals/)
- [OpenTelemetry baggage](https://opentelemetry.io/docs/concepts/signals/baggage/)
- [OpenTelemetry traces](https://opentelemetry.io/docs/concepts/signals/traces/)
- [OpenTelemetry status](https://opentelemetry.io/docs/specs/status/)
- [Riehle et al., Inner Source in Platform-Based Product Engineering](https://oss.cs.fau.de/2015/05/23/inner-source-in-platform-based-product-engineering/)
- [Google Research: Hidden Technical Debt in Machine Learning Systems](https://research.google/pubs/hidden-technical-debt-in-machine-learning-systems/)
- [Google Research: Machine Learning—The High Interest Credit Card of Technical Debt](https://research.google/pubs/machine-learning-the-high-interest-credit-card-of-technical-debt/)
- [Google Research: What Predicts Software Developers' Productivity?](https://research.google/pubs/what-predicts-software-developers-productivity/)
- [Slack Engineering: Technology lifecycle](https://slack.engineering/technology-lifecycle/)
- [Google SRE books and workbook](https://sre.google/)
- [Google SRE: Being On-Call](https://sre.google/sre-book/being-on-call/)
- [Google SRE: Dealing with Interrupts](https://sre.google/sre-book/dealing-with-interrupts/)
- [Stack Overflow 2025 Developer Survey announcement](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/)
- [Spotify five years of Backstage, staging URL](https://stage.engineering.atspotify.com/2025/4/celebrating-five-years-of-backstage)
- [Stack Overflow 2025 survey overview](https://survey.stackoverflow.co/2025/)
- [Stack Overflow 2025 work results](https://survey.stackoverflow.co/2025/work)
- [CNCF platform-engineering maturity model](https://tag-app-delivery.cncf.io/whitepapers/platform-eng-maturity-model/)
- [Team Topologies: Thinnest Viable Platform](https://teamtopologies.com/key-concepts-content/what-is-a-thinnest-viable-platform-tvp)
- [Meltwater: Centralizing Developer Docs in Backstage](https://underthehood.meltwater.com/blog/2022/07/19/centralizing-developer-docs-in-backstage/)
- [Anthropic list prices](https://www-cdn.anthropic.com/files/4zrzovbb/website/3684c2faafb97418665782cea0001f439f74b1d2.pdf)
- [Twelve-Factor App](https://www.12factor.net/)
- [CNCF platform-engineering maturity-model announcement](https://www.cncf.io/blog/2023/11/20/announcing-the-platform-engineering-maturity-model/)
- [EDPB Opinion 28/2024 announcement, 2024-12-18](https://www.edpb.europa.eu/news/edpb-opinion-on-ai-models-gdpr-principles-support-responsible-ai_en)
- [FinOps shared-platform case](https://www.finops.org/assets/fair-cost-allocation-in-a-shared-platform-as-a-service/)
- [FinOps terminology](https://www.finops.org/assets/terminology/)
- [Flexera State of the Cloud press release](https://www.flexera.com/about-us/press-center/new-flexera-report-finds-84-percent-of-organizations-struggle-to-manage-cloud-spend)
- [US DOJ CLOUD Act executive-agreement process](https://www.justice.gov/criminal/criminal-oia/regarding-cloud-act-executive-agreements)
- [Linux Foundation January 2025 newsletter](https://www.linuxfoundation.org/blog/linux-foundation-newsletter-january-2025?hs_amp=true)
- [Linux Foundation Agentic AI Foundation announcement](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation?hs_amp=true)
- [Microsoft Research: The SPACE of Developer Productivity](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/)
- [Microsoft MCP security and governance, 2026-02-12](https://www.microsoft.com/insidetrack/blog/protecting-ai-conversations-at-microsoft-with-model-context-protocol-security-and-governance/)
- [Nick McKenzie: Backstage](https://www.nickmck.net/posts/backstage)
- [NIST TEVV](https://www.nist.gov/ai-test-evaluation-validation-and-verification-tevv)
- [NIST AI Agent Standards Initiative programme](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)
- [NIST evaluation probes, updated 2026-05-05](https://www.nist.gov/programs-projects/building-evaluation-probes-agentic-ai)
- [NIST AI RMF 1.0 publication record](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10)
- [NTSB Uber ATG investigation](https://www.ntsb.gov/investigations/Pages/HWY18MH010.aspx)
- [OPA discovery](https://www.openpolicyagent.org/docs/management-discovery)
- [OPA control-plane concepts](https://www.openpolicyagent.org/docs/ocp/concepts)
- [Reddit: built and tested over 40 MCP servers](https://www.reddit.com/r/ClaudeAI/comments/1l1sgb9/ive_built_and_tested_over_40_mcp_servers_heres_my/)
- [Reddit production MCP governance comment by `jake_that_dude`](https://www.reddit.com/r/ClaudeAI/comments/1tuqqpn/comment/opcznh0/)
- [Reddit gateway experience comment by `sammcj`](https://www.reddit.com/r/LocalLLaMA/comments/1kmragz/comment/msdwh8r/)
- [Reddit managed-gateway rationale comment](https://www.reddit.com/r/LocalLLaMA/comments/1kmragz/comment/mw61nkt/)
- [Reddit: Backstage is not user-friendly](https://www.reddit.com/r/devops/comments/1171it7/backstage_is_not_userfriendly_i_want_something/)
- [Reddit Backstage usability comment by `p33k4y`](https://www.reddit.com/r/devops/comments/1171it7/comment/j99r4gj/)
- [Reddit: Backstage opportunity-cost discussion](https://www.reddit.com/r/devops/comments/15bke0w)
- [Reddit Backstage friction comment by `NormalUserThirty`](https://www.reddit.com/r/devops/comments/15bke0w/comment/jtrqo04/)
- [Reddit: platform-engineering hype](https://www.reddit.com/r/devops/comments/18fshs8/)
- [Reddit platform-engineering comment #kcwc1nx](https://www.reddit.com/r/devops/comments/18fshs8/comment/kcwc1nx/)
- [Reddit platform-engineering comment #kcxd9je](https://www.reddit.com/r/devops/comments/18fshs8/comment/kcxd9je/)
- [Reddit: Which internal developer portal should we use?](https://www.reddit.com/r/devops/comments/1dyb1f1/which_internal_developer_portal_should_we_use/)
- [Reddit portal-versus-platform comment by `oshtratn`](https://www.reddit.com/r/devops/comments/1dyb1f1/comment/lcb2wi0/)
- [Reddit IDP acronym comment by `Soverance`](https://www.reddit.com/r/devops/comments/1dyb1f1/comment/lcc2v8j/)
- [Reddit: catalogue drift as a Kubernetes lens](https://www.reddit.com/r/kubernetes/comments/1tcc53b/)
- [Reddit: custom centralized MCP gateway](https://www.reddit.com/r/mcp/comments/1rhavm1/anyone_else_building_a_centralized_mcp_gateway_to/)
- [Reddit: connect 100 MCP servers](https://www.reddit.com/r/mcp/comments/1t73igk/how_to_connect_100_mcp_servers_without_the/)
- [Reddit: LiteLLM MCP gateway boundary](https://www.reddit.com/r/mcp/comments/1uhelfu/where_do_you_draw_the_line_with_litellms_mcp/)
- [Reddit: build versus buy an MCP gateway](https://www.reddit.com/r/mcp/comments/1uokcud/build_vs_buy_on_mcp_gatewaytool_servers/)
- [Reddit: developer portals](https://www.reddit.com/r/sre/comments/194ga03/developer_portals/)
- [Reddit Backstage operating-model comment by `mithrilsoft`](https://www.reddit.com/r/sre/comments/194ga03/comment/khg84m5/)
- [Reddit: platform support](https://www.reddit.com/r/sre/comments/1fzihvl)
- [Shaun Bent: Why federated design systems keep failing](https://www.shaunbent.co.uk/blog/why-federated-design-systems-keep-failing/)
- [Thoughtworks: Incremental developer platform](https://www.thoughtworks.com/radar/techniques/incremental-developer-platform)
- [Uber GenAI Gateway](https://www.uber.com/en-AT/blog/genai-gateway/)
- [Uber Michelangelo PyML](https://www.uber.com/us/en/blog/michelangelo-pyml/)
- [USENIX: TFX industrial-scale ML](https://www.usenix.org/conference/opml19/presentation/baylor)
- [MLOps architecture research data](https://zenodo.org/records/12537232)
