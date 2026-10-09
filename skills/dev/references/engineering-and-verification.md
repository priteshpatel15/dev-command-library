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
| Work | Implement consistently with those decisions; revise material scope/behavior changes before dependent implementation. |
| Verify | Inspect actual imports, call paths, responsibilities, and contracts against all three levels; record findings and resolutions. |

## Ponytail integration

- Use the installed `ponytail:ponytail` skill through [SKILL.md activation rules](../SKILL.md#load-dependencies).
- Apply this file's architecture and acceptance requirements alongside the skill; honor explicit user overrides.
- Load actual installed companion skills only when needed, using the same discovery and context-reuse rules.

| Installed skill | Use it when |
| --- | --- |
| `ponytail:ponytail-review` | Reviewing a completed code change during work or verify; provide the selected diff/files and relevant requirements explicitly. |
| `ponytail:ponytail-audit` | A broader assessment is requested or needed to understand the selected work; keep the assessment within that scope. |
| `ponytail:ponytail-debt` | Examining deliberate shortcuts relevant to the work, or when requested; persist a ledger only when requested. |
| `ponytail:ponytail-gain` / `ponytail:ponytail-help` | Requested information; these are not acceptance gates. |

- Require a current Ponytail review for code-change acceptance unless explicitly overridden by the user.
- Reuse a prior Ponytail review only when relevant code, requirements, dependencies, and review instructions remain unchanged.
- Record actual skill sources, available versions, and overrides once per verification record; update them when the instructions used change.

## Implementation and testing

- Choose implementation/testing order to fit the change; a prior failing test run is not required.
- Complete meaningful regression/contract coverage and applicable unit, integration, and end-to-end acceptance.
- Test observable behavior and invariants; avoid tests that duplicate implementation.
- Cover relevant errors, validation, permissions, empty states, concurrency, retries, idempotency, and boundaries.
- Diagnose observed regressions and complete missing coverage; record only checks actually performed.
- For documentation-only changes, validate documents/schemas/affected behavior without claiming application acceptance.
- Use existing project test tools when sufficient.
- Run focused checks during iteration; complete required integration acceptance before verified status.
- Broaden regression checks for changed shared contracts/dependencies.
- Reuse still-valid results with an explicit reason; rerun affected checks after changes.
- Investigate repeated identical failures before retrying broad suites.

## Telemetry

- Use the project's existing observability facilities.
- Cover workflow starts/outcomes, errors, state transitions, dependency calls, timing, correlation, and recovery.
- Use structured events, metrics, or traces appropriate to the component.
- Preserve correlation across actual runtime boundaries.
- Verify meaningful telemetry and failure paths through tests and applicable runtime evidence.
- Exclude secrets, tokens, and unrestricted customer records from logs and reports.
- Avoid duplicate events and noise from trivial helpers; keep workflows and failures diagnosable.

## UI and database acceptance

### UI

- Cover all designed functionality, states, and end-to-end workflows with applicable Playwright checks.
- Inspect real rendered behavior, responsive states, keyboard/accessibility, and failure/recovery experience.
- Use screenshots as supporting evidence, not workflow proof alone.
- Use mocks/component checks for development; complete required acceptance against the real stack.

### Database

- Use a real testing copy for database-backed acceptance.
- Before mutation-capable QA, verify copy provenance and actual connection identity for every participating app/admin/migration/test/worker process.
- Use the established guard and runtime identity query, such as PostgreSQL `select current_database()`.
- Do not infer connection identity from names or environment variables alone.
- If the copy is unavailable, report the blocker; never fall back to source/production databases.
- Independently assert required effects, tenant isolation, and data preservation.
- Keep credentials and sensitive records out of evidence.

### Applicability

- Apply UI/DB gates only when relevant; CLI-only work does not invent a UI requirement.
- Missing required environments or evidence block acceptance; they are not passes or silent skips.

## Engineering review

- Inspect the actual diff and affected call paths after implementation.
- Use the Ponytail review integration above for code changes.
- Check Clean Architecture, decoupling, SOLID, validation/error handling, telemetry, accessibility, and acceptance coverage.
- Use an independent reviewer for material architecture, shared-boundary, security, or data-contract changes.
- Record the actual reviewer/method, reviewed scope, findings, and resolutions.
- Distinguish introduced violations, affected existing defects, and unrelated debt.
- Resolve required findings within scope; avoid unrelated legacy rewrites.
- Do not use passing functional tests to excuse unresolved required engineering findings.
- Review architectural meaning explicitly; a linter alone cannot establish SOLID compliance.

## Evidence and freshness

Use the [verification template](../assets/templates/verification.md) for one change-local `verification.md`.

### Record

- Change identity, target repository/worktree, and explicit path bases.
- Governing instructions and actual skills used, including available versions and overrides.
- Tested commit plus relevant dirty/untracked content identities; commit identity alone is insufficient.
- Relevant test, fixture, configuration, dependency, and accepted-requirement identities.
- Requirement/scenario coverage, exact commands, environments, timestamps, results/exit codes, and evidence paths.
- Review findings/resolutions and applicable UI/database/telemetry observations.
- Failed, skipped, missing, or stale checks; unresolved defects; completion eligibility.

### Assess freshness

- Map relevant source, tests, fixtures, configuration, dependencies, and requirements to their checks.
- If relevant inputs change, invalidate affected evidence and rerun appropriate checks.
- If relevance cannot be established, treat the evidence as stale.
- Record why unchanged prior evidence remains valid.
- Never turn a planned check, fixture, task checkbox, or native `all_done` into a passing result.
- Use existing harness identities or content hashes; keep verification an evidence record rather than another task database.

### Store evidence

- Use existing harness-owned locations for logs, reports, screenshots, and traces.
- Use `artifacts/development/<change>/<run>/` only as an explicitly ignored, privacy-controlled fallback.
- Commit safe summaries and references; exclude secrets and unrestricted records.
- Declare repository-relative or external path bases; keep references resolvable after archival.

### Complete the change

- Work and verify update evidence; revise invalidates affected evidence.
- Finish checks freshness before specification synchronization/archive and preserves the evidence.
- Block verified status and finish on required failures, missing checks, mandatory skips, stale evidence, or unresolved material findings.
- Archival alone is not verified delivery.
- Support these instruction-based gates with actual checks, CI, and independent review where applicable.
