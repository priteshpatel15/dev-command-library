# Engineering and verification contract

## Purpose and authority

- Define required code design, implementation quality, and evidence for completion.
- Apply rules to the selected scope without weakening accepted behavior.
- Follow applicable project/nested `AGENTS.md` instructions and accepted product constraints.
- Keep concrete project boundaries/commands in `AGENTS.md`; reference that authority from OpenSpec configuration.
- Record change-specific technical decisions in existing planning artifacts.
- Honor explicit user changes; surface unresolved conflicts instead of silently choosing weaker rules.

## Architecture, decoupling and SOLID

Apply this hierarchy intentionally: **Clean Architecture → decoupled components within modules → SOLID functions, classes, and contracts.**

### Clean Architecture: system organization and dependencies

- Map affected modules, responsibilities, ownership, and dependencies before changing code.
- Separate domain rules, application use cases, and infrastructure concerns.
- Keep domain rules independent of UI, transport, databases, frameworks, and vendor SDKs.
- Direct source dependencies inward; outer adapters implement application/domain contracts.
- Connect concrete dependencies at composition boundaries.
- Place business behavior in its owning module; avoid competing implementations in adapters.
- Apply these boundaries through the project's existing structure rather than cosmetic layers.

### Decoupling: components within each module

- Give each component a cohesive responsibility.
- Use narrow, explicit contracts across component boundaries.
- Pass dependencies explicitly; avoid hidden global dependencies.
- Isolate external interactions behind appropriate boundaries.
- Keep implementation details private; avoid reaching into another component's internals.
- Make component behavior independently testable and reusable where appropriate.

### SOLID: functions, classes, and contracts

| Principle | Required design |
| --- | --- |
| Single responsibility | Give each function/component one cohesive purpose. |
| Open/closed | Support required variations through appropriate extension points. |
| Liskov substitution | Interchangeable implementations preserve input/output, error, and invariant contracts. |
| Interface segregation | Require only the operations and data each consumer needs. |
| Dependency inversion | Business behavior depends on suitable contracts rather than infrastructure details. |

- Apply each principle where relevant; substitution/interface rules concern cooperating components, not every isolated function.
- Judge abstractions by the boundary they protect; one implementation can still justify a boundary.
- Reuse architecture/import checks; add a focused invariant check when a changed dependency rule warrants it.

### Apply and verify architectural decisions

| Stage | Required action |
| --- | --- |
| Design / plan | State affected responsibilities, boundaries, dependency direction, and reuse decisions in the existing design or proposal. |
| Work | Write the change map, implement consistently with it, and revise material scope/behavior changes before dependent implementation. |
| Verify | Inspect actual imports, call paths, responsibilities, and contracts against all three levels; record findings and resolutions. |

## Ponytail integration

Ponytail saves time by shaping the code before it is written, not by reviewing it afterwards.

