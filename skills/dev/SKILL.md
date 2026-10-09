---
name: dev
description: Coordinate reusable product design, outcome roadmaps, and one OpenSpec change at a time with Ponytail and evidence-based QA. Use for $dev setup, design, plan, work, verify, revise, finish, or status, including adoption of an existing development effort.
metadata:
  version: "1.0.4"
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
- Resolve exact skill names from the session catalog; read and apply their actual installed `SKILL.md` files according to the routing table below.
- Default Ponytail to full; honor explicit overrides, including disabling it.
- Load a skill once per agent context; reuse its instructions while available and unchanged.
- If instructions are unavailable or the installed version/content changes, reload the actual skill.
- Never substitute a remembered summary or hardcode a versioned cache path.
- A command requiring no additional Ponytail skill does not deactivate an already-active mode.
- Use native OpenSpec context/status/instructions for roots, stores, schemas, artifact graphs, and output paths; do not recreate its parser, schema, or templates.
- Set `OPENSPEC_TELEMETRY=0` on read-only discovery/status subprocesses to prevent first-run configuration writes.
- Missing OpenSpec still permits product design and diagnostic status.

## Command routing

- This table owns skill selection. Skill names are instructions to load and apply, not shell commands.
- Listed skills are required unless marked conditional or explicitly overridden by the user. Load conditional skills only when their condition applies.

| Command | Ponytail skills | OpenSpec skills / CLI | Reference |
| --- | --- | --- | --- |
| `setup` | No additional skill | Native CLI setup/discovery; no setup skill | [Setup](references/openspec-workflow.md#setup); [maintenance](references/maintenance.md) for dependency/install issues |
| `design` | `ponytail:ponytail` | Optional `openspec-explore` for unresolved exploration in an OpenSpec project | [Product planning](references/product-planning.md) |
| `plan` | `ponytail:ponytail` | `openspec-propose` | [Plan](references/openspec-workflow.md#plan) |
| `work` | `ponytail:ponytail`; `ponytail:ponytail-review` for code-change acceptance | `openspec-apply-change` | [Work](references/openspec-workflow.md#work); [engineering](references/engineering-and-verification.md) |
| `verify` | `ponytail:ponytail`; `ponytail:ponytail-review` when required code-review evidence is missing or stale | Read-only native CLI context/status/validation; no verification skill | [Engineering](references/engineering-and-verification.md) |
| `revise` | `ponytail:ponytail` | `openspec-update-change` for the selected change | [Revise](references/openspec-workflow.md#revise) |
| `revise --effort` | `ponytail:ponytail` | No required skill; do not revise dependent changes implicitly | [Product planning](references/product-planning.md) |
| `finish` | No additional skill; require current applicable review evidence or return to `verify` | `openspec-archive-change`, which invokes `openspec-sync-specs` synchronously when sync is needed | [Finish](references/openspec-workflow.md#finish) |
| `status` | No additional skill | Read-only native CLI discovery/status; no status skill | [Status](references/commands.md#status) |

- For optional exploration, follow [OpenSpec skill boundaries](references/openspec-workflow.md#skill-boundaries); return to the selected command for its outputs.
- Use [engineering](references/engineering-and-verification.md#ponytail-integration) for review freshness and conditional Ponytail audit/debt/help/gain usage.

## Handoff

- Report the selected effort/change and observed state: planning, implementation pending verification, verified, blocked, or archived.
- Include exact artifact paths, concise evidence/blockers, and one copyable next command.
- Do not treat archival alone as verified delivery, invent completion percentages, or maintain another task database.
- Consult [architecture](references/architecture.md) for layout, ownership, and diagrams.
