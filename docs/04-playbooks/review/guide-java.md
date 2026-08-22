# Review Guide – Java

> **Purpose:** technology-specific extension to the generic Code Review Book for Java implementation.

Use this guide only for Java-relevant concerns. It supplements, but does not replace, scope/contract/domain/security/test review.

## Language & API Correctness

* Are `equals()` / `hashCode()` contracts correct where identity/value semantics matter?
* Is mutability intentional? Could immutable value objects/records reduce risk?
* Are `null` semantics explicit and consistent?
* Are `Optional` usages meaningful rather than used as fields/parameters without reason?
* Are exceptions appropriate, preserved and translated at the correct boundary?
* Are resources closed correctly (`try-with-resources`)?
* Are streams used where they improve clarity, not where imperative code would be safer/readable?
* Are side effects hidden inside stream operations?
* Are collection choices and mutability appropriate?
* Are `BigDecimal` scale/rounding semantics explicit for financial logic?
* Are date/time APIs timezone-aware where required?

## Concurrency

Where applicable:

* Are shared mutable objects thread-safe?
* Is synchronization scope correct and minimal?
* Are atomic operations truly atomic across the whole invariant?
* Are executors/futures managed and terminated correctly?
* Are blocking operations accidentally introduced into asynchronous/reactive paths?
* Are visibility and publication assumptions valid?

## Object & Domain Design

* Do constructors/factories preserve invariants?
* Are domain rules located close to the domain rather than scattered across controllers/services?
* Is inheritance used only where subtype semantics are valid?
* Are sealed types/records/value objects useful for making impossible states harder to represent?
* Are public methods exposing more mutability or implementation detail than necessary?

## Error Handling

* Are exceptions swallowed or logged-and-rethrown redundantly?
* Is exception translation consistent with layer boundaries?
* Are retryable and non-retryable failures distinguishable?
* Are checked/unchecked exceptions used intentionally rather than mechanically?

## Performance / Memory

* Is accidental quadratic behavior present in loops/streams/collections?
* Are large collections copied unnecessarily?
* Are expensive computations repeated?
* Are unbounded caches/collections introduced?
* Are object allocations material in hot paths?

## Testing Signals

* Do tests assert observable behavior rather than private implementation details?
* Are parameterized tests useful for rule matrices/boundaries?
* Are concurrency/time-sensitive tests deterministic?
* Are test fixtures readable and domain-relevant?

## AI-Specific Red Flags

AI-generated Java often deserves extra attention for:

* invented utility abstractions,
* unnecessary generic frameworks,
* overuse of `Optional`/streams,
* duplicate validation at several layers,
* broad catch blocks,
* missing domain-specific edge cases,
* mechanically generated tests with weak assertions.

> **Review principle:** Prefer explicit, maintainable Java that preserves domain intent over clever language usage.
