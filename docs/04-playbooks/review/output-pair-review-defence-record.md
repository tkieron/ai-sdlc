# Review Output – Pair Review & Defence Record

Canonical logical output for a risk-driven pair review / engineering defence session.

> **Purpose:** preserve evidence that the Human Owner can explain, justify and defend the material implementation and that the reviewer independently challenged the solution before final approval.

This artifact MAY be represented by a lightweight PR note, meeting record or another organization-approved mechanism. It SHOULD be used where required by the assigned risk class or where reviewer confidence depends on deeper explanation.

## Required metadata

* **Change / PR:**
* **Risk class:** R0 / R1 / R2 / R3 / R4
* **Author / Human Owner:**
* **Reviewer(s):**
* **Session timestamp:**
* **Reason pair review was required:** Risk policy / Reviewer request / Material AI-generated implementation / Other

## Author defence

The Human Owner SHOULD be able to explain, proportionally to risk:

* what changed and why,
* how the solution satisfies the approved intent,
* material implementation decisions,
* material AI-made local decisions or assumptions,
* alternatives or trade-offs considered,
* relevant architecture / contract implications,
* important failure modes,
* how correctness was validated,
* known limitations and residual risks.

## Reviewer challenge record

Record material questions or challenges only; this artifact is not intended to become a transcript.

| Topic / challenge | Author explanation | Reviewer assessment | Follow-up |
| --- | --- | --- | --- |
|  |  | Accepted / Concern / Blocking |  |

## Cognitive ownership assessment

The reviewer SHOULD assess:

* Author demonstrates sufficient mental model of the change: Yes / No / Unclear
* Author can explain material decisions without relying only on AI-generated explanation: Yes / No / Unclear
* Author understands key failure modes: Yes / No / Unclear
* Author understands validation evidence and its limits: Yes / No / Unclear
* Material AI assumptions are understood and accepted: Yes / No / N/A

If the answer to a material item is **No** for a risk class requiring cognitive ownership, the change SHOULD return for further author review rather than being approved solely because CI and AI review are green.

## Findings / decisions

* **Blocking findings discovered:**
* **Material decisions requiring upstream authority:**
* **Accepted deviations:**
* **Required rework:**
* **Residual risk:**

## Outcome

Choose one:

* **DEFENCE PASSED** — reviewer has sufficient confidence in both the implementation and the Human Owner's understanding.
* **REWORK REQUIRED** — implementation or understanding is insufficient for approval.
* **ESCALATE** — a Material Decision, specification conflict or risk issue requires upstream resolution.

### Session sign-off

* **Outcome:**
* **Reviewer:**
* **Author / Human Owner:**
* **Date / time:**
* **Next step:** Final reviewer re-check / Return to implementation / Escalate

## Governance rule

Pair Review / Defence is a control for engineering understanding and independent challenge. It MUST NOT become a ceremonial presentation or a substitute for direct code inspection by the reviewer.
