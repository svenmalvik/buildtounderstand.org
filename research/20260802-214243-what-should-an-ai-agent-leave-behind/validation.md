# Validation report

## Verdict

**PASS_WITH_NOTES**

The updated dossier satisfies the research plan, structural minimums, source minimums, global sourcing rules, and all six tasks from the first validation. The checkable defects are corrected: MCP's release candidate is dated `2026-05-29` and its stable revision `2026-07-28`; community quotations carry exact dates, handles or names, and direct URLs; the undated LinkedIn dissent is now a transparent paraphrase rather than a quotation; temporal claims use `YYYY-MM-DD`; SCITT architecture references consistently use draft `-22`; and the synthesis contains near-term indicators for all four scenarios.

The notes are limitations rather than remaining defects. Community evidence is a small, self-selected qualitative sample; scenario probabilities are analytical estimates; absence of a universal standard is a bounded search result rather than proof of global nonexistence; and no controlled prototype evaluation yet establishes that receipts reduce total work. These limitations are disclosed prominently and do not require further dossier edits.

## File-by-file findings

### `00-extracted.md` — PASS

- Front matter at lines 1–6 includes the required `Under exploration.` excerpt and exact `2026-08-02` date.
- The source follows Question → Exploration → Prototype → Conclusion at lines 10, 18, 38, and 67.
- It frames the receipt as a question and experiment, not an established answer. Zero sources is appropriate for the supplied source artifact.

### `01-interpretation.md` — PASS

- The thesis, seven source claims, named entities, numbers, assumptions, missing evidence, and confidence assessment are present at lines 1–74.
- Twelve mandatory research questions and 10 research seeds appear at lines 76–113.
- The plan at lines 115–177 assigns every required and optional section. Conspiracy is explicitly `Skip` at lines 168–177. Zero sources is appropriate for a planning artifact.

### `02-history.md` — PASS

- Required sections are complete: long arc at lines 3–15, direct precedents at 17–47, five failed attempts at 49–69, recurring cast at 71–80, what is new at 82–96, expected next developments at 98–108, and categorized receipts at 110–158.
- The file has 41 distinct linked sources. It uses primary standards and incident records for load-bearing history and keeps community material out of historical proof.
- The former approximate era at line 5 is now non-temporal prose; all actual event dates use `YYYY-MM-DD`.
- It explicitly states that the direct SCITT agent profile is individual and unadopted at lines 15 and 35 and that authenticated registration does not prove truth at lines 67–69.

### `03-mechanism.md` — PASS

- The distinctions among log, trace, provenance record, attestation, domain result, explanation, and receipt are explicit at lines 3–7.
- The 10-step walkthrough at lines 9–101 identifies producers, data movement, failure boundaries, and reviewer actions. Inputs, internals, failure modes, constraints, side effects, and analogy are present at lines 103–257.
- The file has 56 distinct linked sources, the largest angle-level set. Standards, technical documentation, filings, incident reports, and practitioner sources are separated.
- It does not treat a signature as truth, a trace as domain state, or replay as guaranteed reproducibility. No padding or unresolved factual contradiction was found.

### `04-stakeholders.md` — PASS

- Required coverage is complete: cast at lines 13–36, geography at 38–51, optional numbers at 53–64, money at 65–82, power at 84–95, impact at 97–112, under-recognized winners and losers at 114–129, silence at 131–139, receipts at 141–173, and document inventory at 175–201.
- The file has 29 distinct linked sources. Law, regulators, standards, vendors, and communities are explicitly categorized.
- Legal claims remain conditional on role, classification, data, sector, and jurisdiction. The amendment is now tied to publication on `2026-07-24` at lines 20 and 44 rather than described by year alone.
- Vendor pricing is presented as non-comparable reference data, not proof of net value. Unknown organization-specific facts remain labelled Unknown/Undisclosed.

### `05-contrarian.md` — PASS

- Six serious competing explanations with falsifiers appear at lines 15–28. Interests, omitted evidence, dissenting community material, quantitative reframes, negative search results, and evidence that would change the story appear at lines 30–148.
- The file has 21 distinct linked sources and does not build straw men. It preserves control-plane, retrieval, custody, organizational, portability, and verification explanations that could displace the receipt boundary.
- All SCITT architecture links at lines 9, 23, 60, 127, 146, and 155 now use draft `-22`, matching History and the synthesis.
- Temporal references formerly expressed only by year now use exact dates at lines 10, 24, 42, 66, 107, 157, and 169–171. `USENIX Security 2023` at lines 23 and 168 is the conference's proper title, not an event date.
- Community quotations at lines 77–99 carry exact dates, handles, direct URLs, and disclosed stakes.

