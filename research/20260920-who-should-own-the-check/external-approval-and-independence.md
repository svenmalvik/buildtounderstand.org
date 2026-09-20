# External approval and independence: what happens when the check leaves the team

**Question this document answers:** When a review or approval is moved out of the team that made the change and given to a separate body or function, what does the record show about the effect? And do the rules that are usually cited as the reason for doing it actually require it?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 03

**Last updated:** 2026-09-20

Scope: the evidence on externalised change approval, and the wording of the rules commonly invoked to justify it. It is a research note, not legal advice, and it does not describe any one company's compliance position. It complements `research/20260915-where-did-the-second-pair-of-eyes-come-from/functions-versus-persons.md`, which covers the same EU texts from the persons-versus-functions angle.

A naming hazard runs through this note. **DORA** means two unrelated things: Google's DevOps Research and Assessment program, and Regulation (EU) 2022/2554, the Digital Operational Resilience Act. Every section below says which one it means.

## Main findings

**No rule found here requires the reviewer to sit outside the implementing team.** Across four bodies of rules — EU DORA and its RTS, PCI DSS v4.0.1, the US federal audit manual FISCAM, and what SOX ITGC testing inherits from it — the strictest wording found is "persons independent of the programmer" (FISCAM CM-3.1.12) and "individuals other than the originating code author" (PCI DSS 6.2.3.1). Both are satisfied by a teammate. The EU rule is looser still: it names *functions*, not persons.

**The research finding everyone cites is a self-reported survey of about 1,000 people, not telemetry.** The 2019 Accelerate State of DevOps Report is the source of "no evidence was found to support the hypothesis that a more formal, external review process was associated with lower change fail rates." Sample: almost 1,000 respondents, snowball-sampled, cross-sectional, with both the practice and the outcome reported by the same person on the same questionnaire.

**A financial regulator's own study reached the same place by a different road, and with much better data.** The FCA analysed over 1 million production changes from 23 firms in 2019 and found CABs "approved over 90% of the major changes they reviewed, and in some firms the CAB had not rejected a single change during 2019." Major changes — the ones subject to CAB — failed at 3.8%, more than twice the 1.6% rate of all change types.

**But the FCA also found the opposite of the simple anti-governance reading.** "There was a positive correlation between the longevity of governance arrangements and higher change success rates." Governance was not the problem; a rubber-stamping body was. This is the finding that complicates the DORA story and it should not be left out of the chapter.

**Organisational distance is the named mechanism, in both the DORA capability page and Google's own research.** Google's own engineers report organisational distance as "the cause of delays in the review process"; DORA's capability page says "people that far removed from the change might not understand the implications of those changes." The cost is attributed to distance from the change, not to the existence of a second check.

**The one well-documented central review function that survived is a mentorship programme, not a gate — and it is still controversial internally.** Google's readability programme routes CLs to a centralised set of reviewers outside the author's team. It is staffed by 1–2% of Google engineers, all volunteers; ~20% of engineers are in the process at any time; Google's own internal research reports a net positive velocity effect. Google also publishes the complaint: "some engineers complain that it's an unnecessary bureaucratic hurdle and a poor use of engineer time."

---

## 1. The DORA (Google) finding on external change approval

### 1.1 The primary text: 2019 Accelerate State of DevOps Report

Source: Forsgren, N., Smith, D., Humble, J., Frazelle, J., *Accelerate State of DevOps 2019*, DORA / Google Cloud, 2019. Retrieved from <https://services.google.com/fh/files/misc/state-of-devops-2019.pdf> (pp. 48–52). Read from the PDF directly.

The setup, verbatim:

> "Others, backed by lean and agile philosophies, argue that more streamlined change approvals lead to faster feedback, better information flow, and better outcomes. To investigate these hypotheses, we created two new constructs—one that captures a lightweight, clearly understood change approval process, and another that captures a more formal, heavyweight change approval process—and tested their impact on software delivery performance."

The throughput finding, verbatim:

> "We found that formal change management processes that require the approval of an external body such as a change advisory board (CAB) or a senior manager for significant changes have a negative impact on software delivery performance. Survey respondents were 2.6 times more likely to be low performers if their organization had this kind of formal approval process in place. This expands on our previous research, which found that heavyweight change approvals process were negatively correlated with change failure rates."

The stability finding, verbatim:

> "The motivation behind the heavyweight change management processes proposed by ITSM frameworks is reducing the risk of releases. To examine this, we investigated whether a more formal approval process was associated with lower change fail rates and we found no evidence to support this hypothesis, consistent with earlier research. We also examined whether introducing more approvals results in a slower process and the release of larger batches less frequently, with an accompanying higher impact on the production system that is likely to be associated with higher levels of risk and thus higher change fail rates. Our hypothesis was supported in the data."

