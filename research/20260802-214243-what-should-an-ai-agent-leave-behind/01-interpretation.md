## One-sentence summary

An unpublished exploration proposes testing a small, portable “agent receipt” that makes a completed AI-agent task understandable and verifiable without preserving an exhaustive activity log.

## The actual question this material is answering

What is the minimum durable evidence an autonomous system must leave after acting so that another person can understand, verify, challenge, reverse, or reproduce its work without the evidence itself creating disproportionate cost, surveillance, or platform lock-in?

## Thesis / central claim

The author provisionally asserts that a successful output or a raw activity log is insufficient for trustworthy autonomous work. The candidate alternative is a compact, portable receipt connecting the result to the responsible agent, its authority and information, its actions and changes, and the evidence used for verification. No external people or institutions are reported as making these claims; the piece is a proposal for an experiment, not a report of established findings.

## Key claims (numbered)

1. **Claim:** A successful result alone may not make autonomous work trustworthy. **Evidence in source:** The draft asks what another person must be able to understand or verify after the agent runs, but provides no case study or data. **Evidence type:** absent.
2. **Claim:** Evidence requirements should increase with authority, impact, and difficulty of reversal. **Evidence in source:** The draft contrasts a read-only summarizer with an agent that moves money or changes production infrastructure. **Evidence type:** anecdotal/hypothetical.
3. **Claim:** More logs do not necessarily create more trust. **Evidence in source:** The author argues that complete logs can be too detailed to review, costly to retain, and incapable of explaining why a result deserves trust. **Evidence type:** absent.
4. **Claim:** A useful post-task artifact should connect the outcome to agent identity, authority, information, changes, and verification evidence. **Evidence in source:** These fields are described in prose and represented in the proposed YAML receipt. **Evidence type:** primary as evidence of the proposed design, absent as evidence of its effectiveness.
5. **Claim:** Reversibility, reproducibility, reviewability, and portability are important properties of the retained record. **Evidence in source:** They appear as explicit research questions and, for reversibility, as a prototype field. **Evidence type:** primary as design requirements, absent as validated requirements.
6. **Claim:** The smallest useful record could remove repeated review, incident, and audit work. **Evidence in source:** The draft states this as something the experiment should reveal; it offers no baseline, measurement method, or observed savings. **Evidence type:** absent.
7. **Claim:** A compact YAML receipt is a plausible prototype for testing these ideas. **Evidence in source:** The draft provides a concrete illustrative schema for a `settlement-explainer` task. **Evidence type:** primary/prototype.

## Named entities

- **Sven** — person; appears only as the illustrative requester in the receipt, treated as an actor.
- **settlement-explainer** — hypothetical agent/product identifier; treated as the actor performing the task.
- **settlement-reader** — hypothetical tool identifier; treated as an execution dependency.
- **approved-eu-provider** — hypothetical provider label rather than an identified institution; treated as an execution dependency and a possible jurisdictional signal.
- **settlement-8472** — hypothetical evidence record; treated as supporting evidence.
- **trace-123** — hypothetical trace identifier; treated as an operational reference.
- **AI agent** — generic technology category, not a named product; treated as the subject.
- No real institution, regulation, place, model vendor, standard, or product is named.

## Numbers and dates

- **“2026-08-02”** — publication/draft date in the front matter; attributed to the exploration file.
- **“0.18”** — illustrative execution cost in the YAML receipt; no currency or attribution is supplied.
- **“a8c21f4”** — illustrative agent revision identifier; attributed to `settlement-explainer` in the prototype.
- **“trace-123”** — illustrative trace identifier; attributed to the execution block.
- **“settlement-8472”** — illustrative evidence identifier; attributed to the result block.
- **“one task”** — scope of the planned experiment; attributed to the author.
- No measured retention period, storage volume, latency, error rate, review time, audit cost, or confidence score is supplied.

## What's assumed but not argued

- That a discrete “completed task” can be identified for long-running, recursive, or multi-agent workflows.
- That agent identity and revision can be made stable and meaningful across vendors and deployments.
- That the receipt can faithfully summarize behavior without being self-serving, incomplete, or fabricated by the same agent whose work it attests.
- That evidence references will remain resolvable and access-controlled for as long as the receipt is retained.
- That authority can be represented compactly rather than reconstructed from dynamic identity, policy, and delegation systems.
- That outcome verification can be represented by a field such as `passed` without preserving who verified what, against which criterion, and with what independence.
- That portability is technically and institutionally achievable without a standard schema or common semantics.
- That smaller records reduce total work once schema governance, ingestion, retention, migration, privacy review, and incident response are counted.
- That reviewability, reproducibility, and reversibility are always compatible; some actions and stochastic outputs may be irreversible or non-reproducible.
- That retaining tool use, prompts, evidence, and requester identity is legally and ethically acceptable.

