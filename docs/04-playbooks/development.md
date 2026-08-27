# Development

> **PoC baseline v0.1.** This playbook is intentionally small. Its purpose is to make the L3 contracts executable in a real development workflow and to give developers a consistent way to work with coding agents such as Codex. It is expected to evolve through AI-SDLC evaluation.

## 1. Purpose

This playbook answers:

> **How should a developer prepare, delegate, supervise, review and accept AI-assisted implementation while preserving human ownership?**

The developer remains the Human Owner of the implementation outcome. AI may perform substantial execution, but its authority is bounded by the approved risk class, implementation contract and AI-SDLC Constitution.

This playbook is tool-agnostic. Codex, Claude Code or another coding agent may implement it through project instructions, an `AGENTS.md`-style file, agent skills or equivalent configuration.

---

# 2. Developer Flow

## Step 1 — Confirm Ready for Development

Before implementation begins, the developer MUST verify that the relevant L3 contracts are sufficiently complete.

At minimum, the developer MUST know:

* the **Human Owner**,
* the approved **R0–R4 risk class**,
* the implementation goal,
* functional intent and acceptance criteria,
* material architecture constraints,
* relevant contracts and invariants,
* test intent / correctness contract,
* Definition of Done,
* known material risks and dependencies.

If a material input is missing, implementation MUST NOT be delegated merely so the agent can infer it.

## Step 2 — Prepare the AI Implementation Contract

For AI-assisted execution, prepare a bounded work package.

### Minimal contract

```plaintext
RISK_CLASS:
HUMAN_OWNER:
GOAL:

ALLOWED_SCOPE:

FORBIDDEN_SCOPE:

MATERIAL_DECISIONS_ALREADY_MADE:

CONTRACTS_AND_INVARIANTS:

CORRECTNESS_CONTRACT:
- acceptance criteria
- approved test intent
- critical scenarios

REQUIRED_VALIDATION:

PERMISSIONS / TOOL BOUNDARIES:

STOP_AND_ESCALATION_CONDITIONS:

DEFINITION_OF_DONE:
```

The contract MAY be assembled from multiple approved artifacts. It does not need to exist as one physical file, but the agent MUST be able to access an unambiguous execution context.

## Step 3 — Select the risk-based execution mode

The Human Owner MUST provide the risk class. The agent MAY recommend a different class, but MUST NOT authoritatively downgrade its own risk.

| Risk | Developer / agent operating mode | Minimum expectation |
| --- | --- | --- |
| **R0 — Trivial / Mechanical** | **Broad bounded autonomy** | Lightweight contract; agent may implement, run tests and perform local mechanical refactoring. Human performs proportional final review. |
| **R1 — Standard** | **Standard autonomous implementation** | Explicit goal, scope and correctness criteria. Agent may implement end-to-end inside the boundary. Human author review is required. |
| **R2 — Significant** | **Explicitly bounded agent execution** | Full Implementation Contract required. Material decisions remain human. Agent Completion Report and independent human review required. |
| **R3 — High Risk** | **Restricted execution with human checkpoint** | Agent MUST first produce a pre-execution plan and wait for human authorization before material writes. Scope is narrow; deviations stop execution. Strong independent validation required. |
| **R4 — Critical** | **Human-first, AI narrowly supporting** | Agent defaults to analysis/advice. Write execution requires explicit authorization and narrowly identified scope. Critical logic and irreversible decisions remain directly human-led. Specialist review is expected. |

The authoritative classification criteria live in **05 Risk Model R0–R4**. This table defines only the initial PoC execution behavior once a class has been assigned.

---

# 3. Agent Start Procedure

Before allowing material agent execution, the developer SHOULD require an **Execution Precheck** containing:

* recognized risk class,
* understood goal,
* allowed scope,
* protected / forbidden areas,
* material contracts and invariants,
* validation to be executed,
* identified stop conditions,
* any unresolved ambiguity.

### R0–R1

If the contract is sufficient, the agent MAY proceed directly after the precheck.

### R2

The agent MAY proceed after the precheck only when the explicit Implementation Contract is complete and no material decision is unresolved.

### R3

The agent MUST stop after the precheck and obtain explicit human authorization before performing material source changes.

### R4

The default mode is read/analyze/propose. The agent MUST NOT perform source modifications unless the Human Owner explicitly grants write authority for a narrowly identified scope.

---

# 4. Agent Execution Rules

During implementation the agent MAY iterate through:

**inspect context → implement bounded change → run validation → analyze failures → correct implementation → repeat**

The agent MUST:

* stay within delegated scope,
* preserve approved contracts and invariants,
* preserve accepted correctness criteria,
* expose material assumptions,
* run the required validation available to it,
* stop when a Material Decision is required,
* stop when risk materially increases,
* stop when protected scope must be modified,
* stop when implementation conflicts with the accepted correctness contract,
* stop when required validation cannot be completed.

