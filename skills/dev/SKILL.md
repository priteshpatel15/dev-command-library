---
name: dev
description: Coordinate reusable product design, outcome roadmaps, and one OpenSpec change at a time with Ponytail and evidence-based QA. Use for $dev setup, design, plan, work, verify, revise, finish, or status, including adoption of an existing development effort.
metadata:
  version: "1.0.0"
---

# Development command library

`$dev <operation>` is a Codex instruction, not a shell executable. Read the selected operation in [commands](references/commands.md). Bare `$dev` means read-only status plus the command card. An unknown operation shows the card without making changes.

## Shared entry

1. Resolve the target code repository from the working environment and request. Read applicable `AGENTS.md` instructions. Respect dirty work and nested instructions. Resolve the effort/change from an explicit target, an unambiguous current conversation reference, or the sole compatible candidate. If several qualify, ask for a short selection; never choose by modification time or a global active-project pointer.
2. For **design, plan, revise, work, and verify**, resolve and read the actual installed `ponytail:ponytail` skill using the session skill catalog. Use full by default, honoring explicit user overrides, including disabling it. Reuse an unchanged skill already read in this session. If it is required but unavailable, report the missing dependency and stop dependent work; a slogan or this document is not a substitute. Do not hardcode a versioned plugin-cache path.
3. Read the relevant parts of [engineering and verification](references/engineering-and-verification.md). Preserve accepted behavior, Clean Architecture, decoupling, SOLID, test-first development, privacy-safe telemetry, and full applicable acceptance. Ponytail reduces unnecessary work, not these obligations. Pass the resolved scope, actual Ponytail instructions, governing rules and relevant artifacts to delegates; give concurrent contributors disjoint file ownership.
4. Load only the references and installed skills needed below. Resolve dependencies before changing files. Use native OpenSpec context/status/instructions for its root, store, schema, artifact graph and output paths. For read-only discovery/status, set `OPENSPEC_TELEMETRY=0` on those subprocesses so first-run analytics metadata does not mutate configuration. Do not recreate its parser, schema or templates. [OpenSpec integration](references/openspec-workflow.md) defines the adapter.
5. Execute only the selected operation. Work includes required QA and corrective iteration. Design/plan stop for review; a later explicit work request starts implementation. Status is read-only; verify writes evidence only. Finish closes one change. Material behavior/scope changes return to revision; ordinary defects remain within work.

## Routing

| Operation | Additional reference / installed skill | Result |
| --- | --- | --- |
| `setup` | [OpenSpec integration](references/openspec-workflow.md#setup); [maintenance](references/maintenance.md) for dependency/install issues | Project instructions and OpenSpec integration |
| `design` | [Product planning](references/product-planning.md) | Product design and outcome roadmap |
| `plan` | [OpenSpec integration](references/openspec-workflow.md); installed `openspec-propose` | One reviewable change |
| `work` | [Engineering and verification](references/engineering-and-verification.md); installed `openspec-apply-change` | Implementation, required QA, review and evidence |
| `verify` | [Engineering and verification](references/engineering-and-verification.md) | Current acceptance report; no product-code edits |
| `revise` | [Product planning](references/product-planning.md) for `--effort`; otherwise installed `openspec-update-change` and [OpenSpec integration](references/openspec-workflow.md) | Coherent revised planning and invalidation notes |
| `finish` | [OpenSpec integration](references/openspec-workflow.md); installed `openspec-sync-specs` and `openspec-archive-change` as applicable | Verified synchronization and archive |
| `status` | [Commands](references/commands.md#status) | Observed state and exact next command |

`setup`, `status`, and `finish` need not load Ponytail merely to diagnose dependencies or inspect retained evidence. They still follow the applicable engineering and completion rules. Missing OpenSpec does not prevent product design or reporting a diagnostic status.

## Handoff

End with the selected effort/change, derived state, exact artifact paths written or inspected, concise evidence/blocker, and one copyable next command. Distinguish planning, implementation pending verification, verified, blocked, and archived; archival alone is not verified delivery. Do not invent completion percentages or maintain another task database.

Never automatically commit product work, publish, deploy, activate production, send messages, or start a later outcome. Honor existing explicit authorization; do not add a permission ritual for routine work. Preserve native OpenSpec review interactions where not already resolved by user instructions.

For the full layout, ownership and diagrams, see [architecture](references/architecture.md). For examples and public command contracts, see [commands](references/commands.md).