## What's missing from the piece

- Definitions that distinguish a receipt from logs, traces, audit trails, provenance records, model cards, decision records, attestations, and ordinary application events.
- A threat model: accidental errors, malicious agents, compromised tools, dishonest operators, prompt injection, evidence tampering, and insider abuse.
- The intended reader and decision: operator, reviewer, auditor, affected person, incident responder, regulator, or future agent.
- Real incidents in which the presence or absence of post-task evidence changed an outcome.
- Existing standards and precedents in distributed tracing, software supply-chain attestations, event sourcing, accounting receipts, safety cases, and regulated decision records.
- A risk-tiering rule that translates authority, impact, and reversibility into required evidence.
- Privacy, employee-surveillance, intellectual-property, security, data-residency, deletion, and subject-access implications.
- Integrity mechanisms: signing, timestamping, append-only storage, independent verification, chain of custody, and schema versioning.
- Evaluation criteria for “smallest useful”: review time, reconstruction success, incident resolution, false confidence, storage cost, and interoperability.
- Community and practitioner voices, including ordinary engineers who would implement, operate, review, and be monitored by such receipts.
- Failure semantics for partial completion, uncertainty, abandoned work, retries, delegation, human intervention, and conflicting evidence.
- Ownership and maintenance: who defines the schema, pays for retention, resolves broken evidence links, and authorizes deletion.

## Confidence read

The source is appropriately tentative: it repeatedly frames the receipt as a hypothesis to test and labels the conclusion “Under exploration.” A careful reader can be confident about the proposed research problem and prototype shape, but not about the receipt’s usefulness, sufficiency, or net leverage because the piece contains no external evidence or completed experiment. Claims **1, 3, 4, 5, and 6** are weak as empirical claims; claim **2** is intuitively plausible but only hypothetically illustrated; claim **7** is well supported only as a description of what the author intends to build.

## Research questions (mandatory)

1. **Why now?** Open: The source names no event, deadline, regulation, incident, or adoption shift that makes post-task evidence newly urgent. Research should test whether the rise of tool-using agents, emerging AI regulation, or recent agent failures supplies the real timing.

2. **Why this choice, not the obvious alternative?** The receipt is chosen as a candidate middle layer between output-only records and exhaustive logs: compact enough to review, but structured enough to point to evidence and changes. Open: The source does not compare this design with existing traces, signed attestations, event logs, human approvals, or risk-tiered audit records.

3. **Capability gap vs incumbents.** Open: No incumbent system or standard is identified, so the receipt’s concrete gains and omissions cannot yet be compared. The proposed schema appears simpler and more portable than full observability platforms, but it may lack integrity, causality, policy context, identity assurance, redaction, and interoperable semantics.

4. **Who else can use this?** The draft implies that teams changing platforms and people reviewing, auditing, or responding to agent work could use it. Open: Access rules, eligibility, onboarding, pricing, affected-person access, and whether the schema is public or proprietary are unspecified.

5. **What else exists in this category?** Open: The source names no peers, competitors, predecessors, or standards. Research should examine agent traces and observability, provenance and lineage, tamper-evident audit logs, software attestations, decision records, and regulated record-keeping as adjacent categories.

6. **Upstream dependencies.** The receipt depends at minimum on stable agent identity and revision, requester identity, tool-use telemetry, trace capture, cost accounting, resolvable evidence, change detection, and a verification mechanism. Open: The source does not explain who supplies or authenticates any of those inputs.

7. **Downstream dependencies.** Reviewers, incident responders, auditors, teams migrating platforms, and possibly future agents could depend on the receipt to reconstruct completed work. Open: The source does not specify workflows, enforcement decisions, appeals, remediation, or systems that consume it.

8. **Money and ownership.** The prototype includes cost `0.18`, implying execution economics matter, but no currency, owner, funder, beneficiary, or retention cost is identified. Open: Research must locate who pays to generate, secure, store, migrate, and review receipts, and who captures value from standardizing them.

9. **Regulation and jurisdiction.** The label `approved-eu-provider` hints at European constraints, but no jurisdiction or rule is actually specified. Open: Research should test how EU AI, privacy, employment, financial-services, health, public-sector, and record-retention rules affect what must be recorded and what must be deleted.

