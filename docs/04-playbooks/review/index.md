# Review

Engineering playbooks and canonical output records for AI-assisted and human code review.

This L4 area implements the review controls defined in **03.09 Review**. It is intentionally tool-adaptable: the same logical records may live in a pull request, Markdown, a review system or a combination of them.

> **Principle:** L3 defines which review evidence must exist. L4 defines how humans and AI agents execute the review and produce that evidence.

## Review flow

**Implementation Complete → Automated Pre-Flight → Independent AI Review → Human Pre-Flight → Independent Human Review → Pair Review / Defence where required → Final Review Decision**

The exact depth is controlled by R0–R4. Not every change requires every standalone record or every technology-specific guide.

# Risk-Based Process & Pre-Flight Gates

## Risk-Based Review Process

[**Review Playbook – Risk-Based Review Process**](risk-based-review-process.md)

This is the canonical L4 process for R0–R4. It defines:

* fail-fast review order,
* Automated Pre-Flight before expensive review work,
* AI Review Independence levels IR-1 / IR-2 / IR-3,
* human review depth by risk,
* specialist-review requirements,
* Pair Review / Defence requirements,
* explicit final approval requirements for critical work.

> **Fail-fast rule:** formal independent human review SHOULD NOT begin while a mandatory automated gate is failing.

## Automated Pre-Flight Checklist

[**Review Gate – Automated Pre-Flight Checklist**](automated-pre-flight.md)

Stable, tool-driven pre-flight sequence covering, where applicable:

* build / compile,
* unit / component / integration tests,
* static analysis / lint,
* architecture rules,
* security / secret / dependency checks,
* contract / schema compatibility,
* database / migration validation,
* coverage policy,
* repository hygiene.

The gate produces exactly one result: **PASS / FAIL / BLOCKED**.

A mandatory **FAIL** returns the change to Implementation. **BLOCKED** requires either waiting for the check or an explicit exception/risk decision.

## Human Pre-Flight Checklist

[**Review Gate – Human Pre-Flight Checklist**](human-pre-flight.md)

Short cockpit-style readiness check before deep human review. It verifies that:

* risk/review profile is known,
* automated gate passed,
* requirements/contracts are available,
* review candidate is stable and complete,
* author ownership evidence is sufficient,
* Agent Completion Report exists where required,
* required AI review independence was achieved,
* relevant review guides are selected,
* reviewer can form an independent view before author defence.

Outcome: **READY FOR INDEPENDENT REVIEW / RETURN TO AUTHOR / ESCALATE**.

# Execution Playbooks

## 1. Code Review Book / Checklist

[**Review Playbook – Code Review Book & Checklist**](code-review-book.md)

The canonical human review sequence. It uses stable review passes covering scope/contract, functional correctness, architecture, data/transactions/concurrency, security, failure handling, tests, observability, maintainability and AI-specific deviations.

It is designed as a **cockpit-style review book**: repeatable enough to reduce omissions, but risk-scaled so that review does not become checkbox bureaucracy.

## 2. AI Review Agent Instructions

[**Review Playbook – AI Review Agent Instructions**](ai-review-agent.md)

Machine-oriented instructions suitable for Codex or a similar review agent.

The agent:

* consumes `RISK_CLASS`, implementation/test contracts and review evidence,
* changes review depth for R0–R4,
* emits structured `AI-RV-###` findings,
* detects scope/correctness-contract deviations,
* uses `STOP → DESCRIBE → PROPOSE → ESCALATE`,
* MUST NOT act as the accountable PR approver.

## 3. Author IDE Review Checklist

[**Review Playbook – Author IDE Review Checklist**](author-ide-review.md)

Short pre-PR routine for the Human Owner. The author reviews the real diff in the IDE, validates Agent Completion Report claims and confirms sufficient cognitive ownership before independent review begins.

The expected author outcomes are:

* **READY FOR REVIEW**
* **REWORK**
* **ESCALATE**

## 4. Pair Review / Defence

[**Review Playbook – Pair Review & Defence**](pair-review-defence.md)

Structured challenge session for material / AI-heavy work. Reviewer independent inspection comes first; author explanation comes second to reduce anchoring.

