# Mechanism: the lightest-sufficient-capability loop

## What I'm unpacking

The mechanism is an evidence-driven loop for choosing, enforcing, measuring, shrinking, replacing, or removing the lightest sufficient shared capability for building and operating AI agents.

The important word is *loop*. “Smallest” is not an architecture diagram or a permanently minimal feature list. A contract can be sufficient for one low-risk workflow and dangerously thin for another; a managed runtime can be justified today and redundant after an incumbent developer platform absorbs its useful functions. The mechanism therefore needs both an escalation path and an exit path.

## The walkthrough

1. **Start with a user job and a measured constraint, not a platform category.** The product/platform owner names a concrete journey—such as registering an internal agent, obtaining model access, or getting an audit trail—and records a baseline: successful-completion rate, elapsed and waiting time, repeated manual work, support load, audit effort, incident rate, and cost per successful outcome. This avoids equating activity with value. The SPACE framework says developer productivity cannot be reduced to one metric, while DORA recommends mapping critical user journeys and making one common workflow demonstrably better before expanding a platform ([Microsoft Research](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/), [DORA](https://dora.dev/capabilities/platform-engineering/)). **Input:** a repeated, consequential constraint and affected personas. **Output:** a falsifiable problem statement and baseline. **Failure:** measuring registrations, page views, or deployments while users still wait, work around the platform, or fail at the actual job.

2. **Set a capability floor from consequence and risk.** The application owner, security, privacy, and the accountable business owner classify the workflow by data sensitivity, tool permissions, reversibility, external impact, and need for human approval. NIST’s AI RMF explicitly connects governance, mapping, measurement, and management across the AI lifecycle; its core calls for post-deployment monitoring, override, decommissioning, incident response, and change management rather than a one-time build review ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)). Agent-specific evidence raises the floor when the agent can act: NIST’s agent-hijacking experiments found current agents vulnerable to malicious instructions embedded in data, and OWASP traces “excessive agency” to excessive functionality, permissions, or autonomy ([NIST, 2025-01-17](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations), [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)). **Input:** workflow and threat model. **Output:** minimum required controls. **Failure:** applying a single enterprise minimum to experiments, internal read-only assistants, and irreversible customer-facing agents alike.

