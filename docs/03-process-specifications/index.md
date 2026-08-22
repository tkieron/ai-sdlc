# 03 Level 3 – Process Specifications

Level 3 defines the **normative contract for each logical step of AI-SDLC**.

L2 describes the overall process flow, its major artifacts and gates. L3 zooms into each logical step and defines **what must be true before the step starts, what responsibilities and decisions belong to humans and AI, what artifacts must exist, what evidence is required, and what conditions must be satisfied before the process may continue**.

L3 remains intentionally **tool-agnostic**. It defines the process interface and contract, not its implementation in Jira, Confluence, GitHub, CI/CD products or any other concrete toolchain.

> **L2 says what process blocks exist and how work flows between them. L3 defines the contract of each block. L4 explains how to execute that contract in practice.**

## 1. Normative language

* **MUST** — mandatory requirement.
* **MUST NOT** — prohibited behavior.
* **SHOULD** — expected default unless a justified exception exists.
* **SHOULD NOT** — normally prohibited unless a justified exception exists.
* **MAY** — optional or permitted behavior.

## 2. Canonical L3 specification structure

Every L3 process specification SHOULD use the same five-block structure.

### I. Intent

Defines Purpose, Scope, Inputs and Entry Criteria.

### II. Responsibility & Authority

Defines Human Responsibilities, AI Responsibilities / Permitted AI Role and Decision Rights.

### III. Execution Contract

Defines Logical Activities, Required Artifacts and Mandatory Artifact Content.

> **L3 defines the schema and contract of an artifact. L4 defines the template and concrete implementation.**

### IV. Control

Defines Exit Criteria / Gate, Required Evidence, Risk Adjustments R0–R4, Stop / Escalation Conditions and Exceptions.

The standard escalation pattern is:

**STOP → DESCRIBE → PROPOSE → ESCALATE**

### V. Traceability & Navigation

Defines Traceability, Upstream / Downstream Contracts and Related L4 Playbooks.

## 3. L3 as a process interface

A Level 3 specification should be readable as an interface between lifecycle stages:

**Inputs + Entry Criteria**  
→ **Responsibilities + Decisions + Logical Activities**  
→ **Artifacts + Evidence**  
→ **Exit Gate**

The implementation of this interface is intentionally flexible.

## 4. Relationship to the AI-SDLC hierarchy

**00 Principles & Governance**  
↓  
**05 Risk Model R0–R4**  
↓  
**L2 Development Process Map**  
↓  
**L3 Process Specifications**  
↓  
**L4 Engineering Playbooks / Organizational Adapters**

Lower-level guidance may add detail and implementation choices, but MUST NOT contradict higher-level principles and controls.

## 5. Process specifications

* [**03.01 Idea & Discovery**](03.01-idea-discovery.md)
* [**03.02 Analysis**](03.02-analysis.md)
* [**03.03 Architecture**](03.03-architecture.md)
* [**03.04 Refinement**](03.04-refinement.md)
* [**03.05 Planning**](03.05-planning.md)
* [**03.06 Test Design**](03.06-test-design.md)
* [**03.07 Implementation Design**](03.07-implementation-design.md)
* [**03.08 Implementation**](03.08-implementation.md)
* [**03.09 Review**](03.09-review.md)
* [**03.10 Verification & Acceptance**](03.10-verification-acceptance.md)
* [**03.11 Release & Deployment**](03.11-release-deployment.md)
* [**03.12 Production Feedback**](03.12-production-feedback.md)

This granularity is intentional. L3 defines meaningful lifecycle contracts without creating a separate specification for every micro-step.

## 6. Working rule for L3 authoring

> **If the statement defines what must be true regardless of the implementation tool, it belongs in L3. If it explains exactly how a team, engineer or agent should execute it, it belongs in L4.**