10. **Track record and risk.** The draft hypothesizes that moving money and changing production infrastructure require stronger evidence than read-only summarization. Open: It gives no incidents, breaches, enforcement cases, failed audits, tampered logs, or examples of receipt-like artifacts working well.

11. **What changes if this fails or succeeds?** If it succeeds, a portable receipt could reduce repeated reconstruction work, support review and migration, and make delegated work more legible while preserving engineering freedom. If it fails, it may become compliance theater, leak sensitive data, create surveillance and storage burdens, or generate misplaced confidence in an agent-authored summary.

12. **Contrarian read.** The strongest challenge is that the proposed receipt is another lossy log format whose neat fields hide uncertainty and invite checkbox trust; the authoritative evidence already belongs in the systems where actions occurred. On this view, investment should go into transactional controls, least privilege, reversible operations, and domain-native audit trails, with any receipt generated only as a disposable index.

## Research seeds

1. What event or adoption shift makes an agent receipt timely now, rather than an old auditability problem with new branding?
2. Which existing agent observability, tracing, provenance, attestation, and audit standards already cover the proposed fields?
3. How should evidence requirements scale with authority, impact, sensitivity, autonomy, and reversibility?
4. Can the acting agent credibly author its own receipt, or must tools, policy engines, and verifiers co-sign it?
5. What should remain in a portable receipt versus source systems, and how are references kept resolvable across migration and deletion?
6. What access, onboarding, pricing, and governance model would let teams, auditors, affected people, and other vendors use the format?
7. Which real incidents demonstrate the value or danger of post-task artifacts?
8. How do ordinary engineers experience current agent traces: what do they actually inspect, ignore, redact, or wish they had during debugging and incidents?
9. Which privacy, workplace-surveillance, security, and retention risks grow when prompts, evidence, tool calls, identities, and uncertainty are preserved?
10. What measurable experiment can determine whether a receipt reduces total review and incident work rather than adding a new maintenance obligation?

## Research plan

### Topic shape

**Technical design hypothesis; governance and accountability pattern; emerging developer practice.** This is an evergreen investigation of whether a minimal, portable evidence artifact can make tool-using AI agents accountable after execution, with current regulation and community practice supplying context rather than a single news event.

### Relevance matrix

