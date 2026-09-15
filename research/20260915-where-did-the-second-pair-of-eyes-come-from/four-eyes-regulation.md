# Where Did the Second Pair of Eyes Come From? — The regulatory root

**Question this document answers:** What does the four-eyes principle mean for a Norwegian payment or e-money institution under Finanstilsynet, how does it reach software changes, and is the EU regulation called DORA related?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 01, "Where Did the Second Pair of Eyes Come From?"

**Last updated:** 2026-09-15

Scope: the regulatory root of "another pair of eyes" for a Norwegian payment or e-money institution supervised by Finanstilsynet. This complements the historical report on pull requests and peer review in the `vce-context` research folder (`research/pull-request-origins/`), which covers the inspection and distributed-development roots. It is a research note, not legal advice, and it does not describe any one company's compliance position.

## Main findings

"Four eyes" in financial regulation has two distinct meanings, and neither of them is code review.

The first is a governance rule: a credit institution must be effectively directed by at least two persons. This is the origin of the German term *Vier-Augen-Prinzip*, and it lives in CRD Article 13 and the German Banking Act. It concerns who runs the company, not who reads a change.[^1][^2]

The second is an operational control: sensitive individual actions need a second, independent person or function. Basel calls these dual controls. Finanstilsynet uses the phrase «fire øyne»-kontroll in inspection reports about manual risk decisions, and Norwegian firms report using «tjenestedeling ("fire øyne-prinsippet")» in their ICT operations.[^3][^4][^5][^6]

Code review inherits the second meaning through ICT change management rules. Until 30 June 2025 the Norwegian rule was IKT-forskriften § 9, which only required that procedures for change handling exist and are followed. Since 1 July 2025, payment and e-money institutions in Norway fall under DORA. DORA Article 9(4)(e) requires that all ICT changes are "recorded, tested, assessed, approved, implemented and verified in a controlled manner", and the RTS on the ICT risk management framework, Article 17(1)(b), requires "mechanisms to ensure the independence of the functions that approve changes and the functions responsible for requesting and implementing those changes".[^7][^8][^9][^10][^11]

Two words in that sentence carry the whole question for AI-generated changes. The rule says *functions*, not *persons*. And DORA's change management requirement is explicitly "based on a risk assessment approach". The regulation requires independent approval of changes. It does not define whether the approving function must be human, nor that every change receives the same depth of review.[^9][^11]

## Two things called DORA

The research folder uses "DORA" for Google's DevOps Research and Assessment program, whose March 2026 analysis describes a verification tax. This note uses DORA for Regulation (EU) 2022/2554, the Digital Operational Resilience Act. They are unrelated. Any published text that cites both must say which one it means each time.[^12]

## The regulatory chain for a Norwegian e-money institution

| Period | Applicable ICT rule | What it says about changes |
| --- | --- | --- |
| 2003 to 30 June 2025 | IKT-forskriften (FOR-2003-05-21-630) | § 6: written procedures for acquisition, development, and testing. § 9: «Foretaket skal sikre at prosedyrer for avviks- og endringshåndtering foreligger og følges.» § 5: guidelines for granting, changing, and controlling access authorisations. No explicit second-person rule for changes.[^7] |
| From 1 July 2025 | DORA-loven and DORA-forskriften (FOR-2025-06-24-1296); DORA applies directly to entities in its Article 2, including payment and e-money institutions | Art. 9(4)(e): documented, risk-based change management; all changes recorded, tested, assessed, approved, implemented, verified. Art. 6(4): an independent ICT risk control function.[^8][^9][^10] |
| Level 2, same period | Commission Delegated Regulation (EU) 2024/1774 (RTS on ICT risk management framework) | Art. 17(1)(b): independence of approving functions from requesting and implementing functions. Art. 16(2): testing and approval of all ICT systems prior to use. Art. 16(3): source code reviews, static and dynamic. Art. 16(8): third-party and open-source code analysed before production. Art. 16(9): applies proportionately to systems developed outside the ICT function.[^11][^13] |
| From 1 September 2026 | DORA-forskriften as amended (FOR-2026-08-20-1657) | Remaining entity types (finansieringsforetak, eiendomsmeglere, inkasso, Norsk naturskadepool) move to selected DORA parts. IKT-forskriften is repealed in full: «Samtidig oppheves IKT-forskriften.»[^14] |

Finanstilsynet's Q&A states the transition plainly: «For foretak som omfattes av virkeområdet til DORA vil IKT-forskriften erstattes av DORA.» Payment and e-money institutions are explicitly listed in DORA Article 2 and were in scope from the Norwegian law's entry into force.[^10]

