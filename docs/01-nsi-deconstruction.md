# NSI SAR Deconstruction

Sources: ISE-SAR Functional Standard v1.5.5 (FS), NSI Indicators documents (rev. 4/24), Assessment and Review of the NSI Indicators (Dec 2024), NSI CONOPS (2008), NSI Privacy Fact Sheet, 28 CFR Part 23.

"Data and AI implications" columns are my analysis, not statements from the sources. "Typical text cues" are inferred from the definitions.

## 1. Key takeaways
- A SAR is documented observed behavior reasonably indicative of pre-operational planning associated with terrorism or other criminal activity (FS 5.s, 5.t).
- An ISE-SAR is a SAR that passed a two-part review and has a potential nexus to terrorism (FS 5.h).
- For ISE-SAR purposes, "other criminal activity" must fall within the 16 Part B behaviors (FS footnote 1).
- "Reasonably indicative" (FS) and "reasonable suspicion" (28 CFR 23.20(c)) are different standards; do not conflate them in the PRD.
- FS Part C step 4 says an ISE-SAR may or may not meet reasonable suspicion; if it does, it may also go to a criminal intelligence database under 28 CFR Part 23.
- 28 CFR Part 23 applies to criminal intelligence systems supported under the Omnibus Crime Control Act (23.3); applicability to a prototype is an assumption to confirm with the supervisor.
- The Assessment and Review validates the 16 indicators and finds no need to add new ones, but suggests re-scoping some definitions.
- FS 1.5.5 was last reviewed about 10 years before Dec 2024, and updates are under discussion.

## 2. The 16 behavioral categories (FS Part B)

### Group A: Defined criminal activity and potential terrorism nexus activity (7)

| # | Indicator | Definition (condensed) | Typical text cues (inferred) | Data and AI implications (analysis) |
|---|-----------|------------------------|------------------------------|-------------------------------------|
| 1 | Breach/Attempted Intrusion | Unauthorized entry or attempt into a restricted, secured, or nonpublic area; impersonating authorized personnel | trespass, fence, perimeter, gate, alarm, posing as staff | Needs facility and location entities; overlaps with Misrepresentation and Testing/Probing, so use multi-label |
| 2 | Misrepresentation | False information or misused insignia, documents, or ID to misrepresent affiliation and conceal possible illegal activity | fake ID, stolen uniform, forged license | Often co-occurs with Breach; extract document and ID entity types |
| 3 | Theft/Loss/Diversion | Stealing or diverting items tied to a facility (badges, uniforms, ID, vehicles, technology, documents) | burglary, stolen badge, missing credential | Ordinary theft is common, so false-positive risk is high; weight facility-context entities |
| 4 | Sabotage/Tampering/Vandalism | Damaging, manipulating, defacing, or destroying part of a facility or protected site | tampered, chained, damaged, removed plugs | Confusable with routine vandalism; infrastructure entity weighting helps |
| 5 | Cyberattack | Compromising, attempting to compromise, or disrupting an organization's IT infrastructure | intrusion, DDoS, network, hack | Technical vocabulary; text may include IPs and domains; consider separate entity types |
| 6 | Expressed or Implied Threat | Spoken or written threat of a crime causing death or injury, or damage to a facility | threat, "wait until", letter, call | Most prevalent and best supported, but also closest to protected speech; require human review |
| 7 | Aviation Activity | Learning to operate, operating, or interfering with an aircraft in a way that threatens harm; may or may not violate FAA rules | aircraft, pilot, helicopter, hovering | Rare class; synthetic data must be built carefully, and evaluation needs enough positives |

### Group B: Potential criminal or non-criminal activity requiring additional information during vetting (9)

The FS says these may be constitutionally protected, so articulable additional facts are required before documenting them in an ISE-SAR containing PII.

