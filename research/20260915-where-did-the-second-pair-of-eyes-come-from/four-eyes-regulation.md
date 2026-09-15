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

## Primary-text verification, 15 September 2026

The following were read from the official Official Journal text, not from secondary reproductions. Four facts were added or corrected by this pass.

**Article 9(4) has a third subparagraph that the first pass missed.** After the list of points, DORA adds: "For the purposes of the first subparagraph, point (e), the ICT change management process shall be approved by appropriate lines of management and shall have specific protocols in place." This is the closest thing in DORA itself to a requirement about who holds approval authority.

**"Based on a risk assessment approach" sits inside Article 9(4)(e) itself**, attached to the policies, procedures and controls rather than to the verification step. Full point (e): "implement documented policies, procedures and controls for ICT change management, including changes to software, hardware, firmware components, systems or security parameters, that are based on a risk assessment approach and are an integral part of the financial entity's overall change management process, in order to ensure that all changes to ICT systems are recorded, tested, assessed, approved, implemented and verified in a controlled manner".

**Article 17 contains no internal proportionality or risk-based qualifier.** Point (b) on independence is stated flatly. Proportionality reaches it from Article 1, the sole article of Title I, headed "GENERAL PRINCIPLE" and titled "Overall risk profile and complexity", which requires that size, overall risk profile, and "the nature, scale and elements of increased or reduced complexity" be taken into account, listing at point (d) "ICT project and change management". Article 17 sits in Title II, so that principle governs it.

**The regulation's own "source code review" requirement means static and dynamic testing, not human reading.** It sits in the RTS, not in DORA. DORA's own single mention of source code review in this sense is Article 25(1), which lists it among resilience testing methods and qualifies it "where feasible". The mandatory version is RTS Article 16(3): "The procedure referred to in paragraph 2 shall contain the performance of source code reviews covering both static and dynamic testing." The obligations that follow are to identify and analyse vulnerabilities and anomalies in the source code, adopt an action plan, and monitor its implementation. Nothing in Article 16 requires a person to read a change. Article 16(2) adds that "The level of testing shall be commensurate to the criticality of the business procedures and ICT assets concerned."

**Article 16 also reaches code the organisation did not write, and code written outside the ICT function.** Article 16(8) requires that proprietary software and, "where feasible", source code from third-party providers or open-source projects be analysed and tested under paragraph 3 before deployment to production. Article 16(9): "Paragraph 1 to 8 of this Article shall also apply to ICT systems developed or managed by users outside the ICT function, using a risk-based approach." (The singular "Paragraph" is how it is printed officially.)

**Persons versus functions is a real contrast in the same body of law.** CRD IV Article 13(1): "The competent authorities shall grant authorisation to commence the activity of a credit institution only where at least two persons effectively direct the business of the applicant credit institution." That says persons. RTS Article 17(1)(b) says functions, twice, in one sentence.

**DORA Article 6(4)** in full: "Financial entities, other than microenterprises, shall assign the responsibility for managing and overseeing ICT risk to a control function and ensure an appropriate level of independence of such control function in order to avoid conflicts of interest. Financial entities shall ensure appropriate segregation and independence of ICT risk management functions, control functions, and internal audit functions, according to the three lines of defence model, or an internal risk management and control model."

**Article 17(2)** applies only to market infrastructure (central counterparties and central securities depositories) and requires stringent testing under simulated stressed conditions after significant changes. There are no paragraphs beyond 17(2).

### Does "effectively direct the business" reach IT?

Asked because an early draft claimed the two-director rule has "nothing to do with software". That is slightly too strong.

CRD IV Article 13 is titled "Effective direction of the business and place of the head office", and Article 3(1)(7) defines the management body as the body "empowered to set the institution's strategy, objectives and overall direction, and which oversee and monitor management decision-making, and include the persons who effectively direct the business of the institution". So the rule concerns governance of the whole institution, which includes IT, but at the level of running the company.

DORA Article 5(2) supplies the explicit link to IT: "The management body of the financial entity shall define, approve, oversee and be responsible for the implementation of all arrangements related to the ICT risk management framework referred to in Article 6(1)", and under point (a) it shall "bear the ultimate responsibility for managing the financial entity's ICT risk". Point (c) requires it to "set clear roles and responsibilities for all ICT-related functions".

