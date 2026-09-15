# Functions versus persons: who or what may approve a change

**Question this document answers:** When a rule requires a second party to approve a software change, do the rules say that party must be a different *person*, or a different *organisational function*? And does anything forbid a machine from being that party?

**Chapter it feeds:** `_explorations/what-is-the-second-pair-of-eyes-for.md`, chapter 01, "The Regulator's Pair of Eyes", and the ownership question in chapter 03.

**Last updated:** 2026-09-15

Scope: the wording of the rules, not advice about any firm's compliance position. Prompted by a plain question about the draft: if the approver is usually another developer on the same team, is that a second function or merely a second person?

## Main findings

**No rule found in this research says the approver must be a human being.** Across seven bodies of rules, the pattern is silence rather than prohibition. One source, a federal audit manual, says the approver must be a different *person*. One, written for the payments industry, makes the different-person requirement conditional on choosing manual review. The rest either speak of roles and functions or name no actor at all.

**The EU rule speaks of functions and never defines the word.** Where the same regulation means people, it says staff. Where it explains segregation of duties, it points at the three lines of defence model, which is a statement about parts of an organisation rather than about individuals.

**This leaves the common practice unexamined.** One developer approving a teammate's change is plainly a second person. Whether two developers on the same team, under the same manager, constitute two functions is not settled by any text found here.

## The EU wording, read directly

Verified from the official Official Journal text (Publications Office, CELEX 32022R2554 and 32024R1774).

**There is no general definition of "function".** The delegated regulation has no definitions article: Article 1 is the proportionality principle, Article 2 covers general elements of ICT security policies. DORA defines only "critical or important function", and defines it as a function "the disruption of which would materially impair the financial performance of a financial entity, or the soundness or continuity of its services and activities". A thing that can be disrupted is an activity, not a person. Even the one definition available treats a function as something the organisation does.

**The same regulation says staff when it means people.** RTS Article 2(1)(d) requires ICT security policies to "specify the responsibilities of staff at all levels to ensure the financial entity's ICT security". Article 2(1)(e) refers to "non-compliance by staff". So a word for human beings was available and used elsewhere.

**Segregation of duties is tied to the three lines of defence.** RTS Article 2(1)(g) requires policies to "specify the segregation of duties arrangements in the context of the three lines of defence model or other internal risk management and control model, as applicable, to avoid conflicts of interest". DORA Article 6(4) similarly requires "appropriate segregation and independence of ICT risk management functions, control functions, and internal audit functions, according to the three lines of defence model". Both passages use "function" for an organisational unit standing in a defined relationship to the business, not for a role held by one employee.

**The requirement itself.** RTS Article 17(1)(b): "mechanisms to ensure the independence of the functions that approve changes and the functions responsible for requesting and implementing those changes." Functions, twice.

## What other rule sets say

Verified by a separate research pass against primary sources where reachable.

| Body of rules | Approver described as | Automation as the independent check |
| --- | --- | --- |
| DORA and RTS 2024/1774 (EU) | "functions", undefined | silent |
| PCI DSS v4.0 | "authorized parties", "roles and functions"; "individuals" only where review is manual | permitted explicitly |
| NIST SP 800-53 Rev 5 | "approval authorities"; "individuals or roles" | permitted for workflow and deployment, silent on the decision |
| GAO FISCAM | "persons independent of the programmer" | silent |
| PCAOB AS 2201 / AS 2110 | silent | silent; automated controls treated as lower risk |
| AICPA TSP 100 CC8.1 | silent | silent |
| ISO/IEC 27002:2022 | not verified, paywalled | not verified |
| COBIT 2019 BAI06 | not verified, paywalled | not verified |

### PCI DSS is the closest precedent for a machine

It is the one standard here written for the payments industry, and it addresses the question directly.

Requirement 6.2.3 requires that bespoke software "is reviewed prior to being released into production or to customers, to identify and correct potential coding vulnerabilities", and its Applicability Notes state: "Code reviews may be performed using either manual or automated processes, or a combination of both."

Requirement 6.2.3.1 then attaches the different-person rule to the manual path only: "If manual code reviews are performed for bespoke and custom software prior to release to production, code changes are: Reviewed by individuals other than the originating code author... Reviewed and approved by management prior to release." Its Applicability Notes add a third distinct party: "An individual that has been formally granted accountability for release control and who is neither the original code author nor the code reviewer fulfills the criteria of being management."

