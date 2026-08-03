# Mechanism: a minimal, portable post-task agent receipt

## What I'm unpacking

The mechanism is a versioned, integrity-protected **agent receipt** that projects the minimum reviewable facts about one completed or stopped task while the identity provider, policy engine, tool-owning domain systems, evidence stores, and telemetry backends retain the authoritative records.

The architectural claim is deliberately narrower than “put the agent on a ledger.” A receipt is a portable index and verification summary. It is not the event store, not a transcript of model reasoning, not a distributed trace, and not proof that the underlying action was correct. That separation follows a mature pattern: W3C PROV supplies portable concepts for entities, activities, agents, derivation, and delegation, while allowing domain-specific extensions; in-toto binds authenticated claims to immutable subjects; and event-sourced systems keep the event stream, rather than a projection, as the system of record ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md), [Microsoft Event Sourcing pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)).

## The walkthrough

### 1. Open a task boundary before the first action

- **Actor:** The orchestrator, not the language model.
- **Input:** Request, requester identity, declared purpose, risk tier, and the agent package/configuration selected to handle it.
- **Output:** A globally unique `receipt_id`, `task_id`, start time, schema/profile URI, and trace context. The task identifier is the business boundary; the trace identifier is only the observability correlation key.
- **What can fail:** Work can start before the boundary exists; retries can create several apparent tasks; or a long-running workflow can be falsely collapsed into one “completed” unit. W3C Trace Context defines portable `traceparent` and `tracestate` fields for linking telemetry across vendors, but it does not define the business task, its authority, or its outcome ([W3C Trace Context](https://www.w3.org/TR/trace-context/)).

The orchestrator should create the receipt skeleton durably before dispatch. That yields an explicit `started`, `abandoned`, `timed_out`, `partially_completed`, `compensated`, or `completed` lifecycle instead of manufacturing a receipt only on the happy path. A2A makes a similar distinction: a `Task` has a lifecycle state, artifacts, message history, and metadata; each artifact is tied to a unit task ([A2A protocol schema](https://github.com/a2aproject/A2A/blob/main/specification/a2a.proto), [A2A life of a task](https://a2aproject.github.io/A2A/latest/topics/life-of-a-task/)).

### 2. Resolve who is acting for whom, and what is allowed now

- **Actor:** Identity provider and policy decision point; the orchestrator supplies task context.
- **Input:** Human/service principal, agent workload identity, requested resource/action, current policy, approval, and any delegation chain.
- **Output:** An authorization-decision reference plus a compact snapshot: issuer, subject, actor, audience/resource, granted action or capability, policy version, decision time, expiry, and approval reference. Never copy bearer tokens or credentials into the receipt.
- **What can fail:** The receipt can name the user but lose the actual actor; record a static role while policy changed mid-task; omit a sub-agent; or accept a token intended for another resource. OAuth Token Exchange distinguishes delegation from impersonation and defines an `act` claim capable of representing a delegation chain; MCP requires audience-bound tokens and forbids token passthrough because otherwise an intermediary can become a confused deputy ([RFC 8693](https://www.rfc-editor.org/info/rfc8693/), [MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)).

The receipt records the **decision that was exercised**, not merely what an agent was generally configured to do. NIST's concept paper released on 2026-02-05 treats task-dependent identity, dynamic authorization, human-agent binding, intent, delegation, auditing, and non-repudiation as open design problems, so any proposed universal authority field should be labeled experimental rather than settled ([NIST agent identity and authorization concept paper](https://www.nccoe.nist.gov/sites/default/files/2026-02/accelerating-the-adoption-of-software-and-ai-agent-identity-and-authorization-concept-paper.pdf)).

### 3. Freeze the execution identity needed to interpret the run

- **Actor:** Orchestrator and deployment/configuration registries.
- **Input:** Agent definition, instruction bundle, model/provider route, tool registry, guardrail set, evaluator set, code/build revision, and environment.
- **Output:** Stable identifiers and content digests for the versions actually used, plus provider-reported model identifiers where available.
- **What can fail:** A friendly label such as `settlement-explainer` or `approved-eu-provider` can point to different code, prompts, models, or regions later. The receipt then describes a name, not an executable identity.

SLSA provenance provides the useful structural precedent: separate the definition of work from run details, bind the output subject by digest, and verify provenance against consumer-defined expectations. Its levels also make the crucial trust distinction: provenance merely existing is weaker than signed provenance produced by a hosted, hardened control plane ([SLSA terminology and verification model](https://slsa.dev/spec/v1.1/terminology), [SLSA build levels](https://slsa.dev/spec/v1.1/levels)). For agents, the analogous `execution_identity` should be produced by the orchestration/control plane, not copied from prose the model emits about itself.

### 4. Execute tools while source systems record domain-native facts

- **Actor:** Tool gateway and the system that owns each effect: database, payment service, source-control platform, cluster API, ticketing system, or document store.
- **Input:** Authorized command with task/receipt correlation identifiers and an idempotency key where the domain supports one.
- **Output:** Domain-native result containing resource/event/transaction ID, state or version, timestamps, actor identity as recognized by that system, and outcome. The receipt stores typed references and selected hashes, not a copied substitute for those records.
- **What can fail:** A tool can report success before a transaction commits; telemetry can be sampled or dropped; the agent can paraphrase an effect incorrectly; or a downstream service can lose correlation context.

This is where a receipt must resist becoming a second, weaker source of truth. Kubernetes audit events, for example, chronicle requests through defined execution stages and are filtered by an audit policy; Stripe events represent changes to API resources and preserve the API version used to render their snapshot. Those records know domain semantics a generic agent schema does not ([Kubernetes auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/), [Stripe Events API](https://docs.stripe.com/api/events)). MCP standardizes a tool-call result and warns clients that tool annotations are untrusted unless they come from a trusted server; it does not make the agent's summary authoritative ([MCP tools specification](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)).

### 5. Preserve causality across tools, services, retries, and delegation

- **Actor:** Orchestrator, instrumented services, and agent-to-agent gateways.
- **Input:** Task ID, parent/child action IDs, trace context, attempt number, idempotency key, and delegation/authority reference.
- **Output:** A causal graph linking request → plan step → tool or sub-agent call → domain event → produced artifact, including superseded attempts and compensation edges.
- **What can fail:** Context is not injected into an asynchronous message; parallel branches are ordered by wall-clock time rather than parentage; retries look like distinct effects; or a sub-agent's actions are incorrectly attributed to its caller.

OpenTelemetry context propagation can carry correlation across process and network boundaries, and its GenAI conventions currently define operations such as `invoke_agent` and `execute_tool`; those conventions are explicitly still in development and warn that tool arguments/results may contain sensitive information ([OpenTelemetry context propagation](https://opentelemetry.io/uk/docs/concepts/context-propagation/), [OpenTelemetry GenAI attributes](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/)). W3C PROV adds semantics that a trace lacks—`wasDerivedFrom`, `wasAssociatedWith`, and `actedOnBehalfOf`—but it still needs a domain profile to express a particular authorization decision or money movement ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/)).

### 6. Resolve inputs and effects as evidence, without ingesting everything

- **Actor:** Receipt assembler operating outside the model loop.
- **Input:** Trace spans, tool results, domain events, source documents, model/configuration identities, and evidence-store metadata.
- **Output:** Typed evidence pointers with immutable version or digest, media type, owning system, access class, retention horizon, and a human-readable label. For mutable resources, point to a versioned snapshot or content digest, not merely a “latest” URL.
- **What can fail:** A URL resolves to changed content; a vendor deletes an event; permissions prevent the reviewer from opening evidence; a hash proves bytes but not their meaning; or a receipt copies sensitive evidence and creates a second disclosure surface.

in-toto's Statement layer binds an attestation to subjects by digest and identifies the predicate schema; W3C PROV-AQ defines mechanisms for discovering and querying provenance records. Both point toward a receipt that carries resolvable, typed references rather than unbounded evidence blobs ([in-toto Statement](https://github.com/in-toto/attestation/blob/main/spec/v1/statement.md), [W3C PROV-AQ](https://www.w3.org/TR/prov-aq/)). Availability remains separate from integrity: SLSA's threat analysis explicitly says that deletion of code, artifacts, or provenance is not currently addressed by its integrity model ([SLSA threats and mitigations](https://slsa.dev/spec/v1.1/threats)).

### 7. Close every branch, including partial and compensating work

- **Actor:** Workflow engine and each domain system.
- **Input:** Per-step terminal status, committed effects, failed attempts, pending work, compensation requests, and compensation outcomes.
- **Output:** A task-level state plus an effects table in which every planned or attempted external action is `not_started`, `rejected`, `committed`, `failed_unknown`, `compensated`, `compensation_failed`, or `irreversible`. “No changes” is an assertion that must be supported by enumerated tool boundaries, not a default empty array.
- **What can fail:** One branch commits while another times out; a retry duplicates an irreversible action; compensation is mistaken for rollback; or the receipt calls a task successful because the natural-language answer completed even though a side effect did not.

Distributed workflows cannot generally be summarized by one Boolean. Microsoft's compensating-transaction guidance says compensations are domain-specific, can themselves fail, may not restore the original state, and must be correlated with the original operation end to end ([Microsoft Compensating Transaction pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/compensating-transaction)). A receipt therefore needs effect-level facts and a task disposition such as `completed_with_uncompensated_effects`, not just `verification: passed`.

### 8. Verify claims independently of the acting agent

- **Actor:** One or more policy/evaluation engines, domain reconcilers, or human approvers distinct from the model that acted.
- **Input:** Receipt draft, authoritative effect references, expected policy, test/evaluation definition, and risk-tier rules.
- **Output:** Typed verification claims: verifier identity and revision, criterion/policy URI, subject digest or effect reference, method, result, timestamp, uncertainty or coverage, and evidence pointer.
- **What can fail:** The “verifier” is the same agent restating its answer; only output style is checked; a policy says `passed` without naming the evaluated subject; or the verifier cannot access the cited source.

The in-toto framework separates a predicate from the Statement that binds it to a subject and the Envelope that authenticates it; its vetted predicate set includes test results and simple verification results. SLSA likewise requires consumers to compare provenance against expectations rather than trust a signature alone ([in-toto predicate registry](https://github.com/in-toto/attestation/blob/main/spec/predicates/README.md), [SLSA threats and mitigations](https://slsa.dev/spec/v1.1/threats)). For high-impact work, domain reconciliation—for example, confirming the actual ledger transaction, deployed image digest, or cluster object version—is stronger than asking a second model whether the first model “looks correct.”

### 9. Project the minimum receipt for the task's risk tier

- **Actor:** Deterministic receipt assembler and redaction/policy engine.
- **Input:** Authenticated facts and references from the earlier steps, risk tier, audience, legal basis, retention policy, and receipt profile.
- **Output:** Canonically encoded, schema-versioned receipt. A useful core is: identity; request/purpose; lifecycle; exercised authority; execution identity; typed inputs; attempted and committed effects; delegations; verification claims; unresolved uncertainty; trace/evidence references; cost/resource summary; reversibility/compensation; access and retention metadata.
- **What can fail:** “Minimal” becomes one universal schema that omits sector facts; “portable” becomes lowest-common-denominator strings; redaction makes a signature unverifiable; or verbose prompt/tool capture recreates a surveillance archive.

Risk tiering should change required claims, not merely retention length. A read-only summary may retain output digest, input versions, trace reference, and evaluation. A production change should add the exact resource versions, approval, exercised authority, before/after references, rollback/compensation status, and an independent domain check. A payment should point to the ledger's transaction and reconciliation events. The EU AI Act requires automatic logging capabilities for high-risk systems sufficient to support risk detection, post-market monitoring, and operational monitoring, but that obligation is scoped to high-risk systems rather than proof that one universal receipt is legally sufficient ([Regulation (EU) 2024/1689, Article 12](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)).

### 10. Sign, timestamp, publish, verify, and eventually expire

- **Actor:** Trusted receipt service, key-management system, optional transparency service, receipt store, and independent consumer.
- **Input:** Canonical receipt payload, signing identity, key/certificate, trusted time, schema/profile, and retention/access policy.
- **Output:** Signed envelope and verification material; optional transparency-log inclusion proof; searchable index; explicit expiry/tombstone semantics; and a consumer-side verification result.
- **What can fail:** A compromised key signs lies; the signature survives but evidence disappears; key revocation makes later verification ambiguous; a public transparency log leaks personal or commercial data; or deletion destroys both content and the ability to explain why it was removed.

DSSE authenticates both arbitrary payload and payload type while deliberately leaving key management and PKI out of scope; a Sigstore bundle packages the material needed to verify later, including transparency entries or timestamps for short-lived certificates. C2PA similarly binds assertions, a claim, and a signature into a verifiable manifest, but bases trust decisions on the signer identity—the signature protects integrity and attribution, not truth ([DSSE specification](https://github.com/secure-systems-lab/dsse), [Sigstore bundle format](https://docs.sigstore.dev/about/bundle/), [C2PA 2.2 specification](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)).

The consumer must independently perform four checks: schema/profile support, signature and signing-time validity, subject/effect digest matching, and policy evaluation against expected issuer/actor/authority/verifier. “Signature valid” is one input to trust, never the final verdict.

## Inputs and dependencies

| Dependency | Specific instance | What the receipt needs from it | Why it cannot simply be copied into the receipt |
|---|---|---|---|
| Task/orchestration store | A2A-style `Task`, or a local workflow record | Stable task ID, lifecycle, attempts, parent/child relationships, artifacts | A2A task history and artifacts may contain sensitive information and require protection; the portable receipt needs a selective projection ([A2A specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)). |
| Identity and authorization | OAuth resource-bound authorization plus RFC 8693 delegation | Issuer, subject, actor/delegation chain, audience, granted action, policy/grant reference, expiry | Tokens are bearer secrets and capture protocol claims, not necessarily the complete policy decision; MCP warns that cached or logged tokens can be stolen ([MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)). |
| Agent/configuration registry | Versioned agent, prompt/instruction, guardrail, evaluator, model route | Stable identifiers and immutable digests | Display names drift; vendor model aliases and provider routes can change. |
| Tool gateway | MCP or framework-specific tool executor | Call ID, trusted server/tool identity, arguments digest or redacted summary, result/effect refs, error | MCP `structuredContent` standardizes result shape, but tool annotations may be untrusted ([MCP tools specification](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)). |
| Domain source of truth | Kubernetes API audit events, source-control commits, payment ledger, ticket event stream | Durable transaction/event/resource IDs, versions, committed state, actor and domain result | Only the owning domain can state whether an effect committed; a generic agent trace observes calls, not necessarily final state ([Kubernetes auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)). |
| Telemetry | W3C Trace Context and OpenTelemetry spans/logs/events | Trace/span IDs, causal links, timings, errors, tool/model usage and resource measures | Sampling, exporter failure, retention, and development-stage semantic conventions make telemetry useful diagnostic evidence but an unsafe sole audit trail ([OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/)). |
| Evidence/provenance store | W3C PROV bundle or versioned object store | Typed, resolvable references; content/version digests; ownership and retention metadata | Provenance can be valid yet partial, and a mutable URL can change after the receipt is signed ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/)). |
| Verification service | Domain reconciler, test result predicate, policy engine, or human approval system | Verifier identity/revision, criterion, subject, method, result, coverage/uncertainty, evidence | A naked `passed` field conceals who checked what and against which expectation. |
| Integrity service | KMS/HSM-backed key, DSSE/in-toto envelope, Sigstore-style verification bundle | Signature, signing identity, trusted time, certificate/key chain, optional inclusion proof | Signing cannot establish factual correctness, and key lifecycle remains a separate trust problem ([in-toto envelope](https://github.com/in-toto/attestation/blob/main/spec/v1/envelope.md)). |
| Schema/profile registry | URI-addressed core schema plus domain/risk profiles | Schema version, semantic profile, compatibility and migration rules | Parsers need the historical meaning of fields, not only syntactic validity. OpenTelemetry's current version-selection work illustrates the operational need to pin semantic-convention versions ([OpenTelemetry version selection](https://opentelemetry.io/docs/specs/semconv/configuration/version-selection/)). |
| Privacy and records policy | GDPR and sector-specific retention rules | Purpose, access class, minimization decision, retention deadline/legal hold, erasure/tombstone behavior | Personal data must be limited to what is necessary and not kept longer than its purpose requires; legal retention and erasure can conflict ([European Commission GDPR principles](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en), [GDPR Article 17](https://eur-lex.europa.eu/legal-content/EN/TXT/?qid=1618398943851&uri=CELEX%3A32016R0679)). |

No special hardware is inherently required for a low-risk receipt. Stronger tiers may require an HSM/KMS, trusted execution boundary, write-once storage, or independent transparency monitor, but adding these only hardens particular claims. Capital and labour are required for schema governance, policy mapping, key rotation, evidence retention, access reviews, verifier maintenance, incident response, and migration; those are the ownership costs the prototype must measure.

## Internals where most coverage waves hands

### 1. A receipt sits between six adjacent record types

| Record type | Primary question | Typical shape | Authority | What it contributes | Why it is not the receipt |
|---|---|---|---|---|---|
| Application log | What message/event did this component emit? | Timestamped records, often local and unstructured | Emitting component | Errors and operational detail | May be incomplete, verbose, mutable, and weakly correlated. |
| Distributed trace | Where did this request travel, and how long did operations take? | Trace of parent/child spans | Instrumented services/collector | Causality, latency, tool/model calls | Observes execution; does not define business authority, committed state, or verification. |
| Audit trail | Which security/domain-relevant action occurred under which identity? | Chronological domain events | Domain/control-plane system | Authoritative actor/action/resource facts | Usually domain-specific and not a compact cross-domain task summary. |
| Provenance | Which entities, activities, and agents influenced this artifact/result? | Graph or bundle | One or more provenance asserters | Derivation, attribution, delegation | Broad interchange model; may be partial and does not prescribe a task verdict. |
| Attestation | Who asserts which typed claim about which immutable subject? | Signed statement/predicate/envelope | Identified signer/control plane | Integrity, subject binding, machine policy input | A receipt contains several claim classes and references; a valid attestation is still only an authenticated claim. |
| Event-sourced record | What sequence of domain events constitutes current state? | Append-only event stream and projections | Domain event store | Replayable authoritative history | Heavy, domain-owned system of record; the receipt should be a projection over it. |
| **Agent receipt** | What completed/stopped task occurred, under whose exercised authority, with what effects and independent checks? | Compact signed projection plus typed pointers | Receipt service drawing from authoritative producers | Cross-domain review, handoff, portability, and discovery | It deliberately delegates detail and authoritative truth to the five systems above. |

OpenTelemetry defines common names and attributes so telemetry can be correlated across platforms; W3C PROV defines portable provenance semantics; in-toto defines authenticated metadata for policy engines; C2PA demonstrates signed provenance manifests; and event sourcing makes events the source of truth ([OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/), [W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md), [C2PA 2.2 specification](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html), [Martin Fowler on Event Sourcing](https://www.martinfowler.com/eaaDev/EventSourcing.html)). The receipt should compose those ideas rather than rename any one of them.

### 2. Causality and authority are different graphs

A trace parent answers “which call led to this call.” A delegation edge answers “which actor exercised authority on behalf of which principal.” A provenance edge answers “which entity or activity influenced this result.” These graphs overlap, but collapsing them creates false attribution: the service that technically called a payment API may differ from the sub-agent that selected the action, the human who delegated authority, and the policy engine that allowed it.

A robust receipt therefore carries separate typed edges:

```yaml
caused_by: action:plan-step-7
acted_by: workload:invoice-agent@sha256:...
on_behalf_of: principal:user-123
authorized_by: authz-decision:8f4...
delegated_from: action:parent-agent-call-2
effect: ledger-event:pay_8472
```

RFC 8693 can express an actor chain in a token, W3C PROV can express `actedOnBehalfOf`, and A2A can carry task/artifact relations; none by itself captures the policy snapshot and committed domain effect. This is also why the receipt should record the authority decision reference at the moment each privileged action occurs, rather than infer permission later from current roles ([RFC 8693](https://www.rfc-editor.org/info/rfc8693/), [W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [A2A protocol specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)).

### 3. Integrity is a chain of producers, not one final signature

Signing only the final YAML proves that a particular key signed those bytes. It does not prove that the tool committed an effect, that the assembler copied the right event, or that the verifier was independent. SLSA's threat model is explicit: provenance produced inside an adversary-controlled worker can contain false values, so stronger levels move provenance generation and signing into a trusted control plane ([SLSA threats and mitigations](https://slsa.dev/spec/v1.1/threats)).

The safer design uses claims from different producers:

1. The identity/policy system authenticates the exercised authorization decision.
2. Each domain system supplies an immutable event/resource version or signed response.
3. The verifier signs a result bound to the exact subjects checked.
4. The receipt service signs the projection and its evidence digests.
5. An optional transparency service supplies inclusion and consistency proofs.

AWS CloudTrail illustrates two subtleties. It hashes each log file, chains hourly digest files, and signs the digest, allowing later detection of modification or deletion; merely enabling delivery does not perform validation, and disabling validation breaks the digest chain ([AWS CloudTrail integrity validation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-intro.html), [AWS CloudTrail digest structure](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-digest-file-structure.html)). Certificate Transparency further shows that append-only Merkle proofs make omission/equivocation detectable only when clients or independent monitors actually compare views; a log can still attempt a split view ([RFC 9162](https://www.rfc-editor.org/rfc/rfc9162.html)).

Thus “signed,” “tamper-evident,” “independently witnessed,” and “factually verified” must be separate receipt fields.

### 4. Evidence pointers need a resolution and decay contract

An evidence pointer needs at least `uri`, `media_type`, `owner`, `version_or_digest`, `captured_at`, `access_class`, `retention_until`, and `availability` semantics. Stripe, for example, states that it guarantees retrieval of Event objects through the API for 30 days; an opaque `evt_...` in a receipt retained longer is not durable evidence unless the owning organization preserves an authorized copy or alternate domain record ([Stripe Events API](https://docs.stripe.com/api/events)).

Portability means a receiving system can understand the reference and verify subject identity without requiring the original receipt vendor. It does **not** mean every consumer gets the underlying sensitive data. A useful export therefore separates:

- Public/portable core metadata.
- Organization-private resolvers and access-control policy.
- Evidence digests or commitments that can remain after content deletion where lawful.
- Optional encrypted evidence packages for authorized transfer.
- A tombstone that says evidence was deleted, by which policy/authority, and when, without retaining the deleted personal content.

Sigstore's bundle format is a helpful model for “verification later”: it packages signature content, certificate/key material, transparency entry, and trusted timestamp so verification need not depend on a currently valid short-lived certificate ([Sigstore bundle format](https://docs.sigstore.dev/about/bundle/)). Its public transparency design is not automatically suitable for agent receipts containing personal or confidential facts; transparency should usually hold a minimal commitment or receipt digest, not the receipt body.

### 5. Redaction and retention must be designed before signing

Operational tracing naturally captures the fields most likely to be sensitive: prompts, retrieved documents, tool arguments, tool results, credentials, personal identities, and business records. OpenTelemetry marks GenAI tool arguments/results as potentially sensitive; the OpenAI Agents SDK records model and function input/output data by default unless sensitive-data capture is disabled, and tracing is unavailable under its Zero Data Retention policy ([OpenTelemetry GenAI attributes](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/), [OpenAI Agents SDK tracing](https://openai.github.io/openai-agents-python/tracing/)). Those vendor defaults are evidence that a receipt cannot safely be generated by serializing “whatever the trace contains.”

Redact/tokenize **before** producing the portable signed view, while preserving a digest and an access-controlled reference to any separately retained evidence. C2PA supports a declaration that assertions were redacted, which is preferable to silent omission, but a receipt profile also needs to state the redaction authority and whether the omitted claim was required for the review being attempted ([C2PA specification](https://c2pa.org/specifications/specifications/1.0/specs/C2PA_Specification.html)).

Retention is a per-field-class decision. Identity/effect metadata, raw prompts, model outputs, retrieved evidence, and cryptographic verification material may have different legal bases and useful lives. GDPR's purpose limitation, data minimization, storage limitation, and erasure rules prevent “auditability” from being a blanket reason to preserve everything forever, while sector record-keeping duties may require particular facts to remain ([European Commission GDPR principles](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en), [European Commission on erasure exceptions](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/dealing-requests-individuals/do-we-always-have-delete-personal-data-if-person-asks_en)).

### 6. Schema evolution and stochastic verification need explicit semantics

Every receipt must name both a syntactic schema version and a semantic profile URI. New optional fields are usually backward-compatible; changing the meaning of `reversible`, `cost`, `agent`, or `passed` is not. in-toto illustrates a workable rule: backward-compatible semantic updates increment minor versions, while meaning changes create a new major Statement type URI ([in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md)). OpenTelemetry's release history also demonstrates that still-developing GenAI conventions can make breaking changes, including agent and tool span semantics ([OpenTelemetry semantic-conventions releases](https://github.com/open-telemetry/semantic-conventions/releases)).

Do not promise byte-for-byte replay of an agent. Even deterministic ML libraries warn that complete reproducibility is not guaranteed across releases, commits, devices, or platforms, including identical seeds across CPU and GPU ([PyTorch reproducibility](https://docs.pytorch.org/docs/stable/notes/randomness)). For agent tasks, independent verification should target claims and effects:

- Can the cited input versions still be resolved?
- Does the result contain the required evidence?
- Did the domain system commit the named effects?
- Was the exercised authority valid at action time?
- Do deterministic invariants and business rules pass?
- Can a fresh agent reach a materially equivalent conclusion within a defined tolerance?

The receipt can preserve model identifier, parameters, seed when available, tool versions, environment, and input digests to support diagnosis. It should label replay as `exact`, `environment-bounded`, `semantic`, `effect-only`, or `not_possible`; a Boolean `reproducible` overclaims.

## Failure modes

| Failure mode | How it breaks the receipt | Historical example | Design response |
|---|---|---|---|
| **The producer or signing boundary is compromised** | A perfectly valid signature authenticates fabricated facts. | In the SolarWinds compromise disclosed on 2020-12-13, malicious behavior was inserted into released Orion software; CISA identified affected versions released during the preceding months ([CISA SolarWinds alert](https://www.cisa.gov/news-events/alerts/2020/12/13/active-exploitation-solarwinds-software)). | Generate effect claims in independent domain/control planes; bind subjects by digest; verify signer identity and policy expectations; do not let the model or its worker hold the only signing key. |
| **A trusted key is stolen or overpowered** | Receipts verify cryptographically while the key-holder's authority has been subverted. | Storm-0558 used a legacy Microsoft signing key during the intrusion detected on 2023-06-15; the 2024-03-20 CSRB report said Microsoft still did not know how or when the actor obtained it ([CISA/CSRB report](https://www.cisa.gov/sites/default/files/2024-04/CSRB_Review_of_the_Summer_2023_MEO_Intrusion_Final_508c.pdf)). | Use short-lived task-scoped signing identities, key separation, timestamps, revocation evidence, independent witnesses, and narrowly scoped verification policy. |
| **Coverage or retention gaps erase the causal chain** | The receipt points to only the visible tail of a task and silently omits earlier actions. | The CSRB found the Exchange compromise detected on 2023-06-15 may have started earlier than Microsoft's published date because standard log retention was 30 days; the intrusion was found by the U.S. Department of State rather than Microsoft ([CISA/CSRB report](https://www.cisa.gov/sites/default/files/2024-03/CSRB%20Review%20of%20the%20Summer%202023%20MEO%20Intrusion%20Final_508c.pdf)). | Record explicit coverage boundaries, sampling/drop counters, first/last observed action, retention horizon, and `evidence_incomplete`; preserve minimum effect facts in domain systems. |
| **There is plenty of telemetry but nobody converts it into a decision** | The record is exhaustive yet does not prevent or explain harm; `passed` becomes a dashboard status. | On 2012-08-01 Knight Capital generated 97 automated emails linked to a deployment failure, but personnel did not act; the SEC said the router sent more than 4 million orders and the firm lost more than $460 million ([SEC Knight Capital order summary](https://www.sec.gov/newsroom/press-releases/2013-222)). | Make verification criteria and owners explicit, gate high-risk completion on domain invariants, and distinguish “observed” from “reviewed” and “accepted.” |
| **Backup/evidence existence is confused with recoverability** | References exist but cannot restore the evidence or reconstruct state when reviewed. | On 2017-01-31 GitLab accidentally removed primary database data; periodic `pg_dump` backups were failing, snapshots were not enabled, and production modifications were irrecoverable ([GitLab postmortem](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)). | Test evidence restoration and resolver permissions; record last successful verification/restore; store durable minimum claims separately from volatile traces. |
| **A mutable or unpinned tool/input is treated as the one that ran** | A later reviewer resolves a current script, model alias, policy, or document that differs from execution time. | The Codecov Bash Uploader was altered without authorization beginning on 2021-01-31 and disclosed on 2021-04-15, exposing why a trusted URL or name is weaker than a verified digest ([CISA Codecov notice](https://content.govdelivery.com/accounts/USDHSCISA/bulletins/2d712c1), [Codecov postmortem](https://about.codecov.io/apr-2021-post-mortem/)). | Pin agent/tool/input digests, retain signer identity, and verify fetched content before use; a URL is metadata, not identity. |
| **Sensitive material leaks through evidence capture** | The receipt/trace becomes a credential or personal-data breach and may outlive the source system's access controls. | The FTC's 2018-04-12 revised Uber action described intruders using a plaintext cloud access key obtained through GitHub to download large volumes of user and driver data during an earlier breach ([FTC Uber breach action](https://www.ftc.gov/business-guidance/blog/2018/04/ftc-addresses-ubers-undisclosed-data-breach-new-proposed-order)). | Never store bearer tokens; allowlist fields; hash or tokenize sensitive arguments; run secret/PII detection before signing; encrypt evidence separately; attach purpose, access, and deletion policy. |
| **Partial work is flattened into success/failure** | A natural-language result succeeds while one effect commits, another fails, and compensation remains pending. | Knight Capital's incident on 2012-08-01 also shows why task-level success is insufficient: one of eight servers retained old code, producing inconsistent behavior under the same deployment ([SEC administrative order](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf)). | Record each attempted/committed effect and compensation state; include idempotency keys and points of no return; forbid `completed` while any high-risk effect is `failed_unknown`. |
| **Schema meaning drifts while old receipts still parse** | Consumers accept a familiar field but interpret it under newer semantics. | OpenTelemetry semantic conventions release `v1.41.0` on 2026-04-28 included a breaking GenAI change requiring the tool name for execute-tool span naming and split `invoke_agent` semantics across client/internal spans ([OpenTelemetry releases](https://github.com/open-telemetry/semantic-conventions/releases)). | Pin schema and profile URIs; publish compatibility rules; reject unknown required claims; retain old validators and migration fixtures; never silently reinterpret signed receipts. |
| **Replay is mistaken for proof of correctness** | A rerun differs because models, providers, hardware, retrieved data, or tools changed; identical output can also repeat the same flaw. | PyTorch's reproducibility note, created on 2018-09-11 and updated on 2025-10-03, says complete reproducibility is not guaranteed across releases, commits, platforms, or CPU/GPU even with identical seeds ([PyTorch reproducibility](https://docs.pytorch.org/docs/stable/notes/randomness)). | Verify inputs, authority, effects, evidence, and invariants; label replay strength; store uncertainty and evaluator coverage instead of a Boolean. |

These examples are precedents for the underlying record/integrity problems, not claims that each involved an AI-agent receipt. The mechanism is new packaging around old distributed-systems, security, privacy, and accountability failures.

## Constraints and ceilings

1. **A receipt cannot prove truth from a compromised observation boundary.** Hashes and signatures prove integrity and attribution relative to keys and captured bytes. C2PA states that trust starts from signer identity; SLSA requires hardening the producer because signed false provenance remains false ([C2PA 2.2 specification](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html), [SLSA threats and mitigations](https://slsa.dev/spec/v1.1/threats)). Independent domain confirmation is the ceiling-raiser, not more receipt fields.

2. **A portable core cannot encode every domain's correctness model.** A deployment, payment, medical recommendation, and hiring decision have different sources of truth, reversal semantics, and legal duties. The core should carry typed extension/profile URIs and verification claims; domain-native events remain authoritative.

3. **Distributed causality is only as complete as context propagation.** W3C Trace Context and OpenTelemetry provide a common carrier, but uninstrumented tools, external services, offline humans, message queues, and lost context create orphans ([W3C Trace Context](https://www.w3.org/TR/trace-context/), [OpenTelemetry context propagation](https://opentelemetry.io/uk/docs/concepts/context-propagation/)). The receipt must expose gaps rather than infer order from timestamps.

4. **Availability and integrity are different.** A digest can remain valid after the evidence is deleted; a resolvable record can be altered unless its version is pinned. SLSA explicitly excludes availability threats such as deleted code, artifact, or provenance ([SLSA threats and mitigations](https://slsa.dev/spec/v1.1/threats)). Portability therefore requires a retention/resolution contract, not only a URI.

5. **Irreversible effects stay irreversible.** A receipt can record an email sent, money transferred, data disclosed, or production outage; it cannot undo the physical, legal, or social consequence. Compensation may create a new correcting event but does not erase the original ([Microsoft Compensating Transaction pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/compensating-transaction)).

6. **Stochastic computation caps exact reproducibility.** Model identifiers, seeds, parameters, inputs, tool versions, and environment improve diagnosis but do not guarantee the same path or text across providers/releases/hardware ([PyTorch reproducibility](https://docs.pytorch.org/docs/stable/notes/randomness)). Effect reconciliation and semantic evaluation are often the honest target.

7. **Privacy limits completeness and permanence.** Raw prompts and tool I/O can be personal, privileged, copyrighted, secret, or security-sensitive. GDPR minimization, storage limitation, and erasure can conflict with indefinite cryptographic archives; public transparency logs are unsuitable for many receipt bodies ([European Commission GDPR principles](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en)).

8. **Review attention is finite.** Knight Capital's 97 unacted-on messages show that recording is not review. The minimum useful receipt is defined by a review decision and a measurable reconstruction task, not by the smallest byte count ([SEC Knight Capital order summary](https://www.sec.gov/newsroom/press-releases/2013-222)).

9. **Current AI-agent standards do not yet supply the whole artifact.** A2A standardizes agent-to-agent tasks/messages/artifacts; MCP standardizes agent-to-tool interaction and authorization; OpenTelemetry GenAI conventions standardize telemetry vocabulary; NIST's AI Agent Standards Initiative, launched on 2026-02-17, still frames identity, security, and interoperability as active work ([A2A protocol](https://a2a-protocol.org/latest/), [MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), [OpenTelemetry GenAI attributes](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/), [NIST AI Agent Standards Initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)). A receipt profile can compose them, but claiming an established universal “agent receipt standard” would be premature.

## Side effects

- **A new control plane and liability boundary.** The service deciding what enters the receipt can shape what the organization later considers to have happened. If it is vendor-owned, portability may be syntactic while trust, resolution, and verification remain locked in.
- **Surveillance pressure.** Capturing requester identity, prompts, retrieved material, tool calls, cost, and evaluator judgments can become employee performance monitoring or behavioural profiling. Data minimization must be enforced structurally, not left to an operator checkbox ([European Commission GDPR principles](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en)).
- **Security concentration.** Receipts become a map of identities, permissions, evidence locations, system topology, and privileged actions. A compromise may reveal how to attack the underlying systems even if raw evidence is absent. OWASP advises excluding or sanitizing sensitive data and protecting logs against unauthorized access, modification, and deletion ([OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)).
- **Checkbox trust.** A green signature or `verification: passed` may increase confidence more than warranted. Signer identity, claim subject, verifier independence, coverage, and unresolved effects must remain visible.
- **Behavioural adaptation and gaming.** Agents and teams may optimize for receipt fields that are measured while moving important judgment into unrecorded channels. Independent domain invariants and sampled human reconstruction tests reduce this incentive.
- **Storage and review work.** Even compact receipts create schema migrations, indexes, resolvers, key rotation, access reviews, legal holds, deletion workflows, and broken-link repair. This work must be counted against the repeated incident/audit work the receipt claims to remove.
- **Better organizational memory and exit.** A vendor-neutral core containing stable identifiers, subject/effect digests, typed evidence pointers, and verification material can let a future maintainer understand work after an agent platform changes. Sigstore bundles demonstrate the value of carrying later-verification material with the signed object ([Sigstore bundle format](https://docs.sigstore.dev/about/bundle/)).
- **A reusable policy interface.** Once effects and verifications are typed, organizations can automate rules such as “no production mutation without an approval and reconciled resource version” or “no payment task completes while compensation is pending.” This is leverage only if the common rule removes more repeated work than the receipt infrastructure creates.

## Plain-language analogy

An agent receipt is like the cover sheet on a shipment assembled from several warehouses: it says who ordered the shipment, which courier acted under which authorization, which sealed packages were picked up, which tracking records and inspection results prove delivery, what went missing or was returned, and where the detailed records live. The warehouses' own inventories and the courier's scans remain authoritative; the cover sheet makes the whole job reviewable without photocopying every shelf and camera recording. The analogy breaks because software agents can delegate dynamically, observe mutable information, make probabilistic choices, and cause effects that are only eventually consistent or irreversible. A signed cover sheet can also be honestly signed and still wrong if the warehouse, courier, inspector, or signing key is compromised.

## Source receipts

### Primary

- [W3C PROV-DM Recommendation](https://www.w3.org/TR/prov-dm/)
- [W3C PROV-AQ](https://www.w3.org/TR/prov-aq/)
- [W3C Trace Context Recommendation](https://www.w3.org/TR/trace-context/)
- [RFC 8693: OAuth 2.0 Token Exchange](https://www.rfc-editor.org/info/rfc8693/)
- [RFC 9162: Certificate Transparency Version 2.0](https://www.rfc-editor.org/rfc/rfc9162.html)
- [Regulation (EU) 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)
- [Regulation (EU) 2016/679](https://eur-lex.europa.eu/legal-content/EN/TXT/?qid=1618398943851&uri=CELEX%3A32016R0679)
- [European Commission: GDPR principles](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en)
- [European Commission: erasure and exceptions](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/dealing-requests-individuals/do-we-always-have-delete-personal-data-if-person-asks_en)
- [NIST: AI Agent Standards Initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)
- [NIST/NCCoE: Software and AI Agent Identity and Authorization concept paper](https://www.nccoe.nist.gov/sites/default/files/2026-02/accelerating-the-adoption-of-software-and-ai-agent-identity-and-authorization-concept-paper.pdf)
- [CISA/CSRB: Review of the Microsoft Exchange Online intrusion](https://www.cisa.gov/sites/default/files/2024-04/CSRB_Review_of_the_Summer_2023_MEO_Intrusion_Final_508c.pdf)
- [CISA: SolarWinds alert](https://www.cisa.gov/news-events/alerts/2020/12/13/active-exploitation-solarwinds-software)
- [CISA: Codecov compromise notice](https://content.govdelivery.com/accounts/USDHSCISA/bulletins/2d712c1)
- [SEC: Knight Capital administrative order](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf)
- [FTC: revised Uber breach action](https://www.ftc.gov/business-guidance/blog/2018/04/ftc-addresses-ubers-undisclosed-data-breach-new-proposed-order)

### Technical Docs

- [OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/)
- [OpenTelemetry GenAI attribute registry](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/)
- [OpenTelemetry context propagation](https://opentelemetry.io/uk/docs/concepts/context-propagation/)
- [OpenTelemetry semantic-convention version selection](https://opentelemetry.io/docs/specs/semconv/configuration/version-selection/)
- [OpenTelemetry semantic-conventions releases](https://github.com/open-telemetry/semantic-conventions/releases)
- [in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md)
- [in-toto Statement specification](https://github.com/in-toto/attestation/blob/main/spec/v1/statement.md)
- [in-toto Envelope specification](https://github.com/in-toto/attestation/blob/main/spec/v1/envelope.md)
- [in-toto predicate registry](https://github.com/in-toto/attestation/blob/main/spec/predicates/README.md)
- [SLSA terminology and verification model](https://slsa.dev/spec/v1.1/terminology)
- [SLSA build levels](https://slsa.dev/spec/v1.1/levels)
- [SLSA threats and mitigations](https://slsa.dev/spec/v1.1/threats)
- [DSSE specification](https://github.com/secure-systems-lab/dsse)
- [Sigstore Rekor](https://docs.sigstore.dev/logging/overview/)
- [Sigstore bundle format](https://docs.sigstore.dev/about/bundle/)
- [C2PA Technical Specification 2.2](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)
- [Model Context Protocol: tools](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)
- [Model Context Protocol: authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)
- [A2A protocol specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)
- [A2A protocol schema](https://github.com/a2aproject/A2A/blob/main/specification/a2a.proto)
- [A2A life of a task](https://a2aproject.github.io/A2A/latest/topics/life-of-a-task/)
- [Kubernetes auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)
- [AWS CloudTrail integrity validation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-intro.html)
- [AWS CloudTrail digest structure](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-digest-file-structure.html)
- [Stripe Events API](https://docs.stripe.com/api/events)
- [OpenAI Agents SDK tracing](https://openai.github.io/openai-agents-python/tracing/)
- [PyTorch reproducibility](https://docs.pytorch.org/docs/stable/notes/randomness)
- [OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)

### Filings

- [SEC: Knight Capital order summary, 2013-10-16](https://www.sec.gov/newsroom/press-releases/2013-222)
- [SEC: Knight Capital administrative proceeding](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf)
- [FTC: Uber revised complaint](https://www.ftc.gov/system/files/documents/cases/1523054_uber_technologies_revised_complaint_0.pdf)

### News

- [CISA: CSRB report landing page](https://www.cisa.gov/resources-tools/resources/cyber-safety-review-board-releases-report-microsoft-online-exchange-incident-summer-2023)
- [CISA: why critical security logs should be available, 2023-07-19](https://www.cisa.gov/news-events/news/when-tech-vendors-make-important-logging-info-available-free-everyone-wins)

### Practitioner Commentary

- [Martin Fowler: Event Sourcing, 2005-12-12](https://www.martinfowler.com/eaaDev/EventSourcing.html)
- [Microsoft: Event Sourcing pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)
- [Microsoft: Compensating Transaction pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/compensating-transaction)
- [GitLab: database outage postmortem, 2017-02-10](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)
- [Codecov: Bash Uploader postmortem](https://about.codecov.io/apr-2021-post-mortem/)

### Snowball pass

- **Round 1, already searched:** OpenTelemetry, W3C PROV, W3C Trace Context, in-toto, SLSA, C2PA, MCP, A2A, NIST, the EU AI Act, GDPR, AWS CloudTrail, Kubernetes, Stripe, OpenAI Agents SDK, PyTorch, Microsoft event sourcing/compensation, GitLab, CISA/CSRB, SEC/Knight Capital, FTC/Uber, SolarWinds, and Codecov. These entities each carry a load-bearing standard, mechanism, limitation, or incident in the analysis above.
- **Round 2, search-now and completed:** DSSE, Sigstore/Rekor, and Certificate Transparency were surfaced by in-toto/SLSA signing and were searched for envelope semantics, later verification, and append-only witnessing. The resulting primary specifications are incorporated in the integrity, retention, and source-receipt sections.
- **Background-only:** Individual OpenTelemetry vendors and agent-observability products were not made load-bearing because their proprietary schemas do not settle the portable mechanism. No second-round search produced a new unsearched entity essential to the mechanism.
