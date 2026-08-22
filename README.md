# AI-SDLC

**AI-Augmented Software Development Lifecycle**

> A human-owned, AI-augmented model of software delivery.

**Version:** 0.1 — working public baseline

AI-SDLC is a working framework for software delivery in which humans retain ownership of problem understanding, engineering decisions, acceptance criteria and production responsibility, while GenAI is used aggressively for execution, automation, documentation, analysis and other engineering toil where this improves delivery without weakening cognitive ownership.

The framework is built around one central idea:

> **AI may perform the work. Humans own the outcome.**

AI-SDLC does not ask *"How much AI can we use?"* It asks:

> **Where is AI autonomy valuable, bounded and safe?**

---

## Why AI-SDLC?

GenAI can accelerate software delivery, but raw agent autonomy is not a software development model.

AI-SDLC provides a structured way to combine:

- human accountability,
- cognitive ownership,
- human decision authority,
- bounded AI autonomy,
- human-defined correctness,
- independent validation,
- production safety and recoverability,
- continuous evaluation.

The objective is **augmentation, not responsibility transfer**.

---

## Four levels of zoom

AI-SDLC uses a four-level model inspired by C4. The levels are different zoom levels on the same lifecycle — not sequential phases.

| Level | Main question | Primary audience |
| --- | --- | --- |
| **L1 — Landscape** | How do we work with GenAI overall? | Everyone / leadership / onboarding |
| **L2 — Process** | How does the whole delivery flow work? | Teams / leads / managers |
| **L3 — Specification** | What exactly must happen in this lifecycle step? | Owners of lifecycle steps |
| **L4 — Playbook** | How exactly should a human, tool or agent execute it? | Developers / QA / agents / automation |

Cross-cutting dimensions apply across all four levels:

- **Principles & Governance**
- **Risk Model R0–R4**
- **Metrics & Evaluation**
- **Decision records and framework evolution**

See [Framework Overview](docs/framework-overview.md).

---

## Lifecycle

The six major process groups are:

**Discover → Design → Build → Validate → Release → Operate & Learn → Discover**

| Phase | Human / AI operating model | Primary outcome |
| --- | --- | --- |
| **Discover** | Human-led + AI-assisted | Validated problem and requirement context |
| **Design** | Human-owned · AI consultative | Approved design, test intent and implementation intent |
| **Build** | Shared Human + AI | Reviewed implementation and implementation evidence |
| **Validate** | AI-heavy + Human validation | Acceptance evidence |
| **Release** | Automation + Human gates | Verified production release |
| **Operate & Learn** | Human-owned + AI-supported | Operational evidence, feedback and learning |

AI participation is intentionally **non-linear**. It contracts where business context, architecture and material engineering decisions dominate, and expands where intent, constraints and correctness have already been made explicit.

A representative execution model is:

**Problem understanding → Human design → Explicit constraints → Test intent → Bounded AI execution → Independent validation**

---

## Risk-based autonomy

AI-SDLC uses a cross-cutting R0–R4 risk classification:

- **R0 — Trivial / Mechanical**
- **R1 — Standard**
- **R2 — Significant**
- **R3 — High Risk**
- **R4 — Critical**

The direction is simple:

> **Higher risk = narrower AI autonomy + stronger independent controls.**

Risk affects planning depth, human ownership, test design, review, NFR validation, release gates, rollout, observability and recovery strategy.

Detailed classification criteria and mandatory controls are still evolving in v0.1.

---

## Core principles

The current constitutional baseline is summarized in [Manifesto](docs/manifesto.md).

Among the foundational rules:

1. Every material change has an identifiable human owner.
2. AI assistance never transfers engineering accountability.
3. Human ownership requires sufficient understanding of the solution.
4. Material engineering decisions remain human decisions.
5. AI autonomy is delegated, bounded and risk-dependent.
6. AI must not silently expand scope or redefine business intent.
7. Correctness must be defined independently of generated implementation.
8. AI output is not trusted by origin alone.
9. Production authority, risk acceptance and recovery remain human-accountable.
10. AI-SDLC must be measured and continuously evolved.

---

## What does Done mean?

> **Done = deployed, verified and operating correctly in production.**

A merged pull request is not Done.

A successful deployment is not Done.

A material release becomes Done only after sufficient evidence confirms that it is deployed correctly, critical smoke paths succeed and production observation does not show unacceptable technical or business degradation.

---

## Full specification

The detailed specification currently lives in Confluence and will be made public.

**AI-SDLC Home:**  
https://tomasz-kieronski.atlassian.net/wiki/spaces/AISDLC/pages/5537793/AI-SDLC+Home

Key sections:

- Principles & Governance: https://tomasz-kieronski.atlassian.net/wiki/spaces/AISDLC/pages/5603329/00+Principles+Governance
- Level 1 — Development Landscape: https://tomasz-kieronski.atlassian.net/wiki/spaces/AISDLC/pages/5373961/01+Level+1+Development+Landscape
- Level 2 — Development Process Map: https://tomasz-kieronski.atlassian.net/wiki/spaces/AISDLC/pages/5636097/02+Level+2+Development+Process+Map
- Level 3 — Process Specifications: https://tomasz-kieronski.atlassian.net/wiki/spaces/AISDLC/pages/5668865
- Level 4 — Engineering Playbooks: https://tomasz-kieronski.atlassian.net/wiki/spaces/AISDLC/pages/5308418/04+Level+4+Engineering+Playbooks
- Risk Model R0–R4: https://tomasz-kieronski.atlassian.net/wiki/spaces/AISDLC/pages/5701633/05+Risk+Model+R0+R4
- Metrics & Evaluation: https://tomasz-kieronski.atlassian.net/wiki/spaces/AISDLC/pages/5701653/06+Metrics+Evaluation

> **Note:** public access to the Confluence specification may still be pending while v0.1 is being prepared.

---

## Current status — v0.1

AI-SDLC is a **working framework**, not a finished standard.

The current objective is to validate the central model on real software delivery work before investing in deeper automation or formalization.

Current priorities:

- validate the lifecycle on real development work,
- refine R0–R4 classification and mandatory controls,
- evolve L3 process contracts,
- create practical L4 engineering playbooks,
- define measurable baselines for delivery, quality and AI-specific effects,
- document field experiments and lessons learned.

See [VERSION.md](VERSION.md) for scope and maturity.

---

## Contributing

AI-SDLC is intended to evolve through real engineering use, criticism and field experiments.

If you want to challenge an assumption, propose a control, report an experiment or improve a playbook, see [CONTRIBUTING.md](CONTRIBUTING.md).

The goal is not to maximize AI usage. The goal is to find **where AI measurably improves software delivery without degrading engineering ownership, quality or capability**.