- Load `ponytail:ponytail` (full unless overridden) through [command routing](../SKILL.md#command-routing) and the shared [loading rules](../SKILL.md#load-dependencies).
- Apply this file's architecture and acceptance requirements alongside the skill; honor explicit user overrides.

### Change map (required before the first code edit)

Write Ponytail's "Before you write" step into `verification.md` as a list of at most ~20 lines:

- Files to touch, and the callers, tests, fixtures, configuration, exports, and contracts the change must reach.
- Existing components/helpers/patterns reused, by path.
- Necessary additions, each with the boundary it protects.
- What is deliberately skipped (features, options, abstractions nobody asked for).
- Change-gate checks: the focused commands and the browser specs this change touches.

Implement only what the map lists; if implementation discovers the map was wrong, update it before continuing.

### Review (once, at the end)

- After the change gate passes, load `ponytail:ponytail-review` and review the diff against the change map and design.
- Resolve required findings, rerun affected focused checks, and record the review with the diff hash it covered. At most one fix-and-recheck round; further findings route to a new small change.
- A review is current while the recorded diff hash matches the current diff. Evidence, documentation, and task-checkbox edits do not invalidate it.
- Use an independent reviewer only when project instructions require it for the boundaries this change touches (for example shared contracts, security, data contracts). Brief it with the diff, change map, and relevant requirements; do not fork the conversation; accept one pass.
- `ponytail-audit`, `ponytail-debt`, `ponytail-gain`, and `ponytail-help` are user-invoked only; they are never acceptance gates.
- Record skill names and versions once per `verification.md`.

## Implementation and testing

- Choose implementation/testing order to fit the change; a prior failing test run is not required.
- Complete meaningful regression/contract coverage and the change gate; the outcome gate runs once through `qualify`.
- Test observable behavior and invariants; avoid tests that duplicate implementation.
- Cover relevant errors, validation, permissions, empty states, concurrency, retries, idempotency, and boundaries.
- Diagnose observed regressions and complete missing coverage; record only checks actually performed.
- For documentation-only changes, validate documents/schemas/affected behavior without claiming application acceptance.
- Use existing project test tools when sufficient.

### Inner and outer loop

- Inner loop: run the smallest check that can fail (one test file, one spec, one scenario title) against an already running stack or reused fixture. Fix, rerun that check only.
- After two identical failures, stop and diagnose (logs, traces, a reproduction) before running anything again.
- Outer loop: run the change gate once in the foreground with a timeout after the inner loop is green. Configure it to report all failures.
- Never rerun a full harness to retest one scenario, and never run a check in the background and poll it.
- Broaden regression checks only for changed shared contracts/dependencies.

## Telemetry

- Use the project's existing observability facilities.
- Cover workflow starts/outcomes, errors, state transitions, dependency calls, timing, correlation, and recovery.
- Use structured events, metrics, or traces appropriate to the component.
- Preserve correlation across actual runtime boundaries.
- Verify meaningful telemetry and failure paths through tests and applicable runtime evidence.
- Exclude secrets, tokens, and unrestricted customer records from logs and reports.
- Avoid duplicate events and noise from trivial helpers; keep workflows and failures diagnosable.

## Acceptance tiers

| Tier | When | Proves | Owner |
| --- | --- | --- | --- |
| Change gate | Every `work`; refreshed by `verify`; required by `finish` | The change's own units/contracts, boundary checks, and the browser specs it touches, run against a running stack when it has UI | Change `verification.md` |
| Outcome gate | Once per roadmap outcome through `qualify`, after its last slice finishes | The whole outcome: integrated harness, copied-database provenance and preservation, full browser device/accessibility matrix | Outcome qualification record |

- `AGENTS.md` names both gates' commands and the fast path for a single spec against a reused stack.
- A slice's change gate never includes the full outcome matrix; a qualification never substitutes for a missing change gate.
- Defects found by the outcome gate become new small changes.

### UI

- Cover the designed functionality and states of the change with Playwright checks at the change gate; cover every designed workflow, device, and accessibility state at the outcome gate.
- Inspect real rendered behavior, keyboard/accessibility, and failure/recovery experience for what the change touches.
- Use screenshots as supporting evidence, not workflow proof alone.
- Use mocks/component checks for development; complete the change gate against the real stack.

### Database

- Use a real testing copy for database-backed acceptance.
- Before mutation-capable QA, verify copy provenance and actual connection identity for every participating process using the project's established guard and runtime identity query, such as PostgreSQL `select current_database()`.
- Do not infer connection identity from names or environment variables alone.
- If the copy is unavailable, report the blocker; never fall back to source/production databases.
- Assert required effects, tenant isolation, and data preservation at the outcome gate; at the change gate, assert the effects the change makes.
- Keep credentials and sensitive records out of evidence.

### Applicability

- Apply UI/DB gates only when relevant; CLI-only work does not invent a UI requirement.
- Missing required environments or evidence block acceptance; they are not passes or silent skips.

## Engineering review

- Inspect the actual diff and affected call paths after implementation, in the single review pass above.
- Check Clean Architecture, decoupling, SOLID, validation/error handling, telemetry, accessibility, and change-gate coverage.
- Record the reviewer/method, reviewed diff hash, findings, and resolutions.
- Distinguish introduced violations, affected existing defects, and unrelated debt.
- Resolve required findings within scope; avoid unrelated legacy rewrites.
- Do not use passing functional tests to excuse unresolved required engineering findings.
- Review architectural meaning explicitly; a linter alone cannot establish SOLID compliance.

## Evidence and freshness

Use the [verification template](../assets/templates/verification.md) for one change-local `verification.md`, and the [outcome verification template](../assets/templates/outcome-verification.md) for `qualify`.

### Tested identity

Record exactly these, once per evidence update:

```sh
git rev-parse HEAD
git diff HEAD | shasum
git ls-files --others --exclude-standard | sort | shasum
```

- Together they identify the tested tree. Do not hash individual inputs, build input manifests, or write reuse-rationale files.
- Evidence is current while all three match; otherwise rerun the change gate and, if the diff hash changed, the review.
- Record the change gate and outcome gate commands exactly as run, with timestamp, exit code, and the harness-owned receipt path.

### Record

- Change identity, target repository/worktree, path bases, and governing instructions.
- Skill names and versions used, with explicit overrides.
- The change map.
- One checks table: check, command, result, receipt.
- Review: method, diff hash, findings, resolutions.
- Failed, skipped, missing, or stale checks; unresolved defects; finish eligibility.
- Never turn a planned check, fixture, task checkbox, or native `all_done` into a passing result.

### Store evidence

- Use existing harness-owned locations for logs, reports, screenshots, and traces.
- Use `artifacts/development/<change>/<run>/` only as an explicitly ignored, privacy-controlled fallback.
- Commit safe summaries and references; exclude secrets and unrestricted records.
- Declare repository-relative or external path bases; keep references resolvable after archival.

### Complete the change

- Work and verify update evidence; revise invalidates affected evidence.
- Finish checks identity before specification synchronization/archive and preserves the evidence.
- Block verified status and finish on required failures, missing checks, mandatory skips, stale evidence, or unresolved material findings.
- Archival alone is not verified delivery; qualification of the outcome is separate.
