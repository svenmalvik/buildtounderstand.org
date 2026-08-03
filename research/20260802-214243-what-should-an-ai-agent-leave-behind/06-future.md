# Futures and second-order effects: what an agent receipt could become

## Forecasting frame

The most defensible forecast is not that a universal `agent-receipt.yaml` standard is about to appear. It is that several adjacent systems are converging on pieces of the problem while leaving a gap between them:

- MCP released the `2026-07-28` revision as a **release candidate on 2026-05-29**, then published the **stable revision on 2026-07-28**. The revision standardizes trace-context propagation, replaces MCP's structured-logging feature with OpenTelemetry integration, and adds extension and conformance machinery. Those are completed protocol changes, but they do not define a portable post-task accountability receipt ([MCP release-candidate explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [MCP releases](https://github.com/modelcontextprotocol/modelcontextprotocol/releases)).
- A2A has a task and artifact lifecycle and is building extensions, an inspector, and a Technology Compatibility Kit, but its published roadmap does not promise a portable post-task accountability record ([A2A roadmap](https://a2a-protocol.org/latest/roadmap/)).
- OpenTelemetry has agent, tool, evaluation, and model-call vocabulary, but the GenAI conventions remain in development; its roadmap issue, opened on **2026-01-25**, labels stabilization of a GenAI core as **unconfirmed**, not committed ([OpenTelemetry GenAI repository](https://github.com/open-telemetry/semantic-conventions-genai), [OpenTelemetry roadmap issue](https://github.com/open-telemetry/semantic-conventions/issues/3330)).
- NIST's AI Agent Standards Initiative explicitly targets interoperable protocols, identity, authentication, authorization, security evaluation, and voluntary guidance, but does not yet publish a receipt schema or a dated delivery schedule ([NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)).
- The EU regulatory stack is creating concrete reasons to preserve intelligible records: the AI Act includes record-keeping and post-market monitoring; the Cyber Resilience Act introduces mandatory vulnerability and incident reporting; and the Product Liability Directive covers software and permits courts to order disclosure of relevant evidence ([EU AI Act standardisation](https://digital-strategy.ec.europa.eu/en/policies/ai-act-standardisation), [Cyber Resilience Act](https://eur-lex.europa.eu/eli/reg/2024/2847/oj), [Product Liability Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj)).

Those developments support a narrower forecast: during the next two years, agent runtimes are likely to emit better traces and more domain-specific audit evidence, while operators build compact projections over those records for review, compliance, and handoff. Whether those projections become portable receipts depends less on inventing fields than on identity, evidence resolution, conformance, privacy, and who is willing to verify another vendor's claims. MCP finalization strengthens the case that the transport layer will converge; because the stable revision still does not bind exercised authority, committed domain effects, and independent verification into one receipt, it does not materially change the scenario probabilities below.

This forecast starts on **2026-08-02**. Dates below are legal deadlines or published protocol-policy thresholds, not guesses. Where an exact future date is unavailable—for NIST guidance, A2A tooling, or OpenTelemetry stabilization—the item belongs in the watch list rather than the calendar.

## Forward calendar

| Date | Published milestone | Why it matters for post-task evidence | Confidence and source |
|---|---|---|---|
| **2026-08-02** | The AI Act's general application date arrives, while Regulation (EU) `2026/1744` moves most high-risk-system duties to later dates. | The implementation phase begins with an unusual split: broad governance is live, but important technical record-keeping duties for high-risk systems remain tied to later standards and guidance. Builders should not mistake delayed high-risk deadlines for absence of present privacy, transparency, or governance obligations. | Enacted law, high confidence ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744), [Commission implementation FAQ](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act)). |
| **2026-09-11** | Cyber Resilience Act Article 14 vulnerability and severe-incident reporting starts, and ENISA says its Single Reporting Platform is scheduled to be operational. | Agent software that falls within the CRA's product scope may need evidence that supports rapid incident classification and reporting. A generic receipt will not replace the report, but correlation identifiers and effect evidence could shorten reconstruction. | Enacted deadline plus ENISA implementation statement, high confidence ([CRA Article 71](https://eur-lex.europa.eu/eli/reg/2024/2847/oj), [ENISA Single Reporting Platform](https://www.enisa.europa.eu/topics/product-security-and-certification/single-reporting-platform-srp)). |
| **2026-12-02** | Providers of generative AI systems placed on the market before `2026-08-02` must take steps to comply with AI Act Article 50(2)'s machine-readable marking requirement for synthetic content. | This is an output-provenance requirement, not an agent-action receipt. Its importance is architectural: provenance obligations may first standardize around particular artifacts and harms, strengthening the case for domain profiles instead of one all-purpose agent record. | Enacted deadline, high confidence ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). |
| **2026-12-09** | EU Member States must transpose the Product Liability Directive; it applies to products placed on the market or put into service after this date. | The Directive expressly includes software, treats AI-system providers as manufacturers in its recitals, allows courts to order proportionate disclosure of evidence, and can presume defectiveness if a defendant fails to disclose. This increases the value of comprehensible, retained evidence without dictating an agent-receipt format. | Enacted directive, high confidence ([Product Liability Directive, Articles 2, 9, 10, and 22](https://eur-lex.europa.eu/eli/dir/2024/2853/oj)). |
| **2027-08-01** | The European Commission must publish guidelines for Annex I high-risk AI systems, including avoiding duplication with sector legislation. | These guidelines can reveal whether regulators expect one integrated evidence layer or parallel AI and product records. Their treatment of proportionality and duplication is directly relevant to whether a receipt removes work or adds another compliance copy. | Enacted deadline, high confidence ([Regulation (EU) 2026/1744, amended Article 96](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). |
| **2027-08-02** | Member States must have at least one operational AI regulatory sandbox; the Commission must also adopt delegated acts specifying where equivalent sector requirements may limit duplicate AI Act duties. | Sandboxes create a venue to test evidence profiles with regulators, while the delegated acts can reward architectures that reference authoritative sector records rather than reproducing them. | Enacted deadlines, high confidence ([Regulation (EU) 2026/1744, amended Articles 2 and 57](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). |
| **2027-09-02** | The Commission must publish guidance, including a voluntary template, for high-risk AI post-market monitoring plans. | The template could become a de facto map of what operational evidence must be retained and aggregated. It will not itself specify a per-task receipt, but it can define the downstream questions receipts and source systems must answer. | Enacted deadline, high confidence ([Regulation (EU) 2026/1744, amended Article 72](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). |
| **2027-12-02** | High-risk obligations for systems classified through AI Act Article 6(2) and Annex III apply. | Providers in employment, education, essential services, law enforcement, migration, justice, and other listed uses will face the strongest near-term demand for automatic logging, technical documentation, human oversight, and post-market evidence. | Enacted deadline, high confidence ([Regulation (EU) 2026/1744, amended Article 113](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). |
| **2027-12-11** | The Cyber Resilience Act becomes generally applicable. | Secure development, vulnerability handling, support periods, and product conformity become part of the operating environment for commercial agent software in scope. Agent evidence designs will need to connect product/version identity to runtime effects without leaking exploitable detail. | Enacted deadline, high confidence ([Cyber Resilience Act, Article 71](https://eur-lex.europa.eu/eli/reg/2024/2847/oj)). |
| **2028-01-28** | Notified bodies already operating under Annex I product legislation must apply for AI Act designation if they want to assess relevant high-risk AI conformity. | Conformity assessors become an influential consumer of evidence formats. Their practical requests may produce sector-specific profiles before a horizontal receipt standard emerges. | Enacted deadline, high confidence ([Regulation (EU) 2026/1744, amended Article 43](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). |
| **2028-08-02** | High-risk obligations apply to systems classified under Article 6(1) and Annex I; aligned machinery delegated acts must also apply by this date. | Evidence requirements meet physical products and safety functions. Irreversibility and harm are more concrete here than in office assistants, so compact self-authored summaries will be least credible without domain-system and assessor evidence. | Enacted deadline, high confidence ([Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)). |
| **2028-09-11** | The Commission must report on the effectiveness of the CRA Single Reporting Platform after consulting ENISA and the CSIRT network. | This supplies an early public test of whether a shared reporting interface actually removes duplicate work while protecting sensitive evidence—a close institutional analogy to the leverage claim behind portable receipts. | Enacted review date, high confidence ([Cyber Resilience Act, Article 70](https://eur-lex.europa.eu/eli/reg/2024/2847/oj)). |

There are more than eight genuinely dated items, so no speculative conference date or undated standards aspiration has been added to pad the calendar.

## Second-order effects map

### 1. Market structure: interoperability commoditizes transport, then moves competition upward

**First order:** MCP and A2A aim to reduce the cost of connecting tools and agents. MCP's stable `2026-07-28` revision makes capabilities independently evolvable through an extension track and conformance requirements; A2A's roadmap emphasizes extensions, a compatibility kit, and SDKs in six languages ([MCP revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [MCP releases](https://github.com/modelcontextprotocol/modelcontextprotocol/releases), [A2A roadmap](https://a2a-protocol.org/latest/roadmap/)).

**Second order:** Once basic calls and task exchange are portable, differentiation moves to higher layers: identity binding, authorization policy, evidence retention, replay, evaluator quality, redaction, and domain connectors. A vendor may truthfully claim protocol interoperability while keeping the most valuable review record proprietary. The likely market is therefore not “one receipt vendor” but a chain of producers, evidence resolvers, signers, policy engines, verifiers, stores, and viewers.

**Third order:** Conformance suites and public test vectors become procurement leverage. Buyers can demand that a runtime export a common core while retaining freedom to choose storage and review tools. The opposite is also possible: separately versioned extensions can fragment semantics faster than the core stabilizes. The extension mechanism adopted to let MCP innovate without breaking its base protocol could also let vendors create incompatible receipt-like extensions.

**Who captures value:** incumbent observability and identity platforms have distribution, but open attestation formats reduce the cost for smaller vendors to compete. The in-toto framework already separates arbitrary typed predicates from subject binding and authentication, showing how a neutral envelope can support competing domain semantics ([in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md)).

### 2. Regulatory ripple: evidence demand rises, but copying evidence becomes a liability

**First order:** The AI Act, CRA, and Product Liability Directive all increase pressure for records that can support monitoring, incident reporting, conformity, and litigation. The Product Liability Directive is especially consequential because it includes software and enables proportionate court-ordered evidence disclosure; failing to disclose can trigger a presumption of defectiveness ([Product Liability Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj)).

**Second order:** Organizations retain more agent evidence “just in case.” That collides with GDPR purpose limitation, data minimisation, accuracy, and storage limitation. A trace that captures prompts, retrieved documents, tool arguments, identities, and outputs can contain personal data or secrets; OpenTelemetry's GenAI vocabulary itself warns that retrieval queries and related content may be sensitive ([GDPR Article 5](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A02016R0679-20160504), [OpenTelemetry GenAI attributes](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/)).

**Third order:** The winning architecture may be a small receipt with typed, access-controlled references—not a self-contained evidence bundle. That reduces duplication, but creates a new governance obligation: keep resolvers, authorization, keys, schema versions, and retention rules working for the life of the claim. A digest can prove the bytes presented later match the bytes referenced earlier; it cannot make deleted evidence available. SLSA explicitly says availability threats are not currently addressed by its integrity model ([SLSA threats and mitigations](https://slsa.dev/spec/v1.1/threats)).

**Regulatory divergence:** Rules are likely to produce profiles rather than one maximum record. Synthetic-content marking, high-risk decision logging, cyber incident reports, and product-liability evidence answer different questions. The Commission's standardisation work already spans ten separate areas, including record keeping, transparency, oversight, cybersecurity, quality management, and conformity assessment ([European Commission AI Act standardisation](https://digital-strategy.ec.europa.eu/en/policies/ai-act-standardisation)).

### 3. Talent and work: less “prompt engineering,” more evidence engineering

**First order:** Agent teams need distributed-systems skills: trace propagation, identity, authorization, event correlation, retries, idempotency, data classification, and incident response. NIST's concept paper treats dynamic authorization, delegation, auditability, and non-repudiation as unresolved agent-identity problems rather than a solved application feature ([NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)).

**Second order:** Platform, security, SRE, privacy, and domain engineers gain influence over agent design because the trustworthy evidence originates in their systems, not in model prose. This can improve engineering discipline, but it can also centralize control in an “AI governance platform” that every team must adopt.

**Third order:** Review work does not disappear; it changes shape. Ordinary engineers already report that raw multi-step logs are difficult to search, that structured events help, that replay remains elusive, and that comprehensive recording creates storage and security concerns. These are anecdotal community reports, sometimes posted by tool vendors, not representative surveys, but their recurring distinction between “more logs” and a usable timeline is directly relevant ([developer debugging thread](https://www.reddit.com/r/LocalLLaMA/comments/1rgwyqi/agent_debugging_is_a_mess_am_i_the_only_one/), [developer RAG debugging thread](https://www.reddit.com/r/LocalLLaMA/comments/1sho0ah/how_are_people_actually_debugging_bad_outputs_in/)).

The labor risk is telemetry administration: maintaining schemas, redaction policies, broken integrations, evaluator rules, and dashboards can consume the time the receipt promised to save. In a forecast published on **2026-05-26**, Gartner, an interested commercial analyst rather than a neutral public authority, predicts that governance failures will cause `40%` of enterprises to demote or decommission autonomous agents during its stated near-term forecast window; the forecast is not an observed outcome, but it identifies governance after production incidents as a plausible adoption brake ([Gartner governance forecast](https://www.gartner.com/en/newsroom/press-releases/2026-05-26-gartner-says-applying-uniform-governance-across-ai-agents-will-lead-to-enterprise-ai-agent-failure)).

### 4. Adjacent industries: signing, evidence stores, audit, insurance, and legal discovery

**First order:** Existing provenance and signing technology is repurposed. W3C PROV supplies portable concepts for entities, activities, agents, responsibility, and delegation. in-toto supplies subject binding, predicates, envelopes, and bundles. Sigstore bundles package signature content with verification material and can support offline verification ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md), [Sigstore bundle format](https://docs.sigstore.dev/about/bundle/)).

**Second order:** Key management, transparency services, retention archives, evidence gateways, and policy engines become part of the agent cost model. Insurance and litigation teams ask not merely whether a receipt exists, but whether it is authentic, comprehensible, complete enough for the asserted purpose, and linked to records the producer was required to retain.

**Third order:** “Signed” becomes a misleading marketing shortcut unless consumers distinguish signature verification from claim verification. Sigstore documentation notes that a bundle can verify the signature and payload, while claim checking is a separate concern; in-toto likewise targets automated policy engines, which must decide whether the authenticated metadata satisfies expectations ([Sigstore verification](https://docs.sigstore.dev/cosign/verifying/verify/), [in-toto specification](https://github.com/in-toto/attestation/blob/main/spec/README.md)). This creates a market for independent verifier profiles—and a risk of rubber-stamp verification badges.

### 5. Jurisdiction: global protocols meet local evidence boundaries

**First order:** MCP, A2A, OpenTelemetry, W3C PROV, and in-toto are designed for cross-system use, while privacy, employment, product, financial, health, and public-sector obligations remain jurisdictional and sectoral.

**Second order:** Multinational operators maintain a common technical core with jurisdiction profiles controlling what can be captured, where evidence may be stored, who can inspect it, and when it must be deleted. The Product Liability Directive harmonizes core liability rules but still relies on national courts and national transposition; the AI Act adds EU-wide requirements plus national competent authorities and sandboxes ([Product Liability Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj), [Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744)).

**Third order:** Portability can split into two meanings. *Schema portability* means another system can parse the receipt. *Practical portability* means the next operator can still resolve the evidence, verify identities and signatures, and lawfully use the contents. The latter is much harder and will favor evidence references with explicit owner, jurisdiction, access class, and retention horizon.

An analyst forecast published on **2025-10-21** offers a more aggressive fragmentation thesis: Gartner predicts that `35%` of countries will be locked into region-specific AI platforms during its stated near-term forecast window. That number is speculative and comes from a commercial forecasting firm, but the mechanism—data localization, regulation, language, and sovereign platforms—is a credible counterweight to universal receipt semantics ([Gartner predictions](https://www.gartner.com/en/newsroom/press-releases/2025-10-21-gartner-unveils-top-predictions-for-it-organizations-and-users-in-2026-and-beyond)).

### 6. Public narrative: from “the agent did it” to “show the effect”—or to surveillance theater

**First order:** The public and enterprise narrative shifts from capability demonstrations toward proof of execution, attribution, and remedy. Community posts already distinguish seeing model calls from proving that an external action occurred; one practitioner thread argues that application-level self-reported logs are insufficient for security monitoring and experiments with kernel-level observation instead ([LocalLLaMA runtime-observation thread](https://www.reddit.com/r/LocalLLaMA/comments/1r8yvu5/i_built_an_ebpf_tracer_to_monitor_ai_agents_the/)). This is a project author's claim, not independent validation, but it exposes the correct trust question: who produced the evidence, and could the actor alter it?

**Second order:** “Receipt available” becomes a trust badge. If the receipt merely restates the agent's own account, it can increase confidence without increasing assurance. Conversely, a receipt designed for managers and auditors can become an employee-monitoring artifact that exposes prompts, mistakes, browsing, or approval behavior beyond the purpose of task verification.

**Third order:** A backlash against exhaustive capture pushes the format toward progressive disclosure: a compact public or team-visible summary, restricted domain evidence, and sealed incident material with audited access. The C2PA provenance specification's attention to privacy and redaction in content credentials shows that provenance ecosystems eventually face personal-control and removal questions, not only immutability ([C2PA `2.2` specification](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)).

The narrative hinge is therefore simple: a receipt succeeds when it gives the next person a faster path to authoritative evidence and remedy. It fails when it is treated as a complete explanation, a surveillance transcript, or proof merely because it is machine-readable.

## Four scenarios

The percentages are analytical estimates, not measured probabilities. The four scenarios are mutually exclusive descriptions of the dominant market shape by **2028-08-02**; their point estimates sum to `100%`.

### Scenario 1 — Base: thin receipt projections emerge, but no universal receipt standard

**Probability:** **Plausible, `45%` point estimate** (`35–55%` band).

**State:** Major agent runtimes export OpenTelemetry-compatible traces and protocol task metadata. Enterprises create a compact per-task projection containing task identity, acting identity, exercised authority reference, effect references, artifact digests, terminal state, verifier results, and evidence pointers. The projection is portable within an organization or sector, but schemas differ at the edges.

**Why this is the base case:** It follows the division already visible in MCP, A2A, OpenTelemetry, W3C PROV, and in-toto. Transport, tracing, provenance concepts, and authenticated envelopes can interoperate without agreeing on every domain effect. W3C PROV was explicitly designed as a domain-agnostic core with extension points, while in-toto allows typed predicates under a common statement and envelope ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [in-toto framework](https://github.com/in-toto/attestation/blob/main/spec/README.md)).

**Falsifiable trigger:** By **2027-08-02**, at least two independent production-grade agent runtimes must export a common core set that can be consumed by the same open verifier without vendor-specific translation for task identity, external effects, and verifier outcome. If no such cross-runtime implementation appears, this scenario weakens toward the downside case.

**Indicators during the next 6–12 months:**

- MCP conformance cases begin to cover correlation, task extensions, or receipt-like extensions rather than transport syntax alone.
- A2A's TCK validates task/artifact lifecycle across multiple SDKs, but leaves domain evidence in extensions.
- OpenTelemetry GenAI conventions add or stabilize evaluation and agent/tool relations while continuing to act as telemetry rather than an audit standard.
- NIST guidance frames identity, delegated authority, and interoperable audit evidence as separable layers.
- EU implementation guidance favors references to existing sector records and explicitly tries to avoid duplicate evidence stores.

### Scenario 2 — Upside: a portable, signed receipt profile converges

**Probability:** **Modest, `20%` point estimate** (`10–30%` band).

**State:** A neutral project publishes a versioned agent-receipt predicate with conformance tests. Receipts bind immutable task outputs and effect references, preserve delegation and policy-decision references, carry independent verifier statements, and use a standard envelope such as in-toto/DSSE or an equivalent. Vendors compete on capture, storage, review, and verification rather than trapping the record.

**Why it can happen:** The pieces already exist. W3C PROV models activities, entities, responsibility, and delegation; in-toto separates predicate, subject binding, authentication, and bundling; Sigstore packages verification material; A2A supplies compatibility mechanisms, while MCP's stable `2026-07-28` revision supplies an extension mechanism ([W3C PROV-DM](https://www.w3.org/TR/prov-dm/), [in-toto framework](https://github.com/in-toto/attestation/blob/main/spec/README.md), [Sigstore bundle](https://docs.sigstore.dev/about/bundle/), [MCP revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [MCP releases](https://github.com/modelcontextprotocol/modelcontextprotocol/releases), [A2A roadmap](https://a2a-protocol.org/latest/roadmap/)). Regulation and procurement could supply the demand that technical elegance alone cannot.

**Falsifiable trigger:** By **2027-08-02**, two independent runtimes, two independent verifier implementations, and one real domain integration must successfully exchange and verify the same public receipt test vector without consulting the producer's proprietary trace backend. These counts are scenario thresholds chosen for falsifiability, not reported market data.

**Indicators during the next 6–12 months:**

- A public schema defines semantics for partial completion, retries, delegation, external effects, evidence expiry, and independent verification—not merely `agent`, `prompt`, `tools`, and `success`.
- Test vectors include tampering, missing evidence, revoked identity, expired keys, and privacy-redacted receipts.
- At least one protocol project adopts the schema as an optional extension while keeping the envelope usable outside that protocol.
- Procurement or regulatory sandbox documents request exportable, machine-verifiable post-task evidence.
- Developer tools render the same receipt from multiple agent frameworks and link back to domain-native records.

### Scenario 3 — Downside: proprietary telemetry and compliance evidence swamp the receipt

**Probability:** **Modest, `30%` point estimate** (`20–40%` band).

**State:** Each platform offers an impressive trace viewer, evaluation dashboard, and “audit log,” but exports lose important semantics or evidence links. Organizations respond to regulation by retaining more prompts and traces, then restrict access because of privacy and security risk. Reviewers still reconstruct outcomes manually across vendor dashboards and domain systems.

**Why it can happen:** OpenTelemetry's GenAI vocabulary remains in development and has already moved to a separate repository; its roadmap issue opened on **2026-01-25** describes GenAI stabilization as unconfirmed. MCP's stable `2026-07-28` revision moves structured observability out to OpenTelemetry, and A2A leaves capabilities to extensions. None of those choices is wrong, but no project currently owns the complete post-task accountability boundary ([OpenTelemetry roadmap](https://github.com/open-telemetry/semantic-conventions/issues/3330), [OpenTelemetry GenAI repository](https://github.com/open-telemetry/semantic-conventions-genai), [MCP revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [MCP releases](https://github.com/modelcontextprotocol/modelcontextprotocol/releases), [A2A roadmap](https://a2a-protocol.org/latest/roadmap/)).

**Falsifiable trigger:** Through **2027-08-02**, leading agent platforms continue to export traces but no independent verifier can determine committed external effects and exercised authority without platform-specific APIs. If neutral verification becomes routine, this scenario is falsified.

**Indicators during the next 6–12 months:**

- Breaking or vendor-specific semantic changes continue around agent, workflow, tool, and evaluation events.
- “Audit” product pages emphasize retention volume and dashboards rather than evidence authenticity, effect reconciliation, or exit.
- Security and privacy teams disable content capture, leaving traces too sparse for post-incident reconstruction.
- Legal and compliance teams build separate evidence repositories rather than consume engineering telemetry.
- Practitioner discussions keep reporting manual JSON logging, unclear replay, disk cost, and difficulty separating model error from tool or retrieval error ([LocalLLaMA debugging thread](https://www.reddit.com/r/LocalLLaMA/comments/1rgwyqi/agent_debugging_is_a_mess_am_i_the_only_one/), [RAG debugging thread](https://www.reddit.com/r/LocalLLaMA/comments/1sho0ah/how_are_people_actually_debugging_bad_outputs_in/)).

### Scenario 4 — Wildcard: domain-native effect records make the generic receipt disappear

**Probability:** **Low, `5%` point estimate** (`1–10%` band).

**State:** Buyers and regulators conclude that a generic agent receipt adds false confidence. They require actions to flow through domain systems with strong identity, policy, idempotency, approvals, and audit records. The only portable artifact is a disposable manifest of domain event references; the “agent” is not a privileged evidence category.

**Why it is possible:** Liability and safety rules focus on products, harms, controls, and evidence, not on preserving an agent's narrative. The Product Liability Directive can require relevant evidence and assess software behavior without defining agent-specific receipts. CRA reporting centers on vulnerabilities and severe security incidents. W3C PROV already allows application-specific provenance to map into a generic core when interchange is needed ([Product Liability Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj), [Cyber Resilience Act](https://eur-lex.europa.eu/eli/reg/2024/2847/oj), [W3C PROV-DM](https://www.w3.org/TR/prov-dm/)).

**Falsifiable trigger:** By **2027-08-02**, at least two regulated sectors or major procurement frameworks explicitly reject self-authored agent summaries and require only independently generated domain events plus human-readable case views. If cross-domain receipt standards instead gain procurement recognition, this wildcard recedes.

**Indicators during the next 6–12 months:**

- Security architectures move observation below the agent runtime or through mandatory tool gateways.
- Regulators and auditors ask for transaction, case, decision, or product records without using agent-specific terminology.
- Agent frameworks become interchangeable callers behind existing workflow and audit systems.
- Receipts shrink to collections of signed references and lose prompts, plans, chain-of-thought, and agent narration.
- Community discussion increasingly treats the source system—not an LLM trace—as the only credible proof that an effect happened.

## The single 90-day signal

**Check on 2026-10-31 whether any neutral standards or open-source project has published a machine-verifiable, cross-vendor schema plus public test vectors that bind all four of these elements: task identity, exercised authority, domain effect references, and an independent verifier result.**

The places to check are the [NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative), [MCP specification and proposal work](https://github.com/modelcontextprotocol/modelcontextprotocol), [A2A extensions and TCK](https://a2a-protocol.org/latest/roadmap/), [OpenTelemetry GenAI conventions](https://github.com/open-telemetry/semantic-conventions-genai), and [in-toto predicate proposals](https://github.com/in-toto/attestation).

Why this one signal: trace schemas without authority and effects cannot answer who was allowed to do what; authority receipts without domain effects cannot prove what happened; and self-declared “passed” fields do not add assurance. A testable cross-vendor combination of all four would show the category is becoming real. Another dashboard, trace viewer, or vendor-only JSON export would not.

## The under-priced effect: evidence decay becomes the real system

The obvious costs are serialization, storage, and a viewer. The under-priced cost is keeping the receipt **true enough to use later**.

A small receipt can outlive every dependency that gives it meaning:

- an evidence URL is deleted or now returns a different version;
- a trace backend expires detailed spans;
- an identity provider rotates or retires keys;
- a policy identifier no longer resolves to the evaluated version;
- a model or agent revision label is reused;
- access rules change so the reviewer cannot open the cited record;
- a schema evolves and silently changes field meaning;
- privacy deletion removes data needed for a later challenge;
- a verifier disappears or its evaluation set cannot be reproduced.

Signing does not solve this. Sigstore bundles demonstrate how verification material and timestamps can travel with a signature, but claim interpretation and underlying evidence remain separate ([Sigstore bundle format](https://docs.sigstore.dev/about/bundle/), [Sigstore verification](https://docs.sigstore.dev/cosign/verifying/verify/)). SLSA explicitly excludes availability from its current protection model ([SLSA threats](https://slsa.dev/spec/v1.1/threats)). The Product Liability Directive can make retained evidence valuable for years—its ordinary limitation period is three years from awareness and its expiry period is generally ten years—while GDPR still requires purpose limitation, minimisation, and storage limitation ([Product Liability Directive, Articles 16 and 17](https://eur-lex.europa.eu/eli/dir/2024/2853/oj), [GDPR Article 5](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A02016R0679-20160504)).

The receipt therefore creates a quiet long-lived system of resolvers, archives, migrations, cryptographic trust roots, deletion exceptions, access reviews, and schema governance. If maintaining that system costs more than the reconstruction work it removes, the receipt has failed the site's leverage test even if the file itself remains tiny.

## Watch list

1. **NIST AI Agent Standards Initiative** — watch for voluntary guidelines, gap analyses, identity/authorization profiles, test methods, and explicit audit-evidence semantics ([initiative page](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative)).
2. **MCP specification, extensions, and conformance suite** — the `2026-07-28` revision is stable; watch adoption and conformance coverage, then whether trace propagation grows into standardized task/effect evidence or remains transport telemetry ([revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/), [release status](https://github.com/modelcontextprotocol/modelcontextprotocol/releases)).
3. **A2A extensions, Inspector, and TCK** — watch which task/artifact metadata becomes interoperable and whether verifier or provenance extensions emerge ([roadmap](https://a2a-protocol.org/latest/roadmap/)).
4. **OpenTelemetry GenAI semantic conventions** — watch stability status, agent/tool/evaluation event changes, privacy guidance, and whether downstream effects are represented or only spans ([GenAI repository](https://github.com/open-telemetry/semantic-conventions-genai), [roadmap issue opened 2026-01-25](https://github.com/open-telemetry/semantic-conventions/issues/3330)).
5. **EU AI Office and AI Board** — watch enforcement guidance, record-keeping interpretation, sandbox outputs, and the treatment of duplicate sector evidence ([AI Board](https://digital-strategy.ec.europa.eu/en/policies/ai-board)).
6. **CEN-CENELEC JTC 21 and harmonised AI standards** — watch drafts for record keeping, human oversight, cybersecurity, quality management, and conformity assessment; the Commission reports this work is still ongoing ([Commission standardisation page](https://digital-strategy.ec.europa.eu/en/policies/ai-act-standardisation)).
7. **ENISA CRA Single Reporting Platform** — watch testing, technical reporting fields, confidentiality controls, and whether one entry point actually reduces duplicate reporting ([ENISA SRP](https://www.enisa.europa.eu/topics/product-security-and-certification/single-reporting-platform-srp)).
8. **National Product Liability Directive transposition** — watch how courts' evidence-disclosure powers and software liability are implemented before `2026-12-09` ([Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj)).
9. **W3C PROV profiles and adoption** — watch for an agent-specific specialization that preserves the generic activity/entity/agent/delegation semantics ([PROV-DM](https://www.w3.org/TR/prov-dm/)).
10. **in-toto Attestation Framework predicates** — watch for agent-task, deployment, policy-decision, or runtime-effect predicates and cross-language verifier support ([framework repository](https://github.com/in-toto/attestation)).
11. **Sigstore bundle and verification tooling** — watch offline verification, keyless/private deployment patterns, and the boundary between authentic payload and verified claim ([bundle format](https://docs.sigstore.dev/about/bundle/)).
12. **SLSA specification** — watch whether provenance availability, runtime evidence, or non-build attestations expand in later versions ([threats model](https://slsa.dev/spec/v1.1/threats)).
13. **C2PA provenance and privacy work** — watch redaction, identity, and selective-disclosure patterns that agent evidence systems may reuse ([C2PA `2.2`](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html)).
14. **Protocol-independent procurement language** — watch EU sandboxes, public tenders, financial/health guidance, and enterprise RFPs for requirements such as exportable evidence, independent verification, effect reconciliation, and exit support.
15. **Ordinary-engineer communities** — watch recurring threads in LocalLLaMA, Hacker News, and standards GitHub issues for the gap between demos and operations: manual event wrapping, replay, silent tool failure, sensitive logs, storage costs, and distrust of self-reported traces ([example debugging thread](https://www.reddit.com/r/LocalLLaMA/comments/1rgwyqi/agent_debugging_is_a_mess_am_i_the_only_one/), [OpenTelemetry agent-systems issue](https://github.com/open-telemetry/semantic-conventions-genai/issues/35), [Hacker News AgentLens thread](https://news.ycombinator.com/item?id=47205382)).
16. **Market correction and governance forecasts** — treat Gartner's near-term cancellation and decommissioning forecasts as hypotheses to compare with observed deployments, not facts; watch whether governance gaps actually become the stated cause of failed projects ([project-cancellation forecast published 2025-06-25](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027), [governance forecast published 2026-05-26](https://www.gartner.com/en/newsroom/press-releases/2026-05-26-gartner-says-applying-uniform-governance-across-ai-agents-will-lead-to-enterprise-ai-agent-failure)).

## Disagreements and uncertainty that should remain visible

1. **Convergence versus fragmentation.** NIST, MCP, A2A, and OpenTelemetry all promote interoperability, but each owns a different layer. Their progress is evidence of ecosystem activity, not evidence that one receipt will converge.
2. **More evidence versus less data.** Product liability, AI monitoring, and cyber reporting reward reconstructable evidence; GDPR and operational security reward minimisation and restricted access. A credible design must support selective disclosure and purpose-specific retention rather than declaring one side dominant.
3. **Trace as foundation versus trace as distraction.** Standards projects treat tracing as essential correlation infrastructure. Practitioners report that traces can still be overwhelming, incomplete, expensive, or self-reported. Both can be true: a trace can be necessary to assemble a receipt without being the receipt a reviewer needs.
4. **Agent-specific standard versus ordinary systems engineering.** The upside scenario gives agents a distinct portable evidence artifact. The wildcard says the durable truth belongs entirely in domain systems and that agent-specific records are a temporary category error. The prototype should be designed to test this disagreement.
5. **Analyst urgency versus observed reality.** Gartner forecasts large adoption and failure rates, but those figures are proprietary analytical predictions and sometimes rely on webinar-attendee polls rather than representative population samples. They are useful scenario inputs, not baselines.

## Proper-noun snowball

**Round 1 — names surfaced by the core architecture and regulation:** MCP, A2A, OpenTelemetry, NIST, EU AI Office, AI Board, CEN, CENELEC, ENISA, W3C PROV, in-toto, SLSA, Sigstore, C2PA, Gartner.

**Round 2 — what their primary materials added:**

- MCP led to an RC on **2026-05-29** for an Extensions Track, conformance suite, W3C Trace Context propagation, and formal deprecation lifecycle, followed by the stable `2026-07-28` revision on **2026-07-28**. Finalization strengthens the interoperable transport foundation without supplying task/effect receipt semantics.
- A2A led to its Inspector, Technology Compatibility Kit, extensions governance, and six official SDK languages.
- OpenTelemetry led to the separate GenAI semantic-conventions repository, the unconfirmed stabilization plan, and active agent-system semantics issues.
- EU AI Act implementation led to JTC 21, harmonised-standard work in ten areas, AI regulatory sandboxes, post-market monitoring guidance, and notified-body designation.
- CRA led to ENISA's Single Reporting Platform and the later effectiveness review.
- Product liability led to evidence disclosure, rebuttable presumptions, software/manufacturer definitions, and long liability horizons.
- in-toto led to DSSE-style envelopes and Sigstore verification bundles; SLSA exposed the unresolved availability boundary.
- W3C PROV and C2PA led to domain profiles, provenance-of-provenance, privacy, and redaction questions.

A third snowball round was not necessary. It would have expanded into individual vendors and sector rules without improving the core forecast.

## Source receipts

| Source | Type and date state | Claims it supports | Limitations / conflicts |
|---|---|---|---|
| [Regulation (EU) 2026/1744](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1744) | Primary enacted EU law, published `2026-07-24` | Revised AI Act application dates; guidance, sandbox, monitoring-template, notified-body, and high-risk deadlines | Does not prescribe a generic agent receipt; applies differently by system classification and role. |
| [European Commission AI Act FAQ](https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act) | Primary institutional implementation guidance, current as researched `2026-08-02` | General versus delayed high-risk application; reasons standards were delayed | Guidance, not the legal act; earlier commentary can be superseded by the final Omnibus. |
| [AI Act standardisation](https://digital-strategy.ec.europa.eu/en/policies/ai-act-standardisation) | Primary Commission programme page | Ten standardisation areas; voluntary standards and presumption of conformity; work still ongoing | Describes process and expectations, not completed standards. |
| [Cyber Resilience Act](https://eur-lex.europa.eu/eli/reg/2024/2847/oj) | Primary enacted EU law | `2026-09-11`, `2027-12-11`, and `2028-09-11` milestones | Product scope and role analysis is required; not every agent deployment is a CRA product. |
| [ENISA Single Reporting Platform](https://www.enisa.europa.eu/topics/product-security-and-certification/single-reporting-platform-srp) | Primary implementing-agency page, updated `2026-07-17` | Scheduled operational date, reporting flow, confidentiality, and scope | Implementation details can change; the CRA remains authoritative. |
| [Product Liability Directive](https://eur-lex.europa.eu/eli/dir/2024/2853/oj) | Primary enacted EU directive | Software scope, evidence disclosure, presumptions, liability periods, and `2026-12-09` transposition | National transposition and court practice will determine application; a receipt is not a statutory safe harbor. |
| [GDPR](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A02016R0679-20160504) | Primary enacted EU law | Purpose limitation, minimisation, accuracy, storage limitation | Does not set one retention period for agent evidence; lawful basis and context matter. |
| [MCP `2026-07-28` revision explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/) and [release status](https://github.com/modelcontextprotocol/modelcontextprotocol/releases) | Primary project proposal and release repository; RC released `2026-05-29`, stable revision released `2026-07-28` | Stable Trace Context, extensions, Tasks, OTel logging replacement, conformance, and deprecation lifecycle | Stable protocol status does not prove adoption and does not supply a complete agent receipt. |
| [A2A roadmap](https://a2a-protocol.org/latest/roadmap/) | Primary project roadmap, updated `2026-03-10` | Extensions, TCK, Inspector, SDKs, and 3–6 month direction | Roadmap is not a delivery guarantee and gives few fixed future dates. |
| [OpenTelemetry roadmap issue](https://github.com/open-telemetry/semantic-conventions/issues/3330) | Primary open project issue, opened `2026-01-25` and explicitly work in progress | GenAI core stabilization is unconfirmed; confirmed priorities lie elsewhere | An open issue can change and is not a final roadmap. |
| [OpenTelemetry GenAI repository](https://github.com/open-telemetry/semantic-conventions-genai) | Primary project repository | Active agent, tool, MCP, metric, span, and event semantics work | Activity and issue counts do not prove adoption or stability. |
| [NIST AI Agent Standards Initiative](https://www.nist.gov/artificial-intelligence/ai-agent-standards-initiative) | Primary U.S. government programme page | Standards, protocols, identity, authorization, security evaluation, and research agenda | No receipt schema or dated publication promise. |
| [W3C PROV-DM](https://www.w3.org/TR/prov-dm/) | Primary W3C Recommendation | Domain-agnostic provenance core, delegation, responsibility, extensibility | Provenance vocabulary does not by itself provide signatures, authorization decisions, or evidence retention. |
| [in-toto Attestation Framework](https://github.com/in-toto/attestation/blob/main/spec/README.md) | Primary open specification | Predicate/statement/envelope/bundle separation and policy-engine consumers | Designed around software artifacts; applying it to runtime agent tasks is an extension hypothesis. |
| [Sigstore bundle format](https://docs.sigstore.dev/about/bundle/) | Primary project documentation | Portable verification material, timestamps, signatures, and DSSE attestations | Signature authenticity does not establish truth or completeness of receipt claims. |
| [SLSA threats and mitigations](https://slsa.dev/spec/v1.1/threats) | Primary open specification | Provenance integrity boundary and unaddressed availability threat | Supply-chain focus differs from runtime agent accountability. |
| [C2PA `2.2`](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) | Primary open specification | Content provenance, privacy, personal control, and redaction concerns | Media/content provenance differs from action and authority evidence. |
| [Gartner project-cancellation forecast](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027) | Commercial analyst forecast | Possible cost, value, and risk-control headwinds; adoption forecast | Forecast, not outcome; vendor taxonomy and polling are not independently validated here. |
| [Gartner governance forecast](https://www.gartner.com/en/newsroom/press-releases/2026-05-26-gartner-says-applying-uniform-governance-across-ai-agents-will-lead-to-enterprise-ai-agent-failure) | Commercial analyst forecast | Hypothesis that authority/governance gaps surface after incidents | Same limitations; useful for scenario construction only. |
| [LocalLLaMA agent debugging thread](https://www.reddit.com/r/LocalLLaMA/comments/1rgwyqi/agent_debugging_is_a_mess_am_i_the_only_one/) | Anecdotal practitioner social discussion, `2026-02-28` onward | Structured timeline preference, replay gap, raw-log burden, security concern | Tiny self-selected sample; some replies promote tools; not representative. |
| [LocalLLaMA RAG debugging thread](https://www.reddit.com/r/LocalLLaMA/comments/1sho0ah/how_are_people_actually_debugging_bad_outputs_in/) | Anecdotal practitioner social discussion, `2026-04-10` onward | Difficulty locating subtle failures; manual metadata; storage concern | Tiny self-selected sample and vendor promotion; useful only as qualitative texture. |
| [LocalLLaMA runtime-observation thread](https://www.reddit.com/r/LocalLLaMA/comments/1r8yvu5/i_built_an_ebpf_tracer_to_monitor_ai_agents_the/) | Project-author social post, `2026-02-19` | Argument that evidence generated below the agent may have a stronger security trust boundary | Self-authored project claim; no independent evaluation established. |

## Bottom line for the exploration

The future-facing question is not “Will agents produce logs?” They already do, and the standards ecosystem is making those logs more interoperable. The question worth building against is:

> Can a small, portable projection help a different person verify identity, authority, committed effects, and independent checks **after the original runtime and vendor are gone**, without copying so much evidence that it becomes a privacy, security, and maintenance system of its own?

The next prototype should therefore be tested twice: once immediately after task completion, and once after deliberately breaking or replacing its trace backend, evidence location, verifier, and agent runtime. The second test is where portability, engineering freedom, and leverage become observable rather than aspirational.
