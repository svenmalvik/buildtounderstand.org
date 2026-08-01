# Futures and second-order effects: preserving freedom in a small AI platform

Research cut-off: 2026-07-31. This is a forward-looking analysis of the question in Chapter 5, not a forecast that the proposed platform will succeed. External dates below are taken from primary notices. Dates labelled **proposed/local checkpoint** are recommendations authored for this dossier to test the chapter's hypothesis, not commitments or announced events from any outside body.

The near-term environment is unusually good for falsifying the chapter's premise. Model, API, prompt, evaluation, and agent-building products all have announced shutdowns in the next six months; the EU has just changed the enforcement timetable of the AI Act; and open agent protocols are gaining neutral governance while still making substantial breaking changes. A platform that claims freedom should be able to absorb those changes without moving workflow ownership into a central runtime.

## Forward calendar

### External deadlines and events

| Date | Event | Source | Why it matters to the freedom question |
|---|---|---|---|
| 2026-08-02 | The European Commission and national authorities begin enforcing the AI Act's new transparency requirements. | [European Commission AI Act guidance](https://digital-strategy.ec.europa.eu/en/policies/guidelines-ai-high-risk-systems) | A repository contract may need to identify provider/deployer roles, disclosure duties, provenance, and the responsible human without dictating a model or runtime. It is an immediate test of whether mandatory evidence can be portable. |
| 2026-08-05 | Anthropic retires `claude-opus-4-1-20250805`; requests after retirement fail. | [Anthropic model deprecations](https://platform.claude.com/docs/en/about-claude/model-deprecations) | This is the first concrete exit rehearsal available after the research cut-off. Any workflow using the model must prove that its evaluation and adapter boundary work under time pressure. |
| 2026-08-10 | OpenAI shuts down `gpt-5.2-chat-latest` and `gpt-5.3-chat-latest`. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | “Latest” aliases do not remove lifecycle work. Contracts should name the required capability and acceptance test separately from the provider binding. |
| 2026-08-26 | OpenAI shuts down the Assistants API in favor of the Responses and Conversations APIs. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | This changes an orchestration API, not only a model. It tests whether conversation state, tools, and execution semantics are owned by the team contract or by a hosted framework. |
| 2026-09-24 | OpenAI shuts down the Videos API and Sora 2 models, with no replacement listed in the notice. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | Portability cannot always mean feature parity. The platform needs an explicit response when a capability disappears: degrade, replace, pause, or redesign the workflow. |
| 2026-09-28 | OpenAI shuts down four legacy GPT model families/snapshots. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | A grouped retirement wave tests inventory accuracy: can teams identify every dependency without a central runtime observing all calls? |
| 2026-10-23 | OpenAI shuts down a broad set of GPT, image, reasoning, and fine-tuned model versions. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | Fine-tuned and base-model migrations will expose provider-specific state that a thin API wrapper cannot make portable. The contract needs to record such non-portable assets honestly. |
| 2026-10-31 | Existing OpenAI Evals become read-only. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | Evaluation artifacts kept only inside a provider stop being an independent test of exit. Exported cases, graders, thresholds, and results should remain with the workflow or in a replaceable evaluation system. |
| 2026-11-30 | OpenAI shuts down reusable prompt objects, the Evals dashboard/API, and Agent Builder. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | Three kinds of workflow state—prompts, evaluations, and orchestration definitions—move at once. This is direct evidence against treating hosted product objects as the durable platform contract. |
| 2026-12-11 | OpenAI retires older GPT-5 and o3 model snapshots. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | Even pinned snapshots have finite lives. A replacement should be evaluated against workflow outcomes rather than presumed equivalent because the vendor recommends it. |
| 2027-01-06 | Existing OpenAI self-serve fine-tuning customers can no longer create new fine-tuning jobs. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | Fine-tuning may become an exit liability unless training data, recipes, evaluation sets, and fallback behavior are independently retained. |
| 2027-01-20 | OpenAI retires legacy audio, realtime, and transcription model families. | [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) | Multimodal and realtime features make lowest-common-denominator abstractions especially weak. The platform should declare capability differences rather than hide them. |
| 2027-12-02 | EU AI Act obligations for Annex III high-risk systems begin applying. | [European Commission AI Omnibus notice](https://digital-strategy.ec.europa.eu/en/news/ai-omnibus-enters-force) | Affected systems will need risk management, traceability, documentation, human oversight, robustness, cybersecurity, and accuracy. These are candidates for a portable evidence contract, but not a reason by themselves to mandate one runtime. |
| 2028-08-02 | EU AI Act obligations begin applying to high-risk AI embedded in regulated physical products. | [European Commission AI Omnibus notice](https://digital-strategy.ec.europa.eu/en/news/ai-omnibus-enters-force) | Robotics and machinery lengthen migration and support horizons. Exit plans must cover deployed products and retained evidence, not only source code. |

The ten OpenAI rows above are **correlated signals from one provider and one deprecation schedule**, not ten independent observations about the market. They establish that OpenAI customers face a concentrated migration wave; they do not by themselves establish an industry-wide retirement rate. Anthropic's separately published 2026-08-05 retirement is one independent provider example, but the calendar still should not be read as a prevalence sample.

OpenTelemetry provides a slower but useful comparison. Its source supplies a deprecation month window of **2026-06 (exact day not stated)** and says specification removal will occur **no earlier than 2027-06 (exact day not stated)**, while shims receive at least a year of maintenance ([OpenTelemetry notice](https://opentelemetry.io/blog/2026/deprecating-opencensus-compatibility/)). That staged approach is a possible model for the platform's own contract: announce deprecation, keep compatibility adapters, publish an earliest-removal window, and measure remaining consumers before removal. These are source-supplied month windows, kept outside the exact-date table rather than assigned invented `YYYY-MM-DD` dates.

### Proposed measurement checkpoints

Every row in this table is a **proposed/local checkpoint** authored for this research. None is an external deadline, vendor commitment, regulatory event, or forecasted fact.

| Proposed local date | Proposed/local checkpoint | Evidence to preserve |
|---|---|---|
| 2026-08-14 | **Proposed/local:** Select one production-shaped workflow and baseline its delivery lead time, failed runs, human interventions, provider-specific assets, platform support time, and current exit path. | A dated baseline in the repository and an inventory of every external object or approval needed to move it. |
| 2026-08-31 | **Proposed/local:** Put the smallest versioned workflow contract and its acceptance tests in the repository; validate in CI without requiring a central execution service. | Contract version, validation result, owner, risk classification, bindings, and documented opt-out. |
| 2026-09-30 | **Proposed/local:** Run the workflow through a second provider and, if feasible, a second agent runtime. Do not change the task-level contract to make the alternative pass; change only declared bindings/adapters or record an explicit capability gap. | Comparable quality, latency, cost, operator time, feature loss, control evidence, and every approval required. |
| 2026-10-29 | **Proposed/local:** Complete the 90-day exit drill and publish the verified exit lead time described below. | A reproducible migration log and a decision to keep, narrow, expand, or abandon the proposed platform contract. |

These checkpoints deliberately start with one workflow. DORA recommends a “minimum viable platform,” warns that an ivory-tower platform creates shadow workarounds, and says platform impact should combine delivery and developer-satisfaction signals rather than adoption alone ([DORA platform engineering capability](https://dora.dev/capabilities/platform-engineering/)).

## Second-order effects map

The map distinguishes a likely first-order move from two or three consequences that follow if it persists. Arrows express a hypothesis to test, not a deterministic claim.

| Branch | First-order change | Two or three downstream effects | Evidence and disagreement |
|---|---|---|---|
| **Market structure** | MCP and A2A make tool and agent communication more standardized and are placed under neutral foundations. | **1.** Basic provider/tool connectivity becomes easier to substitute, so vendors compete higher in the stack on managed state, evaluation, identity, policy, and operating experience. **2.** Control can migrate from a proprietary API to the dominant SDK, registry, conformance suite, or gateway. **3.** Smaller vendors gain access to common interfaces, while organizations with influence over specifications gain agenda-setting power. | Anthropic reported more than 10,000 active public MCP servers and donated MCP to the Linux Foundation's AAIF ([Anthropic](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation)); the Linux Foundation reported A2A support from more than 150 organizations and cross-cloud integration ([A2A announcement](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year)). The counterweight is governance concentration: LFX says two organizations account for more than half of A2A contributions ([LFX Insights](https://insights.linuxfoundation.org/project/agent2agent-a2a-protocol)). Neutral ownership therefore reduces one kind of capture without proving balanced implementation power. |
| **Regulatory ripple** | EU enforcement makes disclosure and, later, high-risk evidence operational rather than aspirational. | **1.** Purpose, owner, model binding, logs, oversight, and incident evidence become contract fields or linked artifacts. **2.** Procurement and audit teams ask for evidence packages that survive vendor changes. **3.** If evidence collection exists only in a central gateway/runtime, compliance makes the nominal paved road a de facto mandate. | The Commission lists logging, documentation, human oversight, robustness, cybersecurity, and accuracy among high-risk duties ([AI Act framework](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)). The implication for contract fields is an inference, not a prescribed implementation. The architecture choice remains open: common evidence formats can preserve choice, while runtime-only evidence can narrow it. |
| **Talent and decision rights** | Platform work shifts from building one agent framework toward maintaining contracts, adapters, evaluation, identity, and exit mechanisms. | **1.** Platform engineers become interface and evidence stewards; product engineers retain workflow semantics. **2.** Security, legal, platform, and product teams need explicit decision rights or exception work bounces among them. **3.** If teams stop exercising provider/runtime choices, local migration skill atrophies and theoretical freedom becomes dependence on the platform team. | DORA argues for extensible platforms and developer independence, while warning about gatekeeping and ticket-ops ([DORA](https://dora.dev/capabilities/platform-engineering/)). A current ExperiencedDevs thread describes AI governance moving among security, legal, and engineering, but another respondent reports a workable split where central IT selects allowed providers and divisions choose workflows ([community thread](https://www.reddit.com/r/ExperiencedDevs/comments/1rtlyww/who_owns_ai_governance_at_your_company/)). These are anecdotes, useful for identifying failure modes but not prevalence estimates. |
| **Adjacent industries** | Interoperability creates demand for conformance, identity, evaluation, registries, and protocol-aware security. | **1.** Independent test suites and compatibility labs become more valuable than another universal wrapper. **2.** Identity and authorization providers extend from human/workload identities to agents acting for people and organizations. **3.** Observability and incident tools compete on cross-provider traces and evidence portability. | NIST's initiative explicitly targets industry-led standards, community protocols, agent identity, and security evaluation ([NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)). The MCP community's SDK-tiering proposal cites uncertain feature support, maintenance, and version timelines and proposes conformance testing ([MCP SEP-1730](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1730)). The latter is community governance work, not a completed guarantee. |
| **Geopolitical posture** | The EU and US pursue interoperability through different policy frames. | **1.** Multinational organizations maintain jurisdictional policy profiles on top of a shared technical contract. **2.** “Open” agent protocols become strategic infrastructure, not merely developer convenience. **3.** Divergent evidence, identity, and sovereignty requirements increase adapter and assurance work even if wire protocols converge. | EU materials frame AI policy around safety, fundamental rights, and European industrial capacity ([European Commission](https://digital-strategy.ec.europa.eu/en/policies/guidelines-ai-high-risk-systems)); NIST frames its agent initiative around industry-led standards, open protocols, secure adoption, and US leadership ([NIST](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)). The divergence is one of emphasis; it does not yet prove incompatible technical requirements. |
| **Public narrative** | “AI platform as accelerator” competes with “platform as golden cage” and “AI as downstream disorder.” | **1.** Leaders increasingly judge platforms by stable delivery and recovery, not code-generation volume or enrollment. **2.** Engineers ask who owns generated systems, incidents, and long-term maintenance. **3.** A security failure can swing the narrative toward central mandates even if the cause was weak local controls rather than local ownership itself. | DORA's survey of nearly 5,000 technology professionals reports a correlation between high-quality internal platforms and AI benefit, while also reporting low or no trust in AI-generated code among 30% of respondents ([2025 DORA report](https://cloud.google.com/blog/products/ai-machine-learning/announcing-the-2025-dora-report)). In an ExperiencedDevs discussion, engineers describe non-engineers creating software while developers inherit review and operational responsibility; another participant advocates sandboxing, controls, and monitoring rather than a blanket ban ([community thread](https://www.reddit.com/r/ExperiencedDevs/comments/1ssdsq5/everyone_in_the_company_is_an_engineer_now_any/)). Survey correlation and self-selected anecdotes answer different questions; neither establishes that a particular platform architecture works. |

The important feedback loop is organizational: more adoption creates more shared evidence and lower marginal integration cost, which makes the platform politically harder to leave; that dependence justifies more staffing and controls, which increases the platform's scope and blast radius. The loop is beneficial only while verified exit cost and total operator work remain low. Adoption by itself cannot distinguish compounding leverage from compounding dependency.

## Four scenarios

The probability buckets are qualitative and refer to the next 12 months from 2026-07-31. They are not additive point estimates.

### Base — Thin contract, thick adapters

**Probability bucket: Plausible (35–55%).** The most likely middle path is a repository-owned contract for owner, purpose, permissions, data boundaries, acceptance tests, telemetry, and provider/runtime bindings, plus provider-specific adapters that remain explicit. The contract is portable; advanced capabilities are not presumed interchangeable.

**Why this bucket:** Vendor shutdowns make migration unavoidable, while the active rewrite of MCP's wire protocol shows that even an open standard remains a moving dependency. The MCP Go SDK describes the 2026-07-28 protocol as a largely rewritten stateless model but preserves backward compatibility and version negotiation ([MCP Go SDK release](https://github.com/modelcontextprotocol/go-sdk/releases)). That combination favors compatibility layers and staged migration over either complete centralization or effortless plug-and-play.

**Falsifiable triggers:** At least one real workflow passes the same repository-owned acceptance suite through two provider/runtime paths; provider shutdowns require adapter and binding changes but no rewrite of workflow purpose or controls; teams can opt out while still producing the required evidence. Falsified if the second implementation needs a different task contract, central approval dominates elapsed migration time, or provider-hosted state cannot be exported or reconstructed.

**Six-to-twelve-month indicators:** share of contract fields unchanged across implementations; verified exit lead time; operator hours per migration; count of provider-specific assets; exception turnaround; whether protocol upgrades are negotiated or become coordinated flag days.

**Effects:** Teams retain meaningful workflow choice but pay the honest cost of adapters and capability-specific tests. The platform team stays focused on schema stewardship, conformance, and common evidence instead of owning execution. Some duplicated provider code remains; that duplication is the price of avoiding a lowest-common-denominator runtime.

### Upside — Exercised portability becomes routine

**Probability bucket: Modest (15–35%).** Open protocols, independent evaluation artifacts, existing identity/observability systems, and small adapters make a provider or framework change an ordinary delivery event rather than a migration program.

**Why this bucket:** MCP and A2A have broad vendor participation and neutral-foundation governance ([MCP donation](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation), [A2A](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year)), and NIST is explicitly supporting open, interoperable agent protocols. Yet current SDK feature/version uncertainty and rapid hosted-product retirements make this better outcome possible rather than likely.

**Falsifiable triggers:** Two materially different workflows complete provider/runtime exit drills without changing mandatory control semantics; conformance tests cover the subset actually used; teams voluntarily retain the platform after a credible opt-out; platform operator toil per team falls while delivery stability does not deteriorate. Falsified if adoption depends on mandate, exit tests are demos with no production-shaped state, or shared controls need vendor-specific rewrites.

**Six-to-twelve-month indicators:** repeated successful drills; lower verified exit lead time; portable eval cases and trace schemas; stable platform staffing despite more consumers; low exception latency; contribution of adapters and validators by consuming teams rather than only the platform team.

**Effects:** Model and framework vendors compete on outcomes because switching is credible. Smaller teams gain controls they could not afford alone. Organizational learning compounds through shared tests and incident evidence while teams retain authority over workflow design.

### Downside — Compliance hardens the paved road into a golden cage

**Probability bucket: Modest (15–35%).** Under deadline pressure, the organization centralizes prompts, evals, agent definitions, routing, credentials, and logs in one managed runtime because it is the fastest route to a common audit story. The platform is nominally optional, but budgets, support, and approvals make alternatives impractical.

**Why this bucket:** EU evidence obligations are real, NIST respondents widely describe agent security as a barrier to adoption ([NIST AI 800-5](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai)), and community reports already describe unclear governance or stricter central scanning. DORA warns that ivory-tower, one-size-fits-all, and ticket-ops platforms produce disempowerment and shadow workarounds ([DORA](https://dora.dev/capabilities/platform-engineering/)).

**Falsifiable triggers:** Mandatory evidence is available only through the central runtime; exception approval exceeds the technical change time; hosted prompt/eval/agent objects outnumber repository-owned artifacts; teams stop maintaining alternate paths. Falsified if non-platform implementations can submit equivalent evidence automatically and routinely receive support.

**Six-to-twelve-month indicators:** growth in ticket queues and central operator headcount; rising provider-specific schema fields; fewer tested adapters; increasing shadow API keys or unregistered agents; platform incidents with organization-wide blast radius; adoption rising while satisfaction and delivery stability fall.

**Effects:** Audit preparation may initially become cheaper and incident response more uniform, but platform outages and policy errors affect more teams. Product engineers lose migration knowledge. The cost of leaving grows until the organization treats centralization as a safety requirement, even when an evidence-level control would have been sufficient.

### Wildcard — Agent identity and attestation become the new control plane

**Probability bucket: Low (<15%).** A major cross-agent security incident or a rapid standards breakthrough moves the center of gravity away from model gateways toward cryptographically verifiable agent identity, delegated authority, signed capability manifests, and portable execution attestations.

**Why this bucket:** NIST is researching agent authentication and identity and developing security evaluations, but has announced future guidelines and deliverables rather than a settled standard ([NIST initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)). NIST's RFI summary says respondents widely agreed that existing cybersecurity practices need adaptation for agent-specific threats ([NIST AI 800-5](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai)). A2A already requires agents to declare supported protocols and authentication in an AgentCard, but that is not yet a universal enterprise trust fabric ([A2A specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)).

**Falsifiable triggers:** A recognized standard or major procurement regime requires interoperable agent identity/authorization or signed attestations, and at least two independent runtimes implement it; alternatively, a material incident makes such evidence a purchasing requirement. Falsified if identity remains proprietary to cloud/runtime control planes or standards work produces guidance without interoperable implementations.

**Six-to-twelve-month indicators:** NIST deliverables; production implementations of agent identity profiles; signed AgentCards or capability manifests; procurement language requiring portable attestations; cross-provider incident traces; conformance suites that validate delegated authority rather than only message syntax.

**Effects:** If identity and evidence travel with the agent contract, runtime choice expands. If one enterprise certificate, directory, or gateway becomes the only trusted issuer, the new control plane creates a different and potentially stronger lock-in. The platform's smallest useful core would shift from a model contract toward identity, delegation, and evidence verification.

## The single 90-day signal

Measure **verified exit lead time** for one production-shaped workflow by 2026-10-29.

Start the clock when the current provider/runtime is declared unavailable. Stop it when the same repository-owned task contract and mandatory control checks pass through an independently operated alternative provider and, where feasible, an alternative agent framework. Adapter and binding changes are allowed; weakening acceptance thresholds, omitting required evidence, or rewriting the workflow's purpose is not. Publish elapsed business time, with engineer hours, platform-operator hours, approvals, feature loss, and unrecoverable provider state as explanatory receipts.

The single headline number is elapsed exit lead time. It is useful because it includes technical, organizational, governance, and support friction rather than rewarding an abstraction that merely compiles. A first measurement is a baseline, not a universal pass threshold. Repeat the drill quarterly and ask whether the number and its operator burden decline. OpenAI's announced retirement of the Assistants API, prompts, Evals, and Agent Builder supplies realistic failure modes; DORA's focus on delivery, recovery, and developer experience supports measuring system outcomes rather than enrollment ([OpenAI](https://developers.openai.com/api/docs/deprecations), [DORA](https://dora.dev/capabilities/platform-engineering/)).

If no second path can be completed in 90 days, that is still a result: the platform does not yet preserve practical freedom for that workflow. Record the blocking layer instead of redefining portability.

## What current coverage is most under-pricing

The under-priced cost is **portability decay**: the recurring work required to keep an exit path true after the first successful demo.

Open standards and pinned model identifiers help, but neither freezes the surrounding system. MCP's 2026-07-28 release largely rewrote the wire protocol while adding negotiation and compatibility behavior ([MCP Go SDK](https://github.com/modelcontextprotocol/go-sdk/releases)). The MCP SDK community separately identified uncertainty in feature support, maintenance commitments, and implementation timelines ([SEP-1730](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1730)). Anthropic guarantees fixed weights/configuration for a pinned model ID yet notes that routing, safety classifiers, and sampling infrastructure can still cause observable behavioral differences ([Anthropic model versioning](https://platform.claude.com/docs/en/about-claude/models/model-ids-and-versions)). OpenAI's notice policy can be as short as two weeks for preview models, at least three months for specialized variants, and at least six months for generally available models absent safety or compliance needs ([OpenAI deprecations](https://developers.openai.com/api/docs/deprecations)).

The consequence is that freedom is not an architectural property established once. It is an operated capability: alternate credentials stay valid, evaluation sets stay representative, adapters track protocol versions, data can still be exported, people remember the procedure, and governance accepts equivalent evidence from the alternate path. A “small” platform that does not budget those drills can be inexpensive only because its exit liability is off the books.

This also explains an apparent disagreement in current coverage. Foundation and vendor announcements reasonably celebrate rapid protocol adoption; maintainers simultaneously propose SDK tiers and conformance tests because adoption does not guarantee equivalent implementations. Both can be true. The chapter should therefore treat “uses an open standard” as a useful input and “completed a recent exit drill” as the evidence.

## Watch list

Review external sources monthly and internal metrics at least quarterly. A watch item should trigger a contract or control review only when it affects a used capability; following every ecosystem change would itself create platform toil.

1. **OpenAI API deprecations:** shutdown dates, replacement APIs, and notice-period changes — [register](https://developers.openai.com/api/docs/deprecations).
2. **Anthropic model deprecations:** active, deprecated, retirement, and partner-platform differences — [register](https://platform.claude.com/docs/en/about-claude/model-deprecations).
3. **Anthropic model versioning:** changes to pinned-ID and serving-infrastructure guarantees — [documentation](https://platform.claude.com/docs/en/about-claude/models/model-ids-and-versions).
4. **MCP specification and SEPs:** breaking protocol proposals, version negotiation, tool versioning, security, and governance — [repository issues](https://github.com/modelcontextprotocol/modelcontextprotocol/issues).
5. **MCP official SDK releases and tiering:** version lag, compatibility windows, conformance coverage, and maintainer commitments — [SDK tier proposal](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1730).
6. **A2A roadmap and specification:** interoperability specification, registries, testing, security, and deployment practices — [Linux Foundation update](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year).
7. **A2A project health:** contributor and organization dependency, retention, and security controls — [LFX Insights](https://insights.linuxfoundation.org/project/agent2agent-a2a-protocol).
8. **Agentic AI Foundation:** governance changes and new foundational projects around MCP and agent contracts — [AAIF/MCP announcement](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation).
9. **OpenTelemetry compatibility and GenAI semantic conventions:** deprecations, stability level, and whether traces remain comparable across providers — [OpenCensus compatibility notice](https://opentelemetry.io/blog/2026/deprecating-opencensus-compatibility/).
10. **NIST AI Agent Standards Initiative:** security, identity, evaluation, guidelines, RFIs, and convenings — [initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative).
11. **NIST AI 800-series:** agent-security findings and changes in the threat/evaluation baseline — [AI 800-5](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai).
12. **EU AI Act implementation:** transparency enforcement, final high-risk classification guidance, standardization, and timetable changes — [Commission framework](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai).
13. **DORA platform evidence:** platform quality, delivery stability, recovery, developer independence, and satisfaction — [capability page](https://dora.dev/capabilities/platform-engineering/) and [2025 report](https://dora.dev/research/2025/dora-report/).
14. **Verified exit lead time:** elapsed business time for the most recent production-shaped provider/runtime drill, plus operator-hour receipts.
15. **Portable contract ratio:** share of task/control contract fields that remain unchanged across two independently operated implementations; review every provider or framework change.
16. **Provider-specific asset inventory:** prompts, evals, vector stores, fine-tunes, conversation state, tool definitions, and logs that cannot be reconstructed from repository-owned sources.
17. **Exception service level:** median and tail time from opt-out request to decision, separated into policy, legal, security, and implementation wait.
18. **Total platform work:** platform operator/support/incident/migration hours plus consuming-team integration and workaround hours, not central-team cost alone.
19. **Voluntary retention and re-entry:** teams that could opt out but stay, teams that leave, and teams that later return; do not count forced enrollment as adoption evidence.
20. **Bypass and blast-radius events:** shadow keys, unregistered agents, missing traces, central-control outages, and policy mistakes affecting multiple workflows.

## Source receipts

### Calendar

- [OpenAI API deprecations](https://developers.openai.com/api/docs/deprecations) — dated model, API, prompt, eval, fine-tuning, and Agent Builder shutdowns; also notice-period policy.
- [Anthropic model deprecations](https://platform.claude.com/docs/en/about-claude/model-deprecations) — 2026-08-05 retirement and at-least-60-day public-model notice policy.
- [European Commission: AI Omnibus enters into force](https://digital-strategy.ec.europa.eu/en/news/ai-omnibus-enters-force) — 2027-12-02 and 2028-08-02 high-risk application dates.
- [European Commission: high-risk guidelines](https://digital-strategy.ec.europa.eu/en/policies/guidelines-ai-high-risk-systems) — 2026-08-02 enforcement/transparency start and current guideline status.
- [OpenTelemetry OpenCensus compatibility deprecation](https://opentelemetry.io/blog/2026/deprecating-opencensus-compatibility/) — staged deprecation in the source-supplied month window `2026-06 (exact day not stated)` and a no-earlier-than `2027-06 (exact day not stated)` removal window.

### Forecast

- [NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative) — announced work on industry standards, open protocols, identity, and evaluations; deliverables remain prospective.
- [Linux Foundation A2A one-year update](https://www.linuxfoundation.org/press/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year) — stated roadmap for interoperability, registry consolidation, testing/tooling, security, and deployment practices.
- [Anthropic/AAIF MCP announcement](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation) — governance direction and ecosystem claims for MCP.
- [DORA platform engineering capability](https://dora.dev/capabilities/platform-engineering/) — recommended minimum viable, extensible platform and balanced measurement model.

### Filing

- [European Commission AI Act framework](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — official risk categories, transparency, and high-risk obligations.
- [European Commission AI Omnibus notice](https://digital-strategy.ec.europa.eu/en/news/ai-omnibus-enters-force) — official record of the changed enforcement timetable and expanded oversight/sandboxes.
- [NIST AI 800-5](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai) — official synthesis of security RFI responses.

### Analyst

- [2025 DORA report announcement](https://cloud.google.com/blog/products/ai-machine-learning/announcing-the-2025-dora-report) — survey and interview findings on AI adoption, trust, platform quality, and delivery stability; a Google-led research program, so correlations should not be read as independent causal proof.
- [DORA platform engineering capability](https://dora.dev/capabilities/platform-engineering/) — platform antipatterns and outcome metrics.
- [LFX A2A Insights](https://insights.linuxfoundation.org/project/agent2agent-a2a-protocol) — project health and contributor/organization dependency indicators; these are ecosystem-health metrics, not proof of protocol interoperability.

### Community

- [MCP Go SDK 2026-07-28 release](https://github.com/modelcontextprotocol/go-sdk/releases) — maintainer record of a largely rewritten wire protocol, compatibility, and negotiation behavior.
- [MCP SEP-1730: SDK tiering](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1730) — community proposal documenting feature, maintenance, and version-support uncertainty.
- [MCP SEP-1766: digest-pinned tool versioning](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1766) — proposal motivated by breaking tool changes in agent workflows; not an adopted universal solution.
- [ExperiencedDevs: AI governance ownership](https://www.reddit.com/r/ExperiencedDevs/comments/1rtlyww/who_owns_ai_governance_at_your_company/) — conflicting practitioner anecdotes about fragmented ownership versus central provider controls with local workflow freedom.
- [ExperiencedDevs: non-engineers creating software](https://www.reddit.com/r/ExperiencedDevs/comments/1ssdsq5/everyone_in_the_company_is_an_engineer_now_any/) — practitioner concerns about inherited review/operations and a counterproposal centered on sandboxing, controls, and monitoring. Self-selected anecdotes are treated as hypotheses, not representative statistics.
