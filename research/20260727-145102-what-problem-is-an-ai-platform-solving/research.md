# The Control Plane After the Prototype — Research Dossier

**Question:** What problem is an AI platform actually solving?
**Last updated:** 2026-07-27

## The Story in One Paragraph

Studies and practitioner communities support a narrower answer than the market does. An AI platform does not solve “AI adoption,” weak problem selection, bad data, missing domain ownership, or the absence of a valuable workflow. It can solve four different candidate problems, only three of which are primarily technical or organizational: **technical lifecycle repetition** when teams repeatedly rebuild deployment, evaluation, tracing, lineage, and incident machinery; **cross-team coordination** when model, data, product, security, finance, and operations work has no shared interface; **governance and accountability** when an organization cannot consistently control access, assign cost, preserve evidence, or contain an autonomous action; and **vendor procurement and consolidation** when buyers or suppliers want one catalogue, contract, control plane, and bill. The first three become real after several valuable production systems expose the same friction. The fourth can simplify purchasing while also serving vendor bundling and lock-in. The most defensible platform is therefore a thin, composable operational layer with stable contracts and escape hatches—not necessarily an end-to-end suite. It earns its cost when it makes the normal path, the exception, the incident, and the exit cheaper. It is unnecessary or harmful when there is one team or use case, no repeated bottleneck, an existing developer platform can be extended, business ownership is unresolved, or centralization creates a queue, premature abstraction, false compliance confidence, or dependency on one vendor. Crucially, adoption, platform activity, and user satisfaction are not causal proof of business value.

## Cast

