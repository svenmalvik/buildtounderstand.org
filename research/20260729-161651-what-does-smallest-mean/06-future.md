# Futures and second-order effects: four ways “smallest” can evolve

This is a set of conditional trajectories, not a claim that one architecture is destined to win. The evidence is unusually weak for confident prediction: a systematic review published on **2026-05-04** found only **2 of 88** included sources from top-tier venues with platform engineering as their primary subject, no longitudinal or quasi-experimental multi-organization evidence, and no peer-reviewed empirical evidence for scorecards despite widespread commercial use ([Frontiers in Computer Science](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)). The probabilities below are therefore decision priors to update with an organization’s own task-success, cost, risk, and reversibility data.

The four scenarios deliberately use different mechanisms:

- **Contracts-only** standardizes representation and leaves execution with teams or incumbent systems.
- **Narrow managed capability** centralizes one proven runtime control, such as agent-tool authorization or model routing.
- **Broad integrated platform** centralizes the development and operating lifecycle.
- **No dedicated AI platform** lets existing developer, identity, security, observability, and FinOps systems absorb AI-specific work.

## Forward calendar

skipped per research plan: this is an evergreen design question with no launch, filing, deadline, or external event calendar; scheduled milestones would create a false news frame.

## Second-order effects map

These branches describe what could follow **if an organization adopts each operating model and it becomes the default path**. They are not assertions that the effects have already occurred.

