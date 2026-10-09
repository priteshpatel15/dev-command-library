# OpenSpec integration

This is an adapter to installed OpenSpec skills, not a replacement manual. Discover and read the relevant installed skill and current CLI instructions. Native schema instructions own artifact structure; the command library adds engineering obligations, evidence assessment and roadmap handoffs.

## Skill boundaries

- Follow [command routing](../SKILL.md#command-routing) for exact skill selection; load and apply the actual installed instructions.
- Use `openspec-explore` only when exploration is requested or unresolved questions warrant it; routine discovery inside propose/update does not need a second skill.
- Keep exploration read-only unless artifact capture is explicitly authorized within the selected scope. It never implements code or initializes a root implicitly. Return to the selected command to produce its artifacts.
- Setup, status, and verify use native CLI capabilities; do not invent corresponding skill names. CLI validation is not implementation acceptance.
- Distinguish `openspec update` (CLI integration refresh) from `openspec-update-change` (revision of an existing change).

## Root, store and paths

Use native `openspec list --json` and `openspec context --json` to resolve a root before writes. Set `OPENSPEC_TELEMETRY=0` for read-only discovery/status subprocesses: the inspected CLI can otherwise create first-run analytics configuration. This process-local setting does not disable the product's required runtime telemetry. Read JSON even if an uninitialized-root response exits nonzero. If a selected/declared store cannot resolve, report its actual error and remedy; do not create a local root as a fallback. An explicit store remains selected on all native operations accepting `--store`.

Resolve the target code repository separately from the planning home. CLI-returned `planningHome`, `changeRoot`, `artifactPaths` and resolved instruction output paths are authoritative. Keep code/evidence references explicit about repository and path base. Do not assume custom schemas use default filenames or task syntax.

Use configured schema defaults. For default spec-driven, technical design is conditional according to native instructions. Spec deltas may be skipped only by its explicit supported no-behavior-change mechanism; don't omit them because a change seems small. Preserve existing capability path organization.

## Setup

Inspect CLI availability/version and root first. The verified baseline is OpenSpec 1.14.1 with `openspec init --tools codex`; check current help when capability/version differs. Initialization is authorized by `$dev setup`. Do not force-clean, reset a store, silently upgrade globally, or overwrite existing configuration.

Discover the explore, propose, apply-change, update-change, sync-specs and archive-change skills named in command routing. If a required skill is missing, use the installed CLI's supported integration generation/update path, inspecting its effects first. Keep generated skills vendor-owned. Add project-owned requirements to `AGENTS.md` and references in supported OpenSpec config fields. Preserve existing configuration and root declarations. Read relevant guidance fields through native instructions; do not mistake advisory prose for enforced code.

Design may run without OpenSpec. Plan/work/finish require the relevant native dependencies. Status can still report missing setup. If setup discovers a missing global dependency, give the precise installation requirement; do not install unrelated tooling as an implicit side effect.

## Plan

Load `openspec-propose`. Use `openspec new change <name>` for a new scaffold; never hand-author `.openspec.yaml` metadata. For an existing selected draft, use the native supported continuation path instead of duplicating it. Inspect relevant code/tests before producing artifacts.

Read status and each artifact's instructions in dependency order. Re-read completed dependency files from disk. Use templates returned by the CLI and native required/conditional/skipped rules. Preserve custom schemas; don't create unused stock files beside them. Record product/outcome links and target repository identity in an appropriate native artifact.

Get current native validation help and validate the produced change as applicable. CLI status is primarily artifact/task state, not proof of coherent behavior or implementation. Review coherence across requirements, technical approach and tasks. Present exact artifact paths and stop for review before implementation.

## Work

Load `openspec-apply-change`, get current native apply instructions and read its context files. Apply tasks with [engineering and verification](engineering-and-verification.md). Native `all_done` is the point to assess evidence, not a substitute for QA. Only check off an obligation when its actual criterion is met; use verification to retain detailed evidence instead of duplicating a second task list.

If an interrupted session has partial code or evidence, inspect it before continuing. If the change is unprepared, report its missing artifact and direct to plan. Material discoveries return to revise; ordinary defects stay in work.

## Revise

For a selected change, load `openspec-update-change` and use its current artifact-level scope and review interactions. `revise --effort` follows [product planning](product-planning.md) instead; report affected dependent changes without revising them implicitly. Do not use this adapter to bypass native limits on creating unstarted artifacts. Respect approved concrete revisions and existing user authorization; ask only for unresolved material choices or an explicit native confirmation not already supplied.

After authorized change-level revision, identify code/tasks/evidence that no longer match. Reopen affected tasks and mark relevant verification stale within that change. For effort-level revision, report these impacts for separately selected change revisions. A different intent may require a new change; preserve history rather than disguising a replacement.

## Finish

First apply the command library's stricter current-evidence gate. Incomplete or stale acceptance and unresolved material engineering findings are not waivable merely because native archive can retain unfinished work.

Load `openspec-archive-change`; it owns the inline `openspec-sync-specs` invocation when sync is needed. Reuse the native fetched specs-rule snapshot, wait for sync to finish, and verify every affected capability before moving the change. Do not launch background sync or add a duplicate pre-sync pass. Preserve unrelated requirements. If required sync is declined, conflicts, or fails, leave the change intact and report unfinished status.

Archive using native resolved paths and naming, avoiding doubled date prefixes or overwriting an existing archive. Move the complete directory, including `.openspec.yaml` and the library's `verification.md`. Update owned roadmap links and check source/evidence references. Report exactly one closed change, its archive, proof and next command. Never turn finish into automatic roadmap execution.

## Compatibility boundary

The library adds no custom schema, task parser, global active pointer or scheduler. `verification.md` is additional evidence stored beside native artifacts, with explicit target identity. A direct native archive outside `$dev` does not establish verified delivery; status inspects retained evidence and sync state honestly.