The standard escalation pattern is:

> **STOP → DESCRIBE → PROPOSE → ESCALATE**

The agent MAY propose adjacent refactoring, dependency updates or improvements, but MUST NOT execute them outside the current scope without re-authorization.

---

# 5. Correctness and Tests

The developer owns test intent. AI may implement the mechanics.

An accepted expected result, acceptance criterion or test oracle MUST NOT be changed by the agent merely to make the implementation pass.

If implementation and the correctness contract conflict, the agent MUST report a **SPECIFICATION / IMPLEMENTATION MISMATCH** and return the decision to a human.

Tests MAY legitimately change when new knowledge is discovered, but only after explicit human acceptance of the changed correctness contract.

---

# 6. Agent Completion Report

For **R2–R4**, and for any otherwise material delegated implementation, an Agent Completion Report is REQUIRED.

R0 MAY omit it. R1 SHOULD use it when useful.

Minimum structure:

```plaintext
AGENT COMPLETION REPORT

Risk class:
Goal completed: YES / NO / PARTIAL

Changed:
- material files / components

Validation executed:
- build
- tests
- static checks
- other required controls

Result:
- passed / failed / not available

Local decisions made autonomously:
- ...

Deviations from approved contract:
- NONE / ...

Known risks / unresolved issues:
- ...

Work deliberately not performed:
- ...

Suggested follow-up outside current scope:
- ...
```

The report supports review. It does not replace source inspection or human ownership.

---

# 7. Developer Author Review

After agent execution, the Human Owner MUST inspect the resulting change before requesting external approval.

The developer SHOULD verify at least:

* does the implementation match the design I approved?
* did the agent stay within scope?
* were contracts or public behavior changed unexpectedly?
* are domain invariants preserved?
* are transaction, consistency and concurrency assumptions correct?
* are failure paths handled deliberately?
* did tests remain faithful to the accepted test intent?
* did the agent introduce unnecessary abstraction, dependencies or refactoring?
* can I explain the implementation and material decisions without relying on the agent summary?

If the developer cannot adequately explain a material change, the change is not ready for approval.

---

# 8. AI Review, CI and Human Review

After Author Review, the normal PoC path is:

**Author Review → AI Review → CI / Quality Gates → Independent Human Review → Pair Review / Defence where required → PR Approved**

AI review SHOULD compare the implementation with the approved contract rather than only perform generic code-quality review.

Review SHOULD consider:

* contract compliance,
* scope compliance,
* architecture,
* correctness,
* error handling,
* security,
* transactions / concurrency,
* observability,
* tests,
* maintainability,
* unexpected changes.

The risk class determines how much of the human review path is mandatory.

---

# 9. Pair Review / Defence

For material changes, especially R2–R4, the Human Owner SHOULD be able to explain to the reviewer:

* what changed,
* why the chosen design is appropriate,
* what alternatives or trade-offs existed,
* which decisions were made by humans,
* which local decisions were delegated to AI,
* important failure modes,
* how correctness was established,
* material operational consequences.

The purpose is not ceremony. It is evidence of cognitive ownership.

---

# 10. AI Provenance — PoC Rule

For the PoC, AI participation SHOULD be visible at **change / PR level** when material.

Recommended metadata:

```plaintext
AI-assisted: yes/no
Agent/tool: <name>
Risk class: R0-R4
Human Owner: <role/person>
Execution mode: advisory / bounded implementation / restricted implementation
```

Source-level comments or annotations are NOT required for every AI-modified method. They MAY be used for machine-generated, machine-managed or specifically regulated artifacts. Detailed provenance conventions remain future L4 work.

---

# 11. PoC Definition of Ready for Agent Execution

Agent execution SHOULD NOT start until the following are known at the level required by risk:

- [ ] Human Owner
- [ ] R0–R4 class
- [ ] Goal
- [ ] Allowed scope
- [ ] Protected / forbidden scope
- [ ] Material decisions resolved
- [ ] Contracts / invariants
- [ ] Correctness contract / test intent
- [ ] Required validation
- [ ] Tool / permission boundaries
- [ ] Stop / escalation conditions
- [ ] Definition of Done

---

# 12. PoC Definition of Complete

AI-assisted implementation is ready to move to formal review when:

- [ ] delegated work is complete or explicitly reported as partial,
- [ ] required validation has been executed,
- [ ] accepted correctness criteria remain intact,
- [ ] no unauthorized scope expansion occurred,
- [ ] deviations are human-approved,
- [ ] completion evidence is available,
- [ ] the Human Owner has inspected the implementation,
- [ ] the Human Owner can explain and defend the material solution.

> **PoC operating rule:** Human designs and owns the change. AI executes as much as the risk class and explicit contract safely allow.