The prescription, verbatim:

> "We recommend that organizations move away from external change approval because of the negative effects on performance. Instead, organizations should 'shift left' to peer review-based approval during the development process."

And the recommended substitute, which is the point that matters most for the chapter:

> "One approach is to require every change be approved by someone else on the team as part of code review, either prior to commit to version control (as part of pair programming) or prior to merge into master."

Note the words *someone else on the team*. DORA's own recommended control for segregation of duties is an in-team reviewer. The report also states the regulatory premise it is working against, verbatim:

> "For example, segregation of duties, which states that changes must be approved by someone other than the author, is often required by regulatory frameworks. While we agree that no individual should have end-to-end control over a process (the intent of this control), there are lightweight, secure ways to achieve this objective that don't suffer the same coordination costs as heavyweight approaches."

The 1.8x counterpart finding, verbatim:

> "Survey respondents with a clear change process were 1.8 times more likely to be in elite performers"

**Sample size and method — survey, self-reported, correlational.** Verbatim:

> "This year, almost 1,000 individuals from a range of industries around the world added their voices to the 2019 Report."

> "With almost 1,000 respondents, our analyses have a 3% margin of error assuming 23 million software professionals worldwide and a 95% confidence interval."

> "This study employs a cross-sectional, theory-based design."

> "Because we don't have a master list of these people … we used snowball sampling to obtain respondents. … Our sample is likely limited to organizations and teams that are familiar with DevOps, and as such, may be doing some of it."

The footnote for "our previous research" points to: Velasquez, N., Kim, G., Kersten, N., & Humble, J. (2014). *State of DevOps Report: 2014*. Puppet Labs.

**Caveats the chapter should carry.** All outcome measures (change fail rate, lead time, deployment frequency) and the predictor (whether a heavyweight approval process exists) come from the same respondent on the same questionnaire. There is no telemetry. The design is cross-sectional and correlational, so "2.6 times more likely to be low performers" is an association, not a causal estimate. The sample is self-selecting and DevOps-aware by the report's own admission.

### 1.2 The *Accelerate* book (2018) wording

Forsgren, N., Humble, J., Kim, G., *Accelerate: The Science of Lean Software and DevOps*, IT Revolution Press, 2018, Chapter 7. The passage reproduced consistently across many independent sources:

> "We found that external approvals were negatively correlated with lead time, deployment frequency, and restore time, and had no correlation with change fail rate. In short, approval by an external body (such as a manager or CAB) simply doesn't work to increase the stability of production systems, measured by the time to restore service and change fail rate. However, it certainly slows things down. It is, in fact, worse than having no change approval process at all."