| Named actor | Role and stake | Public position | Most recent material action |
|---|---|---|---|
| **UK Department for Science, Innovation and Technology (DSIT)** | Government department responsible for evidence and policy on business AI adoption; its programme choices depend on diagnosing barriers correctly. | Need, skills, data practice, and integration matter alongside tools; its surveys do not make a platform a universal prerequisite. | Published the UK Business Data Survey on **2026-06-18** ([DSIT](https://www.gov.uk/government/statistics/uk-business-data-survey-2026/uk-business-data-survey-2026)). |
| **European Commission / European AI Office** | Rule-maker and central GPAI supervisor with a stake in reusable evidence across providers and deployers. | Duties follow actor role and use, not a supplier's “platform” label. | Published Article 50 transparency guidelines on **2026-07-20** before obligations applying on **2026-08-02** ([Commission](https://digital-strategy.ec.europa.eu/en/news/commission-publishes-guidelines-transparency-obligations-providers-and-deployers-certain-ai-systems)). |
| **UK Competition and Markets Authority (CMA)** | Cloud-market regulator with statutory responsibility for switching, interoperability, and competition in infrastructure used by AI platforms. | Amazon and Microsoft have significant cloud market power; egress and interoperability can restrict switching and multi-cloud. | Announced a cloud and business-software action package on **2026-03-31** ([CMA](https://www.gov.uk/government/news/cma-announces-package-of-actions-on-business-software-and-cloud-services)). |
| **US Federal Trade Commission (FTC)** | Competition regulator examining cloud–model partnerships and downstream market effects. | Investment partnerships can combine control, information, integration, exclusivity, revenue-sharing, and cloud-spend commitments. | Released its staff report on Microsoft–OpenAI, Amazon–Anthropic, and Alphabet–Anthropic partnerships on **2025-01-17** ([FTC](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study)). |
| **Cloud Native Computing Foundation (CNCF) and SlashData** | Foundation and research partner mapping platform architecture and ownership, with an ecosystem stake in cloud-native infrastructure. | Hybrid, dedicated, extended-developer-platform, and vendor patterns coexist; ownership is also heterogeneous. | Published the Q1 Technology Radar on **2026-03-24** ([CNCF](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf)). |
| **Stack Overflow** | Developer community and survey publisher with a stake in developer workflow, trust, and practical tooling. | AI use is widespread among respondents, but distrust, rework, and weak collaboration gains remain; many builders reuse ordinary observability tools. | Released its 2025 Developer Survey on **2025-07-29** ([Stack Overflow](https://stackoverflow.co/company/press/archive/stack-overflow-2025-developer-survey/)). |
| **KPMG** | Consultancy selling AI strategy, implementation, governance, and operating-model work. | Large organizations report strategy and scaling far more often than established ROI; KPMG argues that governance and operating-model integration distinguish leaders. | Released Global AI Pulse Q1 2026 on **2026-03-31** ([KPMG](https://assets.kpmg.com/content/dam/kpmgsites/xx/pdf/2026/04/global-ai-pulse.pdf.coredownload.pdf)). |
| **IBM and Oxford Economics** | IBM sells platforms, infrastructure, governance, and consulting; Oxford Economics supplied the research partnership. | Enterprise deployment is outrunning governance, incident, and spend visibility; stronger control is presented as the remedy. | Published the enterprise AI control-gap study on **2026-06-08** ([IBM](https://newsroom.ibm.com/2026-06-08-new-ibm-study-finds-cios-and-ctos-face-growing-ai-control-gap-as-enterprise-deployment-scales?asPDF=1&lnk=hpln1id)). |
| **International Energy Agency (IEA)** | Intergovernmental energy analyst concerned with energy security, grids, and infrastructure forecasting. | AI's software abstraction rests on rapidly growing and geographically concentrated physical demand. | Updated *Key Questions on Energy and AI* on **2026-04-16** ([IEA](https://www.iea.org/reports/key-questions-on-energy-and-ai/executive-summary)). |
| **International Labour Organization (ILO)** | UN labour agency examining job quality, autonomy, distribution, and social dialogue. | Task-level time savings are uneven and do not automatically become organizational productivity or better work. | Published its empirical GenAI evidence review on **2026-06-01** ([ILO](https://www.ilo.org/publications/impact-genai-jobs-productivity-and-work-organization-review-empirical)). |

## Timeline

| Date | Event | Why it matters to the present question |
|---|---|---|
| **2009-11-11** | The first DevOpsDays was publicly recapped after bringing developers and infrastructure operators into one conversation ([DevOpsDays](https://devopsdays.org/blog/2009/11/11/devopsdays-2009-belgium-a-great-success/)). | Established the durable lesson that delivery is a cross-functional operating system, not a tool purchase. |
| **2011-09-28** | NIST published its cloud-computing definition, including PaaS, self-service, pooling, elasticity, and measured service ([NIST SP 800-145](https://www.nist.gov/publications/nist-definition-cloud-computing)). | Supplied the managed-platform template and, in later guidance, an explicit portability warning. |
| **2014-06-06** | The first Kubernetes commit began a portable declarative control plane for container infrastructure ([Kubernetes history](https://kubernetes.io/blog/2024/06/06/10-years-of-kubernetes/)). | Showed that a common control plane can hide infrastructure differences without eliminating the need for a higher-level developer experience. |
| **2017-09-05** | Uber introduced Michelangelo, its internal ML-as-a-service platform ([Uber](https://www.uber.com/bd/en/blog/michelangelo-machine-learning-platform/)). | Made the AI-platform case concrete: teams had inconsistent tools, bespoke production systems, and no reproducible end-to-end lifecycle. Uber later added escape hatches when its abstractions constrained new model types. |
| **2019-05-20** | Thoughtworks published the completed data-mesh argument against a centralized data-platform monolith ([Dehghani](https://martinfowler.com/articles/data-monolith-to-mesh.html)). | Reframed a platform as shared self-service infrastructure with domain ownership, rather than centralized ownership of every artifact. |
| **2020-03-16** | Spotify open-sourced Backstage ([Backstage](https://backstage.io/blog/2020/03/16/announcing-backstage/)). | Demonstrated a common front door and plugin ecosystem over heterogeneous tools, a useful precedent for a composable AI platform. |
| **2021-01-13** | CIDR scheduled the lakehouse paper presentation for this day during its 2021-01-11–2021-01-15 virtual conference. **Date caveat:** the official programme supports the presentation date; the paper's exact publication day is not established ([CIDR programme](https://www.cidrdb.org/cidr2021/program.html); [paper](https://www.vldb.org/cidrdb/2021/lakehouse-a-new-generation-of-open-platforms-that-unify-data-warehousing-and-advanced-analytics.html)). | Captured the opposing commercial logic: technical reunification can reduce duplication while increasing control-plane gravity. |
| **2021-05-18** | Google Cloud launched Vertex AI as a unified MLOps platform ([Google Cloud](https://cloud.google.com/blog/products/ai-machine-learning/google-cloud-launches-vertex-ai-unified-platform-for-mlops)). | Turned manually assembled point solutions into a hyperscaler catalogue, API, and lifecycle control plane. |
| **2023-11-01** | CNCF released a platform-engineering maturity model ([CNCF](https://tag-app-delivery.cncf.io/blog/announcing-the-platform-engineering-maturity-model/)). | Formalized “platform as a product”: adoption must be earned through user and business outcomes, not infrastructure coverage. |
| **2024-07-26** | NIST published its Generative AI Profile ([NIST AI 600-1](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence)). | Made explicit that generative systems add risks and evidence needs across the lifecycle; governance cannot be reduced to model access. |
| **2025-01-17** | The FTC released its staff report on major cloud–AI partnerships ([FTC](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study)). | Documented equity, cloud-spend commitments, information rights, exclusivity, and revenue-sharing structures behind apparently neutral platform choices. |
| **2026-03-24** | CNCF/SlashData published a survey in which hybrid and extended-platform architectures were more common than dedicated AI platforms ([CNCF](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf)). | Current practice points toward federation, not one universal AI operating system. |
| **2026-08-02** | The EU AI Act becomes generally applicable, including Article 50 transparency obligations ([European Commission](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)). | Provides an immediate test of whether a shared layer can turn cross-cutting legal duties into reusable controls and portable evidence. |

The older history matters. CASE environments, centralized data lakes, GE Predix, and IBM Watson Health all show variants of the same failure: integrated tooling did not create process fit, domain evidence, data ownership, adoption, or a coherent operating model. CASE research found that the same tool could succeed in one organization and be abandoned in another because training, staff acceptance, management support, process fit, and integration differed ([Rahim, Khan, and Selamat](https://doi.org/10.1108/09593849710194696)). A platform is an adoption system as much as a technical system.

## Geography and Jurisdiction

| Geography / regime | Why it changes the platform problem |
|---|---|
| **European Union** | Obligations follow actor role and use, not the vendor’s “platform” label. The AI Act places documentation, logging, human-oversight, transparency, incident, and post-market duties across providers and deployers, including some actors outside the EU when outputs are used inside it ([Regulation (EU) 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)). A platform can centralize evidence; it cannot transfer legal responsibility. |
| **United Kingdom** | Official adoption evidence says need and skills often precede tooling. The UK survey found 71% cited no identified need and 60% limited skills, while lack of tools/platforms was a prior barrier for 40% of current adopters ([DSIT, updated 2026-02-13](https://www.gov.uk/government/publications/ai-adoption-research/ai-adoption-research)). The CMA’s cloud work also makes interoperability and exit a procurement issue. |
| **United States** | NIST’s AI RMF and Generative AI Profile are voluntary cross-sector resources, while sector regulators, procurement rules, state law, and courts add binding requirements. A platform may implement a common control language, but the organization still sets risk tolerance and assigns owners. |
| **Global infrastructure** | AI abstraction rests on geographically concentrated compute, chips, networks, and energy. The IEA estimated the United States held 45% of data-centre electricity use in the 2024 reporting year, China 25%, and Europe 15% ([IEA, 2025-04-10](https://www.iea.org/reports/energy-and-ai/executive-summary%C2%A0)). A “sovereign” control plane is not sovereign if its upstream supply and exit routes are not. |

## By the Numbers

These numbers answer different questions. Official enterprise statistics, voluntary developer surveys, cloud-native community surveys, vendor-sponsored executive surveys, prices, and review sentiment must not be collapsed into one adoption or value claim.

### Adoption and need

1. **20.2%** of firms in OECD countries with available data reported AI use in the 2025 reporting year, up from **14.2%** in 2024 and **8.7%** in 2023. Adoption was **52.0%** among large firms and **17.4%** among small firms ([OECD, 2026-01-28](https://www.oecd.org/en/about/news/announcements/2026/01/ai-use-by-individuals-surges-across-the-oecd-as-adoption-by-firms-continues-to-expand.html)). This motivates—but does not prove—the hypothesis that platform fixed costs are easier to spread at enterprise scale.
2. In the UK’s representative **3,500-business** survey, **16%** used at least one AI technology and **80%** neither used nor planned to use one. “No identified need” at **71%** and limited skills at **60%** outranked the platform gap ([DSIT](https://www.gov.uk/government/publications/ai-adoption-research/ai-adoption-research)).
3. Only **21%** of AI-using UK businesses had AI tools integrated into existing business systems. Integrated users had more developed data practices, but this observational survey cannot show that integration caused those practices ([DSIT, 2026-06-18](https://www.gov.uk/government/statistics/uk-business-data-survey-2026/uk-business-data-survey-2026)).

### Architecture and ownership

4. Among **364** CNCF/SlashData respondents integrating AI workflows, **35%** used separate experimentation with shared production deployment, **19%** a dedicated AI platform, **17%** an extension of an existing developer platform, **18%** primarily vendor platforms, and **5%** left infrastructure to AI teams. The plurality was hybrid, not monolithic ([CNCF, 2026-03-24](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf)).
5. In the same study, **41%** of **422** respondents said several DevOps/SRE/infrastructure teams collaboratively supplied platform capabilities; **28%** reported a dedicated platform team. This is consistent with the hypothesis that ownership and coordination can precede product selection; the community sample cannot establish that ordering for firms generally.

### Delivery, trust, and control

6. Stack Overflow received more than **49,000** responses across **177 countries**. Of respondents answering its AI questions, **84%** used or planned to use AI tools, but **46%** distrusted output accuracy versus **33%** who trusted it; **66%** cited “almost right” answers as a frustration ([Stack Overflow, 2025](https://survey.stackoverflow.co/2025/ai)). Access without verification does not solve the production problem.
7. Among Stack Overflow agent users, roughly **70%** reported task-time reduction and **69%** productivity improvement, but only **17%** reported better team collaboration. Individual acceleration and organizational coordination are different outcomes.
8. DORA’s observational 2025 analysis estimated that each **25%** increase in AI adoption was associated with **1.5% lower delivery throughput** and **7.2% lower delivery stability**, despite perceived individual benefits. DORA describes AI as an amplifier of the surrounding delivery system, not an automatic upgrade ([DORA](https://dora.dev/research/ai/gen-ai-report/dora-impact-of-generative-ai-in-software-development.pdf)).
9. IBM’s vendor-sponsored survey of **2,000** technology executives found **77%** said adoption was outpacing governance, **85%** lacked full real-time AI-spend visibility, and respondents reported an average of **54 agent incidents** in the prior year. These are self-reports, not independently audited incident data ([IBM, 2026-06-08](https://newsroom.ibm.com/2026-06-08-new-ibm-study-finds-cios-and-ctos-face-growing-ai-control-gap-as-enterprise-deployment-scales?asPDF=1&lnk=hpln1id)).

### Value and evidence quality

10. KPMG’s vendor-sponsored survey of **2,110** leaders at large organizations found **95%** had an AI strategy, **64%** reported “meaningful business value,” **39%** were scaling organization-wide, and only **8%** reported established ROI. Respondents planned an average **US$186 million** over the next twelve months ([KPMG, 2026-03-31](https://assets.kpmg.com/content/dam/kpmgsites/xx/pdf/2026/04/global-ai-pulse.pdf.coredownload.pdf)). Activity, sentiment, and established return are not equivalent.
11. A 2026 multivocal platform-engineering review included **88** sources, but only **2**, or **2.3%**, were tier-1 publications primarily about platform engineering; it found **zero peer-reviewed empirical effectiveness studies** for platform scorecards ([Anjum, 2026-05-04](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)).
12. A preprint examining more than **8,000 G2 reviews** found seven of nine MLOps practices associated with user satisfaction. Review selection and observational design mean the result supports useful practices among reviewers, not causal business value or an integrated-platform mandate ([Pasch, 2025-10-11](https://arxiv.org/abs/2510.09968)).
13. RAND interviewed **65** experienced data scientists and engineers. In the **50-person** failure-pattern counts, **30** raised persistent data-quality problems, **16** described technology-first behavior, and **10** raised missing domain understanding; misunderstanding project intent and purpose was the most common failure factor ([RAND](https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2600/RRA2680-1/RAND_RRA2680-1.pdf)). The categories overlap and are qualitative, but they block the inference that a high project-failure rate proves a platform deficit.

### Money and physical scale

14. Current platform pricing is a bundle of meters. AWS lists **US$0.21 per completed human-evaluation task** and **US$1 per 1,000 intelligent-routing requests**, before model and adjacent-service consumption ([AWS Bedrock pricing](https://aws.amazon.com/bedrock/pricing/)). Google lists Gemini 2.5 Pro at **US$1.25 per million input tokens** and **US$10 per million output tokens** at up to 200,000 input tokens, with separate grounding charges ([Vertex AI pricing](https://cloud.google.com/vertex-ai/generative-ai/pricing)).
15. Alphabet reported **US$91.4 billion** in 2025 capital expenditure and **US$149.1 billion** in purchase commitments and other obligations at 2025-12-31, mainly related to technical infrastructure, though not all was exclusively AI ([Alphabet 2025 Form 10-K](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm)).
16. The IEA estimated global data-centre electricity use at **485 TWh** in the 2025 reporting year and projects about **950 TWh** in 2030; it says AI-focused data-centre consumption rose **50%** in 2025 and could triple by 2030 ([IEA, 2026-04-16](https://www.iea.org/reports/key-questions-on-energy-and-ai/executive-summary)).

## How It Actually Works

An AI platform is best understood as a control system around an application—not as the application itself. It sits between product teams and a changing supply chain of models, data, tools, compute, evaluators, and policies.

### The operational loop

1. **A team declares intent and ownership.** The use case needs an accountable business owner, expected outcome, error tolerance, data boundary, and autonomy level. A platform can require these fields; it cannot invent them.
2. **The platform resolves dependencies.** Identity and policy determine which models, data, tools, regions, and budgets the workload may use. A catalogue without identity-aware entitlements is discovery, not governance.
3. **The system compiles an executable run.** Code, prompt, model, retrieved context, tool schema, permissions, runtime, and configuration become a versioned execution. Provider routing considers quality, latency, availability, policy, and cost—not merely the cheapest token.
4. **The run produces an artifact graph.** Reproducibility requires links among source data, model and prompt versions, retrieval corpus, tool calls, intermediate outputs, evaluations, deployment, approvals, and observed production behavior. A “save run” button without those relationships is incomplete.
5. **Evaluation makes a decision.** Offline and online evaluators, human review, red-team tests, and business metrics must be versioned with thresholds and consequences. An evaluation dashboard matters only if a result blocks, routes, escalates, rolls back, or changes a release decision.
6. **Observability joins semantic and operational evidence.** Ordinary latency, errors, saturation, and traces must connect to model choice, token use, retrieved context, tool actions, evaluator results, and user outcome. OpenTelemetry’s evolving GenAI conventions show both the promise and the privacy/cardinality difficulty ([OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/)).
7. **Governance acts at a boundary.** Policies become real at model access, data retrieval, deployment, tool invocation, human approval, spend threshold, or incident response. A static policy document outside those transitions cannot contain behavior.
8. **Operations learn—or merely accumulate logs.** Production evidence should update evaluations, thresholds, routing, prompts, data, and product design. Without an owner and feedback loop, the platform centralizes telemetry rather than learning.

### Capability test

| Candidate problem | Shared capability that can solve it | Evidence that it worked | Failure pattern |
|---|---|---|---|
| **Technical lifecycle repetition** | Reusable pipelines, artifact lineage, evaluation harnesses, deployment, rollback, monitoring, and incident tooling. | Local adapters and duplicate pipelines are retired; idea-to-production and recovery time fall. | The platform becomes one more layer while local glue remains. |
| **Cross-team coordination** | Stable contracts, self-service paths, service ownership, documentation, support, and explicit exception handling. | Teams complete common work without tickets; 95th-percentile exception time falls; platform adoption is voluntary. | A central queue replaces bilateral handoffs. |
| **Governance and accountability** | Identity, least privilege, policy enforcement, inventories, evaluation gates, cost attribution, evidence export, revocation, and human escalation. | An auditor or incident responder can reconstruct who authorized what, with which artifacts, and contain it quickly. | Dashboards are green but decisions cannot be reproduced and owners are unclear. |
| **Vendor procurement and consolidation** | One contract, marketplace, bill, support path, and model catalogue. | Total cost and switching time fall while provider choice remains credible. | Bundling obscures unit economics, committed spend shapes routing, and evidence or identity cannot leave. |

Security deserves special treatment because agents can act rather than merely predict. The platform must treat the model as an untrusted reasoner: give each agent a non-human identity, narrow and expiring delegated authority, typed tools, policy checks at execution, network and data boundaries, human approval for consequential transitions, and a revocation path. A generic prompt instruction is not an authorization control.

The architectural north star is a **stable operational layer with replaceable components above and below it**. That is what practitioners mean when they ask for routing, policy, telemetry, attribution, caching, observability, and evaluation while rejecting a monolith. The platform should standardize evidence and decision boundaries more strongly than it standardizes application logic.

## Money, Power, and Stakeholder Impact

The platform changes both the money flow and who can say yes.

### Where money moves

Amounts are stated only where a public schedule or filing supports them; otherwise they are **Unknown** or explicitly **n/a** rather than inferred.

| # | Payer → recipient | Directed flow | Amount / trigger | Source and significance |
|---:|---|---|---|---|
| 1 | Enterprise customer → hyperscaler AI platform | Inference, runtime, routing, guardrails, evaluation, retrieval, storage, and network consumption | Metered per token, task, request, capacity, or storage period; AWS examples include US$0.21/human-evaluation task and US$1/1,000 routing requests | [AWS pricing](https://aws.amazon.com/bedrock/pricing/). A “single platform” is economically a bundle of meters. |
| 2 | Enterprise customer → model developer, often through a marketplace | Token or provisioned-throughput fees | Model- and contract-dependent; public revenue share **Unknown** for the reviewed partnerships | [FTC, 2025-01-17](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study). Catalogue choice shapes distribution. |
| 3 | Cloud provider / investor → frontier-model developer | Equity, cash, compute discounts, and engineering resources | Multi-billion-dollar arrangements; confidential allocation **Unknown** | [FTC](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study) documents consultation, control, exclusivity, information, and revenue-sharing rights. |
| 4 | Frontier-model developer → cloud partner | Contracted cloud consumption funded partly by the partner's investment | **Unknown**; triggered by partnership consumption commitments | The [FTC](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study) found commitments to spend a large portion of a partner's investment on that partner's cloud. |
| 5 | Central technology budget → internal platform team | Salaries, on-call capacity, product management, support, and shared infrastructure | **Unknown**; annual budget and ongoing consumption | [CNCF, 2026-03-24](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf). “Build” converts licence spend into persistent staffing and service commitments. |
| 6 | Product team / business unit → central platform or cloud account | Chargeback or showback for calls, applications, environments, and experiments | **Unknown**; monthly allocation, quota, or threshold | [AWS cost management](https://docs.aws.amazon.com/bedrock/latest/userguide/cost-management.html) documents attribution by IAM principal, project, application, request, environment, or experiment. |
| 7 | Customer → open-source commercializer | Enterprise controls, support, private storage, and managed compute | Hugging Face lists Enterprise at US$50/month plus usage and private storage at US$8–12/TB/month on the retrieved page | [Hugging Face pricing](https://huggingface.co/pricing). Open access shifts monetization toward identity, support, storage, and compute. |
| 8 | Hyperscaler → chip, server, network, construction, grid, and energy suppliers | Capital equipment, inventory, leases, and energy contracts | Alphabet: US$91.4bn 2025 capex and US$149.1bn commitments at 2025-12-31, not all AI | [Alphabet Form 10-K](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm). Customer demand flows upstream into physical infrastructure. |
| 9 | Customer → human evaluators, data workers, and domain reviewers | Labels, red-teaming, preference data, benchmark and production review | AWS-mediated human evaluation US$0.21/task plus inference; other wages/margins **Unknown** | [AWS pricing](https://aws.amazon.com/bedrock/pricing/) and [ILO](https://www.ilo.org/publications/artificial-intelligence-adoption-and-its-impact-jobs). “Automated” evaluation still purchases human judgment. |
| 10 | Exiting or multi-homing customer → cloud provider, staff, and migration suppliers | Egress, duplicate operation, re-engineering, retraining, and exit work | Representative total **Unknown**; triggered by exit, renewal, or resilience test | [CMA case record](https://www.gov.uk/cma-cases/cloud-services-market-investigation) and [Microsoft's response](https://assets.publishing.service.gov.uk/media/67d1bea40c569e0d48fb0a6f/Microsoft_response_to_provisional_decision_1.pdf) disagree on the relative importance of egress versus operational switching cost. |
| 11 | Government → operator or customer | Subsidy, tax incentive, R&D grant, or procurement payment | **n/a at category level:** no programme, operator, or jurisdiction is defined | No representative transaction was established; assigning one to “AI platforms” would invent a flow. |
| 12 | Operator → government | Tax, supervisory fee, levy, or fine | **n/a at category level:** role, revenue, breach, and jurisdiction are unspecified | The [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689) creates enforcement exposure, but no operator-specific assessment is in scope. |
| 13 | Operator → customer, or customer → operator | Refund, service credit, rebate, claw-back, or termination fee | **n/a:** representative enterprise-contract clauses are not public | Public [AWS](https://aws.amazon.com/bedrock/pricing/), [Google](https://cloud.google.com/vertex-ai/generative-ai/pricing), and [Hugging Face](https://huggingface.co/pricing) schedules expose list meters, not negotiated reverse flows. |
| 14 | Customer/operator → insurer, bank, or hedge counterparty | E&O/cyber premium, interest, performance security, FX hedge, or swap | **n/a:** no representative policy, debt, hedge, or currency exposure was retrieved | These indirect flows may alter total cost and risk transfer, but a direction or amount without a named contract would be speculation. |

### Where authority moves

| Pivotal decision | Formal decider | Required approval sequence | Explicit veto | Soft influence | Reversal conditions | Source |
|---|---|---|---|---|---|---|
| Models/providers allowed | CIO/CTO or delegated AI-governance body with procurement and security | Product need → evaluation → security/privacy → contract → catalogue | CISO, DPO/privacy counsel, procurement, regulated risk owner within remit | Platform engineers, vendors, cloud account teams, finance, application teams | Incident, model or contract change, failed evaluation, sanction/export rule, portability review | [FTC](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study); [NIST](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) |
| Data/tools accessible | Data owner/controller and process owner; security/privacy for controls | Purpose → classification/legal basis → scope design → security/privacy approval → runtime grant | Data owner, CISO, DPO/privacy counsel, tool owner | Workers, users, domain experts, connector vendors, platform defaults | Purpose change, review, incident, owner withdrawal, expiry, reclassification | [DSIT](https://www.gov.uk/government/statistics/uk-business-data-survey-2026/uk-business-data-survey-2026); [EDPB](https://www.edpb.europa.eu/news/edpb-opinion-on-ai-models-gdpr-principles-support-responsible-ai_ga) |
| Evidence sufficient for production | Product owner plus applicable risk/security/legal approvers | Baseline/risk class → versioned evaluation → domain review → mandatory reviews → gate | Product owner for failed outcome; mandatory control owner for failed threshold; regulator where prior authorization applies | Platform authors defaults; vendors supply benchmarks; auditors and affected groups shape expectations | Drift, incident, artifact change, legal change, failed audit, exception expiry | [NIST](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/); [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689) |
| Capacity and budget | CFO and business sponsor, advised by technology leadership | Accountable use case → estimate → risk/capacity review → prioritization → quota | CFO/budget owner; capacity owner; business sponsor | Cloud vendors, telemetry, FinOps models, teams with easily measured outcomes | KPI miss, overrun, incident, capacity shortage, higher-value alternative, renewal | [IBM](https://newsroom.ibm.com/2026-06-08-new-ibm-study-finds-cios-and-ctos-face-growing-ai-control-gap-as-enterprise-deployment-scales?asPDF=1&lnk=hpln1id); [AWS](https://docs.aws.amazon.com/bedrock/latest/userguide/cost-management.html) |
| Exception or unlisted tool | Delegated architecture/risk owner under a published exception policy | Owner/request → rationale/compensating controls → mandatory reviews → time-bounded grant → expiry review | Every mandatory control owner affected by the exception | Platform capacity, vendor roadmap, peer teams, executive urgency | Expiry, missing control, incident, supported alternative, repeated demand, reclassification | [CNCF](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf); [NIST](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) |
| Provider exit | Executive sponsor, procurement, architecture, data owner, risk leadership | Trigger → inventory → legal/data review → portability test → duplicate run → acceptance → termination | Executive/budget owner; data owner; risk owner where continuity/evidence fails | Incumbent, alternative vendors, skills, committed spend, users, regulators | Failed drill, unacceptable outage/risk/cost, renegotiation, incumbent remediation | [CMA](https://www.gov.uk/cma-cases/cloud-services-market-investigation); [OECD](https://www.oecd.org/en/publications/competition-in-artificial-intelligence-infrastructure_623d1874-en/full-report/component-6.html) |

The central bargain is clear:

> Product teams give up some local model and tool agency in exchange for lower repeated integration cost, safer defaults, shared evidence, and organizational visibility.

That bargain is attractive to large, mature organizations with several production systems and regulated or high-consequence work. It is poor for a small firm asked to buy enterprise coordination before it has enterprise scale. It also creates under-recognized winners: FinOps, audit, identity, policy, existing observability teams, hyperscalers, and upstream infrastructure suppliers. Under-recognized losers include small providers outside approved catalogues, product teams constrained by central defaults, workers whose judgment is rendered as an input rather than a decision right, and communities hosting energy-intensive infrastructure.

### Stakeholder impact

| Stakeholder | Direction | Magnitude | Mechanism | Horizon | Source |
|---|---|---|---|---|---|
| Executives/business owners | Mixed | Material | Gain portfolio visibility and repeatable production paths; activity can substitute for workflow redesign and value measurement. | 6–18 months | [KPMG](https://assets.kpmg.com/content/dam/kpmgsites/xx/pdf/2026/04/global-ai-pulse.pdf.coredownload.pdf) |
| Platform/MLOps teams | Mixed | Material | Gain scope, reuse, and fleet visibility; inherit queue, support, abstraction, and common-outage risk. | Immediate–24 months | [CNCF](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf) |
| Product/application engineers | Mixed | Material | Supported paths retire glue; allowlists and exceptions can reduce autonomy and delay novel work. | Immediate–12 months | [Stack Overflow](https://survey.stackoverflow.co/2025/ai); [CNCF](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf) |
| Data scientists/ML engineers | Mixed | Material | Versioning, orchestration, registries, compute, and monitoring aid handoff; model-centric abstractions constrain experimentation. | 6–18 months | [Kreuzberger et al.](https://doi.org/10.1109/ACCESS.2023.3262138); [Amrit and Kolar](https://doi.org/10.1016/j.jik.2024.100637) |
| Security/privacy/legal/model risk | Wins / exposed | Material | Central controls increase leverage while centrally permitted failures increase accountability and false-confidence risk. | Immediate/continuous | [NIST](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/); [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689) |
| Finance/procurement | Wins / exposed | Material | Attribution and consolidated negotiation improve visibility; meters and commitments can obscure marginal cost and weaken exit. | Immediate–renewal | [AWS](https://docs.aws.amazon.com/bedrock/latest/userguide/cost-management.html); [FTC](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study) |
| Hyperscalers/integrated vendors | Wins | Material | Earn across compute, model, data, routing, evaluation, network, and governance; integration raises distribution and switching leverage. | 1–3 years | [FTC](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study); [Alphabet](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm) |
| Open-source maintainers/smaller providers | Exposed / mixed | Material | Can become portable components; integrated catalogues can exclude or commoditize them while support stays local. | 1–3 years | [OECD](https://www.oecd.org/en/publications/competition-in-artificial-intelligence-infrastructure_623d1874-en/full-report/component-6.html); [Hugging Face](https://huggingface.co/pricing) |
| SMEs/non-adopters | Exposed | Material | Managed controls can substitute for scarce skills, but enterprise fixed cost may precede any repeated coordination problem. | Immediate–24 months | [DSIT](https://www.gov.uk/government/publications/ai-adoption-research/ai-adoption-research); [OECD](https://www.oecd.org/en/about/news/announcements/2026/01/ai-use-by-individuals-surges-across-the-oecd-as-adoption-by-firms-continues-to-expand.html) |
| Workers/domain experts | Mixed / exposed | Material | Assistance and escalation may improve; monitoring, intensity, diminished discretion, and lost learning work may rise. | 1–5 years | [ILO](https://www.ilo.org/publications/impact-genai-jobs-productivity-and-work-organization-review-empirical); [OECD workplace](https://www.oecd.org/en/publications/using-ai-in-the-workplace_73d417f9-en.html) |
| End users/affected people | Mixed / exposed | Material; potentially existential per decision | Shared testing and remedy can improve accountability; common errors and weak thresholds scale. | Immediate/continuous | [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689); [NIST](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) |
| Grid operators/host communities | Exposed / mixed | Material | Investment grows while concentrated loads create connection, reliability, affordability, land, and water trade-offs. | 1–5 years | [IEA](https://www.iea.org/reports/key-questions-on-energy-and-ai/executive-summary) |
| Regulators/auditors | Mixed | Material | Standardized records improve legibility; private platform schemas can remain substantively incomplete. | 1–3 years | [Commission](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai); [ISO 42001](https://www.iso.org/standard/42001) |

## Counter-Narratives

### 1. The binding problem is problem selection, not production infrastructure

RAND found misunderstanding of intent and purpose more common than any other failure factor in its interviews; data quality, technology-first behavior, and missing domain knowledge also recurred ([RAND](https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2600/RRA2680-1/RAND_RRA2680-1.pdf)). A separate expert-interview study grouped AI-project failure factors across unrealistic expectations, use cases, organizational constraints, resources, and technical issues—not one missing-platform category ([Schlegel, Schuler, and Westenberger](https://aisel.aisnet.org/ijispm/vol11/iss3/3/)).

**Interest served:** business owners, domain experts, workers, and product teams benefit when attention returns to workflow design and ownership. Platform vendors, transformation programmes, and executives seeking a purchasable strategy benefit from treating ambiguity as an architecture gap.

**Verdict:** strongly supported. A platform can encode and operate a decision after it exists; it cannot decide which problem is worth solving.

### 2. Ordinary engineering plus thin AI-specific extensions is enough

Microsoft’s ICSE case study observed teams incorporating a nine-stage ML workflow into established Agile-like engineering processes while still encountering genuinely harder data, versioning, and entanglement problems ([Amershi et al.](https://www.microsoft.com/en-us/research/publication/software-engineering-for-machine-learning-a-case-study/)). Stack Overflow respondents building agents often reused Grafana/Prometheus and Sentry rather than an entirely new observability stack ([Stack Overflow](https://survey.stackoverflow.co/2025/ai)). DORA recommends a minimum viable platform for one journey, outside contributions, and no big-bang or one-size-fits-all rollout ([DORA](https://dora.dev/capabilities/platform-engineering/)).

**Interest served:** existing developer-platform, data, identity, security, and observability teams; open-source component vendors; application teams seeking autonomy. A separate central AI organization has an incentive to define a new stack and mandate.

**Verdict:** plausible default for most organizations. AI has distinctive seams—evaluation, artifacts, model supply, agent authority—but a separate end-to-end platform does not follow logically.

### 3. Centralization creates governance

The pro-platform version says one control point makes inventory, access, policy, evidence, and incidents tractable. The counter is that governance depends on distributed roles, domain context, risk acceptance, and communication. An ICSE analysis of **73 MLOps Community videos and 66 hours** found **17 socio-technical anti-patterns**, often rooted in leadership vacuum, organizational silos, or internal communication; tools could mitigate symptoms while causes remained organizational ([Mailach and Siegmund](https://sws.informatik.uni-leipzig.de/wp-content/uploads/2023/01/socio-technical-anti-patterns-icse2023.pdf)).

**Interest served:** security, legal, audit, procurement, central AI leaders, and vendors gain a legible control surface. Product teams and affected people benefit only if local accountability, contestability, and exception rights survive.

**Verdict:** central enforcement can help; “governance equals platform” is unsupported. A control plane can record a bad decision perfectly.

### 4. Integration removes glue

Google’s technical-debt paper famously argued that mature ML systems may contain at most 5% ML code and at least 95% glue. Platform advocates read that as demand for reuse. The same paper warns that generic packages can lock systems to package peculiarities and that a clean native solution can sometimes cost less than reuse ([Sculley et al.](https://proceedings.neurips.cc/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf)).

**Interest served:** integrated vendors can price the reduction of visible glue; application teams and composable-tool advocates emphasize that much “glue” is the application-specific data and workflow itself.

**Verdict:** both mechanisms are real. The relevant measurement is total lifecycle work retired, including migration and exception cost—not initial setup time.

### 5. One platform improves buyer leverage

Consolidated procurement can reduce contracts, vendor reviews, duplicated support, and inconsistent terms. But cloud–model partnerships and bundled services can turn one bill into upstream dependency. The UK CMA found Amazon and Microsoft had significant cloud market power and identified egress and interoperability barriers; the FTC documented cloud-spend and partnership structures in frontier AI ([CMA](https://www.gov.uk/cma-cases/cloud-services-market-investigation); [FTC](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study)).

**Interest served:** procurement and finance gain immediate simplicity; hyperscalers gain recurring consumption and cross-layer control. Smaller suppliers and product teams benefit from portable interfaces and credible multi-homing.

**Verdict:** procurement consolidation is a real fourth problem, but it is not evidence that one technical platform is best. Convenience and lock-in can be the same architecture viewed at different times.

## Community Pulse

The public conversation is active across Reddit, Hacker News, GitHub, MLOps Community, LinkedIn, and specialist engineering blogs. It is not representative: participants self-select, anonymous roles are hard to verify, and founders or vendors often have a stake. Its value is in discovering concrete failure modes.

### Where sentiment sits

- **Strong supporters** say integration itself has become a permanent team. They want routing, inference, deployment, observability, and policy in one supported path.
- **Cautiously positive** is the dominant posture in this scan: share operational primitives, preserve flexibility above and below them.
- **Sceptical-but-engaged** practitioners accept the need for routing, evals, and tracing but ask whether existing standards or mature tools already suffice.
- **Hostility** usually targets vendor lifespan, hype, or lock-in rather than denying the operational work.
- **Confusion** remains because “AI platform” can mean a model endpoint, SDK, gateway, lifecycle suite, developer portal, internal team, or procurement bundle.

### The argument in practitioners’ own words

The clearest statement of the pain comes from an r/mlops engineer:

> “At some point, I felt like my job was just writing glue codes to stick tools together.”
>
> — `symphonicdev`, [Reddit](https://www.reddit.com/r/mlops/comments/1uf4h1i/are_we_starting_to_see_fullstack_infra_platforms/), **2026-06-25**

The same person immediately questioned whether a unified approach would remain flexible enough. Another respondent supplied the most useful boundary:

> “They seem to want a stable operational layer that can sit between rapidly changing applications and rapidly changing model providers.”
>
> — `c0ventry`, [Reddit](https://www.reddit.com/r/mlops/comments/1uf4h1i/are_we_starting_to_see_fullstack_infra_platforms/), **2026-06-26**

That reply predicts consolidation around “routing, policy, telemetry, attribution, caching, observability” while retaining choice above and below the layer. This is narrower and more falsifiable than “end-to-end.”

Hacker News has asked for the concrete ticket since the agent-tooling wave began:

> “What problem(s) does this solve? I have a ticket in my backlog. Your SDK unlocks the solution. What is that ticket's title?”
>
> — `a_wild_dandan`, [Hacker News](https://news.ycombinator.com/item?id=39371297), **2024-02-14**

The pre-agent platform discussion had already answered part of it:

> “deployed to prod is only 50% of the story; someone poor fool has to manage (and account for) these things in life!”
>
> — `sgt101`, [Hacker News](https://news.ycombinator.com/item?id=19626275), **2019-04-10**

GitHub shows what “manage and account” becomes. A LiteLLM user asked to gate expensive models by user tier; the maintainer translated that into spend per model and per user ([LiteLLM issue #361](https://github.com/BerriAI/litellm/issues/361), **2023-09-13**). A LangSmith user needed organization-specific cost rather than list-price estimates ([LangSmith issue #858](https://github.com/langchain-ai/langsmith-sdk/issues/858), **2024-07-09–2024-07-10**). OpenTelemetry contributors then debated how to preserve rich message evidence without spamming listeners or making records impossible to query ([issue #1621](https://github.com/open-telemetry/semantic-conventions/issues/1621), **2024-11-26–2024-11-27**).

MLOps Community supplies the organizational precedent. Uber’s Kai Wang said teams initially built “their own one off workflows or infrastructure,” leading to systems that were difficult to productionize, inconsistent, and duplicated across teams ([MLOps Community](https://home.mlops.community/public/videos/inside-ubers-ai-revolution-everything-about-how-they-use-aiml), **2025-07-04**). Uber’s answer was not total standardization: common templates for roughly 80% of users and direct infrastructure access for advanced users.

LinkedIn gives the emerging job-category version:

> “We’re not blocked by GPUs, we’re blocked by the sheer drag of getting anything to production.”
>
> — Jagan Jeyapal, [LinkedIn](https://www.linkedin.com/posts/jaganathanj_aiengineering-platformengineering-aiinfra-activity-7361045939098185749-VjOq), **2025-08-12**

The same post says routing, evals, and observability are stitched together with scripts and configs, and jokes that token-cost tracking is a calculator at midnight. The useful signal is concrete; the caveat is that LinkedIn conversation is heavily shaped by people defining and selling the category.

Substack adds authored practitioner argument rather than a representative comment corpus. MLOps Roundup recommended: “Build integrations and connectors between tools -- this allows you to personalize your tooling choice for your business use cases and best utilize this nascent industry.” — Nihit Desai and Rishabh Bhargava, [MLOps Roundup](https://mlopsroundup.substack.com/p/issue-19-mlops-tooling-vertex-ai), **2021-05-31**. Keith Townsend later compressed the enterprise problem into: “The thing they’re missing isn’t a place to run workloads. It’s a control model” — [The CTO Advisor](https://ctoadvisor.substack.com/p/the-most-complete-on-prem-ai-platform), **2026-06-10**. Both authors have professional incentives to frame integration and control as a distinct layer, and public Substack comments were too inconsistently accessible to support a venue-wide sentiment claim.

### Details practitioners surface that broad coverage misses

1. **IAM and cost attribution are one problem.** The identity allowed to call a model is also the identity to which cost, risk, and business context must attach. Employees, service accounts, CI jobs, experiments, and demos are tenants even when they do not pay an invoice.
2. **Evaluation and observability are the feedback loop, not two dashboards.** Traces need to connect operational failure to model, prompt, retrieval, tool, policy, evaluator, and release. The result must trigger a decision.
3. **The platform can become its own bottleneck.** Median onboarding can improve while unusual workloads wait weeks. The 95th-percentile exception time is often more revealing than adoption.
4. **Ownership does not move with infrastructure.** A central team can operate the control plane, but it cannot own the product error tolerance, data meaning, worker impact, or business outcome for every domain.
5. **Premature abstraction is demand timing.** One team with one model does not prove a platform need. Repeated independent implementations of the same constraint do.

### Confusions worth clearing up

- **Model access is not a platform.** An endpoint solves supply; it does not solve lifecycle, evidence, authority, or accountability.
- **A unified interface need not imply a monolith.** Open contracts can present one operational surface over replaceable systems.
- **“LLM observability” is overloaded.** It can mean model introspection or ordinary application tracing with AI semantics; those are different problems.
- **The platform does not remove application-team ownership.** If it does, it recreates the handoff it was supposed to eliminate.
- **DevOps, MLOps, platform engineering, AgentOps, and AI platform engineering are unsettled labels.** The stable unit is the work required to make probabilistic, tool-using systems operable and accountable.

No named individual can defensibly be called “conspicuously silent”: there is no canonical event with an expected response set, and absence cannot be verified across private groups or deleted posts. The venue audit on **2026-07-27** found:

- **X/Twitter:** exact-phrase and site-restricted searches did not yield a stable public status page containing full text, handle, date, and thread context; direct search required authentication. No quote was admitted.
- **Public Discord/Slack:** Linen/Answer Overflow searches produced a rotating [Botpress archive root](https://www.linen.dev/s/botpress), not a stable message; [MLOps Community Slack](https://home.mlops.community/) required joining or sign-in. No quote was admitted.
- **YouTube comments:** [Inside Uber’s AI Revolution](https://www.youtube.com/watch?v=x5cIMPmYAzw) exposed six comments, all praise or advertising complaints; [Aggressively Helpful Platform Teams](https://www.youtube.com/watch?v=az8lXG9v4uo) exposed none. No substantive answer was admitted.
- **Substack:** two stable public post bodies were usable, but comments varied by sign-in/subscription. They are treated as authored essays, not community sentiment.
- **Stack Overflow:** concrete Q&A supplies useful framework failure cases, but the directly platform-shaped discussion was stronger in GitHub and HN. This exclusion improves quote verifiability but limits breadth.

## Forward Calendar

Only confirmed dated events are included. Conferences are diagnostic checkpoints, not promised standards releases.

| Date | Confirmed event | What to watch |
|---|---|---|
| **2026-08-02** | The EU AI Act becomes generally applicable, including Article 50 transparency obligations ([Commission timeline](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)). | Can multi-model platforms implement provider-agnostic marking, contextual disclosure, and exportable evidence, or must every product team assemble them separately? |
| **2026-08-13 to 2026-08-14** | MCP Dev Summit Seoul ([Linux Foundation](https://www.linuxfoundation.org/press/agentic-ai-foundation-announces-global-2026-events-program-anchored-by-agntcon-mcpcon-north-america-and-europe)). | Does interoperability move beyond connection syntax to identity, delegated authority, audit, revocation, and containment? |
| **2026-09-17 to 2026-09-18** | AGNTCon + MCPCon Europe, Amsterdam ([Linux Foundation](https://www.linuxfoundation.org/press/agentic-ai-foundation-announces-global-2026-events-program-anchored-by-agntcon-mcpcon-north-america-and-europe)). | Look for cross-vendor conformance and migration demonstrations, not announcement volume. |
| **2026-10-22 to 2026-10-23** | AGNTCon + MCPCon North America, San Jose ([Linux Foundation](https://www.linuxfoundation.org/press/agentic-ai-foundation-announces-global-2026-events-program-anchored-by-agntcon-mcpcon-north-america-and-europe)). | A second checkpoint for portable identity, traces, policy evidence, and tool permissions. |
| **2027-12-02** | Extended EU AI Act obligations begin for high-risk systems in listed sensitive areas ([Commission timeline](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)). | Can lineage, logging, documentation, human oversight, and monitoring compose into reproducible evidence rather than parallel spreadsheets? |
| **2028-08-02** | Extended transition ends for high-risk AI embedded in regulated products ([Commission timeline](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)). | Does a horizontal AI platform integrate with product-safety and quality systems, or do sector systems remain the real control plane? |

## Scenarios

### Base

**Federated extension of the existing platform — 50% probability.**

Identity, data, security, observability, developer tooling, and GRC absorb AI-specific capabilities. Separate experimentation feeds shared production controls; dedicated AI platforms remain a minority architecture.

**Probability rationale and sources:** this best fits the heterogeneous architecture and ownership patterns in the [CNCF Q1 2026 survey](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf), although that community sample cannot forecast the whole market. Limited adoption in the [OECD statistics](https://www.oecd.org/en/about/news/announcements/2026/01/ai-use-by-individuals-surges-across-the-oecd-as-adoption-by-firms-continues-to-expand.html) and [UK DSIT survey](https://www.gov.uk/government/publications/ai-adoption-research/ai-adoption-research) makes extension more plausible than wholesale replacement for the median organization.

**Six-month leading indicators, by 2027-01-27:**

- Enterprise release notes emphasize connectors to existing identity, observability, catalogues, CI/CD, ticketing, and GRC rather than replacement suites.
- EU transparency implementation produces reusable controls, but varies by content type, provider, and deployer context.
- Agent standards progress on connection/discovery while identity, delegated authority, revocation, and non-repudiation remain active work in [NIST's agent initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative) and [NCCoE concept work](https://www.nccoe.nist.gov/news-insights/new-concept-paper-identity-and-authority-software-agents).

**Twelve-month leading indicators, by 2027-07-27:**

- Comparable surveys keep hybrid plus extended-platform approaches at or above 50%, with dedicated AI platforms at or below 25%.
- Organizations report fewer duplicate integrations and better inventories while retaining sector/product systems for risk decisions.
- Platform teams publish service objectives for onboarding and exceptions; outcome evidence remains heterogeneous, consistent with [DORA's amplifier finding](https://research.google/pubs/dora-2025-state-of-ai-assisted-software-development-report/).

**Falsifier:** dedicated AI-platform use rises well above 25% in comparable surveys and independently measured outcomes clearly outperform hybrid or extended-platform approaches.

### Upside

**Shared evidence becomes a measurable coordination advantage — 20% probability.**

Portable artifact graphs, evaluation records, agent identities, policy decisions, and cost attribution allow several teams to reuse controls without losing local ownership. Auditors and incident responders can reproduce decisions; teams can switch providers while preserving evidence.

**Probability rationale and sources:** recurring lifecycle components and challenges in [Kreuzberger, Kühl, and Hirschl](https://doi.org/10.1109/ACCESS.2023.3262138) and [Amrit and Kolar](https://doi.org/10.1016/j.jik.2024.100637) make common-work savings plausible. The probability remains below Base because the large G2-review study is observational and satisfaction-based rather than causal ([Pasch](https://arxiv.org/abs/2510.09968)).

**Six-month leading indicators, by 2027-01-27:**

- Multi-model platforms export a portable evidence bundle covering provenance, evaluation, prompt/policy version, tool authority, approval, and incident history.
- At least two independent organizations publish timed model-switching or agent-revocation drills with failure modes.
- Platform teams report duplicate integrations retired, controls inherited, and evidence hours reduced—not only users or runs.

**Twelve-month leading indicators, by 2027-07-27:**

- At least three independent multi-organization studies find both production/change lead time and audit/incident effort down by at least 20%, without higher fully loaded cost, severe incidents, or supplier concentration.
- At least one study includes failed or abandoned use cases.
- Auditors, regulators, or insurers accept reproducible platform evidence and reduce parallel documentation.

### Downside

**An expensive activity concentrator — 25% probability.**

Platform spend, registered workloads, dashboards, and routed traffic rise, but product outcomes, delivery stability, and incident containment do not. Teams keep shadow gateways and spreadsheets because the central path is slow. Bundled procurement is renamed standardization.

**Probability rationale and sources:** the [KPMG](https://assets.kpmg.com/content/dam/kpmgsites/xx/pdf/2026/04/global-ai-pulse.pdf.coredownload.pdf) scaling-versus-ROI gap, [IBM/Oxford Economics](https://newsroom.ibm.com/2026-06-08-new-ibm-study-finds-cios-and-ctos-face-growing-ai-control-gap-as-enterprise-deployment-scales?asPDF=1&lnk=hpln1id) control-gap self-reports, and [DORA](https://dora.dev/research/ai/gen-ai-report/dora-impact-of-generative-ai-in-software-development.pdf) delivery associations supply plausible failure mechanisms. All are observational or vendor-sponsored, keeping the estimate below Base.

**Six-month leading indicators, by 2027-01-27:**

- EU transparency is implemented through provider-specific patches and manual attestations.
- Governance queues grow; teams create unofficial accounts, local gateways, or spreadsheet evidence.
- Scorecards emphasize calls, seats, catalogue entries, or checks with no outcome, incident, or retired-duplication denominator.

**Twelve-month leading indicators, by 2027-07-27:**

- In at least two transparent cohorts, platform spend/activity rises at least 25% without better business outcome, lead time, or high-severity incident measures.
- Exception and switching time worsen; audits find inventories without owners or logs without lineage.
- Platform programmes are reorganized despite rising AI usage because they cannot connect activity to value.

### Wildcard

**Open operational standards commoditize the category — 5% probability.**

Agent identity, delegated authority, revocation, tool discovery, telemetry, evaluations, and compliance evidence become portable across clouds and runtimes before integrated vendors entrench them.

**Probability rationale and sources:** pieces exist in the [Agentic AI Foundation programme](https://www.linuxfoundation.org/press/agentic-ai-foundation-announces-global-2026-events-program-anchored-by-agntcon-mcpcon-north-america-and-europe), [NIST agent work](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative), [OpenTelemetry GenAI conventions](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/), [ISO/IEC 42001](https://www.iso.org/standard/42001), and [ISO/IEC 42005:2025](https://www.iso.org/standard/42005?browse=tc). The probability is low because these layers have different owners, maturity, and incentives.

**Six-month leading indicators, by 2027-01-27:**

- AAIF events yield public conformance artifacts or test suites rather than only demos.
- Core OpenTelemetry agent, tool, evaluation, usage, and cost fields move toward stable status with privacy guidance.
- NIST identity work produces implementable profiles adopted in vendor roadmaps.

**Twelve-month leading indicators, by 2027-07-27:**

- Stable specifications and conformance tests cover identity/authority, revocation, tool discovery, telemetry, evaluation, and evidence.
- At least two major clouds, two open-source runtimes, and two enterprise vendors demonstrate end-to-end interoperability.
- Two public migration drills preserve policy and evidence without application rewrites.

**Threshold caveat for all scenarios:** probabilities are judgmental, not measured frequencies. Counts, percentages, and 20%/25% cut-offs are analyst-defined falsification thresholds, not published forecasts or known natural boundaries.

## The 90-Day Signal

**Window:** 2026-07-27 through 2026-10-25.

Watch how major multi-model enterprise platforms implement the EU transparency obligations beginning on 2026-08-02. This is unusually diagnostic because the duty crosses provider behavior, machine-readable marking, deployer disclosure, content type, downstream transformation, and evidence.

**Positive signal:** by 2026-10-25, at least three major platforms publicly document provider-agnostic controls that preserve or add required marks, let deployers configure contextual disclosures, and export versioned evidence showing which rule, model, transformation, and deployment path applied.

**Negative signal:** implementations remain model- or content-tool-specific; deployers assemble disclosures themselves; or a platform can show that a check ran but cannot export evidence that survives transformation and migration.

The threshold is analytical, while the legal date is confirmed by the European Commission’s [2026-07-20 guidelines announcement](https://digital-strategy.ec.europa.eu/en/news/commission-publishes-guidelines-transparency-obligations-providers-and-deployers-certain-ai-systems). A positive result would demonstrate reusable coordination, not prove ROI.

## Tensions and Open Questions

1. **What is the scale threshold?** No defensible study identifies a number of teams, models, providers, incidents, or regulated systems after which a dedicated AI platform has positive economics.
2. **Which complexity is truly common?** Routing, identity, telemetry, and evidence often repeat; data meaning, workflow, error tolerance, and domain evaluation remain local.
3. **Can control remain portable?** A platform that makes the current vendor governable but cannot export identity, policies, evaluations, lineage, and evidence worsens long-term dependency.
4. **Does self-service reduce queues or hide them?** Measure median and 95th-percentile exception time, not only onboarding time.
5. **Can governance preserve accountability?** A control plane must make owners and risk acceptance more explicit, not let teams claim “the platform approved it.”
6. **What is the unit of cost?** Tokens and requests are visible; integration, review, human change, incidents, failures, exceptions, and exit are usually not. Cost per successful business outcome is the harder denominator.
7. **What is the unit of value?** More experiments, users, models, traces, or policy checks can coexist with weak ROI. Adoption and satisfaction remain product signals, not causal business-value evidence.
8. **Can the platform learn without surveilling?** Rich traces and worker interaction data improve debugging and evaluation while expanding privacy and power concerns.
9. **Will standards arrive before lock-in?** OpenTelemetry and agent standards are moving, but identity, authority, revocation, evaluation, and evidence portability are still incomplete.
10. **Who can choose no AI?** A mature platform should make rejection and retirement easier when the use case is unnecessary, unsafe, or uneconomic.
11. **Who absorbs physical externalities?** Software teams see token prices; host communities and grids experience power, water, land, and connection constraints.
12. **What evidence would settle the category?** Independent matched or longitudinal comparisons of dedicated, extended, composable, and no-platform strategies on fully loaded cost, delivery, incidents, audit effort, switching, and business outcomes.

The practical decision rule is:

> Do not begin with “Which AI platform do we need?” Begin with “Which repeated constraint is preventing a valuable, owned workflow from operating safely?” Build or buy the smallest shared capability that removes that constraint, prove that it retires more work than it creates, and earn the next layer.

## Receipts

### Primary

- [NIST SP 800-145: The NIST Definition of Cloud Computing](https://www.nist.gov/publications/nist-definition-cloud-computing) — managed-platform and self-service precedent.
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) — lifecycle governance, roles, and outcomes.
- [NIST Generative AI Profile, 2024-07-26](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence) — GenAI-specific risk and evidence profile.
- [Regulation (EU) 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689) and [European Commission implementation timeline](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai) — binding actor duties and dates.
- [FTC staff report on cloud–AI partnerships, 2025-01-17](https://search.ftc.gov/news-events/news/press-releases/2025/01/ftc-issues-staff-report-ai-partnerships-investments-study) — partnership, spend, information, exclusivity, and competition evidence.
- [UK CMA cloud services market investigation](https://www.gov.uk/cma-cases/cloud-services-market-investigation) and [2026-03-31 actions](https://www.gov.uk/government/news/cma-announces-package-of-actions-on-business-software-and-cloud-services) — market power, egress, interoperability, and switching.
- [OECD firm AI adoption, 2026-01-28](https://www.oecd.org/en/about/news/announcements/2026/01/ai-use-by-individuals-surges-across-the-oecd-as-adoption-by-firms-continues-to-expand.html) — adoption and firm-size gaps.
- [UK DSIT AI Adoption Research, updated 2026-02-13](https://www.gov.uk/government/publications/ai-adoption-research/ai-adoption-research) — representative evidence on need, skills, tools, and adoption.
- [UK Business Data Survey, 2026-06-18](https://www.gov.uk/government/statistics/uk-business-data-survey-2026/uk-business-data-survey-2026) — integration and data-practice evidence; the source contains an internal contradiction over a 17% policy figure, so that figure is not used here.
- [IEA Energy and AI, 2025-04-10](https://www.iea.org/reports/energy-and-ai/) and [2026-04-16 update](https://www.iea.org/reports/key-questions-on-energy-and-ai/executive-summary) — infrastructure geography, electricity, and forecasts.
- [Alphabet 2025 Form 10-K](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm) — audited capex and commitment totals; not exclusively AI.
- [AWS Bedrock pricing](https://aws.amazon.com/bedrock/pricing/), [AWS cost attribution](https://docs.aws.amazon.com/bedrock/latest/userguide/cost-management.html), and [Google Vertex AI pricing](https://cloud.google.com/vertex-ai/generative-ai/pricing) — current mutable commercial meters, not total cost.
- [IBM Watson Health asset-sale announcement, 2022-01-21](https://newsroom.ibm.com/2022-01-21-Francisco-Partners-to-Acquire-IBMs-Healthcare-Data-and-Analytics-Assets), [IBM investor segment recast](https://www.ibm.com/investor/news/ibm-provides-historical-software-segment-data-to-reflect-announced-divestiture), [GE Predix APM launch](https://www.ge.com/news/press-releases/ge-revolutionizes-equipment-operations-first-complete-asset-performance-management), [GE investor update](https://www.ge.com/sites/default/files/GE%20Investor%20Update_Presentation_11132017.pdf), and [GE digital-business restructuring](https://www.ge.com/news/press-releases/ge-advances-digital-leadership-launch-12-billion-industrial-iot-software-company) — corporate announcements and investor materials, retained as primary company claims rather than news.
- [GE 2018 Form 10-K](https://www.sec.gov/Archives/edgar/data/40545/000004054519000014/ge10-k2018.htm), [NVIDIA 2026 Form 10-K](https://www.sec.gov/Archives/edgar/data/1045810/000104581026000021/nvda-20260125.htm), and [Zillow 2021 filing](https://www.sec.gov/Archives/edgar/data/1617640/000161764021000085/z-20211102.htm) — company filings used for historical or infrastructure context; none alone proves platform causality.
- [UT System 2018 audit](https://utsystem.edu/sites/default/files/documents/report-state/2018/consolidated-annual-financial-report-fy-2018/ut-system-audit-afr-2018.pdf), [Robo-debt Royal Commission](https://robodebt.royalcommission.gov.au/), [OpenAI incident write-up](https://status.openai.com/incidents/01JMYB63BJ47J3SXV6KSCT4D2A/write-up), and [Microsoft Tay postmortem](https://blogs.microsoft.com/blog/2016/03/25/learning-tays-introduction/) — primary audit, inquiry, status, and company incident records.
- [EU AI Act official-journal URI](https://eur-lex.europa.eu/eli/reg/2024/1689/oj?locale=en), [EDPB Opinion 28/2024](https://www.edpb.europa.eu/news/edpb-opinion-on-ai-models-gdpr-principles-support-responsible-ai_ga), [ICO Snap investigation](https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2024/05/ico-warns-organisations-must-not-ignore-data-protection-risks-as-it-concludes-snap-my-ai-chatbot-investigation/), and [OECD governing-with-AI report](https://www.oecd.org/en/publications/2025/06/governing-with-artificial-intelligence_398fa287.html) — official regulatory and government records.
- [Eurostat 2025 enterprise-AI release](https://ec.europa.eu/eurostat/web/products-eurostat-news/w/ddn-20251211-2), [Eurostat Digital Economy and Society series](https://ec.europa.eu/eurostat/web/digital-economy-and-society), [OECD digital-business statistics topic](https://www.oecd.org/en/topics/sub-issues/digital-transformation-of-businesses.html), and [OECD adoption landing page](https://www.oecd.org/en/publications/the-adoption-of-artificial-intelligence-in-firms_f9ef33c3-en.html) — official statistics and report indexes.
- [NIST SP 800-146](https://nvlpubs.nist.gov/nistpubs/legacy/sp/nistspecialpublication800-146.pdf), [NIST AI RMF programme page](https://www.nist.gov/itl/ai-risk-management-framework), [NIST AI programme](https://www.nist.gov/artificial-intelligence/nist-information-technology-laboratory-itl-ai-program), and [NIST SP 800-18r2 release](https://csrc.nist.gov/news/2026/nist-releases-sp-800-18r2) — official cloud portability, AI programme, and machine-readable security-plan material.
- [NIST PaaS glossary](https://csrc.nist.gov/glossary/term/platform_as_a_service), [NCSC secure ML deployment](https://www.ncsc.gov.uk/collection/machine-learning-principles/secure-deployment), [NCSC prompt-injection guidance](https://www.ncsc.gov.uk/blog-post/prompt-injection-is-not-sql-injection), and [OWASP LLM Top 10 v2025](https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-v2025.pdf) — official or standards-body security guidance.
- [FOCUS project](https://focus.finops.org/) and [FOCUS specification](https://focus.finops.org/focus-specification/) — primary FinOps cost-schema sources.
- [OpenTelemetry semantic-conventions repository](https://github.com/open-telemetry/semantic-conventions) and [semantic-conventions concept page](https://opentelemetry.io/docs/concepts/semantic-conventions/) — primary open-standard repository and documentation.
- [AWS Bedrock product page](https://aws.amazon.com/bedrock/), [Bedrock overview](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html), and [cross-region inference](https://docs.aws.amazon.com/bedrock/latest/userguide/cross-region-inference.html) — primary vendor architecture and routing documentation.
- [Microsoft Foundry overview](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-ai-foundry), [cost guidance](https://learn.microsoft.com/en-us/azure/foundry/concepts/manage-costs), and [model router](https://learn.microsoft.com/en-us/azure/foundry/openai/concepts/model-router) — primary vendor product and commercial documentation.
- [Databricks Foundation Model API compliance](https://docs.databricks.com/aws/en/machine-learning/foundation-model-apis/compliance), [Hugging Face Enterprise](https://huggingface.co/enterprise), [MLflow model registry](https://www.mlflow.org/docs/2.4.2/model-registry.html), [MLflow GenAI overview](https://www.mlflow.org/docs/latest/genai/overview/), and [MLflow AI Platform](https://mlflow.org/ai-platform) — primary vendor/project documentation.
- [Google Gemini Enterprise Agent Platform announcement](https://cloud.google.com/blog/products/ai-machine-learning/introducing-gemini-enterprise-agent-platform), [Backstage CNCF acceptance](https://backstage.io/blog/2020/09/23/backstage-cncf-sandbox/), [CNCF platform-engineering overview](https://www.cncf.io/blog/2023/05/26/what-is-platform-engineering-and-why-adopt-it-in-your-company/), and [CNCF reports index](https://www.cncf.io/reports/) — corporate or foundation announcements and official project materials.
- [Uber scaling Michelangelo](https://www.uber.com/jm/en/blog/scaling-michelangelo/) — primary company retrospective.
- [The Open Group TOGAF 10 launch](https://www.opengroup.org/open-group-announces-launch-togaf-standard-10th-edition) and [TOGAF 9.2 overview](https://www.opengroup.org/togaf-standard-version-92-overview) — primary standards-organization materials.
- [IEA Energy and AI report](https://www.iea.org/reports/energy-and-ai) and [ILO/NASK exposure-index release](https://www.ilo.org/resource/news/one-four-jobs-risk-being-transformed-genai-new-ilo%E2%80%93nask-global-index-shows) — official intergovernmental report pages.

### News

- [TIME: IBM Watson Health’s mixed clinical record](https://time.com/5556339/artificial-intelligence-robots-medicine/) — domain integration, evidence, and workflow warnings.

### Expert

- [RAND, *The Root Causes of Failure for Artificial Intelligence Projects*](https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2600/RRA2680-1/RAND_RRA2680-1.pdf) — 65 interviews; purpose, data, incentives, and domain expertise.
- [Schlegel, Schuler, and Westenberger, AI-project failure factors](https://aisel.aisnet.org/ijispm/vol11/iss3/3/) — expert-interview study across technical and nontechnical factors.
- [Mailach and Siegmund, socio-technical anti-patterns](https://sws.informatik.uni-leipzig.de/wp-content/uploads/2023/01/socio-technical-anti-patterns-icse2023.pdf) — ICSE analysis of 73 MLOps Community videos.
- [Kreuzberger, Kühl, and Hirschl, MLOps overview](https://doi.org/10.1109/ACCESS.2023.3262138) — peer-reviewed synthesis of lifecycle, roles, architecture, and workflow.
- [Amrit and Kolar, MLOps challenges](https://doi.org/10.1016/j.jik.2024.100637) — systematic review plus 12 practitioner interviews.
- [Sculley et al., Hidden Technical Debt in ML Systems](https://proceedings.neurips.cc/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf) — glue, entanglement, feedback, and abstraction debt.
- Google Research hosting for [Hidden Technical Debt](https://research.google/pubs/hidden-technical-debt-in-machine-learning-systems/), [TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/), and [The ML Test Score](https://research.google/pubs/the-ml-test-score-a-rubric-for-ml-production-readiness-and-technical-debt-reduction/) — distinct official research URLs retained for lifecycle, production-platform, and readiness evidence.
- [Amershi et al., Software Engineering for Machine Learning](https://www.microsoft.com/en-us/research/publication/software-engineering-for-machine-learning-a-case-study/) — evidence that AI work can extend existing engineering systems.
- [Anjum, platform-engineering multivocal review, 2026-05-04](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full) — thin peer-reviewed base and missing scorecard-effectiveness evidence.
- [DORA platform-engineering guidance](https://dora.dev/capabilities/platform-engineering/) and [2025 AI impact report](https://dora.dev/research/ai/gen-ai-report/dora-impact-of-generative-ai-in-software-development.pdf) — minimum viable platforms, failure modes, and AI-as-amplifier evidence; Google-sponsored and observational.
- [Stack Overflow 2025 Developer Survey](https://survey.stackoverflow.co/2025/ai) — developer trust, task, collaboration, and tool-reuse evidence; voluntary sample.
- [CNCF/SlashData Q1 2026 Technology Radar](https://www.cncf.io/wp-content/uploads/2026/03/Q1-2026-CNCF-Technology-Radar-Report.pdf) — current architecture and ownership mix; cloud-native community sample.
- [Pasch, *Operationalizing AI*, 2025-10-11](https://arxiv.org/abs/2510.09968) — more than 8,000 G2 reviews; preprint and association, not causal value.
- [ILO evidence review, 2026-06-01](https://www.ilo.org/publications/impact-genai-jobs-productivity-and-work-organization-review-empirical) — worker productivity, autonomy, and job-quality evidence.
- [KPMG Global AI Pulse, 2026-03-31](https://assets.kpmg.com/content/dam/kpmgsites/xx/pdf/2026/04/global-ai-pulse.pdf.coredownload.pdf) and [IBM control-gap study, 2026-06-08](https://newsroom.ibm.com/2026-06-08-new-ibm-study-finds-cios-and-ctos-face-growing-ai-control-gap-as-enterprise-deployment-scales?asPDF=1&lnk=hpln1id) — directional large-enterprise evidence; both are vendor-sponsored self-reports and not causal proof.
- [KPMG alternate hosted edition of the same Q1 2026 report](https://assets.kpmg.com/content/dam/kpmgsites/gr/pdf/2026/05/gr-global-ai-pulse.pdf.coredownload.inline.pdf) — distinct hosting URL retained; not an independent source.
- [Enterprise-architecture alignment review](https://doaj.org/article/56ccd6279e914047809b1c87ebb65577), [EA adoption review](https://ijeecs.iaescore.com/index.php/IJEECS/article/view/18485), and [CASE adoption-prediction study](https://doi.org/10.1108/02635570410522099) — organizational adoption precedents.
- [MLOps multivocal review](https://arxiv.org/abs/2406.09737), [MLOps systematic review](https://www.sciencedirect.com/science/article/abs/pii/S0950584925000722), [data-lake governance review](https://www.mdpi.com/1999-5903/12/8/126), and [policy-aware data-lake study](https://pmc.ncbi.nlm.nih.gov/articles/PMC7454728/) — lifecycle, governance, and data-platform evidence.
- [LLM evaluation survey](https://arxiv.org/abs/2405.13058), [LLM observability study](https://arxiv.org/abs/2407.09107), [agent security research](https://arxiv.org/abs/2407.15821), and [socio-technical AI governance article](https://onlinelibrary.wiley.com/doi/10.1002/aaai.70002) — AI-specific evaluation, observability, security, and governance research.
- [AI incident or governance study in JNCI](https://academic.oup.com/jnci/article/109/5/djx113/3847623), [ACM study DOI 10.1145/3653697](https://doi.org/10.1145/3653697), and [MLOps adoption article](https://www.sciencedirect.com/science/article/pii/S0167739X21002090) — peer-reviewed sources retained from the angle files; applicability is described where cited.
- [Microsoft ICSE paper PDF](https://www.microsoft.com/en-us/research/wp-content/uploads/2019/03/amershi-icse-2019_Software_Engineering_for_Machine_Learning.pdf) — distinct direct-hosting URL for the Amershi paper already cited above.
- [OECD/BCG/INSEAD adoption report PDF](https://www.oecd.org/content/dam/oecd/en/publications/reports/2025/05/the-adoption-of-artificial-intelligence-in-firms_8fab986b/f9ef33c3-en.pdf) — official/consultancy/academic analysis; adopter sample and commercial interest noted.
- [DORA research archive](https://dora.dev/research/) and [DORA 2024 report](https://dora.dev/research/2024/dora-report/) — practitioner-research series on delivery and platforms.
- [Martin Fowler: engineering practices for LLM applications](https://martinfowler.com/articles/engineering-practices-llm.html) and [2026 fragment](https://martinfowler.com/fragments/2026-02-18.html) — authored practitioner analysis.
- [MLflow lifecycle explainer](https://mlflow.org/articles/ml-lifecycle-management-explained-for-engineers) and [MLflow lifecycle paper](https://www.databricks.com/sites/default/files/2023-08/accelerating-the-machine-learning-lifecycle-with-mlflow.pdf) — project/vendor-authored lifecycle material.
- [Stack Overflow Blog on IBM enterprise workflows](https://stackoverflow.blog/2026/01/15/transforming-enterprise-workflows-how-ibm-is-unlocking-ai-s-potential/) and [agent harnesses](https://stackoverflow.blog/2026/07/10/building-more-than-just-an-agent-harness/) — editorial/practitioner sources, not independent outcome studies.
- [ZenML on hundreds of platform teams](https://www.zenml.io/blog/reflections-on-working-with-100s-of-ml-platform-teams), [infrastructure abstraction](https://www.zenml.io/blog/why-your-data-scientists-need-infrastructure-abstraction), and [MLOps standards](https://www.zenml.io/blog/why-your-data-team-needs-mlops-standards-now) — vendor-affiliated field essays.

### Community

- [Reddit r/mlops: full-stack infrastructure for agentic AI](https://www.reddit.com/r/mlops/comments/1uf4h1i/are_we_starting_to_see_fullstack_infra_platforms/) — **2026-06-25–2026-06-26**; glue, monoliths, and the stable-operational-layer thesis.
- [Hacker News: Google’s end-to-end AI platform](https://news.ycombinator.com/item?id=19626275) — **2019-04-10**; production integration, management, accounting, and vendor lifespan.
- [Hacker News: OpenLLMetry](https://news.ycombinator.com/item?id=39371297) — **2024-02-14**; concrete-ticket demand and existing observability standards.
- [Hacker News: OpenTelemetry as LLM observability standard](https://news.ycombinator.com/item?id=45398467) — **2025-09-27–2025-09-28**; evals, richer semantics, and overloaded terminology.
- [LiteLLM feature wishlist](https://github.com/BerriAI/litellm/issues/361) — opened **2023-09-13**; entitlements, budgets, routing, and per-user/per-model spend.
- [LangSmith custom cost issue](https://github.com/langchain-ai/langsmith-sdk/issues/858) — **2024-07-09–2024-07-10**; organization-specific cost attribution.
- [OpenTelemetry GenAI messages issue](https://github.com/open-telemetry/semantic-conventions/issues/1621) — **2024-11-26–2024-11-27**; evidence volume, privacy, and queryability.
- [MLOps Community: Inside Uber’s AI Revolution](https://home.mlops.community/public/videos/inside-ubers-ai-revolution-everything-about-how-they-use-aiml) — **2025-07-04**; duplicated workflows, centralized lifecycle services, prioritization, and escape hatches.
- [LinkedIn: Jagan Jeyapal on production drag](https://www.linkedin.com/posts/jaganathanj_aiengineering-platformengineering-aiinfra-activity-7361045939098185749-VjOq) — **2025-08-12**; scripts, routing, evals, observability, and manual cost tracking.
- [Reddit and Hacker News minimalist framework critiques](https://www.reddit.com/r/LangChain/comments/1iwrhuu/i_built_an_llm_framework_in_179_lineswhy_are_the/) and [HN discussion](https://news.ycombinator.com/item?id=36645575) — premature abstraction, opacity, and framework lock-in; self-selected and sometimes alternative-product-affiliated.
- [Hacker News: McKinsey AI platform](https://news.ycombinator.com/item?id=47333627) and [GoModel gateway](https://news.ycombinator.com/item?id=47849097) — vendor hostility, model switching, cost, and benchmarks.
- [LiteLLM entitlement comment](https://github.com/BerriAI/litellm/issues/361#issuecomment-1718220939), [LiteLLM spend-dashboard comment](https://github.com/BerriAI/litellm/issues/361#issuecomment-1718225628), [LangSmith maintainer reply](https://github.com/langchain-ai/langsmith-sdk/issues/858#issuecomment-2220759255), and [OpenTelemetry queryability reply](https://github.com/open-telemetry/semantic-conventions/issues/1621#issuecomment-2502330515) — stable deep links for exact quoted implementation requirements.
- [MLOps Community: Aggressively Helpful Platform Teams](https://home.mlops.community/en/public/videos/aggressively-helpful-platform-teams), [MLOps Community 2.0](https://mlops.community/blog/mlops-community-2-0), and [community developer portal](https://dev.mlops.community/) — practitioner-community sources and infrastructure.
- [LinkedIn: Fizz Orange](https://www.linkedin.com/posts/fizz-orange_your-employees-are-tenants-and-you-should-activity-7446188339264708608-4vuB) and [Bailey Caldwell](https://www.linkedin.com/posts/baileycaldwell_ive-had-dozens-of-ai-conversations-in-the-activity-7429892270004350976-gLIi) — internal-tenancy, attribution, governance, and cost-to-outcome posts.
- [Reddit: agentic infrastructure](https://www.reddit.com/r/AI_Agents/comments/1jgofsj/we_dont_need_more_frameworks_we_need_agentic/), [DevOps and AI](https://www.reddit.com/r/devopsjobs/comments/1s292u9/devops_ai_where_are_we_headed_need_honest/), [platform-team reflection](https://www.reddit.com/r/mlops/comments/1do2lqx/reflections_on_working_with_100s_of_ml_platform/), [SageMaker/Vertex and MLOps roles](https://www.reddit.com/r/mlops/comments/1hy5xji/why_do_we_need_mlops_engineers_when_we_have/), [AI-risk tracking](https://www.reddit.com/r/mlops/comments/1pgi54j/how_do_teams_actually_track_ai_risks_in_practice/), and [build-versus-buy MLOps systems](https://www.reddit.com/r/mlops/comments/1uy6rby/to_the_people_building_mlops_systems_do_you_build/) — pseudonymous practitioner evidence; not prevalence data.
- [Stack Overflow: unnecessary agent tool use](https://stackoverflow.com/questions/77141910/langchain-agent-always-tries-to-use-the-tool-even-when-not-needed) and [intermediate chain outputs](https://stackoverflow.com/questions/79257787/how-to-get-intermediary-chain-step-outputs-in-final-output) — narrow, version-specific abstraction failures.
- [YouTube: Inside Uber’s AI Revolution](https://www.youtube.com/watch?v=x5cIMPmYAzw) and [Aggressively Helpful Platform Teams](https://www.youtube.com/watch?v=az8lXG9v4uo) — comment sections checked on 2026-07-27; no substantive community answer found.

### Background

- [Rahim, Khan, and Selamat on CASE adoption versus abandonment](https://doi.org/10.1108/09593849710194696) — historical evidence that tool success depends on adoption systems and organizational fit.
- [DevOpsDays history](https://devopsdays.org/about) — cross-functional delivery precedent.
- [Kubernetes ten-year history](https://kubernetes.io/blog/2024/06/06/10-years-of-kubernetes/) — declarative, portable control-plane precedent.
- [Uber Michelangelo](https://www.uber.com/bd/en/blog/michelangelo-machine-learning-platform/) and [PyML escape hatch](https://www.uber.com/en-GB/blog/michelangelo-pyml/) — internal ML platform and the cost of overconstrained abstractions.
- [Backstage launch](https://backstage.io/blog/2020/03/16/announcing-backstage/) — common portal over heterogeneous tools.
- [Zhamak Dehghani, data mesh](https://martinfowler.com/articles/data-monolith-to-mesh.html) — shared infrastructure with domain ownership.
- [Armbrust et al., lakehouse](https://www.vldb.org/cidrdb/2021/lakehouse-a-new-generation-of-open-platforms-that-unify-data-warehousing-and-advanced-analytics.html) — technical unification and open-platform claim.
- [Google Cloud Vertex AI launch](https://cloud.google.com/blog/products/ai-machine-learning/google-cloud-launches-vertex-ai-unified-platform-for-mlops) — hyperscaler consolidation framing.
- [CNCF platform-engineering maturity model](https://tag-app-delivery.cncf.io/blog/announcing-the-platform-engineering-maturity-model/) — platform-as-product framing.
- [OpenTelemetry GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/) — emerging operational interoperability and privacy caveats.
