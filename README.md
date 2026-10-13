# Development command library

One global Codex skill for product design, outcome roadmaps, and delivery through one OpenSpec change at a time.

## Start here

- Open the target project in Codex.
- Enter commands in **Codex chat**, not a terminal.
- Use `$dev status` to resume an existing effort.
- For a new effort, run the commands below individually. Replace placeholders with your goal, outcome, and change name.

```text
$dev setup
$dev design "Describe the product or improvement"
$dev plan <outcome-id>
$dev work <change-name>
$dev finish <change-name>
```

- Use `setup` when project integration is missing or needs repair.
- Review the design/roadmap before `plan`; review the change before `work`.
- `work` includes implementation, required tests, applicable UI/copied-database QA, review, and fixes.
- `verify` is available for a separate evidence review; it is optional when acceptance is already current.
- `finish` synchronizes specs when needed and archives one verified change.
- Select each next operation manually. These commands do not automatically advance, commit product work, or deploy.

## Everyday commands

| Command | Use it to |
|---|---|
| `$dev` | See the command card and current state. |
| `$dev setup` | Configure an existing or new project for this workflow. |
| `$dev design <goal or source>` | Create or adopt a product design and outcome roadmap. |
| `$dev plan [outcome or request]` | Prepare one bounded OpenSpec change. |
| `$dev work [change]` | Implement or resume that change and complete required QA. |
| `$dev verify [change]` | Assess acceptance and refresh evidence without editing implementation. |
| `$dev revise <feedback>` | Revise the selected change's planning artifacts. |
| `$dev revise --effort <id> "<feedback>"` | Revise product design and roadmap. |
| `$dev finish [change]` | Sync specifications and archive a verified change. |
| `$dev status` | Inspect state, evidence, blockers, and the exact next command. |

- `<value>` is required; `[value]` is optional. Omit the brackets when typing.
- Name the target when several changes or efforts qualify; an unambiguous existing target can be inferred.
- Adopt existing work with `$dev design <existing-document-or-checklist>`.
- For a bounded bug, use `$dev plan "Fix <observed problem>"`; a separate product roadmap is optional.

## Artifacts and governing rules

- Product design and roadmap: normally `docs/development/<effort-id>/`; reuse suitable canonical documents.
- Change plans, tasks, and `verification.md`: the native OpenSpec change location in the project or selected planning store.
- Code, tests, and QA output: existing project locations. See the [artifact ownership table](skills/dev/references/architecture.md#project-artifacts-and-ownership).
- Clean Architecture governs module boundaries and dependencies; decoupling governs reusable components; SOLID governs responsibilities and interfaces within them.
- Load actual installed Ponytail and OpenSpec skills through the [command routing table](skills/dev/SKILL.md#command-routing). Provider instructions stay with their installed skills.
- Current acceptance evidence and resolved required findings govern completion. Task checkboxes and archival alone do not prove delivery.

## Reference guide

| Document | Read it for |
|---|---|
| [Command reference](skills/dev/references/commands.md) | Exact inputs, outputs, examples, affected files, and stopping points. |
| [Architecture and artifact guide](skills/dev/references/architecture.md) | Diagrams, complete file layout, ownership, and how commands connect. |
| [Product planning](skills/dev/references/product-planning.md) | Design, journeys, roadmap outcomes, and adoption of existing work. |
| [OpenSpec integration](skills/dev/references/openspec-workflow.md) | Native workflows, change artifacts, schemas, stores, and archive behavior. |
| [Engineering and verification](skills/dev/references/engineering-and-verification.md) | Clean Architecture, SOLID, Ponytail, testing, telemetry, copied databases, UI QA, and evidence. |
| [Installation and maintenance](skills/dev/references/maintenance.md) | Setup, validation, updates, rollback, removal, and troubleshooting. |
| [Implementation plan](docs/implementation-plan.md) | Historical approved construction decisions and initial project handoff. |
| [Behavioral scenarios](tests/scenarios.md) | Reproducible library evaluations. |
| [Evaluation records](tests/evidence/) | Observed results, tested versions, and limitations; older reports remain historical. |

## Installation model

```text
/Users/po/codeandconfigs/dev-command-library/skills/dev
                           ↑
/Users/po/.agents/skills/dev  (one symbolic link)
```

- The source repository owns the library; one global link exposes it across projects.
- Validate candidate updates before editing the linked source; changes become globally visible immediately.
- Reload changed instructions or start a fresh session after updates.
- Follow [maintenance](skills/dev/references/maintenance.md) for installation, validation, updates, and recovery.