| First-order effect | Second-order effect 1 | Second-order effect 2 | Second-order effect 3 |
|---|---|---|---|
| **Contracts-only makes schemas, metadata, policies, instructions, and conformance tests the shared layer.** | **Market structure:** value moves from a stand-alone portal or agent-builder product toward interoperable registries, validators, adapters, and support. That is a credible trajectory because the Linux Foundation placed MCP and AGENTS.md under a vendor-neutral foundation on **2025-12-09**, reporting broad cross-vendor participation and more than **10,000 published MCP servers** ([Linux Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation?hs_amp=true)). | **Talent flows:** fewer engineers may be assigned to a new AI control plane, but product-management, schema-governance, migration, and contribution-model work moves into existing platform teams. CNCF says a platform can be as thin as a wiki page, while also stressing that capabilities and providers still require a consistent user experience; thinness changes the work, not whether somebody owns it ([CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/es/whitepapers/platforms/)). | **Public narrative:** “platform” may stop meaning a portal and start meaning machine-readable organizational context. Backstage already exposes catalogue and scaffolder actions as MCP tools, including filtered servers, authentication, metrics, and traces; its current implementation demonstrates how an existing catalogue can become an agent-facing surface without a new AI portal ([Backstage MCP Actions](https://backstage.io/docs/ai/mcp-actions/), accessed **2026-07-29**). |
| **A narrow managed gateway becomes the common path for model calls or agent-tool actions.** | **Regulatory and security ripple:** identity, delegated authority, audit, and non-repudiation become more important than model choice. NIST’s AI Agent Standards Initiative, announced on **2026-02-17**, specifically targets agent authentication, authorization, interoperability, and security evaluation; its RFI analysis published on **2026-05-18** says respondents broadly agreed that familiar cybersecurity practices remain relevant but require adaptation for agents ([NIST initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative); [NIST RFI analysis](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai)). | **Adjacent industries:** observability, identity, policy-as-code, and FinOps become part of the gateway’s practical product boundary. OpenTelemetry showed GenAI traces that join model calls, token counts, and tool activity on **2026-05-14**, while FinOps practitioners reported that AI cost visibility, allocation, and value remain unresolved even though **98%** of **693** respondents manage AI spend ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/); [State of FinOps](https://data.finops.org/), accessed **2026-07-29**). | **Public narrative:** the gateway may be sold internally as “guardrails,” even though it can prove only what passed through it. AWS made externalized tool authorization in AgentCore Policy generally available on **2026-03-03**; the design intercepts gateway traffic but does not establish that all agents use that gateway or that allowed actions produce correct business outcomes ([AWS](https://aws.amazon.com/about-aws/whats-new/2026/03/policy-amazon-bedrock-agentcore-generally-available/)). |
| **A broad integrated platform combines catalogue, runtime, gateway, policy, evaluation, observability, and deployment workflows.** | **Market structure:** hyperscalers gain an advantage because they can bundle models, runtime, identity, policy, telemetry, and hosting. Microsoft Foundry presents agents, more than **1,900 models**, observability, governance, and a single management plane; Google Agent Engine similarly combines managed runtime, sessions, evaluation, observability, templates, and CI/CD ([Microsoft Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/azure-openai-in-azure-ai-foundry); [Google Vertex AI Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/reasoning-engine/overview?authuser=3), accessed **2026-07-29**). The inference is that a broad internal build competes not only with one vendor feature but with an expanding bundle. | **Talent flows:** platform engineers acquire product, security, reliability, and support responsibilities, while application teams lose some infrastructure work but become consumers of a central roadmap. DORA’s guidance, updated **2026-01-12**, warns against “build it and they will come,” recommends a minimum viable platform, and requires adoption, retention, task success, developer satisfaction, and delivery metrics rather than feature output ([DORA](https://dora.dev/capabilities/platform-engineering/)). | **Geopolitical posture:** infrastructure region, provider control, model supply, and policy implementation become coupled procurement decisions. EU general-purpose-model obligations entered into application on **2025-08-02**, but downstream system providers retain their own role-specific duties; a broad vendor platform can provide evidence and controls without assuming the deployer’s full accountability ([European Commission](https://digital-strategy.ec.europa.eu/en/factpages/general-purpose-ai-obligations-under-ai-act)). The inference is that “sovereign” or region-specific bundles become more attractive, while exit becomes more complex. |
| **No dedicated AI platform is created; incumbent developer and governance systems absorb the work.** | **Market structure:** an “AI platform” category can dissolve into Git hosting, portals, identity, observability, cloud cost management, and ordinary delivery tooling. GitHub already lets enterprises define agents as Markdown in a governed repository and apply enterprise rulesets, while Backstage has introduced an `AiResource` entity and an `mcp-server` API subtype ([GitHub enterprise agents](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents); [Backstage v1.51](https://backstage.io/docs/releases/v1.51.0/), accessed **2026-07-29**). | **Regulatory ripple:** responsibility stays distributed among application, security, privacy, records, procurement, and audit owners. NIST’s GenAI profile, published on **2024-07-26** and updated on **2026-04-08**, treats risk management as lifecycle and role work rather than as one product; this supports extending existing governance but also makes fragmentation visible ([NIST AI 600-1](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence)). | **Public narrative and organizational politics:** avoiding a named AI platform may look like inaction even when incumbents are doing the work; conversely, it can expose that most needs were ordinary platform problems. DORA describes AI as an amplifier of existing strengths and dysfunctions and says low-quality platforms can absorb local AI gains in downstream disorder ([DORA](https://dora.dev/capabilities/platform-engineering/)). The inference is that leadership attention may shift from agent counts to delivery-system quality—or demand a visible program despite weak evidence. |

### Cross-model effects that do not disappear

**Interoperability can lower switching cost and increase attack surface at the same time.** MCP’s authorization specification defines transport-level authorization, but authorization is optional and implementation choices remain; NIST and OWASP have separately identified agent identity, delegated authority, goal hijacking, and tool misuse as material concerns ([MCP authorization specification](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2025-03-26/basic/authorization.mdx); [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/), published **2025-12-09**). Open contracts make substitution and reuse easier, but every new compatible client can become another privileged caller.

**Better agents increase the value of downstream platform quality, not only the value of agent infrastructure.** METR’s experienced-maintainer study published on **2025-07-10** measured a **19% slowdown** with early tools, while its later report published on **2026-05-19** found a small estimated **4%–20% benefit** from later public agents and warned that selection effects probably matter ([METR early study](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/); [METR later update](https://metr.org/blog/2026-05-19-frontier-risk-report/?dot=INC-029)). The disagreement is informative: as capability changes, the bottleneck can move from code production to review, testing, deployment, authorization, and operational feedback. It does not by itself prove that a dedicated AI platform is the remedy.

**Instrumentation standards can commoditize telemetry while making semantics the scarce layer.** OpenTelemetry now defines attributes for agents, conversations, providers, evaluations, tool calls, data sources, and token use ([OpenTelemetry GenAI attributes](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/), accessed **2026-07-29**). If those fields become portable, collecting traces becomes less differentiating; deciding which business outcome, risk, owner, and evaluation a trace refers to becomes the harder organizational contract.

## Four scenarios

The four probabilities sum to **100%**. They are estimates as of **2026-07-29**, not frequencies derived from a population. “Leading indicators” are observable over **2026-07-29** to **2027-07-29**; they replace calendar cross-links because the research plan correctly skips an external event calendar.

### Base — Contracts become the platform

**Headline:** A versioned agent contract consumed by Backstage or source-control workflows removes enough discovery, ownership, cost-allocation, and governance friction that a separate AI runtime or portal is not justified.

**Trigger conditions, all falsifiable**

1. At least three materially different teams adopt the same contract voluntarily for one repeated workflow.
2. At least **80%** of representative users complete that workflow without synchronous help from the contract owner.
3. Required ownership, model/provider, data-use, evaluation, cost-allocation, and lifecycle fields remain at least **90%** conformant for two consecutive monthly samples.
4. Median waiting time and support effort do not increase by more than **10%** against the pre-contract baseline.
5. No audit, incident, or high-impact use-case review demonstrates a need for a common runtime enforcement point.

**Leading indicators over the next 6–12 months**

- Backstage’s experimental `AiResource` and `mcp-server` catalogue types move toward stable semantics, and adopters can extend them without forking the catalogue model ([Backstage v1.51](https://backstage.io/docs/releases/v1.51.0/), accessed **2026-07-29**).
- Organization- and enterprise-scoped Markdown agent definitions become normal across developer tools, reducing the value of a separate authoring UI ([GitHub custom agents](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/copilot-cli/use-copilot-cli/invoke-custom-agents), accessed **2026-07-29**).
- OpenTelemetry’s GenAI vocabulary converges on stable identifiers for agents, tools, data sources, evaluations, and usage, allowing the contract to point into ordinary observability systems ([OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/), accessed **2026-07-29**).
- Exceptions remain rare and expire; teams do not create shadow registries or request a portal to understand the schema.

**Probability: Plausible — 35%.** The CNCF’s “thinnest reasonable layer,” DORA’s minimum viable platform, open agent conventions, and Backstage’s AI metadata trajectory make the mechanism credible ([CNCF](https://tag-app-delivery.cncf.io/es/whitepapers/platforms/); [DORA](https://dora.dev/capabilities/platform-engineering/)). The probability is capped because contracts do not themselves enforce runtime authorization, prove metadata truth, or make a text-based workflow usable for every non-engineer.

**Downstream effects**

- The existing developer platform gains strategic importance without a new AI product boundary.
- Schema reviewers, metadata owners, and migration tooling become the real platform team, even if no team carries that name.
- Vendor switching is easier where contracts reference portable protocols and telemetry, but weak semantics can produce nominal rather than operational portability.
- Removal remains comparatively cheap if the contract has explicit consumers, versions, and deprecation tests.

### Upside — One narrow managed choke point earns its keep

**Headline:** A gateway for model access or agent-tool authorization removes a measured cross-team constraint while application teams continue to own agent design, evaluation, deployment, and business outcomes.

**Trigger conditions, all falsifiable**

1. A baseline shows repeated waiting, duplicated authorization, missing spend attribution, or audit work across at least three teams.
2. A gateway pilot cuts the selected constraint—such as median credential lead time, audit-evidence preparation, or unattributed spend—by at least **30%**.
3. At least **80%** of pilot teams retain the path voluntarily after eight weeks, while bypass stays below **10%** of eligible calls.
4. P95 added latency stays within the workload’s predeclared budget, and gateway incidents do not increase failed task completion by more than **5%**.
5. The gateway remains a replaceable boundary: agent code, evaluation data, and business workflows do not depend on its proprietary runtime.

**Leading indicators over the next 6–12 months**

- NIST’s agent-identity work produces implementable guidance that can be satisfied by an identity-and-policy boundary rather than a full development platform ([NIST](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative), updated **2026-04-20**).
- MCP authorization and enterprise gateway patterns converge on per-user, per-agent, per-tool, and per-request scopes instead of static shared tokens ([MCP authorization](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2025-03-26/basic/authorization.mdx), specification dated **2025-03-26**).
- Managed gateways expose policy decisions, tool identity, cost, traces, and exportable logs through ordinary standards. AWS already supports log-only versus enforced policy modes and publishes authorization decisions and reasons to telemetry ([AWS AgentCore policy docs](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/policy.html), accessed **2026-07-29**).
- The pilot’s support queue stays bounded rather than expanding into requests for hosting, memory, prompt management, UI, and business evaluation.

**Probability: Plausible — 40%.** Agent identity and tool authorization are genuinely agent-specific enough to create a shared enforcement need, and both NIST and current cloud products are converging on that boundary ([NIST RFI analysis](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai); [AWS AgentCore Policy](https://aws.amazon.com/about-aws/whats-new/2026/03/policy-amazon-bedrock-agentcore-generally-available/)). It is the highest-weight scenario because it centralizes a hard-to-duplicate control without assuming that every surrounding concern needs a new platform.

**Downstream effects**

- Identity, observability, and FinOps teams become co-owners of what began as a gateway.
- The gateway becomes critical infrastructure quickly, so on-call, rate limits, fallback, provider routing, and decommission tests are needed earlier than its small feature list suggests.
- Common policy reduces local duplication but increases common-mode failure: one wrong rule can deny or permit actions across many teams.
- Platform success becomes measurable as constraint removal and task success rather than the number of agents routed through it.

### Downside — The “minimum” expands into an integrated platform before evidence arrives

**Headline:** Catalogue, gateway, runtime, evaluation, observability, governance, and deployment are bundled into a mandatory internal product whose coordination cost and lock-in exceed the duplicated work it was meant to remove.

**Trigger conditions, all falsifiable**

1. Scope grows to four or more lifecycle categories before a baseline and a single target workflow have been measured.
2. Leadership measures registrations, agent count, portal visits, or token volume but cannot report task success, waiting time, support hours, exceptions, or cost per successful outcome.
3. Mandatory adoption exceeds **80%** while voluntary retention, satisfaction, or unassisted task completion remains below **60%**.
4. More than **25%** of adopter teams require exceptions or custom plugins, and the central backlog’s median age rises for three consecutive months.
5. A replacement exercise cannot move one representative agent, its policy, traces, and evaluation evidence within ten engineer-days.

**Leading indicators over the next 6–12 months**

- Vendor bundles continue adding runtime, memory, gateways, policy, identity, observability, evaluation, and deployment under one management plane ([Microsoft Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/azure-openai-in-azure-ai-foundry); [Google Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/reasoning-engine/overview?authuser=3), accessed **2026-07-29**).
- Backstage’s agent-facing action surface expands faster than the organization’s permission model and ownership data mature. Its current documentation already labels some external authentication paths experimental and a static token path temporary ([Backstage MCP Actions](https://backstage.io/docs/ai/mcp-actions/), accessed **2026-07-29**).
- Platform hiring and vendor commitments precede task baselines; product roadmaps describe feature coverage rather than the constraint each feature removes.
- Support tickets and exception paths grow after nominal adoption, matching DORA’s warning that platform value follows a J-curve and that “build it and they will come” is an anti-pattern ([DORA](https://dora.dev/capabilities/platform-engineering/), updated **2026-01-12**).

**Probability: Modest — 15%.** Commercial bundles and executive demand for visible control create real scope pressure, but the scenario is not the base case because established platform guidance now explicitly recommends minimum viable scope, extensibility, feedback, and outcome measurement. The thin empirical base makes both the enthusiasm and the confidence suspect ([Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full), published **2026-05-04**).

**Downstream effects**

- Application autonomy becomes exception management; the central team gains authority and permanent operational load.
- Integrated defaults can improve consistency while increasing the blast radius of a policy, identity, telemetry, or runtime failure.
- Stand-alone portal and orchestration vendors face stronger bundling pressure from cloud and developer-tool incumbents.
- Exit cost becomes a hidden liability because metadata, traces, policies, deployment state, and agent memory cross product boundaries.
- A failed platform can discredit useful shared controls along with unnecessary ones, causing a pendulum swing back to unmanaged local adoption.

### Wildcard — The AI-platform category disappears into incumbents

**Headline:** Existing source control, Backstage, identity, cloud, observability, security, and FinOps systems add enough AI-aware capability that no dedicated AI platform—or even a distinct contracts program—survives as an organizational object.

**Trigger conditions, all falsifiable**

1. Fewer than two repeated consequential constraints remain after existing systems add AI fields, policies, telemetry, and cost allocation.
2. Teams can use provider runtimes directly while ordinary identity and observability capture at least **90%** of in-scope calls and ownership.
3. Security and audit accept evidence from incumbent systems without a separate agent registry or gateway.
4. Central AI-platform proposals repeatedly fail the replacement test: an incumbent feature solves the same user job within one planning cycle at lower total support cost.
5. No dedicated AI-platform on-call rotation, budget, or roadmap is created during the observation period.

**Leading indicators over the next 6–12 months**

- GitHub, Backstage, and other incumbent developer systems keep turning agent configuration into repository-owned, organization-governed files and catalogue entities ([GitHub enterprise agents](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents); [Backstage v1.51](https://backstage.io/docs/releases/v1.51.0/), accessed **2026-07-29**).
- FOCUS and ordinary cloud billing exports add model, token, GPU, and agent attribution without requiring a separate AI FinOps database. The FinOps Foundation reports that practitioners’ top requested capability is granular AI spend monitoring and that AI management is already becoming ordinary technology-value work ([State of FinOps](https://data.finops.org/), accessed **2026-07-29**).
- OpenTelemetry and existing application-performance tools make provider-neutral agent traces routine ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/), published **2026-05-14**).
- Incident and audit reviews find that failures arise primarily in product-specific data, workflow, and authorization design rather than in missing shared AI infrastructure.

**Probability: Low — 10%.** The scenario is structurally possible because many “AI platform” needs are existing platform concerns and incumbents are adding AI-specific extensions. It remains low because agent identity, delegated tool authority, variable model economics, and evaluation create enough novel coordination that at least a contract or narrow shared service is likely to persist.

**Downstream effects**

- “AI platform engineer” work disperses into developer productivity, IAM, observability, security, data governance, and FinOps roles.
- Organizations avoid a new common-mode dependency but tolerate more variance in provider choice and local practice.
- Vendors market AI features as extensions of established control planes rather than as a separate platform category.
- Governance becomes less visible as a program and more dependent on the quality of existing ownership and delivery data.

## The single 90-day signal

**Signal:** the **unassisted task-success rate** for one repeated, consequential agent workflow after introducing only a versioned contract and conformance tests.

Starting from the dossier date, the 90-day window ends on **2026-10-27**. Select one workflow that currently crosses at least three teams—for example, registering an internal agent with a named owner, approved model/data class, cost center, evaluation evidence, and incident contact. Give representative engineers and non-engineer builders the contract through their existing workflow. Measure the percentage who complete the task correctly without synchronous help; audit correctness after completion rather than accepting self-report.

- **At least 80% unassisted success, with no material control gap:** raise the contracts-only scenario.
- **Below 50%, but a narrow gateway or generator removes the observed block:** raise the narrow-managed scenario.
- **Below 50% because several coupled lifecycle tasks are missing:** raise the broad-platform scenario only after testing whether incumbents can supply those tasks.
- **No improvement over the existing direct path:** raise the no-dedicated-platform scenario and retire the contract experiment.

This is the most informative single signal because DORA ties platform value to developer independence and explicitly recommends task-success measurement, while its guidance also warns that adoption alone can hide compulsion or poor fit ([DORA](https://dora.dev/capabilities/platform-engineering/), updated **2026-01-12**). Support tickets, portal logins, token volume, and agent counts are diagnostic context, not substitutes for the signal.

## What current coverage is most under-pricing

**The under-priced effect is the moment a “contracts-only” platform becomes a privileged execution surface.**

An agent metadata contract looks passive when read by humans or displayed in a catalogue. Once an agent consumes that catalogue and can invoke its exposed actions, names, schemas, tool descriptions, owner records, and policy metadata influence runtime behavior. Backstage now exposes catalogue and scaffolder capabilities as MCP actions, supports multiple filtered servers, and attaches authenticated-principal and agent fields to traces; its documentation simultaneously warns that some authentication support is highly experimental and that static-token access is temporary ([Backstage MCP Actions](https://backstage.io/docs/ai/mcp-actions/), accessed **2026-07-29**). NIST’s agent-security respondents broadly agreed that familiar security controls need adaptation, and OWASP lists agent goal hijacking and tool misuse among the material agentic risks ([NIST](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai), published **2026-05-18**; [OWASP](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/), published **2025-12-09**).

The consequence is not that contracts-only is unsafe. It is that **read-only metadata, agent-consumable context, and executable tools are three different capability classes** even when one portal serves all three. The minimum should specify which class each contract field and endpoint belongs to, the principal on whose behalf an action runs, the permitted tools and parameters, and how an operator can revoke or trace it. Otherwise the organization can believe it avoided a runtime platform while quietly creating one.

## Watch list

| What to monitor | Where to look | Change that would matter |
|---|---|---|
| **Backstage `AiResource` entity semantics** | [Backstage release notes](https://backstage.io/docs/releases/v1.51.0/) | Promotion from alpha, a stable versioned descriptor, or a contribution model would strengthen contracts-only; incompatible churn would increase migration cost. Page accessed **2026-07-29**. |
| **Backstage MCP action permissions and authentication** | [MCP Actions documentation](https://backstage.io/docs/ai/mcp-actions/) | Stable delegated-user authentication, granular action policy, and safe defaults would support incumbent extension; persistent experimental/static-token paths would support a dedicated gateway. Page accessed **2026-07-29**. |
| **MCP specification releases and authorization changes** | [MCP specification repository](https://github.com/modelcontextprotocol/modelcontextprotocol) | Per-agent identity, scope step-up, credential isolation, and portable audit semantics would reduce proprietary gateway advantage. Repository accessed **2026-07-29**. |
| **Agentic AI Foundation governance and project convergence** | [Linux Foundation AAIF announcement](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation?hs_amp=true) | Neutral governance that produces compatible implementations strengthens contracts and incumbents; fragmentation or dominant-vendor extensions strengthen integrated platforms. Foundation formed **2025-12-09**. |
| **NIST agent identity and authorization guidance** | [AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative) | A small, implementable control profile would favor a narrow gateway; requirements spanning full lifecycle governance could raise the capability floor. Page updated **2026-04-20**. |
| **NIST agent-security evidence** | [RFI response analysis](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai) | Empirical incident patterns that concentrate at tool boundaries would favor gateways; failures dominated by product context would favor local ownership. Published **2026-05-18**. |
| **OWASP agentic risk revisions** | [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) | Mitigations that require shared runtime interception strengthen narrow or broad managed paths; repository/process controls strengthen contracts-only. Published **2025-12-09**. |
| **OpenTelemetry GenAI semantic-convention stability** | [GenAI attribute registry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/) | Stable agent, tool, evaluation, data-source, and usage identifiers would make telemetry portable; incompatible vendor fields would raise integration work. Page accessed **2026-07-29**. |
| **FinOps cost-and-usage standard coverage for AI** | [State of FinOps](https://data.finops.org/) and its FOCUS references | Provider-neutral token, model, GPU, agent, and business-owner fields would allow existing FinOps systems to absorb the work; persistent opacity favors a gateway. Page accessed **2026-07-29**. |
| **AWS AgentCore scope growth and separability** | [AgentCore release notes](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/release-notes.html) | Independent adoption/export of Gateway and Policy favors narrow-managed; increasing coupling among runtime, memory, identity, policy, and telemetry favors broad integration. Page accessed **2026-07-29**. |
| **Microsoft Foundry management-plane breadth** | [Microsoft Foundry overview](https://learn.microsoft.com/en-us/azure/ai-foundry/azure-openai-in-azure-ai-foundry) | More unified policy, models, agents, tools, and observability increases bundling pressure; clean external runtimes and exports preserve modularity. Page accessed **2026-07-29**. |
| **Google Agent Engine control coverage and portability** | [Vertex AI Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/reasoning-engine/overview?authuser=3) | Broader GA runtime/evaluation/observability capabilities strengthen integrated-platform economics; framework-neutral deployment and OpenTelemetry export reduce lock-in. Page accessed **2026-07-29**. |
| **Enterprise-scoped agent files in GitHub** | [GitHub enterprise custom agents](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents) | Stable repository governance, rulesets, audit, and cross-surface support would make contracts an incumbent feature; policy gaps would leave room for a separate platform. Page accessed **2026-07-29**. |
| **DORA platform-quality and AI-amplification evidence** | [DORA platform-engineering capability](https://dora.dev/capabilities/platform-engineering/) | Replicated evidence linking platform quality to organizational AI outcomes would raise the case for investment; evidence that narrow task success dominates maturity would support subtraction. Page updated **2026-01-12**. |
| **Independent platform-engineering research** | [Frontiers multivocal review](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full) and subsequent citations | A controlled comparison of contracts-only, narrow, broad, and decentralized models would materially update all four probabilities. Review published **2026-05-04**. |
| **Independent task-level AI productivity experiments** | [METR research](https://metr.org/blog/2026-05-19-frontier-risk-report/?dot=INC-029) | Sustained gains with downstream review/test/deploy bottlenecks would strengthen ordinary platform investment; highly workflow-specific gains would strengthen local autonomy. Update published **2026-05-19**. |

## Source receipts

### Calendar

- n/a: the Forward calendar is skipped per the research plan, and no scheduled external event is used as a scenario trigger.

### Forecast

- [DORA platform-engineering capability, updated **2026-01-12**](https://dora.dev/capabilities/platform-engineering/)
- [Frontiers platform-engineering multivocal review, published **2026-05-04**](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)
- [METR experienced-maintainer study, published **2025-07-10**](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/)
- [METR later-agent update, published **2026-05-19**](https://metr.org/blog/2026-05-19-frontier-risk-report/?dot=INC-029)
- [State of FinOps, accessed **2026-07-29**](https://data.finops.org/)

### Filing

- n/a: no financial filing, contract expiry, earnings forecast, or public-company revenue claim is load-bearing for these internal operating-model scenarios.

### Analyst

- [NIST AI Agent Standards Initiative, announced **2026-02-17** and updated **2026-04-20**](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)
- [NIST agent-security RFI analysis, published **2026-05-18**](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai)
- [NIST GenAI Risk Management Profile, published **2024-07-26** and updated **2026-04-08**](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence)
- [European Commission general-purpose AI obligations, accessed **2026-07-29**](https://digital-strategy.ec.europa.eu/en/factpages/general-purpose-ai-obligations-under-ai-act)
- [OWASP Top 10 for Agentic Applications, published **2025-12-09**](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- [OpenTelemetry GenAI observability walkthrough, published **2026-05-14**](https://opentelemetry.io/blog/2026/genai-observability/)
- [OpenTelemetry GenAI attribute registry, accessed **2026-07-29**](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/)
- [AWS AgentCore Policy general availability, **2026-03-03**](https://aws.amazon.com/about-aws/whats-new/2026/03/policy-amazon-bedrock-agentcore-generally-available/)
- [AWS AgentCore Policy documentation, accessed **2026-07-29**](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/policy.html)
- [AWS AgentCore release notes, accessed **2026-07-29**](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/release-notes.html)
- [Microsoft Foundry overview, accessed **2026-07-29**](https://learn.microsoft.com/en-us/azure/ai-foundry/azure-openai-in-azure-ai-foundry)
- [Google Vertex AI Agent Engine, accessed **2026-07-29**](https://cloud.google.com/vertex-ai/generative-ai/docs/reasoning-engine/overview?authuser=3)

### Community

- [CNCF Platforms White Paper, accessed **2026-07-29**](https://tag-app-delivery.cncf.io/es/whitepapers/platforms/)
- [Linux Foundation Agentic AI Foundation announcement, **2025-12-09**](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation?hs_amp=true)
- [MCP authorization specification dated **2025-03-26**](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2025-03-26/basic/authorization.mdx)
- [MCP specification repository, accessed **2026-07-29**](https://github.com/modelcontextprotocol/modelcontextprotocol)
- [Backstage MCP Actions documentation, accessed **2026-07-29**](https://backstage.io/docs/ai/mcp-actions/)
- [Backstage v1.51 release notes, accessed **2026-07-29**](https://backstage.io/docs/releases/v1.51.0/)
- [GitHub custom-agent invocation documentation, accessed **2026-07-29**](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/copilot-cli/use-copilot-cli/invoke-custom-agents)
- [GitHub enterprise custom-agent governance, accessed **2026-07-29**](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents)

### Snowball pass

The first pass surfaced DORA/Google Cloud, CNCF, Backstage/Spotify, the Linux Foundation and Agentic AI Foundation, MCP/Anthropic, OpenTelemetry, NIST/CAISI/NCCoE, OWASP, the European Commission, FinOps Foundation, AWS, Microsoft, Google, GitHub, and METR. The search-now list was NIST agent identity, MCP authorization, OpenTelemetry GenAI semantics, Backstage’s current AI entity/action surface, the three hyperscaler agent control planes, GitHub’s enterprise agent governance, and FinOps AI attribution; each received a targeted search and primary-source check. A second pass added no unsearched parent, regulator, protocol steward, or named product necessary to distinguish the four mechanisms. Anthropic, Block, OpenAI, Azure identity, Google Cloud operations, and individual Backstage plugin vendors remain background-only where the cited foundation, specification, or product documentation already supports the claim.
