# Operations rules

## Load when

Load this reference when the project has hosted environments, deployable artifacts, domains, scheduled or background runtime, production data, monitoring, support ownership, or a release and recovery process. Scale it down for local-only tools or static artifacts.

## Establish scope

Confirm from product material, repository evidence, or the user:

- environments, regions, runtime owners, release authority, and support boundaries;
- artifact source, configuration, secrets, managed dependencies, domains, and certificates;
- availability, latency, capacity, cost, maintenance-window, and acceptable-downtime expectations;
- migrations, queues, workers, schedules, caches, external integrations, and stateful resources;
- monitoring, alert ownership, incident response, backup, restore, recovery time, and recovery point needs.

## Rules

- Make the deployed revision or artifact traceable to reviewed source. Keep environment-specific configuration outside source control and never print secret values.
- Separate build, release, migration, traffic switch, verification, and rollback steps when they can fail independently.
- Make release procedures repeatable and non-interactive where practical. Record required approvals, operator actions, stop conditions, and safe retry behavior.
- Check migration compatibility, backup readiness, capacity, permissions, dependencies, workers, schedules, caches, and external side effects before release.
- Define health checks around the dependency level they claim. A process check, dependency check, and authenticated user flow prove different things.
- Emit logs, metrics, traces, or events that let an operator identify revision, environment, request or job, duration, outcome, and failure cause without exposing secrets.
- Tie alerts to an owner and an action. Do not create alerts that nobody can interpret or respond to.
- Define timeout, retry, backoff, rate, concurrency, resource, and cost limits for runtime work where unbounded behavior can cause failure.
- Give stateful systems tested backup and recovery procedures. Record recovery targets when the product has availability or data-loss commitments.
- Treat production writes, deployments, DNS changes, external messages, destructive operations, and paid services as separate authorities.

## Evidence

Choose checks that match the operational risk:

- build and artifact provenance;
- environment, dependency, permission, configuration-name, and capacity preflight without secret values;
- deployment dry run or equivalent safe rehearsal where available;
- migration, worker, scheduler, cache, and external-integration checks;
- revision, health, logs, metrics, and changed-flow verification after release;
- rollback or forward-repair evidence, including repeat execution and interrupted execution for fragile procedures;
- incident, restore, and alert-path exercises when the stated service level requires them.

Put exact environments, CI/CD behavior, commands, observability tools, on-call ownership, thresholds, and forbidden production actions in the relevant scoped `AGENTS.md` and release runbook.
