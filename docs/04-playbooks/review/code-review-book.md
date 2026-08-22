# Review Playbook – Code Review Book & Checklist

> **Purpose:** provide a repeatable, risk-aware review sequence that reduces reviewer omission, preserves independent engineering judgement and prevents AI-assisted review from degrading into superficial diff scanning.

This checklist is a **review book**, not a substitute for judgement. Reviewers SHOULD execute it in a stable order, like a cockpit checklist, while spending depth proportionally to the assigned risk class.

## 1. Review Preconditions

Before reviewing, confirm:

* the change / PR is identifiable,
* the assigned **RISK_CLASS** is known,
* the approved functional intent is accessible,
* relevant architecture / ADRs are accessible,
* Test Intent / correctness contract is accessible where applicable,
* Agent Completion Report is available for material AI-assisted implementation,
* CI/local validation evidence is available or clearly marked incomplete.

If the risk class is missing or material intent is unavailable, the reviewer SHOULD stop and request the missing context rather than infer a lower-risk interpretation.

## 2. Recommended Review Order

### PASS 1 — Scope & Contract

Check first whether the change is the change that was authorized.

* Does the implementation stay inside the approved scope?
* Are there unrelated refactors, dependency upgrades or opportunistic changes?
* Does the diff match the Implementation Contract / intended work item?
* Were accepted requirements, test oracles or Definition of Done changed?
* Are material deviations explicit and approved?
* Did the agent or author introduce hidden scope expansion?

**Stop condition:** material scope or correctness-contract mismatch.

### PASS 2 — Domain & Functional Correctness

* Are domain rules and invariants preserved?
* Are happy, negative and boundary cases implemented correctly?
* Are validation rules applied at the correct boundary?
* Are error paths explicit rather than accidental?
* Does the implementation solve the approved problem rather than a plausible adjacent problem?
* Are permissions and actor-specific behaviors correct?

### PASS 3 — Architecture & Boundaries

* Are component/service/module responsibilities preserved?
* Are public APIs, events and contracts changed intentionally?
* Does the change introduce new coupling or dependency direction violations?
* Is data ownership preserved?
* Are architecture decisions already approved, or has implementation created a new Material Decision?
* Is configuration/environment behavior consistent with architecture?

### PASS 4 — Data, Transactions & Concurrency

Where applicable:

* Are transaction boundaries correct and intentionally placed?
* Are partial-failure states understood?
* Is data consistency appropriate to the business requirement?
* Are retries/idempotency relevant and correct?
* Can duplicate execution corrupt state?
* Are optimistic/pessimistic locking assumptions valid?
* Are race conditions, lost updates, deadlocks or visibility issues possible?
* Are schema/data changes backward compatible where required?

### PASS 5 — Security, Privacy & Permissions

* Is authentication/authorization enforced at the correct boundary?
* Is input validated and output exposure appropriate?
* Are secrets or sensitive data logged, returned or persisted accidentally?
* Are permission checks missing, duplicated or bypassable?
* Does the change widen data access?
* Are external inputs treated as untrusted?
* Are dependency/security implications introduced?

For material security uncertainty: **STOP → DESCRIBE → PROPOSE → ESCALATE**.

### PASS 6 — Failure Handling & Resilience

* What happens when dependencies fail or time out?
* Are retries bounded and safe?
* Is fallback behavior intentional?
* Are partial results or intermediate states safe?
* Are timeouts/circuit breakers/backpressure relevant?
* Is failure observable?
* Is recovery possible without manual data repair where expected?

### PASS 7 — Tests & Correctness Evidence

* Do tests verify behavior rather than implementation trivia?
* Are critical scenarios covered?
* Are important negative/failure paths represented?
* Did the implementation modify tests to fit itself?
* Are assertions meaningful?
* Is there overuse of mocks hiding integration behavior?
* Are E2E tests selective and justified?
* Are material NFRs validated when required by risk?

**Rule:** green tests are evidence, not proof that the specification is correct.

### PASS 8 — Observability & Operability

* Can the new behavior be diagnosed in production?
* Are important failures logged with useful context and without sensitive data?
* Are metrics/traces/events required?
* Will operators distinguish expected rejection from system failure?
* Are rollout/recovery implications visible?

### PASS 9 — Maintainability & Readability

* Is the design understandable without AI-generated explanation?
* Are names, boundaries and abstractions coherent?
* Is complexity justified?
* Is duplication preferable to a premature abstraction, or vice versa?
* Are comments explaining _why_ rather than restating code?
* Does the change create hidden temporal coupling or surprising side effects?
* Could another engineer reasonably maintain it?

### PASS 10 — AI-Assisted Change Check

Where AI participated materially:

* Are autonomous assumptions visible?
* Are material local decisions listed in the Agent Completion Report?
* Did the agent operate within the assigned risk profile?
* Did it touch forbidden areas?
* Did it continue work after the delegated goal was complete?
* Does the Human Owner actually understand the resulting change?

## 3. Finding Severity

Use a simple shared scale:

* **Blocking** — must be resolved or explicitly escalated before approval.
* **Major** — material defect/risk/design concern; normally requires change.
* **Minor** — non-material quality issue worth correcting.
* **Observation** — non-blocking note, follow-up or potential improvement.

A finding SHOULD include concrete evidence and the violated requirement, invariant, contract or engineering rationale.

## 4. Risk Scaling

### R0

* lightweight checklist,
* focus on scope, correctness and automated evidence,
* independent review MAY be waived by policy.

### R1

* standard checklist,
* normal independent human review,
* investigate material findings only.

### R2

* complete relevant passes,
* independent review REQUIRED,
* explicit review of Agent Completion Report and material deviations,
* Pair Review / Defence SHOULD be considered for substantial AI-generated code.

### R3

* strong evidence across all relevant passes,
* lead/specialist involvement where applicable,
* Pair Review / Defence normally expected for material changes,
* security/data/concurrency/recovery concerns require explicit treatment.

### R4

* multi-party/specialist review,
* checklist evidence MUST be explicit,
* AI review is supplemental only,
* critical assumptions and irreversible effects require direct human verification.

## 5. Review Outcome

The reviewer ends with exactly one disposition:

* **APPROVE**
* **REQUEST CHANGES**
* **ESCALATE**

The detailed evidence SHOULD be captured using the canonical **Human Review Record** and, where required, **Pair Review & Defence Record** and **Review Decision Record**.

> **Operating principle:** Review the contract before reviewing the elegance of the code. A beautifully implemented wrong solution is still wrong.