The EBA's 2019 Guidelines on ICT and security risk management, which contained the earlier European change-management and segregation-of-duties expectations for payment institutions, had sections 3.1 to 3.7 deleted in February 2025 for entities now covered by DORA. The lineage is EBA guideline to DORA, not a new invention.[^15]

## What Article 17 actually requires

The full list in Article 17(1) of the RTS, for "all changes to software, hardware, firmware components, systems or security parameters":

- (a) verification that ICT security requirements have been met
- (b) "mechanisms to ensure the independence of the functions that approve changes and the functions responsible for requesting and implementing those changes"
- (c) clear roles so that changes are specified and planned, an adequate transition is designed, changes are tested and finalised in a controlled manner, and there is effective quality assurance
- (d) documentation and communication of the purpose and scope, the timeline, and the expected outcomes
- (e) fall-back procedures and responsibilities, including aborting or recovering from failed changes
- (f) procedures, protocols, and tools for emergency changes with adequate safeguards
- (g) procedures to document, re-evaluate, assess, and approve emergency changes after implementation, including workarounds and patches
- (h) identification of the change's impact on existing security measures[^11]

Recital 17 explains the reasoning: changes "regardless of their scale, carry inherent risks", so a verification process is needed to confirm that changes meet security requirements.[^13]

Read against the pull request template in the exploration draft, points (b), (d), and (e) map directly onto "who must approve", "what this changes and why", and "how to reverse this". The template is not compliance tooling, but it asks for the same facts the regulation asks the organisation to record.

## What the rule does not settle

**Whether the approving function must be a human.** Article 17(1)(b) requires independence between functions. It does not say the approving function is a person. An organisation that lets an automated reviewer approve routine changes would have to argue that the reviewer is an independent function, with its own ownership, and that this satisfies a risk-based reading of Article 9(4)(e). Nothing found in this research shows a supervisor accepting or rejecting that argument.

**Whether the same model can implement and approve.** If one model generates a change and the same model, in another invocation, approves it, the independence in (b) is at least questionable. The research on LLM judges preferring their own output, recorded in the adoption draft, is the engineering version of the same worry. This is a question for the compliance function and for supervisory dialogue, not for the platform team alone.

**How depth may vary by risk.** Article 9(4)(e) says change management is "based on a risk assessment approach". A mechanical, reversible change and a change to money movement may legitimately receive different approval depth. The risk-based table in the AI review-capacity report is compatible with this. It is not a statement that a supervisor has endorsed such a table.

**What supervisors have said about AI-generated code.** The ESAs' joint statement of 31 July 2026 on frontier AI addresses cyber risk from AI-assisted attackers, asset inventories, and resilience testing. It says nothing about AI used in software development or about approving AI-generated changes. Finanstilsynet's ROS 2024 reports firms' own position: «Endringer i KI-løsninger må skje i henhold til foretakets rutiner for håndtering av endringer for å sikre at risikoen knyttet til bruk av løsningene ikke bryter med foretakets fastsatte risikotoleranse.» That concerns changes *to* AI systems, not changes *made by* AI.[^16][^5]

**What Finanstilsynet already rates as likely to be weak.** ROS 2025 rates the probability of weaknesses in change management routines, including insufficient testing, as «middels til høy», and the probability of insufficient controls for detecting unauthorised changes, meaning changes put into production without following the change process, also as «middels til høy», both with moderate to serious consequence. A supervisor already worried about unauthorised changes is a supervisor who will ask how an agent's change reached production and who approved it.[^17]

## How the four-eyes phrase is used in Norwegian supervision

The phrase appears in inspection practice, not in a statute.

- 2012, real-estate brokerage letter: Finanstilsynet recommends that a firm writes down which functions have responsibility and authority for tasks, and that routines show «hvor det er påkrevet med ekstra kontroll (fire øyne) og hvilken funksjon som kan utføre dette». Quoted from a search index; the page itself was not reachable at the time of writing.[^4]
- 20 November 2023, Askim & Spydeberg Sparebank inspection report and administrative fine: «Finanstilsynet bemerket også at det ikke var noen «fire øyne»-kontroll for manuell nedjustering av risiko.» The context is anti-money-laundering risk classification, where an employee could manually lower a customer's risk level alone.[^3]
- ROS 2024, section 4.2, reporting firms' own statements: «Foretakene benytter tjenestedeling ("fire øyne-prinsippet") så langt som mulig.»[^5]

In every case the phrase means a second independent person for a sensitive manual decision. It is a control against one person's error or misconduct. That is closer to Saltzer and Schroeder's separation of privilege than to Fagan's inspections, and it is the tradition that DORA's Article 17(1)(b) continues.

## What this means for the exploration

