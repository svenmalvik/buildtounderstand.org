# Futures: what the smallest-AI-platform decision could become

## Forward calendar

Optional per research plan; produced because regulation and already-announced model and agent-service retirements provide concrete stress tests for platform scope and portability.

| Date | Event | Why it matters |
|---|---|---|
| 2026-08-02 | The EU AI Act becomes generally applicable, including Article 50 transparency duties for providers and deployers. | Teams operating in the EU need an attributable way to implement and evidence applicable transparency controls; that can favour a narrow shared control/evidence capability without proving that a full AI platform is necessary ([European Commission](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai), [Article 50 FAQ](https://digital-strategy.ec.europa.eu/en/faqs/transparency-obligations-under-article-50-ai-act)). |
| 2026-09-15 | Microsoft Foundry schedules retirement of the listed `sora-2` preview version. | A central model contract and eval suite should make this migration cheaper; hard-coded application integrations expose whether the organisation has a repeated constraint worth sharing ([Microsoft Foundry retirement schedule](https://learn.microsoft.com/es-es/azure/foundry/openai/concepts/model-retirement-schedule)). |
| 2026-09-18 | Azure OpenAI schedules retirement of the listed `o1-pro` version. | The replacement forces teams to rerun workflow-specific evaluations rather than assume model interchangeability ([Microsoft model retirements](https://learn.microsoft.com/es-es/azure/ai-foundry/openai/concepts/model-retirements)). |
| 2026-10-02 | Azure Databricks schedules retirement of Gemini 2.5 Flash pay-per-token and provisioned-throughput serving, and Gemini 2.5 Pro provisioned throughput. | A second distribution channel retiring the same model family on a different date tests whether model lifecycle tracking belongs in each application or in one shared capability ([Azure Databricks](https://learn.microsoft.com/en-us/azure/databricks/machine-learning/retired-models-policy)). |
| 2026-10-14 | Microsoft Foundry schedules retirement of GPT-4.1, GPT-4.1 mini, and GPT-4.1 nano versions listed in its catalogue. | Coordinated migration across a model family tests routing, compatibility, eval, and communication mechanisms together ([Microsoft Foundry retirement schedule](https://learn.microsoft.com/pt-pt/azure/foundry/openai/concepts/model-retirement-schedule)). |
| 2026-10-16 | Google Cloud schedules retirement of Gemini 2.5 Pro, Flash, and Flash-Lite on Vertex AI. | The date is close to Microsoft’s model-family retirements but not identical, making provider-neutral lifecycle inventory and regression testing more valuable than a provider-specific abstraction alone ([Google Cloud Vertex AI release notes](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/release-notes)). |
| 2026-11-15 | Microsoft Foundry schedules retirement of the listed Codex-mini version. | Coding workflows are particularly sensitive to behavioural changes; the migration is an observable test of whether teams retained task-level evals or relied on a platform label ([Microsoft Foundry retirement schedule](https://learn.microsoft.com/pt-pt/azure/foundry/openai/concepts/model-retirement-schedule)). |
| 2026-11-26 | Google Cloud says Vertex AI Extensions will be shut down and recommends migration to Agent Platform. | This is direct evidence of vendor-suite consolidation pressure and a test of whether internal abstractions reduce or merely postpone vendor migration work ([Google Cloud Vertex AI release notes](https://docs.cloud.google.com/vertex-ai/docs/release-notes)). |
| 2026-12-02 | The limited Article 50 grace period ends for marking and detection obligations applying to covered systems placed on the market before 2026-08-02. | Legacy systems become part of the transparency-control inventory, increasing demand for discovery and evidence but not necessarily for a broad developer portal ([European Commission](https://digital-strategy.ec.europa.eu/en/faqs/transparency-obligations-under-article-50-ai-act)). |

## Second-order effects map

| First-order effect if it lands | 2–3 second-order effects |
|---|---|
| **Market structure: narrow gateways and eval services become the first shared AI capability.** | 1. Model access, credentials, token limits, routing and telemetry become commodity gateway features; Microsoft already packages these in a managed gateway and says direct provider access remains simpler for one application without shared-governance needs ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)). 2. Competition shifts upward to evaluation, policy, workflow context and evidence because OpenTelemetry is standardising provider-neutral agent and model signals ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/)). 3. AI-platform vendors respond by bundling the narrow primitives into broader suites; Scale AI’s commercially interested build-and-buy guide explicitly recommends buying a common substrate while building differentiating logic ([Scale AI](https://scale.com/guides/build-vs-buy)). |
| **Regulatory ripple: governance moves from documents into shared enforcement and evidence.** | 1. Article 50 creates a dated transparency obligation, so organisations need to identify covered systems and demonstrate controls; national market-surveillance authorities are the principal enforcers ([European Commission](https://digital-strategy.ec.europa.eu/en/faqs/transparency-obligations-under-article-50-ai-act)). 2. Central logs and policy can reduce repeated evidence work but create a privacy and availability chokepoint; Azure says data residency depends on the complete gateway, backend and telemetry path ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)). 3. The absence of finished harmonised standards increases demand for vendor interpretations: CEN-CENELEC is using exceptional measures to target availability of key standards late in the year, without an exact publication date for each standard ([CEN-CENELEC](https://www.cencenelec.eu/news-events/news/2025/brief-news/2025-10-23-ai-standardization/)). |
| **Talent flows: platform work becomes more product, evaluation and policy work, not less operations.** | 1. Platform teams need product discovery, adoption measurement and task-success skills; DORA recommends a product manager, user-journey mapping, developer-satisfaction measures and delivery metrics ([DORA](https://dora.dev/capabilities/platform-engineering/)). 2. AI-specific work shifts toward evaluation datasets, observability, model lifecycle and policy calibration, while application teams retain domain success criteria; NIST’s map-measure-manage loop is explicitly contextual rather than a universal checklist ([NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)). 3. Maintenance does not disappear: Spotify’s Backstage guidance assigns a central team deployment, CI/CD, support, adoption and eventual on-call duties ([Backstage](https://backstage.io/docs/overview/adopting/)). |
| **Adjacent industries: observability, portals, FinOps and migration tooling converge around agents.** | 1. OpenTelemetry releases already add agent spans, tool-call detail, evaluation events, token and streaming metrics, creating a common substrate for observability and cost products ([OpenTelemetry releases](https://github.com/open-telemetry/semantic-conventions/releases)). 2. Portals expand from service catalogues to agent context catalogues; Backstage has an open `AIContext` proposal motivated by growing context files for Claude Code, GitHub Copilot and Cursor ([Backstage issue](https://github.com/backstage/backstage/issues/33575)). 3. Dense model-retirement schedules create a market for inventory, regression evaluation and automated migration rather than for model access alone ([Google Cloud](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/release-notes), [Microsoft Foundry](https://learn.microsoft.com/pt-pt/azure/foundry/openai/concepts/model-retirement-schedule)). |
| **Geopolitical posture: region and lawful control become architectural selection criteria.** | 1. Microsoft’s managed AI Gateway preview is initially limited to East US 2 and Sweden Central, so organisations outside or between those regions must accept cross-region paths, self-host another layer, or choose another provider ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)). 2. EU transparency enforcement and data-path scrutiny favour explicit inventories of gateway, model, tool and telemetry jurisdictions rather than a generic “EU-hosted platform” claim ([European Commission](https://digital-strategy.ec.europa.eu/en/faqs/transparency-obligations-under-article-50-ai-act), [Microsoft Learn](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)). 3. Provider diversity becomes resilience and bargaining leverage only if interfaces, evals and data can move; otherwise multi-provider catalogues add complexity without practical exit. The last point is an inference from the documented retirement and region differences, not a measured outcome. |
| **Public narrative: “AI platform” shifts from launch object to measurable operating loop—or provokes a backlash.** | 1. DORA frames AI as an amplifier of existing organisational strengths and weaknesses, which weakens claims that buying one platform is sufficient ([DORA](https://dora.dev/research/2025/dora-report/)). 2. The recent literature review found only 2 of 88 included sources were tier-one publications primarily about platform engineering and found no peer-reviewed evidence for IDP scorecard effectiveness; independent outcome evidence will therefore matter more as vendor claims grow ([Frontiers in Computer Science](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)). 3. If mandates raise usage while exceptions, support load or delivery outcomes worsen, engineers are likely to describe the initiative as centralisation rather than enablement; this is a scenario inference, not an observed population estimate. |

## Four scenarios

### Base — A narrow internal capability portfolio grows one proven constraint at a time

- **Trigger conditions:** At least two independent teams show the same blocked workflow; a gateway, shared eval suite, model inventory or policy service removes that constraint; retained voluntary use and task success improve without worse stability, throughput or support load.
- **Leading indicators in the next 6–12 months:** Teams use the retirements in the [forward calendar](#forward-calendar) to reroute models and rerun evals without application-by-application crisis work; platform roadmaps add lifecycle inventory, evals and observability before portals or training infrastructure; DORA-style task and delivery measures accompany adoption counts ([DORA](https://dora.dev/capabilities/platform-engineering/)).
- **Probability:** **Plausible (45%)**. Microsoft now explicitly distinguishes the many-model/governance gateway case from the simpler direct-call case, while Google says there is no one-size-fits-all platform; both support scoped adoption, although both vendors benefit from selling the underlying services ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview), [Google Cloud](https://cloud.google.com/solutions/platform-engineering)).
- **Downstream effects:** Small platform teams become owners of interfaces, evidence and exceptions; application teams retain workflow logic; deletion remains credible because each capability has its own outcome and dependency boundary.

### Upside — Managed primitives absorb commodity operation while the organisation owns policy and feedback

- **Trigger conditions:** Managed gateways publish production SLAs, pricing and adequate regions; provider-neutral telemetry and model contracts work across at least two providers; organisations can export logs/evals and exercise rollback without material rewrite.
- **Leading indicators in the next 6–12 months:** Azure AI Gateway exits best-effort preview or materially expands its two-region footprint; OpenTelemetry stabilises a core GenAI convention set; the migrations in the [forward calendar](#forward-calendar) are handled behind stable organisational contracts rather than vendor-specific application changes ([Azure](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview), [OpenTelemetry roadmap](https://github.com/open-telemetry/semantic-conventions/issues/3330)).
- **Probability:** **Modest (25%)**. Provider-managed routing and policy already exist, and AWS recommends managed APIs as the usual starting point, but pricing, regional coverage, semantic-convention stability and exit evidence are incomplete ([AWS](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-enterprise-ready-gen-ai-platform/infrastructure.html)).
- **Downstream effects:** Cloud and AI vendors capture more operating spend; internal teams become thinner product, evaluation and governance groups; portability depends more on tests, telemetry and contracts than on self-hosting infrastructure.

### Downside — Compliance anxiety and agent sprawl produce a broad mandatory platform

- **Trigger conditions:** Procurement selects an integrated suite before workflows are measured; Article 50 and later controls are interpreted as requiring one central enforcement plane; exceptions require tickets; adoption is mandated; platform scope expands faster than retained voluntary use.
- **Leading indicators in the next 6–12 months:** Google’s [2026-11-26](#forward-calendar) Extensions-to-Agent-Platform migration becomes a wider pattern; vendor reference architectures converge on data, models, security, templates, agents, portals and telemetry as one purchase; case studies report seats or calls without task-success, exception or maintenance measures ([Google Cloud](https://docs.cloud.google.com/vertex-ai/docs/release-notes), [AWS](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-enterprise-ready-gen-ai-platform/layered-approach.html)).
- **Probability:** **Modest (20%)**. Vendor packaging and regulation make centralisation attractive, but DORA and Google both recommend user-centred, iterative platforms rather than a big-bang universal design ([DORA](https://dora.dev/capabilities/platform-engineering/), [Google Cloud](https://cloud.google.com/blog/products/application-development/another-five-myths-about-platform-engineering)).
- **Downstream effects:** Security and finance gain visibility; engineers lose local agency; the platform team becomes a high-blast-radius dependency; switching and deletion become expensive because workflow, evidence and provider contracts are coupled.

### Wildcard — Standards and provider-native controls make most internal AI platforms unnecessary

- **Trigger conditions:** OpenTelemetry GenAI conventions stabilise and are implemented by major frameworks; providers expose adequate identity, policy, evaluation and cost APIs directly; teams satisfy applicable obligations with libraries, templates and evidence stores; broad internal capabilities are measurably unused and deleted.
- **Leading indicators in the next 6–12 months:** Direct-provider deployments survive the [forward-calendar](#forward-calendar) migrations through shared libraries and CI evals; OpenTelemetry adoption grows without a central gateway; teams publish thinnest viable platforms that are documentation and reusable components rather than services ([OpenTelemetry](https://github.com/open-telemetry/semantic-conventions-genai), [Team Topologies](https://teamtopologies.com/key-concepts-content/what-is-a-thinnest-viable-platform-tvp)).
- **Probability:** **Low (10%)**. The technical ingredients exist, and Microsoft concedes direct calls can be simpler, but cross-team identity, evidence, quota and incident needs still create runtime coordination in larger portfolios ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)).
- **Downstream effects:** Application teams regain tool choice; libraries and standards maintainers become critical infrastructure; duplicated integration may return; “platform” becomes an operating convention rather than a product suite.

## The single 90-day signal

**By 2026-10-26, classify every enterprise AI-governance capability newly announced or materially updated in a fixed public sample—Azure AI Gateway, AWS Bedrock/SageMaker guidance, Google Vertex/Agent Platform, OpenTelemetry GenAI conventions and Backstage—as either (a) independently consumable primitive with an API/export path or (b) suite-only capability.** If most material additions are primitives and the [2026-08-02](#forward-calendar) EU compliance guidance can be implemented without adopting a broad suite, raise the Base and Upside weights. If controls, evidence and agent catalogues become available mainly inside integrated suites or migrations such as Vertex Extensions → Agent Platform, raise the Downside weight. Look at the linked official release notes, documentation histories and repositories; this is a deliberately fixed sample, not a claim to represent the whole market.

## What current coverage is most under-pricing

**Deletion and exception handling are the under-priced future.** Vendor coverage concentrates on which layers to add, while NIST explicitly includes safe decommissioning and periodic review in AI governance, and the Government Digital Service showed that even a reliable, used platform can rationally be sunset when provider capability, user capability and reinvestment economics change ([NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), [GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). Model retirements make that lifecycle immediate: each exception, bypass, migration and unused capability is evidence for whether to expand, narrow, buy or delete. A platform without an exception ledger and deletion trigger can only grow, so “smallest” becomes a launch adjective rather than an enduring constraint.

## Watch list

| What to monitor | Where | Change that matters |
|---|---|---|
| Article 50 implementation and enforcement clarifications | [European Commission FAQ](https://digital-strategy.ec.europa.eu/en/faqs/transparency-obligations-under-article-50-ai-act) | Guidance that requires specific runtime evidence versus documentation or process evidence. |
| AI Act application timeline | [European Commission](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) | Any enacted change to applicability dates or scope; distinguish enacted law from proposals. |
| Harmonised AI standards | [CEN-CENELEC](https://www.cencenelec.eu/news-events/news/2025/brief-news/2025-10-23-ai-standardization/) | Publication of exact standards and dates that turn vague compliance work into implementable controls. |
| Azure AI Gateway maturity | [Microsoft Learn](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview) | General availability, SLA, pricing, region expansion, per-key least-privilege changes, and export/exit support. |
| Microsoft model lifecycle | [Foundry schedule](https://learn.microsoft.com/pt-pt/azure/foundry/openai/concepts/model-retirement-schedule) | Date changes, shorter overlap windows, and whether migrations preserve API and evaluation compatibility. |
| Google model and agent lifecycle | [Vertex AI release notes](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/release-notes) | More forced migration into Agent Platform versus provider-neutral APIs. |
| Databricks partner-model lifecycle | [Maintenance policy](https://learn.microsoft.com/en-us/azure/databricks/machine-learning/retired-models-policy) | Retirement-date divergence from underlying providers, which increases inventory value. |
| OpenTelemetry GenAI standards | [GenAI repository](https://github.com/open-telemetry/semantic-conventions-genai) and [releases](https://github.com/open-telemetry/semantic-conventions/releases) | Stabilised core conventions, evaluation events, framework coverage, and breaking changes. |
| Backstage’s AI catalogue boundary | [`AIContext` RFC](https://github.com/backstage/backstage/issues/33575) and [roadmap](https://github.com/backstage/backstage/issues/32083) | Whether agent context becomes a small catalogue extension or expands the portal into an AI control plane. |
| DORA platform findings | [DORA capability page](https://dora.dev/capabilities/platform-engineering/) | New evidence separating voluntary adoption, task success, delivery performance and AI effects. |
| Independent platform evidence | [Frontiers review](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full) | New peer-reviewed longitudinal or comparative studies, especially scorecard, exception and deletion evidence. |
| NIST lifecycle guidance | [AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) | Revised guidance that changes inventory, third-party, incident, review or decommission expectations. |
| Vendor scope expansion | [AWS layered guidance](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-enterprise-ready-gen-ai-platform/layered-approach.html) and [Scale AI guide](https://scale.com/guides/build-vs-buy) | New layers sold as universally necessary versus explicit workload thresholds and exit paths. |
| Shared-service incidents | [OpenAI status](https://status.openai.com/history) and [Cloudflare postmortem](https://blog.cloudflare.com/cloudflare-service-outage-june-12-2025/) | Gateway, identity, telemetry or shared-store failures that reveal real blast radius and fallback quality. |
| Practitioner implementation mix | [r/platformengineering](https://www.reddit.com/r/platformengineering/) and [Backstage issues](https://github.com/backstage/backstage/issues) | Firsthand reports of narrow gateways/evals, broad suites, bypass queues, maintenance load, or deliberate non-platform choices. |

## Source receipts

### Calendar

- [European Commission — AI Act application timeline](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)
- [European Commission — Article 50 FAQ](https://digital-strategy.ec.europa.eu/en/faqs/transparency-obligations-under-article-50-ai-act)
- [Microsoft Foundry — model retirement schedule](https://learn.microsoft.com/pt-pt/azure/foundry/openai/concepts/model-retirement-schedule)
- [Microsoft — Azure OpenAI model retirements](https://learn.microsoft.com/es-es/azure/ai-foundry/openai/concepts/model-retirements)
- [Azure Databricks — generative-model maintenance policy](https://learn.microsoft.com/en-us/azure/databricks/machine-learning/retired-models-policy)
- [Google Cloud — Generative AI on Vertex AI release notes](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/release-notes)
- [Google Cloud — Vertex AI release notes](https://docs.cloud.google.com/vertex-ai/docs/release-notes)
- [CEN-CENELEC — accelerated AI-standard development](https://www.cencenelec.eu/news-events/news/2025/brief-news/2025-10-23-ai-standardization/)

### Forecast

- [Microsoft Learn — AI Gateway tier overview](https://learn.microsoft.com/en-us/azure/api-management/ai-gateway-overview)
- [DORA — platform engineering capability](https://dora.dev/capabilities/platform-engineering/)
- [DORA — State of AI-assisted Software Development](https://dora.dev/research/2025/dora-report/)
- [AWS — layered enterprise generative-AI platform](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-enterprise-ready-gen-ai-platform/layered-approach.html)
- [AWS — generative-AI infrastructure starting points](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-enterprise-ready-gen-ai-platform/infrastructure.html)
- [Google Cloud — platform engineering](https://cloud.google.com/solutions/platform-engineering)
- [Google Cloud — iterative minimum viable platform](https://cloud.google.com/blog/products/application-development/another-five-myths-about-platform-engineering)
- [Scale AI — build versus buy](https://scale.com/guides/build-vs-buy)
- [Team Topologies — thinnest viable platform](https://teamtopologies.com/key-concepts-content/what-is-a-thinnest-viable-platform-tvp)

### Filing

- None used: there is no focal listed company, transaction, contract renewal or filing-defined event.

### Analyst

- [NIST — AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)
- [Frontiers in Computer Science — multivocal platform-engineering review](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)
- [OpenTelemetry — GenAI observability](https://opentelemetry.io/blog/2026/genai-observability/)
- [Government Digital Service — GOV.UK PaaS decommission](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)
- [Cloudflare — shared-dependency outage postmortem](https://blog.cloudflare.com/cloudflare-service-outage-june-12-2025/)

### Community

- [OpenTelemetry semantic-conventions releases](https://github.com/open-telemetry/semantic-conventions/releases)
- [OpenTelemetry GenAI semantic-conventions repository](https://github.com/open-telemetry/semantic-conventions-genai)
- [Backstage `AIContext` RFC](https://github.com/backstage/backstage/issues/33575)
- [Backstage roadmap](https://github.com/backstage/backstage/issues/32083)
- [Backstage adoption guidance](https://backstage.io/docs/overview/adopting/)
- [r/platformengineering](https://www.reddit.com/r/platformengineering/)

### Snowball pass

First-round proper nouns classified **already searched**: European Commission; EU AI Act; Article 50; AI Office; Microsoft; Azure AI Gateway; Microsoft Foundry; Microsoft Entra ID; Azure Databricks; Google Cloud; Vertex AI; Gemini; Agent Platform; DORA; GitHub; GitLab; CNCF; WSO2; OpenTelemetry; NIST; AI RMF; AWS; Amazon Bedrock; Amazon SageMaker AI; Scale AI; Spotify; Backstage; Team Topologies; Government Digital Service; GOV.UK PaaS; Cloudflare. Classified **search-now**: CEN-CENELEC and its standards schedule; Google Agent Platform as the named destination for Vertex AI Extensions; OpenTelemetry GenAI releases and stability roadmap. All received targeted primary-source queries and were folded into the calendar, effects, scenarios and watch list. Classified **background-only** because they were incidental rather than load-bearing: Anthropic; Cursor; Claude Code; Kubernetes; Application Insights; CEN-CLC/JTC 21; East US 2; Sweden Central. The follow-up searches added no new load-bearing unsearched entity, so the snowball stopped after one targeted round.
