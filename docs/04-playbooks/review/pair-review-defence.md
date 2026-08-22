# Review Playbook – Pair Review & Defence

> **Purpose:** create a structured human checkpoint for material or AI-heavy changes where code inspection alone is not sufficient to establish cognitive ownership and reviewer confidence.

Pair Review / Defence is not a presentation ritual. It is an engineering challenge session performed **after the reviewer has formed an independent view** of the change.

## 1. When to Use

Pair Review / Defence SHOULD be used when:

* risk policy requires it,
* the change is R2 with substantial AI-generated implementation,
* the change is R3 or R4 and material,
* reviewer confidence depends on author explanation,
* implementation contains complex domain, data, concurrency, security or integration behavior,
* the reviewer detects material AI-made assumptions or deviations,
* the author’s cognitive ownership is uncertain.

It MAY be skipped for low-risk changes where standard review provides sufficient confidence.

## 2. Preconditions

Before the session:

### Reviewer

* MUST inspect the source change independently where practical,
* SHOULD record initial findings before hearing the full author narrative,
* SHOULD identify the areas requiring challenge or clarification.

### Author / Human Owner

* MUST have completed Author IDE Review,
* MUST understand the approved design and correctness contract,
* SHOULD review Agent Completion Report and AI findings,
* MUST be prepared to explain material decisions rather than read an AI-generated summary.

## 3. Session Structure

Target a focused engineering session, not a full walkthrough of every line.

### Step 1 — Author Summary

In a few minutes, the author explains:

* the problem being solved,
* the chosen implementation approach,
* the main affected components/contracts,
* material AI participation,
* known limitations and residual risk.

### Step 2 — Reviewer Challenges

The reviewer asks targeted questions based on independent inspection.

Suggested challenge areas:

* Why this solution and not the main alternative?
* Which invariants must always hold?
* What are the main failure modes?
* What happens if a dependency partially fails?
* Where are transaction/consistency boundaries?
* Can duplicate/retried/concurrent execution break correctness?
* What public or integration contracts changed?
* What did AI decide locally that was not explicitly designed?
* Which tests give confidence, and what do they _not_ prove?
* What would you inspect first if production behavior degraded?
* How would the change be rolled back, disabled or otherwise recovered where relevant?

Technology-specific guides SHOULD supply additional questions.

### Step 3 — Contract Challenge

Explicitly check:

* approved scope vs actual implementation,
* test/correctness contract vs actual behavior,
* architecture intent vs actual boundaries,
* risk class vs newly discovered impact,
* Agent Completion Report vs actual diff.

### Step 4 — Cognitive Ownership Assessment

Reviewer assesses whether the author can explain, proportionally to risk:

* system behavior,
* material implementation decisions,
* key assumptions,
* failure modes,
* validation evidence and limitations,
* operational consequences.

A correct answer does not need to reproduce every implementation detail. The author must demonstrate an adequate **mental model**.

## 4. Failure Conditions

The session SHOULD NOT pass when:

* the author can explain the change only by repeating AI output,
* material behavior is not understood,
* the author is unaware of important changed contracts,
* reviewer discovers a hidden Material Decision,
* correctness criteria were changed to fit implementation,
* risk materially increased without reclassification,
* blocking review findings remain unresolved.

A green pipeline does not override these failure conditions.

## 5. Outcomes

Choose exactly one:

### DEFENCE PASSED

Use when reviewer has sufficient confidence in implementation, author demonstrates sufficient cognitive ownership, no blocking finding remains and material decisions/deviations are appropriately owned.

### REWORK REQUIRED

Use when implementation or author understanding requires improvement before approval.

### ESCALATE

Use when a Material Decision, specification conflict, security/data concern, risk increase or authority gap cannot be resolved within review.

## 6. Required Output

For risk classes requiring evidence, record the result in the canonical **Pair Review & Defence Record**.

Record only material challenge/response points; do not create a meeting transcript.

After successful defence, the reviewer SHOULD perform a final targeted re-check of any areas clarified or changed before issuing the Review Decision.

> **Operating principle:** The goal is not for the author to win the defence. The goal is for the reviewer to establish that the solution is both technically acceptable and genuinely human-owned.
