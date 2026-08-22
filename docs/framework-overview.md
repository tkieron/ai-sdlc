# AI-SDLC Framework Overview — v0.1

AI-SDLC is a four-level, human-owned and AI-augmented software delivery model.

## Four levels

| Level | Purpose |
| --- | --- |
| **L1 — Development Landscape** | Executive and onboarding view of the complete lifecycle and Human/AI participation |
| **L2 — Development Process Map** | Logical process contract: activities, artifacts, ownership and gates |
| **L3 — Process Specifications** | Detailed contract for each lifecycle step |
| **L4 — Engineering Playbooks** | Concrete instructions, checklists, prompts, skills and agent guidance |

These are different zoom levels on the same lifecycle.

## Lifecycle

**Discover → Design → Build → Validate → Release → Operate & Learn → Discover**

### Discover

**Idea → Discovery → Analysis → Analysis Approved**

Purpose: understand the problem, business need and opportunity well enough to create reliable input for solution design.

AI is useful for clarification, synthesis, gap detection and documentation. Business intent remains human-owned.

### Design

**Architecture → Refinement → Planning → Test Design → Implementation Design → Ready for Development**

Purpose: decide how the solution should work and how correctness will be recognized before implementation begins.

This is deliberately strongly human-owned. AI acts primarily as consultant, challenger and analytical assistant.

Ready for Development means more than a described ticket. The team should be able to explain:

1. how the solution is intended to work, and
2. how it will recognize that the solution works correctly.

### Build

Representative flow:

**AI Implementation Contract → Implementation → Agent Completion Report → Author Review → AI Review → CI Quality Gate → Independent Human Review → Pair Review / Defence → PR Approved**

Controls vary by risk class.

AI may perform substantial bounded implementation after human design and correctness intent have been established.

When execution reaches a decision outside delegated authority:

**STOP → DESCRIBE → PROPOSE → ESCALATE**

The Human Owner reviews implementation against a design they already understand rather than discovering the design from generated code.

### Validate

Representative model:

**Functional Validation + Manual / Exploratory + Selected E2E + Relevant NFR Validation → Acceptance Passed**

Validation activities may run in parallel.

AI may heavily support test implementation, test data, execution and evidence analysis. Humans retain ownership of test intent, acceptance meaning and material risk decisions.

E2E is selective rather than a 1:1 transcription of every manual test.

### Release

Representative flow:

**Merge → Build Once → Immutable Artifact → INT → QA → PREPROD → Ready for Production → PROD → Smoke → Observation → Release Accepted**

AI-SDLC prefers:

**build once → verify → promote**

Release safeguards include deployment strategy, recovery strategy, rollback/roll-forward capability, feature flags where appropriate, migration strategy, observability and defined recovery triggers.

Deployment success is not final acceptance.

**Smoke → Observation → Release Accepted**

### Operate & Learn

Inputs include production metrics, incidents, user feedback, support signals, business KPIs, defects and operational observations.

AI may support signal aggregation, summarization, pattern detection and release-to-incident correlation.

Humans decide which conclusions become changes to product, architecture, process or AI-SDLC itself.

**Production Evidence → Learning → Backlog / New Ideas → Discover**

## Major gates

| Gate | Meaning |
| --- | --- |
| **Analysis Approved** | Problem and requirement context are sufficient for design |
| **Ready for Development** | Design, constraints and correctness intent are sufficient for implementation |
| **PR Approved** | Implementation is understood, reviewed and accepted |
| **Acceptance Passed** | Required functional and non-functional evidence is sufficient |
| **Ready for Production** | Release risk and operational readiness are acceptable |
| **Release Accepted** | Production release has been verified and operates acceptably |

## Artifact flow

A representative logical chain is:

**Problem Context**  
↓  
**Functional Specification**  
↓  
**Architecture / Design**  
↓  
**Test & Correctness Contract**  
↓  
**Implementation Contract**  
↓  
**Trusted Code Artifact**  
↓  
**Acceptance Evidence**  
↓  
**Release Package**  
↓  
**Production Evidence**

Not every artifact must be a separate document. Each represents engineering information or evidence that must be available and sufficiently trusted for downstream work.

## Cross-cutting risk model

Working classes:

- **R0 — trivial / mechanical**
- **R1 — standard**
- **R2 — significant**
- **R3 — high risk**
- **R4 — critical**

The class controls the strictness of planning, human ownership, test design, review, NFR validation, release gates, rollout, observability and recovery strategy.

Exact v0.1 classification criteria and mandatory controls are still being developed.

## Evaluation

Initial candidate metrics include:

### Delivery and quality

- Lead time
- Cycle time
- PR size
- Review time
- Escaped defects
- Change failure rate
- Rollback rate
- Rework
- E2E stability
- Incident rate

### AI-specific

- AI-generated code accepted vs reworked
- Human interventions during agent execution
- Agent implementation failures
- Defects attributable to AI-assisted changes
- Time saved in documentation, testing and analysis workflows

Exact definitions, baselines and success criteria remain part of the v0.1 validation work.

## Full specification

The detailed and evolving specification is published on GitHub Pages:

https://tkieron.github.io/ai-sdlc/