### `06-future.md` — PASS

- The file has 31 distinct linked sources and all required sections: forecasting frame at lines 3–15, 12-entry forward calendar at 17–34, six second-order effect domains at 36–94, four scenarios at 96–170, exact 90-day signal at 172–178, under-priced effect at 180–198, 16-item watch list at 200–217, disagreements at 219–225, and receipts at 244–269.
- MCP chronology is correct throughout: RC on `2026-05-29`, stable revision on `2026-07-28` at lines 7, 124, 142, 203, 233, and 255. No stale “still pre-release” claim remains.
- The stable revision is correctly treated as stronger transport, extension, and conformance infrastructure—not a complete post-task receipt. Lines 13 and 106 explain why finalization does not materially change the scenario probabilities.
- Probabilities remain 45%, 20%, 30%, and 5%, sum to 100%, include bands and falsifiable triggers, and each scenario has 6–12-month indicators.
- OpenTelemetry and Gartner temporal shorthand was normalized to exact publication/opening dates plus explicitly non-date forecast-window wording. No day was invented for a broad forecast horizon.

### `07-community.md` — PASS_WITH_NOTES

- The file has 16 distinct linked sources across Hacker News, Reddit, GitHub, X, and LinkedIn. Required sections cover platform location, full sentiment range, practitioner takes, confusions, silence, receipts, and snowballing at lines 5–116; the optional before/after section is responsibly `n/a` at lines 67–69.
- The Hacker News sequence is now correct at lines 9 and 27: opening discussion on `2024-02-14`, `lmeyerov` follow-up on `2024-02-17`.
- `ZestyData` is explicitly tied to `2024-05-19` at lines 10, 23, and 53. Every direct community quotation includes a handle or name, exact date, and direct URL.
- The LinkedIn dissent at line 13 is an undated paraphrase, not a quotation, and is explicitly excluded from timeline evidence. That is the correct treatment when the page exposes only a relative date.
- The note is inherent: this is not a representative sample of “average engineers.” Lines 3, 19, 73–79, and 116 state the sampling and missing-voice limits clearly.

### `08-conspiracy.md` — PASS

- Every planned conspiracy heading appears at lines 1–45 and is explicitly skipped with the matching reason from `01-interpretation.md:168–177`.
- No conspiracy claims or sources are manufactured. Zero sources is appropriate for a planned `Skip` angle.

### `research.md` — PASS_WITH_NOTES

- The synthesis is complete and self-contained: story and cast at lines 7–26, timeline at 28–48, jurisdiction and numbers at 50–81, mechanism at 83–120, money/power/stakeholders at 122–160, counter-narratives at 162–173, community at 175–217, calendar at 219–237, scenarios at 239–305, exact signal at 307–311, tensions at 313–330, and categorized receipts at 332–385.
- It has 94 distinct linked sources and preserves source interests, legal scope, community sampling limits, unknown averages, counterarguments, and the difference between authenticity, completeness, truth, availability, and usefulness.
- MCP chronology is correct at lines 19, 47–48, 237, 247, 263, and 279. The stable revision is not overclaimed as a receipt standard.
- Community attribution is corrected at lines 181–205. The undated LinkedIn counterpoint at line 197 is paraphrased and excluded from timeline use.
- All four scenario blocks contain probability, band, rationale, trigger, and restored near-term indicators at lines 243–305. The point estimates sum to 100%.
- The note is epistemic: the proposed evidence-manifest design and scenario weights remain synthesis and hypotheses until the blind-review, hostile, restore, and exit tests at lines 315–330 are actually run.

## Cross-file consistency

The final corpus is internally consistent on its load-bearing claims:

