# 04 Level 4 – Engineering Playbooks

Level 4 translates AI-SDLC specifications into **concrete execution guidance for humans, teams, automation and AI agents**.

It answers:

> **How exactly should this activity be executed in practice?**

L4 may contain technical instructions, checklists, prompts, skills, agent/system instructions, templates, examples, Definition of Done fragments, MUST / MUST NOT rules and technology-specific conventions.

Unlike L1–L3, this level may intentionally contain tool-specific adapters such as Codex instructions, repository conventions, Jira/Confluence mappings, CI/CD implementation, testing frameworks and organization-specific automation.

## PoC Scope v0.1

The first AI-SDLC proof of concept deliberately implements only the minimum L4 needed to test the core model on real development work.

### Active PoC playbooks

1. [**Development**](development.md)

    * developer-side preparation and supervision,
    * AI Implementation Contract,
    * R0–R4 execution modes,
    * Agent Completion Report,
    * Author Review,
    * AI review / CI / human review flow,
    * PoC provenance rule.

2. [**AI Agents & Skills**](ai-agents-skills.md)

    * Codex/coding-agent baseline instruction,
    * risk-aware behavior for R0–R4,
    * STOP → DESCRIBE → PROPOSE → ESCALATE,
    * correctness and scope rules,
    * machine-oriented Completion Report format,
    * minimal AI review instruction.

3. [**Review**](review/)

    * risk-based review process,
    * automated and human pre-flight gates,
    * independent AI review,
    * human code review book,
    * pair review / defence,
    * technology-specific review guides,
    * canonical review output records.

### Additional areas

* [**Testing**](testing.md)
* [**Release**](release.md)

## PoC starter files — repository placement

```plaintext
<repository-root>/
├── AGENTS.md
├── .agents/
│   └── skills/
│       └── ai-sdlc-risk-aware-implementation/
│           └── SKILL.md
└── docs/
    └── ai-sdlc/
        └── AI-SDLC-IMPLEMENTATION-CONTRACT.md
```

### `AGENTS.md` — repository root

Purpose:

* durable AI-SDLC rules for the repository,
* requirement to identify `RISK_CLASS: R0 | R1 | R2 | R3 | R4`,
* instruction to use the risk-aware implementation skill,
* durable correctness, scope and escalation rules,
* project-specific build/test/architecture conventions.

Do **not** duplicate the complete AI-SDLC framework in `AGENTS.md`. Keep repository-specific durable context there and reusable execution logic in the skill.

### `SKILL.md` — repo-level Codex skill

Purpose:

* convert the assigned R0–R4 class into concrete agent behavior,
* vary implementation autonomy and human gates according to risk,
* enforce scope and correctness boundaries,
* define escalation behavior,
* require an Agent Completion Report for R2–R4.

| Risk | Default coding-agent behavior |
| --- | --- |
| **R0** | Execute efficiently with high local autonomy; escalate only when the task stops being trivial/mechanical. |
| **R1** | Standard autonomous implementation inside established conventions and scope. |
| **R2** | Bounded autonomous execution based on an explicit Implementation Contract; Completion Report required. |
| **R3** | Read/analyze/plan first; **human authorization is required before material write execution**. |
| **R4** | Read/analyze/verify/recommend by default; material write requires explicit `WRITE_AUTHORIZED: true` and an exact approved write scope. |

The risk class is a constraint. The agent MUST NOT silently downgrade it.

### `AI-SDLC-IMPLEMENTATION-CONTRACT.md` — task contract template

Purpose:

* provide a lightweight template for task-level delegation,
* explicitly communicate objective, risk class, scope, protected areas, invariants, correctness criteria, validation and stop conditions,
* provide the R3 plan-approval and R4 write-authorization fields.

The template is **not a mandatory file format**. A project may represent the same logical contract in Jira, documentation, repository metadata or another approved system, provided that the coding agent receives the required information unambiguously.

### Typical PoC usage

```plaintext
Human-approved task context
        +
AI-SDLC Implementation Contract
        +
RISK_CLASS
        ↓
AGENTS.md loads durable repository rules
        ↓
ai-sdlc-risk-aware-implementation skill
        ↓
Risk-adjusted agent execution
        ↓
Validation + Completion Report
        ↓
Human Author Review
```

> **PoC rule:** Start with the smallest executable L4 that can prove or falsify the AI-SDLC assumptions on real work.

## L4 relationship to upper levels

**L1 — Landscape** defines the operating model.  
**L2 — Process** defines logical phases, artifacts and gates.  
**L3 — Specification** defines what each process step MUST satisfy.  
**L4 — Playbook** defines how humans and machines execute those contracts in a concrete environment.

Lower-level playbooks MAY specialize upper-level rules but MUST NOT contradict the AI-SDLC Constitution, risk model or L3 contracts.