| Owner | Section | Status | Reason |
|-------|---------|--------|--------|
| History | Long arc | Required | Audit trails, receipts, provenance, and accountable delegation predate AI and define the problem’s foundations. |
| History | Direct precedents | Required | Tracing, event sourcing, decision records, attestations, and regulated records may already solve parts of it. |
| History | Failed attempts | Required | Compliance logs and observability systems often fail through volume, weak semantics, or poor reviewability. |
| History | Recurring cast | Required | Standards bodies, platform vendors, auditors, regulators, developers, and affected people repeatedly shape evidence systems. |
| History | What's new | Required | Tool-using, probabilistic, delegated agents may alter scale, causality, identity, and explanation requirements. |
| History | Experienced observer next | Required | The likely path toward risk tiers, standard fields, signed evidence, and vendor-specific extensions needs testing. |
| Mechanism | What | Required | The investigation needs a precise distinction between receipt, log, trace, attestation, and source-of-truth record. |
| Mechanism | Walkthrough | Required | An end-to-end task example can expose where each field originates and how a reviewer uses it. |
| Mechanism | Inputs | Required | Identity, policy, tools, costs, evidence, changes, and verification all require upstream data. |
| Mechanism | Internals | Required | Authenticity, correlation, evidence pointers, schema evolution, signing, retention, and redaction are load-bearing. |
| Mechanism | Failure modes | Required | Omission, fabrication, tampering, broken references, false verification, and sensitive leakage could defeat the design. |
| Mechanism | Constraints | Required | Token, storage, privacy, interoperability, stochasticity, and irreversibility constrain completeness. |
| Mechanism | Side effects | Required | Receipts may change behavior, create surveillance, encourage checkbox compliance, or shift liability. |
| Mechanism | Analogy | Required | Accounting receipts, flight recorders, and supply-chain attestations can clarify both promise and limits. |
| Stakeholders | Cast | Required | Builders, operators, reviewers, auditors, affected users, vendors, and regulators have distinct needs. |
| Stakeholders | Geography | Required | Data protection, AI rules, employment monitoring, and sector obligations vary by jurisdiction. |
| Stakeholders | Numbers | Optional | Quantitative evidence on agent adoption, incident cost, telemetry volume, and review time is valuable if comparable. |
| Stakeholders | Money flow | Required | Generation, storage, review, compliance, and migration costs determine whether the artifact creates leverage. |
| Stakeholders | Power | Required | Whoever defines, produces, reads, and deletes receipts controls the accountability boundary. |
| Stakeholders | Impact | Required | Benefits and burdens should be compared across operators, engineers, auditors, organizations, and affected people. |
| Stakeholders | Under-recognized | Required | Security teams, data subjects, future maintainers, and smaller vendors may bear hidden gains or costs. |
| Stakeholders | Silence | Required | Missing voices—especially ordinary engineers and people subject to decisions—are central to the user’s request. |
| Stakeholders | Document inventory | Required | Standards, regulations, incident reports, schemas, repos, and vendor docs should anchor claims. |
| Contrarian | Competing explanations | Required | The problem may be weak controls or poor domain auditability, not absence of a new receipt. |
| Contrarian | Interests | Required | Vendors, compliance teams, employers, and standards advocates may benefit from different framings. |
| Contrarian | Omitted receipts | Required | The draft supplies no incidents, comparative standards, measurements, or practitioner evidence. |
| Contrarian | Community dissent | Required | Skeptical engineers can test whether receipts help operations or merely add telemetry and bureaucracy. |
| Contrarian | Quant reframes | Optional | Storage, review time, false-positive rates, and incident reconstruction data may permit a concrete reframe. |
| Contrarian | What not found | Required | Absence of standards, evidence, or demand is itself important and must be documented transparently. |
| Contrarian | What changes story | Required | Clear falsifiers and success criteria are essential for an exploration rather than advocacy. |
| Futures | Calendar | Required | Near-term standards, regulatory milestones, and platform releases may shape adoption and schema choices. |
| Futures | Effects | Required | Portability, surveillance, liability, automation, and organizational memory create important second-order effects. |
| Futures | Four scenarios | Required | Success, fragmentation, compliance theater, and domain-native alternatives provide useful divergent outcomes. |
| Futures | 90-day signal | Required | A concrete short-horizon signal can make the otherwise evergreen exploration testable. |
| Futures | Under-priced | Required | Integrity, evidence decay, review labor, and exit costs are plausible overlooked issues. |
| Futures | Watch list | Required | Standards, regulators, open-source projects, observability vendors, and practitioner communities warrant monitoring. |
| Community | Where conversation lives | Required | The user explicitly requests communities and average engineers from social media. |
| Community | Sentiment | Required | The research should represent enthusiasm, pragmatism, fatigue, skepticism, and privacy concern. |
| Community | Practitioner takes | Required | Implementation and incident experience can reveal needs missed by vendor and policy sources. |
| Community | Jokes/memes | Optional | Humor may expose frustration with agent logs or “AI slop,” but only if authentic examples exist. |
| Community | Confusions | Required | Receipt, trace, log, memory, explanation, and audit trail are likely conflated in discussion. |
| Community | Before/after | Optional | Compare discourse before and after major agent frameworks or incidents if clear turning points emerge. |
| Community | Silence | Required | Identify absent operators, data subjects, non-US engineers, and regulated-domain practitioners. |
| Conspiracy | Topic-level read | Skip | This is a technical design hypothesis with no meaningful hidden-hand landscape in the source. |
| Conspiracy | The theories in circulation | Skip | No conspiracy theory, covert event, or disputed official narrative is identified. |
| Conspiracy | Where they live | Skip | There is no evidenced conspiracy community to map for this narrow technical artifact. |
| Conspiracy | Evidence audit | Skip | A conspiracy evidence audit would manufacture a frame absent from the topic. |
| Conspiracy | Who benefits from each framing | Skip | Stakeholder incentives belong in the required stakeholder and contrarian work, not a conspiracy frame. |
| Conspiracy | Adjacent priors | Skip | Broad mistrust of big tech is insufficient to justify a conspiracy landscape here. |
| Conspiracy | Mainstream cross-over | Skip | No hidden-hand claim has crossed into mainstream coverage in the source. |
| Conspiracy | Gaps in the official account | Skip | There is no official event account to interrogate; the source is an unpublished proposal. |
| Conspiracy | The strongest case among the theories | Skip | No supported theories are in scope. |
| Conspiracy | The most amplified but least evidenced | Skip | Ranking amplification would be artificial without an identified theory landscape. |
