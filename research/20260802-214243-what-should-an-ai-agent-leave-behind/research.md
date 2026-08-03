# What Should an AI Agent Leave Behind After Completing a Task? — Research Dossier

**Question this dossier answers:** What is the smallest durable artifact that lets another person understand, verify, challenge, reverse, or reconstruct an AI agent's completed work without turning operational evidence into an expensive, invasive, or vendor-locked second system of record?

**Last updated:** 2026-08-02

## The Story in One Paragraph

The most defensible answer is not a transcript and not a self-declared `verification: passed`. An agent should leave a compact, versioned **evidence manifest** that identifies the task, principal and acting workload, authority actually exercised, immutable execution version, attempted and committed effects, independent checks, unresolved uncertainty, cost, reversibility, retention, and typed pointers to authoritative records. Beneath it, a trace preserves causal detail for diagnosis; beside it, domain systems and independent verifiers preserve the facts that establish what really changed. History supplies all the component ideas—event sourcing, audit logs, distributed tracing, W3C PROV, in-toto attestations, SLSA provenance, Sigstore bundles, and SCITT receipts—but no adopted standard yet combines them for one agent task. The central tension is that authenticity, completeness, truth, availability, intelligibility, and lawful retention are different properties. A signed receipt can still be false, a complete trace can still be unusable, and a useful debugging record can still become worker surveillance. The prototype is worth building only if it measurably reduces reconstruction or challenge work after counting capture, review, storage, privacy, migration, deletion, and evidence-decay costs.

## Cast

These are the institutions, projects, suppliers, and people who shape what a post-task artifact can prove and who can use it. They are not parties to one deployment.

