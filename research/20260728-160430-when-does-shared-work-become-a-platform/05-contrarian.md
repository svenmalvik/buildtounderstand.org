## Competing explanations

Chapter 2 is already more cautious than the usual platform pitch: it asks whether documentation, conventions, or libraries can remove a constraint before a platform is built. The contrarian move is to go one step further and question whether “when does shared work become a platform?” is the right frame at all. Shared work may be evidence of a skills problem, an ownership problem, an unnecessarily varied estate, or a poor purchasing decision. None of those necessarily matures into a platform.

| Working claim | Competing explanation | Evidence for the counter | What would falsify the working claim | Current state |
|---|---|---|---|---|
| Repeated AI work eventually justifies a shared platform capability. | Repetition may be the visible symptom of weak documentation, missing training, or unclear ownership. Standard operating guidance and hands-on learning may remove it without adding a runtime dependency. | A mixed-method DevOps study analysed 174,000 Stack Overflow posts and surveyed 21 practitioners. Its respondents asked for better documentation, learning resources, and formal training, and said hands-on experience was needed before the tools felt easy ([Tanzil et al., 2024-03-25](https://arxiv.org/abs/2403.16436)). This is not AI-platform-specific, but it is direct evidence against assuming that tooling is the first remedy for tooling friction. | A matched intervention showing that documentation and training leave the repeated constraint intact while a narrow platform capability removes it at lower total cost. | **Inconclusive.** The alternative is credible, but the available study does not compare it directly with an AI platform. |
| A platform reduces cognitive load by hiding complexity. | A platform can transfer cognitive load from public infrastructure concepts into a proprietary abstraction, plus onboarding, debugging, upgrade, and exception-handling work. | Engineers in a 2024 practitioner thread described company wrappers as another abstraction layer requiring continual maintenance ([Reddit, 2024-07-02](https://www.reddit.com/r/ExperiencedDevs/comments/1dtwsij/curious_what_peoples_experiences_with_platform/)). Backstage’s own issue history records a push to reduce TechDocs transformation layers after it grew from a hack ([GitHub issue 4548, 2021-06-23](https://github.com/backstage/backstage/issues/4548)). | Evidence that total task time, training time, support time, and exception time all fall for both ordinary and non-standard workloads, not merely that the happy path takes fewer clicks. | **Counter leads.** Public evidence documents the transfer mechanism; vendor outcome studies rarely count its full cost. |
| A portal or integrated internal developer platform is the natural unit for shared AI work. | The useful unit may be a repository template, library, CLI, policy check, model gateway, or managed service. Calling the bundle a platform can encourage premature scope expansion. | Team Topologies’ “thinnest viable platform” guidance allows a platform to be as small as a wiki page and warns against a mandatory, bloated platform ([Team Topologies mini-book](https://teamtopologies.com/s/Organization-Dynamics-with-Team-Topologies-Mini-book-MB80.pdf)). In a 2025 Backstage discussion, one engineer said GitHub templates supplied most of the value for development and deployment ([Reddit, 2025-05-06](https://www.reddit.com/r/devops/comments/1kg3gj4/what_really_makes_an_internal_developer_platform/)). | A task-level comparison in which the integrated portal consistently beats the smallest substitute after setup, maintenance, and migration labor are included. | **Counter leads for small and moderately varied estates; inconclusive at large-enterprise scale.** |
| Shared infrastructure creates stable standardisation. | The platform itself becomes a continuously changing product, so standardisation can relocate churn rather than remove it. | Interviews with management and developers in three software organisations found that continuous-delivery infrastructure did not settle into a stable state; practices kept changing with requirements, tools, dependencies, and external conditions ([Nørbjerg and Dittrich, 2024](https://www.sciencedirect.com/science/article/pii/S0164121224001018)). Backstage’s new-backend release tracker described deprecating the legacy system and a large plugin-migration programme ([GitHub issue 24493, 2024-04-24](https://github.com/backstage/backstage/issues/24493)). | Longitudinal evidence that platform-induced migration and support work is smaller than the local churn it replaces across the platform’s full life. | **Roughly even.** Centralisation can absorb change once, but it also creates a shared migration event and blast radius. |
| Building an internal AI platform is the safe route when AI becomes strategic. | Buying managed primitives or retaining a hybrid may be safer when the work is not differentiating, the organisation lacks operating capability, or compliance dominates. | Google’s longstanding ML guidance recommends establishing metrics and a simple non-ML system before adding ML complexity ([Rules of ML](https://developers.google.com/machine-learning/guides/rules-of-ml/)). A 2026 conceptual build-versus-buy analysis argues that agentic AI changes the economics but does not eliminate external infrastructure dependency; regulated and mission-critical systems remain predominantly buy candidates ([Klotz, 2026-04-29](https://arxiv.org/abs/2604.26482)). | A full-cost case showing that an internal platform delivers materially better differentiated outcomes than managed components while matching their reliability, security, compliance, and staffing economics. | **Inconclusive.** The economic paper is conceptual, not a field comparison. |
| If a platform is reliable and widely used, continued investment is justified. | A good platform can still become uneconomic as the surrounding market, organisational skills, and opportunity cost change. | GOV.UK PaaS served 172 services across more than 60 public bodies, achieved 99.95% uptime, and had one major incident in seven years, yet the Government Digital Service retired it because public-cloud offerings and departmental capabilities had evolved and a rebuild would be expensive ([GDS, 2022-07-12](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). | Evidence that platform value remains positive under an explicit periodic build/buy/retire review, including exit cost and alternative-market improvement. | **Counter leads.** Reliability and adoption are necessary but not sufficient evidence of continuing value. |
| Low adoption means engineers are resisting useful standardisation. | Low adoption may be accurate product feedback: the platform solves leadership’s legibility problem rather than engineers’ workflow problem. | DORA defines developer independence as completing lifecycle work without relying on an enabling team and associates that independence with a 5% improvement in individual and team productivity ([DORA, updated 2026-01-12](https://dora.dev/capabilities/platform-engineering/)). Practitioner accounts repeatedly connect poor adoption with mandated tools, ignored feedback, and platform teams not treating application engineers as customers ([Reddit, 2024-07-02](https://www.reddit.com/r/ExperiencedDevs/comments/1dtwsij/curious_what_peoples_experiences_with_platform/)). | Evidence that non-adopters have worse end-to-end outcomes after controlling for workload and that their stated objections are addressed without coercion. | **Counter leads.** Mandate is not adoption, and adoption is not demonstrated value. |

The disconfirming record does not say “never build a platform.” It says the threshold cannot be repetition alone. A platform has to beat the cheapest credible substitute on the same workflow and over the same lifecycle.

## Whose interests does the working framing serve

The framing serves several interests simultaneously. Those interests do not make the claims false, but they change the evidentiary weight.

- **Cloud vendors benefit when “shared work” becomes an internal platform built from their managed services.** Google Cloud defines an IDP as a way to shift complexity away from developers and immediately presents Google Cloud managed services as its building blocks ([Google Cloud platform-engineering page](https://cloud.google.com/solutions/platform-engineering)). Google also states that its internal developer-platform team and Google Cloud package internal capabilities for customers ([Google Cloud, 2025](https://cloud.google.com/blog/products/application-modernization/a-guide-to-platform-engineering/)). Its advice may be sound, but platform expansion also expands cloud consumption and switching cost.

- **AI-platform vendors benefit from classifying common capabilities as undifferentiated infrastructure that should be bought.** Scale AI’s build-versus-buy guide recommends buying the shared foundation and building differentiating logic on top ([Scale AI](https://scale.com/guides/build-vs-buy)). That is a coherent transaction-cost argument and a sales argument from a company selling the foundation.

- **Spotify has both an engineering legacy and a commercial Backstage interest.** Spotify’s published productivity comparison is based on “frequent Backstage users,” and the article presents large activity differences as proof of effectiveness ([Spotify Engineering, 2024](https://engineering.atspotify.com/2024/04/supercharged-developer-portals)). Spotify later described a paid, managed Backstage offering, making clear that its platform narrative is no longer only an open-source adoption story ([Spotify Engineering, 2025](https://engineering.atspotify.com/2025/04/celebrating-five-years-of-backstage)). The internal results remain useful, but they are not an independent evaluation.

- **Google Cloud and Enterprise Strategy Group jointly produced a survey that begins inside the category it promotes.** The study covered 500 respondents at organisations with at least 500 employees, all of which already had formal platform-engineering teams ([Google Cloud and ESG, 2025-01-23](https://cloud.google.com/blog/products/application-modernization/new-platform-engineering-research-report)). It can compare kinds of platform programmes. It cannot tell a smaller organisation whether to form one, because “no formal platform team” is absent from the analysed sample.

- **Platform communities and their sponsors benefit when the practice is described as inevitable.** PlatformEngineering.org’s 2025 report says platform engineering is the “foundational operating system” of the enterprise and bases its claims on 518 engineers ([PlatformEngineering.org, 2025-12-16](https://platformengineering.org/blog/announcing-the-state-of-platform-engineering-vol-4)). An industry community is well placed to find practitioners, but recruiting through a platform-engineering audience makes category enthusiasm and occupational self-selection likely.

- **Engineering leadership benefits from standardisation even where application engineers do not.** A platform makes ownership, controls, cost, and audit evidence more legible. Those are real organisational benefits. They can also turn an engineer-facing “product” into a control plane whose true customers are finance, security, compliance, and management. The distinction should be stated rather than hidden behind developer-experience language.

- **Platform teams benefit from a broad definition of the problem.** A recurring inconvenience can justify a library; a strategic “platform problem” can justify a permanent team, roadmap, product manager, and executive sponsor. Practitioners themselves describe budget-seeking and promotion incentives in platform programmes ([Reddit, 2024-07-02](https://www.reddit.com/r/ExperiencedDevs/comments/1dtwsij/curious_what_peoples_experiences_with_platform/)). This is anecdotal, not proof that most teams are empire-building.

- **Application engineers also have interests.** They may rationally prefer local autonomy, familiar tools, and work whose customer impact is visible. They can underprice duplicated compliance work, on-call risk, and the cost imposed on other teams. The contrarian evidence therefore should not be romanticised as neutral truth; it is strongest when it documents concrete maintenance, queue, migration, and exception costs.

## Receipts the source omitted or downplayed

Chapter 2 is an outline rather than a finished argument, so these are omissions to repair in the eventual chapter, not evidence of deliberate concealment.

1. **A named, successful platform was deliberately retired.** The GOV.UK PaaS record lives on the Government Digital Service blog. It matters because the service was not abandoned after an obvious reliability failure: it had 99.95% uptime, only one major incident in seven years, 3,200 applications, and 122 deployments per day. It was still decommissioned when cloud products and departmental skills changed the economics ([GDS, 2022-07-12](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). A chapter about thresholds needs a retirement threshold too.

2. **The most prominent independent-looking report discloses both positive and negative associations.** DORA’s 2024 overview says internal platforms are associated with higher individual, team, and organisational performance, but also decreased change stability and throughput ([DORA, 2024](https://dora.dev/research/2024/dora-report/)). Its survey instrument also shows that “platform” can mean interaction through a person, ticket, CLI, API, code, or UI ([DORA questions](https://dora.dev/research/2024/questions/)). This breadth weakens any inference that a portal or integrated AI stack caused the outcomes.

3. **DORA is not organisationally independent of a major platform vendor.** The site states that DORA is a Google Cloud programme ([DORA, 2024](https://dora.dev/research/2024/dora-report/)). Its public questions and errata are valuable transparency mechanisms ([DORA errata](https://dora.dev/research/2024/errata/)), but the institutional relationship should accompany every use of its platform findings.

4. **Backstage’s “free” starting point has a visible Day-2 engineering tail.** One maintainer’s public upgrade note says local modifications make template updates progressively harder ([remen, 2022-06-20](https://gist.github.com/remen/06cc21bd3fcf2f1f1177f5943612b57d)). Backstage’s release tracker documents a legacy-backend deprecation and extensive plugin migration work ([GitHub issue 24493, 2024-04-24](https://github.com/backstage/backstage/issues/24493)). License price is therefore a misleading proxy for total platform cost.

5. **The vendor-funded denominator excludes the central decision.** Google and ESG report 500 respondents from organisations with formal platform teams and at least 500 employees ([Google Cloud and ESG, 2025-01-23](https://cloud.google.com/blog/products/application-modernization/new-platform-engineering-research-report)). The study is evidence about how existing programmes describe themselves, not evidence that a company without one should create one.

6. **Tool difficulty can be a training problem.** The DevOps mixed-method study’s respondents explicitly asked for documentation, learning resources, and formal training ([Tanzil et al., 2024-03-25](https://arxiv.org/abs/2403.16436)). A platform business case should price that intervention before assuming another abstraction is cheaper.

7. **Infrastructure keeps evolving after “standardisation.”** The three-organisation continuous-software-engineering study found ongoing negotiation and adaptation rather than a stable destination ([Nørbjerg and Dittrich, 2024](https://www.sciencedirect.com/science/article/pii/S0164121224001018)). The proper comparison is not local churn versus a finished platform; it is local churn versus a permanently maintained shared product.

8. **AI-tool productivity is not AI-platform evidence.** A randomised trial with 96 Google engineers estimated that three AI features reduced time on one enterprise task by about 21%, with a wide confidence interval, and cautioned against assuming the result generalises across tools or time ([Paradis et al., 2024-10-16](https://arxiv.org/abs/2410.12944)). Faster AI-assisted coding may increase demand for shared controls, but it does not establish that a full AI platform is the best control mechanism.

## Community pulse, dissent edition

Community evidence is useful for finding failure modes, not estimating prevalence. The threads below contain positive accounts too. The dominant dissent is therefore weighted as a mechanism probe, not a representative survey.

### Hacker News: the category may be old operations work with a new label

The dissenting read is that “platform engineering” frequently renames longstanding operations and coordination work, while adding a political ownership layer and new abstraction. This diverges from the chapter’s implied progression from repeated work to a distinct platform category.

- `skywhopper`, 2024-05-31: “The only myth is that these labels represent new ideas or unique approaches.” ([thread](https://news.ycombinator.com/item?id=40531258)). **Stake: adjacent** — the commenter reasons from the history of infrastructure work but gives no named employer or programme.
- `matsemann`, 2023-06-25: “I sometimes feek the platform teams add more hurdles than ‘stability and velocity’.” ([thread](https://news.ycombinator.com/item?id=36465220)). **Stake: direct** — the comment compares the author’s own developer experience in workplaces with and without advanced platform machinery.

The same 2023 thread includes strong counterexamples at 20–25 Java teams and 50–70 services, plus compliance and continuity arguments. The dissent is substantial, not unanimous.

### Reddit: templates, libraries, and managed tools often beat the portal

The recurring dissent is not anti-standardisation. It is anti-wrapper and anti-portal when a smaller composable artifact supplies most of the value.

- `StephenM347`, 2024-07-02: “Every platform team I've worked with ends up writing their own libraries and frameworks, and requires the whole company to use them.” ([thread](https://www.reddit.com/r/ExperiencedDevs/comments/1dtwsij/curious_what_peoples_experiences_with_platform/)). **Stake: direct** — the handle describes experience with multiple platform teams.
- `aliendude5300`, 2025-05-06: “GitHub templates get us 90% of the way there.” ([thread](https://www.reddit.com/r/devops/comments/1kg3gj4/what_really_makes_an_internal_developer_platform/)). **Stake: direct** — the comment describes a management-mandated Backstage rollout in the commenter’s organisation.

The second thread also supplies a useful scale counterexample: another engineer reports thousands of weekly Backstage users and a dedicated team of 20. That supports a threshold story, but the implied threshold is far above “we repeat this task.”

### GitHub: an open platform is a maintained software product, not an install

The dissent embedded in GitHub is less ideological and more operational: extensible platform frameworks accumulate architecture and upgrade work that adopters must own.

- `ottosichert`, 2021-06-23: “TechDocs was a wildly successful hack project built on best-of-breed tools of the time.” ([Backstage issue 4548](https://github.com/backstage/backstage/issues/4548)). **Stake: direct** — a Backstage contributor reopening the architecture RFC.
- `remen`, 2022-06-20: “The challenge of keeping Backstage up-to-date, is that it is meant as a template for a developer portal.” ([GitHub Gist](https://gist.github.com/remen/06cc21bd3fcf2f1f1177f5943612b57d)). **Stake: direct** — an adopter documenting an upgrade workflow.

This evidence does not show that Backstage fails overall. It shows what adoption numbers and feature lists omit: the portal’s template, plugins, migration path, and local customisations become somebody’s product backlog.

## Quantitative reframes

| Published framing | Chosen denominator, window, peer group, or unit | Honest alternative | How the conclusion changes |
|---|---|---|---|
| Spotify says frequent Backstage users were 2.3 times as active in GitHub, made twice as many code changes in 17% less cycle time, deployed twice as often, and kept software deployed three times as long ([Spotify Engineering, 2024](https://engineering.atspotify.com/2024/04/supercharged-developer-portals)). | The peer group is **frequent users**, and the units are activity and deployment measures. The public article does not establish random assignment or show that Backstage caused engineers to become frequent, productive users. | Compare all eligible engineers, including non-users and abandoners, before and after rollout; match on team, tenure, service maturity, and prior activity; include defects, support cost, and customer outcome. | The result changes from “Backstage users are more productive because of Backstage” to “highly active engineers who frequently use Backstage also score higher on activity measures.” That is promising correlation, not causal proof. |
| DORA reports a 5% individual and team productivity improvement associated with developer independence and a 6% team-productivity gain from a dedicated platform team ([DORA, 2026-01-12](https://dora.dev/capabilities/platform-engineering); [DORA report PDF](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)). | Productivity is a modelled factor score from survey responses, while platform exposure ranges from talking to a person or opening a ticket to using code or a UI. | Put the 5% and 6% beside the same report’s negative associations with change stability and throughput, and separate platform forms and mandates. Use customer value, reliability, and fully loaded platform labor as co-equal outcomes. | “Platforms improve productivity” becomes “some platform arrangements correlate with modest perceived productivity gains and organisational gains while correlating with delivery trade-offs.” |
| Google and ESG say co-managed platforms let developers spend 47% of time on innovation compared with 38% for internal-only platforms ([Google Cloud and ESG, 2025-01-23](https://cloud.google.com/blog/products/application-modernization/new-platform-engineering-research-report)). | The comparison is within organisations of at least 500 employees that already have formal platform teams. There is no no-platform or small-organisation baseline. | Compare co-managed, internal-only, managed primitives plus templates, and no formal platform, stratified by organisation size and workload heterogeneity. Include vendor fees and internal operating labor. | The nine-percentage-point gap can support a **buy-versus-build** claim inside mature platform programmes. It cannot support “platform engineering is no longer optional.” |
| PlatformEngineering.org calls platform engineering the enterprise’s foundational operating system based on 518 engineers ([PlatformEngineering.org, 2025-12-16](https://platformengineering.org/blog/announcing-the-state-of-platform-engineering-vol-4)). | The respondents are engineers reached by a platform-engineering publication and community; the headline concerns the whole enterprise. | Use a probability sample of application developers, ML engineers, security, finance, executives, and organisations with and without platform teams. Publish the questionnaire, response rate, recruitment channels, weights, and raw cross-tabs. | The report remains a useful pulse of an occupational community. It stops being evidence that nearly all enterprises need the category. |
| Backstage’s reach is commonly represented by adopters, repository stars, conferences, plugins, and frequent users ([Backstage repository](https://github.com/backstage/backstage)). | Visibility and declared adoption are counted; failed evaluations, dormant instances, platform staffing, upgrade labor, and teams bypassing the portal are not. | Report active monthly end users per adopter, median dedicated staff, annual upgrade hours, retention after two years, exception rate, and decommission count. | Popularity demonstrates ecosystem strength. It does not by itself demonstrate positive net value for the median adopter. |
| GOV.UK PaaS could have been counted as a success using 172 services, more than 60 public bodies, 99.95% uptime, and one major incident in seven years ([GDS, 2022-07-12](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)). | The unit is historical service performance and adoption. The decision unit is future marginal value relative to public-cloud alternatives and rebuilding cost. | Recalculate annually using forward-looking demand, market alternatives, platform-team cost, migration cost, and exit option. | The same numbers support both “this was a successful platform” and “retirement is rational.” Platform evaluation needs an expiry test, not only adoption and uptime. |

## What I looked for and did not find

The absence of evidence below is bounded by public web search through 2026-07-28; private internal studies may exist.

- I searched for controlled or matched longitudinal studies comparing an **internal AI platform** with documentation, repository templates, reusable libraries, a narrow gateway, and managed AI services on the same production workflow. I found AI-tool studies and platform surveys, but no public head-to-head study with total costs.
- I searched for independent replications of Spotify’s frequent-Backstage-user productivity figures. I found Spotify’s own publication and commercial follow-on, but no independent replication with the cohort definition and causal identification needed to rule out selection effects.
- I searched for a public **denominator of abandoned or decommissioned internal AI platforms**. I found the named GOV.UK PaaS retirement and many anecdotal low-adoption accounts, but no registry, cohort, or survivorship-adjusted failure rate.
- I searched for audited total-cost-of-ownership comparisons that include internal salaries, on-call, support, upgrades, plugin migrations, training, exception handling, vendor fees, egress, and exit. Vendor calculators and build-versus-buy essays were plentiful; independently audited lifecycle comparisons were not.
- I searched for a validated numerical threshold—team count, number of agents, repeated hours, incident exposure, or queue time—at which a platform becomes net-positive. The evidence offers principles and case-dependent advice, not a defensible universal breakpoint.
- I searched the public Google/ESG and PlatformEngineering.org materials for raw respondent-level data, a no-platform baseline, response rate, and full recruitment/weighting details. The public summaries disclose sample sizes and selected criteria, but I did not find enough to reconstruct the headline claims independently.
- I searched for regulator or auditor findings that require an organisation to build a broad internal AI platform. I found reasons to centralise particular controls, but not a rule that makes a portal, full MLOps stack, or dedicated platform team the necessary implementation.
- I searched for a public postmortem in which an organisation explicitly abandoned a broad **AI** platform in favour of only documentation, conventions, and libraries, with before-and-after engineering measures. I did not find a sufficiently documented named case. This is a real gap and limits how strongly the contrarian case can be stated.

## What would change the story

One result would force a rewrite of the lede: a multi-organisation, preregistered, longitudinal comparison in which teams facing the same repeated AI constraint are assigned or closely matched across four interventions—documentation/training, reusable library or template, narrow managed capability, and internal AI platform—and the platform arm produces persistently better customer, reliability, compliance, and developer outcomes **after** fully loaded build, support, migration, exception, and exit costs are counted.

If that result held across small, medium, and large engineering organisations, the chapter should lead with “shared work becomes a platform when integration effects dominate substitution costs,” not with broad scepticism. If the result instead varied mainly by workflow, regulation, and organisational scale, the present smallest-capability decision rule would be strengthened.

## Source receipts

### Critic

- [Martin Fowler: Platform Prerequisites](https://martinfowler.com/articles/platform-prerequisites.html)
- [Team Topologies: Organisation Dynamics with Team Topologies mini-book](https://teamtopologies.com/s/Organization-Dynamics-with-Team-Topologies-Mini-book-MB80.pdf)
- [Tanzil et al.: A Mixed Method Study of DevOps Challenges](https://arxiv.org/abs/2403.16436)
- [Nørbjerg and Dittrich: The never-ending story—How companies transition to and sustain continuous software engineering practices](https://www.sciencedirect.com/science/article/pii/S0164121224001018)
- [Google: Rules of Machine Learning](https://developers.google.com/machine-learning/guides/rules-of-ml/)
- [Klotz: The Buy-or-Build Decision, Revisited](https://arxiv.org/abs/2604.26482)

### Regulator

- No regulator source was used to claim that a broad AI platform is required; the search did not surface such a requirement.

### Audit

- [DORA 2024 overview](https://dora.dev/research/2024/dora-report/)
- [DORA 2024 survey questions](https://dora.dev/research/2024/questions/)
- [DORA 2024 errata](https://dora.dev/research/2024/errata/)
- [DORA platform-engineering capability page](https://dora.dev/capabilities/platform-engineering/)
- [Government Digital Service: Why we’ve decided to decommission GOV.UK PaaS](https://gds.blog.gov.uk/2022/07/12/why-weve-decided-to-decommission-gov-uk-paas-platform-as-a-service/)
- [Backstage issue 24493: New Backend System release 1.0](https://github.com/backstage/backstage/issues/24493)

### Community

- [Hacker News: Myths about platform engineering](https://news.ycombinator.com/item?id=40531258)
- [Hacker News: How platform engineering works](https://news.ycombinator.com/item?id=36465220)
- [Reddit r/ExperiencedDevs: experiences with platform teams](https://www.reddit.com/r/ExperiencedDevs/comments/1dtwsij/curious_what_peoples_experiences_with_platform/)
- [Reddit r/devops: What really makes an Internal Developer Platform succeed?](https://www.reddit.com/r/devops/comments/1kg3gj4/what_really_makes_an_internal_developer_platform/)
- [Backstage issue 4548: TechDocsX architecture RFC](https://github.com/backstage/backstage/issues/4548)
- [remen: Keeping Backstage updated](https://gist.github.com/remen/06cc21bd3fcf2f1f1177f5943612b57d)

### Counter-press

- [Scale AI: Build vs. buy](https://scale.com/guides/build-vs-buy)
- [Google Cloud: Platform engineering](https://cloud.google.com/solutions/platform-engineering)
- [Google Cloud: How Google does platform engineering](https://cloud.google.com/blog/products/application-modernization/a-guide-to-platform-engineering/)
- [Spotify Engineering: Supercharged Developer Portals](https://engineering.atspotify.com/2024/04/supercharged-developer-portals)
- [Spotify Engineering: Celebrating five years of Backstage](https://engineering.atspotify.com/2025/04/celebrating-five-years-of-backstage)
- [PlatformEngineering.org: State of Platform Engineering Report Volume 4](https://platformengineering.org/blog/announcing-the-state-of-platform-engineering-vol-4)

### Quantitative reframe

- [Google Cloud and ESG: New platform engineering research report](https://cloud.google.com/blog/products/application-modernization/new-platform-engineering-research-report)
- [DORA 2024 report PDF](https://dora.dev/research/2024/dora-report/2024-dora-accelerate-state-of-devops-report.pdf)
- [Backstage repository](https://github.com/backstage/backstage)
- [Paradis et al.: Enterprise AI-development randomised controlled trial](https://arxiv.org/abs/2410.12944)