The goal is to establish both:

1. technical confidence in the implementation, and
2. sufficient Human Owner mental model of the change.

# Technology-Specific Review Guides

Technology guides extend the generic Code Review Book only when the reviewed change touches the relevant area.

## Java

[**Review Guide – Java**](guide-java.md)

Covers Java-specific language/API correctness, object/domain design, exceptions, concurrency, collections, resources, performance and common AI-generated Java failure patterns.

## Spring / Spring Boot

[**Review Guide – Spring**](guide-spring.md)

Covers dependency injection, bean lifecycle, `@Transactional` / proxy behavior, REST contracts, Spring Security, JPA integration, configuration, resilience and Spring test patterns.

## Database

[**Review Guide – Database**](guide-database.md)

Covers schema/data model, migration safety, query correctness, indexes/performance, transaction/isolation/locking, idempotency, security and recoverability.

## Messaging

[**Review Guide – Messaging**](guide-messaging.md)

Covers Kafka/RabbitMQ-style asynchronous integration: message contracts, delivery semantics, idempotency, ordering, producer/consumer reliability, retry/DLQ, consistency, replay and observability.

# Canonical Review Output Records

## 1. AI Review Findings

[**Review Output – AI Review Findings**](output-ai-review-findings.md)

Use to preserve material findings produced by an AI reviewer, including scope/contract deviations, risks, evidence and recommendations.

AI findings are advisory evidence and never constitute final human approval.

## 2. Human Review Record

[**Review Output – Human Review Record**](output-human-review-record.md)

Use for the independent human reviewer checklist, findings, cognitive-ownership assessment and review outcome.

This is the primary structured human review record for R2+ and MAY be represented directly by equivalent PR review evidence for lower-risk work.

## 3. Pair Review & Defence Record

[**Review Output – Pair Review & Defence Record**](output-pair-review-defence-record.md)

Use where the risk model or reviewer requires deeper confirmation that the Human Owner understands and can defend the implementation.

The record captures material challenges and decisions, not a meeting transcript.

## 4. Review Decision Record

[**Review Output – Review Decision Record**](output-review-decision-record.md)

Use to close the Review stage with one logical disposition:

* **PR APPROVED**
* **CHANGES REQUIRED**
* **ESCALATED**

A separate record is unnecessary when the source-control/review platform already preserves equivalent evidence required by the risk class.

# How to Use the Review Library

A typical review does **not** mean reading every page.

Start with:

1. **Risk-Based Review Process**
2. **Automated Pre-Flight**
3. **Human Pre-Flight**
4. **Generic Code Review Book**
5. only the technology-specific guides affected by the change

Use **AI Review Agent Instructions** for the independent AI pass and **Pair Review / Defence** only when required by risk or reviewer judgement.

This keeps review modular and avoids one enormous checklist that every reviewer must execute regardless of context.

## Existing tool evidence is still valid

The following normally remain native system artifacts rather than separate documentation records:

* source diff / PR candidate,
* CI and static-analysis results,
* test execution evidence,
* source-control approval identity and timestamp,
* inline review comments.

AI-SDLC SHOULD avoid duplicating evidence solely for documentation purposes.

## Risk-oriented use

| Risk | Expected review approach |
| --- | --- |
| **R0** | Automated Pre-Flight mandatory; IR-1 sufficient; lightweight human check; Pair Defence normally unnecessary |
| **R1** | Automated Pre-Flight mandatory; IR-1/IR-2; standard independent human review; Pair Defence optional |
| **R2** | Automated Pre-Flight mandatory; IR-2; independent human review required; full relevant passes; Pair Defence recommended for substantial AI-generated code |
| **R3** | Stronger automated verification; IR-2 minimum / IR-3 preferred; independent + specialist human review; Pair Defence mandatory for material changes |
| **R4** | Extended automated evidence; IR-3 AI review supplemental only; specialist/multi-party human review; mandatory Defence and explicit human approval |

The authoritative requirements remain in **03.09 Review** and the **R0–R4 Risk Model**.

> **L4 Review principle:** Automate objective checks first, preserve independent viewpoints, deepen review according to risk, and spend human judgement where judgement is actually required.
