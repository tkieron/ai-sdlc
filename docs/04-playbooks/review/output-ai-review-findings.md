# Review Output – AI Review Findings

Canonical logical output for an AI-assisted code review pass.

> **Purpose:** preserve actionable findings produced by AI without treating AI as the approval authority.

This artifact MAY be implemented as a pull-request comment, Markdown file or another organization-approved form. The logical content matters more than the storage tool.

## Required metadata

* **Change / PR:**
* **Risk class:** R0 / R1 / R2 / R3 / R4
* **Review scope:**
* **AI system / review agent:**
* **Review timestamp:**
* **Human owner:**

## Review basis

The review SHOULD identify which sources were checked, as applicable:

* Implementation Contract / approved design,
* Test Intent / correctness contract,
* architecture decisions,
* source diff,
* Agent Completion Report,
* automated test / CI evidence.

## Findings

Each material finding SHOULD use the following structure:

| Field | Content |
| --- | --- |
| ID | AI-RV-### |
| Severity | Blocking / Major / Minor / Observation |
| Area | Scope / Correctness / Architecture / Security / Data / Concurrency / Tests / Observability / Maintainability / Other |
| Evidence | Concrete file, code path, contract or behavior |
| Finding | What appears wrong, risky or inconsistent |
| Expected contract | Which approved requirement, invariant, design or standard is relevant |
| Recommendation | Proposed correction or next action |
| Confidence / uncertainty | Explicit where material |

## Scope and contract check

The AI review SHOULD explicitly state whether it detected:

* unexpected scope expansion,
* changes to public or material contracts,
* hidden architectural decisions,
* changed test oracles / acceptance expectations,
* unresolved agent deviations,
* new risk factors that may require reclassification.

## Summary

* **Blocking findings:**
* **Major findings:**
* **Minor findings:**
* **Residual uncertainty:**
* **Recommended next step:** Proceed to human review / Return to author / Escalate

## Governance rule

AI Review Findings are **advisory evidence**. They MUST NOT be treated as PR approval or as a substitute for the human review required by the assigned risk class.
