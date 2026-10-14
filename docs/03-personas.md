# Stakeholder Personas

Status: Draft v0.1, pending supervisor validation. Bracketed codes point to rows in `00-source-log.md`, for example [1] for the Functional Standard.
Names are fictional and the personas are composites based on public NSI documents. Fields tagged **(assumed)** are not sourced and are listed for validation.

## Persona map

| Persona | Role in the process | Primary interaction with the system | Main PRD hooks |
|---------|--------------------|--------------------------------------|----------------|
| Avery, Intake and Vetting Analyst | Reviews SARs and makes the first judgment | Daily triage queue | Entity highlights, category suggestions, similar reports |
| Morgan, Supervisory Intelligence Analyst | Secondary review, overrides, queue oversight | Review and approval view | Score breakdown, override log, queue priority |
| Riley, Privacy and Civil Liberties Officer | Audits compliance and bias | Audit and reporting view | Audit trail, retention fields, bias reports |
| Sam, Field Reporting Source (secondary) | Documents the original report | None directly | Input quality, narrative formats |

## 1. Avery, Intake and Vetting Analyst (primary user)

**Role and goals**
- A trained analyst who reviews each SAR against the 16 Part B behaviors, then judges whether there is a potential nexus to terrorism [1].
- Wants to reach a defensible, well-documented decision quickly.

**Workflow**
- Reads the narrative, then checks databases and other reports for linkages [1].
- Applies judgment on context, facts, and circumstances, without presuming why the person acted [1].
- Escalates the report, or declines it, which means it is not shared to the SDR but may be retained locally [1].

**Pain points (assumed)**
- Narratives vary in format and quality.
- Subjective category wording makes consistent calls hard.
- Finding related or duplicate reports takes manual searching.
- Writing up the rationale takes time.

**Needs from the system**
- Highlighted entities (places, dates, infrastructure, weapons, behavioral cues).
- Suggested categories with the cues that triggered them.
- Related reports, shown beside the current one.
- One-click confirm, edit, or reject, with the rationale logged automatically.

**Concerns**
- Over-trusting a score, or having a suggestion anchor the decision.
- Any flag that appears to rely on protected attributes [1].

**Success metric**
- Time from report arrival to decision, and share of decisions with a complete rationale.

**Draft user stories**
- As an analyst, I want entities highlighted so I can find the key facts quickly.
- As an analyst, I want suggested categories with cues so I can verify them against the text.
- As an analyst, I want related reports shown so I can spot linkages without a manual search.

## 2. Morgan, Supervisory Intelligence Analyst

**Role and goals**
- Handles secondary review and approval where the process requires it, before an ISE-SAR is submitted [1].
- Wants consistent, auditable determinations across the team.

**Workflow**
- Reviews escalated or contested items, then approves, changes, or returns them.
- Watches queue health and overrides.

**Pain points (assumed)**
- Reviewing a decision without seeing why it was made.
- Inconsistent calls between analysts.
- Little visibility into backlog and aging reports.

**Needs from the system**
- Queue sorted by priority and confidence.
- A score breakdown showing which factors drove a flag.
- An override log with reviewer, date, and reason.
- A side-by-side view of suggestion and analyst decision.

**Concerns**
- Accountability if analysts defer to the tool.
- Alert volume that hides real signals.

**Success metric**
- Review turnaround time, override rate, and agreement across analysts.

**Draft user stories**
- As a supervisor, I want to see why a flag was raised so I can review it faster.
- As a supervisor, I want to override a suggestion and record why.
- As a supervisor, I want to see aging reports so nothing stalls.

## 3. Riley, Privacy and Civil Liberties Officer

**Role and goals**
- Confirms that review is behavior-based and that protected attributes do not create suspicion [1].
- Confirms retention review, audit trails, and need-to-know rules are followed [8].

**Workflow**
- Samples decisions and logs, checks Group B flags for articulated facts, and reviews retention dates.

**Pain points (assumed)**
- Rebuilding why a decision was made after the fact.
- Checking for bias without test evidence.

**Needs from the system**
- Audit trail with reviewer, date, rationale, and confidence level [8].
- Bias test reports and perturbation results.
- Retention and purge review dates on records [1].
- Exportable logs.

**Concerns**
- Protected attributes influencing scores.
- Group B flags with PII but no articulated facts [1].

**Success metric**
- Audit coverage, bias gap, and zero flags missing a rationale.

**Draft user stories**
- As a privacy officer, I want a complete audit trail for each decision.
- As a privacy officer, I want bias test results I can review before approving use.
- As a privacy officer, I want retention review dates visible on each record.

## 4. Sam, Field Reporting Source (secondary, not a system user)

**Role and goals**
- A local officer, private sector partner, or other source who documents the original report in incident reports, interviews, or similar formats [1].
- Wants to document quickly and learn whether the report mattered; the process includes feedback to source organizations [5].

**Why it matters**
- The wording and structure of these narratives set the quality of the data the system receives.

**Needs (assumed)**
- Clear reporting fields and prompts; the prototype does not change this step.

**Concerns (assumed)**
- Extra reporting burden.

**Success metric**
- Not measured; used to shape synthetic narrative styles.

## Validation status

- All personas are assumptions based on public NSI documents until the supervisor confirms them.

