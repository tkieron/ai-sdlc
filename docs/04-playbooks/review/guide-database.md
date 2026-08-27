# Review Guide – Database

> **Purpose:** technology-specific extension to the generic Code Review Book for relational database, persistence and migration changes.

## Schema & Data Model

* Does the schema preserve domain invariants where the database is an appropriate enforcement boundary?
* Are nullability, defaults and constraints intentional?
* Are primary/foreign/unique constraints correct?
* Are data types appropriate for precision, range and semantics?
* Are timestamps/time zones handled consistently?
* Is denormalization intentional and justified?
* Does the change alter data ownership or meaning?

## Migration Safety

* Is the migration backward compatible with the currently deployed application where coexistence is possible?
* Can old and new application versions operate safely during rollout?
* Does the change follow an appropriate pattern such as **expand → migrate → observe → contract**?
* Are destructive changes separated from initial rollout where practical?
* Is migration runtime/locking impact understood?
* Is existing data transformed safely and deterministically?
* Is failure/restart behavior safe?
* Is rollback actually safe, or is roll-forward/recovery the correct strategy?

## Query Correctness

* Does the query return the intended result for empty/boundary/duplicate data?
* Are joins and predicates semantically correct?
* Could implicit inner/outer join behavior lose required rows?
* Are aggregate/grouping semantics correct?
* Are pagination and ordering deterministic where required?
* Could generated SQL differ materially from reviewer assumptions?

## Performance

* Are indexes aligned with actual predicates, joins and ordering?
* Could a new index create material write/storage cost?
* Are full scans acceptable for the expected data volume?
* Is N+1 behavior introduced by ORM usage?
* Could query plans change materially with production data distribution?
* Are batch sizes and bulk operations bounded?
* Is large data migration tested on representative volume where risk requires it?

## Transactions & Isolation

* Is the transaction boundary aligned with the business invariant?
* Is the configured/default isolation level sufficient?
* Are dirty/non-repeatable/phantom-read assumptions relevant?
* Could lost updates occur?
* Is optimistic/pessimistic locking used intentionally?
* Could lock ordering create deadlocks?
* Are external calls incorrectly coupled to open database transactions?

## Consistency & Idempotency

* Can retries or duplicate requests create duplicate rows/effects?
* Are uniqueness/idempotency constraints enforced reliably?
* Are multi-table updates atomic where required?
* If eventual consistency is intended, are intermediate states acceptable and observable?

## Security & Privacy

* Does the query/change expose more data than required?
* Are tenant/ownership filters enforced reliably?
* Is sensitive data added, copied or retained unexpectedly?
* Are dynamic queries parameterized?
* Are DB permissions broader than necessary?

## Recoverability

For material changes:

* What is the recovery strategy after partial migration?
* Can data be reconstructed or corrected?
* Are backups/restoration assumptions realistic?
* Are irreversible transformations explicitly accepted as risk?
* Has recovery been tested where R3/R4 risk justifies it?

## Testing Signals

* Are migrations tested from a realistic previous schema state?
* Are constraints and failure behavior tested?
* Are representative data volumes used for performance-sensitive changes?
* Are concurrent-update cases tested where relevant?
* Are repository/integration tests validating actual SQL/DB behavior rather than mocks only?

## AI-Specific Red Flags

Pay extra attention to AI-generated database work for:

* plausible but incorrect migration order,
* missing indexes or indexes added without workload reasoning,
* destructive one-step schema changes,
* incorrect assumptions about transaction isolation,
* ORM-generated N+1 behavior,
* migrations that are not restartable,
* tests using empty/tiny datasets that hide real production risk.

> **Review principle:** A schema or data change is judged by its operational and recovery consequences, not only by whether the migration script executes successfully.
