# Development command library

One reusable Codex skill for taking a development effort from product design through a verified OpenSpec change. Enter its commands in **Codex chat**, with the relevant project open.

```text
$dev setup
$dev design "Describe the product or improvement"
$dev plan <outcome-id>
$dev work <change-name>
$dev finish <change-name>
```

Review the design before planning a change, and review that change before requesting work. `work` includes implementation, required tests, UI/database QA, and corrective work. `finish` synchronizes specifications and archives an accepted change. It does not deploy or automatically start the next outcome.

## Everyday commands

| Command | Use it to |
|---|---|
| `$dev` | See the command card and current state. |
| `$dev setup` | Configure an existing or new project for this workflow. |
| `$dev design <goal or source>` | Create or adopt a product design and outcome roadmap. |
| `$dev plan [outcome or request]` | Prepare one bounded OpenSpec change. |
| `$dev work [change]` | Implement or resume that change and complete required QA. |
| `$dev verify [change]` | Review current acceptance and refresh evidence. |
| `$dev revise <feedback>` | Revise the selected change's planning artifacts. |
| `$dev revise --effort <id> "<feedback>"` | Revise product design and roadmap. |
| `$dev finish [change]` | Sync specifications and archive a verified change. |
| `$dev status` | Inspect state, evidence, blockers, and the exact next command. |

An explicit change name is useful when several changes exist. A sole compatible target or an unambiguous conversation reference can be selected without repeating it. Ambiguous targets require selection.

For a small independent bug, start with `$dev plan "Fix <observed problem>"`. A separate product roadmap is optional for a bounded direct request.

## Reference guide

| Document | Read it for |
|---|---|
| [Command reference](skills/dev/references/commands.md) | Exact inputs, outputs, examples, affected files, and stopping points. |
| [Architecture and artifact guide](skills/dev/references/architecture.md) | Diagrams, complete file layout, ownership, and how commands connect. |
| [Product planning](skills/dev/references/product-planning.md) | Design, journeys, roadmap outcomes, and adoption of existing work. |
| [OpenSpec integration](skills/dev/references/openspec-workflow.md) | Native workflows, change artifacts, schemas, stores, and archive behavior. |
| [Engineering and verification](skills/dev/references/engineering-and-verification.md) | Clean Architecture, SOLID, Ponytail, TDD, telemetry, copied databases, UI QA, and evidence. |
| [Installation and maintenance](skills/dev/references/maintenance.md) | Setup, validation, updates, rollback, removal, and troubleshooting. |
| [Implementation plan](docs/implementation-plan.md) | Approved construction decisions and the initial project handoff. |
| [Behavioral scenarios](tests/scenarios.md) | Reproducible library evaluations. |
| [Installation and validation evidence](tests/evidence/2026-10-09-installation-and-adoption.md) | Observed installation, fresh-session checks, project adoption, and acceptance limits. |

## Installation model

```text
/Users/po/codeandconfigs/dev-command-library/skills/dev
                           ↑
/Users/po/.agents/skills/dev  (one symbolic link)
```

The source repository owns the library. The global link makes the skill discoverable in other projects. Product code, design, OpenSpec changes, and test evidence remain in the selected project or its configured planning store.

Ponytail is loaded for design, planning, revision, work, and verification. It seeks the smallest complete solution while preserving accepted functionality, architecture, testing, telemetry, and accessibility requirements. The library uses the installed Ponytail and OpenSpec skills; it does not vendor their instructions or replace their tools.

Source edits are immediately visible through the global link. Validate updates before using them; see [maintenance](skills/dev/references/maintenance.md). Installation and test results belong in actual evaluation reports, not inferred from this README.
