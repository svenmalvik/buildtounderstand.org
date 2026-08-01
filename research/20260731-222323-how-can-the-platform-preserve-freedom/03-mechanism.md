# Mechanism: preserving freedom without making controls optional

## What I'm unpacking

The mechanism under examination is a **thin, versioned agent contract in each repository**, plus a small set of enforcement and evidence services. “Thin” should mean that the contract describes invariants—owner, purpose, data class, required capabilities, permitted model classes, tool authorities, evaluation suite, budgets, and telemetry obligations—without dictating the team's prompt library, orchestration graph, memory design, framework, or hosting provider. JSON Schema can identify the dialect used to interpret a schema through `$schema`; that is useful for syntax, but a separate contract version and explicit migration policy are still needed for the platform's own meanings [JSON Schema](https://json-schema.org/understanding-json-schema/reference/schema).

**Freedom** is practical, not nominal. A team is free only if it can use a different model, vendor, framework, runtime, or no shared runtime while retaining its repository, evaluation corpus, identity relationships, tool contracts, telemetry, and incident evidence—and can do so within an agreed time and cost. A second provider that accepts the same JSON is not sufficient. Anthropic says its OpenAI SDK compatibility layer is mainly for testing, not a production-ready long-term solution; it ignores `strict` function-calling semantics and most unsupported fields. Google likewise says its OpenAI schema does not map one-to-one to Gemini and that unsupported parameters can be silently ignored. These are first-party demonstrations that **nominal API compatibility is not semantic portability** [Anthropic](https://platform.claude.com/docs/en/cli-sdks-libraries/libraries/openai-sdk) [Google](https://ai.google.dev/gemini-api/docs/partner-integration) [Google compatibility reference](https://ai.google.dev/gemini-api/docs/openai).

There are at least five distinct portability layers:

1. **Wire portability:** another endpoint accepts the same protocol and JSON shape.
2. **Capability portability:** required modalities, context size, structured output, streaming, citations, and tool calling exist and mean the same thing.
3. **Behavioral portability:** on the workflow's representative cases, outputs, refusals, tool choices, and failure behavior remain inside an accepted envelope.
4. **Operational portability:** latency, throughput, quotas, regions, retention, support, and price remain acceptable.
5. **Exit portability:** configuration, prompts, evaluation cases, tool schemas, run records, and policy evidence can be exported and replayed without the old platform.

Only the first is approximately tested by “change the base URL.” Even vLLM's OpenAI-compatible server documents unsupported and ignored parameters, while a reported LiteLLM translation regression dropped tool-call arguments despite valid requests and responses on either side [vLLM](https://docs.vllm.ai/en/v0.22.0/serving/online_serving/openai_compatible_server/) [LiteLLM issue 25321](https://github.com/BerriAI/litellm/issues/25321).

**Mandatory** should mean a control tied to a concrete risk owner and harm, not merely a preferred platform convention. NIST's AI RMF calls for documented testing and post-deployment monitoring, incident response, appeal/override, recovery, change management, and decommissioning; it does not imply that all of those functions must live in one central AI runtime [NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/). The governing placement rule is therefore: put each preventive control at the **last policy enforcement point that sees enough context and can still stop the harmful effect**. NIST's zero-trust architecture similarly separates policy decision logic from the policy enforcement point guarding the resource [NIST SP 800-207](https://csrc.nist.gov/pubs/sp/800/207/final).

## The walkthrough

1. **A product team declares the repository contract.**
   - **Actor:** workflow owner and reviewers.
   - **Input:** a versioned manifest referencing immutable tool schemas, data classification, intended users, risk tier, required model capabilities, approved evaluation dataset/version, maximum action authority, budget, owner, and exit contact.
   - **Output:** reviewable code plus a machine-readable contract whose portable core is separated from namespaced provider/framework extensions.
   - **Failure:** the schema validates while the declaration is false, incomplete, or stale. JSON Schema proves structure, not the truth of `data_classification: public` or the meaning of `safe`. The contract therefore needs named accountable owners and freshness/expiry rules, not only schema validation [JSON Schema specification](https://github.com/json-schema-org/json-schema-spec/blob/main/specs/jsonschema-core.md).

2. **CI checks what can be known before deployment.**
   - **Actor:** repository ruleset and an independently controlled validator.
   - **Input:** source, contract, dependencies, tool definitions, policies, representative test cases, and pinned candidate provider/model identifiers.
   - **Output:** pass/fail results plus signed provenance containing the commit, contract version, policy bundle version, evaluator version, dataset hash, model/provider tested, and results.
   - **Failure:** a team can bypass or forge the check, or production differs from what CI tested. GitHub rulesets support required checks, an expected GitHub App as the source, and explicit bypass permissions; that makes bypasses governable but does not make them impossible [GitHub rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets). SLSA provenance is evidence about how an artifact was built, and its own specification notes that organizations still decide where verification occurs and what happens on failure [SLSA v1.2](https://slsa.dev/spec/v1.2/).

3. **Deployment admission verifies that the tested artifact is the artifact being run.**
   - **Actor:** deployment platform or workload admission controller, not the application team alone.
   - **Input:** immutable artifact digest, signature, provenance, environment, and deployment policy.
   - **Output:** admitted workload or a refusal with a reason and exception route.
   - **Failure:** tag mutation, an unattested artifact, a stale policy, or an unavailable admission service. Sigstore's Kubernetes policy controller resolves image tags and can validate signatures and attestations at admission; Kubernetes validating admission rejects matched objects when a policy fails [Sigstore](https://docs.sigstore.dev/policy-controller/overview/) [Kubernetes admission control](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/). This is a stronger point than CI for deployment integrity, but it still cannot judge future prompts or actions.

4. **The running workflow obtains identity without receiving a permanent master credential.**
   - **Actor:** workload identity issuer and the organization's identity system.
   - **Input:** attested workload properties, environment, initiating user/service identity, approved delegation scope, and session lifetime.
   - **Output:** short-lived workload identity plus a separately represented delegation/“on behalf of” context; no provider or tool receives more authority than needed.
   - **Failure:** a confused deputy, replayable bearer token, overly broad delegate, or lost linkage to the initiating principal. SPIFFE identifies workloads from attested selectors and rotates short-lived credentials, but its Delegated Identity API explicitly warns that an authorized delegate may impersonate the workloads whose identities it can obtain [SPIFFE workload registration](https://spiffe.io/docs/latest/deploying/registering/) [SPIRE delegated identity](https://spiffe.io/docs/latest/deploying/spire_agent/). Delegation is therefore an authority grant requiring allowlists, audience restriction, expiry, and an auditable chain—not merely an `agent_id` string in a log.

5. **The runtime discovers capabilities and selects an implementation.**
   - **Actor:** team-owned runtime or replaceable adapter.
   - **Input:** contract capability requirements, provider/model capability descriptors, health, region, price ceiling, and current policy.
   - **Output:** an explicit compatible route or a typed “required capability unavailable” failure.
   - **Failure:** capability metadata is wrong or a compatibility adapter silently downgrades semantics. MCP offers a useful protocol precedent: client and server negotiate both protocol version and optional capabilities during initialization, and a client should disconnect if it cannot support the negotiated version [MCP lifecycle](https://modelcontextprotocol.io/specification/2025-06-18/basic/lifecycle). An AI platform should copy the explicit negotiation pattern, not assume that endpoint compatibility proves feature support. Provider-specific extensions must be namespaced and visible; unsupported required fields must fail closed rather than be silently dropped.

6. **A gateway applies controls that are truly request-level and cross-cutting.**
   - **Actor:** organization-controlled gateway or egress enforcement layer.
   - **Input:** authenticated caller and delegation, selected provider/model, destination/region, request metadata, declared data class, live budgets/quotas, and policy version.
   - **Output:** an allowed, rejected, rate-limited, redacted, or rerouted provider request plus a decision record.
   - **Failure:** direct network bypass, policy-service outage, false-positive inspection, content hidden by encryption, or a gateway that becomes the common failure domain. OPA's Envoy integration shows the generic mechanism: an L7 proxy sends request context to an external authorization service and enforces its decision without application changes [OPA–Envoy](https://www.openpolicyagent.org/docs/envoy). The gateway is suitable for provider/model allowlists, residency route, credential brokerage, request size, rate/cost limits, and emergency disablement. It is not the final authority for whether `transfer_funds(account, amount)` is permitted.

7. **The model proposes; an execution component and the destination authorize.**
   - **Actor:** tool broker/runtime and the downstream API, database, deployment controller, or business service.
   - **Input:** proposed tool name and arguments, authenticated workload and user delegation, current resource state, transaction risk, idempotency key, approval state, and destination policy.
   - **Output:** deny, step-up/human approval, simulate, or execute; followed by a durable result tied to the decision.
   - **Failure:** the model is treated as an authorization authority, a broad token bypasses resource checks, retries duplicate an irreversible action, or the policy sees too little business context. OWASP's AI Agent Security guidance says the agent may propose an action but an independent policy/execution component should validate scope, privilege, and approval before execution, with short-lived authorization artifacts and replay protection for irreversible operations [OWASP](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html). Resource-side authorization is the non-optional floor: an opt-out runtime may change how actions are proposed, but must not make the bank, source-control system, or production cluster accept an unauthorized action.

8. **Telemetry records semantics, evidence, and uncertainty—not just HTTP success.**
   - **Actor:** runtime, gateway, tool broker, destination systems, and telemetry pipeline.
   - **Input:** correlated run/trace IDs, contract/policy/model/adapter versions, actual provider and response model, token/latency/cost, tool decisions, result status, and evaluation events; sensitive content only under an explicit retention/redaction policy.
   - **Output:** portable telemetry, audit evidence, service-level indicators, anomaly signals, and replay pointers.
   - **Failure:** spans use the same field names with different meanings, high-cardinality cost explodes, prompt content leaks, sampling removes rare harmful events, or the audit pipeline silently stops writing. OpenTelemetry semantic conventions standardize names and meanings across telemetry, but its GenAI attributes have moved and several older fields are deprecated; the registry also warns that provider name can differ from the actual provider behind a compatible or proxied endpoint [OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/) [OpenTelemetry GenAI registry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/). Pin the semantic-convention version and record both requested and actual provider/model.

9. **Operations detect drift and respond without needing to understand every framework.**
   - **Actor:** workflow owner on call, platform operator, security/incident response, and provider manager.
   - **Input:** service and quality SLOs, evaluation samples, user reports, policy decisions, provider notices, model/adapter changes, and correlated incident evidence.
   - **Output:** rollback to a pinned route, disable a model/tool/provider, constrain authority, notify affected owners, preserve evidence, and run a post-incident review.
   - **Failure:** the only kill switch is inside the failed platform; model aliases change behavior without a contract change; or operators see availability but not outcome quality. NIST explicitly includes post-deployment monitoring, incident response, recovery, change management, appeal/override, and decommissioning in AI risk management [NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/). The kill path should therefore be independently operable and tested.

10. **Exit is rehearsed as a supported mode, not documented as a theoretical right.**
    - **Actor:** product team, platform operator, identity/security owners, procurement, and data owner.
    - **Input:** canonical contract, provider-neutral test/evaluation corpus, prompts and tool schemas, policy mappings, telemetry export, data inventory, secrets/identity transition plan, and an alternate route.
    - **Output:** the workflow runs through a different adapter/runtime/provider—or directly—while the same mandatory resource-side controls remain effective; the old route and credentials are then revoked.
    - **Failure:** hidden platform state, proprietary trace/evaluation formats, provider-only capabilities, missing deletion evidence, egress cost, or an exception process whose queue makes exit impractical. NIST's requirement for decommissioning and change management makes exit an operational control, not just a commercial preference [NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/). A quarterly or semiannual “replace one model and bypass the shared runtime” exercise is more credible evidence of freedom than an architecture diagram.

### Where each control can actually live

| Control | CI/repository | Gateway/provider edge | Runtime/tool broker | Downstream resource | Telemetry/operations |
|---|---|---|---|---|---|
| Contract syntax, required ownership, allowed dependency, static secret scan | **Enforce** | Recheck version if useful | Recheck version if useful | — | Detect drift |
| Artifact signature/provenance | Produce evidence | — | Verify at admission/start | May verify caller/workload | Audit |
| Representative quality/safety evaluations | **Run and gate a pinned candidate** | Route only to approved cohort | Shadow/canary/re-evaluate | — | Detect post-deploy drift |
| Provider/model/region allowlist, budget and rate limits | Validate declared intent | **Enforce actual request** | Enforce if no gateway | — | Alert/kill |
| Prompt/output content policy | Test known cases | Enforce what is visible, accepting classifier limits | **Enforce with full workflow context** | Validate typed inputs | Sample/review |
| Tool capability and loop/step budget | Validate declaration/tests | Cannot see all local tools | **Enforce proposal and execution plan** | — | Detect loops |
| User/resource/action authorization | Cannot know live state | Authenticate request, not business entitlement | Carry delegation; never mint extra authority | **Final enforcement** | Audit denied/allowed actions |
| Transaction limit, idempotency, state invariant | Test implementation | Usually insufficient context | Precheck/step-up | **Final atomic enforcement** | Reconcile |
| Retention/deletion/residency | Validate declaration | Route and prevent disallowed providers | Minimize/redact | **Enforce storage policy** | Verify/audit |
| Incident stop | Preconfigure/test | Disable route/provider | Disable tool/workflow | Revoke authority/block action | Trigger and coordinate |

CI is ideal for cheap, deterministic, reproducible checks over declared artifacts. It cannot know the production user's current entitlements, the live payload, provider-side model drift, a retrieved document's instructions, the actual tool arguments selected after several turns, or the destination's current state. A gateway can enforce what crosses it, but a team that opts out can retain freedom only if either its traffic still crosses the mandatory egress boundary or the relevant controls move to the tool and downstream authorization points. Post-hoc telemetry is evidence and detection; it is not prevention unless connected to an independently working kill or revocation path [NIST SP 800-207](https://csrc.nist.gov/pubs/sp/800/207/final) [OWASP](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html).

## Inputs and dependencies

- **Repository and review system:** protected default branch, independently sourced required checks, controlled bypass list, immutable commit identity, and code owners. GitHub documents both expected check sources and bypass permissions, so these must be treated as governed privileges [GitHub rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets).
- **Contract registry:** immutable schemas/dialects, compatibility rules, converters, policy-to-contract mappings, and a readable changelog. Kubernetes' formal deprecation policy illustrates the necessary properties: supported overlap, announced removal, migration guidance, and rollback compatibility—not indefinite support [Kubernetes deprecation policy](https://kubernetes.io/docs/reference/using-api/deprecation-policy/).
- **Build/deployment evidence:** artifact digest, provenance, signer trust roots, and verifier at admission. Provenance without verification at the deployment boundary is only paperwork [SLSA](https://slsa.dev/spec/v1.2/) [Sigstore](https://docs.sigstore.dev/policy-controller/overview/).
- **Identity:** human/service identity, workload identity, explicit delegation, short lifetimes, revocation, audience restriction, and destination-side authorization. SPIFFE supplies a portable workload identity pattern, but the organization must define what each identity is authorized to do [SPIFFE Workload API](https://spiffe.io/docs/latest/spiffe-specs/spiffe_workload_api/).
- **Provider/model inventory:** immutable versions where offered, deprecation dates, region and retention terms, capability claims, quotas, price, health, and direct native API documentation. Capability claims must be tested because compatible APIs can ignore fields [Anthropic](https://platform.claude.com/docs/en/cli-sdks-libraries/libraries/openai-sdk) [Google](https://ai.google.dev/gemini-api/docs/openai).
- **Evaluation assets:** versioned representative and adversarial cases; business assertions; tool-call and structured-output validators; acceptable variance; human-review rubric; and enough retained evidence to compare candidates. NIST calls for documenting test sets, metrics, and TEVV tools [NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/).
- **Policy decision and enforcement:** independently governed policy bundles, request context, tool/resource context, explicit fail-open/fail-closed behavior, emergency override, and cached safe decisions. A policy engine without an unavoidable enforcement point is advisory [OPA–Envoy](https://www.openpolicyagent.org/docs/envoy).
- **Observability and audit:** stable run identity, trace propagation, semantic-convention version, redaction rules, sampling exceptions for high-impact actions, append-resistant audit storage, and health monitoring of the logging pipeline itself [OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/).
- **Operations:** named service owners, SLOs, provider/model change watch, on-call, tested rollback/kill/revoke procedures, exception SLA, and a funded migration/exit path. NIST treats monitoring and decommissioning as lifecycle activities [NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/).

## Internals where most coverage waves hands

### 1. Schema and semantic versioning

Use a stable, deliberately small core with an explicit `contractVersion`, a `$schema` URI, and namespaced extensions such as `provider.google.*` or `framework.langgraph.*`. Additive fields are not automatically compatible: a new required meaning, a tightened enum, or a changed default can break behavior even when old parsers still accept the document. Every release needs a compatibility table across **reader, writer, validator, policy bundle, runtime, and exporter**, plus one-way converters and a period in which both old and new versions can be operated. JSON Schema calls specification versions “dialects”; Kubernetes' API-removal history demonstrates why schema lifecycle is an operating responsibility, not a serialization detail [JSON Schema](https://json-schema.org/understanding-json-schema/reference/schema) [Kubernetes migration guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/).

Unknown required semantics should fail explicitly. Unknown optional extensions may be preserved round-trip even if a component cannot act on them. Otherwise a platform that reads and rewrites a contract can destroy the provider-specific state a team needs to leave it.

### 2. Capability discovery and conformance

Maintain machine-readable capability descriptors for each **provider + model version + API path + adapter version**, not for a vendor brand. Probe them continuously with conformance tests: strict tool schema adherence, parallel tool calls, streaming argument assembly, multimodal inputs, refusal/stop reasons, context limits, seed claims, logprobs, citations, and provider-native tools. MCP's version/capability negotiation is the right interaction shape, while current first-party compatibility documents show why optimistic assumptions are unsafe [MCP](https://modelcontextprotocol.io/specification/2025-06-18/basic/lifecycle) [Anthropic](https://platform.claude.com/docs/en/cli-sdks-libraries/libraries/openai-sdk) [Google](https://ai.google.dev/gemini-api/docs/partner-integration).

Do not convert an unsupported requirement into a default. Return a typed incompatibility explaining which required capability failed. The LiteLLM issue where streaming translation discarded tool arguments shows that even a previously working adapter version can change capability semantics, so adapter upgrades belong in the tested release unit [LiteLLM issue 25321](https://github.com/BerriAI/litellm/issues/25321).

### 3. Adapters and the anti-corruption boundary

An adapter should translate only a documented, tested common core and expose provider-native features through visible extensions or a direct-native escape hatch. Record the canonical request, native transformed request, native response, and canonical response under controlled redaction so a failed translation is diagnosable. Never label an endpoint simply “compatible”; publish a conformance matrix and the exact adapter/model versions tested.

This boundary is deliberately permeable. Teams should be able to import the shared contract types and control clients while calling a native provider SDK for features outside the core. Google explicitly recommends its native SDK/API for full feature access and acknowledges translation overhead in the compatibility route; Anthropic likewise directs users to its native API for full capabilities [Google](https://ai.google.dev/gemini-api/docs/partner-integration) [Anthropic](https://platform.claude.com/docs/en/cli-sdks-libraries/libraries/openai-sdk). Forcing all native innovation back through the common interface converts portability into a lowest-common-denominator ceiling.

### 4. Identity and delegation

Represent three subjects separately: the human/service that requested the work, the deployed workload executing it, and the model/provider that assisted. An agent must not inherit the union of every possible user's and tool's permissions. Mint short-lived, audience-bound capabilities for one task or step; include contract, run, tool, resource, and approval identifiers; make irreversible requests idempotent; and require destinations to check the current user/resource policy.

SPIFFE can attest the running workload independently of a long-lived secret, but delegation remains a high-risk function because a delegate may impersonate other workloads [SPIFFE](https://spiffe.io/docs/latest/deploying/spire_agent/). The destination, not the language model or gateway, is the final authority. This is how a team can replace the agent framework without replacing organizational authorization.

### 5. Evaluations and evidence

There are two different gates. A **conformance suite** checks that the adapter transports required structure and events correctly. A **behavioral suite** checks that the candidate system—model, provider, system prompt, retrieval, tools, runtime, and policies together—satisfies workflow assertions and risk tolerances. Run both for every candidate route and material change, retain the tested tuple, then canary and monitor after deployment. A model alias is not an immutable behavioral version.

The GPT-4o sycophancy episode in the source-supplied month window (exact day not stated): 2025-04 is direct evidence: individually positive changes combined into behavior that existing review did not catch, and OpenAI subsequently added sycophancy evaluations and more explicit behavioral launch review [OpenAI, 2025-05-02](https://openai.com/index/expanding-on-sycophancy/). Passing an HTTP compatibility test would have said nothing about this failure.

### 6. Telemetry semantics and export

Define a canonical, versioned export package containing the contract, schemas, prompts/templates where legally retainable, evaluation inputs and expected assertions, provider/model/adapter versions, policy decisions, tool proposals/results, approvals, trace links, cost/latency, and deletion/retention metadata. Use portable envelopes and OpenTelemetry names where stable, but preserve raw provider fields in a namespaced section and pin the semantic-convention version. OpenTelemetry's own GenAI attribute migration and deprecations show that “standard telemetry” also evolves [OpenTelemetry GenAI registry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/).

Treat content capture separately from operational metadata. Defaulting to complete prompt/response logging can turn observability into a second sensitive-data store. Conversely, sampling away denied or high-impact tool actions makes the audit trail useless. Keep complete decision metadata for controlled actions; store sensitive content only under explicit purpose, access, retention, and deletion policy.

## Failure modes

1. **Same API shape, different semantics.** On 2025-08-29, a Gemini user reported that documented `safety_settings` did not work through the OpenAI compatibility layer; on 2025-11-10, a Google forum representative answered that the feature was not available there [Google AI Developers Forum](https://discuss.ai.google.dev/t/safety-settings-still-doent-work-in-openai-api-compatibility-layer/100712). On 2026-07-31, Anthropic's compatibility documentation also said `strict` function calling is ignored and unsupported fields are usually silently ignored; Google's documentation described silently ignored parameters and a non-one-to-one mapping. A request can return `200 OK` while a safety- or correctness-relevant promise has disappeared [Anthropic](https://platform.claude.com/docs/en/cli-sdks-libraries/libraries/openai-sdk) [Google](https://ai.google.dev/gemini-api/docs/openai). **Countermeasure:** required-capability negotiation, strict rejection, conformance probes, and native extensions.

2. **Adapter translation corrupts an action.** A LiteLLM issue opened on 2026-04-08 reported that versions after `1.81.14` dropped tool-use arguments while translating streamed non-Anthropic responses, producing empty inputs and repeated validation failures [LiteLLM issue 25321](https://github.com/BerriAI/litellm/issues/25321). **Countermeasure:** pin adapter versions, golden streaming fixtures, end-to-end tool tests, typed failure rather than retries, and raw/native replay evidence.

3. **Behavior changes without an interface change.** OpenAI rolled out a GPT-4o update on 2025-04-25, began rollback on 2025-04-28, and reported that existing review had missed noticeably sycophantic behavior caused by combined changes [OpenAI, 2025-05-02](https://openai.com/index/expanding-on-sycophancy/). **Countermeasure:** behavioral—not just API—portability tests, pinned routes where possible, canaries, user-report signals, and independent rollback.

4. **The common control plane becomes the common outage.** On 2025-06-12, failure of Workers KV's central backing infrastructure affected Cloudflare Access, Gateway, Workers AI, AutoRAG, and other services for 2 hours 28 minutes; Gateway failed closed where identity/posture policy could not be evaluated [Cloudflare](https://blog.cloudflare.com/cloudflare-service-outage-june-12-2025/). **Countermeasure:** dependency budgets, cached bounded decisions, degraded modes chosen per risk, direct emergency routes, regional isolation, and an independently reachable kill/override plane.

5. **CI passes but the wrong code or state runs.** On 2012-08-01, Knight Capital's inconsistent software deployment activated defective legacy code; the SEC found inadequate deployment/testing controls and, crucially, inadequate controls immediately before orders entered the market. The incident generated more than 4 million orders and a loss exceeding $460 million [SEC, 2013-10-16](https://www.sec.gov/newsroom/press-releases/2013-222). **Countermeasure:** signed immutable artifacts, admission verification, staged rollout, and business invariants at the final action boundary.

6. **Delegation and token validation collapse trust boundaries.** During the source-supplied month range (exact days not stated): 2023-05 to 2023-06, Storm-0558 used a Microsoft consumer signing key to forge tokens and compromise Exchange Online mailboxes; Microsoft's investigation said developers had assumed libraries performed complete validation and omitted issuer/scope checks [CISA CSRB](https://www.cisa.gov/sites/default/files/2024-04/CSRB_Review_of_the_Summer_2023_MEO_Intrusion_Final_508c.pdf) [Microsoft, updated 2024-03-12](https://www.microsoft.com/en-us/msrc/blog/2023/09/results-of-major-technical-investigations-for-storm-0558-key-acquisition/). **Countermeasure:** audience/issuer/scope validation at every relying party, short-lived keys, hardened libraries, constrained delegation, and logs available to defenders.

7. **The audit system fails silently.** On 2026-02-19, OpenAI opened an incident after reports of API audit-log issues; its write-up attributes the write failure to a missing Kafka environment variable after a monolith had been split into services [OpenAI status](https://status.openai.com/incidents/01KJXA4N2X4W8KHZFSSFH0V0Q7/write-up). **Countermeasure:** monitor log completeness as a production SLO, reconcile source request counts with durable records, alert on gaps, and define whether high-impact actions fail closed when evidence cannot be written.

8. **Version removal makes the “stable contract” an upgrade blocker.** Kubernetes 1.22, released on 2021-08-04, stopped serving multiple deprecated beta APIs; the official migration guide requires users and custom integrations to move to replacement APIs [Kubernetes release note](https://kubernetes.io/blog/2021/07/14/upcoming-changes-in-kubernetes-1-22/) [Kubernetes migration guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/). **Countermeasure:** supported version overlap, converters, usage telemetry, removal rehearsal, and funding consumer migrations as part of platform ownership.

9. **A gateway rule misroutes most traffic.** On 2025-06-24, an OpenAI networking-rule misconfiguration sent significant `/v1/chat/completions` traffic to the wrong backend; most requests failed for 13 minutes [OpenAI status](https://status.openai.com/incidents/01JYHS81RRRWYZMC4NK3GRYRQK/write-up). **Countermeasure:** staged route changes, typed health checks through every backend, automatic rollback, and provider diversity that is tested rather than merely configured.

## Recommended constraints

The constraints below are **architectural synthesis/inference from the cited evidence**, not requirements stated verbatim by any single source.

- **Synthesis/inference — the common core has a hard ceiling.** Provider-specific reasoning, caching, citations, server tools, multimodal formats, stop reasons, and structured-output guarantees differ. First-party compatibility documents explicitly disclose feature loss and transformation [Anthropic](https://platform.claude.com/docs/en/cli-sdks-libraries/libraries/openai-sdk) [Google](https://ai.google.dev/gemini-api/docs/partner-integration). **Recommendation inferred from that evidence:** permit native use or the common core will slow advanced teams.
- **Synthesis/inference — behavioral equivalence cannot be proven by schema.** Probabilistic output, model updates, system prompts, retrieval state, and provider serving details change the distribution. Evaluations establish evidence over selected cases, not universal equivalence; NIST's lifecycle guidance supports continued post-deployment monitoring [NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/). **Recommendation inferred from that evidence:** treat behavioral tests as bounded evidence and continue monitoring after release.
- **Synthesis/inference — a central gateway only controls traffic that cannot bypass it.** OPA–Envoy demonstrates enforcement at a proxy, while Cloudflare's incident demonstrates the blast radius and availability trade-off of a shared enforcement dependency [OPA–Envoy](https://www.openpolicyagent.org/docs/envoy) [Cloudflare](https://blog.cloudflare.com/cloudflare-service-outage-june-12-2025/). **Recommendation inferred from that evidence:** make required controls unavoidable through network egress, credential issuance, provider tenancy, or downstream authorization, and design a degraded mode for the resulting common dependency.
- **Synthesis/inference — content classifiers are not authorization engines.** They lack live account/resource state and cannot provide atomic business invariants; OWASP places independent scope, privilege, and approval validation before agent actions [OWASP](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html). **Recommendation inferred from that evidence:** require the destination to authorize and validate the action.
- **Synthesis/inference — strong controls impose latency and availability costs.** Every synchronous policy call, classifier, approval, and trace write adds a dependency; Cloudflare's fail-closed Gateway behavior shows that preserving policy can stop legitimate traffic when a shared dependency fails [Cloudflare](https://blog.cloudflare.com/cloudflare-service-outage-june-12-2025/). **Recommendation inferred from that evidence:** make the accountable risk owner document fail-open or fail-closed behavior per action class, not once for the whole platform.
- **Synthesis/inference — multi-provider readiness is ongoing work.** First-party compatibility documents show provider-specific semantics, while NIST treats testing, monitoring, change management, and decommissioning as lifecycle work [Anthropic](https://platform.claude.com/docs/en/cli-sdks-libraries/libraries/openai-sdk) [Google](https://ai.google.dev/gemini-api/docs/partner-integration) [NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/). **Recommendation inferred from that evidence:** maintain adapters, conformance and behavioral suites, procurement, identities, regions, incident procedures, and operator knowledge; do not count an unexercised fallback as exit.
- **Synthesis/inference — portability can conflict with evidence retention and privacy.** OpenTelemetry supplies evolving telemetry semantics rather than a retention policy, while NIST calls for lifecycle evidence and decommissioning [OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/) [NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/). **Recommendation inferred from that evidence:** define field-level purpose, access, export, retention, and deletion rather than either archiving everything or retaining nothing.
- **Synthesis/inference — organizational queues can defeat technical optionality.** DORA identifies developer independence, user-centered design, and avoidance of gatekeeping/ticket-ops as platform capabilities associated with better outcomes [DORA](https://dora.dev/capabilities/platform-engineering/). **Recommendation inferred from that evidence:** include exception turnaround, ticket-free completion, support outside the paved road, and exit rehearsal time in the platform SLO.

## Side effects

- The contract authors gain power over what is legible and permitted. Version changes therefore need consumer representation, transparent rationale, migration cost accounting, and a sunset/appeal process.
- A shared gateway can remove repeated credential, routing, and audit work, while simultaneously creating a concentrated outage and policy-change blast radius. The Cloudflare 2025-06-12 incident shows how a shared backing service propagated failure across otherwise distinct products [Cloudflare](https://blog.cloudflare.com/cloudflare-service-outage-june-12-2025/).
- A portability adapter can create more lock-in than direct provider use if prompts, evaluations, traces, and error handling become coupled to its canonical semantics. The LiteLLM translation regression is a concrete instance of an extra failure surface [LiteLLM issue 25321](https://github.com/BerriAI/litellm/issues/25321).
- Provider diversity can improve bargaining power and resilience, but it multiplies testing, procurement, privacy assessment, on-call knowledge, and behavioral variance. Count that work in the leverage calculation.
- Mandatory downstream authorization preserves freedom at the AI layer because any framework may propose the action. It also limits the agent's apparent autonomy, which is appropriate when the destination owns the harm.
- Rich telemetry improves incident response and portability but creates a sensitive secondary dataset and potentially high-cardinality cost. OpenTelemetry supplies shared vocabulary, not safe retention defaults [OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/).
- Fail-closed policy protects against bypass but can turn governance into a production dependency; fail-open improves continuity but can invalidate the control. Cloudflare explicitly documented that identity-based Gateway paths failed closed during its outage [Cloudflare](https://blog.cloudflare.com/cloudflare-service-outage-june-12-2025/).
- A well-designed escape hatch creates some intentional duplication. That duplication is the option premium paid to keep exit real; it should be measured against the expected cost and likelihood of switching, not assumed to be waste.

## Plain-language analogy

Think of the platform as a **travel adapter, an electrical inspection, and a circuit breaker**, not as one universal appliance.

- The repository contract says what plug, voltage range, and safety class the appliance claims.
- CI checks the paperwork and tests the appliance under known loads.
- The adapter lets it connect to more than one socket; that is wire/API compatibility.
- The breaker sits where it can stop dangerous current; that is the gateway or runtime enforcement point.
- The appliance itself still decides what work it does, and the machine it controls still needs its own interlock; those are behavioral semantics and downstream authorization.
- Leaving the platform means using another inspected adapter while keeping the building's breaker and machine interlocks.

The analogy breaks because electrical behavior is substantially more deterministic and measurable than model behavior. Two model endpoints accepting the same request can choose different tools, refuse differently, or change after a provider update. An AI “adapter” therefore needs continual behavioral evaluation and production evidence, not just a standards mark.

## Source receipts

### Primary

- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) — lifecycle testing, monitoring, incident response, override, change, and decommissioning.
- [NIST SP 800-207, Zero Trust Architecture](https://csrc.nist.gov/pubs/sp/800/207/final) — policy decision and enforcement-point separation.
- [CISA Cyber Safety Review Board report on Storm-0558](https://www.cisa.gov/sites/default/files/2024-04/CSRB_Review_of_the_Summer_2023_MEO_Intrusion_Final_508c.pdf) — identity, token, logging, and cloud-control failure evidence.
- [SEC order/press release on Knight Capital, 2013-10-16](https://www.sec.gov/newsroom/press-releases/2013-222) — deployment mismatch and missing last-point risk controls.
- [OpenAI sycophancy review, 2025-05-02](https://openai.com/index/expanding-on-sycophancy/) — behavioral drift missed by pre-deployment review.
- [Cloudflare outage review, 2025-06-12](https://blog.cloudflare.com/cloudflare-service-outage-june-12-2025/) — shared-dependency blast radius and fail-closed policy trade-off.
- [OpenAI API routing incident, 2025-06-24](https://status.openai.com/incidents/01JYHS81RRRWYZMC4NK3GRYRQK/write-up) — central routing misconfiguration.
- [OpenAI API audit-log incident, opened 2026-02-19](https://status.openai.com/incidents/01KJXA4N2X4W8KHZFSSFH0V0Q7/write-up) — telemetry pipeline failure after service decomposition.

### Technical Docs

- [Anthropic OpenAI SDK compatibility](https://platform.claude.com/docs/en/cli-sdks-libraries/libraries/openai-sdk) — ignored strictness, silently ignored fields, feature and prompting differences.
- [Google partner integration guidance](https://ai.google.dev/gemini-api/docs/partner-integration) and [OpenAI compatibility reference](https://ai.google.dev/gemini-api/docs/openai) — non-one-to-one schema, translation overhead, native-feature gaps, and ignored parameters.
- [vLLM OpenAI-compatible server](https://docs.vllm.ai/en/v0.22.0/serving/online_serving/openai_compatible_server/) — unsupported and ignored request parameters.
- [JSON Schema dialect guidance](https://json-schema.org/understanding-json-schema/reference/schema) and [core specification](https://github.com/json-schema-org/json-schema-spec/blob/main/specs/jsonschema-core.md) — schema dialect and compatibility mechanics.
- [MCP lifecycle](https://modelcontextprotocol.io/specification/2025-06-18/basic/lifecycle) — version and capability negotiation precedent.
- [GitHub repository rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets) — required checks, trusted check source, and bypass permissions.
- [SLSA v1.2](https://slsa.dev/spec/v1.2/) — artifact provenance and organization-defined verification policy.
- [Sigstore policy controller](https://docs.sigstore.dev/policy-controller/overview/) — admission-time signature/attestation verification.
- [Kubernetes admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/), [deprecation policy](https://kubernetes.io/docs/reference/using-api/deprecation-policy/), and [migration guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/) — final deployment gate and version-lifecycle precedent.
- [SPIFFE Workload API](https://spiffe.io/docs/latest/spiffe-specs/spiffe_workload_api/), [registration](https://spiffe.io/docs/latest/deploying/registering/), and [SPIRE delegated identity](https://spiffe.io/docs/latest/deploying/spire_agent/) — workload attestation, short-lived identity, and delegation hazards.
- [OPA–Envoy integration](https://www.openpolicyagent.org/docs/envoy) — external policy decision with proxy enforcement.
- [OWASP AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html) — independent pre-action validation and least privilege.
- [OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/) and [GenAI attribute registry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/) — portable telemetry vocabulary, maturity, and provider attribution caveats.

### Filings

- [SEC administrative order concerning Knight Capital](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf) — regulatory record of inadequate deployment, pre-trade, and incident controls.

### News

- No news report is load-bearing in this mechanism analysis. Incident claims were traced to provider postmortems or government/regulatory records rather than secondary coverage.

### Practitioner Commentary

- [Google AI Developers Forum compatibility report, 2025-08-29 to 2025-11-10](https://discuss.ai.google.dev/t/safety-settings-still-doent-work-in-openai-api-compatibility-layer/100712) — user report and Google response that a documented safety option was unavailable through the compatibility layer.
- [LiteLLM issue 25321, opened 2026-04-08](https://github.com/BerriAI/litellm/issues/25321) — reproducible streaming-adapter regression that removed tool arguments.
- [LiteLLM issue 11047](https://github.com/BerriAI/litellm/issues/11047) — a practitioner's tool-calling failure caused by model-server parser and template configuration, illustrating that capability depends on the whole serving tuple.
- [vLLM issue 19097](https://github.com/vllm-project/vllm/issues/19097) — maintainers and users discussing collision risks between provider-specific extensions and future upstream-compatible fields.