The chapter "Where Did the Second Pair of Eyes Come From?" currently has two roots: formal inspection and the maintainer's integration decision. For a regulated fintech there is a third root, and it is the one compliance will cite. It is older than code review, it is about authority rather than defects, and it is now written into change management law as the independence of approving functions.

That third root sharpens the question. The regulation does not ask whether a human read every line. It asks whether an independent function approved the change, whether the change was recorded with its purpose and fallback, and whether depth followed risk. Those are the same three things the historical report found behind review: authorization, record, and proportionate examination. The four-eyes rule was never mainly a bug-finding rule in finance either.

## Confidence and gaps

| Claim | Assessment |
| --- | --- |
| The German four-eyes term originates in the two-director rule for banks. | Supported by Gabler Banklexikon and KWG § 33; a full etymology was not researched. |
| Payment and e-money institutions in Norway have been under DORA since 1 July 2025. | High confidence; Finanstilsynet news and Q&A, Lovdata. |
| IKT-forskriften is repealed from 1 September 2026. | High confidence; Finanstilsynet news of 2026 and FOR-2026-08-20-1657. |
| RTS 2024/1774 Article 17(1)(b) wording. | Two independent secondary reproductions agree (Springlex, Advisera). EUR-Lex HTML could not be fetched; verify against the Official Journal before quoting in print. |
| RTS 2024/1774 is incorporated into Norwegian law. | Finanstilsynet published a 2026 note on level 2 implementation and EFTA lists the act as EEA-relevant; the exact Norwegian entry-into-force date was not confirmed here. |
| A supervisor has accepted or rejected automated approval of routine changes. | Not found. Absence of evidence, not evidence of absence. |
| IKT-forskriften § 10 concerned change management. | Wrong. § 10 was repealed in 2015; change management was § 9. Earlier drafts that cite § 10 should be corrected. |

## Sources

Sources accessed on 15 September 2026.

