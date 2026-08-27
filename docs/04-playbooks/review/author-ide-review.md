# Review Playbook – Author IDE Review Checklist

> **Purpose:** provide the Human Owner with a short, repeatable pre-PR review routine before independent review starts.

The author MUST inspect the resulting implementation directly in the engineering environment. AI summaries, generated explanations and green tests are supporting evidence, not substitutes for author understanding.

## 1. Before opening the PR

Confirm:

* I know the assigned **RISK_CLASS**.
* I can state the objective of the change in one or two sentences.
* I know the approved scope and explicit non-scope.
* I know the important contracts, invariants and expected outcomes.
* I know what validation is expected before external review.

If I cannot explain the intended change before reading the implementation, I SHOULD return to the design/contract context first.

## 2. Review the diff in the IDE

Review the full change, not only the files highlighted by the agent.

### Scope

* Is every changed file necessary?
* Did AI touch files/components outside the authorized area?
* Are there unrelated refactors, dependency upgrades or generated changes?
* Did the implementation stop when the delegated objective was complete?

### Correctness

* Does the code implement the expected behavior?
* Are critical negative and edge cases handled?
* Are domain rules and invariants preserved?
* Did any expected outcome/test oracle change during implementation?

### Design / Architecture

* Does the code follow the design I intended?
* Are module/service boundaries preserved?
* Did the implementation create a new material architecture decision?
* Are public contracts changed intentionally?

### Failure / Data / Concurrency

Where applicable:

* What happens on partial failure?
* Are transaction boundaries correct?
* Can duplicate/retried execution damage state?
* Are race conditions, lost updates or locking issues possible?
* Is data migration or persistence behavior safe?

### Security

* Are authentication/authorization assumptions correct?
* Is sensitive data exposed in logs, responses or persistence?
* Did the change broaden access or permissions?

### Tests

* Do tests verify the approved behavior?
* Are assertions meaningful?
* Are important negative/failure cases present?
* Did AI weaken or rewrite tests to make them pass?
* Are required local checks green?

### Operability

* Can this behavior be diagnosed in production?
* Are important failures observable?
* Is logging useful and safe?

### Maintainability

* Can I explain the code without relying on the AI explanation?
* Are names and abstractions clear?
* Is complexity justified?
* Is there surprising side effect or hidden coupling?

## 3. Agent Completion Report Check

For material AI-assisted work verify:

* the reported changed scope matches the actual diff,
* stated validations were actually executed where evidence is available,
* autonomous local decisions are acceptable,
* deviations are visible,
* unresolved risks are not hidden,
* deliberately unimplemented work is understood.

## 4. Author Knowledge Check

Before requesting review, I SHOULD be able to explain:

* what changed,
* why this solution was chosen,
* important alternatives/trade-offs,
* critical failure modes,
* how correctness was validated,
* material AI-made local decisions,
* known limitations and residual risk.

For R2–R4, inability to explain a material part of the change is a signal that the PR is not ready for independent review.

## 5. Author Outcome

Choose one:

* **READY FOR REVIEW** — I understand and accept the implementation and required local evidence is available.
* **REWORK** — implementation or my understanding is insufficient.
* **ESCALATE** — implementation revealed a Material Decision, contract mismatch or risk increase.

> **Author principle:** Do not outsource understanding. The PR should reach the reviewer only after the Human Owner can defend what it does and why.