| # | Indicator | Definition (condensed) | Typical text cues (inferred) | Data and AI implications (analysis) |
|---|-----------|------------------------|------------------------------|-------------------------------------|
| 8 | Eliciting Information | Questioning beyond mere curiosity about a facility's purpose, operations, or security | asked about security, staffing, fuel | "Beyond curiosity" is subjective; high false-positive risk; surface the exact phrases behind a flag |
| 9 | Testing or Probing of Security | Deliberate interactions or challenges that reveal security capabilities | tested response, set off alarm, fled when approached | Overlaps with Breach; context and sequence of events matter |
| 10 | Recruiting/Financing | Direct financial support to operations teams, building teams, or compiling personnel, banking, or travel data | funding, recruit, travel records | PII-heavy; associational activity raises 28 CFR 23.20(b) concerns; strict privacy handling |
| 11 | Photography | Pictures or video of persons, facilities, or infrastructure in an unusual or surreptitious manner | photographed, hiding, fled | Photography alone is lawful; the model must key on concealment and evasion cues, not the activity word |
| 12 | Observation/Surveillance | Unusual or prolonged interest beyond casual or professional interest (binoculars, notes, measuring) | watching, notes, measured distances | Needs a casual-vs-professional distinction; tourists and engineers are common false positives |
| 13 | Materials Acquisition/Storage | Unusual quantities of materials such as phones, pagers, fuel, chemicals, or timers | purchased pounds of, storage unit | Needs quantity extraction and material entities; "unusual" depends on buyer and context |
| 14 | Acquisition of Expertise | Attempts to obtain training or knowledge in security concepts, military weapons or tactics, or other unusual capabilities | training, course, endorsement, asked how to | Lawful training is common; protected-activity risk; rely on articulated facts, not topic keywords |
| 15 | Weapons Collection/Discovery | Unusual amounts or types of weapons, explosives, chemicals, or residue evidence | rifles, devices, magazines, residue | Lawful ownership is common, so "unusual" must come from context; avoid keyword-only scoring |
| 16 | Sector-Specific Incident | Actions tied to characteristics of concern to specific sectors (e.g., public health) | sector terms, chemical tank, pump failure | Catch-all that depends on a sector ontology; consider a sector feature |

### Prevalence in terrorist plots (START, PIRUS-Plots, 1990 to 2021)
- Indicators were present in 80% of plots, averaging 2.2 per incident, which supports multi-label classification.
- Most frequent: Expressed/Implied Threat 47.8%, Recruiting/Financing 34.2%, Observation/Surveillance 31.5%, Weapons Collection/Discovery 31.1%, Acquisition of Expertise 20.5%.
- Implication: expect strong class imbalance; use per-class precision and recall, not accuracy.
- Lone-actor attacks rose to 72.7% in 2011 to 2021, and Recruiting/Financing, Materials, and Weapons indicators declined; keep scoring weights adjustable.
- Source: Assessment and Review, executive summary (p. 4 to 5); the full tables are in the START section.

## 3. Lifecycle and human decision points

| Stage | FS Part C step / CONOPS section | Actor | Human decision | HITL design implication (analysis) |
|-------|---------------------------------|-------|----------------|-------------------------------------|
| Observation / submission | FS 1 / CONOPS 4.2.1 | Citizen, private sector, official, or officer | Observer judges the behavior suspicious | Intake form should capture behavior and context, not personal characteristics |
| Initial response and documentation | FS 2 / CONOPS 4.2.1 | Responding official | Dismiss as innocent or escalate; direct JTTF referral if a clear terrorism connection | System input is the documented report; this stage is outside the prototype |
| Local review | FS 3 / CONOPS 4.2.2 | Source-agency supervisor | Is it appropriate to consider as a SAR; forward to fusion center or JTTF | Prototype queue starts after this point |
| Analyst vetting (part 1) | FS 4 / CONOPS 4.3.1 | Trained analyst | Does the report reflect a Part B behavior; check linkages | System may suggest categories and entities; analyst confirms or edits |
| ISE-SAR determination (part 2) | FS 4 / CONOPS 4.3.2 | Trained analyst, optional secondary review | Professional judgment on potential nexus; if no explicit determination, not shared to the SDR | Human-only decision; show rationale, never auto-decide |
| Sharing | FS 5 / CONOPS 4.4 | Submitting agency | Upload to the NSI SDR; FBI assessment follows | Out of scope; the prototype must not disseminate |
| Reevaluation / feedback | FS D.5 / CONOPS 4.6 | Submitting and source agencies, FBI | Notify participants if an ISE-SAR was designated incorrectly | Log analyst corrections as feedback for evaluation |

