# Findings: What Does “Smallest” Mean?

**Last updated:** 2026-07-29
**Full synthesis:** [research.md](research.md)
**Community evidence:** [07-community.md](07-community.md)
**Validation:** [validation.md](validation.md)

## Short answer

The smallest useful AI platform is not the product with the fewest features. It is:

> the lowest-total-work shared capability that lets a defined group complete one valuable workflow, meets that workflow’s risk floor, and remains cheaper to change or remove than the work it displaces.

For the chapter’s likely starting point, that means:

1. a versioned agent metadata contract beside the code;
2. a named owner and consumer for every required field;
3. schema and conformance checks;
4. reuse of existing identity, delivery, Backstage, observability, and FinOps systems;
5. enforcement only where a consequential violation can still be prevented; and
6. no dedicated agent runtime or AI portal until a measured user job requires one.

The first implementation may therefore be a contract plus validation, not a deployed AI platform. That is a hypothesis to test, not a universal conclusion.

## A precise definition of “smallest”

“Smallest” has four simultaneous tests:

| Test | Question |
|---|---|
| **Outcome** | Does the capability remove the measured constraint and let the intended user complete the job? |
| **Risk** | Does it meet the minimum control level required by the data, authority, reversibility, and impact involved? |
| **Total work** | Does it reduce central **plus exported local** integration, support, audit, incident, migration, and exception work? |
| **Reversibility** | Can its contracts, state, evidence, and consumers be migrated, reduced, or retired at an acceptable cost? |

In compact form:

`smallest = lowest-cost rung that meets the user outcome and risk floor, including exported work and exit cost`

This definition rejects two misleading minima. A YAML file is not small if every team must build adapters and chase audit evidence around it. A broad runtime is not small merely because a vendor operates it if it creates a common failure domain, a permanent on-call dependency, and a difficult exit.

## What the studies show—and do not show

The empirical base is much weaker than the maturity models and market language imply.