[^1]: Directive 2013/36/EU (CRD IV), [Article 13](https://www.legislation.gov.uk/eudr/2013/36/article/13/data.htm?view=plain): "The competent authorities shall grant authorisation to commence the activity of a credit institution only where at least two persons effectively direct the business of the applicant credit institution."

[^2]: Gabler Banklexikon, [Vier-Augen-Prinzip](https://www.gabler-banklexikon.de/definition/vier-augen-prinzip-62358). Credit institutions must have "mindestens zwei geeignete Geschäftsleiter" (§ 33 I 1 Nr. 5 KWG); the principle "erschwert es unsolides, zweifelhaftes oder gar kriminelles Verhalten".

[^3]: Finanstilsynet, [Tilsynsrapport og vedtak om overtredelsesgebyr, Askim & Spydeberg Sparebank](https://www.finanstilsynet.no/contentassets/534f13d8e76b4d568edde86d49d1af85/tilsynsrapport-og-vedtak-om-overtredelsesgebyr---askim--spydeberg-sparebank.pdf), 20 November 2023, section 9.2.1. Partly redacted public version.

[^4]: Finanstilsynet, [Merknader, endelig rapport, Nordmegling](https://www.finanstilsynet.no/nyhetsarkiv/brev/2012/merknader---endelig-rapport21/), 2012. Quoted from search index; the page returned 404 when fetched.

[^5]: Finanstilsynet, [Risiko- og sårbarhetsanalyse (ROS) 2024](https://www.finanstilsynet.no/publikasjoner-og-analyser/risiko--og-sarbarhetsanalyse/2024/ros-2024/risiko--og-sarbarhetsanalyse-ros-2024/), section 4.2. Firms' own statements as reported by the supervisor.

[^6]: Basel Committee on Banking Supervision, [Revisions to the Principles for the Sound Management of Operational Risk](https://www.bis.org/bcbs/publ/d515.pdf), March 2021. Segregation of duties and "dual controls" as elements of the control environment.

[^7]: Lovdata, [Forskrift om bruk av informasjons- og kommunikasjonsteknologi (IKT)](https://lovdata.no/dokument/SFO/forskrift/2003-05-21-630), FOR-2003-05-21-630, repealed 1 September 2026. § 5, § 6, § 9 quoted; § 10 shown as repealed by forskrift 17 December 2015 nr. 1732.

[^8]: Finanstilsynet, [Ny lov om digital operasjonell motstandsdyktighet i finanssektoren (DORA-loven) trer i kraft 1. juli 2025](https://www.finanstilsynet.no/nyhetsarkiv/nyheter/2025/ny-lov-om-digital-operasjonell-motstandsdyktighet-i-finanssektoren-dora-loven-trer-i-kraft-1.-juli): «For mange foretak under tilsyn erstatter DORA-loven forskrift om bruk av informasjons- og kommunikasjonsteknologi (IKT-forskriften) fra og med 1. juli 2025.» See also Lovdata, [DORA-forskriften](https://lovdata.no/dokument/SF/forskrift/2025-06-24-1296), FOR-2025-06-24-1296.

[^9]: Regulation (EU) 2022/2554 (DORA), [Article 9(4)(e)](https://www.springlex.eu/en/packages/dora/dora-regulation/article-9/), as reproduced by Springlex. Article 6(4) on the independent control function per [Springlex](https://www.springlex.eu/en/packages/dora/dora-regulation/article-6/).

[^10]: Finanstilsynet, [Q&A DORA](https://www.finanstilsynet.no/tema/dora/qa-dora/). Scope statements for betalingsforetak and e-pengeforetak; «Om finansieringsforetak skal underlegges helt eller delvis er ikke vurdert enda» at the time of the Q&A.

[^11]: Commission Delegated Regulation (EU) 2024/1774, Article 17, as reproduced by [Springlex](https://www.springlex.eu/en/packages/dora/rts-rmf-regulation/article-17/) and [Advisera](https://advisera.com/cdr-2024-1774/ict-change-management/). Official text: [EUR-Lex](https://eur-lex.europa.eu/eli/reg_del/2024/1774/oj/eng). Norwegian incorporation: Finanstilsynet, [Gjennomføring nivå 2-regelverk under DORA](https://www.finanstilsynet.no/nyhetsarkiv/nyheter/2026/gjennomforing-niva-2-regelverk-under-dora/), 2026; EFTA, [factsheet 32024R1774](https://www.efta.int/eea-lex/32024r1774).

[^12]: Jessica Baolin and Nathen Harvey, DORA (DevOps Research and Assessment), [Balancing AI tensions](https://dora.dev/insights/balancing-ai-tensions/), 10 March 2026. Cited in the AI review-capacity report as source 25. Unrelated to the EU regulation.

[^13]: Commission Delegated Regulation (EU) 2024/1774, Article 16 and recital 17, as reproduced by [Advisera](https://advisera.com/cdr-2024-1774/ict-systems-acquisition-development-and-maintenance-management/) and [Springlex](https://www.springlex.eu/en/packages/dora/rts-rmf-regulation/article-16/).

[^14]: Finanstilsynet, [Regler i DORA erstatter IKT-forskriften](https://www.finanstilsynet.no/nyhetsarkiv/nyheter/2026/regler-i-dora-erstatter-ikt-forskriften), 2026. Lovdata, [Forskrift om endring i DORA-forskriften](https://lovdata.no/dokument/LTI/forskrift/2026-08-20-1657), FOR-2026-08-20-1657.

[^15]: EBA, [Final report on amending Guidelines EBA/GL/2019/04 on ICT and security risk management](https://www.eba.europa.eu/sites/default/files/2025-02/23684f95-f669-4852-94a0-dac6c2ae67ad/Final%20report%20on%20amending%20GLs%20on%20ICT%20risk%20and%20security.pdf), EBA/GL/2025/02, 11 February 2025. Paragraphs 1 to 91, sections 3.1 to 3.7, deleted.

[^16]: ESAs joint statement on ICT risks from frontier AI models, JC 2026 25, 31 July 2026, as summarised by [DORA GRC](https://doragrc.com/blog/esas-frontier-ai-statement-dora-2026) and [Goodwin](https://www.goodwinlaw.com/en/insights/publications/2026/08/alerts-technology-fs-frontier-ai-dora-service-providers-to-eu-financial-entities-take-note). The primary text was not fetched.

[^17]: Finanstilsynet, [ROS 2025, Vedlegg 2: Grunnlag for risikomatrisen](https://www.finanstilsynet.no/publikasjoner-og-analyser/risiko--og-sarbarhetsanalyse/risiko--og-sarbarhetsanalyse-2025/ros-2025/vedlegg-2-grunnlag-for-risikomatrisen/). Change management and unauthorised-change rows. See also [ROS 2025 main report](https://www.finanstilsynet.no/publikasjoner-og-analyser/risiko--og-sarbarhetsanalyse/risiko--og-sarbarhetsanalyse-2025/ros-2025/risiko--og-sarbarhetsanalyse-ros-2025/), section 5.1: «Ved vedlikehold av KI-systemer, inkludert oppdateringer, forutsettes det god styring og kontroll for å unngå at det introduseres feil og sårbarheter.»

## Related documents

The source research lives outside this repository, in the `vce-context` worktree under `research/pull-request-origins/`:

- `pull-request-origins.md`, the sourced history of pull requests and peer review
- `ai-pull-request-growth-and-review-capacity-2026.md`, evidence through September 2026 on review capacity
- `four-eyes-principle-norwegian-fintech-dora.md`, the original of this document
