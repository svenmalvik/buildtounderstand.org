# What Does “Smallest” Mean? — Research Dossier

**Question this dossier answers:** What is the least organizational and technical machinery that can remove a proven, consequential constraint for people building and operating AI-enabled workflows without creating a larger coordination burden, bottleneck, or dependency?

**Last updated:** 2026-07-29

## The Story in One Paragraph

The evidence does not support a universal component list for the smallest AI platform. It supports a decision rule: **smallest is the lightest arrangement that minimizes total system work per successful governed outcome, while meeting the workflow’s risk floor and preserving a credible path to shrink, replace, or remove it**. That definition counts the platform team’s machinery and the integration, validation, audit, support, incident, and migration work exported to everyone else; it also explains why DORA can report productivity gains alongside lower throughput and change stability ([DORA report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). The likely first move is a versioned contract inside existing developer infrastructure, automated conformance, and one real consumer—not a new portal or universal runtime—but agents that can write, spend, disclose, or affect customers raise the minimum to downstream identity, authorization, approval, evidence, and a kill path ([NIST agent hijacking](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations); [OWASP Excessive Agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)). The tension is that thin scope can merely hide work while broad integration can remove real glue at scale; the public evidence remains dominated by first-party cases, vendor surveys, and community accounts rather than controlled comparisons ([Frontiers review](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)).

## Cast

| Actor | Role and stake | Most recent material action reviewed |
|---|---|---|
| **DORA / Google Cloud** | Software-delivery research program; Google also sells cloud and platform products. | On **2026-01-12**, DORA updated its guidance to recommend a minimum viable platform, developer independence, task-success measurement, and avoidance of “big bang” scope ([DORA guidance](https://dora.dev/capabilities/platform-engineering/)). |
| **Mateen Ali Anjum / Frontiers in Computer Science** | Author and venue of the most comprehensive multivocal review in this record; no platform-vendor affiliation declared on the article page. | On **2026-05-04**, Frontiers published Anjum’s review of 88 sources, finding only 2 top-tier sources primarily about platform engineering and no longitudinal or quasi-experimental multi-organization evidence ([Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)). |
| **CNCF Platforms Working Group** | Vendor-neutral convenor with a vendor-rich membership; defines platform concepts and maturity. | On **2023-11-20**, CNCF released a maturity model created by almost 50 contributors after its Platforms White Paper, which says a platform can be as thin as a wiki and succeeds indirectly through users ([CNCF](https://www.cncf.io/blog/2023/11/20/announcing-the-platform-engineering-maturity-model/); [white paper](https://tag-app-delivery.cncf.io/es/whitepapers/platforms/)). |
| **Spotify / Backstage** | Creator of the open-source portal framework and seller of commercial Backstage products; direct product and category stake. | On **2026-06-03**, Spotify described exposing Backstage through MCP and CLIs to coding agents while reporting **76% more pull requests to review** as coding accelerated ([Spotify Engineering](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint?from_theconsensus=1)). |
| **Netflix** | Large-scale operator of paved roads, full-cycle ownership, and Metaflow; first-party architecture evidence. | On **2019-12-03**, Netflix open-sourced Metaflow as a human-centric layer over existing infrastructure rather than a universal UI or vertically complete runtime ([Netflix](https://netflixtechblog.com/open-sourcing-metaflow-a-human-centric-framework-for-data-science-fa72e04a5d9)). |
| **Uber / Michelangelo** | Operator of a broad integrated ML platform; first-party stake in demonstrating scale benefits. | Uber’s later scaling account says Michelangelo supported hundreds of use cases and thousands of models while also spawning specialist NLP and computer-vision platforms when the general system stopped fitting ([Uber](https://www.uber.com/us/en/blog/scaling-michelangelo/), retrieved **2026-07-29**). |
| **Google SRE / Borg, Omega, and filer retirement** | Operator publishing rewrite and decommissioning lessons; first-party operational evidence. | Its filer-retirement case, retrieved **2026-07-29**, documents usage-led phased subtraction across 2.5 billion files, 60,000 users, and multiple specialized replacements ([Google SRE Workbook](https://sre.google/workbook/eliminating-toil/)). |
| **Government Digital Service / GOV.UK PaaS** | Public platform operator that retired a reliable shared service; accountable for the official decision record. | On **2022-07-12**, GDS announced an 18-month sunset despite 99.95% uptime, one major incident in seven years, 172 services, and 3,200 applications ([GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). |
| **NIST** | US standards and risk-management body; no platform sales stake. | On **2026-05-18**, NIST published its analysis of agent-security RFI responses after launching the AI Agent Standards Initiative, emphasizing identity, authorization, interoperability, and adapted security controls ([NIST analysis](https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai)). |
| **OWASP** | Application-security community defining agentic risks and mitigations. | On **2025-12-09**, OWASP published its Top 10 for Agentic Applications, extending the earlier Excessive Agency analysis to agent goal hijacking and tool misuse ([OWASP agentic risks](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)). |
| **OpenTelemetry** | Open telemetry standard and contributor community; stake in portable semantics rather than a single backend. | On **2026-05-14**, OpenTelemetry demonstrated GenAI traces joining model calls, token use, and tool activity, while its registry defines agent, tool, data-source, and evaluation attributes ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/)). |
| **FinOps Foundation / FOCUS** | Practitioner foundation and specification steward for technology cost and value; member ecosystem includes vendors and large buyers. | Its report accessed **2026-07-29** says 98% of 693 respondents manage AI spend, making attribution ordinary FinOps work rather than proof that a full agent platform is needed ([State of FinOps](https://data.finops.org/)). |
| **Microsoft / GitHub** | Cloud, AI-platform, and assistant vendor; direct commercial interest. | On **2024-03-27**, a field-experiment preview covering 1,974 Microsoft and Accenture developers reported more weekly pull requests, with poor statistical power and compliance caveats ([MIT project](https://mit-genai.pubpub.org/pub/v5iixksv/release/2)). |
| **METR** | Independent non-profit measuring frontier-model capability and developer productivity. | On **2026-05-19**, METR updated its earlier slowdown result with a later-agent estimate of a small 4%–20% benefit and warned about selection effects ([METR](https://metr.org/blog/2026-05-19-frontier-risk-report/?dot=INC-029)). |
| **European Commission / EU AI Office** | Rule maker and supervisor; determines risk- and role-based legal floors. | On **2026-05-07**, the Council and Parliament reached a provisional agreement adjusting high-risk implementation dates while retaining EU-level supervision in specified general-purpose-model cases ([Council of the EU](https://www.consilium.europa.eu/en/press/press-releases/2026/05/07/artificial-intelligence-council-and-parliament-agree-to-simplify-and-streamline-rules/pdf/)). |

## Timeline

| Date | Development | Why it matters |
|---|---|---|
| **2009-10-30** | Patrick Debois’s DevOpsDays Ghent convenes development and operations around shared delivery responsibility ([programme](https://legacy.devopsdays.org/events/2009-ghent/program)). | The recurring problem is lifecycle coordination, not an AI product category. |
| **2013-08-15** | Heroku publishes its Twelve-Factor Apps account, while buildpacks operationalize a shared build contract ([Heroku](https://www.heroku.com/blog/twelve-factor-apps/); [Cloud Foundry](https://docs.cloudfoundry.org/buildpacks/index.html)). | A contract can coordinate plural implementations without one universal UI. |
| **2016-03-09** | Netflix describes its paved road for building and delivering code ([Netflix](https://netflixtechblog.com/how-we-build-code-at-netflix-c5d9bd727f15)). | A supported default can win through usefulness while preserving escape hatches. |
| **2017-09-05** | Uber introduces Michelangelo as its company-wide ML platform ([Uber](https://www.uber.com/us/en/blog/michelangelo-machine-learning-platform/)). | Broad integration can remove repeated glue at sufficient scale. |
| **2018-05-17** | Netflix publishes its full-cycle developer model ([Netflix](https://netflixtechblog.com/full-cycle-developers-at-netflix-a08c31f83249)). | Shared capability should preserve ownership and feedback rather than create queues. |
| **2018-06-08** | Google documents why Omega did not replace Borg as imagined ([Google SRE](https://sre.google/workbook/simplicity/)). | A clean platform competes with the improved future incumbent and its migration cost. |
| **2019-12-03** | Netflix open-sources Metaflow ([Netflix](https://netflixtechblog.com/open-sourcing-metaflow-a-human-centric-framework-for-data-science-fa72e04a5d9)). | A thin framework can reuse existing compute and storage. |
| **2020-03-16** | Spotify open-sources Backstage ([Backstage](https://backstage.io/blog/2020/03/16/announcing-backstage/)). | Repository metadata plus an extensible portal becomes a contracts-and-adapters precedent. |
| **2022-07-12** | GDS announces the retirement of GOV.UK PaaS ([GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). | A reliable platform can cease to be the lightest continuing investment. |
| **2024-10-22** | DORA releases mixed platform findings ([Google Cloud](https://cloud.google.com/blog/products/devops-sre/announcing-the-2024-dora-report); [report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). | Productivity gains can coexist with lower throughput and change stability. |
| **2024-11-25** | Anthropic releases the Model Context Protocol ([Anthropic](https://www.anthropic.com/news/model-context-protocol)). | An AI-specific integration seam can remain open and plural. |
| **2025-01-17** | NIST publishes agent-hijacking evaluation work ([NIST](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations)). | Acting agents move consequential control from declared intent to runtime mediation. |
| **2025-12-09** | The Linux Foundation forms the Agentic AI Foundation around MCP, AGENTS.md, and related interoperability work ([Linux Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation?hs_amp=true)). | Neutral governance may reduce the need for proprietary integration layers. |
| **2026-05-04** | Frontiers publishes its 88-source platform-engineering review ([Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)). | Confident prescriptions remain weakly supported by independent causal evidence. |
| **2026-06-03** | Spotify reports coding acceleration and 76% more pull requests to review ([Spotify](https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint?from_theconsensus=1)). | AI can move the bottleneck downstream; code volume is not successful delivery. |

## Geography and Jurisdiction

This optional angle is material because jurisdiction can impose a capability floor without prescribing a monolith.

| Layer | Location / authority | Minimum-design consequence | Source |
|---|---|---|---|
| Contract metadata | Existing source-control, identity, and portal estate | Reuse avoids a new data plane but not ownership, validation, access, retention, or schema migration. | [Backstage catalogue](https://backstage.io/docs/features/software-catalog/) |
| Model API / narrow gateway | Gateway region plus every model-provider endpoint and subprocessor | A “single endpoint” can conceal multiple processing locations; provider, region, and data-flow metadata may be minimum fields. | [AWS Bedrock pricing and regions](https://aws.amazon.com/bedrock/pricing/) |
| Broad integrated platform | Vendor control plane, customer data plane, replicas, telemetry, backups, and support locations | “Region” does not answer which legal entities and support personnel can access data; contract and subprocessor review remain. | [Alphabet filing](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm) |
| EU deployer and users | EEA or systems placed on or used in the EU market | Duties vary by role and risk; a platform can supply evidence but cannot accept the employer’s, bank’s, health provider’s, or public authority’s use-case risk. | [European Commission](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act) |
| General-purpose-model supervision | EU market; EU AI Office and national authorities | Model-provider obligations and downstream-system duties are distinct and must not be collapsed into one platform owner. | [Commission guidance](https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers) |
| US-provider compelled access | Provider-controlled data wherever stored | EU-region storage alone does not determine whether a US-headquartered provider can be compelled to disclose data it controls. | [US DOJ](https://www.justice.gov/criminal/criminal-oia/regarding-cloud-act-executive-agreements) |
| Governing law, liability, and exit | Contract-specific | SLA credits, audit rights, termination help, data return/deletion, indemnities, and usage commitments are **Unknown** without the buyer’s order form, MSA, DPA, and SLA. | Public product pages do not supply the organization-specific contract. |
| Sanctions / export control | Workload, model, chip, user, and destination specific | No restricted export or counterparty is proposed here; add a use-case gate when facts make it real rather than building an export-control subsystem for every experiment. | No load-bearing transaction exists in the source chapter. |

The first asymmetry is between **where data is stored** and **which entities or people can access or be compelled to disclose it**. The second is between provider and deployer obligations: buying a model or broad platform does not transfer business-use accountability ([European Commission](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)). The practical minimum should encode data class, provider/region constraints, accountable owner, and required evidence before selecting a platform rung.

## By the Numbers

No source supports a universal AI-platform ROI. These observations use different units and evidence types; vendor and first-party figures are retained with their incentives visible.

| Figure | Category | Meaning and limitation | Direct source |
|---:|---|---|---|
| **88 sources; 2 of 88 (2.3%) top-tier sources primarily about platform engineering** | Evidence maturity | No longitudinal or quasi-experimental multi-organization comparison was found; single-author screening is a stated limitation. | [Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full) |
| **Nearly 3,000 respondents; +8% individual productivity, +10% team, +6% organization, -8% throughput, -14% change stability** | Delivery outcomes | Observational and multidimensional; one flattering metric can conceal a worsening denominator. | [DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf) |
| **438 respondents; 68% velocity, 60% reliability, 59% productivity, 55% security benefits reported** | Adoption / perception | Self-report with snowball sampling; Puppet sells automation and Humanitec sponsored the study. | [Puppet](https://www.puppet.com/system/files/report-puppet-sodor-2023-platform-engineering.pdf) |
| **34% slower cycle time; 32% adoption resistance; 32% poor change communication** | Failure reaction | Shared capability can add coordination delay while producing other perceived gains. | [Puppet](https://www.puppet.com/system/files/report-puppet-sodor-2023-platform-engineering.pdf) |
| **44.67% did not measure success; 26.64% did not know whether metrics improved** | Measurement gap | A vendor-sponsored respondent pool cannot support defensible ROI when many adopters do not measure outcomes. | [State of Platform Engineering](https://sequolia.com/hubfs/State%20of%20Platform%20Engineering%20Report%20Volume%203%20-%202024.pdf) |
| **35% used spreadsheets; 53% some form of portal; 43% surveys versus 5% DORA and 5% SPACE for productivity** | Adoption / measurement | “Portal” spans spreadsheets, in-house systems, Backstage, and commercial products; Port sells a portal. | [Port](https://www.port.io/state-of-internal-developer-portals-2024) |
| **55% lower onboarding time; 280 teams, 2,000+ services, 300+ websites, 4,000+ data pipelines, 200+ mobile features** | Enterprise scale | Strong single-company evidence; Spotify created Backstage and now sells related products. | [Backstage announcement](https://backstage.io/blog/2020/03/16/announcing-backstage/) |
| **80% of contributions outside the core team; 200+ engineers, 120+ plugins, 50+ teams** | Distributed labor | A small core may depend on large distributed contribution work; central headcount is not total work. | [Spotify](https://engineering.atspotify.com/2021/5/a-product-story-the-lessons-of-backstage-and-spotifys-autonomous-culture) |
| **40,000+ entities synchronized daily by a four-person team** | Catalogue operation | Automation can keep a large catalogue alive, but source integration remains product work. | [Zalando](https://engineering.zalando.com/posts/2023/08/sunrise-zalandos-developer-platform-based-on-backstage.html) |
| **16 maintainers, 246 tasks, 19% slower despite believing 20% faster** | AI productivity | Independent RCT but narrow cohort and early-2025 tools; perception and task time diverged. | [METR](https://metr.org/Early_2025_AI_Experienced_OS_Devs_Study-paper.pdf) |
| **96 Google engineers, about 21% faster on one complex task** | Conflicting AI productivity | Context, task, and tool differ from METR; wide confidence interval and single-company setting. | [Google RCT](https://arxiv.org/abs/2410.12944) |
| **98% of 693 respondents manage AI spend, up from 63% and 31%** | Cost allocation / growth | AI cost visibility is ordinary FinOps work; it supports a metadata/billing floor more directly than a full runtime. | [State of FinOps](https://data.finops.org/) |
| **$2 / $10 per million input/output tokens through 2026-08-31, then $3 / $15** | Pricing reference | One promotional Claude Sonnet 5 Bedrock example; retrieval, storage, evaluation, networking, telemetry, and labor are extra. | [AWS](https://aws.amazon.com/bedrock/pricing/) |
| **$148,100 US mean software-developer annual wage** | Workforce cost | Wage floor before benefits, management, recruiting, equipment, cloud, support, or on-call; not a platform-team budget. | [US BLS](https://www.bls.gov/news.release/ocwage.t01.htm) |
| **99.95% uptime, one major incident in seven years, 172 services, 3,200 applications** | Subtraction | Reliability and use did not settle whether GOV.UK PaaS remained the lightest continuing investment. | [GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/) |
| **41 critical services migrated by one department** | Exit cost | Deletion exported engineering, coordination, cutover, and out-of-hours work. | [DBT](https://digitaltrade.blog.gov.uk/2025/05/12/delivering-seamless-migrations-and-a-future-ready-platform/) |
| **2.5 billion files, 300 TB, 60,000 users, 400 volumes, 124 appliances, 60 sites** | Decommission mechanics | Google used phased cohorts and several specialized replacements rather than one new universal platform. | [Google SRE](https://sre.google/workbook/eliminating-toil/) |
| **At most 5% ML code and at least 95% glue** | Hidden work | Illustrative architecture ratio, not a modern-agent census; warns against minimizing only the visible AI layer. | [Sculley et al.](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf) |

## How It Actually Works

“Smallest” is a recurring decision, not a fixed architecture.

1. **Name one user job and baseline it.** Measure successful completion, elapsed and waiting time, repeated manual work, support load, audit effort, incidents, and cost. “Register an agent with a valid owner, approved data use, evaluation evidence, cost centre, and incident contact” is a testable job. “Build an AI platform” is not. SPACE rejects one-dimensional productivity measures, while DORA recommends mapping critical journeys and improving one common workflow before expansion ([SPACE](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/); [DORA](https://dora.dev/capabilities/platform-engineering/)).

2. **Set the capability floor from consequence.** Classify data sensitivity, tool permissions, reversibility, external impact, and approval needs. Low-risk read-only workflows may tolerate warnings and local execution. Irreversible or customer-affecting actions need least privilege, downstream authorization, evidence, and often human approval ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/); [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)).

3. **Try rungs in increasing ownership order.** The practical ladder is: documentation or convention → repository template or module → versioned metadata contract → automated validation and conformance tests → CI/admission policy → narrow gateway or policy service → managed runtime. Choose the lowest rung that clears both the user outcome and risk floor after exported work is counted; Anthropic’s production guidance similarly says to start with the simplest solution and add complexity only when outcomes improve ([Anthropic](https://www.anthropic.com/engineering/building-effective-agents)).

4. **Define the contract before the service.** A viable contract has a named owner, version, semantics, examples, lifecycle, compatibility policy, validators, and consumers. Backstage’s `apiVersion`/`kind` envelope and A2A’s Agent Card establish useful identity and discovery precedents without supplying a complete internal governance contract ([Backstage descriptor](https://backstage.io/docs/features/software-catalog/descriptor-format/); [A2A](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)).

5. **Separate declared, observed, and attested facts.** “Owner: payments” is declared by a team. “Revision abc123 is running” is observed by delivery or runtime systems. “Approved for restricted data until 2027-01-31” is attested by an authority. A single self-authored YAML document should not impersonate all three; Backstage itself documents late processing errors, orphaned entities, and dangling relations ([Backstage entity lifecycle](https://backstage.io/docs/features/software-catalog/life-of-an-entity/); [model extension](https://backstage.io/docs/features/software-catalog/extending-the-model/)).

6. **Enforce at the narrowest boundary where harm is preventable.** Syntax can fail in the editor or CI. Missing ownership can block catalogue admission. Tool declarations cannot authorize tool use: downstream IAM or runtime policy must mediate consequential actions. OPA separates decisions from enforcement and requires deliberate handling of unloaded policy and fail-open/fail-closed behavior ([OPA](https://www.openpolicyagent.org/docs); [operations](https://www.openpolicyagent.org/docs/operations)).

7. **Treat interfaces as adapters over the same semantics.** Engineers may prefer reviewed YAML, a CLI, or a template. Auditors, approvers, occasional builders, and domain reviewers may need a portal or purpose-built UI. Google explicitly says an internal developer platform may or may not include a portal; Backstage can render source-controlled metadata without becoming the authoring source ([Google Cloud](https://cloud.google.com/solutions/platform-engineering); [Backstage](https://backstage.io/docs/features/software-catalog/)).

8. **Keep management out of the execution path unless risk requires it.** Registration, configuration, policy distribution, and evidence are control-plane jobs. Agent turns and tool calls are data-plane jobs. Prefer last-known-good local execution and asynchronous status collection so a portal outage does not stop already-approved low-risk work; AWS and OPA document the reliability benefits of control/data-plane separation and local policy evaluation ([AWS](https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/control-planes-and-data-planes.html); [OPA management](https://www.openpolicyagent.org/docs/management-introduction)).

9. **Link observability, evaluation, and cost with one run identity.** Traces explain what ran; domain evaluations decide whether it was acceptable; cost data shows what that acceptable result consumed. OpenTelemetry and FOCUS provide portable semantics, while each product team remains responsible for its business rubric and sensitive-data choices ([OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/); [FOCUS](https://focus.finops.org/focus-specification/v1-3/)).

10. **Make exceptions informative and temporary.** Record owner, reason, expiry, compensating control, and review date. Repeated exceptions mean either the control is wrong or a missing common capability has become consequential; a silent or permanent bypass makes adoption and compliance statistics meaningless ([OPA operations](https://www.openpolicyagent.org/docs/operations)).

11. **Review five outcomes: grow, hold, shrink, replace, remove.** Grow only when repeated failures prove the current rung insufficient. Shrink when a lower rung now produces the same governed outcome. Replace when an incumbent or supplier absorbs the job at lower total cost. Remove when the original constraint disappears and consumers can migrate safely; Google’s error-budget and decommissioning cases provide concrete decision and migration precedents ([error budgets](https://sre.google/sre-book/embracing-risk/); [decommissioning](https://sre.google/workbook/eliminating-toil/)).

### Contract versus enforcement

| Contract job | Lightest adequate mechanism | What it cannot prove |
|---|---|---|
| Shared vocabulary | Documentation and examples | Completeness, freshness, or compliance |
| Shape and syntax | Schema validation | Semantic truth |
| Producer/consumer compatibility | Versioned conformance tests | Runtime authorization |
| Deployment admission | CI or admission policy | Correct behavior after deployment |
| Runtime authority | Downstream authorization, local policy, approval | Business correctness of an allowed action |

A contract can be the stable platform boundary, but a contract without ownership, conformance, freshness, a consumer, and consequences is documentation. Backstage explicitly warns that `spec.owner` is for responsibility/display and not runtime authorization ([descriptor](https://backstage.io/docs/features/software-catalog/descriptor-format/)). Conversely, not every field deserves hard enforcement; the decision follows the consequence and reversibility of a violation.

### Build agents versus run agents

| Scope | Plausible minimum | Responsibilities deliberately left local |
|---|---|---|
| **Help teams build** | Approved provider pattern, agent/tool metadata, templates or SDK examples, identity guidance, eval hooks, trace/cost fields, and deployment hooks into the existing application platform | Prompts, domain tools, product memory, business success rubric, downstream entitlements, and product-risk acceptance |
| **Run agents for teams** | Everything at left plus durable execution semantics, per-run identity, authorization, retries and idempotency, cancellation, rate limits, provenance, online risk signals, approval/handoff, isolation, capacity, SLOs, incident response, recovery, and decommissioning | Domain truth and acceptable business harm still cannot be centralized safely by default |

The boundary should be crossed only when several teams repeatedly rebuild the same consequential runtime responsibility and centralization reduces total work or risk after on-call and common-mode costs are included. LangGraph’s own server documentation makes the added database, task queue, workers, checkpoints, and scaling modes visible; “several teams use agents” is not enough ([LangGraph Agent Server](https://langchain-ai.github.io/langgraph/concepts/langgraph_server/); [control plane](https://langchain-ai.github.io/langgraph/concepts/langgraph_control_plane/)).

### What the platform should deliberately not provide by default

- A universal agent framework, prompt model, memory abstraction, or domain tool set.
- A new identity provider, observability backend, billing engine, or deployment substrate when incumbent systems can absorb the necessary fields and hooks.
- A portal that duplicates an existing portal merely to create an AI-branded front door.
- A synchronous central control-plane dependency for every low-risk agent turn.
- Platform-authored business evaluation criteria or permission to accept product harm.
- Raw prompt and tool payload collection without a defined privacy, retention, access, redaction, and sampling need.
- Permanent exceptions, indefinite compatibility, or a feature without a named consumer and removal rule.

### Failure modes and ceilings

| Failure mode | What breaks | Evidence |
|---|---|---|
| **Decorative contract** | Metadata exists without a validator, consumer, freshness check, or consequential enforcement. | An 812-project Terraform study found that infrastructure-as-code did not itself ensure adoption of security practices ([Verdet et al.](https://arxiv.org/abs/2308.03952)). |
| **Schema evolution strands consumers** | Producers, portal plugins, generators, and runtime clients interpret incompatible fields or defaults. | Kubernetes `v1.22` removed beta APIs and changed required fields, illustrating the migration work behind “compatible” contracts ([release](https://kubernetes.io/blog/2021/08/04/kubernetes-1-22-release-announcement/); [guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/)). |
| **Policy engine present but not enforcing** | The caller does not ask, ignores the answer, or starts with no loaded policy and silently fails open. | OPA documents `undefined` decisions and the need for deliberate failure behavior ([OPA operations](https://www.openpolicyagent.org/docs/operations)). |
| **Build-only controls applied to an acting agent** | Reviewed prompts or declarations cannot stop a compromised agent using excessive downstream permissions. | NIST exercised malicious instructions embedded in email, files, websites, and simulated tools ([NIST](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations)). |
| **Portal becomes a handoff machine** | Every change crosses extra systems or teams, raising waits and workarounds. | DORA associates platform use with lower throughput and change stability alongside productivity gains; it does not establish causality ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). |
| **Central runtime creates correlated failure** | One control, configuration, or dependency error affects many agents. | AWS’s 2017 S3 incident propagated across S3, EC2 launches, EBS snapshots, Lambda, and the status path ([AWS](https://aws.amazon.com/message/41926/)). |
| **Control plane enters the data path** | Running workloads fail when the catalogue, portal, policy distributor, or analytics system is unavailable. | Cloudflare’s 2023 control-plane outage left much of the network data plane forwarding while newer hidden dependencies failed ([Cloudflare](https://blog.cloudflare.com/post-mortem-on-cloudflare-control-plane-and-analytics-outage/)). |
| **Metrics optimize the platform instead of the outcome** | Registrations, token volume, or deployments rise while quality, delivery, cost, or user success worsens. | SPACE and DORA both reject a single flattering productivity measure ([SPACE](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/); [DORA](https://dora.dev/research/2024/dora-report/)). |
| **Reversibility is assumed rather than engineered** | Consumers are not inventoried, state is not portable, and deprecation becomes a surprise migration programme. | Kubernetes formalizes support windows and warnings because shared APIs create dependencies ([Kubernetes](https://kubernetes.io/docs/reference/using-api/deprecation-policy/)). |

The hard ceilings are consequence, semantics, human attention, operational economics, attribution, availability, interface diversity, jurisdiction, and reversibility. A generic platform can standardize identity, envelopes, cost, and trace semantics; it cannot define every domain’s correct outcome or acceptable harm. A central runtime must scale support sublinearly, and any design that owns state, secrets, workflow semantics, and operational history makes later subtraction less credible ([NIST GenAI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf); [Google SRE toil](https://sre.google/sre-book/eliminating-toil/)).

## Four Operating Models

| Model | What is shared | Where work goes | Best fit / primary failure | Evidence anchor |
|---|---|---|---|---|
| **No dedicated AI platform** | Existing Git, IAM, delivery, observability, security, and FinOps absorb AI work | Application and control teams perform integrations and reconciliation locally | Few workflows or strong incumbents / shadow spend, repeated reviews, uneven safety | GitHub and Backstage are already absorbing agent configuration and metadata ([GitHub](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents); [Backstage](https://backstage.io/docs/releases/v1.51.0/)). |
| **Contracts-only** | Versioned metadata, policies, templates, and conformance through source control or an existing portal | Teams retain runtime/domain responsibility; contract owners inherit semantics, reconciliation, migration | Discovery, ownership, attribution, governance / decorative or stale metadata | Backstage provides the source-controlled precedent and documents lifecycle drift ([catalogue](https://backstage.io/docs/features/software-catalog/); [lifecycle](https://backstage.io/docs/features/software-catalog/life-of-an-entity/)). |
| **Narrow managed capability** | One choke point such as provider access, routing, attribution, or tool authorization | Central team owns a bounded critical service and on-call; teams keep product logic/evaluation | Repeated cross-team control or toil / scope creep and common-mode failure | NIST and AWS are converging on agent identity and policy boundaries ([NIST](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative); [AWS](https://aws.amazon.com/about-aws/whats-new/2026/03/policy-amazon-bedrock-agentcore-generally-available/)). |
| **Broad integrated platform** | Catalogue, portal, gateway, runtime, evaluation, observability, governance, deployment | Central product/SRE imports lifecycle work; domain teams still supply truth and risk acceptance | Large repeated glue or regulated legacy queues / golden cage, lock-in, broad blast radius | Michelangelo and TFX demonstrate first-party scale economies, not a general threshold ([Uber](https://www.uber.com/us/en/blog/scaling-michelangelo/); [TFX](https://www.usenix.org/system/files/opml19papers-baylor.pdf)). |

No model dominates categorically. Contracts-only is the most credible first experiment; a narrow managed service is the strongest likely steady state when identity, delegated authority, or attribution problems genuinely repeat. Broad integration has demonstrated economies in first-party Uber and TFX cases, but no transferable threshold; no dedicated platform remains valid when incumbents solve the jobs ([Uber](https://www.uber.com/us/en/blog/scaling-michelangelo/); [TFX](https://www.usenix.org/system/files/opml19papers-baylor.pdf); [CNCF/SlashData](https://www.cncf.io/announcements/2026/03/24/cncf-and-slashdata-report-finds-platform-engineering-tools-maturing-as-organizations-prepare-for-ai-driven-infrastructure/)).

## Money, Power, and Stakeholder Impact

The four models relocate the same work—schema stewardship, integration, evaluation, access control, cost allocation, audit evidence, incidents, upgrades, and exit—onto different budgets. A small central invoice can coexist with high distributed labor; a broad central product can lower local repetition while importing permanent fixed cost ([Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)).

### Directed money-flow map

| From → to | Flow | Amount / trigger | Model effect | Evidence |
|---|---|---|---|---|
| **Application team / business unit → model or cloud provider** | Inference, storage, retrieval, evaluation, networking, support | Per token, request, storage unit, evaluator, capacity commitment, or contract; one Bedrock example is **$2 / $10 per 1M input/output tokens** through 2026-08-31 | Direct under no-platform; attributed/routed under narrow; bundled with more services under broad; contract-only mainly adds labels | [AWS pricing](https://aws.amazon.com/bedrock/pricing/) |
| **Enterprise → commercial portal / orchestrator vendor** | Subscription, support, implementation, professional services | **Unknown:** public Spotify Portal and Humanitec pages do not publish a general enterprise price | Absent in pure OSS contracts-only; most likely and largest under broad integration | [Spotify Portal](https://backstage.spotify.com/docs/portal); [Humanitec](https://developer.humanitec.com/platform-orchestrator/docs/platform-orchestrator/overview/) |
| **Enterprise → platform workforce and contractors** | Wages, benefits, recruiting, product, UX, support, on-call | Continuous; **$148,100** US mean software-developer wage is a reference, not loaded cost | Existing owners may absorb contract work; narrow concentrates a bounded team; broad needs a continuing product/SRE organization | [US BLS](https://www.bls.gov/news.release/ocwage.t01.htm); [Backstage adoption](https://backstage.io/docs/overview/adopting/) |
| **Application teams → central platform team** | Internal funding, chargeback/showback, requirements, tickets, contributed engineering | Organization-specific and **Unknown** here | Lowest visible flow under contracts-only; grows with managed scope; under no-platform it reappears as reactive advice and reconciliation | Puppet found **82%** of platform teams supported multiple business units ([Puppet](https://www.puppet.com/system/files/report-puppet-sodor-2023-platform-engineering.pdf)) |
| **Platform team → application teams** | Paved-road automation, templates, support, migrations, incident help | Non-cash internal service; **Unknown** | The actual value flow; contract-only supplies semantics, narrow one operational service, broad more lifecycle work | CNCF defines platform success indirectly through users ([CNCF](https://tag-app-delivery.cncf.io/es/whitepapers/platforms/)) |
| **Application teams → application teams / control functions** | Duplicate integration, evaluation, security review, audit evidence, support, incident work | Hidden in delivery budgets; **Unknown** | Highest and least visible with no dedicated platform; material under contracts-only; reduced only for capabilities actually centralized | [Puppet](https://www.puppet.com/system/files/report-puppet-sodor-2023-platform-engineering.pdf); [Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full) |
| **Component-owning teams → contract / catalogue owner** | Metadata authoring, correction, ownership confirmation, schema migration | Internal labor at every lifecycle or ownership change; **Unknown** | Defining work of contracts-only and still present under portal models | [Backstage catalogue](https://backstage.io/docs/features/software-catalog/) |
| **Platform operator → cloud, identity, database, network, and observability suppliers** | Runtime and integration consumption | Architecture- and contract-specific; **Unknown** | None for a document/schema alone, bounded for a gateway, multiple coupled services for broad integration | [Frontiers component review](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full) |
| **Parent company → cloud/platform business unit** | Equity, intercompany service, transfer pricing, shared infrastructure allocation | Not separable as AI-platform flow | Relevant to vendor incentives, not the internal buyer’s TCO | Amazon, Microsoft, and Alphabet disclose broad cloud segments, not AI-platform accounts ([Amazon](https://www.sec.gov/Archives/edgar/data/1018724/000101872426000004/amzn-20251231.htm); [Microsoft](https://www.microsoft.com/investor/reports/ar25/index.html); [Alphabet](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm)) |
| **Operator ↔ government** | Taxes, fees, grants, procurement, fines | **Not applicable at this design-question level:** no entity, grant, infringement, or procurement is proposed | Add only when a named use case or transaction makes it real | EU duties remain actor- and risk-specific ([European Commission](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)) |
| **Vendor → enterprise on outage or termination** | SLA credits, refunds, rebates, migration help, data return/deletion | **Unknown:** contract-specific | Managed paths may provide remedies; broad dependence makes exit help more important | Inspect the order form, MSA, DPA, SLA, and exit schedule; product pages are insufficient. |

### Power and authority map

| Decision | Formal decider and approval sequence | Veto / soft influence | Reversal condition |
|---|---|---|---|
| **1. Whether a dedicated AI platform exists** | Accountable CTO/CIO/VP Engineering or delegated investment council: documented constraint → baseline/users → incumbent and no-platform comparison → security/privacy/legal/finance review → named product and operational owner → continuing funding | Budget, security/privacy, architecture, and procurement can veto; AI advocates, consultants, vendors, and a newly hired platform leader shape the agenda without proving necessity | Constraint disappears; total central-plus-distributed cost exceeds baseline; retention/task success stays poor; an incumbent absorbs the job. Puppet notes platform work needs continuing product funding and records consultant/top-down triggers ([Puppet](https://www.puppet.com/system/files/report-puppet-sodor-2023-platform-engineering.pdf)). |
| **2. What enters the shared contract or product scope** | Platform product owner for scope; domain, security, data, finance, and architecture owners for their semantics: user research → smallest workflow → design → real adopters → task-success test → general availability | Domain team can veto inaccurate metadata/evals; risk owners can veto unsafe access; vendors benefit when maturity is defined as more integration | Low voluntary use; rising exceptions; reduced independence or delivery stability; field has no decision consumer. DORA recommends one golden path and extensibility ([DORA](https://dora.dev/capabilities/platform-engineering/)). |
| **3. Whether use is mandatory and who grants exceptions** | Accountable policy/risk owner, not the platform team: identify obligation → define minimum control/evidence → normal path → exception authority/expiry → user test → audit compliance and bypass | Statutory/sectoral owner and business risk owner can veto; platform defaults exert soft power; teams exert de facto power through bypass | Mandate lowers task success without reducing named risk; bypass grows; exception volume shows a golden cage. Spotify says adoption had to be earned by being the better option ([Spotify](https://engineering.atspotify.com/2021/5/a-product-story-the-lessons-of-backstage-and-spotifys-autonomous-culture)). |
| **4. Whether to shrink, replace, or remove** | Service owner proposes; technology, business-risk, records, procurement, and dependent product owners approve: dependency inventory → actual usage → incident/audit/financial impact → replacement/no-replacement → exit review → migration → verification | Critical dependency, records duty, contractual commitment, and failed migration can veto; sunk-cost owners and vendor customer-success teams resist informally | Failed migration, unowned control gap, or total exit cost exceeds avoided continuing cost. Deep integrations create value and lock-in simultaneously ([Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)). |

### Stakeholder impact

Direction and magnitude are relative to decentralized teams consuming existing cloud/model services; magnitude remains **Unknown** where no organization-specific baseline exists.

| Stakeholder | Contracts-only | Narrow managed | Broad integrated | Direction / magnitude | Source |
|---|---|---|---|---|---|
| Application engineers | Maintain metadata and runtime freedom; repeat integrations | One access/cost/policy path; retain product logic | Lifecycle convenience with abstractions and central roadmap | Mixed; material at scale | DORA ties benefit to independence; Frontiers documents learning and over-engineering risk ([DORA](https://dora.dev/capabilities/platform-engineering/); [Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)) |
| Non-engineer builders / reviewers | Contract may be unusable without generator or existing UI | Governed façade may help but workflow UI remains | Most likely to provide usable review/approval surface | Mixed; unknown | General GUI and low-code evidence supports segmentation by expertise, not one interface ([GUI/TUI study](https://pmc.ncbi.nlm.nih.gov/articles/PMC2655855/); [low-code review](https://www.sciencedirect.com/science/article/pii/S259011842200082X)) |
| Platform engineers | Small formal scope but schema, adoption, support, migration remain | Own bounded critical service and on-call | Gain headcount/authority; inherit plugins, SRE, support, roadmap | Mixed; material | Backstage lists central ownership and eventual on-call ([Backstage](https://backstage.io/docs/overview/adopting/)) |
| Security, privacy, compliance, audit | Common inventory language but truth still requires verification | Central access and logs for routed calls | Strong defaults with larger common-control blast radius | Mixed; material for consequential use | A Backstage owner field is not runtime authorization; EU duties remain use-specific ([Backstage](https://backstage.io/docs/features/software-catalog/descriptor-format/); [Commission](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)) |
| Finance / FinOps | Labels enable showback only if carried end-to-end | Central provider/cost metadata and budgets | Broad dashboards but bundled allocation can remain opaque | Wins under narrow; mixed under broad; material | 98% of surveyed practitioners manage AI spend; AWS only standardized Bedrock export metadata on 2026-07-20 ([FinOps](https://data.finops.org/); [AWS](https://aws.amazon.com/about-aws/whats-new/2026/07/aws-data-exports-amazon-bedrock-product-metadata/)) |
| Product / business owners | Keep accountability with inconsistent evidence | Comparable usage/cost, not automatic value | Faster prototyping but platform activity can be mistaken for business success | Exposed; material | Conflicting RCTs show why task context matters ([METR](https://metr.org/Early_2025_AI_Experienced_OS_Devs_Study-paper.pdf); [Google RCT](https://arxiv.org/abs/2410.12944)) |
| Incident response / operations | Ownership lookup helps only when current | Gateway gives one choke point and dependency | Central coordination with larger blast radius | Mixed; material | Spotify reports catalogue discoverability; Cloudflare shows control-plane dependency risk ([Spotify](https://engineering.atspotify.com/2021/5/a-product-story-the-lessons-of-backstage-and-spotifys-autonomous-culture); [Cloudflare](https://blog.cloudflare.com/post-mortem-on-cloudflare-control-plane-and-analytics-outage/)) |
| Procurement / legal | Maintain approved terms/provider metadata | Negotiate fewer provider paths | Larger, stickier contract and exit plan | Mixed; material | Hyperscaler filings bundle AI with broad cloud estates ([Amazon](https://www.sec.gov/Archives/edgar/data/1018724/000101872426000004/amzn-20251231.htm); [Microsoft](https://www.microsoft.com/investor/reports/ar25/index.html); [Alphabet](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm)) |
| Existing developer/IAM/observability/data teams | Gain relevance; absorb AI schema and consumers | Often natural home for the narrow service | Risk duplication or forced integration | Mixed; material | Backstage’s model is extensible and repository-owned ([Backstage descriptor](https://backstage.io/docs/next/features/software-catalog/descriptor-format/)) |
| Executives | Low initial spend and optionality; less visible transformation | Bounded investment with a measurable control goal | Visible standardization, vendor relationship, and sunk cost | Mixed; unknown | Puppet found 48% said senior management did not understand platform value ([Puppet](https://www.puppet.com/system/files/report-puppet-sodor-2023-platform-engineering.pdf)) |
| Model / cloud vendors | Contracts can make substitution easier | Consolidated traffic with routing competition | More consumption, adjacent services, and switching cost | Vendor wins; material | Vendor filings do not disclose stand-alone AI-platform revenue ([Amazon](https://www.sec.gov/Archives/edgar/data/1018724/000101872426000004/amzn-20251231.htm); [Microsoft](https://www.microsoft.com/investor/reports/ar25/index.html); [Alphabet](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm)) |
| Customers, employees, citizens | Depend on each team’s competence | More consistent routed controls; product failures remain | Stronger defaults but larger shared blast radius and opaque flows | Exposed without consent; potentially existential in high-impact use | EU obligations follow actor and use, not internal platform adoption ([Commission](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)) |
| Open-source maintainers / plugin contributors | Small, forkable core | Integrations create compatibility work | Ecosystem externalizes upgrades and security surface | Mixed; materially underpriced | Backstage is Apache-2.0; the review notes 800+ plugins of varied quality/status ([FAQ](https://backstage.io/docs/faq/product/); [Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)) |

### Under-recognized winners, losers, and exposed parties

The quiet winner in contracts-only is the **existing platform estate**—Git, identity, Backstage, observability, and FinOps—which gains relevance while its maintainers inherit schema, ingestion, migration, and support work. The quiet winner in a broad design is the vendor whose AI entry point expands cloud, data, security, support, and commitment revenue; broad cloud revenue must not be mistaken for AI-platform revenue. The quiet losers are application teams asked to keep metadata and evaluation evidence current without capacity, and platform teams told to operate an internal product “part time.” Finance, audit, incident response, open-source maintainers, and end users are exposed without choosing the architecture: the first three inherit reconciliation and failure work, maintainers absorb “free” compatibility labor, and customers, employees, or citizens bear privacy, discrimination, security, and service-quality consequences that adoption metrics do not capture ([Backstage adoption](https://backstage.io/docs/overview/adopting/); [European Commission](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)).

## Subtraction and Reversibility

Three cases prevent “remove it later” from becoming hand-waving.

**Google Omega:** Google planned a cleaner successor to Borg. Borg improved faster than expected, Omega’s benefits were overestimated, and migration would have required moving millions of configuration lines across thousands of services while running both systems for years. Useful Omega ideas were folded into Borg and Kubernetes. The lesson is to compare a new platform with the improved future incumbent, not with today’s frustrations ([Google SRE](https://sre.google/workbook/simplicity/); [Google Research](https://research.google/pubs/borg-omega-and-kubernetes/)).

**GOV.UK PaaS:** GDS retired a platform with 99.95% uptime, one major incident over seven years, 172 services, and 3,200 applications. Public-cloud capability and departmental skill had improved, growth lagged, full cost recovery was not possible, and renewal required major architectural investment ([GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/); [live assessment](https://www.gov.uk/service-standard-reports/gov-dot-uk-platform-as-a-service-paas-live-assessment)). Yet an 18-month central sunset became multi-year downstream work; one department describes migrating 41 critical services with coordinated cutovers and out-of-hours work ([DBT](https://digitaltrade.blog.gov.uk/2025/05/12/delivering-seamless-migrations-and-a-future-ready-platform/)). The lesson is that retirement can be correct and still expensive.

**Google filer retirement:** Google examined actual use across 2.5 billion files, 300 TB, 60,000 users, and 60 sites. It used several specialized replacements because no single successor served every job, phased cohorts, created self-service tooling only when needed, and kept the team deliberately lean. The lesson is that subtraction often means replacing a broad shared system with several narrower capabilities, not building another universal platform ([Google SRE Workbook](https://sre.google/workbook/eliminating-toil/)).

A reversible capability therefore needs, from creation:

- a versioned interface and consumer inventory;
- actual usage telemetry, not declared ownership alone;
- portable configuration, evidence, and state where applicable;
- a compatibility and deprecation policy ([Kubernetes](https://kubernetes.io/docs/reference/using-api/deprecation-policy/));
- one tested representative migration;
- last-known-good or rollback behavior;
- explicit exit funding and a decision date.

## Counter-Narratives

| Working claim | Competing explanation and disconfirming evidence | What would falsify the competing explanation | Current read |
|---|---|---|---|
| The minimum is a distinct AI capability. | **“AI platform” mostly rebrands developer platform, DataOps, IAM, observability, CI/CD, security, and FinOps.** A mapping study finds 35 MLOps components and roots the field in DevOps; CNCF/SlashData reports 35% using hybrid existing-platform-plus-specialist-tooling approaches; Backstage already aggregates ordinary platform categories ([mapping](https://arxiv.org/abs/2406.19847); [CNCF/SlashData](https://www.cncf.io/announcements/2026/03/24/cncf-and-slashdata-report-finds-platform-engineering-tools-maturing-as-organizations-prepare-for-ai-driven-infrastructure/); [Backstage plugins](https://backstage.io/plugins/)). | A multi-organization capability inventory showing most recurring cost or risk cannot be handled by incumbents and is uniquely model- or agent-dependent. | Counter leads, except for probabilistic evaluation, combined model/prompt/retrieval/tool provenance, and delegated-action controls ([production-ML interviews](https://arxiv.org/abs/2209.09125); [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)). |
| A contract, template, library, or CLI is smaller than a managed platform. | **Thin scope exports adapters, policy interpretation, audit evidence, support, and incident work.** The classic ML-debt paper places most engineering outside the model; DORA hypothesizes that handoffs and added machinery explain throughput penalties; Backstage lists 246 active plugins while warning community plugins are not fully vetted ([ML debt](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf); [DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf); [plugins](https://backstage.io/plugins/)). | End-to-end time-and-motion data showing contracts-only reduces combined platform, product, risk, support, audit, and incident labor rather than only central headcount. | Counter leads; apparent minimality is often an accounting boundary. |
| Broad scope is platform bloat. | **Integration can have economies of scope at scale.** Michelangelo replaced bespoke systems across hundreds of use cases and thousands of models; TFX pipelines served hundreds of teams ([Uber](https://www.uber.com/us/en/blog/scaling-michelangelo/); [TFX](https://www.usenix.org/system/files/opml19papers-baylor.pdf)). | Comparable organizations achieving the same reuse, reliability, and governance with independent thin capabilities at lower total cost and no extra integration burden. | Roughly even: first-party scale cases are concrete but promotional, and Uber later created specialist platforms when the general one stopped fitting. |
| A dedicated UI is optional. | **A UI is minimum infrastructure for non-engineers, occasional users, approvers, and auditors.** Novices completed equivalent tasks in less time and fewer steps with a GUI; a low-code review makes usability central for non-programmers ([GUI/TUI study](https://pmc.ncbi.nlm.nih.gov/articles/PMC2655855/); [low-code review](https://www.sciencedirect.com/science/article/pii/S259011842200082X)). | Task studies in the actual mixed cohort showing equal completion, error, accessibility, and support outcomes through API/CLI/chat alone. | Counter leads for mixed cohorts; API/CLI may remain sufficient for frequent experts. |
| A Backstage-consumed metadata contract can itself be the platform. | **A contract without conformance, freshness, ownership, and consequences is documentation.** Architecture research separates decision agreement from implementation conformance; policy-as-code research requires explicit enforcement; Backstage users were blocked by guidance that had drifted nearly 20 versions ([architecture enforcement](https://www.sciencedirect.com/science/article/pii/S0164121218301614); [policy as code](https://researchportal.vub.be/en/publications/an-empirical-study-of-policy-as-code-adoption-purpose-and-mainten/); [Backstage issue](https://github.com/backstage/backstage/issues/22162)). | Longitudinal evidence that voluntary contracts remain complete, current, semantically correct, and audit-ready without automated or human conformance work. | Counter leads. The contract can be the interface, but validation and enforcement are real capability. |
| Removability makes a platform smaller. | **Deletion is an option with a large exercise price.** GOV.UK’s 18-month sunset generated multi-year migrations, including 41 critical services; a 104-expert cloud-migration study describes migration as difficult and costly ([GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/); [DBT](https://digitaltrade.blog.gov.uk/2025/05/12/delivering-seamless-migrations-and-a-future-ready-platform/); [migration study](https://arxiv.org/abs/2004.10724)). | A full-cost case where migration and product opportunity cost are lower than the discounted owner cost avoided. | Inconclusive on final economics; decisive that exit work is material. |
| Helping teams build can be separated cleanly from running agents. | **For agents with write authority, build metadata and runtime identity, authorization, audit, and approval form one loop.** MCP uses OAuth-based, audience-bound authorization and OWASP recommends least privilege and human approval for high-impact action ([MCP](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization); [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)). | Evidence that build-time contracts alone reliably constrain production tool use across model, prompt, data, and tool changes. | Counter leads for consequential write access; separation remains plausible for low-risk read-only workflows. |

### Whose interests does the framing serve?

“Start with almost nothing” protects application-team autonomy and makes a proposal easy to approve, but can let product teams externalize assurance to security, finance, audit, and incident response. A new AI-platform label can secure a central team’s budget and architectural authority; a tiny contract can secure the same foothold by appearing cheap. Control functions prefer common inventory and evidence because distributed exceptions are expensive for them, not because one platform is necessarily efficient. “No UI” privileges frequent technical users unless another surface translates for non-engineers. Platform vendors and category makers benefit when maturity means more integrated capability: PlatformEngineering.org says its conceptual framework grew alongside Humanitec’s product, while Spotify now sells managed Portal and commercial plugins around the open-source Backstage ecosystem ([PlatformEngineering.org](https://platformengineering.org/about); [Humanitec](https://humanitec.com/platform-engineering); [Spotify Portal](https://info.backstage.spotify.com/get-portal); [Spotify FAQ](https://backstage.spotify.com/faqs/)). Survey publishers also have incentives: the Frontiers review flags vendor bias in Port and Humanitec material, and DORA is run by Google Cloud even though it publishes methods and negative findings ([Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full); [DORA overview](https://dora.dev/research/2024/dora-report/)).

## Community Pulse

This is a purposive sample of implementation, migration, maintenance, adoption, and production-failure discussions—not a representative survey. “Active” and “Heavy” describe what the search surfaced, not population prevalence. Anonymous accounts provide mechanisms and texture; vendor, employer-product, and consultancy stakes are identified.

### Where the conversation lives

| Platform / community | Rough volume in this search | Dominant frame |
|---|---:|---|
| **Hacker News** | Active | Does shared infrastructure remove distributed operations and compliance work, or replace understandable systems with wrappers and a larger organization? The central thread had 112 points and 49 comments when captured ([HN](https://news.ycombinator.com/item?id=36465220), 2023-06-25). |
| **Reddit: r/devops, r/kubernetes, r/AI_Agents, r/aiagents** | Heavy, noisy | Templates versus portals, required team size, catalogue drift, trace/eval/identity failures, and whether runtime ownership follows agent adoption ([r/devops](https://www.reddit.com/r/devops/comments/1kg3gj4/what_really_makes_an_internal_developer_platform/); [r/AI_Agents](https://www.reddit.com/r/AI_Agents/comments/1tbwlqw/are_you_actually_running_ai_agents_in_production/)). |
| **GitHub issues / discussions** | Active | Mechanics omitted by product narratives: schema consistency, soft versus hard errors, trace models, authorization, and non-engineer review UI ([Backstage #26093](https://github.com/backstage/backstage/issues/26093); [Langfuse](https://github.com/orgs/langfuse/discussions/11391)). |
| **LinkedIn** | Active, vendor-heavy | Named experience travels with vendor selection, consulting, and training incentives; setup cost and evaluation practice recur ([David Tuite](https://www.linkedin.com/posts/davidtuite_backstage-has-a-skills-mismatch-problem-activity-7402737541109764097-8hDS); [Hamel Husain](https://www.linkedin.com/posts/hamelhusain_the-most-common-mistake-teams-make-when-building-activity-7438260194305986560-ePtK)). |
| **Named blogs / company engineering** | Active | Start with an outcome, buy or reuse before building, and integrate with real source-of-truth systems ([Chad McElligott](https://chadxz.dev/platform/); [Zalando](https://engineering.zalando.com/posts/2023/08/sunrise-zalandos-developer-platform-based-on-backstage.html)). |
| **PlatformEngineering.org** | Heavy, commercially entangled | Golden paths, opt-in adoption, portals as optional front ends, and platform-as-product; the site grew from work around Humanitec ([about](https://platformengineering.org/about/)). |
| **USENIX / conference talks** | Active | A portal is a multi-year product and adoption programme, not an installable result ([Mauritius Commercial Bank](https://www.usenix.org/conference/srecon25emea/presentation/mckenzie); [Tony McCulley](https://www.usenix.org/conference/srecon23americas/presentation/mcculley)). |
| **X, public Discord/Slack, YouTube comments** | Search completed; no auditable corpus | Public search was login-gated, invite-only, or exposed relative dates rather than exact publication dates. These venues contribute an honest access limitation, not a negative sentiment result ([X search](https://x.com/search?q=%22Backstage%22%20%22platform%20engineering%22&src=typed_query); [Backstage Discord](https://discord.com/servers/backstage-687207715902193673); [CNCF group](https://ocgroups.dev/cncf/group/platform-engineering-technical-community-group); [YouTube](https://www.youtube.com/watch?v=n1IrNe5MmZg)). |

### Sentiment range

- **Strong supporters — about one-fifth of sampled excerpts.** They cluster at enterprise or regulated scale where shared standards collapse long approval queues and many local runbooks. Zalando’s Lacey Nagel wrote, “Users really celebrated a deeper integration,” while the four-person team synchronized 40,000+ entities daily ([Zalando Engineering](https://engineering.zalando.com/posts/2023/08/sunrise-zalandos-developer-platform-based-on-backstage.html), **2023-08-03**; employer-project stake).
- **Cautiously positive — about one-third, the largest group.** They want one narrow journey, a “good enough” 80%, and escape hatches. Chad McElligott’s formulation is “only ~80% of our vision ... can often be ‘good enough’ for now” ([How Platform Engineering Works](https://chadxz.dev/platform/), **2023-06-24**; named practitioner, no relevant commercial stake disclosed).
- **Sceptical but engaged — about one-third.** They accept the coordination problem but challenge scope, ownership cost, and wrappers that obscure underlying failures. Their typical question is whether the portal removes work or moves it.
- **Hostile — less than one-sixth.** Hostility focuses on “god systems,” forced adoption, and needing a platform team to debug routine infrastructure. The memorable language is useful sentiment, not proof of system performance.
- **Confused / asking basic questions — about one-fifth, overlapping all categories.** Engineers repeatedly cannot tell whether “platform” means catalogue, portal, framework, workflow engine, infrastructure control plane, or managed runtime.

### Practitioner takes the press missed

> “In mine devs just use Terraform modules and follows the README.md files. We require like 2 variable inputs to the modules, naming convention etc is all taken care of, cicd captures all required logging and permissions on environments means security is taken care of.”
>
> — `darkklown`, r/devops, [direct thread](https://www.reddit.com/r/devops/comments/1kg3gj4/what_really_makes_an_internal_developer_platform/), **2025-05-06**. Anonymous practitioner; no disclosed vendor stake.

This is the strongest concrete contracts-and-templates example: a shared module, defaults, README, and CI can be a platform capability without a portal or runtime. It does not generalize to organizations where legacy approvals and integrations dominate the remaining work.

> “our backstage is wildly used across the whole company, thousands visit it every week. But we also have a team of 20 dedicated to maintaining it and its ecosystem.”
>
> — `Jmc_da_boss`, r/devops, [direct thread](https://www.reddit.com/r/devops/comments/1kg3gj4/what_really_makes_an_internal_developer_platform/), **2025-05-06**. Anonymous practitioner; no disclosed vendor stake.

This is not a contradiction. A large product team can be economical across thousands of users and decades of approval integration. The missing denominator is the queues removed and the work that remains outside the 20-person team.

> “Backstage works until the team that set it up rotates out, then the catalog drifts and you've got a portal showing services that were deprecated months ago. The model assumes someone owns the YAML; in practice nobody does.”
>
> — `OkProtection4575`, r/kubernetes, [direct thread](https://www.reddit.com/r/kubernetes/comments/1tcc53b/whats_your_experience_with_internal_developer/), **2026-05-14**. Anonymous practitioner; no vendor stake disclosed.

Backstage maintainer `freben` supplies the more nuanced mechanism: “there's no such thing as atomic company wide updates to an entire model” ([GitHub issue #26093](https://github.com/backstage/backstage/issues/26093), **2024-08-22**; maintainer/employer-project stake). The minimum therefore includes provenance, reconciliation, visible stale/unknown states, and an explicit warn-versus-block choice.

> “the current UI/UX experience sometimes leads them in circles”
>
> — `xstraven`, Langfuse roadmap discussion, [direct discussion](https://github.com/orgs/langfuse/discussions/11391), **2026-01-05**. Product user; no commercial stake disclosed.

The same user said “the non-technical domain experts would be the main focus” on **2026-01-06**. A builder UI may be optional while a review and approval UI is load-bearing for customer-service representatives, product managers, auditors, and risk owners.

> “evaluation ended up being a much bigger problem than we expected. once workflows got longer, prompt-level tests stopped telling us much.”
>
> — `Radiant-Anteater-418`, r/AI_Agents, [direct thread](https://www.reddit.com/r/AI_Agents/comments/1tbwlqw/are_you_actually_running_ai_agents_in_production/), **2026-06-06**. Anonymous practitioner; later mentions a commercial evaluation tool, so commercial influence is possible.

This distinguishes build enablement from runtime ownership. Multi-step agents add state, tool authority, provenance, human review, and cross-agent trace continuity without proving that one shared runtime is the answer.

> “So don't depend on or adopt their tools.”
>
> — `tvararu`, Hacker News, [GOV.UK PaaS discussion](https://news.ycombinator.com/item?id=32067879), **2022-07-12**. Long-time user and early research participant; no vendor stake disclosed.

The same account listed IAM, service-principal, naming, support, and incident work the PaaS had removed. Retirement exports work and changes trust in the next shared service.

### The authentic joke and what it compresses

> “infrastructure the infrastructure?”
>
> — `cmckn`, Hacker News, [Backstage launch discussion](https://news.ycombinator.com/item?id=22593568), **2020-03-16**. Pseudonymous commenter; no disclosed stake.

The joke compresses the dominant suspicion: a portal can add navigation and maintenance without removing underlying infrastructure work. The AI-specific variant asks whether teams are “just vibes-checking outputs and praying” ([`Old_Medium5409`, r/aiagents](https://www.reddit.com/r/aiagents/comments/1rfscdx/whats_your_honest_tier_list_for_agent/), **2026-02-27**; anonymous account), which compresses the gap between traces and defensible evaluation.

### Most-cited confusion or misreading

The most persistent confusion is **portal = platform**. “Or a framework? Or both?” asked `beardedman` ([Hacker News](https://news.ycombinator.com/item?id=22593568), **2020-03-16**; pseudonymous commenter). Backstage is a framework for building portals; a portal may be the front door to a broader platform, while the platform may exist without that front door. The confusion becomes commercially motivated when a managed product’s convenience is compared with an open-source framework’s setup burden as if they were the same scope.

### Honest silence result

No actor is conspicuously silent in the journalistic sense because Chapter 3 is an evergreen design inquiry, not a launch, dispute, or decision that creates a duty to respond. Naming a person as silent would manufacture a news frame. Relevant maintainers and operators do appear in GitHub, first-party engineering posts, practitioner blogs, and conferences; X, Discord/Slack, and YouTube did not yield a publicly retrievable, exact-dated implementation corpus, which is a retrieval limitation rather than evidence of silence.

## Scenarios

These are decision priors as of **2026-07-29**, not frequencies derived from a population. They sum to 100% and should be updated with local task-success, cost, risk, and reversibility data; the evidence base is too immature for confident population forecasting ([Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)).

### Base — Contracts become the platform

**Probability: Plausible — 35%.** Open contracts, DORA’s minimum viable platform, and Backstage’s AI metadata trajectory make the mechanism credible; the probability is capped because contracts neither enforce runtime authority nor guarantee usable interfaces for mixed cohorts ([CNCF](https://tag-app-delivery.cncf.io/es/whitepapers/platforms/); [DORA](https://dora.dev/capabilities/platform-engineering/); [Backstage v1.51](https://backstage.io/docs/releases/v1.51.0/)).

A versioned agent contract, conformance tests, and an existing Backstage or source-control surface remove enough discovery, ownership, attribution, and governance friction that no new portal or runtime is justified.

**Trigger conditions**

- at least three materially different teams adopt the same contract voluntarily;
- at least 80% of representative users complete the target workflow unassisted;
- required fields remain at least 90% conformant over two monthly samples;
- median waiting and support effort do not rise more than 10%;
- no incident or review reveals a need for common runtime enforcement.

**Leading indicators over 6–12 months**

- Backstage’s `AiResource` and `mcp-server` types move toward stable semantics without forcing catalogue forks ([Backstage v1.51](https://backstage.io/docs/releases/v1.51.0/)).
- Enterprise-scoped Markdown agent definitions and rulesets become ordinary repository governance ([GitHub enterprise agents](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents)).
- OpenTelemetry stabilizes agent, tool, data-source, evaluation, and usage identifiers ([OpenTelemetry registry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/)).
- Exceptions expire and teams do not create shadow registries or request a separate portal to understand the contract.

**Downstream effects:** the existing developer platform gains strategic weight; schema owners and migration tooling become the real platform team; vendor substitution becomes easier only where semantics are portable; and removal stays comparatively cheap if consumers and versions remain explicit.

### Upside — One narrow managed choke point earns its keep

**Probability: Plausible — 40%.** This is the highest-weight scenario because identity, delegated tool authority, and attribution are genuinely agent-sensitive shared boundaries, while centralizing them does not require owning every agent lifecycle stage ([NIST initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative); [AWS AgentCore Policy](https://aws.amazon.com/about-aws/whats-new/2026/03/policy-amazon-bedrock-agentcore-generally-available/)).

A gateway for model access, cost attribution, or agent-tool authorization removes a measured cross-team constraint while teams retain agent design, deployment, evaluation, and business outcomes.

**Trigger conditions**

- the same consequential access, audit, attribution, or authorization problem repeats across at least three teams;
- a pilot cuts that constraint by at least 30%;
- 80% or more retain the path voluntarily after eight weeks;
- bypass remains below 10% and latency stays within the declared budget;
- a representative agent can leave the gateway without proprietary runtime migration.

**Leading indicators over 6–12 months**

- NIST’s agent-identity work produces an implementable profile satisfiable at an identity/policy boundary rather than across a whole lifecycle ([NIST](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)).
- MCP authorization converges on per-user, per-agent, per-tool, and per-request scope rather than shared static credentials ([MCP authorization](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2025-03-26/basic/authorization.mdx)).
- Gateways expose policy decisions, identities, costs, traces, and exportable logs; AWS already documents log-only and enforced modes ([AWS policy docs](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/policy.html)).
- The support queue stays bounded rather than expanding into hosting, memory, prompt, UI, and business-evaluation demands.

**Downstream effects:** identity, observability, and FinOps become co-owners; the service needs on-call, limits, fallback, and decommission tests early; one wrong policy creates common-mode denial or permission; success becomes constraint removal rather than routed-agent count.

### Downside — The minimum expands before evidence arrives

**Probability: Modest — 15%.** Commercial bundles and demand for visible control create scope pressure, but mature guidance now explicitly argues for minimum viable scope, extensibility, feedback, and outcomes ([Microsoft Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/azure-openai-in-azure-ai-foundry); [Google Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/reasoning-engine/overview?authuser=3); [DORA](https://dora.dev/capabilities/platform-engineering/)).

Catalogue, gateway, runtime, evaluation, observability, governance, and deployment become one mandatory product before a baseline or one proven workflow exists.

**Trigger conditions**

- four or more lifecycle categories enter scope before one target outcome is measured;
- success is reported as registrations, agents, portal visits, or token volume;
- mandatory adoption exceeds 80% while unassisted completion or voluntary retention stays below 60%;
- more than 25% of teams require exceptions or custom plugins;
- one representative migration cannot be completed within ten engineer-days.

**Leading indicators over 6–12 months**

- Vendor bundles keep adding runtime, memory, gateway, policy, identity, observability, evaluation, and deployment under one management plane ([Microsoft](https://learn.microsoft.com/en-us/azure/ai-foundry/azure-openai-in-azure-ai-foundry); [Google](https://cloud.google.com/vertex-ai/generative-ai/docs/reasoning-engine/overview?authuser=3)).
- Backstage’s agent-facing actions expand faster than delegated permissions and ownership data mature; some external-authentication paths remain experimental and static-token support temporary ([Backstage MCP actions](https://backstage.io/docs/ai/mcp-actions/)).
- Platform hiring and vendor commitments precede task baselines; roadmaps describe feature coverage rather than removed constraints.
- Support tickets, exceptions, and plugin backlog rise after nominal adoption.

**Downstream effects:** autonomy becomes exception management; the central team imports permanent operations and authority; a shared policy or runtime error gains a larger blast radius; cloud bundles pressure stand-alone vendors; and failure can discredit useful narrow controls with unnecessary ones.

### Wildcard — The category disappears into incumbents

**Probability: Low — 10%.** Incumbents are absorbing many AI-aware fields and controls, but agent identity, delegated authority, variable model economics, and evaluation are likely to leave at least a contract or narrow shared service ([GitHub enterprise agents](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents); [Backstage v1.51](https://backstage.io/docs/releases/v1.51.0/)).

Git, Backstage, IAM, delivery, observability, security, and FinOps systems add enough agent-aware fields and controls that no dedicated AI platform or separate contracts program survives.

**Trigger conditions**

- fewer than two repeated consequential gaps remain after incumbent extension;
- existing identity and telemetry cover at least 90% of in-scope calls and ownership;
- audit accepts incumbent evidence without a separate registry or gateway;
- incumbent features repeatedly solve the same job within one planning cycle at lower support cost;
- no dedicated platform budget, on-call, or roadmap is needed.

**Leading indicators over 6–12 months**

- GitHub and Backstage continue turning agent configuration into repository-owned, organization-governed files and catalogue entities ([GitHub custom agents](https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/copilot-cli/use-copilot-cli/invoke-custom-agents); [Backstage v1.51](https://backstage.io/docs/releases/v1.51.0/)).
- FOCUS and cloud exports add provider-neutral model, token, GPU, agent, and owner attribution inside ordinary FinOps workflows ([State of FinOps](https://data.finops.org/)).
- OpenTelemetry and existing APM tools make provider-neutral agent traces routine ([OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/)).
- Incidents and audits find failures concentrated in product-specific data, workflow, and authorization design rather than missing common infrastructure.

**Downstream effects:** AI-platform work disperses into developer productivity, IAM, observability, security, data governance, and FinOps; the organization avoids a new common-mode dependency but accepts greater local variance; vendors market AI as extensions of established control planes; and governance becomes less visible as a programme.

## The 90-Day Signal

Measure the **unassisted task-success rate for one repeated, consequential workflow after introducing only a versioned contract and conformance tests**.

The window from the dossier date ends on **2026-10-27**. Choose one workflow crossing at least three teams—for example, registering an agent with a valid owner, provider and data constraints, cost centre, evaluation evidence, and incident contact. Give representative engineers and non-engineer builders the contract through their existing workflow. Audit correctness; do not accept self-report alone.

- **At least 80% unassisted success with no material control gap:** favor contracts-only.
- **Below 50%, with one gateway or generator removing the observed block:** favor narrow-managed.
- **Below 50% because several coupled lifecycle tasks remain:** test incumbent extensions before considering a broad platform.
- **No improvement over the existing direct path:** favor no dedicated platform and retire the experiment.

Track waiting time, support minutes, correction work, exceptions, audit-evidence effort, and cost around this signal. Agent count, portal visits, tokens, and support tickets are diagnostic context, not substitutes for successful completion. DORA ties platform value to developer independence and task success while warning that adoption can hide compulsion or poor fit ([DORA](https://dora.dev/capabilities/platform-engineering/)).

## Limitations

- No controlled, longitudinal, multi-organization study compares no platform, contract plus conformance, narrow-managed, and broad-integrated models across equivalent risk classes ([Frontiers](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)).
- No public total-cost ledger counts central and distributed labor, audit, incidents, exceptions, and migration in one model.
- No validated threshold based on team count, agent count, risk, or duplicated hours predicts when central integration becomes cheaper.
- The strongest quantitative platform studies are observational or vendor-associated. They reveal trade-offs but cannot establish causality.
- First-party cases such as Spotify, Uber, Netflix, Google, and GDS are rich in mechanism but may omit failed alternatives and organization-specific advantages.
- Community accounts are self-selected, sometimes anonymous, and commercially noisy. They support mechanisms and language, not prevalence.
- General GUI and low-code studies do not decide the interface for a specific internal AI workflow.
- Public records do not disclose a full economic comparison of continuing GOV.UK PaaS versus retirement.
- Agent capabilities and vendor bundles are changing quickly. The stable conclusion is the decision loop and evidence requirement, not any 2026 product boundary.

## Tensions and Open Questions

1. **What counts as success?** A faster builder journey can coexist with lower delivery stability, worse review queues, or weaker end-user outcomes. Which denominator is authoritative for each risk class ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf))?
2. **Where is the risk floor?** Which agent actions require runtime mediation, and which can remain governed by build-time contracts and downstream systems ([NIST](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations))?
3. **Who owns semantic truth?** Which fields are team declarations, which are observed automatically, and which require independent attestation?
4. **When should validation warn versus block?** Hard failure can prevent harm but also erase an entity from the catalogue or create waiting; soft failure preserves flow but can normalize stale data ([Backstage issue](https://github.com/backstage/backstage/issues/26093)).
5. **Which user needs which surface?** Can one contract serve engineers through Git and domain reviewers through a UI without creating competing sources of truth ([Langfuse discussion](https://github.com/orgs/langfuse/discussions/11391))?
6. **What is the crossover point for a managed runtime?** How much repeated authorization, state, retry, approval, and incident work justifies a common execution layer after on-call and blast-radius costs?
7. **Can the existing platform absorb the AI-specific fields?** The alternative is often not a new AI platform versus chaos, but extending Backstage, IAM, observability, FinOps, and delivery separately.
8. **How will common policy fail?** What continues on last-known-good state, what fails closed, who can grant exceptions, and how are policy versions correlated with decisions?
9. **What data should not be collected?** Portable trace semantics make collection easy; privacy, retention, redaction, and access still need a purpose-limited design.
10. **How is displaced work counted?** Which budgets record local adapters, audit preparation, manual review, debugging, migration, and incident reconstruction?
11. **What would falsify the platform?** Every capability needs a dated hold, shrink, replace, or remove threshold before adoption creates a constituency.
12. **What evidence would change the central answer?** The decisive study would independently compare all four operating models with full labor, governed task success, cohort-specific usability, incidents, exceptions, and exit cost.

## Receipts

This is the recomputed union of every distinct URL in `02-history.md` through `07-community.md`, including alternate canonical paths and fragment URLs where the angle files used them. Evidence types remain separated: official records and specifications are **Primary**; dated releases and announcements are **News**; research, surveys, and expert analyses are **Expert**; practitioner discussions are **Community**; discovery, product, and contextual material is **Background**.

### Primary

- <https://airc.nist.gov/airmf-resources/airmf/5-sec-core/>
- <https://aws.amazon.com/bedrock/pricing/>
- <https://aws.amazon.com/message/41926/>
- <https://backstage.io/assets/files/X41-Backstage-Audit-2024-eb8535297d6f2542b0d61bf73c87f7fc.pdf>
- <https://backstage.io/docs/ai/mcp-actions/>
- <https://backstage.io/docs/architecture-decisions/adrs-adr002/>
- <https://backstage.io/docs/faq/product/>
- <https://backstage.io/docs/features/software-catalog/>
- <https://backstage.io/docs/features/software-catalog/configuration/>
- <https://backstage.io/docs/features/software-catalog/descriptor-format/>
- <https://backstage.io/docs/features/software-catalog/extending-the-model/>
- <https://backstage.io/docs/features/software-catalog/life-of-an-entity/>
- <https://backstage.io/docs/features/software-catalog/software-catalog-api/>
- <https://backstage.io/docs/features/software-templates/>
- <https://backstage.io/docs/next/features/software-catalog/descriptor-format/>
- <https://backstage.io/docs/overview/adopting/>
- <https://backstage.io/docs/reference/catalog-model.entitypolicy>
- <https://backstage.io/docs/releases/v1.51.0/>
- <https://blog.cloudflare.com/post-mortem-on-cloudflare-control-plane-and-analytics-outage/>
- <https://data.finops.org/>
- <https://digital-strategy.ec.europa.eu/en/factpages/general-purpose-ai-obligations-under-ai-act>
- <https://digital-strategy.ec.europa.eu/en/faqs/guidelines-obligations-general-purpose-ai-providers>
- <https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act>
- <https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai>
- <https://digitaltrade.blog.gov.uk/2025/05/12/delivering-seamless-migrations-and-a-future-ready-platform/>
- <https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/policy.html>
- <https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/release-notes.html>
- <https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/control-planes-and-data-planes.html>
- <https://docs.cloudfoundry.org/buildpacks/index.html>
- <https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents>
- <https://docs.github.com/en/enterprise-cloud%40latest/copilot/how-tos/copilot-cli/use-copilot-cli/invoke-custom-agents>
- <https://engineering.atspotify.com/2021/03/happy-birthday-backstage-spotifys-biggest-open-source-project-grows-up-fast>
- <https://engineering.atspotify.com/2021/5/a-product-story-the-lessons-of-backstage-and-spotifys-autonomous-culture>
- <https://engineering.atspotify.com/2026/6/code-with-claude-coding-is-no-longer-the-constraint?from_theconsensus=1>
- <https://engineering.zalando.com/posts/2023/08/sunrise-zalandos-developer-platform-based-on-backstage.html>
- <https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=legissum%3A4762484>
- <https://focus.finops.org/focus-specification/v1-3/>
- <https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/>
- <https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/>
- <https://github.com/a2aproject/A2A/blob/main/docs/specification.md>
- <https://github.com/modelcontextprotocol/modelcontextprotocol>
- <https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/specification/2025-03-26/basic/authorization.mdx>
- <https://github.com/open-telemetry/semantic-conventions-genai>
- <https://groups.google.com/g/agile-system-administration/c/hp7WBg4uCJI>
- <https://kubernetes.io/blog/2021/08/04/kubernetes-1-22-release-announcement/>
- <https://kubernetes.io/docs/reference/using-api/deprecation-guide/>
- <https://kubernetes.io/docs/reference/using-api/deprecation-policy/>
- <https://langchain-ai.github.io/langgraph/concepts/langgraph_control_plane/>
- <https://langchain-ai.github.io/langgraph/concepts/langgraph_server/>
- <https://learn.microsoft.com/en-us/azure/ai-foundry/azure-openai-in-azure-ai-foundry>
- <https://legacy.devopsdays.org/events/2009-ghent/program>
- <https://modelcontextprotocol.io/docs/develop/clients/client-best-practices>
- <https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices>
- <https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization>
- <https://modelcontextprotocol.io/specification/draft/basic/authorization>
- <https://netflixtechblog.com/full-cycle-developers-at-netflix-a08c31f83249>
- <https://netflixtechblog.com/how-we-build-code-at-netflix-c5d9bd727f15>
- <https://netflixtechblog.com/open-sourcing-metaflow-a-human-centric-framework-for-data-science-fa72e04a5d9>
- <https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf>
- <https://opentelemetry.io/docs/specs/semconv/>
- <https://opentelemetry.io/docs/specs/semconv/non-normative/code-generation/>
- <https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/>
- <https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html>
- <https://sre.google/sre-book/eliminating-toil/>
- <https://sre.google/sre-book/embracing-risk/>
- <https://sre.google/sre-book/service-best-practices/>
- <https://sre.google/sre-book/service-level-objectives/>
- <https://sre.google/workbook/eliminating-toil/>
- <https://sre.google/workbook/simplicity/>
- <https://www.anthropic.com/engineering/building-effective-agents>
- <https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents>
- <https://www.anthropic.com/news/model-context-protocol>
- <https://www.gov.uk/guidance/defining-an-api-management-strategy>
- <https://www.gov.uk/service-manual/technology/deciding-how-to-host-your-service>
- <https://www.gov.uk/service-standard-reports/gov-dot-uk-platform-as-a-service-paas-live-assessment>
- <https://www.heroku.com/blog/twelve-factor-apps/>
- <https://www.justice.gov/criminal/criminal-oia/regarding-cloud-act-executive-agreements>
- <https://www.microsoft.com/investor/reports/ar25/index.html>
- <https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative>
- <https://www.nist.gov/itl/ai-risk-management-framework>
- <https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence>
- <https://www.nist.gov/publications/summary-analysis-responses-request-information-regarding-security-considerations-ai>
- <https://www.openpolicyagent.org/docs>
- <https://www.openpolicyagent.org/docs/integration>
- <https://www.openpolicyagent.org/docs/kubernetes>
- <https://www.openpolicyagent.org/docs/management-introduction>
- <https://www.openpolicyagent.org/docs/operations>
- <https://www.sec.gov/Archives/edgar/data/1018724/000101872426000004/0001018724-26-000004-index.htm>
- <https://www.sec.gov/Archives/edgar/data/1018724/000101872426000004/amzn-20251231.htm>
- <https://www.sec.gov/Archives/edgar/data/1650372/000165037225000060/0001650372-25-000060-index.htm>
- <https://www.sec.gov/Archives/edgar/data/1650372/000165037225000060/team2025annualreport.pdf>
- <https://www.sec.gov/Archives/edgar/data/1652044/000165204426000018/goog-20251231.htm>
- <https://www.uber.com/us/en/blog/michelangelo-machine-learning-platform/>
- <https://www.uber.com/us/en/blog/scaling-michelangelo/>

### News

- <https://aws.amazon.com/about-aws/whats-new/2026/03/policy-amazon-bedrock-agentcore-generally-available/>
- <https://aws.amazon.com/about-aws/whats-new/2026/07/aws-data-exports-amazon-bedrock-product-metadata/>
- <https://backstage.io/blog/2020/03/16/announcing-backstage/>
- <https://cloud.google.com/blog/products/devops-sre/announcing-the-2024-dora-report>
- <https://opentelemetry.io/blog/2026/genai-observability/>
- <https://www.cncf.io/announcements/2026/03/24/cncf-and-slashdata-report-finds-platform-engineering-tools-maturing-as-organizations-prepare-for-ai-driven-infrastructure/>
- <https://www.cncf.io/blog/2022/03/15/backstage-project-joins-the-cncf-incubator/>
- <https://www.cncf.io/blog/2023/11/20/announcing-the-platform-engineering-maturity-model/>
- <https://www.consilium.europa.eu/en/press/press-releases/2026/05/07/artificial-intelligence-council-and-parliament-agree-to-simplify-and-streamline-rules/pdf/>
- <https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation?hs_amp=true>
- <https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations>
- <https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents>

### Expert

- <https://arxiv.org/abs/2004.10724>
- <https://arxiv.org/abs/2209.09125>
- <https://arxiv.org/abs/2308.03952>
- <https://arxiv.org/abs/2406.19847>
- <https://arxiv.org/abs/2410.12944>
- <https://doi.org/10.1145/3610285>
- <https://dora.dev/capabilities/platform-engineering/>
- <https://dora.dev/research/2024/dora-report/>
- <https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf>
- <https://metr.org/Early_2025_AI_Experienced_OS_Devs_Study-paper.pdf>
- <https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/>
- <https://metr.org/blog/2026-05-19-frontier-risk-report/?dot=INC-029>
- <https://mit-genai.pubpub.org/pub/v5iixksv/release/2>
- <https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf>
- <https://pmc.ncbi.nlm.nih.gov/articles/PMC2655855/>
- <https://research.google.com/pubs/pub46484.html>
- <https://research.google/pubs/borg-omega-and-kubernetes/>
- <https://research.google/pubs/hidden-technical-debt-in-machine-learning-systems/>
- <https://research.google/pubs/what-improves-developer-productivity-at-google-code-quality/>
- <https://researchportal.vub.be/en/publications/an-empirical-study-of-policy-as-code-adoption-purpose-and-mainten/>
- <https://sequolia.com/hubfs/State%20of%20Platform%20Engineering%20Report%20Volume%203%20-%202024.pdf>
- <https://tag-app-delivery.cncf.io/es/whitepapers/platforms/>
- <https://teamtopologies.com/s/Organization-Dynamics-with-Team-Topologies-Mini-book-MB80.pdf>
- <https://www.atlassian.com/software/compass/resources/state-of-developer-2024>
- <https://www.bis.org/publ/work1208.htm>
- <https://www.bls.gov/news.release/ocwage.t01.htm>
- <https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full>
- <https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/>
- <https://www.microsoft.com/en-us/research/uploads/prod/2023/05/BestOfBothWorlds.pdf>
- <https://www.port.io/state-of-internal-developer-portals-2024>
- <https://www.puppet.com/blog/platform-engineering-teams>
- <https://www.puppet.com/sites/default/files/pdfs/report-puppet-sodor-2023-platform-engineering.pdf>
- <https://www.puppet.com/system/files/report-puppet-sodor-2023-platform-engineering.pdf>
- <https://www.sciencedirect.com/science/article/pii/S0164121218301614>
- <https://www.sciencedirect.com/science/article/pii/S0950584921001580>
- <https://www.sciencedirect.com/science/article/pii/S259011842200082X>
- <https://www.usenix.org/conference/srecon23americas/presentation/mcculley>
- <https://www.usenix.org/conference/srecon25emea/presentation/mckenzie>
- <https://www.usenix.org/system/files/opml19papers-baylor.pdf>

### Community

- <https://chadxz.dev/platform/>
- <https://discord.com/servers/backstage-687207715902193673>
- <https://github.com/backstage/backstage/issues/22162>
- <https://github.com/backstage/backstage/issues/22162#issuecomment-2895691140>
- <https://github.com/backstage/backstage/issues/22162#issuecomment-2895717047>
- <https://github.com/backstage/backstage/issues/26093>
- <https://github.com/open-telemetry/semantic-conventions-genai/issues/315>
- <https://github.com/orgs/langfuse/discussions/11391>
- <https://hamel.dev/blog/secret.html>
- <https://hamelhusain.substack.com/p/evals-skills-for-coding-agents>
- <https://news.ycombinator.com/item?id=22593568>
- <https://news.ycombinator.com/item?id=32067879>
- <https://news.ycombinator.com/item?id=36465220>
- <https://news.ycombinator.com/item?id=36468229>
- <https://news.ycombinator.com/item?id=36502512>
- <https://news.ycombinator.com/item?id=44194187>
- <https://ocgroups.dev/cncf/group/platform-engineering-technical-community-group>
- <https://platformengineering.org/about>
- <https://platformengineering.org/about/>
- <https://platformengineering.org/blog/backstage-implementations-for-more-than-100k-developers>
- <https://platformengineering.org/blog/beyond-devops-an-architects-field-notes-on-the-shift-to-platform-engineering>
- <https://platformengineering.org/blog/building-your-golden-path-lessons-from-the-trenches>
- <https://platformengineering.org/blog/golden-cage-syndrome-why-internal-developer-platforms-fail>
- <https://platformengineering.org/blog/platform-engineering-predictions-for-2025>
- <https://talks.ekern.me/applying-a-serverless-mindset-to-internal-developer-platforms.html>
- <https://www.linkedin.com/posts/davidtuite_backstage-has-a-skills-mismatch-problem-activity-7402737541109764097-8hDS>
- <https://www.linkedin.com/posts/hamelhusain_the-most-common-mistake-teams-make-when-building-activity-7438260194305986560-ePtK>
- <https://www.reddit.com/r/AI_Agents/comments/1tbwlqw/are_you_actually_running_ai_agents_in_production/>
- <https://www.reddit.com/r/AI_Agents/comments/1u01q5d/how_are_teams_handling_authiam_for_production/>
- <https://www.reddit.com/r/aiagents/comments/1rfscdx/whats_your_honest_tier_list_for_agent/>
- <https://www.reddit.com/r/devops/comments/1ae7l8r/actual_succesfull_experiences_with_internal/>
- <https://www.reddit.com/r/devops/comments/1kg3gj4/what_really_makes_an_internal_developer_platform/>
- <https://www.reddit.com/r/devops/comments/1kgfqys/comment/mqymey2/>
- <https://www.reddit.com/r/devops/comments/1kgfqys/comment/mqz46xg/>
- <https://www.reddit.com/r/devops/comments/1ldjjcu/whos_using_backstage_what_are_your_use_cases/>
- <https://www.reddit.com/r/kubernetes/comments/1tcc53b/whats_your_experience_with_internal_developer/>
- <https://www.reddit.com/r/kubernetes/comments/xpdttg/problems_after_upgrade_cluster_to_122/>
- <https://www.youtube.com/watch?v=n1IrNe5MmZg>
- <https://x.com/search?q=%22Backstage%22%20%22platform%20engineering%22&src=typed_query>

### Background

- <https://backstage.io/plugins/>
- <https://backstage.spotify.com/docs/portal>
- <https://backstage.spotify.com/faqs/>
- <https://cloud.google.com/solutions/platform-engineering>
- <https://cloud.google.com/vertex-ai/generative-ai/docs/reasoning-engine/overview?authuser=3>
- <https://developer.humanitec.com/platform-orchestrator/docs/platform-orchestrator/overview/>
- <https://devopsdays.org/about>
- <https://humanitec.com/blog/platform-as-a-product-the-evolution-of-devops-and-platform-engineering>
- <https://humanitec.com/platform-engineering>
- <https://info.backstage.spotify.com/get-portal>
- <https://metaflow.org/>
- <https://spinnaker.io/success-stories/>
- <https://www.cloudfoundry.org/wp-content/uploads/CFF-Charter-September-2023.pdf>