The accurate statement is therefore: the two persons who direct the business are accountable for the institution's ICT risk framework and strategy, and they approve no individual change. The per-change approval requirement lives in Article 9(4)(e) and RTS Article 17(1)(b), which speak of functions.

### Norwegian and Basel verification, 15 September 2026

Read from the document text, not from search snippets.

**Basel does not require a human for dual control.** The March 2021 operational risk principles, paragraph 50, define the control as "a process that uses two or more separate entities (usually persons) operating in concert to protect sensitive functions or information". The parenthetical is "entities (usually persons)", not "persons". The phrase "four eyes" appears zero times in the 44-page document. Served from `https://www.bis.org/publications/202103-guidelines-revisions-principles-sound-management-operational-risk.pdf`; the older `d515.pdf` path now redirects there.

**"Vier-Augen-Prinzip" is not statutory language.** KWG § 33 is titled "Versagung der Erlaubnis" and lists grounds on which a licence must be refused. Paragraph 1 sentence 1 no. 5 covers an institution that "nicht mindestens zwei Geschäftsleiter hat, die nicht nur ehrenamtlich für das Institut tätig sind". The phrase "Vier-Augen-Prinzip" appears nowhere on the § 33 page; it is commentary and supervisory usage. The ground is also conditional in scope rather than applying to every institution.

**Norwegian «fire øyne» usage is about internal fraud, not change management.** The phrase appears in Finanstilsynet's ROS reports for 2024, 2025 and 2026, always as «tjenestedeling («fire øyne-prinsippet»)» and always inside a subsection headed "Interne misligheter", alongside logging, alerting, and access control. In each case Finanstilsynet is reporting what firms do, not imposing a rule: ROS 2024, "Foretakene benytter tjenestedeling ("fire øyne-prinsippet") så langt som mulig." ROS 2026 calls such controls "godt innarbeidet".

**Not found in IT inspection reports.** Four available IT inspection PDFs (DNB Bank 2022, ODIN Forvaltning 2021, Hølland og Setskog Sparebank 2021, Kredinor 2024) contain neither «fire øyne» nor «tjenestedeling». The 2023 Askim & Spydeberg Sparebank quote recorded elsewhere in this note comes from an anti-money-laundering inspection, a different document class, and was not re-checked in this pass.

**IKT-forskriften § 6 contained an approval requirement, not only a procedure requirement.** Both sentences: "Foretaket skal ha skriftlige prosedyrer for anskaffelse, utvikling, videreutvikling og testing av IKT-systemer. IKT-systemene skal ikke settes i ordinær drift før ansvarlig har godkjent dette." The second sentence bars putting a system into ordinary operation before the responsible person has approved it. Earlier drafts that describe the pre-2025 Norwegian rule as merely requiring that procedures exist understate it.

### The provision that named a person, and its repeal

IKT-forskriften § 6 second sentence: "IKT-systemene skal ikke settes i ordinær drift før ansvarlig har godkjent dette." Approval rested on «ansvarlig», the responsible one. Singular, no count given, and no species specified, but person-like in a way DORA's "functions" is not.

§ 9, headed "Avviks- og endringshåndtering", is confirmed as the change-management provision. Its first sentence is the one usually quoted: "Foretaket skal sikre at prosedyrer for avviks- og endringshåndtering foreligger og følges." The section continues on deviation handling, escalation, and incident reporting to Finanstilsynet, so the familiar quote is sentence one only, not the whole provision.

§ 10 was repealed by forskrift 17 December 2015 nr. 1732 ("§ 10 oppheves", in force immediately); the consolidated text shows "§ 10. (Opphevet)". In the 2003 promulgated text, § 10 was "Krav til kontinuitet", covering a current continuity plan, roles and risk, criteria for invoking fallback, and recovery procedures. Caveat: the regulation was amended twice in 2009, so the December 2015 wording may have differed. Lovdata exposes no version history and the Internet Archive rate-limited every attempt, so this could not be closed.

Dates confirmed: DORA-loven in force 1 July 2025, with Finanstilsynet stating "For mange foretak under tilsyn erstatter DORA-loven ... IKT-forskriften ... fra og med 1. juli 2025", and its Q&A confirming "Banker, betalingsforetak og e-pengeforetak er omfattet av virkeområdet til DORA, se art. 2." Full repeal by FOR-2026-08-20-1657 part IV, "Forskrift 21. mai 2003 nr. 630 om bruk av informasjons- og kommunikasjonsteknologi (IKT) oppheves", in force 1 September 2026 per part V.