Notes:
- The FS maps the cycle to 9 steps; the CONOPS describes 12 steps in 5 phases. Cite which one you use.
- The Privacy Fact Sheet describes the two vetting forms as source-agency supervisor review, then trained analyst review against the 16 behaviors.

## 4. Standards and legal framework

### 4.1 "Reasonably indicative" (FS)
- Takes into account the circumstances and the training and experience of a reasonable law enforcement officer (FS 5.p).
- Requires an articulable concern that the behavior may indicate pre-operational planning.
- Analysts should not assume why a person acted; the determination rests on observed behavior or documented circumstances (FS footnote 15).

### 4.2 "Reasonable suspicion" (28 CFR 23.20(c))
- Established when facts give a trained officer a basis to believe there is a reasonable possibility that an individual or organization is involved in a definable criminal activity or enterprise.
- Collect and maintain intelligence on an individual only if reasonable suspicion exists and the information is relevant (23.20(a)).

### 4.3 Retention and review (23.20(h))
- Procedures must ensure retained information has relevancy and importance.
- Periodic review; destroy information that is misleading, obsolete, or unreliable; advise recipients of corrections.
- Retained records must show reviewer name, review date, and explanation of the decision to retain.
- Validate before the retention period expires; the period may never exceed five years.
- FS side: ISE-SARs follow local or Federal retention policies; the FS data model includes ReportPurgeDate and ReportPurgeReviewDate fields for privacy fields.
- CONOPS: time-dependent purging of ISE-SARs after human review.

### 4.4 Dissemination, security, and audit (23.20(e) to (g), (m))
- Share only with a need to know and right to know, and generally only with law enforcement authorities.
- Keep a record of who received information, why, and when.
- Label information by sensitivity level, confidence level, and submitting agency.
- Use administrative, technical, and physical safeguards, including audit trails.
- Adopt sanctions for unauthorized access, use, or disclosure.

### 4.5 Protected activity and bias exclusions
- Race, ethnicity, gender, national origin, religion, sexual orientation, and gender identity must not be factors creating suspicion (FS Part A and Part B).
- Those attributes may appear in specific suspect descriptions for identification purposes.
- The nine Group B behaviors may be constitutionally protected and must not be documented in an ISE-SAR with PII without articulable facts showing the behavior is not innocent.
- SAR reporting rests on observable, clearly defined behaviors, not race, culture, religion, or political associations (CONOPS 4.1.4).
- Do not collect or maintain information on political, religious, or social views or associations unless directly related to criminal conduct with reasonable suspicion (23.20(b)).
- No harassment or interference with lawful political activities (23.20(l)).
- The Privacy Fact Sheet says the FS reinforces First Amendment protections and limits the use of race, ethnicity, national origin, or religion.

## 5. Design implications for the capstone
- Treat model output as decision support for analyst vetting and determination, with the human always making the ISE-SAR call.
- Keep demographic and protected-attribute terms out of scoring features; test for leakage as part of the bias audit.
- Separate privacy fields from the rest of the record in the schema, mirroring the FS detailed vs summary distinction.
- Store confidence level, reviewer, review date, and rationale with every flag to mirror 23.20(g) and (h).
- Add retention and purge-review fields and an audit log of access and dissemination events.
- Use multi-label categories with per-class evaluation, given co-occurring indicators and class imbalance.
- Require extra articulated-fact checks before surfacing Group B flags with PII.

## 6. Open questions for the supervisor
- Does the intended system fall under 28 CFR Part 23, or is it an ISE-SAR vetting aid only?
- Is the DPS workflow aligned with FS 1.5.5, and are there local category codes beyond the 16?
- What retention period and review cadence does DPS apply to unvetted SARs?
- Which errors cost more: missed signals or false positives?
- Are there analyst-facing fields or labels you would want in the triage view?