- **Artifact boundary:** `00-extracted.md:18–65`, `03-mechanism.md:3–7,123–205`, and `research.md:83–108` converge on a compact projection over a trace and authoritative evidence, not a transcript or second source of truth.
- **Assurance properties:** `02-history.md:67–69`, `03-mechanism.md:154–168`, `05-contrarian.md:7–13`, and `research.md:9,83–120` consistently separate authenticity, integrity, completeness, truth, availability, intelligibility, and lawful retention.
- **MCP:** `06-future.md:7,203,233,255` and `research.md:19,47–48,237` agree on RC publication on `2026-05-29`, stable publication on `2026-07-28`, and the remaining accountability gap.
- **SCITT:** History, Contrarian, and the synthesis consistently use architecture draft `-22`. The separate agent-execution profile remains version `-00`, correctly identified as an individual, unadopted proposal rather than the architecture draft.
- **Community:** `07-community.md:9,27` and `research.md:182` agree on the `lmeyerov` follow-up date. All quoted social voices are attributable; the undated LinkedIn response is consistently paraphrased.
- **Regulation:** `04-stakeholders.md:38–51`, `06-future.md:17–34`, and `research.md:50–65,219–237` agree on current EU dates and condition applicability on system role and classification.
- **Futures:** `06-future.md:96–170` and `research.md:239–305` use the same four probabilities, bands, triggers, and near-term indicator families. The 90-day signal is identical in substance.
- **Skip handling:** `08-conspiracy.md` follows the plan rather than manufacturing a hidden-hand narrative.

No stale pre-release wording, cross-file date contradiction, unexplained SCITT version drift, probability arithmetic error, or dropped load-bearing scenario indicator remains. No padding or invented participant material was found.

## Source quality audit

Exact Markdown-URL normalization yields **159 distinct linked sources** across the 10 audited files. This is one fewer than the first validation because the obsolete SCITT draft `-01` URL was removed; draft `-22` was already present elsewhere. Counts below treat each exact URL once. They do not imply 159 independent owners, since an institution may supply multiple documents or versions.

| Category | Distinct sources | Typical contents |
| --- | ---: | --- |
| Primary | 105 | Laws, regulations, standards, RFCs, official specifications, repositories, regulator reports, filings, and first-party protocol documentation |
| News | 10 | Official institutional announcements and dated project or regulator news releases |
| Expert | 17 | Peer-reviewed research, conference papers, analyst work, specialist essays, and incident analyses |
| Community | 18 | Hacker News, Reddit, X, LinkedIn, and GitHub discussions used as practitioner evidence |
| Background | 9 | Vendor product documentation, pricing pages, architecture patterns, and contextual references |
| **Total** | **159** | Exact distinct URLs; fewer independent source owners |

Per-file exact counts:

| File | Distinct linked sources | Result |
| --- | ---: | --- |
| `00-extracted.md` | 0 | Exempt: source artifact |
| `01-interpretation.md` | 0 | Exempt: interpretation and plan |
| `02-history.md` | 41 | Pass |
| `03-mechanism.md` | 56 | Pass |
| `04-stakeholders.md` | 29 | Pass |
| `05-contrarian.md` | 21 | Pass |
| `06-future.md` | 31 | Pass |
| `07-community.md` | 16 | Pass |
| `08-conspiracy.md` | 0 | Exempt: planned `Skip` file |
| `research.md` | 94 | Pass |

Every substantive research-angle file exceeds the 12-source minimum. Source diversity is strongest in Mechanism and History. Multiple EUR-Lex, CISA/CSRB, NIST, OpenTelemetry, MCP, OpenAI, SCITT, and supply-chain pages share owners or ecosystems, so exact-URL volume should not be mistaken for independent corroboration. The synthesis appropriately labels official self-description, vendor pricing, analyst forecasts, and community posts according to their limitations.

## Sourcing audit

