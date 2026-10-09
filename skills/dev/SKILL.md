---
name: dev
description: Coordinate reusable product design, outcome roadmaps, and one OpenSpec change at a time with Ponytail and evidence-based QA. Use for $dev setup, design, plan, work, verify, revise, finish, or status, including adoption of an existing development effort.
metadata:
  version: "1.0.3"
---

# Development command library

## Purpose

- Use `$dev <operation>` in Codex chat to guide design, planning, implementation, and acceptance.
- Read the selected operation in [commands](references/commands.md); these are chat instructions, not shell commands.

## Resolve the request

- Resolve the code repository from the request and working environment.
- Read applicable root and nested `AGENTS.md` instructions.
- Select the explicit target, unambiguous conversation target, or sole compatible effort/change.
- If multiple targets qualify, ask for selection; never choose by modification time or a global active-project pointer.
- If the command is bare `$dev`, report read-only status and the command card.
- If the operation is unknown, show the card without changing files.

## Shared rules

- Perform only the selected operation; preserve unrelated dirty work.
- Follow [engineering and verification](references/engineering-and-verification.md): accepted behavior, Clean Architecture, decoupling, SOLID, required tests, privacy-safe telemetry, and applicable QA.
- Use Ponytail to remove unnecessary work while preserving these obligations.
- Choose implementation/testing order freely; required acceptance must still pass.
- Stop design and plan at reviewable artifacts; start implementation on an explicit work request.
- Include required QA and corrective iteration in work; keep ordinary defects within work.
- If a discovery materially changes behavior or scope, return to revision.
- Keep status read-only.
- Limit verify to evidence updates.
- Limit finish to one change.
- Give delegates the same scope, governing rules, and artifacts; supply actual Ponytail instructions or require them to load the installed skill.
- Assign concurrent contributors disjoint file ownership.
- Require explicit authorization for product commits, publication, deployment, production activation, messages, or starting another outcome.
- Honor existing authorization; do not request it again for routine work.
- Preserve native OpenSpec review interactions unless user instructions already resolve them.

## Load dependencies

- Load only the references and installed skills needed for the selected operation.
- Resolve required dependencies before changing files; report missing dependencies and stop dependent work.
- For design, plan, revise, work, and verify, read the actual installed `ponytail:ponytail` skill from the session catalog unless explicitly disabled.
- Default Ponytail to full; honor explicit overrides, including disabling it.
- Load a skill once per agent context; reuse its instructions while available and unchanged.
- If instructions are unavailable or the installed version/content changes, reload the actual skill.
- Never substitute a remembered summary or hardcode a versioned cache path.
- Setup, status, and finish need not load Ponytail for dependency diagnosis or evidence inspection; engineering and completion rules still apply.
- Use native OpenSpec context/status/instructions for roots, stores, schemas, artifact graphs, and output paths; do not recreate its parser, schema, or templates.
- Set `OPENSPEC_TELEMETRY=0` on read-only discovery/status subprocesses to prevent first-run configuration writes.
- Missing OpenSpec still permits product design and diagnostic status.

## Command routing

| Command | Additional instructions | Result |
| --- | --- | --- |
| `setup` | [OpenSpec setup](references/openspec-workflow.md#setup); [maintenance](references/maintenance.md) for dependency/install issues | Project integration |
| `design` | [Product planning](references/product-planning.md) | Design and roadmap |
| `plan` | [OpenSpec integration](references/openspec-workflow.md); installed `openspec-propose` | Reviewable change |
| `work` | [Engineering](references/engineering-and-verification.md); installed `openspec-apply-change` | Implementation, QA, review, evidence |
| `verify` | [Engineering](references/engineering-and-verification.md) | Current acceptance report |
| `revise` | [Product planning](references/product-planning.md) for `--effort`; otherwise [OpenSpec integration](references/openspec-workflow.md) and installed `openspec-update-change` | Revised planning and invalidation notes |
| `finish` | [OpenSpec integration](references/openspec-workflow.md); installed `openspec-sync-specs` and `openspec-archive-change` as applicable | Verified sync and archive |
| `status` | [Status](references/commands.md#status) | Observed state and next command |

## Handoff

- Report the selected effort/change and observed state: planning, implementation pending verification, verified, blocked, or archived.
- Include exact artifact paths, concise evidence/blockers, and one copyable next command.
- Do not treat archival alone as verified delivery, invent completion percentages, or maintain another task database.
- Consult [architecture](references/architecture.md) for layout, ownership, and diagrams.