**Verification status: reproduced identically by multiple independent sources, but not read from the book.** The wording above is byte-identical across the Wikipedia article on change-advisory boards (<https://en.wikipedia.org/wiki/Change-advisory_board>), Octopus Deploy's engineering blog (<https://octopus.com/blog/change-advisory-boards-dont-work>), Kosli's blog, and several others. I could not open the book text itself and Google Books was rate-limited. Treat the quote as high-confidence but formally second-hand; if the essay quotes it, cite the book with a page number the author can check against a copy. The underlying data is the 2014–2017 State of DevOps Reports, i.e. the same survey instrument as §1.1, over four years.

### 1.3 The dora.dev capability page (current, undated)

Source: DORA, "Capabilities: Streamlining change approval," <https://dora.dev/capabilities/streamlining-change-approval/>. Retrieved 2026-09-20. This page cites the 2019 report and carries no later data.

> "Traditionally, these goals have been met through a heavyweight process involving approval by people external to the team proposing the change: a change advisory board (CAB) or a senior manager. However, DORA's research shows that these approaches have a negative impact on software delivery performance. Further, no evidence was found to support the hypothesis that a more formal, external review process was associated with lower change fail rates."

The mechanism it names, verbatim, from the "Common pitfalls" section:

> "Reliance on a centralized Change Approval Board (CAB) to catch errors and approve changes. This approach can introduce delay and often error. CABs are good at broadcasting change, but people that far removed from the change might not understand the implications of those changes."

> "Treating all changes equally. When all changes are subject to the same approval process, change review is inefficient, and people are unable to devote time and attention to those that require true concentration because of differences in risk profile or timing."

And the residual role it grants the CAB:

> "This transition, from gatekeeper to process architect and information beacon, is consistent with the practices of organizations that excel at software delivery performance."

### 1.4 Has DORA revisited the finding, 2023–2026?

**Short answer: no. The 2019 construct has not been re-tested in any report from 2023 to 2026.** The capability page still cites 2019. What the later reports add is adjacent, not confirmatory.

**2023** — *Accelerate State of DevOps 2023*, <https://services.google.com/fh/files/misc/2023_final_report_sodr.pdf>. Sample: "This year, nearly 3,000 working professionals" (survey, self-reported). No CAB or external-approval construct. What it does say, verbatim:

> "Teams with shorter code review times have 50% better software delivery performance."

> "When subject-matter experts are closer to the team, they can review code faster because they have a better understanding of the impact of the changes. A loosely coupled design enables the team to test, build, and deploy without other teams being a potential bottleneck."

> "The involvement of multiple teams across geographical locations leads to longer duration, less engagement in the process, and increased costs."

This is the closest DORA has come to re-stating the distance argument since 2019, and it is about *review*, not approval boards. Note "50% better software delivery performance" is a survey-to-survey association with n ≈ 3,000, not a measured latency reduction.

**2024** — *Accelerate State of DevOps 2024*, <https://services.google.com/fh/files/misc/2024_final_dora_report.pdf>. Sample: "nearly 3,000 working professionals" (survey; recruited by a mix of snowball and paid panel). The relevant AI finding, verbatim:

> "A 25% increase in AI adoption is associated with a… 7.5% increase in documentation quality / 3.4% increase in code quality / 3.1% increase in code review speed / 1.3% increase in approval speed / 1.8% decrease in code complexity"

The report immediately qualifies it, verbatim, and this qualification is more useful to the essay than the numbers:

> "Of course, faster code reviews and approvals do not equate to better and more thorough code review processes and approval processes. It is possible that we're gaining speed through an over-reliance on AI for assisting in the process or trusting code generated by AI a bit too much. This finding is not at odds with the patterns in Figure 9, but it also not the obvious conclusion."

The report's own definitions of the two measures, verbatim:

> "Code review speed — The average time required to complete a code review for the primary application or service."
> "Approval speed — The typical duration from proposing a code change to receiving approval for production use in the primary application or service."

Both are respondent estimates, not instrumented timings.

**2025** — *State of AI-assisted Software Development* (the 2025 DORA report), <https://services.google.com/fh/files/misc/2025_state_of_ai_assisted_software_development.pdf>. Sample, verbatim: "This year, a total of 4,867 respondents answered our survey," collected "between June 13 and July 21, 2025," plus "more than 100 hours of qualitative data." The relevant key findings, verbatim:

> "AI adoption has become nearly universal. The majority of survey respondents (90%) use AI as part of their work and believe (more than 80%) it has increased their productivity. Yet a notable portion (30%) currently report little to no trust in the code generated by AI, indicating a need for critical validation skills."

> "AI adoption now improves software delivery throughput, a key shift from last year. However, it still increases delivery instability. This suggests that while teams are adapting for speed, their underlying systems have not yet evolved to safely manage AI-accelerated development."

> "While most developers use AI to increase productivity, there is healthy skepticism about the quality of its output. This 'trust but verify' approach is a sign of mature adoption."

> "AI's primary role in software development is that of an amplifier. It magnifies the strengths of high-performing organizations and the dysfunctions of struggling ones."

The 2025 report contains no CAB or external-approval construct either.

**2026** — **no DORA report exists as of 2026-09-20.** The dora.dev research index (<https://dora.dev/research/>) lists 2014 through 2025 and nothing later; the dora.dev homepage still promotes the 2025 "ROI of AI-assisted Software Development" report as its latest. So there is nothing from a 2026 DORA report on AI and review/approval to cite. If the essay needs a 2026 data point on this, it does not yet exist from DORA. (DORA reports have historically appeared in September–October, so one may land during the essay's life.)

---

## 2. ITIL, the CAB, and what it is supposed to protect

**Verification status: weak. I could not read the ITIL primary text.** ITIL 4 and ITIL v3 publications are behind Axelos/PeopleCert licensing and I could not fetch them. The claims below come from how the CAB is characterised by parties describing it from outside, and should be labelled as such in the essay.

What a CAB is *for*, in the DORA capability page's characterisation (§1.3): "Compliance managers and security managers rely on change management processes to validate compliance requirements, which typically require evidence that all changes are appropriately authorized." And the two stated goals: "decreasing the risk of making changes, and satisfying regulatory requirements."

The FCA glossary (see §4) defines it, verbatim:

> "Change Advisory Board — A governance body that support the assessment,"

(the FCA page truncates the definition at that point in the rendered HTML; the full glossary entry is in the PDF, which I did not open.)

The FCA also records what firms said the CAB should be, verbatim:

> "workshop attendees emphasised that CAB members should be carefully selected to ensure that the requested changes are thoroughly checked from both a technical and business perspective. Firms also stressed the importance of having a range of Subject Matter Experts (SMEs) review the changes from both a technical and business perspective."

That is the steelman for an out-of-team body: not more eyes, but *different* eyes — business impact that the implementing team cannot see. The essay should engage with this rather than the weaker "more scrutiny" claim.

---

## 3. The regulated-industry counterpart: who must actually review?

### 3.1 EU DORA and the RTS — *functions*, not persons, and no requirement to be outside the team

Read directly from the Official Journal text on EUR-Lex (CELEX 32022R2554 and 32024R1774).

**Regulation (EU) 2022/2554, Article 9(4)(e)** — <https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32022R2554>. Verbatim, in full:

> "implement documented policies, procedures and controls for ICT change management, including changes to software, hardware, firmware components, systems or security parameters, that are based on a risk assessment approach and are an integral part of the financial entity's overall change management process, in order to ensure that all changes to ICT systems are recorded, tested, assessed, approved, implemented and verified in a controlled manner;"

**Article 9(4)(e) says nothing about who approves.** The word "approved" appears with no actor attached. The independence requirement lives one level down, in the RTS.

**Commission Delegated Regulation (EU) 2024/1774, Article 17(1)** — <https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32024R1774>. For all changes to software, hardware, firmware, systems or security parameters, verbatim:

> "(a) a verification of whether the ICT security requirements have been met"
>
> "(b) mechanisms to ensure the independence of the functions that approve changes and the functions responsible for requesting and implementing those changes"
>
> "(c) a clear description of the roles and responsibilities to ensure that: (i) changes are specified and planned; (ii) an adequate transition is designed; (iii) the changes are tested and finalised in a controlled manner; (iv) there is an effective quality assurance"
>
> "(d) the documentation and communication of change details, including: (i) the purpose and scope of the change; (ii) the timeline for the implementation of the change; (iii) the expected outcomes"
>
> "(e) the identification of fall-back procedures and responsibilities, including procedures and responsibilities for aborting changes or recovering from changes not successfully implemented"
>
> "(f) procedures, protocols, and tools to manage emergency changes that provide adequate safeguards"
>
> "(g) procedures to document, re-evaluate, assess, and approve emergency changes after their implementation, including workarounds and patches"
>
> "(h) the identification of the potential impact of a change on existing ICT security measures and an assessment of whether such change requires the adoption of additional ICT security measures"

**Article 16(3)**, on code review, verbatim:

> "The procedure referred to in paragraph 2 shall contain the performance of source code reviews covering both static and dynamic testing. That testing shall contain security testing for internet-exposed systems and applications in accordance with Article 8(2), point (b), points (v), (vi) and (vii)."

Note: Article 16(3) requires *static and dynamic testing*, i.e. tools. It does not require a human reader.

**DORA Article 6(4)**, the organisational-independence provision, verbatim:

> "Financial entities, other than microenterprises, shall assign the responsibility for managing and overseeing ICT risk to a control function and ensure an appropriate level of independence of such control function in order to avoid conflicts of interest. Financial entities shall ensure appropriate segregation and independence of ICT risk management functions, control functions, and internal audit functions, according to the three lines of defence model, or an internal risk management and control model."

**Answer to the question posed: the EU rule requires a separate *function*, not a person outside the team.** Article 17(1)(b) attaches the obligation to "mechanisms to ensure the independence," not to an organisational chart. The stated purpose, per RTS recital 17, is objectivity and conflict-of-interest avoidance — not defect detection. Whether two developers on the same team under the same manager constitute two functions is not resolved by any text; see the companion note `functions-versus-persons.md` for the fuller argument, including the point that EBA/GL/2021/05 ¶175's definition of an independent internal control function would exclude a teammate, but that Article 17(1)(b) never says the approving function must be a second-line control function.

### 3.2 PCI DSS v4.0.1 — conditional on choosing manual review

**Verification status: partial. The PCI SSC document library requires acceptance of a licence agreement; direct fetches of the PDF returned HTTP 403.** The requirement text below was obtained from two independent compliance-framework mirrors that reproduce it identically, not from the PCI SSC PDF.

**Requirement 6.2.3**, the parent, verbatim (source: <https://ce.prod.cloudaware.com/frameworks/pci-dss-v4.0/06/02/03/>):

> "Bespoke and custom software is reviewed prior to being released into production or to customers, to identify and correct potential coding vulnerabilities."

The bullets under it, as reproduced:

> "Code reviews ensure code is developed according to secure coding guidelines"
> "Code reviews look for both existing and emerging software vulnerabilities"
> "Appropriate corrections are implemented prior to release"

**6.2.3 names no actor at all.** It says code is "reviewed." It does not say by whom, or by what.

**Requirement 6.2.3.1**, verbatim (identical wording at <https://ce.prod.cloudaware.com/frameworks/pci-dss-v4.0/06/02/03/01/> and <https://learn.daydream.ai/requirements/pci-dss-6-2-3-1>):

> "If manual code reviews are performed for bespoke and custom software prior to release to production, code changes are reviewed by individuals other than the originating code author, and who are knowledgeable about code-review techniques and secure coding practices reviewed and approved by management prior to release."

**Two things follow, and both matter for the chapter.** First, the sentence opens with **"If manual code reviews are performed"** — the different-person requirement is conditional on the organisation choosing manual review. The standard does not mandate manual review; 6.2.3 can be satisfied by other means. Second, where it does impose a person requirement, the bar is **"individuals other than the originating code author"** — the author's teammate qualifies. Nothing here requires a reviewer outside the team.

**What I could not verify for PCI:** the exact wording of the 6.2.3 Applicability Notes and the text that explicitly permits automated code review tools. The lead's brief asserts 6.2.3 "permits automated code review tools" and that is consistent with 6.2.3.1's conditional framing, but I could not read the sentence that says so from a primary source. Do not quote a specific automated-tools sentence without opening the PCI SSC PDF.

### 3.3 SOX IT general controls — what the audit manuals actually say

SOX itself (Sarbanes-Oxley §404) and PCAOB AS 2201 set no code-review requirement; the specifics come from audit programmes built on control frameworks. The most authoritative *public* text is GAO's Federal Information System Controls Audit Manual (FISCAM), GAO-09-232G, <https://www.gao.gov/assets/gao-09-232g.pdf>, which is what federal ITGC testing runs on and which the Big Four ITGC programmes closely parallel.

**FISCAM CM-3.1.12**, verbatim — the strongest person-level requirement found anywhere in this research:

> "Program changes are moved into production only when approved by management and by persons independent of the programmer."

Independent of *the programmer*. Not independent of the team. The associated audit procedure, verbatim:

> "Examine a selection of program changes to determine whether they were approved by management prior to being moved to production."

**FISCAM CM-3.1.4**, verbatim — and note where it puts the reviewer:

> "Detailed specifications are prepared by the programmer and reviewed by a programming supervisor for system and application software changes."

The reviewer here is the programmer's own supervisor: inside the team, and above it in the reporting line. This is the opposite of an external board.

**FISCAM CM-3.1.16**, verbatim:

> "Program development and maintenance, testing, and production programs are maintained separately (for example, libraries) and movement between these areas is appropriately controlled, including appropriate consideration of segregation of duties"

with the audit procedure:

> "Review program changes procedures for adherence to appropriate segregation of duties between application programming and movement of programs into production."

**FISCAM's segregation-of-duties chapter** locates the separation between activities, verbatim:

> "Key areas of concern during a general controls review involve the segregation of duties among major operating and programming activities, including duties performed by users, application programmers, and data center staff. For example, where possible, the following types of activities should be separated: development versus production, security versus audit, accounts payable versus accounts receivable, and encryption key management versus the changing of keys."

And the risk it is guarding against, verbatim:

> "Inadequate segregation of duties (for example, software developer is the same individual who puts the software into production)."

**Answer to the question posed: what an auditor tests for is that the person who wrote the code is not the person who deployed it, and that management approved the move.** The separation is *developer versus deployer*, not *team versus external body*. FISCAM also explicitly scales the expectation to organisation size, verbatim:

> "The extent to which duties are segregated depends on the size of the entity and the risk associated with its facilities and activities. … These smaller entities may rely more extensively on supervisory review to control activities."

---

## 4. A central approval body, measured: the FCA's 1-million-change study

Source: Financial Conduct Authority, *Implementing Technology Change*, multi-firm review, published 5 February 2021. <https://www.fca.org.uk/publications/multi-firm-reviews/implementing-technology-change>. This is a **regulator's own first-party study**, not a survey of opinions and not vendor marketing. It is the strongest evidence in this note.

**Method and sample, verbatim:**

> "We used a data-driven approach to analyse over 1m production changes implemented in 2019 by a sample of FS companies leveraging different business models at varying scale. We supplemented our data with a qualitative questionnaire, a confidential board questionnaire and industry workshops"

> "we requested 18 key operational metrics from 23 firms. This included the total number of IT changes implemented by change type over 2019, the number of incidents resulting from change by type, the proportion of incidents that had an impact on customers and the average change implementation duration over 2019."

So: change-log data (1m+ changes, 23 firms) plus questionnaires and workshops. Mixed method, with the headline numbers drawn from firm-submitted operational data rather than self-assessment.

**The CAB finding, verbatim:**

> "The Change Advisory Board (CAB) was one of the key controls firms used when implementing major changes. However, we found that CABs approved over 90% of the major changes they reviewed and in some firms, they had not rejected a single change during 2019. This may indicate that many CABs perform more of a 'flight control' role rather than an assurance function."

**The failure rates, verbatim:**

> "Our analysis showed that, in general, change was managed effectively by the industry with 1.6% of technology changes resulting in an incident. However, due to the volume of change implemented by sample firms, this resulted in significant disruption; amounting to over 13,767 incidents in 2019, of which 14% had customer-facing impact."

> "In total, the sampled firms deployed nearly 68,000 major changes over 2019, which resulted in 2,600 incidents. This is an average failure rate of 3.8%, compared to 1.6% from all change types. We understand that major changes are generally subject to a higher level of scrutiny and governance due to the potential for disruption to services. However, despite the increased oversight, we found that changes classified as 'major' are twice as likely to result in an incident when compared with other change types. Workshop attendees attributed this to their complexity, and the inability to break them down into smaller components."

**The finding that complicates the story, verbatim** — do not omit this from the chapter:

> "While there is no single approach, process, or control that improves change success rates, our analysis and discussions with firms found that stronger governance, day-to-day risk management, increased automation and more robust testing and planning can contribute to successful change activity and less disruption."

> "There was a positive correlation between the longevity of governance arrangements and higher change success rates in the sampled firms. Our data showed that robust governance can help reduce the number and impact of operational incidents resulting from change."

> "We found that the majority of firms had their current technology change governance arrangements in place for between 6 months and a year. We found a positive correlation between the longevity of governance arrangements and higher change success rates in the firms. Firms that had governance arrangements in place for more than a year experienced a lower proportion of incidents resulting from change when compared to peers with newer arrangements."

**On batch size, converging with DORA, verbatim:**

> "Overall, we found that firms that deployed smaller, more frequent releases had higher change success rates than those with longer release cycles. Firms that made effective use of agile delivery methodologies were also less likely to experience a change incident."

**On manual review as a risk, verbatim:**

> "However, we found that firms are still heavily reliant on manual testing and peer review, both of which are prone to human error."

**From the earlier proof-of-concept (4 firms, 2018 data, ~8.5 million data points), verbatim:**

> "CABs were also not being used as effectively as they could be to mitigate the risks associated with change."

**Reading the causality carefully.** The 3.8% vs 1.6% comparison is not evidence that CABs cause failures — major changes are selected into CAB review *because* they are risky and complex, and the FCA explicitly attributes their failure rate to "their complexity, and the inability to break them down into smaller components." What the data does support is narrower and still damaging: a body that approves over 90% of what it sees, and in some firms rejects nothing at all in a year, is not functioning as a filter. The 90% approval rate is the finding to lead with; the 3.8% is context, not proof.

---

## 5. A central review function that was built, measured, and kept: Google readability

Source: Winters, T., Manshreck, T., Wright, H. (eds.), *Software Engineering at Google*, O'Reilly, 2020, Chapter 3, "Knowledge Sharing." Free full text at <https://abseil.io/resources/swe-book/html/ch03.html>. This is a **first-party company account**, including its own criticism.

This is the closest thing in the public record to a working central code review function for software changes. Verbatim:

> "At Google, 'readability' refers to more than just code readability; it is a standardized, Google-wide mentorship process for disseminating programming language best practices."

> "Readability started as a one-person effort. In Google's early days, Craig Silverstein (employee ID #3) would sit down in person with every new hire and do a line-by-line 'readability review' of their first major code commit."

> "Today, around 20% of Google engineers are participating in the readability process at any given time, as either reviewers or code authors."

> "Around 1 to 2% of Google engineers are readability reviewers. All reviewers are volunteers, and anyone with readability is welcome to self-nominate to become a readability reviewer."

**The explicit centralisation trade-off, verbatim — this is the most quotable passage in this note:**

> "One of the primary advantages of the readability program is that it exposes engineers to more than just their own team's tribal knowledge. To earn readability in a given language, engineers must send CLs through a centralized set of readability reviewers who review code across the entire company. Centralizing the process makes a significant trade-off: the program is limited to scaling linearly rather than sublinearly with organization growth, but it makes it easier to enforce consistency, avoid islands, and avoid (often unintentional) drifting from established norms."

**The named costs, verbatim:**

> "These benefits come with some costs: readability is a heavyweight process compared to other mediums like documentation and classes because it is mandatory and enforced by Google tooling"

> "Increased friction for teams that do not have any team members with readability, because they need to find reviewers from outside their team to give readability approval on CLs."

> "Potential for additional rounds of code review for authors who need readability review."

**The internal dissent, published by Google itself, verbatim:**

> "But aspirations aren't enough. Readability is a controversial program: some engineers complain that it's an unnecessary bureaucratic hurdle and a poor use of engineer time."

**The internal evidence for keeping it, verbatim:**

> "The EPR team performed in-depth studies of readability, including but not limited to whether people were hindered by the process, learned anything, or changed their behavior after graduating. These studies showed that readability has a net positive impact on engineering velocity. CLs by authors with readability take statistically significantly less time to review and submit than CLs by authors who do not have readability."

> "Self-reported engineer satisfaction with their code quality—lacking more objective measures for code quality—is higher among engineers who have readability versus those who do not."

**What makes this survive where CABs do not — and the caveat.** Readability is a *certification* function with an exit: authors graduate out of it and then approve their own CLs. It is not a standing gate on every change forever. Google states this directly: "Certified authors implicitly provide readability approval of their own CLs." The out-of-team check is temporary by design, and the reviewers are volunteers with subject-matter expertise, not a scheduled board.

**Caveat on the velocity claim.** "CLs by authors with readability take statistically significantly less time to review and submit" compares *authors who have completed the programme* with *authors who have not*. Google's own footnote acknowledges the confound: "This includes controlling for a variety of factors, including tenure at Google and the fact that CLs for authors who do not have readability typically need additional rounds of review compared to authors who already have readability." The underlying study is not published; only the summary is. Treat the velocity number as a first-party claim about an unpublished internal study, not as independent evidence. Readability also applies only inside the monorepo: "readability as described here applies only to the monorepo because it is a notion of within-repository consistency."

---

## 6. Out-of-team review, measured at Google

Source: Sadowski, C., Söderberg, E., Church, L., Sipko, M., Bacchelli, A., "Modern Code Review: A Case Study at Google," *ICSE-SEIP '18*, Gothenburg, 2018. <https://sback.it/publications/icse2018seip.pdf>. Peer-reviewed, industrial-track, with telemetry.

**Sample — this is telemetry, not a survey, and the only large telemetry dataset in this note besides the FCA's:**

> "Our final dataset includes the approximately 9 million changes created by more than 25,000 authors and reviewers from January 2014 until July 2016 that meet these criteria, and about 13 million comments collected from all changes between September 2014 and July 2016."

Supplemented by 12 interviews (median tenure 5 years) and a questionnaire sent to 98 engineers.

**What review is for, verbatim:**

> "Finding 1. Expectations for code review at Google do not center around problem solving. Reviewing was introduced at Google to ensure code readability and maintainability. Today's developers also perceive this educational aspect, in addition to maintaining norms, tracking history, gatekeeping, and accident prevention. Defect finding is welcomed but not the only focus."

**The two out-of-team mechanisms, verbatim:**

> "Ownership. The Google codebase is arranged in a tree structure, where each directory is explicitly owned by a set of people. Although any developer can propose a change to any part of the codebase, an owner of the directory in question (or a parent directory) must review and approve the change before it is committed; even directory owners are expected to have their code reviewed before committing."

> "Every change must be either authored or reviewed by someone with a readability certification for the language(s) used."

**Latency, verbatim:**

> "In terms of speed, we find that developers have to wait for initial feedback on their change a median time of under an hour for small changes and about 5 hours for very large changes. The overall (all code sizes) median latency for the entire review process is under 4 hours. This is significantly lower than the median time to approval reported by Rigby and Bird, which is 17.5 hours for AMD, 15.7 hours for Chrome OS and 14.7, 19.8, and 18.9 hours for the three Microsoft projects. Another study found the median time to approval at Microsoft to be 24 hours."

**Reviewer count, verbatim:**

> "At Google, by contrast, fewer than 25% of changes have more than one reviewer, and over 99% have at most five reviewers with a median reviewer count of 1."

**Change size, verbatim:**

> "At Google, over 35% of the changes under consideration modify only a single file and about 90% modify fewer than 10 files. Over 10% of changes modify only a single line of code, and the median number of lines modified is 24."

**The distance finding — the direct empirical answer to the research question, verbatim:**

> "Distance: Interviewees perceive distance in code review from two perspectives: geographical (i.e., the physical distance between the author and reviewers) and organizational (e.g., between different teams or different roles). Both these types of distance are perceived as the cause of delays in the review process or as leading to misunderstandings."

Note this is from the qualitative strand (12 interviews), not the 9-million-change telemetry. It is perception, reported in a peer-reviewed venue, not a measured latency differential by organisational distance. The authors state the generalisability limit explicitly: "our results may not generalize to other contexts."

**A second finding worth the chapter's attention, verbatim** — on what an approval gate becomes when it is a source of leverage over another person:

> "Power refers to using the code review process to induce another person to change their behavior; for example, dragging out reviews or withholding approvals."

---

## What I could not verify

1. **The *Accelerate* (2018) book quote from the book itself.** Reproduced byte-identically across Wikipedia, Octopus Deploy's blog, Kosli's blog and several LinkedIn posts, but I never opened the book. Google Books API was over quota. **Mark as second-hand** or check against a physical copy before quoting with a page number.

2. **PCI DSS v4.0.1 from the PCI SSC PDF.** All direct fetches returned HTTP 403; the document library requires accepting a licence. Requirements 6.2.3 and 6.2.3.1 were read from two independent compliance-framework mirrors with identical wording. **The Applicability Notes and the sentence permitting automated code review tools were not obtained at all.** Do not quote a specific automated-tools clause. Requirements 6.5.3 and 6.5.4 (pre-production / production environment separation and separation of duties between development and production personnel) were **not retrieved** and are unverified.

3. **ITIL's own definition of the CAB and what it is chartered to protect.** Axelos/PeopleCert publications are paywalled. Section 2 rests entirely on how outside parties characterise the CAB, which is a weak basis for a claim about what ITIL requires. If the chapter makes a claim about what ITIL says, it needs a source I did not find.

4. **The FCA glossary's full definition of "Change Advisory Board."** The rendered HTML truncates it; the PDF was not opened.

5. **DORA (Google) 2026.** No 2026 report exists as of 2026-09-20. dora.dev/research lists 2014–2025 only. Any claim about "the 2026 DORA report" would be fabrication.

6. **DORA (Google) 2020, 2021, 2022** were not checked for a re-test of the change-approval construct. I checked 2023, 2024 and 2025 and found none; the 2019 finding is still what the current capability page cites, which is strong indirect evidence that it has not been re-tested, but I did not read 2020–2022 to confirm.

7. **A documented reversal — an organisation that built a central code review board and then dismantled it, with published numbers on queue depth or staffing cost.** I did not find one. Google's readability is the nearest published account and it was *kept*, not reversed; its costs are named qualitatively ("increased friction," "additional rounds of code review") but never quantified in days, queue length or FTE. Web search was unavailable for the latter half of this research (session budget exhausted, then DuckDuckGo rate-limiting), so absence here is weak evidence of absence. **This is the biggest remaining gap and worth a second pass with working search.**

8. **Sample size for the 2024 DORA report** is given in the report as "nearly 3,000 working professionals" — I could not find a precise integer, unlike 2025's 4,867.

9. **Big Four / PCAOB / ISACA descriptions of SOX ITGC change-management testing.** ISACA's page 404'd and searches failed. Section 3.3 rests on GAO FISCAM, which is a genuine federal audit manual and is closely paralleled by commercial ITGC programmes, but is **not** itself SOX guidance. Do not write "SOX requires" on the basis of FISCAM; write "the federal audit manual that federal ITGC testing runs on requires."

## Source inventory by type

| Source | Type | Sample | Primary? |
| --- | --- | --- | --- |
| Accelerate State of DevOps 2019 | Survey, self-reported, cross-sectional | ~1,000 respondents | Yes, read from PDF |
| Accelerate (book, 2018) | Survey, 2014–2017 reports pooled | Not stated in quote | No, second-hand |
| dora.dev capability page | Vendor/programme summary of 2019 | n/a | Yes, read directly |
| DORA 2023 / 2024 / 2025 reports | Survey, self-reported | ~3,000 / ~3,000 / 4,867 | Yes, read from PDF |
| FCA, Implementing Technology Change (2021) | Regulator study, operational change-log data + questionnaires + workshops | 23 firms, >1m changes (2019); PoC: 4 firms, ~8.5m data points (2018) | Yes, read directly |
| Reg (EU) 2022/2554; Del. Reg (EU) 2024/1774 | Regulation text | n/a | Yes, EUR-Lex OJ text |
| PCI DSS v4.0.1 6.2.3, 6.2.3.1 | Standard text | n/a | **No** — two mirrors, PDF gated |
| GAO FISCAM (GAO-09-232G) | Federal audit manual | n/a | Yes, read from PDF |
| Software Engineering at Google, ch. 3 | First-party company account + unpublished internal study | ~20% of engineers in process; 1–2% are reviewers | Yes, read directly |
| Sadowski et al., ICSE-SEIP 2018 | Peer-reviewed, telemetry + 12 interviews + 98-person survey | ~9m changes, >25,000 people | Yes, read from PDF |
