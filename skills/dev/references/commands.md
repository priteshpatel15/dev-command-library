# Command reference

- Enter commands in Codex or Claude Code chat; arguments are natural language, not shell syntax.
- `<value>` means required input; `[value]` means optional input. Omit the brackets when typing.
- Follow [SKILL.md](../SKILL.md) for target selection, shared rules, dependency loading, and handoffs.

| Command | Purpose |
| --- | --- |
| `$dev setup` | Prepare or repair project integration |
| `$dev design <goal or source>` | Design a product/improvement or adopt existing work |
| `$dev plan [outcome or request]` | Prepare one small change for review |
| `$dev work [change]` | Implement or resume one change through its change gate |
| `$dev verify [change]` | Assess change-tier acceptance and refresh evidence |
| `$dev revise <feedback>` | Revise the selected change plan |
| `$dev revise --effort <id> <feedback>` | Revise product design and roadmap |
| `$dev qualify <effort>/<outcome>` | Run the outcome gate once for a finished outcome |
| `$dev finish [change]` | Close one verified change |
| `$dev status` | Report state, blockers, and next command |

## Selection and shared inputs

- Read current project instructions and artifacts from disk.
- Bare `$dev` shows read-only status and the command card; unknown operations show the card without writes.
- For bare plan, select only an unambiguous ready outcome or next slice; ask if several qualify.
- Preserve an explicitly selected OpenSpec store throughout native operations; identify the code repository separately.
- Reuse compatible existing artifacts when repeating a command; do not create duplicate changes.
- Treat task checkboxes as progress, not acceptance evidence.

## Size budget

One change must fit all of these; otherwise slice it.

- At most 8 tasks.
- At most 2 owning modules or apps (for example one backend owner and one UI app).
- At most 10 requirement/scenario IDs in its change gate.
- Implementable, including its change gate, in one session.

Slicing:

- `plan` records the slice list in the roadmap outcome row as `<outcome>/<slice-n>` with a one-line result each, then plans only the first unplanned slice as one native change.
- Each slice is a complete, testable step, normally one owner contract end to end (domain → application → adapter → UI), not a layer.
- `work` checks the budget first; if the selected change exceeds it, stop and report `$dev revise <change> "split per size budget"`.

## Setup

**Purpose:** Prepare project instructions and OpenSpec integration.

**Inputs**
- Discover repository rules, installed dependencies, architecture, test/UI/DB tooling, telemetry, and evidence locations.