## What the rule does not settle

**Whether the approving function must be a human.** Article 17(1)(b) requires independence between functions. It does not say the approving function is a person. An organisation that lets an automated reviewer approve routine changes would have to argue that the reviewer is an independent function, with its own ownership, and that this satisfies a risk-based reading of Article 9(4)(e). Nothing found in this research shows a supervisor accepting or rejecting that argument.

**Whether a teammate is a second function.** The most common implementation of a second pair of eyes is one developer approving another developer's change on the same team, under the same manager, with the same delivery objectives. Article 17(1)(b) asks for independence of the *functions* that approve from those that request and implement. Nothing in the text found settles whether same-team peer review meets that, or whether "functions" is meant at the organisational level implied by DORA Article 6(4)'s three lines of defence. Firms commonly treat author-cannot-approve-own-change segregation as sufficient. No supervisory statement either accepting or rejecting that reading was found. This is the weakest link in the common claim that a pull request satisfies the regulation.

**Whether the same model can implement and approve.** If one model generates a change and the same model, in another invocation, approves it, the independence in (b) is at least questionable. The research on LLM judges preferring their own output, recorded in the adoption draft, is the engineering version of the same worry. This is a question for the compliance function and for supervisory dialogue, not for the platform team alone.

**How depth may vary by risk.** Article 9(4)(e) says change management is "based on a risk assessment approach". A mechanical, reversible change and a change to money movement may legitimately receive different approval depth. The risk-based table in the AI review-capacity report is compatible with this. It is not a statement that a supervisor has endorsed such a table.

**What supervisors have said about AI-generated code.** Nothing found, and the absence was checked directly. The ESAs' joint statement JC 2026 25 of 31 July 2026, "Toward a consistent and risk-based approach for ICT risks from frontier AI models", was read in full (8 pages). The following terms appear zero times: "four eyes", "dual control", "segregation", "approval", "approve", "change management", and "human". The statement instead encourages automation of the delivery path, with a prevention row headed "Implement automated security controls into development, deployment, and operational workflows" and actions ranging "from basic automated vulnerability scanning and patch management to (AI-augmented) 'DevSecOps'". Its Annex disclaims new obligations: it "does not establish additional requirements, nor should be regarded as a comprehensive checklist." Where it does ask for human involvement, it means the board: "Management body accountability to evolve from periodic oversight to continuous, informed decision making." So the honest finding is that no rule was found, not that a rule forbids it. Finanstilsynet's ROS 2024 reports firms' own position: «Endringer i KI-løsninger må skje i henhold til foretakets rutiner for håndtering av endringer for å sikre at risikoen knyttet til bruk av løsningene ikke bryter med foretakets fastsatte risikotoleranse.» That concerns changes *to* AI systems, not changes *made by* AI.[^16][^5]

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
| RTS 2024/1774 Article 17(1)(b) wording. | Verified 15 September 2026 against the official Official Journal XHTML from the Publications Office Cellar repository (CELEX 32024R1774, `L_202401774EN.000101.fmx.xml`, OJ L, 25.6.2024). Word for word as quoted. EUR-Lex's own HTML endpoints sit behind an AWS WAF challenge and returned no content. |
| RTS 2024/1774 is incorporated into Norwegian law. | Finanstilsynet published a 2026 note on level 2 implementation and EFTA lists the act as EEA-relevant; the exact Norwegian entry-into-force date was not confirmed here. |
| A supervisor has accepted or rejected automated approval of routine changes. | Not found, and the absence was tested directly: the ESAs' July 2026 frontier-AI statement was read in full and contains none of "approval", "human", "segregation", or "four eyes". Absence of a rule, not a rule against. |
| Basel's dual control requires a human. | No. Paragraph 50 says "entities (usually persons)". |
| «Fire øyne» is a Norwegian change-management requirement. | No. It appears in Finanstilsynet's ROS reports under "Interne misligheter", describing what firms do about internal fraud, not as a rule about software changes. |
| The pre-2025 Norwegian rule only required that procedures exist. | Understated. § 6 also barred ordinary operation before «ansvarlig» had approved the system. |
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
