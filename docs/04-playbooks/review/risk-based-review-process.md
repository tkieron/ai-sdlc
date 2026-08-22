# Review Playbook – Risk-Based Review Process

> **Purpose:** define the executable L4 review flow for R0–R4, including mandatory automated verification, AI review independence, author ownership, human review depth and Pair Review / Defence.

## Core flow

**Implementation Complete → Automated Pre-Flight → Independent AI Review → Author IDE Review → Human Pre-Flight → Independent Human Review → Pair Review / Defence where required → Review Decision**

The process is intentionally **fail-fast**.

> **Do not spend human review capacity on defects that Deterministic & Tool-Based Verification can detect automatically.**

A failed mandatory automated gate MUST return the change to Implementation before manual review continues, unless an explicit exception is authorized.

## Review stages

### Stage 1 — Automated Pre-Flight

Run all **Deterministic & Tool-Based Verification** applicable to the risk class and affected technology.

Typical checks include compile / build, required unit / component / integration tests, static analysis, lint / formatting where enforced, architecture rules, SAST / secret / dependency checks, API / schema / contract compatibility, migration validation and other project-specific policy checks.

Output: **PASS / FAIL / BLOCKED**.

If a mandatory check is **FAIL**, return to Implementation. If a mandatory check is **BLOCKED** because tooling or infrastructure is unavailable, the condition MUST be explicit and handled through the risk/exception policy rather than silently ignored.

### Stage 2 — Independent AI Review

AI review is performed only after the mandatory automated pre-flight has passed or an explicit exception exists.

The reviewer SHOULD start from a **fresh review context**, with the approved requirements/contracts and source diff, rather than from the implementation conversation.

AI Review Independence levels:

* **IR-1 — Context Independent:** fresh context; same model allowed.
* **IR-2 — Model Independent:** fresh context; different reviewer model.
* **IR-3 — Provider Independent:** fresh context; different vendor/provider or strongly independent review model.

AI review produces **AI Review Findings**. It MUST NOT constitute accountable approval.

### Stage 3 — Author IDE Review

The Human Owner reviews the actual diff directly in the engineering environment after automated checks have passed.

The author MUST verify, proportionally to risk:

* actual scope vs delegated scope,
* correctness vs approved intent,
* architecture/contracts/invariants,
* material AI-made decisions and deviations,
* tests and validation evidence,
* failure/data/concurrency/security concerns where applicable,
* sufficient personal understanding of the resulting implementation.

Expected author outcomes:

* **READY FOR REVIEW**
* **REWORK**
* **ESCALATE**

The author MAY use AI findings as additional evidence, but MUST still inspect and understand the implementation directly.

### Stage 4 — Human Pre-Flight

Before deep independent human review, the reviewer confirms that the change is actually reviewable:

* risk class is known,
* required automated gates passed,
* Author IDE Review is complete where required,
* approved intent and relevant design/test contracts are available,
* diff is complete enough for review,
* Agent Completion Report exists where required,
* known deviations are visible,
* required AI Review Independence level was achieved,
* reviewer has access to relevant technology-specific guides.

If these conditions are not met, return the change rather than spending review time reconstructing missing process context.

### Stage 5 — Independent Human Review

Human review uses the **Code Review Book / Checklist** plus only the technology-specific guides relevant to the change.

The reviewer SHOULD form an initial view before reading detailed author explanations and, where practical, before relying on AI findings. This reduces anchoring.

A useful sequence is:

**contract / source inspection → initial human findings → compare with AI findings → author explanation → final re-check**

### Stage 6 — Pair Review / Defence

Where required by risk or reviewer judgement, the Human Owner explains and defends the material implementation after the reviewer has formed an independent view.

The goal is to establish both implementation confidence and sufficient cognitive ownership by the Human Owner.

### Stage 7 — Review Decision

Exactly one disposition closes Review:

* **PR APPROVED**
* **CHANGES REQUIRED**
* **ESCALATED**

AI MAY prepare evidence and summaries. Final accountable approval remains human where required by the risk model.

# Risk Profiles

## R0 — Trivial / Mechanical

**Goal:** maximize speed while retaining basic objective evidence.

Required flow:

**Automated Pre-Flight → IR-1 AI Review where used → Lightweight Author/Human Check or policy-defined waiver → Decision**

Controls:

* Automated Pre-Flight: **MANDATORY**
* AI independence: **IR-1** sufficient
* Author/human review: lightweight; independent review MAY be waived by approved policy
* Pair Review / Defence: normally not required
* Output evidence: native PR/CI evidence usually sufficient

