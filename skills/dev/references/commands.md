# Command reference

These commands are messages to Codex. Angle brackets describe required input; square brackets describe optional input. They are not characters to type. Natural-language arguments are interpreted by the agent; there is no shell argument parser.

| Command | Use it when |
| --- | --- |
| `$dev setup` | Prepare a repository once, or diagnose/repair its integration |
| `$dev design <goal or source>` | Define a product/large enhancement or adopt an existing effort |
| `$dev plan [outcome or request]` | Prepare one change for review |
| `$dev work [change]` | Implement or resume it, including required QA |
| `$dev verify [change]` | Obtain a fresh acceptance review or refresh stale evidence |
| `$dev revise <feedback>` | Revise the selected change plan |
| `$dev revise --effort <id> <feedback>` | Revise product direction or roadmap |
| `$dev finish [change]` | Close a currently verified change |
| `$dev status` | See state, artifacts, blockers and the next command |

For an explicit change revision, name the change in the request, e.g. `$dev revise onboarding-invitations "Keep existing invitation expiry behavior"`. Bare `$dev` shows status and this card. Unknown commands do not mutate files.

## Selection and shared inputs

Read applicable project instructions and current artifacts from disk. An explicit repository or change takes precedence over a conversational reference; otherwise use the sole compatible target. Ask when multiple candidates fit. A bare plan selects the next unambiguous ready outcome, not an arbitrary item in a parallel-ready set. Do not use recency as selection. Respect an explicitly selected OpenSpec store throughout its native operations; record the target code repository separately.

Every mutating command reports the exact paths it created or updated. Do not overwrite unrelated dirty files or treat prior checked boxes as passing acceptance. Repeating a command should reuse its selected existing artifacts when compatible with the request. Do not silently create a second similarly named change.

## Setup

**Input:** working repository, existing instructions/configuration, OpenSpec/Ponytail installations, build/test/database/UI tooling.

Inspect before editing. Discover actual layers, test commands, existing architecture checks, harness output paths, database isolation guards, and telemetry conventions. If absent, initialize OpenSpec using the installed CLI's supported Codex integration. Setup explicitly authorizes project initialization, not a tool upgrade, destructive reset, schema replacement, or live-system access.

Create or merge a bounded development-workflow section in root `AGENTS.md`, preserving existing and nested instructions. Put project-specific boundaries and concrete commands there or link their canonical maintained runbook. Reference those rules from OpenSpec context/artifact/operation guidance; preserve the user's schema and configuration. Configuration guidance is advisory, not executable enforcement. Avoid rewriting CLI-generated skills; use the supported CLI integration mechanism if required skills are missing.

**Writes:** `AGENTS.md`, bounded OpenSpec configuration changes, CLI-generated integration files when needed; ignore rules only when creating an owned raw-output location. **Stop:** ready, or a concrete missing dependency/configuration conflict with its remedy. No product documents, code or acceptance claims.

## Design

**Input:** goal, source document(s), or selected existing effort; governing rules and relevant existing implementation.

Use [product planning](product-planning.md), with actual Ponytail loaded. Produce a complete intended experience and an outcome roadmap. Resolve material ambiguity interactively; record minor proposed defaults. Reuse canonical design documents when suitable. Preserve accepted requirements and classify existing work using evidence.

**Writes:** normally `docs/development/<effort-id>/design.md` and `roadmap.md`, or selected equivalents. Optional diagrams/wireframes are linked only when useful. **Stop:** reviewable design/roadmap with material open decisions stated. No implementation. Design works before OpenSpec initialization.

Example: `$dev design "Administrator invitations and secure member onboarding"`.

## Plan

**Input:** `effort-id/outcome-id`, a clear request, or the sole ready outcome; product design, main capability specs, relevant source/tests/configuration.

Resolve the OpenSpec root first. If uninitialized, direct the user to setup without implicitly initializing. Load Ponytail and the installed proposal skill; inspect actual impact before drafting. Create exactly one bounded change using native artifact instructions. Include implementation and required verification tasks. Record reusable components, necessary additions, affected boundaries and dependency direction in the technical design, or concise proposal/task notes when no technical design is warranted.

**Writes:** CLI-created change metadata and schema-required artifacts; a link on the owned roadmap row when applicable. Native spec-driven usually means proposal, spec deltas, conditional design and tasks. No custom verification pass yet. **Stop:** artifacts ready for review; no product-code edits. Preserve the native proposal-to-apply review boundary.

Example: `$dev plan onboarding/M01`. A direct request such as `$dev plan "Fix the expired-session redirect loop"` does not require inventing a product roadmap.

## Work

**Input:** selected prepared change, current code/tests, governing rules, upstream constraints and prior verification.

