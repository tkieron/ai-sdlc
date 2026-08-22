# Review Output – Human Review Record

Canonical logical output of the independent human review required by AI-SDLC.

> **Purpose:** preserve evidence that a human reviewer formed an independent engineering judgement and evaluated the implementation against the approved intent, not only against superficial code quality.

This artifact MAY be represented by PR comments, an approved review checklist, Markdown or another organization-approved mechanism.

## Required metadata

* **Change / PR:**
* **Risk class:** R0 / R1 / R2 / R3 / R4
* **Reviewer:**
* **Author / Human Owner:**
* **Review timestamp:**
* **Review scope:**

## Independent-review declaration

The reviewer SHOULD confirm that they formed an initial view of the change before relying on detailed author or AI explanations where practical.

* Independent inspection performed: Yes / No / Not applicable
* Material context reviewed:
* Known limitations to reviewer independence:

## Review checklist

Record findings proportionally to risk. Not every line requires narrative evidence when there is no material concern.

| Review dimension | Result | Notes / evidence |
| --- | --- | --- |
| Scope & Implementation Contract compliance | Pass / Finding / N/A |  |
| Functional correctness / domain invariants | Pass / Finding / N/A |  |
| Architecture & boundaries | Pass / Finding / N/A |  |
| Error and failure handling | Pass / Finding / N/A |  |
| Transactionality / consistency | Pass / Finding / N/A |  |
| Security / permissions / privacy | Pass / Finding / N/A |  |
| Concurrency / synchronization | Pass / Finding / N/A |  |
| Persistence / data handling | Pass / Finding / N/A |  |
| Observability / operational behavior | Pass / Finding / N/A |  |
| Test adequacy / correctness contract | Pass / Finding / N/A |  |
| Maintainability / readability | Pass / Finding / N/A |  |
| Performance / resource implications | Pass / Finding / N/A |  |
| Unexpected dependencies / scope changes | Pass / Finding / N/A |  |
| AI assumptions / deviations surfaced | Pass / Finding / N/A |  |

## Findings

Each blocking or material finding SHOULD record:

* **ID:** HR-RV-###
* **Severity:** Blocking / Major / Minor / Observation
* **Evidence:**
* **Finding:**
* **Relevant requirement / architecture / invariant / standard:**
* **Requested action:**
* **Resolution status:** Open / Resolved / Accepted deviation / Escalated

## Human ownership check

The reviewer SHOULD explicitly assess whether the author demonstrates sufficient cognitive ownership for the assigned risk class.

* Author understands the intended behavior: Yes / No / Unclear
* Author can explain material implementation decisions: Yes / No / Unclear
* Material AI-made decisions are visible: Yes / No / N/A
* Additional Pair Review / Defence required: Yes / No

## Review outcome

Choose one:

* **APPROVE** — no blocking findings remain and the required review controls are satisfied.
* **REQUEST CHANGES** — blocking or material findings must be resolved before approval.
* **ESCALATE** — a Material Decision, risk increase, specification conflict or authority issue requires upstream resolution.

### Reviewer statement

* **Outcome:**
* **Blocking findings remaining:**
* **Accepted deviations:**
* **Residual risks / uncertainty:**
* **Reviewer:**
* **Date / time:**

## Governance rule

Human review evidence MUST NOT become ceremonial checklist completion. The reviewer remains responsible for engineering judgement appropriate to the risk class.