Review focus: scope, obvious functional correctness, regression risk and automated verification. Avoid review noise and stylistic over-analysis.

## R1 — Standard

Required flow:

**Automated Pre-Flight → IR-1 or IR-2 AI Review → Author IDE Review → Human Pre-Flight → Standard Independent Human Review → Decision**

Controls:

* Automated Pre-Flight: **MANDATORY**
* AI independence: **IR-1 or IR-2**
* Author IDE Review: standard
* Human review: standard
* Pair Review / Defence: optional
* Relevant technology guide(s): use when affected

## R2 — Significant

Required flow:

**Automated Pre-Flight → IR-2 AI Review → Author IDE Review → Human Pre-Flight → Independent Human Review → Pair Review / Defence when material AI-generated implementation warrants it → Decision**

Controls:

* Automated Pre-Flight: **MANDATORY**
* AI independence: **IR-2 REQUIRED** for the formal AI pass
* Author IDE Review: **REQUIRED**
* Human review: **INDEPENDENT REVIEW REQUIRED**
* Full relevant Code Review Book passes
* Agent Completion Report explicitly reviewed
* Pair Review / Defence: **RECOMMENDED**, especially for substantial AI-generated code
* Material deviations MUST be explicit

## R3 — High Risk

Required flow:

**Stronger Automated Pre-Flight → IR-2 / preferably IR-3 AI Review → Author IDE Review → Human Pre-Flight → Independent Human Review + Specialist Review as applicable → Mandatory Pair Review / Defence → Explicit Review Decision**

Controls:

* Automated Pre-Flight: **MANDATORY AND STRONGER**
* AI independence: **IR-2 minimum; IR-3 preferred**
* Author IDE Review: **MANDATORY**
* Independent human review: **MANDATORY**
* Pair Review / Defence: **MANDATORY for material changes**
* Specialist review: Security / Database / Messaging / Architecture / other area as risk requires
* Checklist evidence SHOULD be explicit
* Critical assumptions, consistency boundaries, recovery/failure behavior and security implications MUST be examined where applicable

## R4 — Critical

Required flow:

**Extended Automated Pre-Flight → IR-3 Supplemental AI Review → Author IDE Review → Human Pre-Flight → Specialist / Multi-Party Independent Human Review → Mandatory Pair Review / Defence → Explicit Human Approval**

Controls:

* Automated Pre-Flight: **EXTENDED**
* AI review: **SUPPLEMENTAL ONLY; IR-3 preferred**
* Author IDE Review: **MANDATORY**
* Human review: **SPECIALIST / MULTI-PARTY REQUIRED**
* Pair Review / Defence: **MANDATORY**
* Final approval: **EXPLICIT HUMAN AUTHORITY**
* Critical/irreversible assumptions MUST be directly verified by humans or deterministic evidence where possible
* AI MUST NOT be the final source of confidence for a critical decision

# Fail-Fast Rules

Manual review SHOULD NOT begin while a mandatory automated gate is failing.

Return to Implementation when:

* build does not compile,
* required tests fail,
* blocking static/security/architecture policy checks fail,
* required contract/schema compatibility fails,
* required migration validation fails,
* mandatory evidence is missing and cannot be reconstructed safely during review.

Exceptions require explicit ownership and must remain visible.

# Review Independence Rule

Higher risk requires greater independence of evidence.

**R0 → IR-1**  
**R1 → IR-1 / IR-2**  
**R2 → IR-2**  
**R3 → IR-2 / IR-3 preferred**  
**R4 → IR-3 preferred, AI supplemental only**

Reasoning depth is useful, but **higher reasoning effort is not equivalent to independent review**. Independence comes primarily from fresh context, different model/provider where appropriate, deterministic tools and independent humans.

# Related L4 Assets

* [**Automated Pre-Flight Checklist**](automated-pre-flight.md)
* [**Human Review Pre-Flight Checklist**](human-pre-flight.md)
* [**Code Review Book & Checklist**](code-review-book.md)
* [**AI Review Agent Instructions**](ai-review-agent.md)
* [**Author IDE Review Checklist**](author-ide-review.md)
* [**Pair Review & Defence Playbook**](pair-review-defence.md)
* Java / Spring / Database / Messaging Review Guides

> **Operating principle:** automate what can be objectively checked, isolate the AI reviewer from implementation bias, and spend human judgement on the areas where judgement is actually required.
