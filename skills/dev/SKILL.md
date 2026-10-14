---
name: dev
description: Coordinate reusable product design, outcome roadmaps, and one small OpenSpec change at a time with Ponytail-first implementation and two-tier evidence-based QA. Use for $dev setup, design, plan, work, verify, revise, qualify, finish, or status, including adoption of an existing development effort.
metadata:
  version: "1.1.0"
---

# Development command library

## Purpose

- Use `$dev <operation>` (Codex) or `/dev <operation>` (Claude Code) in chat to guide design, planning, implementation, and acceptance.
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
- Keep every change inside the [size budget](references/commands.md#size-budget). `plan` slices larger outcomes; `work` on an oversized change stops and routes to `revise` or `plan` to split it.
- Apply Ponytail before code: write the [change map](references/engineering-and-verification.md#ponytail-integration) first, then implement the smallest complete change.
- Use two acceptance tiers: the change gate inside `work`, and the outcome gate once per roadmap outcome through `qualify`. See [acceptance tiers](references/engineering-and-verification.md#acceptance-tiers).
- Run long checks in the foreground with a timeout; never start a check in the background and poll it.
- Start `work` and `qualify` in a fresh session; planning artifacts and `verification.md` carry all needed state.
- Choose implementation/testing order freely; required acceptance must still pass.
- Stop design and plan at reviewable artifacts; start implementation on an explicit work request.
- Include required QA and corrective iteration in work; keep ordinary defects within work.
- If a discovery materially changes behavior or scope, return to revision.
- Keep status read-only. Limit verify to evidence updates. Limit finish to one change.
- Give delegates a short brief: scope, change map, diff, and the rules they need. Do not fork the whole conversation into a delegate.
- Assign concurrent contributors disjoint file ownership.
- Require explicit authorization for product commits, publication, deployment, production activation, messages, or starting another outcome.
- Honor existing authorization; do not request it again for routine work.
- Preserve native OpenSpec review interactions unless user instructions already resolve them.

## Load dependencies

- Load only the references and installed skills needed for the selected operation.
- Resolve required dependencies before changing files; report missing dependencies and stop dependent work.
- Resolve exact skill names from the session catalog; read and apply their actual installed `SKILL.md` files according to the routing table below.
- Load `ponytail:ponytail` once per session at full level unless the user overrides it. Load `ponytail:ponytail-review` only at the review step.
- Never open `ponytail-audit`, `ponytail-debt`, `ponytail-gain`, or `ponytail-help` unless the user invokes them by name.
- After context compaction, continue from the change map, tasks, and `verification.md`; re-read a reference only when a specific rule is needed. Do not reload every skill.
- Never substitute a remembered summary for a skill that has not been loaded in this session, and do not hardcode a versioned cache path.
- Use native OpenSpec context/status/instructions for roots, stores, schemas, artifact graphs, and output paths; do not recreate its parser, schema, or templates.
- Set `OPENSPEC_TELEMETRY=0` on read-only discovery/status subprocesses to prevent first-run configuration writes.
- Missing OpenSpec still permits product design and diagnostic status.

## Command routing

- This table owns skill selection. Skill names are instructions to load and apply, not shell commands.
- Listed skills are required unless marked conditional or explicitly overridden by the user.

| Command | Ponytail skills | OpenSpec skills / CLI | Reference |
| --- | --- | --- | --- |
| `setup` | No additional skill | Native CLI setup/discovery; no setup skill | [Setup](references/openspec-workflow.md#setup); [maintenance](references/maintenance.md) for dependency/install issues |
| `design` | `ponytail:ponytail` | Optional `openspec-explore` for unresolved exploration in an OpenSpec project | [Product planning](references/product-planning.md) |
| `plan` | `ponytail:ponytail` | `openspec-propose` | [Plan](references/openspec-workflow.md#plan) |
| `work` | `ponytail:ponytail` for the change map and implementation; `ponytail:ponytail-review` once at the end | `openspec-apply-change` | [Work](references/openspec-workflow.md#work); [engineering](references/engineering-and-verification.md) |
| `verify` | `ponytail:ponytail-review` only when the recorded review does not match the current diff | Read-only native CLI context/status/validation; no verification skill | [Engineering](references/engineering-and-verification.md) |
| `revise` | `ponytail:ponytail` | `openspec-update-change` for the selected change | [Revise](references/openspec-workflow.md#revise) |
| `revise --effort` | `ponytail:ponytail` | No required skill; do not revise dependent changes implicitly | [Product planning](references/product-planning.md) |
| `qualify` | No additional skill | Read-only native CLI status; no qualification skill | [Qualify](references/commands.md#qualify); [acceptance tiers](references/engineering-and-verification.md#acceptance-tiers) |
| `finish` | No additional skill; require a current change-tier review or return to `verify` | `openspec-archive-change`, which invokes `openspec-sync-specs` synchronously when sync is needed | [Finish](references/openspec-workflow.md#finish) |
| `status` | No additional skill | Read-only native CLI discovery/status; no status skill | [Status](references/commands.md#status) |

- For optional exploration, follow [OpenSpec skill boundaries](references/openspec-workflow.md#skill-boundaries); return to the selected command for its outputs.

## Model settings

- Recommended reasoning effort: `design`, `plan`, `revise`: high or xhigh. `work`, `verify`, `qualify`, `finish`: medium or high. Delegated reviewers: medium.
- `max` and `ultra` roughly triple wall time per step without changing what acceptance requires; reserve them for a genuinely hard design decision.
- Keep each `work` in its own session so requests stay small; a long-lived thread repeats compaction and re-reads.

## Handoff

- Report the selected effort/change and observed state: planning, implementation pending verification, verified, qualified, blocked, or archived.
- Include exact artifact paths, concise evidence/blockers, and one copyable next command.
- Do not treat archival alone as verified delivery, invent completion percentages, or maintain another task database.
- Consult [architecture](references/architecture.md) for layout, ownership, and diagrams.
