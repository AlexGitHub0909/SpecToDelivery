# Database and storage rules

## Load when

Load this reference for durable structured data, business state, accounts, workflow history, reporting, search indexes, audit records, object metadata, or another stateful store. Do not load it for a static project with no owned persistent data.

## Establish scope

Confirm from product material or the user:

- entities, ownership, tenancy, relationships, state transitions, and deletion responsibility;
- expected volume, growth, access patterns, latency, consistency, and reporting needs;
- retention, audit, privacy, residency, encryption, export, and deletion requirements;
- source-of-truth boundaries between databases, caches, search indexes, files, and external systems;
- migration, backfill, backup, restore, and acceptable-downtime expectations.

## Rules

- Model business invariants with suitable types, nullability, uniqueness, checks, relationships, and application rules. Do not rely on UI validation for data integrity.
- Define units, currency precision, time zones, timestamps, identifiers, ordering, and state values explicitly.
- Add indexes from real access paths and expected scale. Review write cost, selectivity, uniqueness, and query plans instead of indexing every field.
- Keep transaction and locking boundaries consistent with business invariants. Define behavior for concurrent updates, retries, duplicates, and partial writes.
- Design migrations for the actual deployment model. Separate schema expansion, data backfill, code transition, constraint enforcement, and cleanup when one-step migration is unsafe.
- Give every destructive change a verified backup, restore, rollback, or forward-repair path. A down migration alone is not proof that data can be recovered.
- Keep cache and search data rebuildable unless the product explicitly treats them as a source of truth.
- Keep seeds, fixtures, logs, exports, and test databases free of real credentials and unnecessary personal or customer data.
- Enforce least-privilege access and document sensitive fields, retention, deletion, and audit ownership.

## Evidence

Choose checks that match the data risk:

- schema and migration tests from supported starting states;
- invariant, uniqueness, relationship, transaction, and concurrency tests;
- representative query-plan or performance checks for high-volume paths;
- backfill restart, repeatability, and partial-failure checks;
- backup and restore evidence before destructive or high-risk changes;
- privacy, tenancy, retention, export, and deletion tests where required.

Put concrete database engine rules, naming, migration commands, transaction patterns, test isolation, backup tooling, and forbidden data practices in the relevant scoped `AGENTS.md`.