**Actions**
- Follow [OpenSpec setup](openspec-workflow.md#setup).
- Initialize missing OpenSpec integration through the installed CLI; preserve existing schemas and configuration.
- Merge a bounded workflow section into root `AGENTS.md`; preserve existing and nested instructions.
- Record concrete project boundaries and the two gate commands (change gate, outcome gate), or link their canonical runbook.
- Reference project rules from supported OpenSpec context/artifact/operation guidance; that prose is advisory, not executable enforcement.
- Use native integration generation/update for missing workflows; keep generated skills vendor-owned.

**Writes**
- `AGENTS.md`, bounded OpenSpec configuration, and required CLI-generated integration files.
- Ignore rules only when creating an owned raw-output location.
- No product documents/code, tool upgrades, destructive resets, schema replacement, or live-system access.

**Stop / next**
- Ready: report integration status and the next command for the observed project state.
- Blocked: identify the missing dependency/configuration conflict and remedy.
- Do not claim product acceptance from setup.

**Example:** `$dev setup`

## Design

**Purpose:** Define the intended experience and outcome roadmap, or adopt existing work.

**Inputs**
- User goal, source documents, or selected effort; discover governing rules and relevant implementation.

**Actions**
- Follow [product planning](product-planning.md); OpenSpec initialization is not required.
- Resolve material ambiguity with the user; record minor proposed defaults.
- Reuse suitable canonical documents and preserve accepted requirements.
- Classify existing work using evidence.
- Name each outcome's outcome gate (the project command or scenario set that proves the whole outcome).

**Writes**
- Normally `docs/development/<effort-id>/design.md` and `roadmap.md`, or their selected equivalents.
- Link diagrams/wireframes when useful; no implementation changes.

**Stop / next**
- Present reviewable design/roadmap and unresolved material decisions.
- After review, use plan for one selected outcome; use setup first if OpenSpec is absent.

**Example:** `$dev design "Administrator invitations and secure member onboarding"`

## Plan

**Purpose:** Prepare exactly one change, within the [size budget](#size-budget), for review.

**Inputs**
- An `effort-id/outcome-id`, `effort-id/outcome-id/slice-n`, clear request, or sole ready outcome.
- Relevant product design, main capability specs, source, tests, and configuration.

**Actions**
- Resolve the native OpenSpec root; if absent, return setup without initializing implicitly.
- Apply the size budget: slice the outcome if needed and select the first unplanned slice.
- Follow [OpenSpec planning](openspec-workflow.md#plan) and native proposal/artifact instructions.
- Inspect implementation impact and include required implementation and change-gate tasks; do not add outcome-gate tasks to a slice.
- Record reuse, necessary additions, affected boundaries, and dependency direction in technical design or proposal/task notes when design is unnecessary.
- Name the change gate: the focused checks and the browser specs this change touches.
- Allow standalone fixes without inventing a product roadmap.

**Writes**
- CLI-created change metadata and schema-required artifacts: normally proposal, spec deltas, conditional design, and tasks.
- The owned roadmap slice list/link when applicable; no product-code changes or verification pass claims.

**Stop / next**
- Present artifacts for review; preserve the native proposal-to-apply review boundary.
- Start work only after an explicit request.

**Example:** `$dev plan onboarding/M01` or `$dev plan "Fix the expired-session redirect loop"`

## Work

**Purpose:** Implement or resume the selected change through its change gate and one review.

**Inputs**
- Prepared change, current code/tests, governing rules, upstream constraints, and prior evidence.

**Actions, in order**
1. Load the change, tasks, and native apply instructions. Check the [size budget](#size-budget); stop and route to revise if exceeded.
2. Write the change map (see [Ponytail integration](engineering-and-verification.md#ponytail-integration)) into `verification.md` before the first code edit.
3. Implement per the map with focused tests alongside; reuse existing components; keep the diff minimal and complete.
4. Run the change gate: the project's fast checks for touched areas, then the touched browser specs against a running stack when the change has UI. Use the project's fast path (single spec, reused stack/fixture) named in `AGENTS.md`.
5. On failure: fix, rerun only the failing check. After two identical failures, stop and diagnose before any further run. Never rerun a full harness to retest one scenario.
6. Review once: load `ponytail:ponytail-review`, review the diff against the change map and design, resolve required findings, rerun affected focused checks. At most one fix-and-recheck round. Request an independent reviewer only when project instructions require it for this change's boundaries; brief it with the diff and change map only.
7. Record evidence in `verification.md`: identity, checks table, review, gaps. Check tasks whose criteria are met.

**Writes**
- Scoped source/tests/configuration/migrations/docs, task progress, change-local `verification.md`, and harness-owned evidence.

**Stop / next**
- Passed: change gate and review pass; report finish as the next action.
- Blocked: identify the unresolved dependency or material decision; missing environments remain incomplete acceptance.

**Example:** `$dev work onboarding-invitations`

## Verify

**Purpose:** Assess current change-tier acceptance and refresh evidence.

**Inputs**
- Accepted requirements, actual implementation, existing evidence, and tested identity.

**Actions**
- Follow [engineering and verification](engineering-and-verification.md).
- Compare the recorded identity with the current one; rerun invalidated change-gate checks and the review only when the diff hash changed.
- Do not run the outcome gate; that belongs to `qualify`.

**Writes**
- `verification.md` and test-run evidence only.
- Safely isolated test-data mutations are permitted within authorized QA.
- Do not edit product code, tests, accepted requirements, expected-result snapshots, or task completion.

**Stop / next**
- Report actual coverage, review result, freshness, and exact gaps.
- Return defects or missing tests to work; report finish only when the change gate and review pass with no required gaps.

**Example:** `$dev verify onboarding-invitations`

## Revise

**Purpose:** Update selected planning artifacts in response to feedback.

**Inputs**
- Feedback and an explicit/unambiguous change; `--effort <id>` selects product-level revision.

**Actions**
- For an effort, follow [product planning](product-planning.md): preserve canonical authority and identify dependent changes needing revision.
- For a change, follow [OpenSpec revision](openspec-workflow.md#revise) and native artifact-level review interactions.
- For a split, keep the current change as the first slice and record the remaining slices in the roadmap for later `plan`.
- Route unstarted artifacts outside native update scope to plan.
- If intent changes, assess whether a new change is needed instead of repurposing the existing one.

**Writes**
- Authorized planning documents, evidence-validity notes, and reopening of affected tasks.
- No implementation or fabricated fresh evidence.

**Stop / next**
- Present a coherent revision for review.
- If only part is accepted, report remaining inconsistencies; do not declare readiness or continue implementation through them.

**Example:** `$dev revise onboarding-invitations "Keep existing invitation expiry behavior"`

**Effort example:** `$dev revise --effort onboarding "Defer bulk invitations"`

## Qualify

**Purpose:** Run the outcome gate once for an outcome whose changes are all finished.

**Inputs**
- The roadmap outcome, its finished/archived changes, and the outcome gate named in the roadmap or `AGENTS.md`.

**Actions**
- Confirm every slice of the outcome is finished; otherwise report the remaining slice and stop.
- Run the outcome gate once in the foreground with a timeout: the project's integrated harness, copied-database proof, full browser/accessibility matrix, and preservation assertions as the project defines them.
- Configure the run to report all failures, not the first.
- Do not edit product code or tests. Route each defect to `$dev plan "<defect>"` as a new small change; rerun qualify after those changes finish.

**Writes**
- `docs/development/<effort-id>/qualification/<outcome-id>.md` using the [outcome verification template](../assets/templates/outcome-verification.md), plus harness-owned evidence.
- The roadmap outcome row's delivery evidence link.

**Stop / next**
- Qualified: report the record path and the next ready outcome.
- Failed: list defects with receipts and one `$dev plan` command for the first.

**Example:** `$dev qualify operator-experience/W02`

## Finish

**Purpose:** Synchronize specifications and archive one verified change.

**Inputs**
- Current change-gate evidence, review result, task state, spec deltas, and optional roadmap association.

**Actions**
- Check the recorded identity against the current working tree; stale evidence routes to verify.
- Require the change gate and review to pass; checked tasks or native `all_done` are insufficient. The outcome gate is not required here.
- Block closure on failed, mandatory-skipped, missing, or stale evidence; route defects to work and evidence gaps to verify.
- Follow [OpenSpec finish](openspec-workflow.md#finish); verify required spec synchronization before archival.
- If required sync is declined or fails, leave the change active.
- Preserve native review interactions and existing authorization.
- Archive the whole change directory with metadata/evidence; update only owned roadmap links and check references resolve.
- If this was the outcome's last slice, report `$dev qualify <effort>/<outcome>` as the next command.

**Writes**
- Main capability specs, archive move, and owned roadmap links/delivery summary.

**Stop / next**
- Report exactly one closed change and its evidence.
- A finished change does not qualify the roadmap outcome; `qualify` does.
- Do not automatically start another outcome, commit product work, publish, deploy, activate production, or send messages.

**Example:** `$dev finish onboarding-invitations`

## Status

**Purpose:** Report observed state and the exact next action.

**Inputs**
- Current project/effort/change artifacts and evidence; dependencies may be missing.

**Actions**
- Inspect artifacts and evidence; diagnose missing OpenSpec/Ponytail without installing them.
- Derive state from evidence using the definitions below.
- When reporting whether a process is live, check retained terminal receipts or actual process state; an old `running` label is insufficient.
- Compare recorded and current identity before claiming evidence is current.

**Writes**
- None; do not create a tracking file.

**Stop / next**
- Report selected target, state, artifact locations, blockers, and one actionable next command.
- If initialized with no effort/change, suggest design, or plan when the request already defines a bounded change.
- If a concrete next stage exists, do not suggest status again.

**Example:** `$dev status`

### State definitions

| State | Evidence |
| --- | --- |
| Planning | Scope/artifacts incomplete or awaiting review |
| Implementation pending verification | Code/task progress exists without current change-gate evidence |
| Verified | Current change gate and review pass |
| Qualified | Outcome qualification record passes for every slice of the outcome |
| Blocked | A concrete prerequisite prevents the selected action; explain how to clear it |
| Archived | Native archive exists; separately assess verified delivery |

## Everyday sequences

- **New product:** setup → design → review → plan → review → work → finish, repeated per slice → qualify.
- **Existing effort:** design using existing documents/checklist/evidence → review adopted roadmap → plan the selected outcome's first slice → review → work.
- **Small fix:** plan the request → review → work → finish.
- **Returning session:** status → the suggested work, verify, or other concrete command.
- Report target, exact artifacts, evidence/limitations, and next command after every operation.
- Use existing commands for start/resume/next/review; do not add parallel workflow primitives.