3. **Choose the lowest rung that can satisfy that floor.** Test interventions in increasing order of ownership and coupling: documentation or convention; repository template; versioned metadata contract; schema validation and conformance tests; CI/CD policy; shared gateway or policy decision service; managed execution runtime. Anthropic’s production guidance is unusually direct: start with the simplest solution, add complexity only when it demonstrably improves outcomes, and recognize that agents trade latency and cost for task performance ([Anthropic, 2024-12-19](https://www.anthropic.com/engineering/building-effective-agents)). **Input:** capability floor plus existing company systems. **Output:** the smallest candidate intervention and explicit non-goals. **Failure:** selecting a full “AI platform” because the category exists, or selecting a contract because it looks cheap while exporting all integration and assurance work to every team.

4. **Define a contract before building a service.** A named schema owner writes a machine-readable, versioned contract with clear semantics, examples, lifecycle states, and an evolution policy. Backstage already demonstrates the core pattern: YAML lives with code, Git is the source of truth, owning teams update metadata through their normal workflow, and the catalog harvests and visualizes it ([Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)). Its envelope uses `apiVersion` plus `kind` so parsers know how to interpret the payload; components require a lifecycle and owner ([Backstage descriptor format](https://backstage.io/docs/features/software-catalog/descriptor-format/)). A2A’s Agent Card supplies a useful interoperability subset—identity, version, endpoint, capabilities, skills, supported interfaces, and authentication requirements—but it is a discovery contract, not a complete internal risk or ownership record ([A2A specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)). **Input:** agreed semantics. **Output:** a versioned contract, owner, validators, fixtures, and compatibility policy. **Failure:** arbitrary annotations that have no agreed meaning, no consumer, no owner, and no removal policy.

5. **Attach enforcement at the narrowest boundary where a violation is still preventable.** Syntactic mistakes can fail in the editor or CI; missing ownership can block catalogue ingestion; deployment rules can run at admission; tool authorization and high-impact approval must be mediated at execution. OPA separates policy decision-making from enforcement and can put the same policy in CI/CD, an API gateway, or a local sidecar; Kubernetes admission control can reject non-conforming create, update, and delete requests ([OPA documentation](https://www.openpolicyagent.org/docs), [OPA Kubernetes admission control](https://www.openpolicyagent.org/docs/kubernetes)). **Input:** contract instance plus contextual facts. **Output:** pass, warn, deny, or require approval, with an actionable reason. **Failure:** treating a green catalogue entry as proof of runtime authorization; Backstage explicitly says `spec.owner` is for responsibility/display and must not be used to assign runtime authorization ([Backstage descriptor format](https://backstage.io/docs/features/software-catalog/descriptor-format/)).

6. **Expose the capability through users’ existing work surfaces.** The contract/API is the stable boundary. Engineers may edit YAML, use a CLI, or instantiate a repository template; reviewers, finance, auditors, and occasional builders may need a portal view or form. A dedicated AI UI is therefore not a minimum by default. Google’s platform definition says an internal developer platform *may or may not* include a portal, while Backstage can present source-controlled metadata and aggregate existing tools around catalog entities ([Google Cloud](https://cloud.google.com/solutions/platform-engineering), [Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)). **Input:** contract/API and persona research. **Output:** one or more thin adapters over the same semantics. **Failure:** a CLI-only path that excludes occasional or assistive-technology users, or a portal-only path that removes scriptability, reviewability, and local feedback.

7. **Keep the control plane out of the execution path unless the risk requires otherwise.** The control plane should register agents, distribute configuration and policy, collect status, and expose evidence. The runtime/data plane should execute requests and tool calls. AWS’s fault-isolation guidance notes that control planes are complicated orchestration systems, whereas data planes provide the service’s primary function and should have fewer moving parts; separation improves performance and availability ([AWS control-plane/data-plane guidance](https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/control-planes-and-data-planes.html)). OPA shows one implementation: centrally distribute bundles and collect decisions/status, but evaluate policies beside the workload for low latency and availability ([OPA management architecture](https://www.openpolicyagent.org/docs/management-introduction)). **Input:** approved versioned configuration. **Output:** independently executable runtime state plus control-plane status. **Failure:** every agent turn depends synchronously on the portal, catalogue, or central management database.

8. **Instrument outcomes, not merely calls.** Application teams provide domain eval cases and success criteria; the shared layer can standardize trace correlation, cost attribution, policy decisions, and score transport. NIST calls for objective, repeatable or scalable test, evaluation, verification, and validation before deployment and regularly in operation ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)). OpenTelemetry’s semantic conventions provide shared names and meanings for spans, metrics, and events, including GenAI work, but telemetry semantics do not decide whether an answer or action was good ([OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/), [OpenTelemetry GenAI repository](https://github.com/open-telemetry/semantic-conventions-genai)). FOCUS similarly standardizes cost-and-usage dimensions and metrics, including allocation, but the organization must still choose a meaningful unit such as cost per resolved case rather than raw token spend ([FOCUS specification](https://focus.finops.org/focus-specification/v1-3/)). **Input:** runtime traces, eval fixtures, user outcomes, spend, incidents, and support data. **Output:** an outcome scorecard by workflow and risk class. **Failure:** a beautiful trace dashboard with no domain rubric or decision threshold.

9. **Run exceptions as evidence, not as silent bypasses.** A risk owner may grant a time-bounded exception with a reason, owner, expiry, compensating control, and review date. Repeated exceptions are either evidence that the control is wrong or evidence that a missing common capability has become consequential. OPA’s operational guidance makes the important choice explicit: policy systems need deliberate fail-open/fail-closed behavior; an unloaded policy can otherwise return `undefined` while appearing responsive ([OPA operations](https://www.openpolicyagent.org/docs/operations)). **Input:** failed control plus business context. **Output:** deny, repair, or expiring exception. **Failure:** permanent waivers, fail-open defaults nobody chose, or a central team manually approving routine work.

10. **Review the capability against grow, hold, shrink, replace, and remove thresholds.** The platform owner and user representatives compare the scorecard with the original baseline. Grow only when repeated failures show that the current rung cannot meet the capability floor. Shrink when a lower rung now achieves the same outcome; replace when an existing platform or vendor absorbs the capability at lower total cost; remove when the original constraint has disappeared and migration is safe. Google’s SRE guidance provides concrete precedents: error budgets turn reliability into a shared decision rule, and its filer decommission used access data, phased migration, specialized alternatives, self-service, and a deliberately lean team rather than an all-at-once replacement ([Google SRE error budgets](https://sre.google/sre-book/embracing-risk/), [Google SRE decommission case](https://sre.google/workbook/eliminating-toil/)). **Input:** outcome trend, ownership cost, dependency map, exceptions, and exit cost. **Output:** a funded next decision and dated review. **Failure:** adding features after every request while never asking which existing capability can now disappear.

### Decision rule in compact form

The loop can be expressed as:

`minimum shared capability = lowest-cost rung that meets the agreed user outcome and risk floor, including the work it exports to consuming teams`

That final clause prevents a contracts-only design from looking artificially cheap. Conversely, the calculation must include the central team’s staffing, on-call, migration, vendor, and common-mode-failure costs, or a broad runtime will look artificially cheap.

## Inputs and dependencies

| Dependency | Smallest concrete instance | Why it is still required | What can remain outside the platform |
|---|---|---|---|
| Problem and outcome owner | Named owner for one user journey and its success measure | Without an accountable outcome, adoption and request volume become substitutes for value. SPACE rejects a single productivity metric; Google research identifies infrastructure tools/support, code quality, team communication, priorities, and organizational process as distinct causal factors in perceived productivity ([Microsoft Research](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/), [Google Research](https://research.google/pubs/what-improves-developer-productivity-at-google-code-quality/)). | Enterprise-wide developer-productivity surveillance and individual ranking. |
| Contract owner and repository | One versioned schema package, examples, changelog, and CODEOWNERS-style owner | Backstage’s `apiVersion`/`kind` pair gives parsers the interpretation context, and its docs warn that custom kinds and stricter validation can break plugins or previously valid entities ([Backstage descriptor](https://backstage.io/docs/features/software-catalog/descriptor-format/), [Backstage model extension](https://backstage.io/docs/features/software-catalog/extending-the-model/)). | A new schema registry product if the existing Git/release mechanism suffices. |
| Metadata producer | A checked-in file or generated descriptor beside each agent | Source-controlled metadata creates review history and lets the owning team update it in its ordinary workflow ([Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)). | A dedicated AI catalogue database as the authoring source. |
| Metadata consumer | Existing Backstage catalogue processor/plugin | A contract has value only when something validates, displays, queries, or acts on it. Backstage accepts many software types and can attach existing tooling around an entity ([Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)). | A separate AI portal when the existing portal can present the job. |
| Identity and authorization | Existing workforce/workload identity, OAuth scopes, and downstream authorization | MCP’s HTTP authorization uses OAuth-based flows; OWASP recommends executing actions in the user’s context, minimizing scopes, and enforcing authorization in downstream systems ([MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), [OWASP excessive agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)). | A platform-owned identity provider or universal superuser credential. |
| Policy decision and enforcement point | CI validator for metadata; downstream authorization or a local policy engine for actions | Contracts describe intended state; enforcement prevents prohibited state. OPA can compile/embed policy or evaluate locally while a management plane distributes bundles and collects decisions ([OPA integration](https://www.openpolicyagent.org/docs/integration), [OPA management architecture](https://www.openpolicyagent.org/docs/management-introduction)). | A central synchronous policy service if local enforcement meets consistency and audit needs. |
| Evaluation set and rubric | A small, versioned set of real failures and critical tasks owned by each domain team | Generic platform metrics cannot define domain correctness. Anthropic reports that 20–50 tasks drawn from real failures can be a useful starting set and stresses mixing graders to match the system ([Anthropic, 2026-01-09](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)). | Platform-authored business truth or a compulsory heavyweight evaluation product. |
| Telemetry contract | Trace/run ID, agent/version, model/provider, tool, policy decision, latency, token/usage, outcome/eval reference, and error | Shared semantics make cross-tool correlation possible, but unstable conventions need version handling ([OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/), [OpenTelemetry versioning guidance](https://opentelemetry.io/docs/specs/semconv/non-normative/code-generation/)). | One mandated observability backend; exporters can feed existing systems. |
| Cost attribution | Cost centre/product/agent identifier carried from request to provider bill | FOCUS defines dimensions, metrics, tags, allocation, consumed quantity, and schema metadata needed for comparable cost-and-usage data ([FOCUS specification](https://focus.finops.org/focus-specification/v1-3/)). | A new billing engine if finance already has one. |
| Runtime owner, only when shared runtime exists | Named on-call rotation, SLO, runbook, capacity model, backup/recovery, and deprecation plan | Running stateful agents adds queues, persistence, retries, cancellation, streaming, secrets, and scale. LangGraph’s own Agent Server documentation illustrates the added database, task queue, API servers, queue workers, checkpoints, and scaling modes ([LangGraph Agent Server](https://langchain-ai.github.io/langgraph/concepts/langgraph_server/)). | Application-specific prompts, tools, business logic, and domain escalation policy. |
| Deprecation and migration mechanism | Consumer inventory, warning, parallel version, migration tool, last-supported date, and rollback | Kubernetes requires compatibility windows, warnings, versioned API removal, and transition paths precisely because shared contracts become dependencies ([Kubernetes deprecation policy](https://kubernetes.io/docs/reference/using-api/deprecation-policy/)). | Indefinite compatibility for experimental fields or unused features. |
| Talent and operating capacity | Product ownership, schema/API design, security, developer experience, and SRE skills proportional to the selected rung | A YAML contract still needs semantic ownership and support; a runtime needs production engineering. Google caps SRE toil because manual operational work otherwise expands and prevents engineering improvement ([Google SRE](https://sre.google/sre-book/eliminating-toil/)). | A permanently staffed “AI platform” organization before the workload justifies it. |

## Internals where most coverage waves hands

### 1. Metadata is an API, not documentation

A viable agent metadata contract needs four layers:

1. **Stable identity:** organization namespace, agent name, owning team, and lifecycle.
2. **Discovery:** description, version, skills/capabilities, supported input/output modes, and endpoints. A2A’s Agent Card already standardizes much of this layer and supports signed cards and caching ([A2A specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)).
3. **Governance:** risk class, data classifications used, permitted model/provider/regions, cost centre, accountable business owner, review date, and exception reference.
4. **Operations:** runtime location, source revision, tool identities/scopes, human escalation, eval-suite/version, telemetry destination, SLO, and runbook.

Backstage provides a useful envelope but does not supply those agent semantics. Its docs permit custom kinds and fields, but warn that custom API spaces may not be understood by plugins, arbitrary fields risk collisions, stricter rules can invalidate existing entities, and relations can dangle ([Backstage model extension](https://backstage.io/docs/features/software-catalog/extending-the-model/)). That means “put it in Backstage” is not the design. The design is:

- a separate, versioned agent schema owned by a named group;
- generated types and validators;
- golden valid/invalid fixtures;
- compatibility tests for every consumer;
- a Backstage processor/plugin as one adapter;
- staged deprecation with usage telemetry.

The contract should distinguish *declared*, *observed*, and *attested* facts. “Owner: payments” is declared. “Last deployed revision: abc123” is observed from CI/runtime. “Approved for restricted customer data until 2027-01-31” is an attestation by an authority. Collapsing these into one YAML file lets application owners self-assert facts that should come from an independent system.

Backstage itself exposes the staleness problem. Owning teams are responsible for updates; processing errors can appear long after registration; moved or deleted sources can produce orphaned entities; and observability of processing-loop errors is still an explicit concern ([Backstage entity lifecycle](https://backstage.io/docs/features/software-catalog/life-of-an-entity/)). Minimum governance therefore needs freshness timestamps, authoritative source per field, stale/unknown states, and a consumer that acts on them.

### 2. Contracts versus enforcement is a risk-gradient decision

A contract can do at least five different jobs, which are often confused:

| Contract role | Example | Enforcement level |
|---|---|---|
| Vocabulary | Define `owner`, `riskClass`, `tools`, `evalSuite` | Documentation only |
| Shape | Require type, enum, and reference syntax | Schema validation |
| Compatibility | Ensure producers and consumers agree across versions | Contract/conformance tests |
| Admission | Prevent a deployment lacking required metadata or approval | CI/CD or deployment gate |
| Runtime mediation | Prevent an agent/tool action outside identity, scope, budget, or approval | Downstream authorization / runtime policy |

The lightest adequate choice depends on when harm becomes irreversible. A missing description can be a warning. A missing cost centre may block production model access if attribution is mandatory. A tool declaration is not authorization: OWASP recommends complete mediation in downstream systems, least privilege, and human approval for high-impact actions ([OWASP excessive agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)). NIST’s agent-hijacking work is the empirical reason: an agent may treat untrusted data as instructions, so a prompt-level promise not to call a tool is not an enforcement boundary ([NIST, 2025-01-17](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations)).

Policy-as-code is not magic enforcement either. OPA deliberately decouples decision from enforcement: the application or admission controller must ask for and honor the decision ([OPA documentation](https://www.openpolicyagent.org/docs)). Its operations guide notes that no loaded policy can produce an `undefined` result and that deployments must deliberately choose fail-open or fail-closed ([OPA operations](https://www.openpolicyagent.org/docs/operations)). The minimum mechanism therefore includes policy distribution status, decision logs, policy-version correlation, readiness checks, and tests for unavailable/undefined behavior.

Empirical evidence supports the gap between declarations and reality. A study of 812 open-source Terraform projects found that using infrastructure-as-code did not itself prevent misconfiguration; explicit practices still varied, with encryption at rest among the least-adopted categories ([Verdet et al., 2023-08-07](https://arxiv.org/abs/2308.03952)). The lesson is not “enforce everything centrally.” It is to attach enforceable checks only to the constraints whose violation is consequential, and leave the rest as guidance or feedback.

### 3. The control plane/runtime boundary determines both scope and blast radius

A build-enabling platform can stop at:

- schema, SDK/template, model/provider access bootstrap;
- CI validation and evaluation hooks;
- registration/catalogue;
- deployment recipe;
- trace and cost semantic conventions.

It does **not** have to execute agent turns. An application team can deploy on the existing compute platform and use existing identity, queues, databases, secrets, and observability.

A shared agent runtime starts when the platform owns any of the following on behalf of multiple teams:

- the agent loop or workflow scheduler;
- durable run/thread state and checkpoints;
- task queues, retries, cancellation, and streaming;
- tool execution credentials and authorization mediation;
- model routing, quotas, caching, or fallback;
- runtime guardrails and human-approval orchestration;
- production SLO/on-call for those paths.

The difference is operational, not semantic. LangGraph’s deployment docs make the cost visible: a managed Agent Server includes persistence, a task queue, API servers, queue workers, checkpoints, and separate scaling behavior ([LangGraph Agent Server](https://langchain-ai.github.io/langgraph/concepts/langgraph_server/)). Its control-plane documentation adds deployment state, revisions, integrations, listeners, metrics, secrets/configuration, and databases ([LangSmith control plane](https://langchain-ai.github.io/langgraph/concepts/langgraph_control_plane/)). Those can be valuable, but they are not “just a place to run agents.”

The safest default is asynchronous control: distribute versioned policy/configuration, let the runtime continue on last-known-good state, and collect status and decisions. OPA explicitly supports this local-evaluation pattern ([OPA management architecture](https://www.openpolicyagent.org/docs/management-introduction)). Cloudflare’s incident from 2023-11-02 through 2023-11-04 demonstrates why: its network data plane continued forwarding traffic while much of the customer-facing control plane and analytics were unavailable; hidden dependencies still broke newer services that had not completed the high-availability path ([Cloudflare, 2023-11-04](https://blog.cloudflare.com/post-mortem-on-cloudflare-control-plane-and-analytics-outage/)). A minimal control plane should therefore be able to fail without stopping already-approved low-risk execution; high-risk actions may deliberately fail closed.

### 4. UI, API, CLI, template, and portal are adapters with different users

The smallest platform needs an interface, but not necessarily its own graphical interface. A YAML contract is a human and machine interface; an API is a compositional interface; a CLI provides automation and fast expert feedback; a repository template shapes a new system at creation; a portal supports discovery, status, comparison, and occasional tasks.

The selection rule is job/persona based:

| Job | Lightest likely surface | Add another surface when |
|---|---|---|
| Register/change an agent in a code-owning team | Reviewed YAML plus editor/CI validation | Authors repeatedly fail on syntax/semantics or cannot see derived state |
| Bootstrap a common agent repository | Template or CLI backed by the same schema | Choices need explanation, preview, or accessible non-terminal interaction |
| Discover owner, risk, status, docs, and costs | Existing Backstage page/plugin | Existing portal cannot query or display the required semantics |
| Approve a high-impact action | Existing workflow/approval UI near the downstream system | No existing surface can show context and record the decision |
| Automate governance queries | API/export | Consumers are screen-scraping a portal or duplicating data stores |
| Audit a fleet | Portal/report built from authoritative and observed facts | Raw API access creates repeated manual reconciliation |

There is no evidence for “GUI always” or “CLI always.” Google explicitly says an internal developer platform may or may not include a portal ([Google Cloud](https://cloud.google.com/solutions/platform-engineering)). A Microsoft mixed-methods study found internal-tool usability—including limited, rough UI—among reported productivity barriers, while compliance and education/support also appeared, showing that a screen alone does not solve the journey ([Microsoft Research](https://www.microsoft.com/en-us/research/uploads/prod/2023/05/BestOfBothWorlds.pdf)). Backstage’s model supports the thinner arrangement: source-controlled YAML remains authoritative while the portal renders and connects it to operational tools ([Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)).

The mechanism should therefore build the contract/API once and add adapters only when observed completion, accessibility, discoverability, or error-recovery problems justify them. A dedicated AI portal is a feature, not the definition of the platform.

### 5. “Build agents” and “run agents” have different minimums

For **build-only scope**, the minimum can plausibly be contracts plus enablement:

- approved provider/model-access pattern;
- agent and tool metadata;
- template/SDK examples;
- identity integration guidance;
- eval harness contract;
- telemetry/cost fields;
- deployment hooks to the existing application platform.

For **run-agent scope**, the minimum is higher because the platform inherits operational fate:

- durable execution semantics or explicit stateless limits;
- per-run identity and tool authorization;
- timeouts, retry ceilings, idempotency, cancellation, and rate limits;
- trace/provenance and cost correlation;
- online quality/risk signals;
- human handoff and kill/disable mechanism;
- isolation, capacity, SLO, incident response, recovery, and decommissioning.

The trigger to cross that boundary should not be “several teams use agents.” It should be evidence that several teams are repeatedly and consequentially rebuilding the *same runtime responsibility*, and that centralization reduces total work or risk after on-call and common-mode costs. Anthropic distinguishes deterministic workflows from model-directed agents and recommends simpler workflows where predictability suffices ([Anthropic, 2024-12-19](https://www.anthropic.com/engineering/building-effective-agents)). NIST and OWASP provide the counterweight: as soon as models independently select tools and act on external systems, identity, authorization, monitoring, and approval can become a genuine shared floor ([NIST, 2026-02-05](https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents), [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)).

What the shared runtime should deliberately **not** own by default is equally important: application prompts, domain tool selection, business success rubrics, product-specific memory, downstream data entitlements, and the business decision about acceptable harm. Centralizing these creates a universal agent framework whose platform team lacks the domain context to operate safely.

### 6. Evaluation, observability, and cost form one decision system

These are often sold as three products. Mechanically, they answer different parts of one question:

- **Observability:** what path ran, with which versions, tools, policies, latencies, errors, and resources?
- **Evaluation:** was the result acceptable for this user job and risk class?
- **Cost:** what did that acceptable result consume, and who owns the spend?

The minimum useful record links all three with a stable run ID and immutable version references. A practical scorecard should include:

| Dimension | Example measures | Decision it supports |
|---|---|---|
| User outcome | task success, correction/rework, elapsed time, waiting time, abandonment | Did the capability remove the original constraint? |
| Independence | self-service completion, platform-team touch rate, time to actionable error | Did shared machinery remove or create a dependency? |
| Delivery | lead time, deployment frequency, change failure, recovery time | Did the path improve flow without destabilizing delivery? |
| Agent quality/safety | eval pass by risk class, tool-call error, policy deny, override, human escalation, harmful-action near miss | Is the control floor adequate? |
| Reliability | user-centered SLI/SLO, error-budget burn, queue saturation, dependency failures | Does a managed runtime justify its operational cost? |
| Economics | provider/platform cost, support/toil, audit effort, cost per successful outcome | Is centralization cheaper after hidden work is counted? |
| Governance | metadata completeness/freshness, orphan rate, exception count/age, audit evidence retrieval time | Is the contract alive and enforceable? |
| Reversibility | consumers by version, portable/exportable state, migration estimate, last fallback test | Can the capability actually be shrunk or removed? |

SPACE supports the multidimensional treatment ([Microsoft Research](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/)). DORA’s platform findings are a warning against selecting only the flattering dimensions: the report released on 2024-10-22 associated internal platforms with higher individual/team productivity and organizational performance, but also found lower throughput and change stability; mandatory exclusive use for the whole lifecycle was associated with a throughput decrease ([DORA report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf), [Google Cloud, 2024-10-22](https://cloud.google.com/blog/products/devops-sre/announcing-the-2024-dora-report)). Those are observational estimates, not proof that platforms caused either result, but they show why adoption or perceived productivity cannot be the sole grow signal.

Telemetry should be open and portable. OpenTelemetry defines shared semantics, and FOCUS defines normalized cost-and-usage data ([OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/), [FOCUS](https://focus.finops.org/focus-specification/v1-3/)). Domain eval cases should remain application-owned. The smallest platform can provide transport, storage hooks, sampling, redaction, and comparison machinery without pretending to know whether a refund, fraud decision, code change, or customer answer was correct.

### 7. Shrinking and removal require engineered reversibility

Removal is a feature with its own telemetry and interface:

1. inventory every producer, consumer, enforcement point, and runtime dependency;
2. stop or discourage new adoption;
3. observe actual usage rather than declared ownership;
4. provide one or more alternatives for each real job;
5. warn and migrate in phases;
6. run old and new paths long enough to compare outcomes;
7. delete only after the rollback and exception windows close.

Google’s filer retirement is the strongest concrete precedent found. The team analyzed access across 2.5 billion files, 300 terabytes, 60,000 users, 400 volumes, 124 appliances, and 60 sites; it used several specialized replacements because no single new platform covered every job. The program averaged three team members, reduced home directories from 65,000 to around 50, and built tooling only as later phases required it ([Google SRE decommission case](https://sre.google/workbook/eliminating-toil/)). This is “smallest” as an operating method: replace one broad shared system with multiple better-fitting capabilities and keep migration tooling proportional to the next cohort.

Kubernetes supplies the contract mechanics: version API groups independently, preserve round-tripping, do not replace stable interfaces with less stable ones, emit deprecation warnings, and provide minimum support windows ([Kubernetes deprecation policy](https://kubernetes.io/docs/reference/using-api/deprecation-policy/)). Its migration guide shows that “compatible in principle” still requires field-by-field work; the `v1.22` removal of beta Ingress, webhook, and CRD APIs changed required fields and defaults ([Kubernetes migration guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/)).

The economic removal case is GOV.UK PaaS. On 2022-07-12, GDS announced decommissioning despite 99.95% uptime, one major incident in seven years, 172 services, and more than 122 tenant deployments per day. The reasons were strategic: slower growth than other platforms, better hyperscaler offerings, stronger departmental cloud capability, and a choice between major architecture investment and sunset ([GDS, 2022-07-12](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). A 2021-02-10 service assessment had already found the platform could not fully recoup cost through recharge and depended on central funding, and told tenants to maintain exit plans ([GOV.UK service assessment, 2021-06-11](https://www.gov.uk/service-standard-reports/gov-dot-uk-platform-as-a-service-paas-live-assessment)). Reliability and affection did not settle whether the platform remained the lightest sufficient intervention.

## Failure modes

| Failure mode | Thin or broad side | What actually breaks | Historical example and lesson |
|---|---|---|---|
| **Decorative contract** | Too thin | Metadata exists but no validator, consumer, freshness check, or runtime mediation; declared intent diverges from reality. | In the 812-project Terraform study published on 2023-08-07, using declarative scripts did not itself ensure security-practice adoption; encryption at rest was among the most neglected categories. A contract needs checks at the consequential boundary ([Verdet et al.](https://arxiv.org/abs/2308.03952)). |
| **Stale or ambiguous ownership** | Too thin | The catalogue shows a team that no longer owns the agent, a dangling relation, or an unreadable descriptor; incident and audit routing fail. | Backstage documents late processing errors, orphaning after moved/deleted sources, dangling relations, and the need for operators to monitor processing. Treat “unknown/stale” as a state, not valid ownership ([Backstage entity lifecycle](https://backstage.io/docs/features/software-catalog/life-of-an-entity/), [Backstage model extension](https://backstage.io/docs/features/software-catalog/extending-the-model/)). |
| **Schema evolution strands consumers** | Both | A producer upgrades, but portal plugins, deployment generators, or runtime clients interpret old fields or defaults. | Kubernetes `v1.22`, released on 2021-08-04, stopped serving several beta APIs; Ingress field names and required `pathType` changed, webhook defaults changed, and CRDs required structural schemas. Versioning, rehearsal, warnings, and migration tooling are platform work ([Kubernetes, 2021-08-04](https://kubernetes.io/blog/2021/08/04/kubernetes-1-22-release-announcement/), [migration guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/)). |
| **Policy engine present but not enforcing** | Too thin | The application fails to ask, ignores the decision, starts without policy, or silently fails open. | OPA warns that an instance with no policy can return `undefined` and that fail-open/fail-closed is a deployment choice. Readiness and failure-path tests matter as much as Rego ([OPA operations](https://www.openpolicyagent.org/docs/operations)). |
| **Build-only controls applied to an acting agent** | Too thin | A reviewed prompt or metadata declaration cannot prevent a compromised agent from using excessive downstream permissions. | NIST’s agent-hijacking experiments published on 2025-01-17 exercised malicious instructions in email, files, websites, and simulated tools; the finding supports downstream authorization and runtime mediation for consequential tools ([NIST](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations)). |
| **Portal or mandate becomes a handoff machine** | Too broad | Every change traverses extra systems/teams, even when the path is not fit for the job; workarounds and waiting grow. | The DORA report released on 2024-10-22 associated platform use with an estimated 8% lower throughput and 14% lower change stability, alongside productivity benefits; exclusive mandated use across the lifecycle was associated with a 6% throughput decrease. The report offers hypotheses rather than causal proof, but it is a clear reason to measure end-to-end flow ([DORA report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). |
| **Central runtime creates a common-mode dependency** | Too broad | A control/configuration error or dependency outage affects every consuming agent, and the status system may fail with the platform it reports on. | On 2017-02-28, an incorrect S3 maintenance-command input removed more servers than intended, affecting S3, EC2 launches, EBS snapshots, Lambda, and even the dashboard used to report status. AWS responded by prioritizing smaller cells and moving dashboard administration across regions ([AWS, 2017-02-28](https://aws.amazon.com/message/41926/)). |
| **Control plane enters the data path** | Too broad | Running workloads cannot continue when catalogue, portal, policy distribution, or analytics is unavailable. | During Cloudflare’s outage beginning 2023-11-02, network services continued while customers could not make many changes and analytics/logging failed; newer products with hidden dependencies on a failed facility suffered more. Last-known-good local execution reduced impact, while incomplete separation exposed exceptions ([Cloudflare, 2023-11-04](https://blog.cloudflare.com/post-mortem-on-cloudflare-control-plane-and-analytics-outage/)). |
| **UI is omitted or added for the wrong reason** | Both | CLI-only excludes some users and increases errors; portal-only removes composability and duplicates a mature existing interface. | Microsoft’s study reported developer-tool usability, including rough internal UIs, as a barrier; Google’s platform definition explicitly says a portal is optional. The historical lesson is to research the job and persona, not settle an ideological GUI/CLI contest ([Microsoft Research](https://www.microsoft.com/en-us/research/uploads/prod/2023/05/BestOfBothWorlds.pdf), [Google Cloud](https://cloud.google.com/solutions/platform-engineering)). |
| **Metrics optimize the platform instead of the outcome** | Both | Registration, token volume, deployment count, or trace volume rises while quality, delivery, cost, or user success worsens. | DORA’s 2024 mixed results and SPACE’s warning against single-dimensional productivity measures show how a platform can look successful under one denominator and harmful under another ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf), [SPACE](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/)). |
| **The platform survives its comparative advantage** | Too broad | A once-useful capability now duplicates cheaper or better incumbents, but sunk cost and downstream dependency block removal. | GDS decided on 2022-07-12 to decommission GOV.UK PaaS after cloud providers and departmental teams reduced its unique value and growth slowed, despite strong reliability and meaningful use. “Works well” is not the same as “still the lightest sufficient shared capability” ([GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). |
| **Deprecation becomes an unplanned migration programme** | Broad-side aftermath | Consumers were never inventoried, state is non-portable, and no compatibility window or fallback exists. | Google’s filer retirement required a multiyear, phased programme, multiple specialized replacements, usage telemetry, a self-service portal, and long-tail tooling. Reversibility must be designed before retirement is urgent ([Google SRE](https://sre.google/workbook/eliminating-toil/)). |

## Constraints and ceilings

1. **The consequence floor.** A contracts-only approach has a hard ceiling when an agent can cause irreversible, externally visible, financial, safety, privacy, or security effects. Metadata can inform authorization but cannot replace downstream least privilege, complete mediation, rate limits, and approval. OWASP and NIST both support that floor ([OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html), [NIST](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations)).

2. **The probabilistic-quality ceiling.** Trace completeness cannot prove task correctness. Agents operate across multiple turns and tools, and real failures must become versioned eval cases; NIST requires repeated lifecycle testing, and Anthropic notes that agent flexibility makes evaluation harder than single-turn model testing ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), [Anthropic, 2026-01-09](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)).

3. **The semantics ceiling.** A generic schema can standardize envelopes, references, identity, cost, and telemetry, but not every domain’s definition of a safe action or successful outcome. Backstage warns that extensions affect plugins and validation assumptions; its owner field is explicitly not runtime authorization ([Backstage model extension](https://backstage.io/docs/features/software-catalog/extending-the-model/), [Backstage descriptor](https://backstage.io/docs/features/software-catalog/descriptor-format/)).

4. **The human-attention ceiling.** Every field, approval, dashboard, and exception consumes attention. DORA found that added machinery and handoffs can reduce throughput, while its guidance emphasizes independence and actionable feedback ([DORA report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf), [DORA capability guidance](https://dora.dev/capabilities/platform-engineering/)). A platform that requires routine central assistance has crossed from self-service into ticket-ops.

5. **The operational-economics ceiling.** A managed runtime creates fixed cost, capacity planning, incident response, upgrades, data retention, security review, and on-call. Google’s SRE organization caps toil at 50% because operational work otherwise expands to consume engineering capacity ([Google SRE](https://sre.google/sre-book/eliminating-toil/)). The platform must scale support sublinearly or hand responsibilities back.

6. **The attribution ceiling.** Provider invoices, shared gateways, retries, caches, and multi-agent calls can obscure unit cost. FOCUS can normalize the billing schema, but accurate cost per successful business outcome still requires request-level business context and an allocation rule ([FOCUS](https://focus.finops.org/focus-specification/v1-3/)).

7. **The availability ceiling.** Centralization gains consistency but increases correlated failure. AWS’s 2017-02-28 S3 incident and Cloudflare’s 2023-11-02 control-plane incident show why cells, local evaluation, independent status paths, and last-known-good state matter ([AWS](https://aws.amazon.com/message/41926/), [Cloudflare](https://blog.cloudflare.com/post-mortem-on-cloudflare-control-plane-and-analytics-outage/)).

8. **The interface ceiling.** No single surface serves repository-native engineers, occasional builders, auditors, finance, and approvers equally. A contract/API plus thin adapters is smaller and more accessible than forcing every persona into one “single pane of glass.” The evidence supports user research and multiple dimensions, not a universal GUI or CLI ([Microsoft Research](https://www.microsoft.com/en-us/research/uploads/prod/2023/05/BestOfBothWorlds.pdf), [Google Cloud](https://cloud.google.com/solutions/platform-engineering)).

9. **The regulatory and organizational floor varies by context.** NIST’s GenAI profile explicitly says risk-management profiles should align with the user’s goals, legal requirements, risk tolerance, and resources ([NIST, 2024-07-26](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)). There is therefore no evidence for one global “smallest” platform independent of jurisdiction, sector, workflow, and authority model.

10. **The reversibility ceiling.** The more state, secrets, workflow semantics, identity, and operational history a shared runtime owns, the less credible “replace or remove” becomes. Kubernetes’ formal deprecation windows and Google’s multiyear filer migration show that exit cost grows with dependency depth ([Kubernetes deprecation policy](https://kubernetes.io/docs/reference/using-api/deprecation-policy/), [Google SRE decommission case](https://sre.google/workbook/eliminating-toil/)).

## Side effects

- **A contracts-only platform creates an organization-wide language.** This improves discovery and makes ownership, lifecycle, evaluation, cost, and tool scopes queryable. It also creates semantic governance work: somebody must adjudicate field meaning, compatibility, authoritative sources, and exceptions. Backstage’s extensibility warnings show that this is product/API work even when the artifact is “just YAML” ([Backstage model extension](https://backstage.io/docs/features/software-catalog/extending-the-model/)).

- **Thin central scope exports work.** Application teams retain framework choice and autonomy, but they may each implement provider integration, retries, redaction, policy hooks, and audit evidence. If that repeated work is omitted from the cost model, minimality is accounting theatre. Google Research’s finding that infrastructure tools and support affect developer productivity is a reason to measure the exported burden directly ([Google Research](https://research.google/pubs/what-improves-developer-productivity-at-google-code-quality/)).

- **Broad central scope imports risk and creates bargaining power.** A runtime team can standardize security and reduce duplication, but it becomes a release gate, on-call owner, vendor selector, and common failure domain. DORA’s mixed platform results and AWS’s S3 incident show both organizational and technical versions of this effect ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf), [AWS](https://aws.amazon.com/message/41926/)).

- **Standard telemetry can create data exhaust and surveillance pressure.** Correlated traces and cost records help debugging and audit, but high-cardinality content, prompts, tool inputs, and user identity create privacy, retention, and access-control obligations. OpenTelemetry defines semantics, not a mandate to collect sensitive payloads ([OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/)). The minimum should default to metadata, sampling, and redaction appropriate to the risk.

- **A portal changes what becomes legible.** Owners, deprecated agents, missing evals, and spend become visible to builders and governance teams. That is useful; it can also turn incomplete or self-declared metadata into a false aura of control. Backstage’s processing-error and orphan behavior is a reminder to display freshness and provenance, not only a green scorecard ([Backstage entity lifecycle](https://backstage.io/docs/features/software-catalog/life-of-an-entity/)).

- **Enforcement moves conflict earlier.** CI/admission failures can prevent risky deployment cheaply, but poor error messages and rigid global controls create waiting and bypass. DORA identifies clear feedback and developer independence as central platform capabilities ([DORA](https://dora.dev/capabilities/platform-engineering/)). A deny must say what failed, why, who owns the rule, and the fastest safe repair or exception path.

- **Measurement changes behavior.** Cost per token rewards cheap verbosity differently from cost per successful resolution; deployment count rewards batch fragmentation differently from user value. SPACE’s multidimensional framework and Google SRE’s user-centered SLO guidance are safeguards against one-number optimization ([SPACE](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/), [Google SRE](https://sre.google/sre-book/service-best-practices/)).

- **Removal creates temporary complexity.** Parallel versions, migration tools, adapters, and communications can make the system larger before it becomes smaller. Google’s filer case accepted that temporary cost and built only what each migration phase required ([Google SRE](https://sre.google/workbook/eliminating-toil/)).

## Plain-language analogy

Think of the smallest AI platform as a building code, not a government construction company. For a garden shed, a shared vocabulary and a checked plan may be enough. For a hospital, the same code needs qualified inspectors, tested fire doors, operating records, and authority to stop unsafe use. The code is versioned; owners can see which buildings depend on which edition; exceptions expire; and obsolete requirements can be retired. A portal is merely one counter where people can view or submit the paperwork—it is not the code, the inspector, or the building. The analogy breaks because software can validate some rules continuously and distribute policy automatically, while an agent’s behavior remains probabilistic and can change with models, tools, prompts, and runtime context; therefore evidence from actual runs and evaluations must feed the loop.

## Source receipts

### Primary and standards

- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) — framework first published 2023-01-26; page retrieved 2026-07-29.
- [NIST Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — published 2024-07-26.
- [NIST: Strengthening AI agent hijacking evaluations](https://www.nist.gov/news-events/news/2025/01/technical-blog-strengthening-ai-agent-hijacking-evaluations) — published 2025-01-17.
- [NIST: Software and AI agent identity and authorization concept paper](https://www.nist.gov/news-events/news/2026/02/new-concept-paper-identity-and-authority-software-agents) — published 2026-02-05.
- [OWASP LLM06:2025 Excessive Agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html) — version dated 2025-01-27; retrieved 2026-07-29.
- [Model Context Protocol authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization) — specification dated 2025-06-18.
- [A2A protocol specification and Agent Card](https://github.com/a2aproject/A2A/blob/main/docs/specification.md) — repository state retrieved 2026-07-29.
- [Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/) — retrieved 2026-07-29.
- [Backstage catalog descriptor format](https://backstage.io/docs/features/software-catalog/descriptor-format/) — retrieved 2026-07-29.
- [Backstage: extending the catalogue model](https://backstage.io/docs/features/software-catalog/extending-the-model/) — retrieved 2026-07-29.
- [Backstage: the life of an entity](https://backstage.io/docs/features/software-catalog/life-of-an-entity/) — retrieved 2026-07-29.
- [Kubernetes deprecation policy](https://kubernetes.io/docs/reference/using-api/deprecation-policy/) — retrieved 2026-07-29.
- [Kubernetes deprecated API migration guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/) — retrieved 2026-07-29.
- [Kubernetes `v1.22` release announcement](https://kubernetes.io/blog/2021/08/04/kubernetes-1-22-release-announcement/) — published 2021-08-04.
- [Open Policy Agent documentation](https://www.openpolicyagent.org/docs) — retrieved 2026-07-29.
- [Open Policy Agent integration choices](https://www.openpolicyagent.org/docs/integration) — retrieved 2026-07-29.
- [Open Policy Agent management APIs and architecture](https://www.openpolicyagent.org/docs/management-introduction) — retrieved 2026-07-29.
- [Open Policy Agent Kubernetes admission control](https://www.openpolicyagent.org/docs/kubernetes) — retrieved 2026-07-29.
- [Open Policy Agent operations and failure modes](https://www.openpolicyagent.org/docs/operations) — retrieved 2026-07-29.
- [OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/) — retrieved 2026-07-29.
- [OpenTelemetry GenAI semantic-conventions repository](https://github.com/open-telemetry/semantic-conventions-genai) — repository state retrieved 2026-07-29.
- [OpenTelemetry semantic-convention versioning guidance](https://opentelemetry.io/docs/specs/semconv/non-normative/code-generation/) — retrieved 2026-07-29.
- [FOCUS specification `v1.3`](https://focus.finops.org/focus-specification/v1-3/) — retrieved 2026-07-29.

### Academic and empirical studies

- [Forsgren et al., “The SPACE of Developer Productivity”](https://www.microsoft.com/en-us/research/publication/the-space-of-developer-productivity-theres-more-to-it-than-you-think/) — published 2021-02-01.
- [Cheng et al., “What Improves Developer Productivity at Google? Code Quality.”](https://research.google/pubs/what-improves-developer-productivity-at-google-code-quality/) — published 2022-11-14 in the ESEC/FSE 2022 industry track.
- [Storey et al., “DevEx: What Actually Drives Productivity?”](https://doi.org/10.1145/3610285) — published 2023-10-20.
- [Verdet et al., “Exploring Security Practices in Infrastructure as Code: An Empirical Study”](https://arxiv.org/abs/2308.03952) — published 2023-08-07.
- [Microsoft, “The Best of Both Worlds: Unlocking the Potential of Hybrid Work for Software Engineers”](https://www.microsoft.com/en-us/research/uploads/prod/2023/05/BestOfBothWorlds.pdf) — published 2023-05-01.
- [DORA Accelerate State of DevOps Report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf) — released 2024-10-22.

### Primary engineering and operational writeups

- [Anthropic, “Building effective agents”](https://www.anthropic.com/engineering/building-effective-agents) — published 2024-12-19.
- [Anthropic, “Demystifying evals for AI agents”](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) — published 2026-01-09.
- [Google Cloud, highlights from the tenth DORA report](https://cloud.google.com/blog/products/devops-sre/announcing-the-2024-dora-report) — published 2024-10-22.
- [DORA platform-engineering capability guidance](https://dora.dev/capabilities/platform-engineering/) — retrieved 2026-07-29.
- [Google Cloud platform-engineering definition](https://cloud.google.com/solutions/platform-engineering) — retrieved 2026-07-29.
- [Google SRE: eliminating toil](https://sre.google/sre-book/eliminating-toil/) — retrieved 2026-07-29.
- [Google SRE: error budgets and embracing risk](https://sre.google/sre-book/embracing-risk/) — retrieved 2026-07-29.
- [Google SRE: production-service best practices](https://sre.google/sre-book/service-best-practices/) — retrieved 2026-07-29.
- [Google SRE Workbook: decommissioning filer-backed home directories](https://sre.google/workbook/eliminating-toil/) — retrieved 2026-07-29.
- [AWS: control planes and data planes](https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/control-planes-and-data-planes.html) — retrieved 2026-07-29.
- [AWS S3 service disruption summary](https://aws.amazon.com/message/41926/) — incident dated 2017-02-28.
- [Cloudflare control-plane and analytics outage postmortem](https://blog.cloudflare.com/post-mortem-on-cloudflare-control-plane-and-analytics-outage/) — published 2023-11-04.
- [GDS: why GOV.UK PaaS was decommissioned](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/) — published 2022-07-12.
- [GOV.UK PaaS live service assessment](https://www.gov.uk/service-standard-reports/gov-dot-uk-platform-as-a-service-paas-live-assessment) — assessed 2021-02-10; published 2021-06-11.
- [LangGraph Agent Server runtime architecture](https://langchain-ai.github.io/langgraph/concepts/langgraph_server/) — retrieved 2026-07-29.
- [LangSmith control plane](https://langchain-ai.github.io/langgraph/concepts/langgraph_control_plane/) — retrieved 2026-07-29.

### Practitioner commentary

- [Hacker News discussion of the GOV.UK PaaS decommission](https://news.ycombinator.com/item?id=32067879) — thread dated 2022-07-12. Used as a dissent/check on GDS’s official account, not as authority for the decommission rationale.
- [r/devops: “Actual successful experiences with Internal Developer Platforms”](https://www.reddit.com/r/devops/comments/1ae7l8r/actual_succesfull_experiences_with_internal/) — thread dated 2024-01-30. Practitioners describe success after reducing scope to a few jobs; treated as anecdotal.
- [r/kubernetes: problems after upgrading to `v1.22`](https://www.reddit.com/r/kubernetes/comments/xpdttg/problems_after_upgrade_cluster_to_122/) — thread dated 2022-09-27. Concrete report of manifests failing against removed `extensions/v1beta1` Ingress; corroborated by Kubernetes’s official migration guide.

### Snowball pass

The first pass surfaced Backstage/Spotify, Kubernetes, CNCF, OPA, OpenTelemetry, NIST/CAISI, OWASP, DORA/Google, SPACE/Microsoft Research, FOCUS/FinOps Foundation, MCP, A2A, AWS, Cloudflare, LangGraph/LangSmith, Anthropic, GOV.UK PaaS, and GDS.

- **Already searched:** Backstage/Spotify; Kubernetes; OPA; OpenTelemetry; NIST/CAISI; OWASP; DORA/Google; SPACE/Microsoft Research; FOCUS; MCP; AWS; Cloudflare; Anthropic; GOV.UK PaaS/GDS.
- **Search-now and completed:** A2A Agent Card (needed to test whether an agent metadata contract already exists); LangGraph/LangSmith (needed to expose what “run agents” adds operationally); Kubernetes `v1.22` migration (needed for a concrete versioning failure); Google’s filer decommission (needed for a concrete subtraction mechanism).
- **Background-only:** CNCF and the Linux Foundation as project hosts; AgentDojo and ETH Zurich as dependencies of NIST’s already-sourced evaluation; individual commercial portal and gateway vendors whose marketing was not needed to establish the mechanism.

A second proper-noun pass added no unresolved load-bearing entity. Vendor claims were excluded where standards, peer-reviewed work, official architecture documentation, or first-party postmortems supplied stronger evidence.