- A peer-reviewed multivocal review published on **2026-05-04** included 88 sources but found only 2 top-tier publications primarily about platform engineering. It found no longitudinal or quasi-experimental multi-organization evidence and no peer-reviewed empirical evidence for IDP scorecards. This is the strongest evidence-quality finding in the dossier ([Frontiers in Computer Science](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)).
- DORA’s report released on **2024-10-22** associated internal-platform use with approximately 8% higher individual productivity, 10% higher team performance, and 6% higher organizational performance. The same analysis associated it with approximately 8% lower throughput and 14% lower change stability; exclusive mandatory use was associated with a further throughput penalty. These are observational associations, not causal estimates ([DORA report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)).
- The SPACE framework and DevEx research support multidimensional measurement rather than one productivity number. Activity, satisfaction, flow, quality, and organizational context can move in different directions ([Microsoft Research](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/), [ACM DevEx paper](https://doi.org/10.1145/3610285)).
- Empirical work supports the gap between a declared contract and an implemented reality. A study of 812 open-source Terraform projects found that infrastructure-as-code did not itself ensure security-practice adoption; a separate architecture study found recurring divergence between intended architecture, implementation, and maintained documentation ([Terraform study](https://arxiv.org/abs/2308.03952), [architecture/source-code study](https://www.sciencedirect.com/science/article/pii/S0950584921001580)).
- ML research does justify a narrow AI-specific floor. Production ML adds changing data, behavioural evaluation, linked model/data/configuration provenance, monitoring, and feedback-loop risks that ordinary deployment health checks do not resolve ([Google, “Hidden Technical Debt in Machine Learning Systems”](https://research.google/pubs/hidden-technical-debt-in-machine-learning-systems/), [production-ML interview study](https://arxiv.org/abs/2209.09125)).
- Agent tool use raises the floor again. NIST has demonstrated agent hijacking through malicious instructions embedded in data, while OWASP connects excessive agency to excessive functionality, permissions, and autonomy. A metadata declaration cannot replace downstream authorization for consequential actions ([NIST](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations), [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)).

What the literature does **not** establish is a universal threshold based on company size, team count, agent count, or risk label. It also does not compare, under matched conditions, the four relevant operating models below. Broad platform success stories from Uber, Google, Spotify, and hyperscalers are useful primary case studies, but they are not independent counterfactuals. Vendor-sponsored surveys report perceived gains and useful failure patterns, but they cannot prove the vendor category causes those gains.

## Four candidate operating models

| Model | What is shared | Best fit | Hidden cost | Exit profile |
|---|---|---|---|---|
| **No dedicated AI platform** | Existing source control, identity, delivery, security, observability, and FinOps absorb AI work | Few production workflows; little repeated consequential friction; strong incumbent systems | Teams repeat provider integration, evaluation, evidence, and incident work; spend and data flows may be discovered late | Easiest centrally, but local implementations may be inconsistent and hard to inventory |
| **Contracts-only** | Versioned metadata, templates, policy vocabulary, schema validation, conformance tests, and adapters into existing systems | Discovery, ownership, cost allocation, and governance are the repeated constraints; existing runtimes are adequate | Schema stewardship, freshness, consumer compatibility, migrations, and local runtime controls remain real work | Comparatively strong if consumers and versions are inventoried |
| **Narrow managed capability** | One operational choke point, such as authenticated model access, tool authorization, evaluation transport, or cost attribution | Several teams repeatedly need the same consequential control and local implementations are measurably wasteful or unsafe | It becomes critical infrastructure and inherits on-call, latency, provider churn, policy mistakes, and bypass | Good only if application logic, eval data, and telemetry remain exportable |
| **Broad integrated platform** | Portal, catalogue, gateway, runtime, policy, evaluation, observability, deployment, and governance workflows | High scale and repeated cross-lifecycle glue make economies of scope larger than central product and migration cost | Common-mode failure, roadmap queues, mandatory abstractions, unused features, plugin/upgrade debt, and vendor lock-in | Weakest; state, policy, identity, traces, and workflows span one product boundary |

History supports all four in different conditions. Metaflow shows a thin library over replaceable infrastructure; Michelangelo and TFX show broad integration paying off at large scale; Backstage shows a contract and portal growing from a catalogue; GOV.UK PaaS shows a reliable platform can still lose its comparative advantage ([Netflix Metaflow](https://netflixtechblog.com/open-sourcing-metaflow-a-human-centric-framework-for-data-science-fa72e04a5d9), [Uber Michelangelo](https://www.uber.com/us/en/blog/michelangelo-machine-learning-platform/), [Google TFX](https://research.google.com/pubs/pub46484.html), [GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)).

The recommended default is **extend incumbents with contracts first**, then move to a narrow managed capability only when local evidence shows that enforcement or repeated runtime work cannot remain distributed.

## Proposed minimum agent metadata contract

Backstage supplies a useful `apiVersion`/`kind` envelope and source-controlled ownership workflow, while A2A’s Agent Card supplies discovery fields. Neither is a complete internal risk and operating contract by itself ([Backstage descriptor format](https://backstage.io/docs/features/software-catalog/descriptor-format/), [A2A specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)).

The smallest credible internal `Agent` record should contain:

| Area | Minimum fields | Why it exists |
|---|---|---|
| Identity | `apiVersion`, `kind`, `name`, `namespace`, `version` | Stable interpretation, lookup, and migration |
| Accountability | `owner`, `businessOwner`, `lifecycle`, `purpose` | Change, incident, risk, and retirement routing |
| Risk | `riskClass`, `dataClassifications`, `impact`, `humanApprovalRequired` | Selects the capability and enforcement floor |
| Execution | `runtimeType`, `deploymentRef`, `sourceRevision`, `executionOwner` | Distinguishes a catalogue entry from what actually runs |
| Models | `provider`, `allowedModels`, `regions` | Procurement, data-flow, substitution, and incident evidence |
| Tools | tool references, required scopes, authorization mode | Discovery must not be confused with permission |
| Evaluation | `evalSuite`, `evalVersion`, `evalOwner`, last result/reference | Behavioural regression and domain evidence |
| Operations | `runbook`, `incidentContact`, `disableOrKillRef` | Response and safe shutdown |
| Telemetry and cost | trace/run identifier convention, telemetry destination, `costCenter`, product/workflow | Correlation and cost per successful outcome |
| Lifecycle evidence | `reviewedAt`, `expiresAt`, exception reference, schema version | Freshness, temporary waivers, and removal |

Every field should also identify its evidence type:

- **declared:** asserted by the application team;
- **observed:** generated by CI, runtime, provider, or telemetry;
- **attested:** approved by an independent authority.

This prevents a self-declared `owner`, `approved`, or `lastDeployedRevision` from acquiring the false authority of an observed or attested fact. The contract needs a named schema owner, generated validators, valid/invalid fixtures, compatibility tests for each consumer, and a deprecation policy. Backstage itself documents processing errors, orphaning, and dangling relations, which means stale and unknown must be visible states rather than silently treated as valid ([Backstage entity lifecycle](https://backstage.io/docs/features/software-catalog/life-of-an-entity/)).

## Contracts versus enforcement

A contract can perform five different jobs:

| Job | Example | Lightest mechanism |
|---|---|---|
| Vocabulary | Define `owner`, `riskClass`, `tools`, `evalSuite` | Documentation and examples |
| Shape | Require types, enums, and references | Editor and schema validation |
| Compatibility | Keep producers and consumers aligned across versions | Contract and conformance tests |
| Admission | Prevent an ineligible production deployment | CI/CD or deployment gate |
| Runtime mediation | Prevent an unauthorized tool action or budget breach | Downstream authorization or local runtime policy |

The decision rule is:

> enforce at the latest boundary where the harm is still preventable, and no earlier than needed.

A missing description can warn. A malformed owner reference can fail CI. A missing production risk approval can block deployment. A high-impact write must be authorized by the downstream system in the user or workload context; a green catalogue entry is not authorization. Backstage explicitly warns that its owner field is for responsibility and display, not runtime access control ([Backstage](https://backstage.io/docs/features/software-catalog/descriptor-format/)).

Policy-as-code does not remove this distinction. OPA separates policy decisions from enforcement, so the application or admission point must ask for and honor the result. Failure behavior—fail open, fail closed, or last-known-good—must be an explicit design choice ([OPA documentation](https://www.openpolicyagent.org/docs), [OPA operations](https://www.openpolicyagent.org/docs/operations)).

## Does the smallest platform need a UI?

It needs an interface, not necessarily its own graphical interface.

| Persona and job | Lightest likely surface | Add a dedicated UI when |
|---|---|---|
| Engineer registers or changes an agent | Reviewed YAML plus editor/CI feedback | Syntax, derived state, or remediation repeatedly blocks completion |
| Engineer bootstraps a common repository | Template or CLI backed by the same schema | Choices need explanation, preview, or accessible non-terminal interaction |
| Non-engineer or occasional builder configures a bounded workflow | Existing form, low-code surface, chat, or generated pull request | The existing surface cannot explain options, validate input, or recover from errors |
| Domain expert evaluates outputs | Purpose-built review/annotation UI | Almost immediately if trace navigation and comparison are part of the job |
| Risk owner approves a consequential action | Existing approval UI near the downstream system | Context, evidence, and decision recording are otherwise fragmented |
| Finance, audit, or incident response inspects the fleet | Existing portal/report over authoritative data | Raw APIs create repeated reconciliation and cannot show freshness/provenance |
| Another system consumes metadata | API or export | Never force automation to scrape a portal |

Google’s platform definition explicitly says an internal developer platform may or may not include a portal, and Backstage already separates source-controlled metadata from its rendered portal ([Google Cloud](https://cloud.google.com/solutions/platform-engineering), [Backstage](https://backstage.io/docs/features/software-catalog/)). General UI studies suggest novices can complete some equivalent tasks faster and in fewer steps with a GUI, but no study reviewed compares UI, CLI, chat, and templates for this mixed internal-AI population ([GUI/TUI study](https://pmc.ncbi.nlm.nih.gov/articles/PMC2655855/)).

The evidence therefore supports a contract/API with thin persona-specific adapters, not “GUI always” or “CLI always.”

## Build versus run

Helping teams **build** agents and **running** agents are different commitments.

| Build-enabling minimum | Shared-runtime minimum |
|---|---|
| Approved model/provider access pattern | Durable or explicitly stateless execution semantics |
| Agent/tool metadata and repository template | Per-run identity and tool authorization |
| Evaluation hooks and version references | Queueing, retries, timeouts, idempotency, cancellation, and streaming |
| Telemetry and cost conventions | Runtime policy, quotas, isolation, and capacity |
| Deployment hooks into the existing application platform | Checkpoints/state, recovery, human approval, and kill/disable |
| Catalogue and ownership discovery | SLO, on-call, incident response, evidence retention, and decommissioning |

Cross that boundary only when several teams are repeatedly and consequentially rebuilding the **same runtime responsibility**, and central ownership lowers total work or risk after support, on-call, migration, and common-mode costs are included.

The platform should not run agents merely because several teams build them. Anthropic recommends simpler workflows where predictability suffices, while NIST and OWASP show why tool-using agents with write authority require stronger runtime identity and mediation ([Anthropic](https://www.anthropic.com/engineering/building-effective-agents), [NIST agent identity concept paper](https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents), [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)).

## Deliberate non-goals

The initial platform should deliberately **not**:

- define one universal agent framework, prompt pattern, memory system, or orchestration model;
- own product prompts, domain tool selection, business rubrics, or the decision about acceptable harm;
- replace existing workforce/workload identity, deployment, observability, incident, billing, or data-governance systems;
- provide a new portal when Backstage, Git, a template, an existing approval surface, or an API serves the job;
- become the source of truth for facts available from CI, runtime, provider, identity, or finance systems;
- store prompt and tool payloads by default when metadata, sampling, or redaction is sufficient;
- authorize tool use merely because the tool appears in metadata;
- require all experiments and low-risk workflows to use the same production controls;
- promise indefinite compatibility for unused or experimental fields;
- mandate adoption to compensate for an unhelpful path; and
- run agents before repeated runtime constraints justify an operational service.

These are boundaries, not omissions to “complete later.” Each can be reconsidered only against a measured constraint.

## What engineers and communities report

The community evidence is a purposive sample across Hacker News, Reddit, GitHub, LinkedIn, practitioner writing, specialist media, and conference talks. It reveals mechanisms and failure modes, not prevalence. Many accounts are pseudonymous; platform media is commercially entangled; Spotify and Backstage maintainers have employer-product stakes; LinkedIn was usable but vendor- and training-heavy. Targeted searches of X/Twitter, public Backstage Discord and CNCF Slack surfaces, and YouTube comments did not produce a publicly auditable, exact-dated implementation corpus because login or invite gates and relative-only dates limited retrieval. That is an access limitation, not evidence of absence or sentiment. These limitations are disclosed in the full [community evidence](07-community.md).

The recurring experiences are:

- **A README, module, or repository template can be enough.** One r/devops practitioner described Terraform modules with two required variables; another said GitHub templates covered about 90% of their need. The counterexample in the same thread was an enterprise with thousands of weekly Backstage users and a dedicated team of 20, where templates could not replace legacy approvals and external-system registration ([r/devops](https://www.reddit.com/r/devops/comments/1kg3gj4/what_really_makes_an_internal_developer_platform/)).
- **Backstage is a product commitment, not a catalogue install.** A practitioner’s first action after inheriting it was deprecation because the organization could not justify a dedicated React/platform team. Spotify’s own guidance says a central team must operate the deployment, support users, drive adoption, encode templates, coordinate standards, and eventually provide on-call ([r/devops](https://www.reddit.com/r/devops/comments/1ldjjcu/whos_using_backstage_what_are_your_use_cases/), [Backstage adoption guidance](https://backstage.io/docs/overview/adopting/)).
- **Metadata goes stale when ownership is social rather than operational.** A Kubernetes practitioner described deprecated services remaining visible after the original team rotated out. Backstage maintainers explain that reorganizations are non-atomic and dangling relations sometimes must remain soft errors rather than block ingestion ([r/kubernetes](https://www.reddit.com/r/kubernetes/comments/1tcc53b/whats_your_experience_with_internal_developer/), [Backstage issue #26093](https://github.com/backstage/backstage/issues/26093)).
- **A UI becomes load-bearing for non-engineer evaluation.** A Langfuse user reported more than 20 non-technical reviewers and said the interface sometimes led them in circles. The smallest builder surface can be a CLI while the smallest reviewer surface is still a purpose-built UI ([Langfuse discussion](https://github.com/orgs/langfuse/discussions/11391)).
- **Voluntary adoption is diagnostic.** Named practitioners at Sotheby’s and Red Hat recommend opt-in adoption or letting adoption follow value. Mandatory risk controls may still be necessary at the action boundary, but a mandatory portal can hide a poor path ([Chad McElligott](https://chadxz.dev/platform/), [Pablo Castelo](https://platformengineering.org/blog/beyond-devops-an-architects-field-notes-on-the-shift-to-platform-engineering)).
- **Wrappers impose a debugging tax.** Engineers object when platform abstractions preserve all the underlying Docker, Kubernetes, or cloud knowledge while adding custom concepts and an extra dependency. Escape hatches and time-to-root-cause are part of the capability, not advanced options ([Hacker News](https://news.ycombinator.com/item?id=36465220)).
- **Decommissioning changes future trust.** A long-time GOV.UK PaaS user argued that the migration experience discouraged adoption of later GDS tools even though the PaaS had removed substantial operations work. This is one anecdote, but it identifies a cost absent from feature and uptime comparisons ([Hacker News](https://news.ycombinator.com/item?id=32067879)).
- **AI-specific pain is not solved by trace collection alone.** Practitioners report custom scripts, spreadsheet reviews, weak handoff tracing, stale source identity, and prompt-level tests failing once workflows become longer. OpenTelemetry contributors likewise describe trace capture across chains, tools, and high-cardinality inputs as unresolved work; domain experts still decide whether the result was useful ([Ask HN](https://news.ycombinator.com/item?id=44194187), [OpenTelemetry issue](https://github.com/open-telemetry/semantic-conventions-genai/issues/315)).

The community does not agree that portals are bad or that templates are sufficient. It agrees more strongly on the accounting rule: include the people and systems required to keep the abstraction useful.

## The central counterargument

“What is the smallest AI platform?” may still be a solution-first question.

Most proposed capabilities—identity, deployment, networking, secrets, ownership, observability, cost attribution, incident response, and audit—already belong to developer, security, data, and FinOps platforms. A CNCF/SlashData survey found that extending existing cloud-native platforms with specialist AI tooling was the most common reported approach, while MLOps architecture research treats MLOps as an extension of DevOps rather than a separate universe ([CNCF/SlashData](https://www.cncf.io/announcements/2026/03/24/cncf-and-slashdata-report-finds-platform-engineering-tools-maturing-as-organizations-prepare-for-ai-driven-infrastructure/), [MLOps mapping study](https://arxiv.org/abs/2406.19847)).

But subtraction can become accounting theatre. Google’s ML-debt paper illustrates mature ML systems as a small amount of model code surrounded by large amounts of glue; a tiny central contract can export that glue to every application team. Broad integration has demonstrated economies at Uber and Google scale, even though those are first-party cases rather than neutral comparisons ([Google ML debt](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf), [Uber Michelangelo](https://www.uber.com/us/en/blog/scaling-michelangelo/), [Google TFX](https://www.usenix.org/system/files/opml19papers-baylor.pdf)).

The stronger question is therefore:

> Which arrangement produces the least total work per successful, governed outcome?

## Capability floor by risk class

The floor follows consequence, not the word “agent.” This is a proposed operating classification, not a legal or research-validated universal taxonomy.

| Class | Example | Minimum shared capability | Enforcement floor |
|---|---|---|---|
| **0 — experiment** | Local prototype; synthetic/public data; no external action | Owner, purpose, lifecycle, approved access guidance, deletion date | Repository validation or none; no production claim |
| **1 — internal read-only** | Search, summarization, drafting with internal data | Class 0 plus data class, provider/region, evaluation reference, trace/cost correlation, incident contact | Identity, data entitlement, retention/redaction, monitored access |
| **2 — reversible action** | Creates drafts, tickets, code changes, or bounded transactions subject to review | Class 1 plus tool/scopes, per-run identity, approval rule, rollback/cancellation, runbook, kill switch | Complete downstream authorization, rate limits, audit log, human approval where impact requires it |
| **3 — high-impact or hard-to-reverse** | Customer, financial, employment, safety, regulated, or privileged infrastructure action | Class 2 plus accountable business/risk owner, formal evaluation threshold, SLO/on-call, evidence retention, incident and decommission plan | Strong isolation, fail-closed critical controls, ongoing evaluation/monitoring, independent approval or attestation |

A higher risk class does not automatically require one shared runtime. It requires the control to exist and be demonstrably effective somewhere. A narrow authorization service plus existing compute may satisfy the floor better than a universal agent runtime.

NIST’s AI RMF makes lifecycle governance, monitoring, override, incident response, change management, and decommissioning contextual to the organization and use case; the EU AI framework likewise assigns obligations by actor and risk rather than by whether an internal platform exists ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), [European Commission](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)).

## A falsifiable decision loop

| Step | Required evidence | Decision |
|---|---|---|
| 1. Name the job | Valuable workflow, owner, affected personas | Stop if the workflow itself is not worth supporting |
| 2. Baseline the constraint | Completion, waiting, support, audit, incident, and cost data | Observe if no repeated consequential constraint appears |
| 3. Set the risk floor | Data, authority, reversibility, external impact, jurisdiction | Identify controls that cannot be optional |
| 4. Test the lowest rung | Documentation → template → contract → conformance → admission → gateway → runtime | Keep the first rung that meets outcome and risk |
| 5. Assign semantics and consumers | Owner, source, freshness, version, validator, decision made from each field | Delete fields with no consumer; reject ownerless contracts |
| 6. Place enforcement | Last point where harm remains preventable | Warn, deny, require approval, or mediate at runtime |
| 7. Fit interfaces to jobs | Task success by persona, frequency, and accessibility need | Add only the thin adapter that removes the observed block |
| 8. Measure displaced work | Central and local labor, support, exceptions, incidents, audit, migration | Reject apparent savings that merely move work |
| 9. Review exceptions | Owner, reason, expiry, compensating control | Change a bad rule or add a proven missing capability |
| 10. Decide on a date | Grow, hold, shrink, replace, or remove against the baseline | No capability continues by default |

The hypothesis is falsified if a lighter intervention fails the risk floor or increases total work; it is also falsified if a broader intervention cannot improve the named outcome enough to repay its central and exit costs.

## When to shrink, replace, or remove

**Shrink** when:

- a lower rung now achieves the same user outcome and risk result;
- most features or plugins have no active decision consumer;
- support and exceptions do not decline with adoption;
- the platform has absorbed domain-specific logic its owner cannot evaluate; or
- the execution path can move back to existing compute while contracts and evidence remain.

**Replace** when:

- an incumbent or supplier now provides the proven capability at lower total cost;
- the replacement preserves or improves exports, identity, evidence, and failure isolation;
- migration and dual-running costs fit inside the remaining avoided ownership cost; and
- a representative workload can move without rebuilding product logic and evaluation data.

**Remove** when:

- the original constraint has disappeared;
- no risk obligation or critical consumer still depends on the capability;
- actual usage, not declared ownership, confirms the long tail is gone;
- each real user job has a tested alternative or intentionally no replacement; and
- retention, migration, rollback, communication, and trust costs are funded.

Google’s Omega experience shows why replacement must be compared with the improved future incumbent, not the incumbent’s current defects. GOV.UK PaaS shows that reliability and affection do not prove continuing comparative advantage; its 18-month sunset also shows that deletion is a migration program, not the inverse of installation ([Google SRE](https://sre.google/workbook/simplicity/), [GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)).

## Measures

No single measure proves success. The minimum scorecard should cover:

| Dimension | Measures |
|---|---|
| User outcome | Correct task completion, rework/correction, elapsed time, waiting time, abandonment |
| Independence | Unassisted completion, platform-team touch rate, time to an actionable error |
| Delivery | Lead time, deployment frequency, change failure, recovery time |
| Agent quality and safety | Evaluation pass by risk class, harmful-action near miss, policy deny, override, human escalation |
| Reliability | User-centred SLI/SLO, error-budget burn, queue saturation, dependency failure |
| Economics | Central labor, local integration labor, support/toil, audit effort, provider cost, cost per successful outcome |
| Governance | Metadata completeness, freshness, orphan rate, exception count/age, audit-evidence retrieval time |
| Adoption quality | Voluntary adoption, retention, abandonment, bypass, satisfaction by persona |
| Reversibility | Consumers by version, portable state/evidence, migration estimate, fallback-test age |

Page views, agent counts, token volume, fields completed, and deployments are diagnostics. They are not outcome measures.

## Missing evidence

The most important missing result is an independent, preregistered, longitudinal comparison of teams facing equivalent AI constraints under:

1. no dedicated platform;
2. a contract plus automated conformance;
3. one narrow managed capability; and
4. a broad integrated platform.

It should include all central and local labor, task success by persona, delivery, evaluation, security events, audit effort, exceptions, cost per successful outcome, migration, and exit. No such head-to-head evidence was found.

For this chapter’s organization, the missing internal receipts are more immediate:

- a baseline for one repeated workflow;
- a map of existing identity, Backstage, observability, FinOps, and deployment capabilities;
- time spent on duplicate adapters, approvals, support, evidence, and incidents;
- current agent ownership and data/tool-risk distribution;
- interface task studies with engineers and non-engineers;
- contracts, data-processing terms, commitments, and export/termination rights;
- exception, bypass, incident, and decommission records; and
- a funded owner for schema evolution and retirement.

Without those receipts, “contracts-only,” “gateway,” and “integrated platform” remain competing hypotheses.

## One 90-day experiment

**Window:** 2026-07-30 through **2026-10-27**.

**Question:** Can a versioned contract plus conformance checks remove the repeated work of registering one production-bound internal agent without a new AI portal or runtime?

The cohort size, two-week baseline option, and every percentage gate below are dossier-proposed local decision thresholds for this experiment. They are not research-validated cutoffs, industry benchmarks, or transferable defaults.

**Cohort (local design):** at least three materially different teams using the same workflow. Include at least one occasional or non-engineer builder if that population is genuinely in scope.

**Baseline:** use recent comparable registrations or the first two weeks to record completion correctness, elapsed and waiting time, synchronous help, support effort, missing ownership/data/tool/evaluation evidence, and audit reconstruction time.

**Intervention:**

1. Check in the proposed `Agent` descriptor beside the code.
2. Validate its shape and references in the editor and CI.
3. Populate observed fields from CI/runtime rather than asking teams to self-assert them.
4. Ingest it into the existing Backstage catalogue.
5. Show freshness, provenance, exceptions, and lifecycle state.
6. Keep execution on the existing application platform.
7. Enforce only the applicable risk-class controls at CI, deployment, identity, or downstream tool boundaries.
8. Offer a template or generated pull request before building a dedicated UI.

**The dossier proposes a local pass by 2026-10-27 only if all are true:**

- at least 80% of representative users complete the workflow correctly without synchronous platform-team help;
- required metadata remains at least 90% conformant and current in two consecutive monthly samples;
- median elapsed or waiting time improves by at least 30%;
- combined central and consuming-team support effort does not rise more than 10%;
- no material audit, incident, or high-impact review finds a control gap that requires a common runtime; and
- one descriptor can be exported and removed from Backstage without affecting the running agent.

**Decision at the end:**

- **Pass:** hold at contract plus conformance; do not add scope.
- **Interface-only failure:** add the smallest generator, form, or review surface that addresses the observed persona.
- **Repeated enforcement failure:** test one narrow gateway or policy capability, without absorbing application runtime.
- **Several coupled runtime failures:** consider a shared runtime only after showing that incumbents cannot supply the missing responsibilities.
- **No measurable improvement:** remove the contract experiment and keep the incumbent path.

This experiment is intentionally about one workflow. A 90-day platform build would test delivery capacity; this tests whether the proposed minimum actually removes work.

## Bottom line

The smallest AI platform is not a miniature version of a broad one. It is the lightest owned arrangement that produces a successful, governed outcome after central work, local work, risk, and exit are all counted.

For Chapter 3, the most defensible first answer is:

> start with an agent contract and conformance checks inside the existing platform estate; add a persona-specific interface or one narrow managed control only when measured failure proves it necessary; do not run agents until repeated runtime responsibility—not enthusiasm for agents—justifies the operational burden.
