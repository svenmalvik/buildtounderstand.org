# Contrarian research: “smallest” may be the wrong optimization

## Bottom line

The chapter is right to distrust feature-rich products, but its subtraction test is incomplete. A central capability can look small only because application teams, security reviewers, auditors, and non-engineer builders absorb the missing integration, validation, interface, and migration work. Conversely, a broad platform can be genuinely economical when it replaces repeated glue at sufficient scale. The strongest evidence therefore does not support one universal “smallest AI platform.” It supports minimizing **total system work per successful, governed outcome**, including work hidden outside the platform team.

There is also a naming problem. A systematic mapping study found 35 components across MLOps architectures and describes MLOps as an extension of DevOps; a CNCF/SlashData survey of more than 400 professional developers found that the most common AI approach was to extend existing cloud-native platforms with specialist tooling, not build a separate AI estate. That is strong evidence that much of the “AI platform” is existing developer, data, security, and operations capability under a new boundary. It is not the whole story: production ML interviews identify evaluation, versioning, and performance monitoring as recurring model-specific work, while OWASP identifies excessive agency as an agent-specific risk. The honest contrarian position is therefore “extend first, specialize only where behavior demands it,” not “AI changes nothing.” ([MLOps architecture mapping](https://arxiv.org/abs/2406.19847), [CNCF/SlashData technology radar](https://www.cncf.io/announcements/2026/03/24/cncf-and-slashdata-report-finds-platform-engineering-tools-maturing-as-organizations-prepare-for-ai-driven-infrastructure/), [production-ML interview study](https://arxiv.org/abs/2209.09125), [OWASP excessive agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html))

## Competing explanations

| Working claim | Competing explanation | Evidence for the counter | What would falsify the working claim | Current state |
|---|---|---|---|---|
| “Smallest” is the minimum AI capability that must be shared. | “AI platform” is mostly a new purchasing and ownership label for developer platform, DataOps, IAM, observability, CI/CD, security, and FinOps work. | The MLOps mapping study found 35 components and explicitly roots MLOps in DevOps. CNCF/SlashData found 35% using hybrid platforms that combine existing developer platforms with specialist AI tooling. Backstage’s own directory categorizes plugins under authentication, FinOps, deployment, observability, security, and machine learning—evidence of aggregation, not an independent AI stack. ([mapping study](https://arxiv.org/abs/2406.19847), [CNCF/SlashData](https://www.cncf.io/announcements/2026/03/24/cncf-and-slashdata-report-finds-platform-engineering-tools-maturing-as-organizations-prepare-for-ai-driven-infrastructure/), [Backstage plugin directory](https://backstage.io/plugins/)) | A multi-organization capability inventory showing that most recurring cost or risk cannot be handled by incumbent systems and is uniquely model- or agent-dependent. | **Counter leads**, with a narrow exception for evaluation, model/prompt/data provenance, and delegated-action controls. |
| A thin contract, template, library, or CLI is smaller than a managed platform. | Thin central scope externalizes adapter code, policy interpretation, audit evidence, support, and incident work to every consuming team. | Google’s ML-systems paper says a mature system may be at most 5% ML code and at least 95% glue, and warns that generic packages can make alternatives prohibitively expensive. DORA’s platform chapter hypothesizes that added handoffs and machinery explain its measured throughput decline. The Backstage plugin directory lists 246 active plugins while warning that community plugins are not fully vetted. ([hidden technical debt](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf), [DORA report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf), [plugin directory](https://backstage.io/plugins/)) | End-to-end time-and-motion data showing that a contract-only approach reduces combined platform, product, security, compliance, and support labor rather than merely central headcount. | **Counter leads**; the draft counts central machinery more clearly than displaced work. |
| Broad scope is platform bloat. | Shared data, training, deployment, serving, evaluation, and monitoring can have economies of scope because their contracts and failure modes cross component boundaries. | Uber reports that Michelangelo replaced bespoke one-off production systems, supported hundreds of use cases and thousands of models, and allowed product teams to reuse shared features and company-wide tooling. Google reports TFX continuous pipelines used across hundreds of teams. These are promotional first-party cases, but they are concrete evidence that integration can remove repeated glue at scale. ([Uber Michelangelo](https://www.uber.com/us/en/blog/scaling-michelangelo/), [Google TFX](https://www.usenix.org/system/files/opml19papers-baylor.pdf)) | Comparable organizations achieving the same scale, reliability, and reuse with independent thin capabilities at lower total cost and no increase in duplicated integration. | **Roughly even**: broad integration has demonstrated scale benefits, while Uber also had to add domain-specific platforms when the general system stopped fitting. |
| A dedicated UI is optional. | A UI is part of the minimum when the user population includes non-engineers, occasional users, approvers, auditors, or people who cannot memorize a CLI’s state and syntax. | In an empirical comparison, novices completed equivalent tasks in significantly less time and fewer steps with a GUI, although cognitive load did not fall. A low-code usability review screened 207 papers and retained 38, emphasizing that users often lack programming backgrounds and that usability is therefore central. Spotify now sells a hosted, no-code “Backstage in a box,” which is interested vendor evidence that customers will pay to remove setup and interface friction. ([GUI/TUI study](https://pmc.ncbi.nlm.nih.gov/articles/PMC2655855/), [low-code review](https://www.sciencedirect.com/science/article/pii/S259011842200082X), [Spotify Portal](https://info.backstage.spotify.com/get-portal)) | Task studies in the actual mixed user population showing equal completion, error, accessibility, and support outcomes through API/CLI/chat alone. | **Counter leads for mixed cohorts**; CLI/API may remain the minimum for expert, frequent users. |
| A metadata contract consumed by Backstage might itself be the platform. | A contract without conformance checks, freshness guarantees, ownership, and consequences is documentation, not control. | An expert study of 17 software architects separates agreement on design decisions from checking implementation conformance and says both are needed to prevent erosion. A large policy-as-code study analyzed 10,560 files from 499 repositories and defines policy as machine-enforceable rules with explicit enforcement strategies. Backstage’s own issue history shows users blocked by configuration guidance that had drifted almost 20 versions. ([architecture-enforcement study](https://www.sciencedirect.com/science/article/pii/S0164121218301614), [policy-as-code study](https://researchportal.vub.be/en/publications/an-empirical-study-of-policy-as-code-adoption-purpose-and-mainten/), [Backstage issue](https://github.com/backstage/backstage/issues/22162)) | Sustained measurements showing voluntary contracts remain complete, current, semantically correct, and audit-ready without automated or human conformance work. | **Counter leads**. A contract can be the interface, but validation and enforcement are part of the real capability. |
| Removability makes a platform smaller. | Deletion is an option with a potentially large exercise price: migrations, dual running, retraining, data movement, revalidation, and product delay can exceed years of ongoing ownership. | GOV.UK PaaS served 172 services and 3,200 applications before its planned 18-month decommission. One department later described migrating 41 critical services, simultaneous platform construction and onboarding, repeated iterations, coordinated cutovers, and out-of-hours work. An empirical cloud-migration study validated common challenges with 104 experts and characterizes migration as difficult and high-cost. ([GDS decommission](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/), [41-service migration](https://digitaltrade.blog.gov.uk/2025/05/12/delivering-seamless-migrations-and-a-future-ready-platform/), [migration study](https://arxiv.org/abs/2004.10724)) | A public, full-cost comparison in which retirement and migration are lower than the discounted owner cost avoided, including product opportunity cost and risk. | **Inconclusive**: exit work is clearly material, but the public cases do not disclose a comparable cost ledger. |
| Helping teams build agents can be separated cleanly from running them. | Once agents invoke tools, build-time metadata and runtime authorization, identity, audit, and approval form one control loop. | MCP authorization reuses OAuth 2.1 and requires audience-bound tokens; OWASP recommends least privilege and human approval for high-impact agent actions. These are familiar IAM controls, but model-directed tool selection makes the coupling operationally consequential. ([MCP authorization](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), [OWASP excessive agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)) | Evidence that build-time contracts alone reliably constrain production tool use across model, prompt, and tool changes. | **Counter leads for agents with write authority**; separation remains plausible for read-only or low-risk workflows. |

## Whose interests does the working framing serve

- **The author and application teams:** “start with almost nothing” protects team autonomy and reduces the chance that a central team becomes a gate. It can also let product teams externalize cross-cutting assurance until an auditor, incident responder, or platform team inherits it.
- **Central platform teams:** defining a new AI capability can secure ownership, budget, and architectural authority. Defining it as a small contract can produce the opposite political benefit: a low apparent cost that is easier to approve, even if later enforcement expands the scope.
- **Security, compliance, finance, and audit:** a central inventory, policy point, and evidence stream make their work legible. Their preference for integration is not proof that one platform is efficient; it reflects that distributed exceptions are expensive for them.
- **Non-engineer builders and occasional users:** a portal or guided UI lowers recall and syntax requirements. “No UI” privileges frequent technical users unless another interface—chat, forms, or an existing portal—does the translation.
- **Platform vendors and category makers:** PlatformEngineering.org’s own history says Humanitec launched a product when few people understood the problem and then created a conceptual framework called “platform engineering.” It later spun out training, certification, research, and consulting. That does not invalidate the discipline, but it is an unusually direct admission that category education and commercial demand grew together. ([PlatformEngineering.org history](https://platformengineering.org/about), [Humanitec product page](https://humanitec.com/platform-engineering))
- **Spotify:** the open-source Backstage framework creates adoption and ecosystem reach; Spotify now sells a hosted no-code Portal and closed-source commercial plugins. Again, useful software and commercial interest can coexist, but “reuse Backstage” is not a neutral architectural suggestion. ([Spotify Portal](https://info.backstage.spotify.com/get-portal), [Spotify commercial-plugin FAQ](https://backstage.spotify.com/faqs/))
- **Survey publishers:** the strongest broad platform evidence is still largely industry research. A 2026-05-04 multivocal review found only 2 of 88 included sources were tier-1 publications primarily about platform engineering and explicitly flags vendor bias in Port and Humanitec surveys. DORA is run by Google Cloud, though its report publishes methods and includes negative findings. ([multivocal review](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full), [DORA overview](https://dora.dev/research/2024/dora-report/))

## Receipts the source omitted or downplayed

1. **The best-known quantitative platform result is not a clean win.** DORA’s survey of nearly 3,000 working professionals reports 8% higher individual productivity, 10% higher team performance, and 6% higher organizational performance for platform users—but also approximately 8% lower throughput and 14% lower change stability. The report offers hypotheses, not causal proof. A chapter that optimizes only reduced waiting or perceived productivity can reach the opposite conclusion from one that optimizes deployment throughput or rework. ([DORA PDF](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf))
2. **The evidence base is academically immature.** The multivocal review’s 2-of-88 tier-1 result means confident prescriptions about a universal minimum are mostly extrapolated from practitioner cases and vendor surveys. That is useful evidence, but not a settled comparative science. ([multivocal review](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full))
3. **“Thin” can be 95% glue somewhere else.** The ML technical-debt paper’s 5%/95% illustration is not a census of modern agent systems, but it correctly reframes software outside the model as the dominant engineering surface. A metadata file can be tiny while its adapters, identity flows, evidence, and lifecycle are not. ([hidden technical debt](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf))
4. **Broad platforms have demonstrated economies at large scale.** Michelangelo and TFX are not neutral comparisons, but both document company-wide reuse across many teams and lifecycle stages. The source’s subtraction instinct underweights the fixed-cost economics that make integration rational after sufficient repetition. ([Uber Michelangelo](https://www.uber.com/us/en/blog/scaling-michelangelo/), [Google TFX](https://www.usenix.org/system/files/opml19papers-baylor.pdf))
5. **Contracts decay without operational machinery.** The Backstage thread is a small but unusually crisp public record: users could reproduce a registration bug in the current release while following old guidance, and a maintainer reopened it. The failure was not absence of schema; it was versioned behavior and documentation no longer lining up. ([Backstage issue](https://github.com/backstage/backstage/issues/22162))
6. **Deletion is not the inverse of creation.** GOV.UK PaaS was reliable—99.95% uptime and one major incident over seven years—yet its economics and architecture no longer justified investment. The sunset still forced many downstream migrations, including a 41-service program described years after the announcement. “Can be deleted” should therefore be priced as a funded migration option, not treated as an intrinsic property of small code. ([decommission decision](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/), [migration account](https://digitaltrade.blog.gov.uk/2025/05/12/delivering-seamless-migrations-and-a-future-ready-platform/))
7. **A UI can be the capability, not decoration.** For a non-engineer, the smallest successful intervention may be a bounded form with explanation, previews, and approval—not a powerful CLI. The empirical GUI study and low-code review do not prove which UI an AI platform needs, but they disprove treating interface removal as costless. ([GUI/TUI study](https://pmc.ncbi.nlm.nih.gov/articles/PMC2655855/), [low-code review](https://www.sciencedirect.com/science/article/pii/S259011842200082X))

## Community pulse, dissent edition

These are qualitative signals, not representative samples. Each thread is self-selected and should be read for mechanisms and language rather than prevalence.

### Hacker News

**Dominant dissenting read:** the label is vague and the answer is conditional on scale and team skill. Some experienced engineers see central platform teams as an added layer; others say that same overhead becomes rational when infrastructure, security, and compliance exceed local expertise.

- `deterministic`, 2023-06-28: “every time an ‘ops’ team gets involved, complexity and cost goes up, with zero or negative benefits.” ([direct comment](https://news.ycombinator.com/item?id=36502512)) **Stake:** direct practitioner.
- `kodah`, 2023-06-25: “At that point the overhead and abstractions are worth it.” The “point” was teams lacking infrastructure expertise or compliance scaling beyond developer knowledge. ([direct comment](https://news.ycombinator.com/item?id=36468229)) **Stake:** direct platform practitioner.

The useful dissent is not simply anti-platform. It says the minimum is contingent: local competence and risk determine whether central overhead is waste or leverage.

### Reddit r/devops

**Dominant dissenting read:** a portal framework can hide a staffed software product. Engineers object less to a catalogue than to the React, YAML, plugin, upgrade, and support work required to make it useful.

- `hijinks`, 2025-05-06: “you need 2-3 people to support and build it out for it to work.” ([direct comment](https://www.reddit.com/r/devops/comments/1kgfqys/comment/mqymey2/)) **Stake:** direct former user.
- `fistagon7`, 2025-05-06: “I didn’t have the cycles for my platform engineering team to manage yet-another-platform.” ([direct comment](https://www.reddit.com/r/devops/comments/1kgfqys/comment/mqz46xg/)) **Stake:** direct engineering leader.

The same thread contains defenders who call Backstage a useful UI around existing automation. That disconfirms both extremes: a UI can remove user work, while the team behind it absorbs substantial product work.

### GitHub Backstage issues

**Dominant dissenting read:** declarative catalog metadata is not self-executing governance; versioned code, providers, documentation, and maintainers determine whether the contract works.

- `briemarie`, 2025-05-20: “I can't find anything in the docs and this is blocking us.” ([direct comment](https://github.com/backstage/backstage/issues/22162#issuecomment-2895691140)) **Stake:** direct implementer.
- `awanlin`, 2025-05-20: “I would not trust that being correct nearly 20 versions later.” ([direct maintainer comment](https://github.com/backstage/backstage/issues/22162#issuecomment-2895717047)) **Stake:** direct maintainer.

This is one issue, not an adoption study. Its value is narrower: it demonstrates the precise failure mode the contract-only hypothesis must fund—compatibility, validation, current guidance, and remediation.

## Quantitative reframes

| Framing choice | What the chapter currently foregrounds | Honest alternative denominator or unit | How the conclusion changes |
|---|---|---|---|
| **Platform success metric** | User success and less waiting. | Measure individual productivity, team performance, organization performance, throughput, and change stability separately. DORA reports `+8%`, `+10%`, `+6%`, `-8%`, and `-14%` respectively. ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)) | “Platform helps” and “platform harms” can both be true. The minimum depends on which outcome and risk class matters. |
| **Cost boundary** | Platform-team headcount, services, and features. | `Total cost = central fixed cost + central variable cost + Σ(team integration + support + audit + incident + exception work)`. | A one-file contract can be larger than a managed service if every team writes adapters and evidence. A broad service wins after repeated local cost exceeds its fixed cost. |
| **Adoption denominator** | Whether an organization “has a platform.” | DORA used a broad definition and found 89% of respondents used an IDP; CNCF/SlashData separately found 28% had a dedicated platform team, 41% used multi-team management, and 35% used a hybrid approach for AI. ([DORA](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf), [CNCF/SlashData](https://www.cncf.io/announcements/2026/03/24/cncf-and-slashdata-report-finds-platform-engineering-tools-maturing-as-organizations-prepare-for-ai-driven-infrastructure/)) | A high “platform adoption” figure does not imply broad centralized products are dominant; it may include shared pipelines, portals, or federated capability. |
| **Code size versus work** | Number of platform components or deployed services. | Count glue, data pipelines, validation, tool authorization, evidence, and migration. The ML debt paper illustrates a mature system as up to 5% ML and at least 95% glue. ([hidden technical debt](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)) | Minimizing the visible AI layer can optimize the smallest fraction of the system. |
| **UI efficiency** | Expert engineer speed through CLI/API. | Completion time, errors, accessibility, and support requests for the entire target cohort, segmented by expertise and frequency. Novices in the GUI/TUI experiment needed significantly less time and fewer steps with the GUI. ([GUI/TUI study](https://pmc.ncbi.nlm.nih.gov/articles/PMC2655855/)) | “No UI” is small only when non-engineers and occasional users are outside the denominator. |
| **Removal economics** | Annual cost of owning a capability. | Compare discounted continuing owner cost with migration engineering, dual running, data transfer, revalidation, retraining, product delay, and cutover risk. GOV.UK’s 18-month sunset created multi-year downstream programs; one department migrated 41 critical services. ([GDS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/), [DBT](https://digitaltrade.blog.gov.uk/2025/05/12/delivering-seamless-migrations-and-a-future-ready-platform/)) | Deletion can be economically wrong even when ongoing ownership is visibly expensive. “Removable” must include a funded exit path and portability. |
| **AI novelty** | Count capabilities sold as AI infrastructure. | Count only needs caused by probabilistic behavior or delegated model action: evaluation under changing distributions, linked model/prompt/data versions, output validation, and tool-level authority. Production-ML interviews identify validation and versioning; OWASP identifies excessive agency. ([interview study](https://arxiv.org/abs/2209.09125), [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)) | Most capability should remain in incumbent platforms; the AI-specific minimum is narrower but more operational than metadata alone. |

## What I looked for and did not find

- **A controlled, multi-organization comparison of no dedicated AI platform versus contract-only, narrow-managed, and broad-integrated approaches.** Searches for platform engineering comparative studies, IDP productivity studies, and MLOps architecture evaluations found surveys, interviews, mappings, and first-party case studies—not a causal head-to-head design.
- **A public total-cost ledger that includes both central and displaced local work.** Vendor ROI material counts platform benefits; platform-team critiques count central upkeep. Neither side routinely measures application-team adapters, security exceptions, audit preparation, support, and incident labor in the same model.
- **A measured threshold for “smallest.”** I found no validated cutoff based on team count, agent count, risk class, or duplicated hours that predicts when shared integration beats decentralization.
- **A UI-versus-CLI study for internal AI platforms with engineers, non-engineers, auditors, and approvers.** General GUI and low-code evidence supports segmentation by expertise, but it cannot select the interface for this case.
- **A documented contract-only agent catalogue with longitudinal completeness, freshness, compliance, and incident outcomes.** Backstage documents descriptor syntax, and its public issues show operational friction, but I did not find a rigorous longitudinal evaluation of an agent metadata contract without enforcement.
- **A full comparison of retirement cost against continued ownership for GOV.UK PaaS.** Public records describe reliability, strategic reasons, migration scale, and operational effort but do not disclose enough comparable cost data to prove that deletion was cheaper—or more expensive—than continued ownership.
- **Evidence that one broad platform remains sufficient indefinitely.** Uber’s account instead reports a general platform followed by specialist NLP and computer-vision platforms, which suggests economies of scope have a boundary. ([Uber](https://www.uber.com/us/en/blog/scaling-michelangelo/))

These absences matter. They make “smallest” a hypothesis to test with local cost and outcome data, not a general result supported by the literature.

## What would change the story

The single most decisive evidence would be an independently run, longitudinal, multi-organization study that randomly or credibly quasi-randomly compares **no dedicated platform**, **contract plus automated conformance**, **narrow managed capability**, and **broad integrated platform** across the same risk classes. It would need to include all central and local labor, audit effort, incidents, cost per successful workflow, user success by expertise, exceptions, and exit cost.

If that study showed that contract plus conformance consistently delivered equal or better governed outcomes at lower total cost—with no penalty for non-engineers and no migration trap—the lede should become “the smallest AI platform is an enforceable contract.” If broad integration won after a reproducible scale or risk threshold, the lede should instead say “smallest is below the optimum; the target is the least total work.”

## Proper-noun snowball pass

### Round 1

- **Already searched:** Backstage, Spotify, DORA, Google Cloud, CNCF, SlashData, Uber, Michelangelo, Google TFX, GOV.UK PaaS, Government Digital Service, MCP, NIST, OWASP, Reddit, Hacker News, GitHub.
- **Search-now and resolved:** Humanitec and PlatformEngineering.org (category origin and commercial interest); Spotify Portal (commercial managed UI); Apache Spark and Cassandra (Uber’s integration-cost account); OAuth 2.1 (MCP authorization dependency); Department for Business and Trade (downstream GOV.UK PaaS migration); Port and OpsLevel (vendor presence in the community thread).
- **Background-only:** AWS, Azure, GCP, Kubernetes, React, TypeScript, Jenkins, Argo CD, Open Policy Agent, Gatekeeper. They are implementation examples, not independent actors load-bearing to this angle.

### Round 2

The first pass added Spotify’s commercial products, Humanitec’s category-building history, and the Department for Business and Trade migration. Targeted searches on each were folded into the interests, receipts, and migration sections. The second pass produced no new unsearched load-bearing organization, product, regulator, or named individual, so the snowball stopped.

## Source receipts

### Critic

- [Hidden Technical Debt in Machine Learning Systems](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)
- [Operationalizing Machine Learning: An Interview Study](https://arxiv.org/abs/2209.09125)
- [Architecture Enforcement Concerns and Activities](https://www.sciencedirect.com/science/article/pii/S0164121218301614)
- [Platform engineering and internal developer portals: a multivocal literature review](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1814498/full)
- [What about the usability in low-code platforms?](https://www.sciencedirect.com/science/article/pii/S259011842200082X)
- [PlatformEngineering.org: Who we are](https://platformengineering.org/about)

### Regulator / standards

- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [OWASP: Excessive Agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/2_0_vulns/LLM06_ExcessiveAgency.html)
- [MCP authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization)

### Audit / public record

- [DORA Accelerate State of DevOps report](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)
- [DORA 2024 report overview](https://dora.dev/research/2024/dora-report/)
- [GOV.UK PaaS live assessment](https://www.gov.uk/service-standard-reports/gov-dot-uk-platform-as-a-service-paas-live-assessment)
- [GDS decommission decision](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)
- [Department for Business and Trade migration account](https://digitaltrade.blog.gov.uk/2025/05/12/delivering-seamless-migrations-and-a-future-ready-platform/)
- [GOV.UK hosting guidance](https://www.gov.uk/service-manual/technology/deciding-how-to-host-your-service)

### Community

- [GitHub: Backstage issue #22162](https://github.com/backstage/backstage/issues/22162)
- [Hacker News: deterministic](https://news.ycombinator.com/item?id=36502512)
- [Hacker News: kodah](https://news.ycombinator.com/item?id=36468229)
- [Reddit: hijinks](https://www.reddit.com/r/devops/comments/1kgfqys/comment/mqymey2/)
- [Reddit: fistagon7](https://www.reddit.com/r/devops/comments/1kgfqys/comment/mqz46xg/)
- [GitHub: briemarie](https://github.com/backstage/backstage/issues/22162#issuecomment-2895691140)
- [GitHub: awanlin](https://github.com/backstage/backstage/issues/22162#issuecomment-2895717047)

### Counter-press / disconfirming vendor and practitioner evidence

- [CNCF/SlashData technology radar](https://www.cncf.io/announcements/2026/03/24/cncf-and-slashdata-report-finds-platform-engineering-tools-maturing-as-organizations-prepare-for-ai-driven-infrastructure/)
- [Uber: Scaling Machine Learning with Michelangelo](https://www.uber.com/us/en/blog/scaling-michelangelo/)
- [Google: Continuous Training for Production ML with TFX](https://www.usenix.org/system/files/opml19papers-baylor.pdf)
- [Spotify Portal](https://info.backstage.spotify.com/get-portal)
- [Spotify commercial-plugin FAQ](https://backstage.spotify.com/faqs/)
- [Humanitec platform engineering](https://humanitec.com/platform-engineering)
- [Backstage plugin directory](https://backstage.io/plugins/)

### Quantitative reframe

- [An Analysis of MLOps Architectures](https://arxiv.org/abs/2406.19847)
- [Empirical study of policy-as-code](https://researchportal.vub.be/en/publications/an-empirical-study-of-policy-as-code-adoption-purpose-and-mainten/)
- [Comparing Text-based and Graphic User Interfaces](https://pmc.ncbi.nlm.nih.gov/articles/PMC2655855/)
- [Challenges in migrating legacy systems to the cloud](https://arxiv.org/abs/2004.10724)
