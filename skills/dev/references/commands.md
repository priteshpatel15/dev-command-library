# Command reference

- Enter commands in Codex chat; arguments are natural language, not shell syntax.
- `<value>` means required input; `[value]` means optional input. Omit the brackets when typing.
- Follow [SKILL.md](../SKILL.md) for target selection, shared rules, dependency loading, and handoffs.

| Command | Purpose |
| --- | --- |
| `$dev setup` | Prepare or repair project integration |
| `$dev design <goal or source>` | Design a product/improvement or adopt existing work |
| `$dev plan [outcome or request]` | Prepare one change for review |
| `$dev work [change]` | Implement or resume, including QA |
| `$dev verify [change]` | Assess acceptance and refresh evidence |
| `$dev revise <feedback>` | Revise the selected change plan |
| `$dev revise --effort <id> <feedback>` | Revise product design and roadmap |
| `$dev finish [change]` | Close one verified change |
| `$dev status` | Report state, blockers, and next command |

## Selection and shared inputs

- Read current project instructions and artifacts from disk.
- Bare `$dev` shows read-only status and the command card; unknown operations show the card without writes.
- For bare plan, select only an unambiguous ready outcome; ask if several qualify.
- Preserve an explicitly selected OpenSpec store throughout native operations; identify the code repository separately.
- Reuse compatible existing artifacts when repeating a command; do not create duplicate changes.
- Treat task checkboxes as progress, not acceptance evidence.

## Setup

**Purpose:** Prepare project instructions and OpenSpec integration.

**Inputs**
- Discover repository rules, installed dependencies, architecture, test/UI/DB tooling, telemetry, and evidence locations.

**Actions**
- Follow [OpenSpec setup](openspec-workflow.md#setup).
- Initialize missing OpenSpec integration through the installed CLI; preserve existing schemas and configuration.
- Merge a bounded workflow section into root `AGENTS.md`; preserve existing and nested instructions.
- Record concrete project boundaries and commands, or link their canonical runbook.
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

**Writes**
- Normally `docs/development/<effort-id>/design.md` and `roadmap.md`, or their selected equivalents.
- Link diagrams/wireframes when useful; no implementation changes.

**Stop / next**
- Present reviewable design/roadmap and unresolved material decisions.
- After review, use plan for one selected outcome; use setup first if OpenSpec is absent.

**Example:** `$dev design "Administrator invitations and secure member onboarding"`

## Plan

**Purpose:** Prepare exactly one bounded OpenSpec change for review.

**Inputs**
- An `effort-id/outcome-id`, clear request, or sole ready outcome.
- Relevant product design, main capability specs, source, tests, and configuration.

**Actions**
- Resolve the native OpenSpec root; if absent, return setup without initializing implicitly.
- Follow [OpenSpec planning](openspec-workflow.md#plan) and native proposal/artifact instructions.
- Inspect implementation impact and include required implementation and verification tasks.
- Record reuse, necessary additions, affected boundaries, and dependency direction in technical design or proposal/task notes when design is unnecessary.
- Allow standalone fixes without inventing a product roadmap.

**Writes**
- CLI-created change metadata and schema-required artifacts: normally proposal, spec deltas, conditional design, and tasks.
- The owned roadmap link when applicable; no product-code changes or verification pass claims.

**Stop / next**
- Present artifacts for review; preserve the native proposal-to-apply review boundary.
- Start work only after an explicit request.

**Example:** `$dev plan onboarding/M01` or `$dev plan "Fix the expired-session redirect loop"`

## Work

**Purpose:** Implement or resume the selected change through required QA and review.

**Inputs**
- Prepared change, current code/tests, governing rules, upstream constraints, and prior evidence.

**Actions**
- Follow native apply instructions and [engineering and verification](engineering-and-verification.md).
- Inspect affected callers, tests, fixtures, configuration, exports, and contracts; reuse existing components.
- Choose implementation/testing order freely; a prior failing test run is not required.
- Complete required automated, integration, UI, and copied-database acceptance; inspect rendered experience, telemetry, and effects.
- Fix ordinary defects and rerun invalidated checks; diagnose a failed broad run before repeating it.
- If findings materially change accepted scope/behavior, return to revise before dependent implementation.
- Record only checks actually performed.

**Writes**
- Scoped source/tests/configuration/migrations/docs, task progress, change-local `verification.md`, and harness-owned evidence.

**Stop / next**
- Passed: current acceptance and required engineering review pass; report finish as the next action.
- Blocked: identify the unresolved dependency or material decision; missing environments remain incomplete acceptance.

**Example:** `$dev work onboarding-invitations`

## Verify

**Purpose:** Assess current acceptance and refresh evidence.

**Inputs**
- Accepted requirements, actual implementation, existing evidence, and tested identities.

**Actions**
- Follow [engineering and verification](engineering-and-verification.md).
- Inspect changed paths, evidence freshness, and required review findings.
- Run missing or invalidated available checks; reuse unchanged valid evidence with a reason.

**Writes**
- `verification.md` and test-run evidence only.
- Safely isolated test-data mutations are permitted within authorized QA.
- Do not edit product code, tests, accepted requirements, expected-result snapshots, or task completion.

**Stop / next**
- Report actual coverage, review results, freshness, and exact gaps.
- Return defects or missing tests to work; report finish only when current acceptance and required engineering review pass with no required gaps.

**Example:** `$dev verify onboarding-invitations`

## Revise

**Purpose:** Update selected planning artifacts in response to feedback.

**Inputs**
- Feedback and an explicit/unambiguous change; `--effort <id>` selects product-level revision.

**Actions**
- For an effort, follow [product planning](product-planning.md): preserve canonical authority and identify dependent changes needing revision.
- For a change, follow [OpenSpec revision](openspec-workflow.md#revise) and native artifact-level review interactions.
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

## Finish

**Purpose:** Synchronize specifications and archive one verified change.

**Inputs**
- Current acceptance evidence, resolved material findings, task state, spec deltas, and optional roadmap association.

**Actions**
- Check evidence against current source/tests/configuration/fixtures/dependencies and accepted scope.
- Require all applicable acceptance and reviews to pass; checked tasks or native `all_done` are insufficient.
- Block closure on failed, mandatory-skipped, missing, or stale evidence; route defects to work and evidence gaps to verify.
- Follow [OpenSpec finish](openspec-workflow.md#finish); verify required spec synchronization before archival.
- If required sync is declined or fails, leave the change active.
- Preserve native review interactions and existing authorization.
- Archive the whole change directory with metadata/evidence; update only owned roadmap links and check references resolve.

**Writes**
- Main capability specs, archive move, and owned roadmap links/delivery summary.

**Stop / next**
- Report exactly one closed change and its evidence.
- A partial contribution does not qualify the whole roadmap outcome.
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
- Check code/test identities before claiming they are unchanged.

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
| Implementation pending verification | Code/task progress exists without required current evidence |
| Verified | Current acceptance and required reviews pass |
| Blocked | A concrete prerequisite prevents the selected action; explain how to clear it |
| Archived | Native archive exists; separately assess verified delivery |

## Everyday sequences

- **New product:** setup → design → review → plan → review → work → finish.
- **Existing effort:** design using existing documents/checklist/evidence → review adopted roadmap → plan the selected outcome → review → work.
- **Small fix:** plan the request → review → work → finish.
- **Returning session:** status → the suggested work, verify, or other concrete command.
- Report target, exact artifacts, evidence/limitations, and next command after every operation.
- Use existing commands for start/resume/next/review; do not add parallel workflow primitives.
