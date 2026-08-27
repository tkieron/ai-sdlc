# Review Output – Review Decision Record

Canonical logical output that closes the review stage and records whether the change may proceed, must return for rework, or requires escalation.

> **Purpose:** provide a concise, traceable review outcome without duplicating detailed AI, human or pair-review findings.

This record MAY be represented by the PR approval/change-request state when the selected tool already preserves the required evidence. A separate document is only needed when the tool does not provide sufficient traceability for the assigned risk class.

## Required metadata

* **Change / PR:**
* **Risk class:** R0 / R1 / R2 / R3 / R4
* **Author / Human Owner:**
* **Final reviewer / approver:**
* **Decision timestamp:**

## Evidence considered

Mark the evidence used for the final decision, as applicable:

* Source change / PR
* Automated CI / quality evidence
* Agent Completion Report
* AI Review Findings
* Human Review Record
* Pair Review & Defence Record
* Relevant architecture / decision records
* Accepted deviations / exception records

## Review disposition

Choose exactly one:

### PR APPROVED

Use when:

* required review controls for the risk class are complete,
* no blocking findings remain,
* material deviations are explicitly accepted,
* the author demonstrates sufficient ownership,
* the implementation is ready to proceed to merge / Verification & Acceptance.

### CHANGES REQUIRED

Use when material findings remain and the change must return to the author / Implementation stage.

### ESCALATED

Use when review identifies a Material Decision, specification conflict, risk increase, authority gap or other issue that cannot be resolved inside Review.

## Decision summary

* **Disposition:** PR APPROVED / CHANGES REQUIRED / ESCALATED
* **Blocking findings remaining:**
* **Material accepted deviations:**
* **Residual risks / uncertainty:**
* **Required downstream attention:**
* **Return / escalation target if not approved:**

## Approval statement

When the outcome is **PR APPROVED**, the authorized human reviewer confirms that, proportionally to the assigned risk class:

* the implementation has been reviewed against approved intent,
* required independent controls were performed,
* blocking review findings are resolved,
* material assumptions/deviations are visible,
* sufficient human understanding and accountability are present.
* **Approver:**
* **Date / time:**

## Governance rule

The Review Decision Record is evidence of a human decision. AI MAY prepare or summarize the record but MUST NOT grant itself PR approval or act as the accountable approver.
