# Capability routing

Use this reference when a task may need a specialized Skill, plugin, connector, external service, or artifact tool beyond the repository's existing commands.

## Start with the need

State the result that the project needs before naming a tool. Examples include checking a real browser flow, producing a PDF, reading current vendor documentation, editing a design file, publishing a release, or writing to a collaboration system.

Do not add a capability because it is available. Add it when it closes a confirmed requirement, supplies required evidence, or materially reduces a known delivery risk.

## Classify the capability

| Class | Meaning | Project treatment |
|---|---|---|
| Existing project capability | A command, dependency, script, or service already approved by the repository | Use it under the nearest `AGENTS.md` rules |
| Optional specialist capability | Improves speed or quality but is not required for acceptance | Use it when available; keep a normal fallback |
| Required delivery capability | Acceptance cannot be proved or completed without it | Record availability, authority, owner, and fallback or blocker in `PLAN.md` |
| Project-specific integration | Depends on organization data, credentials, private systems, or provider contracts | Keep its rules in project documents, not in the reusable Skill |

## Choose and use a capability

1. Read the root and scoped `AGENTS.md`, `PLAN.md`, and routed contracts.
2. Check the repository's existing commands, dependencies, scripts, and approved services first.
3. Inspect only the available Skills or plugins relevant to the confirmed need.
4. Read their instructions before use. Check required files, runtime, version, permissions, cost, network access, and external side effects.
5. Choose the least privileged option that can produce the required result and evidence.
6. Record the choice when it affects delivery, permissions, acceptance, or fallback.
7. Run the capability within the user's authority and keep its output subject to the project's own validation rules.
8. Capture evidence from the resulting artifact or system state. The fact that a tool ran is not proof that the result is correct.

## Record material decisions

Use the optional capability table in `PLAN.md` for decisions that matter:

| Need | Selected capability or tool | Required or optional | Availability and authority | Fallback or blocker |
|---|---|---|---|---|

Omit routine editor, shell, search, and repository commands unless they carry unusual permissions or are part of the acceptance evidence.

## Keep the public Skill portable

- Write rules in terms of capabilities and outcomes, not a catalog of product names.
- Do not force a programming language, framework, hosting provider, or vendor tool.
- Keep organization-specific connectors, credentials, account names, internal URLs, and production procedures in the project repository.
- Prefer installing or linking to a third-party Skill or plugin from its source. If the project vendors or adapts it, check the license, retain required notices, record the source and version, and keep local changes clear.
- Do not describe an optional capability as installed, current, or supported without checking the active environment.
- Do not silently install a Skill or plugin, create an account, accept a license, enable a connector, or grant access.
- Do not let a tool's defaults override repository rules, approved product behavior, privacy constraints, or user instructions.

## Adapt to the runtime

Inspect the active agent and environment before relying on a capability. Do not infer support from the product name alone; versions, permissions, sandboxes, and organization policy can change what is available.

Runtime adaptation changes the execution path, not the requested result or acceptance standard. Use an equivalent method when one exists. If required evidence cannot be produced, keep the task manual or blocked instead of accepting a weaker result.

| Capability | Preferred path | Fallback when unavailable |
|---|---|---|
| Repository read and write | Work directly in the approved project scope | Produce a patch or specification and mark application `MANUAL_REQUIRED` |
| Shell and project commands | Run the repository's documented checks | Provide exact commands for an authorized operator and leave results unverified |
| Python 3 | Run this Skill's standard-library helpers by their resolved installation path | Create or audit the same files directly; do not claim the helper audit ran |
| Browser or network | Verify the relevant current page, documentation, or flow | Use local tests or artifacts and mark live behavior `MANUAL_REQUIRED` or `BLOCKED_EXTERNAL` |
| Skills, plugins, MCP, or connectors | Load only the capability needed for the confirmed outcome | Use repository-native tools or a documented manual path |
| Subagents or parallel workers | Delegate independent, bounded work when useful | Perform the same work sequentially in the current agent |
| External write or deployment | Act only with explicit authority and fresh preflight evidence | Prepare the change or runbook without performing the external action |

Platform-specific metadata, slash commands, plan modes, and custom-agent formats are adapters. Keep the reusable workflow in `SKILL.md`, references, templates, and scripts so their absence does not disable the Skill.

## Use a fallback deliberately

An optional capability must not block the project. Use an existing repository command, a simpler local method, or a clearly marked manual check.

If a required capability is missing, choose one of these outcomes:

- request the minimum permission or input needed;
- use an approved substitute and record the evidence difference;
- mark the task `BLOCKED_EXTERNAL` with an owner and next action;
- narrow the readiness claim to the level supported by current evidence.

Never replace missing runtime, browser, deployment, or external-system evidence with a confident written claim.
