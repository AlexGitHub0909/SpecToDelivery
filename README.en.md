# Build Project Zero to One

[简体中文](README.md)

This Codex skill turns a product brief or an existing repository into a project that can be planned, implemented, checked, and handed over without relying on chat history.

It is opinionated about project control: every managed project needs a current `PLAN.md`, a root `AGENTS.md`, and scoped `AGENTS.md` files where local engineering rules differ. It also keeps product intent separate from implementation evidence, so a written requirement never passes as finished code.

## Installation

You need Git and a Codex App, CLI, or IDE Extension version that supports Skills. Under the current [Codex directory convention](https://developers.openai.com/codex/concepts/customization), personal skills go in `$HOME/.agents/skills`, while project-shared skills go in `.agents/skills` inside the repository.

### Personal installation

A personal installation makes the skill available to all projects on the same machine.

macOS or Linux:

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/AlexGitHub0909/build-project-zero-to-one.git \
  "$HOME/.agents/skills/build-project-zero-to-one"
```

Windows PowerShell:

```powershell
$skillsDir = Join-Path $HOME ".agents\skills"
New-Item -ItemType Directory -Force -Path $skillsDir | Out-Null
git clone https://github.com/AlexGitHub0909/build-project-zero-to-one.git `
  (Join-Path $skillsDir "build-project-zero-to-one")
```

Update a personal installation:

```bash
git -C "$HOME/.agents/skills/build-project-zero-to-one" pull --ff-only
```

In PowerShell, use:

```powershell
git -C (Join-Path $HOME ".agents\skills\build-project-zero-to-one") pull --ff-only
```

### Project-shared installation

To use the skill only in one repository, place it under that project's `.agents/skills` directory. A Git submodule keeps its version and upstream updates explicit:

```bash
git submodule add https://github.com/AlexGitHub0909/build-project-zero-to-one.git .agents/skills/build-project-zero-to-one
git commit -m "chore: add project zero-to-one skill"
```

After cloning the project on another machine, run `git submodule update --init --recursive`. To move to a newer upstream version, run `git submodule update --remote .agents/skills/build-project-zero-to-one`, review the result, and commit the updated submodule pointer.

If the project does not use submodules, copy the skill into the same directory and commit it with the project, without retaining a nested `.git` directory.

Some older Codex versions use `~/.codex/skills`. If an existing installation is already detected, do not install a duplicate. For new installations, use `$HOME/.agents/skills` for personal use or `.agents/skills` inside a project. Codex normally detects skill changes automatically; restart Codex if the skill does not appear.

The repository is self-contained. It does not require an MCP server or a separate plugin.

## When to use it

Use `$build-project-zero-to-one` when you want Codex to:

- start a software project from a PRD, brief, or set of requirements;
- recover the state of an existing repository and continue the work;
- produce an implementation-ready spec and handoff without writing application code;
- add or repair project planning, document routing, traceability, test evidence, and release rules;
- implement the next vertical slice and update the repository facts as it goes.

The skill supports three modes:

| Mode | Use it for |
|---|---|
| `GREENFIELD` | A new project with product material but little or no code |
| `BROWNFIELD` | An existing repository that must be audited before changes |
| `SPEC_ONLY` | A specification and handoff package with no application-code changes |

## What it puts in a project

The supplied templates cover:

- project entry and local setup;
- root and scoped agent rules;
- current planning and change history;
- document routing and ownership;
- product scope and business flows;
- requirement-to-code traceability;
- test and release evidence;
- architecture decisions and rollback.

The default initializer creates the full governance baseline. Use it for a new project, or for an existing repository that has deliberately adopted this layout. Otherwise, adapt individual templates to the repository's canonical files instead of creating a second documentation system.

## Use it

Invoke the skill with the product material or repository in scope:

```text
Use $build-project-zero-to-one to audit this repository, recover the current plan, and implement the next verified product slice.
```

For a new project:

```text
Use $build-project-zero-to-one to turn this PRD into a greenfield project. Set up the plan, agent rules, specs, traceability, and the first working slice.
```

For a spec-only handoff:

```text
Use $build-project-zero-to-one in SPEC_ONLY mode. Produce the contracts, implementation slices, acceptance evidence, and release considerations without changing application code.
```

## Initialize the governance files

The initializer copies missing templates and leaves existing files alone:

```bash
python3 scripts/init_project.py /path/to/project \
  --name "Project name" \
  --mode greenfield \
  --scoped backend \
  --scoped frontend
```

Preview the changes first:

```bash
python3 scripts/init_project.py /path/to/project --name "Project name" --dry-run
```

Audit the result:

```bash
python3 scripts/audit_project.py /path/to/project
```

These scripts check the standard layout supplied by this skill. Do not use missing standard filenames as proof that an older repository lacks equivalent governance. Its own `AGENTS.md`, test standards, and release runbook still decide which stack-specific commands to run.

## Boundaries

The skill does not treat a test pass as proof of deployment. It does not turn product text into an implementation claim, and it does not write to production or external systems without clear authority.

Readiness is reported as `SPEC_READY`, `IMPLEMENTED_LOCAL`, `VERIFIED_LOCAL`, `RELEASE_READY`, `DEPLOYED_VERIFIED`, or `BLOCKED_EXTERNAL`.

## Skill layout

```text
build-project-zero-to-one/
├── SKILL.md
├── README.md          # Chinese, shown by default on GitHub
├── README.en.md       # English
├── agents/
├── references/
├── scripts/
└── assets/templates/project/
```

Codex follows `SKILL.md`. The two README files are for people who want to understand or maintain the skill.

Before publishing a fork, review the templates, replace repository-specific examples, and choose a license that fits how you want others to use the work.