1. **World Wide Web Consortium (W3C).** W3C PROV supplies a mature vocabulary for entities, activities, agents, derivation, attribution, and delegation; Trace Context supplies portable causal correlation. Neither supplies a complete authorization decision, signature policy, or domain verdict ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [W3C Trace Context](https://www.w3.org/TR/trace-context/)).
2. **IETF SCITT Working Group.** SCITT is the clearest “receipt” precedent: an issuer signs a statement and a transparency service proves registration. Its own threat model draws the crucial limit—dishonest issuers can still sign false assertions, so the receipt establishes attribution and accountability, not truth ([SCITT architecture](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html)).
3. **in-toto, SLSA, and Sigstore.** Together they demonstrate typed claims bound to immutable subjects, progressively stronger provenance producers, signed envelopes, transparency logs, and portable verification bundles. They are oriented mainly toward software supply chains, but their separation of payload, subject, producer, envelope, and verifier is directly reusable ([in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md), [SLSA levels](https://slsa.dev/spec/v1.1/levels), [Sigstore bundle format](https://docs.sigstore.dev/about/bundle/)).
4. **OpenTelemetry maintainers.** OpenTelemetry is the likely capture substrate for model, agent, tool, evaluation, cost, and trace correlation. Its GenAI conventions remain in development, and maintainers acknowledge that payloads may be enriched, redacted, truncated, or replaced by references as they move through a pipeline ([GenAI conventions](https://github.com/open-telemetry/semantic-conventions-genai), [issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)).
5. **Model Context Protocol (MCP) and Agent2Agent (A2A) projects.** MCP standardizes agent-to-tool interaction and authorization; its stable `2026-07-28` revision also adds Trace Context propagation, OpenTelemetry integration, extensions, Tasks, and conformance machinery. A2A models tasks, messages, lifecycle, and artifacts. Each contributes a layer, but neither currently defines a complete post-task accountability artifact ([MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), [MCP releases](https://github.com/modelcontextprotocol/modelcontextprotocol/releases), [A2A specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md)).
6. **National Institute of Standards and Technology (NIST).** NIST's log-management and AI risk work emphasizes lifecycle management, least privilege, audit protection, documented roles, monitoring, and independent review. Its AI Agent Standards Initiative, launched on 2026-02-17, makes identity, authorization, interoperability, and security active work rather than solved prerequisites ([NIST SP 800-92](https://csrc.nist.gov/pubs/sp/800/92/final), [NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/), [AI Agent Standards Initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)).
7. **European Parliament, Council, Commission, AI Office, and national authorities.** The EU AI Act creates risk-specific logging and retention duties, while GDPR constrains purpose, data volume, access, and retention. Later Commission guidance, sandboxes, monitoring templates, and standards will influence what evidence is operationally expected ([EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689), [GDPR](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679), [Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32026R1744)).
8. **Agent and observability suppliers such as OpenAI, LangSmith, Langfuse, and Arize Phoenix.** They supply traces, evaluators, viewers, storage, deletion, and export. They can reduce implementation work, but their schemas, retention tiers, URLs, and defaults can become the practical lock-in boundary ([OpenAI Agents tracing](https://github.com/openai/openai-agents-python/blob/main/docs/tracing.md), [LangSmith pricing](https://www.langchain.com/pricing), [Langfuse retention](https://langfuse.com/docs/administration/data-retention), [Phoenix](https://arize.com/docs/phoenix)).
9. **Identity providers, policy engines, tool gateways, and domain systems.** These are the authoritative producers for who acted, what was permitted, what call was made, whether an effect committed, and what resource version resulted. A generic receipt should project their facts rather than replace their logs.
10. **Ordinary application engineers, SREs, and incident responders.** They propagate context, instrument tools, interpret traces, repair broken evidence links, and bear on-call and schema-migration costs. Public community reports show real demand for intermediate state and tool effects, but no representative measurement of time saved ([OpenTelemetry issue #327](https://github.com/open-telemetry/semantic-conventions/issues/327), [r/LocalLLaMA debugging discussion](https://www.reddit.com/r/LocalLLaMA/comments/1sho0ah/how_are_people_actually_debugging_bad_outputs_in/)).
11. **Security, privacy, records, legal, audit, and compliance teams.** They decide trust boundaries, access, retention, legal hold, deletion, sampling, and whether an agent-authored claim is acceptable. A receipt creates continuing work for all of them.
12. **Workers, customers, patients, applicants, citizens, and others affected or incidentally recorded.** They bear consequences and privacy risk. Their need is often a comprehensible explanation and correction path, not raw operational telemetry; the AI Act explanation right and GDPR access right are bounded and different ([AI Act Article 86](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689), [GDPR Article 15](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679)).

## Timeline

| Date | Event | What it adds to this exploration |
|---|---|---|
| **2005-12-12** | Martin Fowler describes [Event Sourcing](https://www.martinfowler.com/eaaDev/EventSourcing.html). | An authoritative event stream can reconstruct how state changed; a compact receipt is only a projection over it. |
| **2006-09-13** | NIST publishes [SP 800-92](https://csrc.nist.gov/pubs/sp/800/92/final). | Logging is a full lifecycle of generation, transport, storage, analysis, access, retention, and disposal—not a file-writing feature. |
| **2011-11-15** | Michael Nygard publishes the [Architecture Decision Record pattern](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions). | A short artifact can preserve context, decision, and consequences for future maintainers, but it is not execution evidence. |
| **2012-08-01** | Knight Capital's failed deployment generates 97 automated messages; the router sends more than four million orders and the firm loses more than USD 460 million ([SEC](https://www.sec.gov/newsroom/press-releases/2013-222)). | Evidence that nobody converts into a decision does not create control; one server retaining old code also exposes partial-state semantics. |
| **2013-04-30** | W3C publishes its [PROV overview](https://www.w3.org/TR/2013/NOTE-prov-overview-20130430/). | Portable provenance can connect activities, agents, entities, delegation, use, and derivation across systems. |
| **2017-01-31** | GitLab loses production database data while several expected backup mechanisms prove ineffective ([postmortem](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)). | The existence of a reference or backup process does not prove later recoverability; evidence restoration must be tested. |
| **2017-04-11** | in-toto specification v0.9 is published ([specification](https://github.com/in-toto/docs/blob/master/in-toto-spec.md)). | Signed link metadata can bind authorized actors, commands, materials, and products to planned supply-chain steps. |
| **2018-03-23** | *Datasheets for Datasets* is posted ([paper](https://arxiv.org/abs/1803.09010)). | Compact structured documentation becomes an AI accountability pattern, though at dataset rather than task level. |
| **2018-10-05** | *Model Cards for Model Reporting* is posted ([paper](https://arxiv.org/abs/1810.03993)). | Intended use, evaluation conditions, performance, and limitations can accompany an AI artifact; again, this is lifecycle documentation rather than a task record. |
| **2021-11-23** | W3C publishes [Trace Context](https://www.w3.org/TR/trace-context/). | Cross-vendor request correlation becomes a standard carrier, but it does not define the business task, authority, outcome, or verification. |
| **2023-09-15** | OpenTelemetry issue [#327](https://github.com/open-telemetry/semantic-conventions/issues/327) proposes modern AI semantic conventions. | Agent and LLM work begins to enter ordinary distributed tracing rather than requiring an entirely separate transport. |
| **2024-07-12** | Regulation (EU) 2024/1689 is published ([EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)). | Covered high-risk systems gain explicit logging and retention requirements, without a universal agent-receipt schema. |
| **2025-03-06** | OpenTelemetry publishes an [AI-agent observability proposal](https://opentelemetry.io/blog/2025/ai-agent-observability/). | Agent, tool, and model telemetry begins converging on shared conventions, still marked as evolving. |
| **2026-02-17** | NIST announces its [AI Agent Standards Initiative](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure). | Institutional focus shifts to agent identity, authorization, interoperability, and security evaluation. |
| **2026-04-13** | An individual Internet-Draft proposes an [AI Agent Execution Profile of SCITT](https://datatracker.ietf.org/doc/html/draft-emirdag-scitt-ai-agent-execution-00). | The closest direct precedent proposes interaction records, independent custody, sequence completeness, redaction receipts, and evidence receipts; it is not adopted or validated. |
| **2026-05-29** | MCP publishes the release candidate for its `2026-07-28` revision ([revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [release repository](https://github.com/modelcontextprotocol/modelcontextprotocol/releases)). | The candidate introduces Trace Context propagation, OpenTelemetry integration, extensions, Tasks, conformance, and a deprecation lifecycle. |
| **2026-07-28** | MCP publishes the stable `2026-07-28` revision ([release repository](https://github.com/modelcontextprotocol/modelcontextprotocol/releases)). | Stable transport and conformance machinery strengthens cross-runtime plumbing, but still does not bind exercised authority, committed domain effects, and independent verification into one accountability receipt. |

## Geography and Jurisdiction

The artifact's lawful and useful shape depends on the system's role, data, sector, and location. Nothing in this dossier establishes that the hypothetical agent is in a regulated category.

| Context | Evidence requirement or constraint | Practical asymmetry |
|---|---|---|
| **EU/EEA when the receipt contains personal data** | GDPR requires a specified purpose, minimisation, accuracy, storage limitation, security, access, and conditional erasure ([GDPR Articles 5, 15, and 17](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679)). | “Keep it for accountability” does not justify capturing every prompt forever. A digest can remain useful after lawful deletion, but may no longer make the evidence available. |
| **EU Annex III high-risk AI** | Providers and deployers must retain automatically generated logs under their control for at least six months, subject to other law; revised application begins **2027-12-02** ([AI Act Articles 12, 19, and 26](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689), [Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32026R1744)). | The floor applies to covered high-risk systems, not every agent call; a portable summary does not automatically satisfy the underlying logging duty. |
| **EU Annex I product-embedded high-risk AI** | Product and AI conformity duties interact; revised high-risk application begins **2028-08-02** ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32026R1744)). | Sector records may be stronger and longer-lived than a generic agent receipt; duplication may add liability rather than leverage. |
| **EU workplace** | Future covered workplace systems require worker and representative notice, while GDPR Article 88 permits additional national or collective safeguards ([AI Act Article 26(7)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689), [GDPR Article 88](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679)). | The same record that helps debug an agent can become a searchable performance dossier under an employment power imbalance. |
| **United Kingdom workplace** | Monitoring must be lawful, fair, transparent, necessary, and proportionate; high-risk monitoring may need a DPIA ([ICO guidance](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/employment/monitoring-workers/)). | UK guidance is separate from EU law and is flagged for review; access and retention must be checked against the current UK regime. |
| **United States, general private sector** | NIST AI RMF is voluntary and risk-based; no general federal agent-receipt mandate was identified ([NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/)). | State privacy, employment, contract, discovery, and consumer-protection rules may still apply; retention is not one national default. |
| **US employment records** | Covered employers generally retain personnel and employment records for one year, with longer preservation after a charge ([EEOC](https://www.eeoc.gov/employers/recordkeeping-requirements)). | Whether a receipt is an employment record depends on its content and use, not on the word “agent.” |
| **US HIPAA scope** | Covered entities and business associates need mechanisms to record and examine activity in systems containing or using ePHI ([HHS](https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html)). | A security audit log, designated record set, patient-access response, and agent receipt are not automatically the same record. |
| **US broker-dealer records** | Rule 17a-4's audit-trail alternative requires complete time-stamped history for covered electronic records, including creation, modification, deletion, identity where applicable, and recreation ([SEC](https://www.sec.gov/investment/amendments-electronic-recordkeeping-requirements-broker-dealers)). | A generic receipt cannot replace a regulated source record unless it actually meets the rule. |
| **US credit decisions using consumer reports** | FCRA adverse-action duties can require notice and dispute/access routes ([FTC](https://www.ftc.gov/business-guidance/resources/using-consumer-reports-credit-decisions-what-know-about-adverse-action-risk-based-pricing-notices)). | A statutory explanation or notice right does not imply access to raw agent traces. |

## By the Numbers

No comparable public evidence establishes an **average** receipt size, cost, review time, storage burden, incident saving, or engineer maintenance burden. Those values remain **Unknown**. The numbers below are bounded facts or product reference points, not a market benchmark.

| Number | What it shows | What it does not show |
|---:|---|---|
| **5 of 20** agencies had comprehensive information for every reported AI use case; the other **15 of 20** had incomplete or inaccurate data ([GAO-24-105980, 2023-12-12](https://www.gao.gov/products/gao-24-105980)). | A formal, structured inventory can standardize incomplete reporting unless ownership and quality checks work. | The likely completeness rate of agent receipts. |
| **164** proof-of-concept kernel exploits were examined in OMNILOG research; one prior design could take **15 ms** to protect logs while a naive attack took about **5 ms** to tamper with them ([USENIX paper](https://www.usenix.org/system/files/usenixsecurity23-gandhi.pdf)). | Integrity depends on capture timing and boundary, not only the final signature. | Performance or security of an agent-specific receipt implementation. |
| **97** automated messages were generated during Knight Capital's incident; the system sent more than **4 million** orders and the firm lost more than **USD 460 million** ([SEC](https://www.sec.gov/newsroom/press-releases/2013-222)). | Recorded warnings without decision ownership and action are not control. | A causal estimate of how much a receipt would have saved. |
| About **90%** of logs submitted to Twitter's earlier central logging platform were discarded by a rate limiter; its later platform ingested **4×** more data ([Twitter engineering](https://blog.x.com/engineering/en_us/topics/infrastructure/2021/logging-at-twitter-updated)). | A trace reference needs loss, sampling, and retention disclosure; retrieval capability matters with volume. | That four times more data produced four times more trust. |
| **14 days** base and **180 days** extended trace retention appear in LangSmith's public offering ([pricing](https://www.langchain.com/pricing)). | Retention is a monetized product decision. | A legal or industry-standard retention period. |
| **USD 39 per seat/month** is the published LangSmith Plus seat price before usage charges ([pricing](https://www.langchain.com/pricing)). | The receipt's evidence ecosystem has supplier and usage costs. | Total implementation, review, migration, privacy, or deletion cost. |
| **At least 6 months** is the future EU high-risk log floor where the relevant logs are under provider or deployer control ([AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)). | Some covered systems need durable records. | That every receipt should live for six months or contain every raw log field. |

The prototype's `cost: 0.18` should be treated only as illustrative execution cost. A defensible ledger must include generation, ingestion, storage, redaction, access control, review, schema governance, migration, deletion, evidence repair, and false-confidence costs.

## How It Actually Works

### The three-layer record

| Layer | Question it answers | Appropriate contents | What it cannot establish alone |
|---|---|---|---|
| **Receipt / evidence manifest** | What task occurred, under whose exercised authority, with what outcome, effects, checks, gaps, and evidence pointers? | Compact versioned projection for a named reader and review decision | Complete execution history, hidden actions, model-internal reasoning, or correctness |
| **Trace** | How did execution travel across models, agents, tools, retries, and services? | Spans, timings, tool/model calls, errors, evaluation events, causal context | Committed domain state, lawful authority, capture completeness, or truth |
| **Attestation and domain evidence** | Who asserted which claim about which immutable subject, and what did the owning system record? | Signed claims, policy decisions, transaction or resource events, verifier results, inclusion proofs | Human comprehensibility or availability forever |

This separation is the synthesis's most important design choice. W3C PROV supplies portable relationships, OpenTelemetry supplies transport and correlation, in-toto and DSSE supply typed authenticated claims, domain systems supply effect semantics, and SCITT can supply independent registration. None should be renamed “the receipt” and expected to do every job ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [OpenTelemetry](https://opentelemetry.io/docs/what-is-opentelemetry/), [in-toto](https://github.com/in-toto/attestation/blob/main/spec/README.md), [SCITT](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html)).

### End-to-end walkthrough

1. **Open a durable task boundary before work begins.** The orchestrator creates a stable task and receipt identifier, lifecycle state, schema/profile URI, start time, and trace context. This ensures failed, abandoned, timed-out, partial, and compensated work also leaves a terminal artifact. A2A's task lifecycle is a useful precedent ([A2A life of a task](https://a2aproject.github.io/A2A/latest/topics/life-of-a-task/)).
2. **Resolve who acts for whom and what is allowed now.** The identity and policy systems produce the principal, workload actor, resource audience, granted action, delegation chain, policy version, expiry, and approval reference. The receipt stores the exercised decision, never bearer credentials. OAuth Token Exchange distinguishes delegation from impersonation, while MCP forbids token passthrough to reduce confused-deputy risk ([RFC 8693](https://www.rfc-editor.org/info/rfc8693/), [MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)).
3. **Freeze execution identity.** Record immutable digests for the agent definition, code/build, instruction bundle, tool registry, guardrails, evaluators, and configuration actually used, plus provider-reported model identity. A friendly name or provider alias is not an executable identity; SLSA's separation of work definition, run details, subject digest, and producer trust is the precedent ([SLSA terminology](https://slsa.dev/spec/v1.1/terminology)).
4. **Let tools and domain systems record effects.** The tool gateway attaches task correlation and idempotency information; the payment ledger, source-control platform, database, cluster API, document store, or ticket system records its own authoritative transaction or resource event. The receipt keeps a typed reference, version, and digest rather than copying a weaker paraphrase ([Kubernetes auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/), [Stripe Events](https://docs.stripe.com/api/events)).
5. **Preserve three different graphs.** Trace edges express technical causality; delegation edges express authority; provenance edges express derivation. They overlap but cannot safely be collapsed. A service that technically calls an API may differ from the sub-agent that selected the action, the human principal, and the policy engine that authorized it ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [RFC 8693](https://www.rfc-editor.org/info/rfc8693/)).
6. **Resolve evidence without ingesting everything.** Evidence pointers need a URI, owner, immutable version or digest, media type, access class, captured time, retention horizon, and availability state. Mutable “latest” URLs are insufficient; a hash proves bytes, not meaning or availability. W3C PROV-AQ and in-toto subject binding supply parts of the pattern ([W3C PROV-AQ](https://www.w3.org/TR/prov-aq/), [in-toto Statement](https://github.com/in-toto/attestation/blob/main/spec/v1/statement.md)).
7. **Close every branch and effect.** Each attempted external action is marked `not_started`, `rejected`, `committed`, `failed_unknown`, `compensated`, `compensation_failed`, or `irreversible`. A task-level `completed` state is forbidden while a high-risk effect is unknown. Compensation is a new domain action and may not restore the original state ([Microsoft Compensating Transaction](https://learn.microsoft.com/en-us/azure/architecture/patterns/compensating-transaction)).
8. **Verify claims independently of the acting model.** A verifier binds its identity and revision, criterion or policy URI, exact subject/effect, method, result, time, coverage or uncertainty, and evidence. Domain reconciliation—confirming a ledger transaction, deployed image digest, or resource version—is stronger than asking another model whether the output looks correct ([in-toto predicate registry](https://github.com/in-toto/attestation/blob/main/spec/predicates/README.md), [SLSA threats](https://slsa.dev/spec/v1.1/threats)).
9. **Project a risk-tiered, audience-specific receipt.** A read-only summary might require input versions, output digest, trace pointer, uncertainty, and evaluation. A production change adds exact before/after resource versions, approval, exercised authority, rollback or compensation, and a domain check. A payment adds ledger and reconciliation events. “Minimal” is proportional, not universal.
10. **Redact before signing, then sign and preserve verification material.** Raw prompts, retrieved documents, tool arguments, tool results, identities, and credentials can be sensitive. The portable view should allowlist fields and retain controlled pointers or commitments. DSSE, Sigstore bundles, C2PA redaction patterns, and optional transparency registration can protect attribution and later verification, but not factual truth ([DSSE](https://github.com/secure-systems-lab/dsse), [Sigstore bundle](https://docs.sigstore.dev/about/bundle/), [C2PA 2.2](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)).
11. **Verify as a consumer, not as a viewer.** The consumer checks schema/profile support, signature and signing-time validity, expected issuer and authority, subject/effect digest matching, verifier independence, missing evidence, and policy. “Signature valid” remains one input, never the verdict.
12. **Expire deliberately and test restoration.** Receipt fields, raw traces, evidence, and cryptographic material can have different schedules. Deletion should leave a lawful tombstone where appropriate, while annual export, resolver, key, and evidence-restore tests determine whether portability survives the original platform.

### Failure modes and hard limits

- **Compromised producer:** a valid signature can authenticate fabricated facts. Stronger designs move effect claims and signing out of the agent worker into independent control and domain planes ([SLSA threats](https://slsa.dev/spec/v1.1/threats)).
- **Coverage gap:** Okta spent 14 days following the wrong event semantics because an attacker used a different access path; later log arrivals exposed further gaps ([Okta root-cause report](https://sec.okta.com/articles/2023/11/unauthorized-access-oktas-support-case-management-system-root-cause/)).
- **Volume without review:** the Storm-0558 inquiry showed that enhanced logs and custom rules enabled detection while few organizations analyzed the voluminous relevant log in depth ([CSRB report](https://www.cisa.gov/resources-tools/resources/CSRB-Review-Summer-2023-MEO-Intrusion)).
- **Evidence inaccessible to its subject:** the Post Office Horizon record shows that detailed audit data can exist while cost, quotas, system control, and access prevent the people implicated from challenging it ([Inquiry issues](https://www.gov.uk/government/publications/post-office-horizon-it-inquiry-2020/provisional-list-of-issues), [hearing transcript](https://postofficeinquiry.dracos.co.uk/phase-4/2023-11-17/)).
- **Transformation and loss:** an event can be sampled, redacted, truncated, enriched, post-processed, or replaced by a reference between producer and reviewer ([OpenTelemetry issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)).
- **Availability differs from integrity:** a digest can remain valid after evidence is deleted; SLSA explicitly excludes availability threats from its current protection model ([SLSA threats](https://slsa.dev/spec/v1.1/threats)).
- **Exact replay is often impossible:** model, provider, hardware, retrieved inputs, and tools can change; even PyTorch does not promise complete reproducibility across releases, commits, and platforms ([PyTorch](https://docs.pytorch.org/stable/notes/randomness.html)). The honest target is often semantic or effect-level verification.
- **Irreversible actions stay irreversible:** a receipt can document money sent, data disclosed, or an email delivered; it cannot undo the legal, physical, or social effect.
- **A trace is not model introspection:** observable inputs, outputs, and actions do not reveal the model's internal causal process. In high-stakes contexts, post-hoc explanations can mislead rather than repair an uninterpretable system ([Rudin](https://doi.org/10.1038/s42256-019-0048-x)).

## Money, Power, and Stakeholder Impact

### The real cost ledger

The receipt file may be tiny; the evidence system is not. Total ownership includes:

```text
net evidence value
= avoided reconstruction + avoided duplicate review + faster correction + safer exit
- capture + ingestion + retention + redaction + access control
- review labor + schema governance + key rotation + evidence repair
- migration + legal hold + deletion + privacy response + false confidence
```

No public evidence located supplies a comparable average for these terms. LangSmith's public retention tiers and seat price demonstrate monetization; Langfuse's retention documentation shows deletion can leave dangling references; a Langfuse issue shows physical cleanup across ClickHouse and MinIO can be asynchronous and operationally non-trivial ([LangSmith](https://www.langchain.com/pricing), [Langfuse retention](https://langfuse.com/docs/administration/data-retention), [Langfuse issue #8834](https://github.com/langfuse/langfuse/issues/8834)). Self-hosting removes some license cost while transferring operations to adopters.

### Where power moves

- **Who defines fields defines the visible history.** A vendor or central platform can determine which actions count, which omissions are normal, and which status becomes the enterprise truth.
- **Who captures and signs controls the assurance boundary.** No single team should define the schema, produce every fact, verify its own claims, control access, set retention, and delete the record.
- **Who can resolve evidence controls practical accountability.** A portable YAML file with vendor-only URLs is syntactically portable and institutionally locked in.
- **Who can inspect needs separate views.** Engineers need traces; security needs sensitive effects and identities; auditors need provenance and samples; affected people need comprehensible reasons, relevant personal data, and a remedy path. “Transparent” does not mean public.
- **Who pays is not always who benefits.** Application teams pay instrumentation costs; SREs and future maintainers may receive later savings; affected people bear privacy risk; vendors capture recurring storage and evaluation revenue.

### Stakeholder balance

| Stakeholder | Possible benefit | Risk or work imposed | Evidence needed before calling it leverage |
|---|---|---|---|
| Engineers and SREs | Faster reconstruction, shared handoff, less log archaeology | Instrumentation, schema churn, noisy traces, broken references | Controlled time-to-diagnosis and reconstruction-accuracy comparison |
| Security teams | Clear authority, tool, effect, and integrity evidence | New high-value datastore; attacker can forge or suppress self-reporting | Adversarial omission tests and reconciliation against independent systems |
| Privacy and records teams | Central purpose, source, access, and expiry inventory | More personal data, access requests, legal holds, deletion complexity | Field-level purpose, lawful basis, DPIA where needed, tested deletion |
| Auditors and compliance | Structured sampling and faster evidence retrieval | Checkbox compliance and excessive review queues | Samples tied to source records, named independent verifier, exceptions and remediation |
| Product owner | Safer delegation and cost attribution | Supplier, engineering, audit, and liability costs become explicit | Full cost ledger and repeated avoided work |
| Workers | Evidence of what automation did and where it failed | Performance surveillance, chilling effects, context collapse | Notice, representative involvement where applicable, secondary-use limits |
| Affected customers or citizens | Better explanation, correction, challenge, and preserved evidence | Sensitive disclosure; neat summary can conceal uncertainty | User-tested explanation and accessible human remedy |
| Vendors | Subscription, storage, evaluation, enterprise controls | Compatibility, export, security, and deletion obligations | Conformance, real exit test, disclosed retention and export behavior |
| Future maintainers | Organizational memory after people and platforms leave | Evidence decay, retired keys, unreadable schemas, inherited data | Annual restore, migration, resolver, and verification tests |

The likely design principle is therefore narrower than “agents should leave receipts”: **delegated work should leave proportionate, independently verifiable evidence for the people entitled to inspect it—and no more durable personal detail than its purpose requires.**

## Counter-Narratives

| Counter-narrative | Supporting evidence | What would falsify it | Whose interests the framing serves |
|---|---|---|---|
| **The problem is excessive authority, not missing documentation.** | NIST emphasizes least privilege, protected audit functions, and separation of privileged roles; a receipt after an over-privileged irreversible action does not reduce harm ([NIST SP 800-171r3](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/800-171r3/NIST.SP.800-171r3.html)). | Holding authority and reversibility constant, receipt users detect violations or reconstruct failures materially better than reviewers using domain records alone. | Security architects and domain-system owners; it resists a new centralized AI governance product. |
| **The problem is retrieval and review, not absent evidence.** | Storm-0558 evidence existed but required enhanced access, years of custom rules, and skilled analysis; Twitter's earlier logging platform suffered from query and ingestion limits ([CSRB](https://www.cisa.gov/resources-tools/resources/CSRB-Review-Summer-2023-MEO-Intrusion), [Twitter engineering](https://blog.x.com/engineering/en_us/topics/infrastructure/2021/logging-at-twitter-updated)). | A receipt outperforms tuned search and trace interfaces on time and accuracy rather than duplicating selected fields. | Observability and search vendors; operators who prefer improving existing infrastructure. |
| **The problem is integrity and custody.** | SCITT says signed assertions may still be false; OMNILOG shows audit records can be missed or altered before protection ([SCITT](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html), [OMNILOG](https://www.usenix.org/conference/usenixsecurity23/presentation/gandhi)). | Independent producers and witnesses make omitted or contradictory actions reliably detectable under a compromised agent runtime. | Auditors, security teams, transparency and signing suppliers. |
| **The problem is organizational accountability.** | GAO found incomplete or inaccurate information at 15 of 20 reviewed agency AI inventories despite a formal reporting requirement ([GAO](https://www.gao.gov/products/gao-24-105980)). | Receipts remain accurate, have named reviewers, and regularly trigger corrective action without a growing reconciliation bureaucracy. | Compliance and audit teams, but also managers who may prefer a visible artifact to deeper process change. |
| **The problem is domain verification, not agent explanation.** | Rudin warns that post-hoc explanation can legitimize an opaque high-stakes system, while domain records can directly establish whether a transaction or change occurred ([Nature Machine Intelligence](https://doi.org/10.1038/s42256-019-0048-x)). | Receipt explanations predict independently measured correctness and reveal defects that domain invariants miss. | Domain owners, affected people, and interpretable-system advocates; it weakens agent-platform claims. |
| **A generic receipt is a temporary category error.** | Product liability, cyber reporting, financial, health, employment, and infrastructure regimes care about products, decisions, harms, transactions, and records—not whether an LLM selected the call ([Product Liability Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj), [SEC](https://www.sec.gov/investment/amendments-electronic-recordkeeping-requirements-broker-dealers)). | Independent sectors and runtimes converge on a small cross-domain core that demonstrably reduces review and exit work. | Existing workflow and domain platforms; buyers wary of a new AI-specific control plane. |

The receipt framing especially benefits observability and agent-platform vendors, which can monetize ingestion, retention, evaluation, and access control; compliance functions, which gain a uniform sampling artifact; and managers, who gain visibility. Those interests do not invalidate the design, but they make independent effectiveness, privacy, and exit tests essential. On 2020-12-01, Microsoft announced the removal of individual names and activity from Productivity Score after feedback, demonstrating how organizational analytics can cross into worker monitoring even when that is not the product's stated intent ([Microsoft](https://www.microsoft.com/en-us/microsoft-365/blog/2020/12/01/our-commitment-to-privacy-in-microsoft-productivity-score/)).

## Community Pulse

This is a **small, self-selected qualitative sample**, not a survey and not evidence of prevalence. Handles and self-descriptions cannot establish identity or independence. Vendor founders, project authors, and promoters are retained because their experience is useful, but their stake is explicit.

### Full sentiment range

- **Strong support:** On **2024-05-19**, Reddit user `ZestyData` called monitoring every LLM call “invaluable” for reviewing sessions, intermediate steps, feedback, evaluation, and cost ([r/MachineLearning](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/)). This is a self-reported practitioner account, not measured outcome evidence.
- **Cautiously positive:** On **2024-02-17**, Hacker News user `lmeyerov` reported that adding the instrumentation to Jaeger and Prometheus “Works great!” after first asking how it would interoperate with their existing setup ([Hacker News](https://news.ycombinator.com/item?id=39371297)).
- **Sceptical but engaged:** On **2024-05-19**, Reddit user `Best-Association2369` wrote, “We've looked at dozens and at the end of the day just rolled a mini one for our needs” ([r/MachineLearning](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/)).
- **Hostile to the framing:** On **2024-02-14**, Hacker News user `Aqueous` wrote, “This is just normal system / service observability” and called the summary “misleading marketing” ([Hacker News](https://news.ycombinator.com/item?id=39371297)).
- **Asking for the concrete job:** On **2024-02-14**, `a_wild_dandan` asked, “What problem(s) does this solve?” and requested the backlog-ticket title the SDK would unlock ([Hacker News](https://news.ycombinator.com/item?id=39371297)).

### Platform receipts and practitioner takes

**Hacker News — category boundary.** On **2024-02-14**, `tracerbulletx` wrote, “Pretty sure this just structures logs for requests to common 3rd party LLM providers” ([thread](https://news.ycombinator.com/item?id=39371297)). The disagreement is substantive: telemetry around a model is useful, but does not expose internal reasoning or prove correctness.

**Reddit — buy, build small, or do without.** On **2024-05-19**, `WolvesOfAllStreets` wrote, “Instead, we created our own rules-based/naive functions (quicker, cost nothing)” ([thread](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/)). Other commenters argued that maintaining an internal platform would cost more at scale. The useful conclusion is not that one side wins: team size, traffic, risk, and repeated review work determine the boundary.

**GitHub — mundane interoperability failures.** On **2024-12-10**, OpenTelemetry contributor `lmolkova` wrote, “we cannot provide any guarantees that the body received is exactly the same as the body produced” because processing can enrich, redact, truncate, or externalize it ([issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)). On **2025-08-07**, OpenAI Agents SDK user `asmith26` reported, “unfortunately these seem to disable my MLflow tracer also?” before a processor reset resolved the conflict ([issue #1387](https://github.com/openai/openai-agents-python/issues/1387)). Portability fails in processors and defaults, not only schemas.

**X — builder demand, weak independent evidence.** On **2026-03-02**, `@kmeanskaran` posted, “Designed admin monitoring panel to detect data drift, agent observability, and logs” ([post](https://x.com/kmeanskaran/status/2028550567002509357)). On **2026-03-26**, `@RetardedNi85688` called spend controls and auditability “The boring stuff every developer needs” ([post](https://x.com/RetardedNi85688/status/2037210970309705914)). Both promote projects; they show seller-side attention when agents can spend money, not independent adoption or effectiveness.

**LinkedIn — professional framing.** On **2026-04-21**, Wesley Drone wrote that basic logging could not answer “why didn’t it work?” ([article](https://www.linkedin.com/pulse/agent-observability-required-were-yet-wesley-drone-03xac)). An undated reply under a later LangChain post argued that tracing predates the current agent-observability framing ([discussion](https://www.linkedin.com/posts/langchain_agent-observability-powers-agent-evaluation-activity-7427411112419119105-4jor)). The page exposes only a relative comment date, so this dissent is retained as an undated paraphrase and is not timeline evidence.

Three practitioner insights recur across platforms:

1. **A navigable timeline beats a complete dump.** Engineers want the first divergence, tool call, retrieval chunk, state change, latency, and cost—not an unreadable transcript ([r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1sho0ah/how_are_people_actually_debugging_bad_outputs_in/)).
2. **The evidence producer is part of the threat model.** One project author argues that application self-reporting misses filesystem and network effects visible below the process; replies distinguish semantic intent from independently observed effects. This is a project claim, not independent validation, but the distinction is important ([eBPF discussion](https://www.reddit.com/r/LocalLLaMA/comments/1r8yvu5/i_built_an_ebpf_tracer_to_monitor_ai_agents_the/)).
3. **Small teams optimize for maintenance, not maximum features.** Some build narrow tools; others buy because the continuing internal cost is higher. “Smallest useful” is an empirical ownership question.

The authentic joke is that AI observability vendors are selling shovels during a gold rush. On **2024-05-19**, Reddit user `Deto` described companies “trying to sell shovels,” while `ZestyData` joked, “Beginning to feel like this thread is product market research lmao” ([thread](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/)). No durable meme specific to agent receipts was found.

The most important confusions are:

- observable behavior versus internal model reasoning;
- a retained event versus a complete event;
- common syntax versus common semantics;
- a valid signature versus a true claim;
- reproducibility versus effect verification;
- debugging evidence versus harmless exhaust;
- affected-person explanation versus raw-log access.

Missing voices remain consequential: people affected by agent decisions; engineers outside public AI-tool communities and outside English-speaking North America; worker representatives; accessibility and civil-society advocates; and records, privacy, support, and frontline compliance staff doing routine retrieval and deletion work. No public representative engineer survey or controlled comparison of receipt designs was found.

## Forward Calendar

Only enacted or officially published dates are included. Undated NIST, A2A, OpenTelemetry, and standards aspirations stay in the watch list rather than the calendar.

| Date | Milestone | Relevance |
|---|---|---|
| **2026-09-11** | Cyber Resilience Act vulnerability and severe-incident reporting begins; ENISA plans its Single Reporting Platform to be operational ([CRA](https://eur-lex.europa.eu/eli/reg/2024/2847/oj), [ENISA](https://www.enisa.europa.eu/topics/product-security-and-certification/single-reporting-platform-srp)). | Agent software in scope may need fast, correlated product/version and incident evidence; a receipt cannot replace the statutory report. |
| **2026-12-02** | Pre-existing generative-AI providers must take steps toward Article 50(2) machine-readable synthetic-content marking ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). | This is output provenance, not an action receipt; it favors domain profiles over one universal artifact. |
| **2026-12-09** | EU Member States must transpose the Product Liability Directive; it applies to later products ([Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj)). | Software liability and proportionate court-ordered evidence disclosure increase the value of comprehensible retained evidence without defining its format. |
| **2027-08-01** | Commission guidelines for Annex I high-risk systems are due ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). | Guidance may clarify whether existing sector records can avoid duplicate AI evidence. |
| **2027-08-02** | At least one operational AI regulatory sandbox per Member State and delegated acts on equivalent sector duties are due ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). | A venue to test risk-tiered evidence profiles and whether they create net value. |
| **2027-09-02** | Commission guidance and a voluntary template for high-risk post-market monitoring plans are due ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). | The template may define the downstream questions source systems and receipts must answer. |
| **2027-12-02** | Revised high-risk obligations for Article 6(2)/Annex III systems apply ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). | Employment, education, essential-service, law-enforcement, migration, and justice uses face stronger logging and monitoring demand. |
| **2027-12-11** | Cyber Resilience Act becomes generally applicable ([CRA](https://eur-lex.europa.eu/eli/reg/2024/2847/oj)). | Product identity, vulnerability handling, support periods, and conformity become part of evidence design. |
| **2028-01-28** | Existing notified bodies must apply for AI Act designation to assess relevant high-risk AI conformity ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). | Assessors may drive sector profiles before a horizontal receipt standard appears. |
| **2028-08-02** | Revised high-risk obligations for Article 6(1)/Annex I systems apply ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). | Physical products and safety functions make self-authored summaries least credible without domain and assessor evidence. |
| **2028-09-11** | Commission review of the CRA Single Reporting Platform is due ([CRA Article 70](https://eur-lex.europa.eu/eli/reg/2024/2847/oj)). | A public test of whether one evidence interface reduces duplicate work while protecting sensitive material. |

**MCP chronology:** the release candidate was published on **2026-05-29**, and the stable `2026-07-28` revision followed on **2026-07-28** ([revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [release repository](https://github.com/modelcontextprotocol/modelcontextprotocol/releases)). Finalization settles the protocol status of Trace Context, OpenTelemetry integration, extensions, Tasks, and conformance machinery; it does not create a complete accountability receipt.

## Scenarios

These are analytical estimates for the dominant market shape by **2028-08-02**, not measured probabilities. The point estimates sum to 100%.

### Base — Thin projections emerge, no universal standard

**Probability:** 45% point estimate, 35–55% band.

Organizations project a small task record over OpenTelemetry traces, A2A/MCP metadata, policy decisions, and domain events. A common core emerges inside firms or sectors, but semantics differ at the edges. This follows the existing division of labor among W3C PROV, OpenTelemetry, in-toto, MCP, and A2A. MCP's stable `2026-07-28` revision strengthens the transport and conformance foundation without settling the domain semantics ([W3C PROV](https://www.w3.org/TR/prov-dm/), [in-toto](https://github.com/in-toto/attestation/blob/main/spec/README.md), [MCP releases](https://github.com/modelcontextprotocol/modelcontextprotocol/releases)).

**Trigger:** by **2027-08-02**, two independent production-grade runtimes export a common task/effect/verifier core consumed by one open verifier without vendor translation. Failure moves probability toward the downside.

**Near-term indicators during the next 6–12 months:**

- MCP conformance cases expand from transport into correlation, task extensions, or receipt-like extensions.
- A2A's TCK validates task and artifact lifecycle across SDKs while leaving domain evidence in extensions.
- OpenTelemetry adds or stabilizes agent, tool, and evaluation relations while remaining telemetry rather than an audit standard.
- NIST guidance treats identity, delegated authority, and interoperable audit evidence as separate layers.
- EU implementation guidance favors references to authoritative sector records and tries to prevent duplicate stores.

### Upside — A portable signed receipt profile converges

**Probability:** 20% point estimate, 10–30% band.

A neutral project publishes a versioned predicate and public conformance tests. Two runtimes and two verifiers exchange receipts that bind outputs, exercised authority, committed effects, evidence expiry, and independent checks outside proprietary backends. Existing W3C PROV, in-toto, DSSE, and Sigstore pieces make this technically possible; MCP's stable extension machinery provides another integration route, while regulation or procurement would need to create demand ([in-toto](https://github.com/in-toto/attestation/blob/main/spec/README.md), [Sigstore](https://docs.sigstore.dev/about/bundle/), [MCP revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [MCP releases](https://github.com/modelcontextprotocol/modelcontextprotocol/releases)).

**Trigger:** by **2027-08-02**, two runtimes, two verifier implementations, and one real domain integration verify the same public test vector without producer-specific APIs. These counts are scenario thresholds, not market facts.

**Near-term indicators during the next 6–12 months:**

- A public schema defines partial completion, retries, delegation, external effects, evidence expiry, and independent verification—not only prompts, tools, and success.
- Public test vectors cover tampering, missing evidence, revoked identity, expired keys, and privacy-redacted receipts.
- A protocol adopts the schema as an optional extension while the envelope remains usable outside that protocol.
- Procurement or regulatory-sandbox documents request exportable, machine-verifiable post-task evidence.
- Developer tools render the same receipt from multiple frameworks and resolve domain-native records.

### Downside — Proprietary telemetry and compliance evidence swamp the receipt

**Probability:** 30% point estimate, 20–40% band.

Every platform offers trace viewers and “audit logs,” but exports lose semantics and evidence links. Privacy teams disable sensitive content; compliance teams build separate stores; reviewers keep reconstructing outcomes manually. OpenTelemetry's GenAI stabilization remains unconfirmed; MCP's stable `2026-07-28` revision delegates structured observability to OpenTelemetry; and A2A uses extensions. These are reasonable architectural choices that still leave no owner for the complete accountability boundary ([OpenTelemetry roadmap issue opened 2026-01-25](https://github.com/open-telemetry/semantic-conventions/issues/3330), [MCP revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [MCP releases](https://github.com/modelcontextprotocol/modelcontextprotocol/releases), [A2A roadmap](https://a2a-protocol.org/latest/roadmap/)).

**Trigger:** through **2027-08-02**, independent verifiers still cannot establish committed effects and exercised authority without platform-specific APIs. Routine neutral verification falsifies this case.

**Near-term indicators during the next 6–12 months:**

- Breaking or vendor-specific semantics continue around agents, workflows, tools, and evaluations.
- “Audit” products emphasize retention volume and dashboards rather than authenticity, effect reconciliation, or exit.
- Security and privacy teams disable content capture, leaving traces too sparse for reconstruction.
- Legal and compliance teams build evidence repositories separate from engineering telemetry.
- Practitioners continue reporting manual JSON logging, weak replay, storage cost, and difficulty separating model, retrieval, and tool failures ([agent debugging](https://www.reddit.com/r/LocalLLaMA/comments/1rgwyqi/agent_debugging_is_a_mess_am_i_the_only_one/), [RAG debugging](https://www.reddit.com/r/LocalLLaMA/comments/1sho0ah/how_are_people_actually_debugging_bad_outputs_in/)).

### Wildcard — Domain-native records make the generic receipt disappear

**Probability:** 5% point estimate, 1–10% band.

Buyers and regulators reject agent-authored summaries and require every action through domain gateways with identity, policy, idempotency, approval, and authoritative audit records. The portable artifact shrinks into a disposable list of signed domain references. Liability and sector rules already focus on effects and records rather than an “agent” category ([Product Liability Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj), [W3C PROV](https://www.w3.org/TR/prov-dm/)).

**Trigger:** by **2027-08-02**, two regulated sectors or major procurement frameworks explicitly reject self-authored agent summaries in favor of independently generated domain events and human-readable case views.

**Near-term indicators during the next 6–12 months:**

- Security designs move observation below the agent runtime or through mandatory tool gateways.
- Regulators and auditors request transaction, case, decision, or product records without agent-specific terminology.
- Agent frameworks become interchangeable callers behind existing workflow and audit systems.
- Receipts shrink to signed domain references and omit prompts, plans, chain-of-thought, and agent narration.
- Community discussion increasingly treats the source system as the only credible proof of an external effect.

## The 90-Day Signal

**On 2026-10-31, check whether a neutral standards or open-source project has published a machine-verifiable cross-vendor schema plus public test vectors binding all four of these elements: task identity, exercised authority, domain effect references, and an independent verifier result.**

Watch the [NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative), [MCP specification](https://github.com/modelcontextprotocol/modelcontextprotocol), [A2A extensions and TCK](https://a2a-protocol.org/latest/roadmap/), [OpenTelemetry GenAI conventions](https://github.com/open-telemetry/semantic-conventions-genai), and [in-toto predicate work](https://github.com/in-toto/attestation). A new dashboard, trace viewer, or vendor-only export does not satisfy the signal. The test must establish who acted under what authority, what effect actually committed, and who independently checked it.

## Tensions and Open Questions

1. **Receipt or manifest?** Does the word “receipt” imply payment-grade proof that a lossy index cannot supply? Would “evidence manifest” produce better reviewer expectations?
2. **Who is the reader and what decision must they make?** Operator diagnosis, security investigation, audit sampling, affected-person explanation, regulator inspection, and future migration require different views.
3. **What is the task boundary?** Long-running, recursive, event-driven, and multi-agent work may never have one clean “completion.” What terminal states and child receipts are required?
4. **Can omission be detected?** Which facts originate outside the agent runtime, and how are gaps, exporter failure, sampling, redaction, or uninstrumented paths exposed?
5. **What does `verification` mean?** Who verified what subject against which criterion, with what independence, coverage, and uncertainty? Can a result be `passed` while an effect remains `failed_unknown`?
6. **What does `reversible` mean?** Does it mean a rollback exists, was tested, completed, or merely has a compensating action? Which effects are physically, legally, or socially irreversible?
7. **What survives vendor exit?** Can another implementation understand the schema, verify historical signatures, resolve evidence, and enforce access after the original runtime, trace backend, and vendor are gone?
8. **How does evidence decay?** What happens when a URL changes, a trace expires, a key is retired, a policy version disappears, a verifier shuts down, or lawful deletion removes underlying content?
9. **How small is useful?** The correct measure is not bytes. It is review accuracy and time, resolvable-evidence rate, false confidence, privacy findings, maintenance work, and migration success.
10. **Does the record create leverage?** Will avoided incident, review, and audit work repeatedly exceed capture, review, retention, schema, access, migration, and deletion work?
11. **Does it preserve engineering freedom?** Can teams change agent frameworks, storage, identity, and verifier suppliers without losing operational history or adopting the format owner's control plane?
12. **How should privacy and evidence duties coexist?** Which facts can be digests or controlled references, which must be retained, which must be deleted, and who may challenge the decision?
13. **Can affected people use it?** Does a receipt lead to an understandable reason, responsible owner, correction process, and remedy—or merely to a protected dashboard they cannot access?
14. **What evidence would change the conclusion?** A blind test should compare authoritative domain records alone, raw traces, and trace-plus-receipt on reconstruction accuracy, review time, missed violations, and false confidence. A hostile test should attempt omission, equivocation, fabricated evidence, prompt injection into the receipt, revoked identity, and reference substitution.

The prototype should be tested immediately and again after deliberately replacing its trace backend, evidence location, verifier, and agent runtime. The second test is where portability, engineering freedom, and continuing leverage become observable.

## Receipts

### Primary

- [W3C PROV-DM Recommendation](https://www.w3.org/TR/prov-dm/) and [PROV-AQ](https://www.w3.org/TR/prov-aq/) — portable provenance and discovery.
- [W3C Trace Context](https://www.w3.org/TR/trace-context/) — cross-service correlation.
- [NIST SP 800-92](https://csrc.nist.gov/pubs/sp/800/92/final) and [NIST SP 800-171r3](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/800-171r3/NIST.SP.800-171r3.html) — logging lifecycle, least privilege, audit content, protection, and review.
- [NIST AI RMF](https://airc.nist.gov/airmf-resources/airmf/) and [AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative) — voluntary risk governance and active agent standards agenda.
- [IETF SCITT architecture](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html) — signed statements, transparency receipts, and residual issuer risk.
- [AI Agent Execution Profile of SCITT](https://datatracker.ietf.org/doc/html/draft-emirdag-scitt-ai-agent-execution-00) — direct but individual and unadopted agent-evidence proposal.
- [in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md), [Statement](https://github.com/in-toto/attestation/blob/main/spec/v1/statement.md), and [predicate registry](https://github.com/in-toto/attestation/blob/main/spec/predicates/README.md) — typed claims bound to immutable subjects.
- [SLSA v1.0 rationale](https://slsa.dev/spec/v1.0/whats-new), [levels](https://slsa.dev/spec/v1.1/levels), and [threats](https://slsa.dev/spec/v1.1/threats) — adoption through simplification and provenance trust boundaries.
- [DSSE](https://github.com/secure-systems-lab/dsse) and [Sigstore bundle format](https://docs.sigstore.dev/about/bundle/) — authenticated envelopes and later verification material.
- [OpenTelemetry GenAI conventions](https://github.com/open-telemetry/semantic-conventions-genai), [attributes](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/), and [releases](https://github.com/open-telemetry/semantic-conventions/releases) — evolving portable telemetry semantics.
- [MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), [A2A specification](https://github.com/a2aproject/A2A/blob/main/docs/specification.md), and [A2A roadmap](https://a2a-protocol.org/latest/roadmap/) — tool authorization, task lifecycle, artifacts, and future conformance work.
- [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689), [Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32026R1744), and [GDPR](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679) — current EU logging, delayed applicability, explanation, privacy, access, and retention framework.
- [Cyber Resilience Act](https://eur-lex.europa.eu/eli/reg/2024/2847/oj) and [Product Liability Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj) — incident reporting, product security, software liability, and evidence disclosure.
- [SEC Knight Capital order](https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf), [GAO-24-105980](https://www.gao.gov/products/gao-24-105980), and [FTC audit discussion](https://www.ftc.gov/system/files/ftc_gov/pdf/Combatting%20Online%20Harms%20Through%20Innovation%3B%20Federal%20Trade%20Commission%20Report%20to%20Congress.pdf) — operational alert failure, inventory completeness, and limits of non-independent audits.

### News

- [CISA, Storm-0558 CSRB report page](https://www.cisa.gov/resources-tools/resources/CSRB-Review-Summer-2023-MEO-Intrusion) — logging access, volume, custom analysis, and detection asymmetry.
- [CISA, why critical security logs should be free](https://www.cisa.gov/news-events/news/when-tech-vendors-make-important-logging-info-available-free-everyone-wins) — public-interest response to premium audit telemetry.
- [Microsoft logging expansion, 2023-07-19](https://www.microsoft.com/en-us/security/blog/2023/07/19/expanding-cloud-logging-to-give-customers-deeper-security-visibility/) — vendor response; useful but interested.
- [Microsoft Productivity Score privacy change, 2020-12-01](https://www.microsoft.com/en-us/microsoft-365/blog/2020/12/01/our-commitment-to-privacy-in-microsoft-productivity-score/) — removal of user names and individual activity after privacy feedback.
- [NIST announcement, 2026-02-17](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure) — launch context for the agent standards initiative.

### Expert

- [Fowler, *Event Sourcing*](https://www.martinfowler.com/eaaDev/EventSourcing.html) — authoritative event streams and projections.
- [Nygard, *Documenting Architecture Decisions*](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions) — compact rationale records.
- [Google, *Dapper*](https://research.google/pubs/dapper-a-large-scale-distributed-systems-tracing-infrastructure/) — distributed tracing, sampling, and developer utility.
- [Schneier and Kelsey, *Secure Audit Logs to Support Computer Forensics*](https://www.schneier.com/academic/archives/1999/05/secure_audit_logs_to.html) — cryptographic protection on untrusted machines.
- [Gandhi et al., OMNILOG](https://www.usenix.org/conference/usenixsecurity23/presentation/gandhi) — event-coverage and asynchronous-protection failures.
- [Rudin, *Stop explaining black box machine learning models…*](https://doi.org/10.1038/s42256-019-0048-x) — limits of post-hoc explanation in high-stakes decisions.
- [Gebru et al., *Datasheets for Datasets*](https://arxiv.org/abs/1803.09010) and [Mitchell et al., *Model Cards*](https://arxiv.org/abs/1810.03993) — compact structured AI documentation precedents.
- [GitLab database outage postmortem](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/) and [Okta support-system incident](https://sec.okta.com/articles/2023/11/unauthorized-access-oktas-support-case-management-system-root-cause/) — recoverability, coverage, and semantic gaps.

### Community

- [Hacker News OpenLLMetry discussion, 2024-02-14](https://news.ycombinator.com/item?id=39371297) — category, value, interoperability, price, and marketing dispute.
- [r/MachineLearning observability discussion, 2024-05-19](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/) — build-versus-buy and mixed production value.
- [r/LocalLLaMA agent debugging](https://www.reddit.com/r/LocalLLaMA/comments/1rgwyqi/agent_debugging_is_a_mess_am_i_the_only_one/), [RAG debugging](https://www.reddit.com/r/LocalLLaMA/comments/1sho0ah/how_are_people_actually_debugging_bad_outputs_in/), and [eBPF experiment](https://www.reddit.com/r/LocalLLaMA/comments/1r8yvu5/i_built_an_ebpf_tracer_to_monitor_ai_agents_the/) — timeline usability, retrieval context, replay, storage, and independent observation.
- [OpenTelemetry issue #327](https://github.com/open-telemetry/semantic-conventions/issues/327) and [issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651) — connected traces, event semantics, and transformation.
- [OpenAI Agents SDK issue #1387](https://github.com/openai/openai-agents-python/issues/1387) and [Langfuse issue #8834](https://github.com/langfuse/langfuse/issues/8834) — exporter interaction and deletion/cleanup work.
- [X: `@kmeanskaran`, 2026-03-02](https://x.com/kmeanskaran/status/2028550567002509357) and [X: `@RetardedNi85688`, 2026-03-26](https://x.com/RetardedNi85688/status/2037210970309705914) — promotional builder attention, not independent adoption evidence.
- [Wesley Drone, 2026-04-21](https://www.linkedin.com/pulse/agent-observability-required-were-yet-wesley-drone-03xac) and [LangChain LinkedIn discussion](https://www.linkedin.com/posts/langchain_agent-observability-powers-agent-evaluation-activity-7427411112419119105-4jor) — professional explanation and tracing-is-not-new counterpoint.

### Background

- [OpenAI Agents SDK tracing](https://github.com/openai/openai-agents-python/blob/main/docs/tracing.md), [LangSmith pricing](https://www.langchain.com/pricing), [Langfuse retention](https://langfuse.com/docs/administration/data-retention), and [Arize Phoenix](https://arize.com/docs/phoenix) — current supplier and open-source implementation context; not neutral comparative evidence.
- [Kubernetes auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/), [AWS CloudTrail integrity validation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-intro.html), and [Stripe Events](https://docs.stripe.com/api/events) — domain-native audit, integrity-chain, and evidence-retention precedents.
- [C2PA 2.2](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) — signed content provenance, trust, privacy, and redaction patterns.
- [Post Office Horizon Inquiry](https://www.gov.uk/government/groups/the-post-office-horizon-it-inquiry) — access, contestability, remote alteration, and audit-evidence cost precedent.

No conspiracy section is included because the source presents a technical design hypothesis, not a covert event or disputed official narrative. Manufacturing a hidden-hand frame would add noise rather than evidence.
