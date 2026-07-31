# Contrarian: the case against assuming the AI platform should stay thin

Research date: 2026-07-30

Chapter 4 is exploratory rather than declarative, so there is no finished thesis to “debunk.” The proposition under test here is the direction its setup makes likely: start with a contract, keep the shared surface small, and leave most workflow-aware responsibilities with product teams unless central ownership proves its value. That is a defensible default for a small or heterogeneous organization. It is not a general result. The strongest counter-evidence says that, beyond a threshold of scale, risk, and repeated work, model access, feature/data machinery, evaluation, deployment, monitoring, authorization, and even a gateway can create more value as one integrated product than as contracts connecting locally owned parts.

## Competing explanations

| Working claim | Competing explanation | Evidence for the counter | What would falsify the working claim | Current state |
|---|---|---|---|---|
| **A contract is the best first shared capability because it preserves optionality with little central scope.** | A contract without a runtime, conformance evidence, or authoritative state is coordination theatre: it makes systems look uniform while duplicated adapters, inconsistent enforcement, and stale metadata remain. | The OpenAPI Initiative warns that its schemas do not catch every specification violation ([OpenAPI Specification](https://spec.openapis.org/oas/)). Backstage tells adopters that its catalogue should be a cache rather than the ultimate source of truth and is not ideal for dynamic real-time relationships ([Backstage catalogue graph](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)). A Backstage adopter reported successful registrations that appeared “hours to days to never,” demonstrating the difference between a declared ingest operation and observed catalogue state ([issue #13834](https://github.com/backstage/backstage/issues/13834)). | A comparative pilot in which contract-only teams retire as much duplicated integration and control work as runtime-backed teams, while maintaining fresher state and lower total operating cost. | **Counter leads** for authorization, deployment, and other runtime guarantees; **inconclusive** for discovery-only metadata. |
| **Workflow understanding is a reason to keep evaluation, integrations, deployment, and observability local.** | Local knowledge is necessary for business semantics, but local ownership of the whole stack repeatedly recreates data pipelines, serving containers, feature logic, audit paths, and monitors. The platform can own the repeatable machinery while teams supply domain tests and policies. | Uber says pre-Michelangelo teams built bespoke production systems and lacked reproducible training, experiment storage, and a standard deployment path; its centralized system now spans data, training, evaluation, deployment, serving, and monitoring ([Uber Michelangelo](https://www.uber.com/gb/en/blog/michelangelo-machine-learning-platform/)). Google's peer-reviewed TFX case reports that integration reduced time to production from months to weeks and, in one Google Play deployment, coincided with a 2% increase in installs ([TFX paper](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/)). | At comparable scale, workflow-owned implementations would need lower end-to-end labor and equal or better reliability without duplicating the shared machinery. | **Counter leads** at large-scale ML organizations; evidence is weaker for small organizations and novel workflows. |
| **Thinness best preserves engineering freedom.** | A reliable central runtime can expand practical freedom by removing infrastructure work that teams technically “own” but cannot staff, secure, or operate well. Freedom to choose every component is not the same as freedom to ship safely. | Google's Borg paper says shared cluster management achieves high utilization through admission control, task packing, overcommitment, machine sharing, and isolation—economies that independent team schedulers cannot reproduce efficiently ([Borg paper](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/)). DORA reports that internal developer platforms improve individual, team, and organizational performance, though with stability and throughput trade-offs ([DORA report](https://dora.dev/research/2024/dora-report/)). | A matched study showing that teams with broader local control deliver faster, recover better, and spend less total time on infrastructure than teams using a mature central platform. | **Roughly even.** Central capability can create freedom from toil; it can also remove freedom to escape. |
| **Identity and policy can be federated to the service that knows the workflow.** | Some controls need globally consistent semantics, causal ordering, and one answer across hundreds of services; distributing policy storage and interpretation creates permission drift and audit gaps. | Google's Zanzibar provides one authorization model to hundreds of client services, stores trillions of ACLs, serves millions of checks per second, reports less than 10 ms 95th-percentile latency, and reports availability above 99.999% over three years ([Zanzibar paper](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)). The EU AI Act requires providers of high-risk systems to maintain documented risk and quality-management systems, logs, conformity evidence, and lifecycle controls; it does not mandate one gateway, but it raises the cost of inconsistent local evidence ([Regulation (EU) 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)). | A federated design would need to demonstrate equivalent consistency, latency, audit completeness, revocation, and policy-change behavior at materially lower cost. | **Counter leads** for organization-wide authorization semantics and regulated evidence; resource-side enforcement still needs domain context. |
| **The AI platform should stop before becoming an end-to-end AI product.** | AI is exactly where economies of scope are strongest: data lineage, feature reuse, model catalogues, gateways, evaluation, safety, serving, deployment, and monitoring share state and must evolve together. Splitting them creates glue code and boundary failures. | Uber extended one centralized ML platform into generative AI with a gateway, model catalogue, evaluation framework, prompt toolkit, deployment, serving, monitoring, redaction, cost attribution, and policy controls. It reports about 400 active ML projects, more than 20,000 monthly training jobs, more than 5,000 production models, and 10 million peak real-time predictions per second ([Uber's AI journey](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/)). Its gateway was motivated by more than 60 LLM use cases and redundant integration strategies ([Uber GenAI Gateway](https://www.uber.com/en-AT/blog/genai-gateway/)). | A thin composition at similar scale would need equal time-to-production, safety coverage, provider flexibility, and unit cost with less central staffing and no larger integration burden. | **Counter leads at Uber-like scale**, but most evidence is self-reported and does not establish transferability. |
| **Federated contribution keeps the platform adaptable without a powerful centre.** | Federation can create an ownership vacuum: feature teams optimize for immediate use, do not want support obligations for other teams, and duplicate “reusable” components. A dedicated central team may be the only actor funded to design across contexts. | A multiple-case study of three large organizations found that separating product units as profit centres from a platform cost centre was associated with delayed delivery, higher defect rates, and redundant components; the organizations turned to inner source to repair the incentive problem ([Riehle et al.](https://oss.cs.fau.de/2015/05/23/inner-source-in-platform-based-product-engineering/)). A former Spotify practitioner describes two failed federated design-system attempts in which immediate local needs produced barely reused components and unclear support ownership ([Shaun Bent](https://www.shaunbent.co.uk/blog/why-federated-design-systems-keep-failing/)). | A federated platform with measured reuse, response-time obligations, funded maintainers, and lower defects than a centralized peer would reverse this result. | **Inconclusive.** The failure mechanism is credible, but the design-system account is one named practitioner's experience and not an AI-platform comparison. |

The counter does not imply “centralize everything.” It implies that **thinness must earn its place by measured total work**, just as centralization must. The chapter's current wording gives local workflow knowledge an explicit presumption but gives economies of scope, evidence consistency, and duplicated runtime work no equivalent presumption.

## Whose interests does the working framing serve

### The thin-platform framing

- **Product and domain teams** gain local priority control, provider choice, faster exceptions, and less dependence on a central backlog. They may also externalize less visible costs: duplicated integrations, divergent security controls, bespoke on-call, audit preparation, and migrations. Hacker News practitioners explicitly disagree on this boundary: one product engineer reported waiting weeks for central help, while platform-side commenters described inheriting infrastructure after local owners left ([Hacker News thread](https://news.ycombinator.com/item?id=26935504)).

- **Point-solution and open-source vendors** benefit when an organization composes a gateway, evaluation service, observability backend, catalogue, vector store, identity system, and runtime rather than selecting one integrated platform. “Composable” can preserve exit; it also maximizes the number of products, integrations, and consulting engagements required.

- **A small central platform team** benefits reputationally from a narrow promise it can meet. Thinness prevents the team becoming the owner of every workflow. It can also understate how much work falls back onto teams without ML infrastructure specialists.

- **The author and site philosophy** favour reversibility, agency, and engineering freedom. That value makes lock-in costs visible, which is useful. It can also make central operation look suspect before the alternative's repeated labor, evidence gaps, and abandonment costs are counted.

### The broad-platform counter-framing

- **Cloud and AI-platform vendors** profit when model access, evaluation, monitoring, catalogues, gateways, tools, and deployment become one purchased control plane. Their reference architectures are useful evidence of what must operate, but feature completeness is also a sales strategy. Vendor documentation should not be treated as proof of customer outcomes.

- **Spotify** is not a neutral Backstage evaluator. It reports productivity advantages for frequent users and also sells Spotify Portal, plugins, enterprise support, and consulting. Spotify itself says Backstage evolved into an enterprise business ([Spotify's enterprise-business account](https://engineering.atspotify.com/2025/04/celebrating-five-years-of-backstage)). That conflict does not make its internal measurements false; it makes methodology and counterfactuals essential.

- **Uber's Michelangelo team** has an organizational interest in presenting the integrated platform as instrumental to Uber's AI growth. The engineering posts disclose concrete architecture and scale but not the platform's headcount, fully loaded cost, dissatisfied non-users, failed migrations, or a thin-platform comparison ([Uber's AI journey](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/)).

- **Central security, privacy, risk, and audit functions** gain one place to impose baselines, retrieve logs, revoke access, and demonstrate control. This can close real gaps—NIST calls for clear executive accountability, inventories, monitoring, third-party controls, and decommissioning ([NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/))—but it can also turn administrative convenience into a universal runtime mandate.

- **Platform leaders and consultants** can grow remit, budget, and headcount by defining more work as platform work. Conversely, product leaders can protect headcount and roadmap control by defining the same work as domain-specific. Neither organizational label is evidence about total value.

The honest conflict map is therefore symmetric: **thinness serves autonomy and composable suppliers; breadth serves central operators and integrated suppliers**. The correct boundary cannot be inferred from the advocate's title.

## Receipts the source omitted or downplayed

| Receipt | Where it lives | Why it complicates the framing | Evidence limit / why it may be absent |
|---|---|---|---|
| **An end-to-end AI platform can become the default rather than a cage.** Uber reports that Michelangelo grew from standard ML into a control plane, offline and online data planes, GenAI gateway, catalogue, evaluation, prompts, deployment, and monitoring at substantial production scale ([Uber](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/)). | Named engineering architecture and operating figures | Directly challenges a capability-by-capability presumption of local ownership; the components can compound because they share lifecycle state and evidence. | Company self-report, no independent cost or counterfactual. Chapter 4 is still a question list and may simply not have reached cases yet. |
| **Integration can produce measured business improvement.** The peer-reviewed TFX paper says ad hoc team glue created duplicated effort and fragile systems; one integrated deployment shortened production lead time from months to weeks and reported a 2% increase in Google Play installs ([TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/)). | Google Research / KDD case study | This is stronger than generic platform advocacy because it gives a concrete deployment outcome and identifies duplication before integration. | One company and one highlighted deployment; not an AI-agent platform and not a thin-vs-broad experiment. |
| **Central authorization can meet a scale and consistency problem that contracts cannot.** Zanzibar serves hundreds of Google services with global consistency and reported production SLOs ([Zanzibar](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)). | Google Research / USENIX paper | Weakens the claim that workflow ownership naturally implies local authorization machinery. A service can keep domain policy while sharing the consistency engine. | Google scale is exceptional; a smaller organization may buy rather than build this capability. |
| **Shared scheduling yields physical economies of scope.** Borg combines heterogeneous workloads, admission control, packing, overcommitment, and machine sharing to improve utilization ([Borg](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/)). | Google Research / EuroSys paper | Some platform value comes from pooled capacity, not just interface reuse. A contract cannot create these utilization gains. | Compute orchestration is older than GenAI; the analogy is strongest for shared inference and weakest for domain evaluation. |
| **The best broad evidence also reports harm.** DORA says internal platforms are associated with better individual, team, and organizational performance but with decreased change stability and throughput ([DORA](https://dora.dev/research/2024/dora-report/)). | Cross-organization survey report | Rejects both slogans: “platforms always help” and “thinness always preserves speed.” Implementation and developer independence mediate the result. | Observational survey; the public summary does not isolate platform breadth or AI-specific capabilities. |
| **The strongest Backstage numbers lack a non-user control.** Spotify says frequent users deploy twice as often and software stays deployed three times as long, but its methodology page says high adoption made a non-user control group impossible and the analysis was observational ([Spotify methodology](https://backstage.spotify.com/discover/blog/how-spotify-measures-the-value-of-backstage)). | Spotify's methodology disclosure | The headline can reflect selection: already productive developers may use Backstage more. It is evidence of association, not proof that a portal caused the difference. | Spotify deserves credit for disclosing the limitation; the chapter omitted the case entirely rather than selectively quoting it. |
| **Catalogue freshness and validation are operational problems.** Backstage says the catalogue is a cache, while users have reported registrations that never appear and malformed metadata producing misleading warnings ([Backstage docs](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/), [issue #13834](https://github.com/backstage/backstage/issues/13834), [issue #25622](https://github.com/backstage/backstage/issues/25622)). | Official documentation and public issue tracker | A contract-plus-catalogue start can create false assurance unless observed state, failure reporting, and ownership repair are part of the product. | Bugs are not adoption-wide failure rates; public issues overrepresent problems. |
| **Protocol metadata cannot carry the safety burden.** MCP says tool annotations are untrusted unless their servers are trusted, and its security guidance identifies confused-deputy, token-passthrough, SSRF, session, and prompt-injection risks ([MCP tools](https://modelcontextprotocol.io/specification/2025-06-18/server/tools), [MCP security](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)). | Protocol specification and security guide | Defining how tools are exposed is not enough for high-consequence execution; some host, gateway, sandbox, or resource service must enforce. | MCP does not prescribe that enforcement be one central platform. The receipt argues for runtime ownership, not necessarily central ownership. |
| **Federation has incentive failure modes, not only technical ones.** The three-company inner-source study found platform cost-centre/product profit-centre separation associated with delay, defects, and redundant components ([Riehle et al.](https://oss.cs.fau.de/2015/05/23/inner-source-in-platform-based-product-engineering/)). | IEEE multiple-case research summary | Local contribution does not become reusable merely because a contract exists; support incentives and funding determine whether teams maintain shared assets. | The study examines product platforms and inner source, not current AI platforms. |
| **Regulatory evidence can make a common evidence plane valuable.** The EU AI Act requires continuous risk management, quality management, logs under provider control, conformity assessment, corrective action, and documented responsibility for high-risk systems ([Regulation (EU) 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)). | EUR-Lex official regulation | Repeating these mechanisms independently across teams can be expensive and inconsistent; a shared evidence service has an economy of scope. | The law mandates outcomes and responsibilities, not a central AI platform. Claiming otherwise would be vendor overreach. |

### What these receipts actually support

The evidence supports a **scale- and risk-contingent** result, not maximal centralization. Integrated platforms have credible successes where the same organization runs many models, shares compute and features, needs consistent authorization, or must produce lifecycle evidence. Contracts and catalogues are demonstrably insufficient as enforcement or real-time truth. At the same time, the public evidence is unusually concentrated in Google, Uber, and Spotify—organizations large enough to build platforms and motivated to publicize them.

## Community pulse, dissent edition

These are exact, attributable practitioner statements, not a representative opinion poll. “Dominant” below means the recurring dissenting read in the sampled thread or issue cluster; it does not mean every user of the platform agrees.

### Hacker News: local ownership can externalize operations back to platform teams

**Dominant dissenting view in the sampled thread:** the central team is not always hoarding control; it is often defending itself against unsupported infrastructure that product teams create and later hand off. This cuts against the chapter's implication that the team closest to the workflow is naturally the best long-term owner.

- `dilyevsky`, 2021-04-26: “Platform don’t want control they just don’t want to inherit infra” ([comment](https://news.ycombinator.com/item?id=26939387)). **Stake:** adjacent; commenting from platform/product engineering experience.

- `blabitty`, 2021-04-26: “product engineers ask for full root permissions when they need 5%” ([comment](https://news.ycombinator.com/item?id=26939491)). **Stake:** adjacent; reports direct experience with product-engineer access requests.

The same thread contains strong criticism of platform backlogs and abstraction, so the honest read is not pro-central consensus. Its contrarian contribution is that local agency has an operational tail: abandoned systems, excessive privileges, and handoff work ([full thread](https://news.ycombinator.com/item?id=26935504)).

### Reddit `r/devops`: shared machinery is the point, not a regrettable expansion

**Dominant dissenting view in the sampled thread:** once many teams repeat the same operational work, broad self-service and paved paths are not “platform bloat”; they are the mechanism that removes the bottleneck.

- `lucidguppy`, 2023-12-11: “80% of this stuff is common between solutions - so put that shit behind a button.” ([comment](https://www.reddit.com/r/devops/comments/18fshs8/comment/kcwc1nx/)). **Stake:** adjacent; practitioner discussing platform scope.

- `foresterLV`, 2023-12-11: “platform engineering gives developers platform/tools to do it themself. both solve bottlenecks and efficiency.” ([comment](https://www.reddit.com/r/devops/comments/18fshs8/comment/kcxd9je/)). **Stake:** adjacent; practitioner comparing DevOps staffing with platform self-service.

This thread also calls the label hype and warns against overbuilding. The dissent from a thin default is narrower: repeated operational capabilities can belong behind one self-service surface even when product teams retain code and outcome ownership.

### GitHub Backstage issues: descriptive contracts fail without operational truth and enforced permissions

**Dominant dissenting view in the sampled issue cluster:** a catalogue or permission contract that ingests slowly, reports the wrong validation failure, or delegates enforcement to adopter configuration is not a safe minimum. The shared product must own enough runtime behavior to make its promise true.

- `dayadev`, 2022-09-23: “Taking too long for the registered entity to show up in the catalog. sometimes from hours to days to never.” ([Backstage issue #13834](https://github.com/backstage/backstage/issues/13834)). **Stake:** direct; Backstage adopter reporting production-like catalogue behavior.

- `Joonpark13`, 2022-09-28: “authorization is happening inside the policy instead of inside the plugin. This is an anti-pattern” ([Backstage issue #13891](https://github.com/backstage/backstage/issues/13891)). **Stake:** direct; contributor/adopter analyzing a permission-framework integration.

GitHub issues are biased toward failure and cannot supply incidence rates. They are still valuable mechanism evidence: contracts do not repair stale state or enforce themselves.

## Quantitative reframes

| Framing choice | Denominator or unit implied by the chapter | Honest alternative | How the conclusion changes |
|---|---|---|---|
| **Count central capabilities as scope and local capabilities as freedom.** | Number of functions the platform owns | **Total engineering work per production model or agent**, including duplicated pipelines, adapters, serving, security review, on-call, evidence, and migration | Google's TFX case says integration moved production lead time from months to weeks and one deployment improved installs by 2% ([TFX](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/)). On this denominator, a broad platform can be smaller than many “thin” copies. |
| **Count one central authorization service as a dependency.** | Number of central runtime hops | **Successful consistent checks per unit of latency and availability**, plus the number of services that avoid implementing the machinery | Zanzibar reports millions of requests per second, trillions of ACLs, less than 10 ms 95th-percentile latency, above 99.999% availability over three years, and hundreds of client services ([Zanzibar](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)). At that scale, central machinery is an economy, not merely coupling. |
| **Count platform breadth, not repeated demand.** | Gateway + catalogue + evaluation + deployment + monitoring looks like five central capabilities | **Active projects, models, training jobs, inference volume, and duplicated integrations served by the same lifecycle** | Uber reports about 400 active projects, more than 5,000 production models, more than 20,000 training jobs each month, and 10 million peak predictions each second; its gateway began after more than 60 LLM use cases exposed redundant integration ([Uber platform](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/), [Uber gateway](https://www.uber.com/en-AT/blog/genai-gateway/)). Breadth looks less extravagant when divided by this demand, but the missing denominator is platform headcount and cost. |
| **Treat frequent-user outcomes as platform-caused outcomes.** | Frequent Backstage users versus less-frequent users | **Assigned or credibly matched exposure, with pre-period productivity, task mix, seniority, and team quality controlled** | Spotify reports frequent users are 2.3 times as active in GitHub, make twice as many code changes in 17% less cycle time, deploy twice as often, and keep software deployed three times as long; it also says no non-user control was possible ([Spotify metrics and methodology](https://backstage.spotify.com/discover/blog/how-spotify-measures-the-value-of-backstage)). The result changes from “Backstage caused productivity” to “usage strongly correlates with productivity.” |
| **Use adoption or feature count as platform success.** | Teams onboarded, catalogue entities, gateway calls, or capabilities shipped | **Net delivery outcome after stability, throughput, exception time, and platform/support labor** | DORA finds better individual, team, and organizational performance alongside decreased change stability and throughput for internal-platform users ([DORA](https://dora.dev/research/2024/dora-report/)). A platform can win its adoption KPI while losing a delivery-system KPI. |
| **Treat three local implementations as three expressions of freedom.** | Number of autonomous team solutions | **Reuse per component, defect rate, delay, and unfunded support obligations** | The three-company inner-source study links the platform-cost-centre/product-profit-centre split with delayed deliveries, defects, and redundant components ([Riehle et al.](https://oss.cs.fau.de/2015/05/23/inner-source-in-platform-based-product-engineering/)). Local variety becomes waste when the variants solve the same problem and no owner is funded for reuse. |

No source above supplies the decisive denominator: **fully loaded annual cost per successful, governed, replaceable workflow outcome**. That missing number is more important than the count of platform features.

## What I looked for and did not find

1. **A matched, longitudinal comparison of contract-only, integrated-runtime, federated, and vendor-managed AI platforms.** Queries for `"thin platform" versus "integrated platform" empirical study developer platform`, `"contract-only" AI platform case study failure`, and federated-platform comparisons returned advocacy, vendor cases, or adjacent product-platform research—not a controlled comparison.

2. **A causal Backstage productivity study with a true non-user control.** Spotify's own methodology says adoption was too high to construct that control and explicitly labels the method observational ([Spotify methodology](https://backstage.spotify.com/discover/blog/how-spotify-measures-the-value-of-backstage)). Searches surfaced vendor and CNCF case studies but no independent replication using random assignment or a credible natural experiment.

3. **Public fully loaded cost for Michelangelo, TFX, Zanzibar, or Backstage.** The architecture reports publish traffic, adoption, and outcomes, but not central headcount, on-call load, cloud cost, product-team integration time, abandoned use cases, exception queues, or decommissioning cost. Without this, “economy of scope” remains plausible but not priced.

4. **A public incidence rate for stale catalogue metadata or failed permission integrations.** GitHub issues show real mechanisms, not prevalence. There is no denominator of total registrations, entities, installations, or permission decisions against which to interpret issue counts.

5. **A regulation that requires one central AI gateway or platform.** Regulation (EU) 2024/1689 requires risk management, quality management, logging, conformity, and accountability for covered systems, but leaves architecture open ([EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)). Vendor claims that regulation itself mandates a gateway would overstate the record.

6. **A broad-platform failure corpus published by the platform owners.** Searches for integrated AI-platform failure and central ML-platform postmortems produced many general outages and security advisories, but few candid, scoped postmortems from internal AI-platform teams. The evidence base is publication-biased toward launch architecture and success.

7. **Evidence that a schema or catalogue alone reduced AI incidents.** OpenAPI and Backstage documentation explain representation and ingestion; MCP specifies discovery metadata. I did not find a comparative incident study showing that descriptive contracts without admission or runtime enforcement materially reduced harm.

8. **Evidence that federation reliably preserves exit.** Federation can reduce one central dependency, but the studies and practitioner accounts surfaced coordination, support, and duplication problems. I found no quantified switching-time comparison proving that federated ownership made a capability cheaper to remove.

These absences do not prove the thin thesis false. They lower confidence in any universal answer and show why successful-company architecture posts should be treated as hypotheses with operating receipts, not templates.

## What would change the story

One evidence item would force a rewrite: **a preregistered, multi-organization, two-year matched comparison of the same AI capability operated as contract-only, central runtime, federated control, and vendor-managed service, stratified by organization scale and workflow risk, that publishes platform and product-team labor, lead time, throughput, stability, incidents, exception latency, audit findings, provider-switch time, decommissioning cost, and user-reported agency**.

If contract-only or federated designs produced equal governed outcomes with lower total labor and faster exit, the lede should favour thinness. If integrated platforms consistently retired more work, improved safety, and preserved acceptable switching time, the lede should say the platform should be broad once repeated demand crosses a measurable threshold. Nothing in the current public record meets that bar.

## Source receipts

### Critic

- [DORA report: platform benefits with stability and throughput trade-offs](https://dora.dev/research/2024/dora-report/)
- [Machine Learning: The High Interest Credit Card of Technical Debt](https://research.google/pubs/machine-learning-the-high-interest-credit-card-of-technical-debt/)
- [Inner Source in Platform-Based Product Engineering](https://oss.cs.fau.de/2015/05/23/inner-source-in-platform-based-product-engineering/)
- [Why Federated Design Systems Keep Failing](https://www.shaunbent.co.uk/blog/why-federated-design-systems-keep-failing/)

### Regulator

- [Regulation (EU) 2024/1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32024R1689)
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)

### Audit

- [Spotify's Backstage measurement methodology and control-group limitation](https://backstage.spotify.com/discover/blog/how-spotify-measures-the-value-of-backstage)
- [Backstage catalogue graph and source-of-truth guidance](https://backstage.io/docs/features/software-catalog/creating-the-catalog-graph/)
- [OpenAPI schema limitations](https://spec.openapis.org/oas/)
- [MCP tool specification](https://modelcontextprotocol.io/specification/2025-06-18/server/tools)
- [MCP security best practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)

### Community

- [Hacker News: product/platform ownership thread](https://news.ycombinator.com/item?id=26935504)
- [Hacker News comment by `dilyevsky`](https://news.ycombinator.com/item?id=26939387)
- [Hacker News comment by `blabitty`](https://news.ycombinator.com/item?id=26939491)
- [Reddit `r/devops`: platform engineering hype](https://www.reddit.com/r/devops/comments/18fshs8/)
- [Reddit comment by `lucidguppy`](https://www.reddit.com/r/devops/comments/18fshs8/comment/kcwc1nx/)
- [Reddit comment by `foresterLV`](https://www.reddit.com/r/devops/comments/18fshs8/comment/kcxd9je/)
- [Backstage issue #13834 by `dayadev`](https://github.com/backstage/backstage/issues/13834)
- [Backstage issue #13891 by `Joonpark13`](https://github.com/backstage/backstage/issues/13891)
- [Backstage issue #25622 by `awanlin`](https://github.com/backstage/backstage/issues/25622)

### Counter-press

- [Uber: From Predictive to Generative—Michelangelo's integrated AI platform](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/)
- [Uber: GenAI Gateway](https://www.uber.com/en-AT/blog/genai-gateway/)
- [Uber: original Michelangelo architecture and motivation](https://www.uber.com/gb/en/blog/michelangelo-machine-learning-platform/)
- [Spotify: Backstage as an enterprise business](https://engineering.atspotify.com/2025/04/celebrating-five-years-of-backstage)

### Quantitative reframe

- [TFX production-scale ML platform paper](https://research.google/pubs/tfx-a-tensorflow-based-production-scale-machine-learning-platform/)
- [Zanzibar global authorization paper](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)
- [Borg cluster-management paper](https://research.google/pubs/large-scale-cluster-management-at-google-with-borg/)
- [Uber's current Michelangelo scale](https://www.uber.com/us/en/blog/from-predictive-to-generative-ai/)
- [Spotify Backstage metrics and disclosed methodology](https://backstage.spotify.com/discover/blog/how-spotify-measures-the-value-of-backstage)

### Snowball audit

Round one followed the named technologies and organizations that directly bear on the chapter: MCP, Backstage, OpenAPI, DORA, NIST, the European Union, Uber Michelangelo, Google TFX, Google Borg, Google Zanzibar, Spotify, and Team Topologies-adjacent platform research. Round two followed entities surfaced by those records: Uber's GenAI Gateway, Google Play, the OpenAPI Initiative, EUR-Lex, the Backstage issue reporters, the Spotify commercial Portal and plugins business, Hacker News commenters, Reddit `r/devops` commenters, and the three-company inner-source research programme. After round two, no named parent company, regulator, platform operator, standards body, or quoted practitioner remained load-bearing but unsearched.
