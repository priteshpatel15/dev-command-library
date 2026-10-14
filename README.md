# Development command library

One global skill (Codex and Claude Code) for product design, outcome roadmaps, and delivery through one small OpenSpec change at a time.

## Start here

- Open the target project in Codex or Claude Code.
- Enter commands in **chat**, not a terminal (`$dev …` in Codex, `/dev …` in Claude Code).
- Use `$dev status` to resume an existing effort.
- For a new effort, run the commands below individually. Replace placeholders with your goal, outcome, and change name.

```text
$dev setup
$dev design "Describe the product or improvement"
$dev plan <outcome-id>            # slices a large outcome; plans the first slice
$dev work <change-name>           # one slice: change map → code → change gate → one review
$dev finish <change-name>         # repeat plan/work/finish per slice
$dev qualify <effort>/<outcome>   # full outcome gate, once, after the last slice
```

- Use `setup` when project integration is missing or needs repair.
- Review the design/roadmap before `plan`; review the change before `work`.
- `work` writes a Ponytail change map before any code, implements the smallest complete change, runs the change gate (focused checks plus the browser specs it touches), and reviews once.
- `qualify` runs the project's full harness (copied database, whole browser/accessibility matrix) once per outcome; its defects become new small changes.
- `verify` is available for a separate evidence review; it is optional when acceptance is already current.
- `finish` synchronizes specs when needed and archives one verified change.
- Select each next operation manually. These commands do not automatically advance, commit product work, or deploy.

## Keep it fast

- Keep every change inside the size budget (≤ 8 tasks, ≤ 2 owning modules/apps, ≤ 10 scenario IDs, one session). Oversized changes are the main cause of multi-hour runs.
- Start each `work` in a fresh session; long threads compact repeatedly and re-read everything.
- Reasoning effort: high/xhigh for design and plan; medium/high for work, verify, qualify, finish. `max`/`ultra` roughly triples wall time.
- Iterate on the single failing check against a running stack; run the full harness once, in the foreground, reporting all failures.

## Everyday commands

| Command | Use it to |
|---|---|
| `$dev` | See the command card and current state. |
| `$dev setup` | Configure an existing or new project for this workflow. |
| `$dev design <goal or source>` | Create or adopt a product design and outcome roadmap. |
| `$dev plan [outcome or request]` | Prepare one small OpenSpec change (slicing a large outcome). |
| `$dev work [change]` | Implement or resume that change through its change gate and one review. |
| `$dev verify [change]` | Assess change-gate acceptance and refresh evidence without editing implementation. |
| `$dev revise <feedback>` | Revise the selected change's planning artifacts. |
| `$dev revise --effort <id> "<feedback>"` | Revise product design and roadmap. |
| `$dev qualify <effort>/<outcome>` | Run the outcome gate once for a finished outcome. |
| `$dev finish [change]` | Sync specifications and archive a verified change. |
| `$dev status` | Inspect state, evidence, blockers, and the exact next command. |

- `<value>` is required; `[value]` is optional. Omit the brackets when typing.
- Name the target when several changes or efforts qualify; an unambiguous existing target can be inferred.
- Adopt existing work with `$dev design <existing-document-or-checklist>`.
- For a bounded bug, use `$dev plan "Fix <observed problem>"`; a separate product roadmap is optional.

## Artifacts and governing rules

- Product design and roadmap: normally `docs/development/<effort-id>/`; reuse suitable canonical documents.
- Change plans, tasks, and `verification.md`: the native OpenSpec change location in the project or selected planning store.
- Outcome qualification records: `docs/development/<effort-id>/qualification/<outcome-id>.md`.
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
                           ↑                ↑
/Users/po/.agents/skills/dev       /Users/po/.claude/skills/dev
        (Codex)                         (Claude Code)
```

- The source repository owns the library; one global link per agent exposes it across projects. Claude Code also needs the Ponytail plugin and per-project links to the OpenSpec skills (see [maintenance](skills/dev/references/maintenance.md#first-installation)).
- Validate candidate updates before editing the linked source; changes become globally visible immediately.
- Reload changed instructions or start a fresh session after updates.
- Follow [maintenance](skills/dev/references/maintenance.md) for installation, validation, updates, and recovery.
