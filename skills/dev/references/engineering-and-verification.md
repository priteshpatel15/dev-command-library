# Engineering and verification contract

These are the user's required engineering obligations. Apply them proportionally to the actual product without weakening accepted scope. Applicable project/nested instructions add concrete conventions. Explicit user changes take precedence; do not silently waive obligations to produce a shorter diff or green report.

## Ponytail at every decision stage

The shared entry loads the **actual installed Ponytail skill** for design, plan, revise, work and verify, with full default and explicit user overrides respected. Discovery uses available skill metadata; never pin its versioned cache location. Reuse an unchanged instruction already read in the session. Delegates receive the actual skill instructions and the same scope/rules.

| Stage | Apply Ponytail by | Retained decision/evidence |
| --- | --- | --- |
| Design | Avoid unnecessary proposed capabilities, options and speculative architecture while meeting complete requested journeys | Product scope, boundaries, justified deferrals and reuse opportunities |
| Plan | Inspect all affected callers/tests/fixtures/config/exports; reuse existing capabilities; choose the smallest complete solution | Reuse/dependency decisions in native design or concise proposal/tasks |
| Revise | Reassess complexity and obsolete work without silently dropping accepted behavior | Coherent revisions and affected acceptance/task/evidence notes |
| Work | Reuse local components, then standard/platform or installed capabilities; fix the root cause once; preserve validation/errors | Actual code, tests, scoped task progress and QA |
| Verify | Review implementation and call paths for avoidable duplication, abstractions, dependencies and incomplete scope | Concrete findings and resolution in verification |
| Finish | Require applicable current review evidence | Completion eligibility and preserved archive evidence |

Least code is not a line-count threshold. Simplicity is judged across the complete change, including consumers and tests. No speculative frameworks, extension points, wrappers or interface-per-class rules. A necessary abstraction protects an actual boundary or consumer; its benefit must be concrete.

## Architecture, decoupling and SOLID

Map the project before editing. Domain rules remain independent of UI, transport, persistence and vendor SDK details. Application behavior coordinates use cases through meaningful boundaries. Outer adapters implement infrastructure; composition connects them. Reuse the project's real structure instead of manufacturing layers for appearance.

Keep business behavior with its owning component, avoid duplicating it in UI/API adapters, and expose narrow interfaces for actual consumers or replaceable dependencies. Review cohesive responsibilities, dependency inversion, compatible substitutions, interface size and unnecessary coupling. Reuse existing boundary tests and CI checks; add a focused invariant test when the changed dependency rule warrants it.

The project `AGENTS.md` records concrete layers and commands; OpenSpec config points to that authority. Product design adds durable product constraints; native change design records the selected technical solution. Conflicts are surfaced, not silently resolved by the agent.

## Test-first implementation

Before nontrivial behavior changes, identify edge cases and add/run a focused failing regression or contract test. Implement until it passes, then refactor with required checks. Test observable behavior and meaningful invariants rather than duplicating implementation. Include applicable errors, validation, permissions, empty states, concurrency/retry/idempotency and boundary cases based on the change.

Adopting existing code does not permit inventing a historical failing run. Record the existing state, demonstrate current regressions where present, and add missing meaningful coverage before new implementation. Documentation-only changes need relevant structural/behavioral validation, not invented application tests. No new generic testing framework is needed when project tools suffice.

Focused tests support iteration; complete required integration acceptance before verified status. Broaden regression for changed shared contracts/dependencies. Preserve still-valid earlier checks with a reason; don't rerun every product suite after each small edit. Investigate repeated identical failures before broad retrying.

## Telemetry

Use the project's existing observability system. Cover relevant workflow starts/outcomes, errors, state transitions, dependency calls, durations, correlation and recovery in structured events/metrics/traces appropriate to the component. Preserve trace/correlation propagation across actual runtime boundaries. Verify meaningful events and error paths in tests and runtime evidence where applicable.

Do not log secrets, tokens or unrestricted customer records. Do not duplicate events in every layer, add log noise to trivial helpers, or build a new telemetry framework merely to satisfy this rule. Comprehensive means the actual workflow and failure paths are diagnosable.

## UI and database acceptance

For UI changes, cover all designed functionality, states and end-to-end workflows with applicable Playwright checks. Inspect real rendered behavior, responsive states, keyboard/accessibility and failure/recovery experience; screenshots alone are not workflow proof. Mocks/component tests support development but do not replace required real-stack acceptance.

Database-backed acceptance uses a real testing copy. Before mutation-capable QA, verify the intended copy, actual connection identity, and every participating app/admin/migration/test/worker process's target. Use the project's established guard and runtime identity query, such as PostgreSQL `select current_database()`. Names or environment variables alone do not prove the active connection. Never fall back to a source/production DB when the copy is missing. Independently assert effects, tenant isolation and required data preservation. Keep secrets out of reports.

CLI-only work does not acquire a fictional UI gate. Missing applicable UI/DB environments are explicit blockers to that acceptance; they never count as passes or become silent skips.

## Engineering review

Inspect the actual diff and affected call paths after implementation. Record files/findings and how they were resolved. Review architecture, SOLID, reuse, unnecessary code/dependencies, validation/error handling, telemetry, accessibility and acceptance coverage. Use an independent reviewer for material architecture, shared-boundary, security or data-contract changes; otherwise identify the actual review method honestly.

Distinguish introduced violations, affected pre-existing defects and unrelated debt. Fix required findings within scope; do not expand into unrelated legacy rewrites. Functional green tests do not excuse unresolved required engineering findings. A semantic review is necessary; a linter cannot prove SOLID.

## Evidence and freshness

Use [the verification template](../assets/templates/verification.md) for one change-local `verification.md`. It is an evidence record, not another task tracker. Record:

1. Change identity, target repository/worktree and explicit path bases; governing instructions and actual skill source/version where available.
2. Tested commit plus relevant dirty/untracked file content identity; relevant test, fixture, configuration and dependency identity. A commit hash alone is insufficient in a dirty tree. Use existing harness identities or content hashes through existing tools; no new identity controller is needed.
3. Requirement/scenario coverage, actual commands, environments, timestamps, exit/results and retained artifact paths.
4. Review method, concrete findings/resolutions, and required UI/database/telemetry observations.
5. Missing/skipped/failed checks, unresolved defects and whether finish is eligible.

Map relevant source, tests, fixtures, configuration, dependencies and accepted requirements to their checks. If any changes, invalidate affected evidence and rerun the appropriate checks. When relevance cannot be established, treat the evidence as stale. Record why unchanged prior evidence can be reused. Never convert a planned test, fixture, checked task or native `all_done` into a result.

Store raw reports/logs/screenshots/traces in the existing harness-owned paths. Only use `artifacts/development/<change>/<run>/` as an explicitly ignored/privacy-controlled fallback. Commit safe summaries and references, not secrets or unrestricted records. Use repository-root-relative references with a declared base, or identified external artifact locations; archive must not silently break references.

Work and verify update the report. Revise marks affected evidence invalid. Finish checks freshness before synchronization/archive and preserves it. Direct archive is not verified completion. Required failing, missing, skipped or stale evidence, or unresolved material review findings, prevents verified status and finish.

These are workflow gates with observable supporting checks, not a claim that prompt text provides infallible enforcement. Reuse CI and independent review where available.