Load actual Ponytail and native apply instructions. Implement the accepted outcome using existing project components and complete required test coverage. Choose implementation/testing order to fit the change. Investigate all affected callers, tests, fixtures, configuration, exports and contracts. Keep concurrent ownership disjoint. Ordinary fixes remain inside this operation. A material discovery changing accepted scope/behavior requires revision before dependent implementation.

Run relevant automated checks and complete required integration, UI and copied-database acceptance. Inspect the actual UI experience, telemetry and effects. Fix defects and rerun invalidated checks until acceptance passes, or report the specific unresolved dependency. Do not repeat a failing broad run without investigating its cause. Record only checks actually run; a prior failing test run is not required.

**Writes:** scoped source/tests/config/migrations/docs, task completion, change-local `verification.md`, and harness-owned raw evidence. **Stop:** acceptance and engineering review pass, or a concrete blocker/material decision. Missing environments remain incomplete acceptance. This command is also resume.

Example: `$dev work onboarding-invitations`.

## Verify

**Input:** acceptance artifacts, actual implementation, existing evidence and its tested identities.

Load Ponytail. Check which previous results still apply, inspect changed paths and required review findings, and run missing or invalidated available checks. Follow [engineering and verification](engineering-and-verification.md). A separate review need not rerun unchanged valid evidence without reason.

**Writes:** `verification.md` and test-run evidence only. Safely isolated test-data mutations may be part of authorized QA. Do not edit product code, test implementation, accepted requirements, snapshots used as expected results, or task completion; missing tests and defects return to work. **Stop:** honest coverage, review and freshness result, with exact gaps and next command.

## Revise

**Input:** feedback plus an explicit/unambiguous change; `--effort <id>` explicitly selects product-level revision.

Load Ponytail. At product level, preserve accepted source authority and update the selected design/roadmap; identify dependent changes needing revision. At change level, use the native update skill's artifact instructions and review interactions. Changes to intent may require a new change rather than repurposing an existing one. Do not use update to invent unstarted artifacts outside its native scope; route to plan.

**Writes:** authorized affected planning documents, affected verification-validity notes, and reopening affected tasks. **Stop:** coherent revision ready for review. No code or fabricated fresh evidence. If only part of a proposed revision is accepted, report remaining inconsistency; do not mark the plan ready or continue implementation through it.

## Finish

**Input:** current acceptance evidence, resolved material engineering findings, task state, spec deltas and an optional roadmap association.

Confirm evidence matches the relevant current source/tests/configuration/fixtures/dependencies and accepted scope. All required acceptance and review obligations must pass; native task completion or `all_done` does not establish this. Do not close on failed, skipped mandatory, missing or stale evidence. Report work for defects or verify for evidence gaps.

Use native spec synchronization and archive workflows. If deltas require sync, verify the main specs reflect them before archiving. Required sync declined or failed leaves finish incomplete and the change unarchived. Honor applicable native review interactions without asking for already-resolved authorization. Move the whole native change directory and preserve its metadata/evidence. Update only its owned roadmap delivery links and confirm references still resolve.

**Writes:** main capability specs, archive move, owned roadmap links/delivery summary. **Stop:** exactly one change closed. No automatic next outcome, product commit, publication, deployment, production activation or messages. A partial contribution does not complete an entire roadmap outcome.

## Status

Read artifacts and evidence only. Missing OpenSpec/Ponytail can be diagnosed without installing anything. Present effort/change, state, artifact locations, blockers and one next command. Derive state rather than creating a tracking file:

For an initialized project with no effort/change, suggest `$dev design "<goal>"`, or `$dev plan "<bounded request>"` when the request already supplies a small change. Do not send the user back to status immediately after reporting status when a concrete next stage is available.

- **Planning:** proposed scope/artifacts incomplete or awaiting review.
- **Implementation pending verification:** code or task progress exists, but required current evidence does not.
- **Verified:** current acceptance and required reviews pass.
- **Blocked:** a concrete prerequisite prevents the selected next action; describe how it clears.
- **Archived:** native archive exists; separately state whether verified delivery is supported.

Do not interpret a historical `running` label as a live process. Use a retained terminal receipt or observed process state. Do not claim a code/test identity is unchanged without checking it.

## Everyday sequences

New product: `$dev setup` → `$dev design "goal"` → review → `$dev plan` → review → `$dev work` → `$dev finish`.

Existing effort: `$dev design docs/existing-design.md` (include its checklist/evidence) → review adopted roadmap → `$dev plan effort/W01` → review → `$dev work`.

Small fix: `$dev plan "request"` → review → `$dev work` → `$dev finish`.

Returning session: `$dev status` → suggested `$dev work <change>`, `$dev verify <change>`, or another concrete command.

After every operation, report selected target, exact artifacts, evidence/limitation and next command. No additional start/resume/next/approve primitives are necessary.