So in PCI DSS, choosing automated review means requirement 6.2.3.1 does not apply by its own terms. The independent-human requirement is a consequence of choosing a human process.

Requirement 6.5.4 separates at the organisational level: "Roles and functions are separated between production and pre-production environments to provide accountability such that only reviewed and approved changes are deployed." Its Applicability Notes permit one person to hold both: "In environments with limited personnel where individuals perform multiple roles or functions, this same goal can be achieved with additional procedural controls that provide accountability." The glossary, by contrast, defines separation of duties at the person level, as "dividing steps in a function among multiple individuals".

Caveat: verified against v4.0 (March 2022) via an Internet Archive copy, because the current document sits behind a licence form. Differences in v4.0.1 were not checked.

### NIST automates around the decision, not the decision

An earlier hypothesis that NIST permits automated approval is wrong. CM-3(1), "Automated Documentation, Notification, and Prohibition of Changes", uses automated mechanisms to "Notify [approval authorities] of proposed changes to the system and request change approval" and to "Prohibit changes to the system until designated approvals are received". The mechanism requests approval from an authority rather than granting it. CM-3(3) automates implementation and CM-3(5) automates response to unauthorised change. The approval decision itself is untouched. CM-3b names no actor: "Review proposed configuration-controlled changes to the system and approve or disapprove such changes".

SA-11(1) requires static analysis but keeps a human judging the output, asking for "evidence that defects were inspected by developers or security professionals".

### The strictest source is an audit manual, not a regulation

GAO's FISCAM CM-3.1.12 is the only text found that states the rule at the person level: "Program changes are moved into production only when approved by management and by persons independent of the programmer." Its section 3.4 adds: "one computer programmer should not be allowed to independently write, test, and approve program changes. Often, segregation of duties is achieved by splitting responsibilities between two or more organizational groups."

That last sentence is worth noting: even the person-level source describes the usual implementation as splitting work between organisational groups, which is a function-level control.

### The standards behind SOX work never say who

PCAOB AS 2201 does not mention segregation of duties or change management. Its one relevant line favours machines: "an automated control would generally be expected to be lower risk if relevant information technology general controls are effective". AS 2110 Appendix B states the risk rather than the control: "The possibility of IT personnel gaining access privileges beyond those necessary to perform their assigned duties, thereby breaking down segregation of duties."

AICPA TSP Section 100, CC8.1, is silent on the actor: "Approves System Changes: A process is in place to approve system changes prior to implementation." Its segregation point of focus permits substitution: "Management segregates incompatible duties and, where such segregation is not practical, management selects and develops alternative control activities."

## What this does and does not settle

Settled: the EU rule says functions, gives no definition, uses "staff" for people elsewhere, and ties segregation of duties to the three lines of defence. No rule found requires a human approver. PCI DSS explicitly contemplates automated code review, and makes its different-person rule conditional on the manual path.

Not settled: whether same-team peer review satisfies RTS Article 17(1)(b). Whether a supervisor would accept an automated approver for low-risk changes. Whether ISO 27002 or COBIT phrase this at the person or function level, both being paywalled.

## Confidence and gaps

| Claim | Assessment |
| --- | --- |
| RTS 2024/1774 has no definition of "function" | High. Article-by-article check of the official text; no definitions article exists. |
| DORA's "critical or important function" describes an activity | High. Quoted definition turns on disruption of services. |
| RTS Article 2(1)(g) ties segregation of duties to the three lines of defence | High. Quoted from official text. |
| PCI DSS makes the different-person rule conditional on manual review | High for v4.0. Read from the official PDF via Internet Archive. v4.0.1 unchecked. |
| NIST permits automated change approval | False. Corrected during this research. Automation covers notification, prohibition, and implementation only. |
| Some rule somewhere forbids automated approval | Not found in seven bodies of rules. Silence, not prohibition. |
| ISO 27002 and COBIT wording | Unverified. Both paywalled; do not assert their wording. |

## Related documents

- [`four-eyes-regulation.md`](./four-eyes-regulation.md), the regulatory root and the Norwegian chain.
- [`why-people-wanted-another-person.md`](./why-people-wanted-another-person.md), the motives behind peer review.
