# Contrarian research: the receipt may be the wrong boundary

## Bottom line

The strongest case against an agent receipt is not that post-task evidence has no value. It is that a receipt can become a neat, agent-authored summary of evidence that is already incomplete, mutable, sensitive, or unactionable. In that form it is neither the source of truth nor an independent attestation. It is an index written by the subject of the audit.

The draft is strongest when it asks for the *smallest useful record*. It becomes weaker if the proposed YAML is treated as proof. Existing work draws three boundaries that the prototype currently collapses:

1. **Authenticity is not truth.** A signature can establish who made a statement and whether it was altered. The IETF SCITT architecture explicitly warns that a signed statement can still contain false assertions and that a valid receipt does not make its contents trustworthy ([IETF SCITT](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html)).
2. **Telemetry is not explanation.** Traces can reconstruct calls, timings, tools, inputs, and outputs, but do not expose why a model produced a particular result. That distinction is visible in a Hacker News argument begun on 2024-02-14 over whether “LLM observability” is just conventional service telemetry ([Hacker News](https://news.ycombinator.com/item?id=39371297)), and it echoes Cynthia Rudin's warning that post-hoc explanations of black boxes can be misleading in high-stakes settings ([Nature Machine Intelligence](https://doi.org/10.1038/s42256-019-0048-x)).
3. **Possession is not usability.** A record only creates leverage if someone can retrieve, interpret, and act on it. The Cyber Safety Review Board found that few organizations analyzed the voluminous `MailItemsAccessed` records relevant to the Storm-0558 intrusion, while the U.S. State Department's custom rules and enhanced logging helped it detect the attack ([CISA/CSRB report](https://www.cisa.gov/sites/default/files/2025-03/CSRBReviewOfTheSummer2023MEOIntrusion508.pdf)).

The contrarian design is therefore: keep authoritative events in domain systems; make privileged actions least-privileged, reversible, and independently recorded; then generate a small, disposable, portable index pointing to those records. Call it a receipt only if the name does not imply more assurance than it provides.

## Competing explanations

The draft assumes that completed agent work is hard to trust because a durable post-task artifact is missing. Several rival explanations fit the same symptoms.

| Competing explanation | Evidence that supports it | What would falsify it |
|---|---|---|
| **This is primarily a control-plane problem, not a documentation problem.** Agents are hard to trust because they have excessive authority or can perform irreversible actions, not because their summaries are missing. | NIST puts least privilege, privileged-function logging, separation of audit privileges, and protection against modification at the center of accountable systems ([NIST SP 800-171r3](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/800-171r3/NIST.SP.800-171r3.html)). A receipt written after an over-privileged action does not reduce the blast radius. | In a controlled experiment where authority and reversibility are held constant, reviewers using receipts reconstruct failures or catch policy violations substantially more often than reviewers using domain audit records alone. |
| **This is a retrieval and review-interface problem.** The evidence already exists, but people cannot find the relevant signal in the volume. | The Storm-0558 review describes both the value of enhanced logs and the difficulty of analyzing voluminous records, especially for smaller organizations ([CISA/CSRB report](https://www.cisa.gov/sites/default/files/2025-03/CSRBReviewOfTheSummer2023MEOIntrusion508.pdf)). Twitter reported that logging with poor query capacity had weak adoption; after moving to a stronger query platform it ingested four times more data, though 90% had previously been rate-limited away ([Twitter engineering](https://blog.x.com/engineering/en_us/topics/infrastructure/2021/logging-at-twitter-updated)). | A receipt outperforms a tuned search, correlation, and trace interface on review time and reconstruction accuracy, rather than merely duplicating its selected fields. |
| **This is an integrity and chain-of-custody problem.** A self-reported summary is weak because the actor or compromised runtime can omit or alter incriminating events. | SCITT states that transparency does not prevent dishonest issuers and that a signed statement's contents can still be false ([IETF SCITT](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html)). OMNILOG found that existing audit architectures can leave logs unprotected long enough for an attacker to tamper with them ([USENIX Security 2023](https://www.usenix.org/conference/usenixsecurity23/presentation/gandhi)). | Independently captured and co-signed receipt fields make omission or contradiction reliably detectable, including when the agent runtime is compromised. |
| **This is an organizational accountability problem.** Structured records are collected, but ownership, review, correction, and consequences remain unclear. | In its report published on 2023-12-12, GAO found that only five of 20 reviewed federal agencies supplied comprehensive information for every reported AI use case; the other 15 had incomplete or inaccurate inventory data ([GAO-24-105980](https://www.gao.gov/products/gao-24-105980)). The problem survived a formal inventory requirement. | Receipts are regularly reviewed by a named decision-maker, trigger measurable corrective action, and remain accurate without a growing reconciliation bureaucracy. |
| **This is a standards and portability problem.** The receipt may become one more schema layered over unstable or vendor-specific telemetry. | OpenTelemetry maintainers are still resolving basic event-body versus attribute semantics, including the fact that payloads may be redacted, truncated, enriched, or replaced by references in transit ([OpenTelemetry issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)). An OpenAI Agents SDK user found that disabling the default exporter also disabled a local MLflow tracer until processors were manually reset ([OpenAI Agents issue #1387](https://github.com/openai/openai-agents-python/issues/1387)). | Two independent agent stacks emit semantically equivalent receipts that a third-party reviewer can consume and verify without adapter code or loss of evidence. |
| **This is a verification problem, not an explanation problem.** The useful question is whether the result satisfies independent criteria, not whether an agent can narrate what it did. | Rudin argues that post-hoc explanations of high-stakes black-box models can perpetuate bad practice and mislead, advocating inherently interpretable systems instead ([Nature Machine Intelligence](https://doi.org/10.1038/s42256-019-0048-x)). | Receipt explanations, blind to outcome labels, predict independently measured correctness and reveal defects that domain-specific verification misses. |

These alternatives do not eliminate the case for a receipt. They change its role. A receipt should be evaluated against controls, retrieval, independent capture, and domain verification—not against the weakest alternative of “no record at all.”

## Whose interests the receipt framing serves

### Agent-platform and observability vendors

Standardizing a receipt can create a new ingestion surface, dashboard, retention tier, and switching cost. OpenAI's Agents SDK traces generations, tool calls, handoffs, and guardrails by default, and allows processors to send traces to other destinations ([OpenAI Agents tracing documentation](https://github.com/openai/openai-agents-python/blob/main/docs/tracing.md)). That is useful capability, but it also means the platform's default data model can become the de facto record of work. The same documentation notes that tracing is unavailable for organizations using Zero Data Retention, exposing a direct tension between “keep evidence” and “do not retain data.”

The vendor interest does not invalidate the feature. It does mean that claims of portability should be tested through actual exit and re-import, not inferred from YAML syntax.

### Compliance, risk, insurers, and management

A uniform receipt makes heterogeneous activity easier to count, sample, and present. It can lower the cost of demonstrating that a process exists. But it also makes “field present” easy to confuse with “control effective.” The FTC has warned that algorithmic assessments need recognized standards, meaningful documentation, independent and protected auditors, and cannot substitute for enforcement or remedies ([FTC report to Congress](https://www.ftc.gov/system/files/ftc_gov/pdf/Combatting%20Online%20Harms%20Through%20Innovation%3B%20Federal%20Trade%20Commission%20Report%20to%20Congress.pdf)).

Managers can also repurpose task evidence as worker monitoring. Microsoft removed user names and individual activity from Productivity Score after feedback, shifting several measures to organizational aggregation ([Microsoft, 2020-12-01](https://www.microsoft.com/en-us/microsoft-365/blog/2020/12/01/our-commitment-to-privacy-in-microsoft-productivity-score/)). The lesson is not that all activity evidence becomes surveillance; it is that a system's stated purpose does not constrain its later use.

### Engineers and operators

Engineers gain faster debugging, a handoff artifact, and potentially a portable operational history. They also pay the instrumentation tax: schema updates, redaction rules, broken pointers, storage budgets, access requests, migrations, and alerts about the evidence pipeline itself. OpenTelemetry's event-semantics discussion shows that even mature standards must trade queryability, payload size, backend limits, redaction, and correlation ([issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)).

The burden will be uneven. Large organizations can staff a telemetry platform. Small teams may home-build the minimum or abandon it. In the Reddit discussion below, engineers describe both choices.

### Auditors, incident responders, and affected people

These groups benefit only if the artifact is accessible, intelligible, complete enough for their question, and contestable. An affected person may need the evidence behind a decision and a correction route, while an operator may need call timing and tool parameters. One universal receipt can privilege the operator's question and omit the affected person's.

Privacy law also creates a countervailing interest in deletion. GDPR Article 5 requires purpose limitation, data minimisation, accuracy, and storage limitation for personal data ([EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/?qid=1494678401079&uri=CELEX%3A32016R0679)). “Retain it in case of audit” is not a complete retention policy.

## Receipts the source omits or downplays

The draft usefully names uncertainty, surveillance, cost, and portability as questions, but its compact example downplays the following evidence:

- **The producer problem.** `verification: passed` does not say who verified which claim against what test, nor whether the verifier was independent. SCITT's threat model is the clearest warning: authenticated statements may still be false ([IETF SCITT](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html)).
- **The omission problem.** A summary cannot reveal an event it never captured. OMNILOG's analysis of 164 proof-of-concept kernel exploits found that inefficient audit pipelines can miss attack events and leave records open to tampering ([USENIX paper](https://www.usenix.org/system/files/usenixsecurity23-gandhi.pdf)). Agent traces have a different threat model, but the general failure is relevant: collection completeness must be demonstrated, not declared.
- **The transformation problem.** OpenTelemetry maintainers note that event bodies can be enriched, redacted, truncated, post-processed, or replaced by external references, so the received body cannot be guaranteed identical to the produced one ([OpenTelemetry issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)). A receipt needs lineage for its own transformations.
- **The sensitive-data default.** The OpenAI Agents SDK collects a comprehensive run record and traces by default; its generation and function spans can include inputs and outputs ([OpenAI Agents tracing documentation](https://github.com/openai/openai-agents-python/blob/main/docs/tracing.md)). A receipt that points to such traces inherits their prompt, tool-argument, customer-data, and secret-handling risks.
- **The subject's right to deletion or correction.** A stable evidence pointer can conflict with minimisation, accuracy, and storage limitation when it resolves to personal data ([GDPR Article 5](https://eur-lex.europa.eu/legal-content/EN/TXT/?qid=1494678401079&uri=CELEX%3A32016R0679)). Broken references may sometimes be the intended outcome of compliant deletion.
- **The review-labor problem.** Retention does not create review capacity. The CSRB account of Storm-0558 shows that access to detailed logs mattered, but so did custom detection rules and the ability to analyze them ([CISA/CSRB report](https://www.cisa.gov/sites/default/files/2025-03/CSRBReviewOfTheSummer2023MEOIntrusion508.pdf)).
- **The institutional-quality problem.** GAO's review published on 2023-12-12 shows that a mandated, structured AI inventory can remain incomplete and inaccurate across most reviewed agencies ([GAO-24-105980](https://www.gao.gov/products/gao-24-105980)). A receipt can become compliance theater unless reconciliation and accountability are explicit.
- **The adoption problem.** Even supply-chain provenance standards have had to reduce ambition. SLSA v1.0 was deliberately simpler, more practical, and “less ambitious” than v0.1 after early-adopter feedback ([SLSA v1.0 changes](https://slsa.dev/spec/v1.0/whats-new)). A maximal agent evidence schema is likely to repeat this cycle.
- **The semantic-precision problem.** `outcome`, `evidence`, `verification`, and `reversible` look portable while leaving their meaning local. `reversible: true` could mean a compensating transaction exists, a rollback was tested, or someone merely believes reversal is possible.
- **The cost boundary.** The example's `cost: 0.18` counts model execution but not telemetry ingestion, evidence storage, index maintenance, redaction, access review, incident search, or migration. It risks measuring the easy cost and hiding the ownership cost.

## Community pulse: dissent edition

These are individual practitioner comments, not a representative survey. I used them as hypotheses and friction reports, not prevalence estimates. Dates are the dates shown on the linked posts or threads. “Stake” records disclosed interests where visible; absence of a disclosed affiliation is not proof of independence.

### Hacker News — observability may be ordinary telemetry with AI branding

- **2024-02-14 — `tracerbulletx`:** “Pretty sure this just structures logs for requests to common 3rd party LLM providers.” ([direct thread](https://news.ycombinator.com/item?id=39371297)) **Stake:** HN commenter evaluating an LLM-observability launch; no affiliation disclosed.
- **2024-02-14 — `Aqueous`:** “This is just normal system / service observability.” ([direct thread](https://news.ycombinator.com/item?id=39371297)) **Stake:** HN commenter concerned that telemetry is being confused with introspection; no affiliation disclosed.

The same thread contains useful counter-evidence. A Langfuse founder argued that ordinary observability should not be reinvented but that evaluation and iterative LLM workflows add value beyond traces. This is an interested source, but it narrows the product claim rather than rejecting the tooling ([Hacker News](https://news.ycombinator.com/item?id=39371297)).

### Reddit — small teams often choose a homemade minimum

- **2024-05-19 — `WolvesOfAllStreets`:** “Instead, we created our own rules-based/naive functions (quicker, cost nothing).” ([r/MachineLearning thread](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/)) **Stake:** engineer who says they added LLM features to existing products; no vendor affiliation disclosed.
- **2024-05-19 — `Best-Association2369`:** “We've looked at dozens and at the end of the day just rolled a mini one for our needs.” ([r/MachineLearning thread](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/)) **Stake:** practitioner describing their team's tool evaluation; no affiliation disclosed.

The thread is divided rather than uniformly negative. Other engineers report that tracing, cost monitoring, prompt versions, and live-interaction review are valuable, while several say the market is early or product differentiation is weak. That mixed response supports a small prototype, but not a universal schema claim.

### GitHub — interoperability and fidelity fail at mundane seams

- **2024-12-10 — `lmolkova`:** “we cannot provide any guarantees that the body received is exactly the same as the body produced.” ([OpenTelemetry issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)) **Stake:** OpenTelemetry member and issue author working on event semantics.
- **2025-08-07 — `asmith26`:** “unfortunately these seem to disable my MLflow tracer also?” ([OpenAI Agents issue #1387](https://github.com/openai/openai-agents-python/issues/1387)) **Stake:** SDK user running a local MLflow tracer; no vendor affiliation disclosed.

Neither report is a dramatic agent failure. That is why they matter. Portability often fails through exporters, defaults, field semantics, processors, and transformations rather than through the YAML syntax itself.

### X — the clearest signal found was promotional, not independent

- **2026-03-02 — `@kmeanskaran`:** “Designed admin monitoring panel to detect data drift, agent observability, and logs.” ([direct post](https://x.com/kmeanskaran/status/2028550567002509357)) **Stake:** builder promoting a project and related articles; not independent user evidence.
- **2026-03-26 — `@RetardedNi85688`:** “The boring stuff every developer needs when deploying agents that spend real money.” ([direct post](https://x.com/RetardedNi85688/status/2037210970309705914)) **Stake:** account promoting an agent-payment product/token; not independent user evidence.

These X posts are counter-signals, not dissent: builders believe spend controls and audit logs are marketable when agents can move money. But both are seller-side claims. I did not find a credible, independent X thread with measured evidence that a post-task receipt reduced review time, incident duration, or audit cost. That absence limits what can be inferred from X.

## Quantitative reframes

### “A record exists” is a much weaker threshold than “the record works”

- **5 of 20 versus 15 of 20:** GAO found comprehensive information for every reported AI use case at only five of 20 reviewed agencies; 15 had incomplete or inaccurate data ([GAO-24-105980, 2023-12-12](https://www.gao.gov/products/gao-24-105980)). If a receipt program achieved a similar completeness rate, a clean schema would mostly standardize incompleteness.
- **164 exploit cases:** OMNILOG's researchers examined 164 proof-of-concept kernel exploits when assessing audit-event coverage ([USENIX paper](https://www.usenix.org/system/files/usenixsecurity23-gandhi.pdf)). Their example timing is stark: a prior mechanism could take 15 ms to protect logs while a naive attacker took about 5 ms to tamper with them. Agent workloads are not kernel exploits, but the reframe is transferable: integrity depends on when and where evidence becomes independent of the actor.
- **90% discarded:** Twitter reported that its earlier central logging service ingested roughly 600,000 events per second per data center while rate limiting discarded about 90% of submitted logs ([Twitter engineering, 2021-08-13](https://blog.x.com/engineering/en_us/topics/infrastructure/2021/logging-at-twitter-updated)). A receipt referencing a “trace” needs to disclose sampling, truncation, and loss rather than imply completeness.
- **Four times more logging did not by itself prove better outcomes:** Twitter's migration enabled four times more ingestion and better querying and adoption, but the engineering account does not claim that volume alone produced trust ([Twitter engineering](https://blog.x.com/engineering/en_us/topics/infrastructure/2021/logging-at-twitter-updated)). The useful change bundled capacity with retrieval.

The proposed `cost: 0.18` should therefore be reframed as one term in a total-cost equation:

```text
net evidence value
= avoided reconstruction + avoided duplicate review + faster correction + safer exit
- generation - ingestion - retention - redaction - access control
- review labor - schema governance - migration - deletion - false confidence
```

No source located provides credible values for all of those terms for agent receipts. That should be treated as a result, not filled with speculative numbers.

## What I looked for and did not find

1. **No peer-reviewed evaluation of the proposed receipt shape.** I found research on audit-log integrity, interpretable models, tracing, provenance, and attestations, but no controlled comparison showing that a compact agent-authored receipt reduces mean time to resolution, audit labor, or reconstruction error.
2. **No universal, adopted post-task agent-receipt standard.** OpenTelemetry has GenAI semantic-convention work, but foundational event representation is still evolving ([issue #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)). SCITT remains a supply-chain transparency architecture and explicitly limits what its receipts prove ([IETF SCITT working group](https://datatracker.ietf.org/group/scitt/)). SLSA covers software supply-chain provenance, not general agent decisions ([SLSA](https://slsa.dev/spec/v1.0/whats-new)).
3. **No guarantee that an agent-authored receipt is complete.** Signing can make the statement attributable and tamper-evident; it cannot prove that omitted actions never occurred ([IETF SCITT](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html)).
4. **No evidence that a single receipt serves all readers.** Operator debugging, compliance sampling, incident forensics, managerial oversight, and affected-person contestation require different evidence and access. NIST's own audit guidance makes event selection and additional record content organization-defined rather than universal ([NIST SP 800-171r3](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/800-171r3/NIST.SP.800-171r3.html)).
5. **No neutral social-media sentiment estimate.** The community sources are self-selected discussions. X search especially surfaced builders and promoters more readily than independent operational reports. It would be misleading to turn these quotes into percentages.
6. **No demonstrated portability from syntax alone.** The GitHub issues show that exporter control and event semantics can undermine portability even when the surrounding ecosystem uses OpenTelemetry ([OpenAI #1387](https://github.com/openai/openai-agents-python/issues/1387), [OpenTelemetry #1651](https://github.com/open-telemetry/semantic-conventions/issues/1651)).
7. **No proof that more retained detail is legally safer.** GDPR's minimisation and storage-limitation duties point in the opposite direction for personal data ([EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/?qid=1494678401079&uri=CELEX%3A32016R0679)).
8. **No evidence that `verification: passed` is meaningful without an independent criterion.** The FTC's audit discussion stresses standards, auditor independence, protection, enforcement, and remedies rather than documentation alone ([FTC report](https://www.ftc.gov/system/files/ftc_gov/pdf/Combatting%20Online%20Harms%20Through%20Innovation%3B%20Federal%20Trade%20Commission%20Report%20to%20Congress.pdf)).

## What would change the story

The receipt hypothesis would become substantially stronger if a prototype demonstrated all of the following:

1. **A blind-review advantage.** Give reviewers the same completed tasks and authoritative source records. Randomly add the receipt for half. Measure reconstruction accuracy, time, missed policy violations, and false confidence.
2. **Independent field provenance.** Identity comes from the identity system, authority from the policy decision point, changes from the target system, cost from billing, and verification from a named independent check. The agent may summarize but cannot author every fact about itself.
3. **Explicit assurance levels.** Distinguish `self_reported`, `system_observed`, `independently_verified`, and `cryptographically_attested`. Do not encode all four as `passed`.
4. **Loss disclosure.** Record sampling, truncation, redaction, failed exports, missing spans, and broken evidence pointers. A partially failed receipt should fail closed for high-impact actions.
5. **Risk-tiered minimums.** A read-only summary should not retain the same evidence as a payment or production change. NIST's organization-defined event selection and performance trade-offs are a useful precedent ([NIST SP 800-171r3](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/800-171r3/NIST.SP.800-171r3.html)).
6. **A real exit test.** Export receipts and their evidence links from one platform, remove the original platform, then show that another implementation can still resolve the semantics needed for review.
7. **Privacy and contestability by construction.** Define purposes, readers, retention, redaction, deletion, and correction. Test whether an affected person can understand and challenge the relevant part without receiving secrets or irrelevant telemetry.
8. **Net-cost evidence.** Include instrumentation, retention, access review, schema evolution, and deletion—not only inference cost. The receipt creates leverage only if avoided work repeatedly exceeds all of those costs.
9. **A hostile test.** Let a red team control the agent runtime and attempt omission, equivocation, fabricated evidence, prompt injection into the receipt, and evidence-pointer substitution. SCITT's separation between authenticity and truth is the baseline to beat ([IETF SCITT](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html)).

If the receipt survives those tests, the contrarian conclusion changes: it becomes a genuinely useful evidence manifest rather than a new log format. If it does not, the more defensible principle is that trustworthy agents should leave their effects in systems that can independently prove what happened.

## Source receipts

### Primary standards, government, and regulator sources

1. [NIST SP 800-171r3, *Protecting Controlled Unclassified Information in Nonfederal Systems and Organizations*](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/800-171r3/NIST.SP.800-171r3.html) — least privilege, event selection, audit content, failure handling, and separation of audit privilege.
2. [IETF SCITT architecture draft](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-22.html) — signed-statement authenticity, transparency receipts, privacy warnings, and residual dishonest-issuer risk.
3. [SLSA, *What's new in v1.0*](https://slsa.dev/spec/v1.0/whats-new) — early-adopter pressure toward a simpler and less ambitious provenance specification.
4. [GAO-24-105980, 2023-12-12](https://www.gao.gov/products/gao-24-105980) — completeness and accuracy failures in federal AI-use inventories.
5. [FTC, *Combatting Online Harms Through Innovation*](https://www.ftc.gov/system/files/ftc_gov/pdf/Combatting%20Online%20Harms%20Through%20Innovation%3B%20Federal%20Trade%20Commission%20Report%20to%20Congress.pdf) — limits of assessments and audits without standards, independence, protection, enforcement, and remedies.
6. [EU General Data Protection Regulation, Article 5](https://eur-lex.europa.eu/legal-content/EN/TXT/?qid=1494678401079&uri=CELEX%3A32016R0679) — purpose limitation, minimisation, accuracy, and storage limitation.
7. [Cyber Safety Review Board, Storm-0558 review](https://www.cisa.gov/sites/default/files/2025-03/CSRBReviewOfTheSummer2023MEOIntrusion508.pdf) — value and practical analysis limits of detailed cloud audit logs.

### Technical and research sources

8. [OpenAI Agents SDK tracing documentation](https://github.com/openai/openai-agents-python/blob/main/docs/tracing.md) — default tracing scope, processors, destinations, and ZDR limitation.
9. [OpenTelemetry semantic-conventions issue #327, opened 2023-09-15](https://github.com/open-telemetry/semantic-conventions/issues/327) — initial proposal to represent modern AI telemetry using ordinary distributed tracing conventions.
10. [OpenTelemetry semantic-conventions issue #1651, opened 2024-12-05](https://github.com/open-telemetry/semantic-conventions/issues/1651) — unresolved body/attribute trade-offs and transformation of event payloads.
11. [OpenAI Agents SDK issue #1387, opened 2025-08-06](https://github.com/openai/openai-agents-python/issues/1387) — default exporter control interacting with a local MLflow tracer.
12. [Gandhi et al., OMNILOG, USENIX Security 2023](https://www.usenix.org/conference/usenixsecurity23/presentation/gandhi) — event coverage, synchronous protection, and tamper resistance in audit pipelines.
13. [Rudin, *Stop explaining black box machine learning models…*, 2019-05-13](https://doi.org/10.1038/s42256-019-0048-x) — limits and risks of post-hoc explanations in high-stakes decisions.
14. [Microsoft, Productivity Score privacy changes, 2020-12-01](https://www.microsoft.com/en-us/microsoft-365/blog/2020/12/01/our-commitment-to-privacy-in-microsoft-productivity-score/) — removal of user names and individual-level activity after privacy feedback.
15. [Twitter engineering, *Logging at Twitter: Updated*, 2021-08-13](https://blog.x.com/engineering/en_us/topics/infrastructure/2021/logging-at-twitter-updated) — retention, rate-limiting, query capability, adoption, and ingestion scale.

### Community sources

16. [Hacker News discussion, 2024-02-14](https://news.ycombinator.com/item?id=39371297) — operator debate over ordinary telemetry, LLM introspection, pricing, and concrete benefits.
17. [r/MachineLearning discussion, 2024-05-19](https://www.reddit.com/r/MachineLearning/comments/1cvwohz/d_are_llm_observability_tools_really_used_in/) — mixed practitioner experience with homemade and third-party LLM observability.
18. [X post by `@kmeanskaran`, 2026-03-02](https://x.com/kmeanskaran/status/2028550567002509357) — promotional builder signal for agent monitoring and logs.
19. [X post by `@RetardedNi85688`, 2026-03-26](https://x.com/RetardedNi85688/status/2037210970309705914) — promotional claim for spend controls and agent auditability.

### Search and snowball audit

I searched combinations of *agent receipt*, *agent audit trail*, *LLM observability*, *post-task artifact*, *signed attestation*, *AI inventory audit*, *audit-log failure*, *employee monitoring*, *trace portability*, and *evidence retention*. A first proper-noun pass followed OpenAI, OpenTelemetry, MLflow, Langfuse, SCITT, SLSA, NIST, FTC, GAO, CISA/CSRB, Microsoft, Twitter/X, and GDPR references. A second pass checked the cited standards, issue discussions, regulator reports, and practitioner threads for predecessor projects and contrary evidence. It did not surface a neutral controlled evaluation of a portable post-task agent receipt, so no effectiveness claim is made.