| Load-bearing claim | Ownership and stake | Independence | Confidence | Corroboration and final finding |
| --- | --- | --- | --- | --- |
| A useful receipt is distinct from a trace, provenance record, attestation, domain result, and explanation (`03-mechanism.md:3–7,123–205`; `research.md:83–108`). | W3C, IETF, OpenTelemetry, in-toto/SLSA, domain-system maintainers, and authorial synthesis. Standards projects have adoption stakes but different governance. | Medium-high | High for distinctions; medium-high for the proposed composition | Independently governed specifications support the component boundaries. The evidence-manifest assembly is correctly labelled a design hypothesis. |
| Exercised authority must preserve principal, actor, audience, delegation, and policy context (`03-mechanism.md:20–28,103–119`; `research.md:98–101`). | IETF RFC authors, MCP maintainers, NIST, and identity/policy systems. Each promotes secure protocol use. | High across owners | High | RFC 8693, MCP authorization, and NIST identity work independently support delegation and confused-deputy concerns. |
| Committed effects belong to authoritative domain systems rather than agent narration (`03-mechanism.md:38–63`; `research.md:100–104`). | Kubernetes, Stripe, AWS, Microsoft, and other system owners document their own records. Each has ecosystem or product stake. | Medium | High as an architectural principle | Unrelated domains consistently distinguish attempted calls from committed state. The synthesis avoids treating any one vendor as universal proof. |
| A signed or registered statement can still be false (`02-history.md:67–69`; `05-contrarian.md:9,23,60`; `research.md:9,16,93`). | IETF SCITT, Sigstore, in-toto/SLSA, and security researchers. Transparency systems benefit from precise trust boundaries. | High | High | SCITT draft `-22` explicitly supplies the limitation, corroborated by secure-log and supply-chain threat models. Version consistency now passes. |
| EU high-risk logging duties and GDPR minimisation pull evidence design in different directions (`04-stakeholders.md:7–11,38–51`; `research.md:50–65`). | EU legislature and Commission are authoritative for enacted law and interested in their own implementation framing. | High for enacted text | High for dates and rules; conditional for applicability | The AI Act, amendment, and GDPR corroborate the tension. All files avoid claiming a generic receipt is a legal safe harbor. |
| Missing, gated, voluminous, or late-protected logs can defeat accountability (`02-history.md:49–69`; `03-mechanism.md:207–242`; `research.md:110–120`). | CISA/CSRB, Congress, NIST, incident subjects, inquiry records, and USENIX researchers have different institutional stakes. | Medium-high | High for cited incidents; medium for transfer to agents | Multiple incidents and mechanisms support the failure classes. The dossier does not invent an agent-specific rate. |
| Receipt infrastructure has continuing ownership, retention, and exit costs (`04-stakeholders.md:53–82`; `05-contrarian.md:30–69`; `research.md:122–158`). | LangSmith, Langfuse, Phoenix, vendors, operators, and regulators. Vendors have direct commercial stakes. | Low-medium for vendor comparisons | High for advertised terms; unknown for net value | First-party pricing and retention establish cost mechanisms, not superiority. Unknown averages and missing total-cost data are explicit. |
| Practitioners want intermediate state and navigable timelines but disagree about buying, building, and trusting traces (`07-community.md:17–49`; `research.md:175–217`). | Self-selected engineers, maintainers, founders, and promoters. Some disclose seller or contributor stakes. | Low individually; medium across platforms | Medium for existence of themes; low for prevalence | HN, Reddit, GitHub, X, and LinkedIn provide varied qualitative corroboration. Attribution passes; representativeness remains explicitly limited. |
| No adopted universal post-task agent-receipt standard was found (`03-mechanism.md:224–242`; `05-contrarian.md:123–132`; `research.md:9,19`). | Several independent standards projects and one individual SCITT profile author each cover a slice and may seek broader adoption. | Medium-high across projects | Medium-high, not absolute | Broad official-source search found adjacent components and one unadopted direct proposal. The corpus correctly presents this as a bounded absence finding. |
| MCP's `2026-07-28` revision is stable but incomplete as an accountability artifact (`06-future.md:7,203,233,255`; `research.md:19,47–48,237`). | Official MCP release repository and project explanation. The project has an adoption stake but direct authority over release status. | High for status | High | Official release history establishes RC `2026-05-29` and stable `2026-07-28`. The remaining semantic gap is corroborated by comparison with domain, authorization, and attestation specifications. |
| Four future market shapes and their probabilities are useful hypotheses, not measured forecasts (`06-future.md:96–170`; `research.md:239–305`). | Authorial synthesis over standards, law, community evidence, and Gartner. Gartner has a commercial forecasting stake. | Mixed | Low-medium for weights; high that they are testable hypotheses | Bands, triggers, near-term indicators, and the exact 90-day signal make updating possible. The text does not present probabilities as empirical frequencies. |
| Evidence decay can dominate the long-term cost of a tiny manifest (`06-future.md:180–198`; `research.md:321–324`). | SLSA, Sigstore, privacy and liability law, plus authorial systems reasoning. No single owner measures the combined effect. | Medium-high for components | Medium for combined magnitude | Key, resolver, retention, deletion, schema, and verifier lifecycles corroborate the mechanism; no longitudinal cost study exists, and the text says so. |

The weakest evidence remains the scenario weights, commercial analyst forecasts, population-level implications from community discussion, exhaustive nonexistence of a standard, and any implied net cost advantage. Each is labelled with appropriate limitations. No load-bearing claim now depends on an unattributed quotation, an outdated release status, or an unexplained obsolete draft.

## Improvement tasks

None.
