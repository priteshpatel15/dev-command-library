# OpenSpec integration

## Purpose and authority

- Connect the selected `$dev` operation to native OpenSpec workflows using the selected outcome/change, linked design, project instructions, and current evidence.
- Let installed skills and CLI instructions own schemas, artifact structure, metadata, paths, and lifecycle mechanics.
- Apply the library's [engineering and verification requirements](engineering-and-verification.md) alongside native workflows.
- Store change-local `verification.md` beside native artifacts; add no custom schema, task parser, global project pointer, or scheduler.

## Skill boundaries

- Load and apply actual OpenSpec and Ponytail skills through [command routing](../SKILL.md#command-routing); keep skill selection there.
- Use `openspec-explore` for requested or necessary exploration; routine discovery inside propose/update needs no extra skill.
- Keep exploration read-only unless artifact capture is explicitly authorized; preserve its confirmed scope and return to the selected command for outputs.
- Exploration never implements code or initializes a root implicitly.
- Setup, verify, and status use native CLI capabilities; do not invent corresponding skills.
- Distinguish `openspec update` (integration refresh) from `openspec-update-change` (change revision).

## Root, store, and schema

- Inspect `openspec list --json` and `openspec context --json` before writes; read JSON even when an uninitialized-root response exits nonzero.
- A missing root requires explicit initialization authorization; `$dev setup` supplies it. Do not create a root implicitly during another operation.
- If a selected/declared store cannot resolve, report its error and remedy; never create a local root as fallback.
- Preserve the selected store on every native operation accepting `--store`.
- Resolve the code repository separately from the planning home; declare repository/path bases in code and evidence references.
- Use CLI-returned `planningHome`, `changeRoot`, `artifactPaths`, and concrete output paths. Never write to a glob pattern or assume default filenames/task syntax.
- Preserve configured schemas and capability path organization; native instructions determine required, conditional, and skipped artifacts.
- For default spec-driven, technical design is conditional; skip spec deltas only through the supported no-behavior-change mechanism.
- Set `OPENSPEC_TELEMETRY=0` for read-only discovery/status subprocesses to avoid first-run configuration writes; product telemetry remains required.
- Missing OpenSpec still permits product design and diagnostic status.

## Setup

- Inspect CLI version, root, configuration, and installed workflow availability before changes.
- Verified baseline: OpenSpec 1.14.1 and `openspec init --tools codex`; consult current help when capabilities/version differ.
- Initialize missing integration through the native CLI; repair required workflows through its supported generation/update path after inspecting effects.
- Keep generated skills vendor-owned. Put project requirements in `AGENTS.md` and references in supported OpenSpec configuration fields.
- Preserve existing instructions, configuration, root declarations, and schemas; do not reset stores, force-clean, or silently upgrade global tools.
- Apply relevant native context/guidance; treat it as instructions rather than executable enforcement.
- Report missing global dependencies and the precise remedy; do not install unrelated tooling implicitly.

## Plan

- Apply `openspec-propose` for one selected outcome slice or bounded request within the [size budget](commands.md#size-budget).
- If the outcome exceeds the budget, record its slices in the roadmap first; create one native change per slice, starting with the first unplanned slice.
- Create new metadata with `openspec new change <name>`; never hand-author `.openspec.yaml`.
- Resume an existing selected draft through native instructions instead of creating a duplicate.
- Read native context/rules and inspect relevant source, tests, and configuration before drafting.
- Follow the native artifact dependency order; reread completed dependency files from disk.
- Use native templates and artifact rules; do not add unused stock files to custom schemas.
- Link the product/outcome and target repository in an appropriate native artifact.
- Name the change gate in tasks; keep outcome-gate obligations out of slice tasks.
- Validate using current native help; review consistency among requirements, technical approach, and tasks.
- Present exact artifact paths and stop for review; start work only on an explicit request.

## Work

- Apply `openspec-apply-change`; read current apply instructions and their context files.
- Inspect partial implementation and retained evidence before resuming; a retained change map is the resume point.
- If required planning artifacts are missing, report them and direct to plan.
- Follow the ordered [work sequence](commands.md#work): size check, change map in `verification.md`, implementation, change gate, one review, evidence.
- Check off an obligation only when its actual criterion is met; retain detailed proof in verification rather than a second task list.
- Native `all_done` triggers evidence assessment; it does not establish acceptance.
- Keep ordinary defects within work; revise material scope/behavior changes before dependent implementation.

## Revise

- Apply `openspec-update-change` to the selected change using its native artifact scope and review interactions.
- Preserve native limits on unstarted/skipped artifacts and its supported confirmed additions to partially populated glob artifacts.
- Honor existing concrete authorization; ask only for unresolved material choices or native confirmations not already supplied.
- After change-level revision, reopen affected tasks and mark relevant evidence stale within that change.
- Keep implementation outside revision; preserve history when a different intent warrants a new change.
- Route `revise --effort` to [product planning](product-planning.md); report dependent-change impacts without editing those changes implicitly.

## Verify and status

- Use native read-only context/status/validation as appropriate; artifact/task state and CLI validation do not prove implementation acceptance.
- Follow the [verify contract](commands.md#verify): assess current acceptance, run applicable checks, and update only verification/test-run evidence. Preserve authorized isolated QA data scope.
- Send implementation defects or missing tests back to work; do not edit code, tests, accepted behavior, or task completion during verify.
- Follow the [status contract](commands.md#status): report observed state, missing dependencies, blockers, and one next command without writes.
- Assess retained evidence and sync state even after native archival; archival alone is not verified delivery.

## Finish

- Require a current passing change gate and recorded review before synchronization/archive; native permission to archive unfinished work does not satisfy this gate. The outcome gate belongs to `qualify`, not finish.
- Route defects to work and missing/stale evidence to verify.
- Apply `openspec-archive-change`; it owns the inline `openspec-sync-specs` invocation when sync is needed.
- Follow native lookup rules: archive guidance is optional; required specs instructions must succeed before main-spec writes.
- Reuse the fetched specs-rule snapshot, wait for synchronization, then verify every affected capability before moving the change.
- Do not launch background sync or add a duplicate pre-sync pass; preserve unrelated requirements.
- If required sync is declined, blocked, or fails, leave the change active and report unfinished status.
- Use native resolved archive paths/naming; do not double date prefixes or overwrite an existing archive.
- Move the complete directory, including `.openspec.yaml` and `verification.md`; update owned roadmap links and check evidence references resolve.
- Report one closed change, archive path, proof, and next command; after an outcome's last slice, the next command is `qualify`. Do not start another outcome automatically.
