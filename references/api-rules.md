# API rules

## Load when

Load this reference when a browser, mobile app, partner, webhook sender, automation, service, or external customer needs a stable programmatic contract. Do not assume every backend requires a separately managed API.

## Establish scope

Confirm from product material or the user:

- consumers, owners, trust boundaries, and whether the API is internal, partner-facing, or public;
- protocol, authentication, authorization, tenancy, and credential lifecycle;
- resource ownership, commands, queries, events, and expected traffic patterns;
- compatibility period, release coordination, deprecation, and support expectations;
- timeout, retry, idempotency, ordering, webhook, and rate-limit behavior where relevant.

## Rules

- Define routes or operations, methods, request and response schemas, status outcomes, permissions, errors, and examples before implementation depends on them.
- Use stable field meanings and machine-readable error identifiers. Keep validation, permission, conflict, dependency, and unexpected failures distinguishable.
- Define pagination, filtering, sorting, search, field selection, limits, and deterministic ordering when a collection can grow.
- State idempotency and duplicate-delivery behavior for writes, retries, imports, callbacks, and webhooks.
- Define timeouts, retry guidance, rate limits, quotas, and back-pressure behavior only where the consumer needs them. Do not invent public guarantees without an owner.
- Treat authentication and authorization as separate checks. Document tenant and object ownership rules in addition to role checks.
- Define accepted origins, content types, request sizes, file handling, and webhook or callback verification where those boundaries exist.
- Review compatibility before changing or removing a field, status, default, or side effect. Use versioning or coordinated migration when consumers cannot move atomically.
- Keep the executable schema or contract source synchronized with implementation and examples when the project uses OpenAPI, GraphQL schemas, protobuf, event schemas, or an equivalent format.
- Do not call an API public, production-ready, or supported until access, documentation, limits, support ownership, and target-environment evidence exist.

## Evidence

Choose checks that match the contract:

- schema or contract validation;
- positive, validation, permission, not-found, conflict, rate-limit, and dependency-failure cases that apply;
- compatibility tests against current consumers or fixtures;
- idempotency, pagination, ordering, timeout, retry, and webhook-signature tests where relevant;
- generated documentation or example checks;
- target-environment smoke tests that avoid unauthorized writes.

Put concrete route conventions, schema tooling, error envelope, version policy, generation commands, and consumer test requirements in the relevant scoped `AGENTS.md`.
