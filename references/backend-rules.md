# Backend rules

## Load when

Load this reference for server-side business behavior, authentication, scheduled work, queues, webhooks, private integrations, shared application services, or trusted data processing.

## Establish scope

Confirm from product material or the user:

- which behavior belongs on the trusted server boundary and which actors may invoke it;
- synchronous, asynchronous, scheduled, event-driven, and manual paths;
- data ownership, transaction boundaries, consistency needs, and concurrency risks;
- external systems, timeouts, retries, idempotency, credentials, and production-write authority;
- latency, throughput, audit, retention, and failure-recovery expectations.

## Rules

- Keep transport parsing, application orchestration, domain rules, and persistence responsibilities distinguishable. Follow the selected framework's established pattern instead of adding layers for appearance alone.
- Validate and normalize untrusted input at the boundary. Enforce authorization before reading or changing protected state.
- Put transaction boundaries around business invariants rather than individual repository calls. Define concurrency, duplicate-request, and partial-failure behavior where they matter.
- Make externally triggered writes idempotent when retries or duplicate delivery are possible. Store enough evidence to distinguish success, failure, and unknown outcomes.
- Give background work explicit payload ownership, retry limits, backoff, timeout, dead-letter or terminal-failure handling, and operator visibility.
- Map domain, validation, permission, dependency, and unexpected failures to stable observable outcomes without leaking secrets or internal details.
- Put timeouts and bounded retries around external calls. Record side effects before retrying any operation whose result may be unknown.
- Log stable identifiers, outcomes, durations, and failure context needed for support while excluding credentials and unnecessary personal data.

## Evidence

Choose checks that match the service:

- unit tests for rules with meaningful branches and invariants;
- integration tests for persistence, transactions, permissions, jobs, and external adapters;
- duplicate, timeout, retry, concurrency, and partial-failure tests where those paths exist;
- route, command, worker, and scheduler inventories when they are part of the contract;
- architecture checks required by the repository;
- target-environment evidence for managed dependencies or production-like behavior that local tests cannot prove.

Put concrete framework layers, service boundaries, queue configuration, logging conventions, commands, and forbidden shortcuts in the relevant scoped `AGENTS.md`.
