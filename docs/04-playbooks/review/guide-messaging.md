# Review Guide – Messaging

> **Purpose:** technology-specific extension to the generic Code Review Book for asynchronous messaging, Kafka, RabbitMQ and similar event/message-driven integration.

## Message Contract

* Is the message/event meaning clear and stable?
* Is schema/version compatibility preserved?
* Are required/optional fields intentional?
* Are consumers protected from additive/removal/type changes as required?
* Does the message expose sensitive data unnecessarily?
* Is the event a fact, command or notification with clear semantics?

## Delivery Semantics & Idempotency

* What delivery semantics are actually provided: at-most-once, at-least-once, effectively-once under constraints?
* Can a message be delivered more than once?
* Is the consumer idempotent where duplicates are possible?
* Is idempotency scoped to the correct business operation/key?
* Can producer retries create duplicate business effects?
* Is deduplication state bounded and recoverable?

Never assume “exactly once” from broker terminology without validating end-to-end business effects.

## Ordering

* Does business correctness depend on ordering?
* What is the real ordering boundary: queue, partition, key, consumer instance?
* Is the partition/routing key aligned with the ordering invariant?
* Can parallel consumers violate expected order?
* What happens when an earlier message fails but later messages continue?

## Producer Reliability

* What happens if the database commit succeeds but message publication fails?
* What happens if publication succeeds but local transaction rolls back?
* Is an Outbox / transactional publication pattern required?
* Are publisher confirms/acks configured where relevant?
* Are retries bounded and observable?

## Consumer Processing

* When is the message acknowledged/offset committed relative to business processing?
* Can processing failure lose a message?
* Can retries repeat partially completed side effects?
* Are long-running handlers affecting partition/consumer liveness?
* Is concurrency configured intentionally?
* Are consumer-group semantics understood?

## Retry / DLQ / Poison Messages

* Which failures are retryable vs permanent?
* Is retry policy bounded with suitable backoff?
* Can retry storms overload downstream systems?
* Is there a DLQ/dead-letter mechanism where useful?
* Is DLQ ownership and reprocessing policy defined?
* Can poison messages block a partition/queue indefinitely?
* Is manual replay safe and idempotent?

## Failure & Recovery

* What happens during broker outage?
* What happens when downstream dependencies are unavailable?
* Can messages accumulate without bounded capacity/operational response?
* Is replay after outage safe?
* Can producer/consumer deployment order break compatibility?
* Are recovery procedures consistent with message retention and business invariants?

## Transactions & Consistency

* Is eventual consistency explicitly acceptable?
* Are intermediate states observable and safe?
* Are local DB transactions incorrectly assumed to include broker operations?
* Are saga/compensation semantics required for multi-service workflows?
* Is duplicate compensation itself safe?

## Observability

Review whether operations can detect:

* consumer lag/backlog,
* publish failures,
* retry volume,
* DLQ growth,
* poison messages,
* handler latency,
* duplicate/replay anomalies,
* schema/serialization failures.

Material messages SHOULD carry appropriate correlation/trace/business identifiers without leaking protected information.

## Security

* Are producer/consumer permissions least-privilege?
* Are topic/queue names or routing rules exposing cross-tenant data?
* Is message content encrypted/protected where required?
* Can untrusted message fields influence commands, queries or authorization unsafely?

## Testing Signals

* Are duplicate deliveries tested where relevant?
* Are ordering assumptions tested?
* Are retry/DLQ paths exercised?
* Are schema compatibility tests present for material contracts?
* Are integration tests using realistic broker behavior rather than mocks only where semantics matter?
* Are producer-DB consistency failure cases tested when Outbox or similar patterns are used?

## AI-Specific Red Flags

Pay extra attention to AI-generated messaging code for:

* assuming one delivery per message,
* assuming global ordering in Kafka,
* retrying every exception identically,
* acknowledging before durable business processing,
* missing idempotency,
* using DLQ as an unexplained catch-all,
* changing event schemas without consumer-impact analysis,
* conflating local database transactions with broker transactions,
* tests that mock away the broker semantics being relied upon.

> **Review principle:** Message-driven correctness is defined by business effects under duplicates, retries, reordering and partial failure — not only by successful happy-path delivery.
