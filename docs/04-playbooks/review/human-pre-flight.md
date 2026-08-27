# Review Gate – Human Pre-Flight Checklist

> **Purpose:** provide a short, fixed-order reviewer readiness check before deep independent human review begins.

This checklist is deliberately short. It is not the code review itself. It answers one question:

> **Is this change ready to consume human review attention?**

If the answer is no, return the change before starting detailed review.

# Human Pre-Flight Sequence

## H01 — Risk & Review Profile

- [ ] `RISK_CLASS` is known: R0 / R1 / R2 / R3 / R4
- [ ] required AI Review Independence level is known
- [ ] required human review depth is known
- [ ] Pair Review / Defence requirement is known
- [ ] specialist review requirement is known where applicable

If risk is missing or appears underestimated, stop and request/recommend reclassification.

## H02 — Automated Gate

- [ ] Automated Pre-Flight result is **PASS**
- [ ] no mandatory automated failure remains
- [ ] BLOCKED checks, if any, have an explicit approved exception
- [ ] CI/tool evidence is accessible

**Stop condition:** mandatory gate failure.

## H03 — Intent & Contract Availability

Reviewer can access, as applicable:

- [ ] functional requirement / approved behavior
- [ ] Implementation Contract / implementation design
- [ ] Test Intent / correctness contract
- [ ] material Architecture / ADR decisions
- [ ] Definition of Done
- [ ] known accepted deviations / exceptions

The reviewer SHOULD NOT reconstruct material intent only from the code.

## H04 — Review Candidate Completeness

- [ ] diff / PR is stable enough for meaningful review
- [ ] change is not obviously mid-rework
- [ ] required generated artifacts are present
- [ ] no known missing commits/files invalidate the review
- [ ] review scope is understandable

If the candidate is materially incomplete, return it rather than reviewing a moving target.

## H05 — Author Ownership Readiness

Where required by risk:

- [ ] author completed Author IDE Review
- [ ] author identifies as Human Owner of the change
- [ ] author can explain objective and main approach
- [ ] material uncertainty has been surfaced rather than hidden

For R2–R4, weak author understanding is a readiness concern even before Pair Review / Defence.

## H06 — AI Execution Evidence

Where implementation was materially AI-assisted:

- [ ] Agent Completion Report is available where required
- [ ] reported changed scope can be compared with actual diff
- [ ] material autonomous decisions are listed
- [ ] deviations / unresolved risks are visible
- [ ] work deliberately not performed is visible where relevant

## H07 — AI Review Independence

If formal AI review is required:

- [ ] fresh reviewer context was used
- [ ] required IR level was met
- [ ] AI reviewer did not simply continue the implementation session
- [ ] AI Review Findings are available
- [ ] AI output is treated as advisory evidence, not approval

Risk expectations:

* **R0:** IR-1
* **R1:** IR-1 / IR-2
* **R2:** IR-2
* **R3:** IR-2 minimum, IR-3 preferred
* **R4:** IR-3 preferred; AI supplemental only

## H08 — Review Guides Selected

Select only relevant review books/guides:

- [ ] Generic Code Review Book
- [ ] Java
- [ ] Spring
- [ ] Database
- [ ] Messaging
- [ ] Security specialist guidance
- [ ] Architecture specialist guidance
- [ ] other domain-specific guide

Do not execute irrelevant checklists merely to satisfy process formality.

## H09 — Reviewer Independence

Before reading detailed author defence/explanation:

- [ ] reviewer understands the intended outcome
- [ ] reviewer has access to source evidence
- [ ] reviewer can form an initial independent view
- [ ] known conflicts of perspective/ownership are acceptable for the assigned risk class

For material work, prefer:

**independent inspection → initial findings → author explanation → discussion → final re-check**

rather than:

**author/AI narrative → reviewer searches for confirmation**.

## H10 — Ready to Review Decision

Choose exactly one:

### READY FOR INDEPENDENT REVIEW

Use when all mandatory pre-flight conditions for the risk class are satisfied.

### RETURN TO AUTHOR / IMPLEMENTATION

Use when the candidate is not ready because of failed automation, incomplete context, unstable diff, missing evidence or insufficient author readiness.

### ESCALATE

Use when readiness exposes:

* a risk-class dispute,
* Material Decision without owner,
* missing required authority,
* security/compliance concern,
* explicit exception need.

# Risk Scaling

## R0

Human pre-flight MAY be lightweight or absorbed into author/PR tooling.

Minimum focus:

* automated PASS,
* clear scope,
* change is reviewable.

## R1

Use the standard H01–H10 flow with pragmatic depth.

## R2

Human pre-flight SHOULD be explicit.

Mandatory emphasis:

* automated PASS,
* IR-2 evidence,
* Agent Completion Report where AI execution was material,
* independent reviewer readiness,
* contracts/test intent available.

## R3

Human pre-flight MUST explicitly confirm:

* stronger automated gate passed,
* required specialist review path is selected,
* IR-2 / preferably IR-3 AI review conditions are satisfied,
* author ownership is sufficient to proceed,
* Pair Review / Defence is scheduled/expected for material work.

## R4

Human pre-flight MUST be explicit and traceable.

It MUST confirm:

* extended automated evidence,
* specialist/multi-party human reviewers are identified,
* AI review is supplemental only,
* critical decision authority is available,
* Pair Review / Defence and explicit final approval are planned.

# Compact Pre-Flight Card

For practical use in a PR template or reviewer UI:

```plaintext
HUMAN REVIEW PRE-FLIGHT

[ ] Risk profile known
[ ] Automated gate PASS
[ ] Requirements / contracts available
[ ] Diff stable and complete
[ ] Author IDE review complete
[ ] Agent Completion Report available if required
[ ] Required AI independence achieved
[ ] Relevant review guides selected
[ ] Reviewer can form independent view

RESULT: READY | RETURN | ESCALATE
```

This compact card MAY be implemented directly in source-control tooling. The full page defines the meaning behind each check.

> **Pre-flight principle:** A reviewer should spend engineering judgement on a reviewable change, not on reconstructing missing context or rediscovering failures the pipeline should already have rejected.
