# Work-area discovery

## Purpose

Identify which engineering rules the project needs without forcing every project into the same architecture. Infer from product material and repository evidence before asking the user.

## Classification

Use `APPLIES`, `NOT_APPLICABLE`, `DEFERRED`, and `OPEN_DECISION` as defined in [fact-and-status-model.md](fact-and-status-model.md). These labels describe which rules the project needs, not implementation or release progress.

Do not add six empty rows to every plan. Record areas that apply, remain open, or could surprise the next contributor if omitted.

## Infer before asking

| Work area | Evidence that it may apply | Ask when the evidence is unclear |
|---|---|---|
| Website | Public pages, content discovery, campaigns, documentation, search traffic, public forms | Must people find or evaluate the product without signing in? |
| Frontend | Interactive screens, mobile or desktop clients, authenticated workspaces, rich form flows | Which user-facing interfaces must be built and on which devices? |
| Backend | Server-side rules, scheduled work, queues, private integrations, shared business behavior | Which behavior must run outside the user's device or browser? |
| API | Multiple clients, partner integrations, webhooks, automation, public or internal programmatic consumers | Which systems or clients need a stable programmatic contract? |
| Database | Durable business state, accounts, workflow history, reporting, search, audit, retention | What must persist, who owns it, and how long must it remain available? |
| Operations | Hosted environments, releases, domains, workers, scheduled jobs, monitoring, recovery ownership | Where will the project run, and who must release, observe, and recover it? |

These six areas are common, not exhaustive. Add a project-specific area for a library, CLI, data pipeline, model, embedded system, or another responsibility that has distinct rules. Do not force it into the nearest label.

An affirmative answer can activate more than one area. A public site with a signed-in workspace commonly needs both website and frontend rules. A backend does not automatically imply a separately managed API.

## Ask only what changes the project

1. Summarize what the available evidence already establishes.
2. Ask no more than three related questions at a time.
3. Use product language. Ask who uses a capability and what outcome they need before asking about tools.
4. Offer a recommendation when the project has no code and the user has not chosen an approach.
5. Stop asking once scope, ownership, hard-to-reverse choices, and acceptance evidence are clear enough for the current slice.

Example:

> The brief calls for public product pages and a signed-in workspace, so website and frontend rules apply. I do not see a confirmed external integration. Will partners or another client need a stable API in the first release?

Avoid sending a six-part questionnaire when the product material already answers most of it.

## Record and route

Record the result in `PLAN.md`, the product spec, or the repository's equivalent decision source. Include the evidence or user decision, owner, and any revisit condition.

Load a work-area reference when its status is `APPLIES`, or when the reference is needed to resolve an `OPEN_DECISION`. Do not load or generate rules for `NOT_APPLICABLE` areas. Keep `DEFERRED` areas out of the active implementation unless their future boundary changes the current architecture.

A work area is not a directory. Route confirmed rules into the smallest useful set of root or scoped `AGENTS.md` files after the repository structure is known.
