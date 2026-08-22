# Review Gate – Automated Pre-Flight Checklist

> **Purpose:** provide a fixed, repeatable and tool-driven pre-flight gate before formal AI and human code review begins.

This is the review equivalent of an aircraft pre-flight check: execute the applicable checks in a stable order, fail fast, and do not spend expensive review capacity on defects that automation can detect reliably.

## Gate outcome

The automated pre-flight produces exactly one state:

* **PASS** — all mandatory checks applicable to the assigned risk class passed.
* **FAIL** — at least one mandatory check failed; return to Implementation.
* **BLOCKED** — a mandatory check could not run; explicit exception / risk decision required before proceeding.

> A mandatory FAIL MUST NOT be converted into PASS by reviewer judgement.

# Pre-Flight Sequence

## A01 — Build / Compile

- [ ] project compiles / builds successfully
- [ ] generated sources required by the build are produced correctly
- [ ] no unresolved dependency-resolution errors
- [ ] packaging step succeeds where applicable

**Fail action:** Return to Implementation.

## A02 — Unit / Component Tests

- [ ] mandatory unit tests pass
- [ ] mandatory component/module tests pass
- [ ] no newly introduced ignored/disabled critical tests without explicit reason
- [ ] no unexpected test-suite crash or timeout

**Fail action:** Return to Implementation.

## A03 — Integration / Contract Tests

Where applicable:

- [ ] required integration tests pass
- [ ] API / consumer / provider contract tests pass
- [ ] integration environment dependencies required by policy are healthy enough for valid evidence

**Fail action:** Return to Implementation or mark BLOCKED if infrastructure prevents execution.

## A04 — Static Analysis / Lint / Quality Rules

- [ ] mandatory static-analysis rules pass
- [ ] no blocking quality findings
- [ ] formatter/lint policy passes where enforced
- [ ] no new prohibited warnings/errors introduced

Examples may include Sonar, SpotBugs, PMD, Error Prone, Checkstyle, ESLint or equivalent tooling.

## A05 — Architecture Rules

Where automated architecture rules exist:

- [ ] module/layer dependency rules pass
- [ ] forbidden dependency rules pass
- [ ] architecture tests such as ArchUnit or equivalent pass
- [ ] no prohibited package/module coupling is introduced

## A06 — Security / Secret / Dependency Checks

Where applicable:

- [ ] SAST mandatory checks pass
- [ ] secret scanning passes
- [ ] dependency vulnerability policy passes
- [ ] license/dependency policy passes where required
- [ ] container/image scan passes where relevant

A material security finding MUST NOT be downgraded solely to keep the review flow moving.

## A07 — Contract / Schema Compatibility

Where the change affects contracts:

- [ ] OpenAPI / schema validation passes
- [ ] event/message schema compatibility passes
- [ ] protobuf/Avro/JSON schema compatibility policy passes where used
- [ ] backward/forward compatibility checks required by policy pass

## A08 — Database / Migration Verification

Where the change affects persistence/schema:

- [ ] migration syntax/validation succeeds
- [ ] migrations can be applied from the expected previous schema state
- [ ] migration ordering is valid
- [ ] required rollback/roll-forward/recovery validation passes where automated
- [ ] schema compatibility checks pass where coexistence is required

## A09 — Test / Coverage Policy

Where coverage policy is used:

- [ ] required coverage threshold or changed-code policy passes
- [ ] no material reduction in critical coverage without explicit acceptance

Coverage is supporting evidence only; it MUST NOT be interpreted as proof of correctness.

## A10 — Artifact / Repository Hygiene

Where applicable:

- [ ] no unintended generated/binary/temp files are committed
- [ ] no secrets or local environment files are committed
- [ ] dependency lockfiles/manifests are consistent
- [ ] artifact metadata/versioning rules pass

# Risk Scaling

## R0 — Trivial / Mechanical

Minimum automated gate:

* A01 Build / Compile
* A02 Unit / Component Tests where applicable
* A04 Static Analysis / Lint relevant to the changed area

Additional checks run when the change touches the relevant concern.

## R1 — Standard

Standard gate:

* A01 Build / Compile
* A02 Unit / Component Tests
* A03 Integration / Contract Tests where applicable
* A04 Static Analysis
* A05 Architecture Rules where available
* A06 Security / Dependency baseline checks
* A07–A10 when affected

## R2 — Significant

All relevant standard checks are **MANDATORY**.

Additionally:

* contract/schema checks SHOULD be explicit for external interfaces,
* architecture checks SHOULD be explicit for boundary changes,
* security/dependency evidence SHOULD be retained,
* DB/migration evidence MUST be available for material persistence changes.

## R3 — High Risk

Automated pre-flight is **stronger and explicitly evidenced**.

In addition to all relevant checks:

* stronger SAST/security policy,
* contract compatibility for all material interfaces,
* representative integration evidence,
* migration/recovery automation where available,
* risk-relevant NFR automation such as performance/resilience checks where defined,
* specialist tool output retained where required.

## R4 — Critical

Automated verification is **extended** and acts as one evidence layer among several.

All applicable R3 checks are required, plus any domain-specific critical controls mandated by Security, Compliance, Data, Architecture or Operations.

Passing automation does not authorize approval. Critical changes still require specialist/multi-party human review.

# Pre-Flight Result Template

```plaintext
RISK_CLASS: R0 | R1 | R2 | R3 | R4
CHANGE_ID: <PR / change>

A01_BUILD: PASS | FAIL | N/A | BLOCKED
A02_UNIT_COMPONENT_TESTS: PASS | FAIL | N/A | BLOCKED
A03_INTEGRATION_CONTRACT_TESTS: PASS | FAIL | N/A | BLOCKED
A04_STATIC_ANALYSIS: PASS | FAIL | N/A | BLOCKED
A05_ARCHITECTURE_RULES: PASS | FAIL | N/A | BLOCKED
A06_SECURITY_DEPENDENCY: PASS | FAIL | N/A | BLOCKED
A07_CONTRACT_SCHEMA: PASS | FAIL | N/A | BLOCKED
A08_DATABASE_MIGRATION: PASS | FAIL | N/A | BLOCKED
A09_COVERAGE_POLICY: PASS | FAIL | N/A | BLOCKED
A10_REPOSITORY_HYGIENE: PASS | FAIL | N/A | BLOCKED

MANDATORY_FAILURES: <count>
BLOCKED_MANDATORY_CHECKS: <count>
OVERALL_GATE: PASS | FAIL | BLOCKED
EVIDENCE_LINKS: <CI / report references>
```

A CI/CD platform MAY generate this information automatically. A separate documentation record is not required when native tooling preserves equivalent evidence.

# Fail-Fast Rule

If `OVERALL_GATE = FAIL`, the change returns to **03.08 Implementation**.

If `OVERALL_GATE = BLOCKED`, the change MUST either:

1. wait for the missing check to become available, or
2. proceed only through an explicit risk/exception decision with compensating controls.

> **Operating principle:** machines should reject objectively invalid review candidates before humans spend time reasoning about them.
