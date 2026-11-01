# Global development command library: approved implementation plan

This document records the design approved before construction, amended on 2026-10-09 to allow flexible implementation/testing order while retaining required coverage and QA. It is a construction and acceptance reference, not a claim that its steps have passed. Actual library evaluation results belong in `tests/evidence/`; product completion belongs in project evidence.

## Goal and boundaries

Build one global Codex skill named `dev`, authored in `<repo-root>/skills/dev` and installed through the single link `~/.agents/skills/dev`.

The user enters reusable chat commands to move from product design and an outcome roadmap to bounded OpenSpec changes, implementation, acceptance, and archival. Commands are manual in this version. There is no controller, task database, scheduler, custom OpenSpec schema, or shell execution wrapper.

The package combines product-planning guidance, installed OpenSpec capabilities, and the actual installed Ponytail skill. It preserves the original `specify-product` and Ponytail skills. It draws from `specify-product`'s product design concepts without invoking its compiler, approval runtime, or `develop-product` handoff.

## Public command interface

| Command | Result and boundary |
|---|---|
| `$dev setup` | Inspect dependencies and project conventions; initialize missing OpenSpec configuration; bounded merges of instructions/configuration. No product implementation. |
| `$dev design <goal or source>` | Create or adopt canonical product design and outcome roadmap. Stop at product review. |
| `$dev plan [outcome or request]` | Create one bounded native OpenSpec change with schema-required artifacts. Stop at change review. |
| `$dev work [change]` | Implement/resume and complete required tests, copied-database/UI QA, fixes, and engineering review. Stop accepted or with a concrete unresolved blocker. |
| `$dev verify [change]` | Review current implementation/evidence and run missing or invalidated checks. Write verification/test results; do not alter product code or requirements. |
| `$dev revise <feedback>` | Revise selected change planning artifacts, reopen affected tasks, invalidate affected proof. Use `--effort <id>` for product-level revision. |
| `$dev finish [change]` | Require current passing acceptance; synchronize main specs, archive, update owned roadmap references. No automatic next outcome, deployment, or product commit. |
| `$dev status` | Read-only state, artifacts, blocker, and exact next command. |
| `$dev` | Status and command card. |

`work` includes all required QA; `verify` is an optional separate/repeated evidence review. Standalone bounded bugs can use `plan` directly without an invented product effort.

Targets resolve from the current repository, an explicit argument, an unambiguous conversation reference, or the sole compatible candidate. Multiple candidates require selection. Never select by modification time or a global active-project pointer. Respect OpenSpec stores and custom schemas through CLI-resolved paths.

## Architecture, files, and artifacts

The [architecture guide](../skills/dev/references/architecture.md) is the maintained structural reference, including Mermaid diagrams and complete file-purpose tables. The [command reference](../skills/dev/references/commands.md) is the authoritative operational interface.

```text
README.md                            Human quickstart and reference navigation
.gitignore                           Ignore caches and temporary evaluations
docs/implementation-plan.md          Approved build record
skills/dev/SKILL.md                   Router and essential shared requirements
skills/dev/agents/openai.yaml         Codex display/invocation metadata
skills/dev/references/
  architecture.md                    Architecture, ownership, artifact flow
  commands.md                        Command behavior and examples
  product-planning.md                Design/roadmap creation and adoption
  openspec-workflow.md                Native workflow delegation and lifecycle
  engineering-and-verification.md    Engineering and acceptance requirements
  maintenance.md                     Install, evaluate, update, rollback, remove
skills/dev/assets/templates/
  design.md                          New product design starting structure
  roadmap.md                         Outcomes, dependencies, change links
  verification.md                    Current evidence and findings
tests/scenarios.md                   Reproducible behavior evaluation cases
tests/evidence/<run-id>.md            Observed results and limitations
```

Only the installed `skills/dev` package is required during normal operation. Use progressive loading and avoid duplicating provider instructions. No reusable executable script is needed for this initial instruction-based library.

Product artifacts belong in `docs/development/<effort-id>/design.md` and `roadmap.md`, unless suitable canonical documents already exist. Reuse those documents instead of creating competing authority.

OpenSpec owns scaffolding and schema-required proposal, behavioral specifications, applicable technical design, and tasks under its resolved change root. `verification.md` is an additional library convention alongside those artifacts; test output uses existing project locations with unambiguous path bases. It remains with the archived change.

Product design describes the intended experience and durable constraints. Change design describes a bounded technical solution. The roadmap links observable outcomes to changes rather than duplicating task state.

## Ponytail and engineering governance

Load the actual installed Ponytail skill for **design, plan, revise, work, and verify**. Default to full, respect explicit user overrides, reuse an unchanged copy already loaded in the session, and propagate the applicable rules to delegated agents. Missing capabilities are reported before dependent work. `setup` and `status` can diagnose them; `finish` consumes current review evidence.

| Stage | Ponytail's role |
|---|---|
| Design | Find the simplest complete experience; question unnecessary proposed features and speculative platforms. Preserve accepted scope. |
| Plan | Inspect callers, contracts, tests, fixtures, configuration, and exports. Reuse existing capabilities and explain necessary additions. |
| Revise | Remove obsolete work while preserving accepted requirements and coherent evidence/task state. |
| Work | Make the least necessary code change, fix shared causes, and retain error handling/validation. |
| Verify | Review the actual diff for duplication, needless abstractions/dependencies, and incomplete scope. |
| Finish | Require current acceptance and review before closure. |

The governing principle is the smallest complete solution satisfying the product and engineering requirements. Clean Architecture governs high-level boundaries and dependency direction; decoupling and SOLID govern focused components and interfaces. Ponytail cannot silently weaken accepted functionality, testing, comprehensive privacy-safe telemetry, accessibility, or required QA.

`setup` preserves/extends `AGENTS.md` and references project authority from OpenSpec configuration. It discovers real module boundaries, test commands, architecture checks, and database guards. Reuse meaningful mechanical checks; use semantic engineering review for judgments that tests cannot establish. Material architecture, shared-contract, security, or data-contract changes receive independent review.

Choose implementation/testing order to fit the change; cover meaningful behavior changes and edge cases without requiring a prior failing test run. Complete required unit, contract, integration, and end-to-end coverage. All designed UI functionality and workflows require applicable Playwright coverage and experience inspection. Real database acceptance uses a testing copy, with actual connection identity established before mutation-capable tests. A missing copy is a blocker, not authority to use production.

Verification records governing instructions/Ponytail, tested code/test/config/fixture identity including dirty changes, acceptance coverage, exact commands/results, engineering review, UI/database evidence, and unresolved findings. Checked tasks or OpenSpec `all_done` cannot qualify completion alone. Material edits invalidate affected proof; missing, failed, mandatory-skipped, stale, or materially unresolved evidence blocks `finish`.

Required spec synchronization must succeed before archival. Declining required synchronization leaves the change unarchived. No command silently starts another roadmap outcome.

## Build sequence and acceptance

1. Create the dedicated source repository and behavioral scenarios.
2. Author the router, references, metadata, templates, documentation, diagrams, and maintenance procedures.
3. Run the existing skill-creator validator and check references, metadata, consistency, and template usability.
4. Evaluate realistic requests in isolated projects through independent agents; inspect actual artifacts and actions.
5. Fix demonstrated issues, repeat affected cases, and retain actual results.
6. Install the single global symlink without overwriting an unexpected existing installation.
7. Confirm discovery in a fresh Codex session and exercise the installed skill in an unrelated temporary project.
8. Prepare the current project's continuation as described below.

Required evaluations:

| Scenario | Acceptance |
|---|---|
| Fresh and repeated setup | Correct initialization; existing configuration and unrelated work preserved. |
| Design to roadmap to plan | Coherent outcomes/dependencies and one bounded change; review stops respected. |
| Standalone CLI bug | No mandatory roadmap; meaningful regression coverage, complete work/verify/finish cycle. |
| Small UI fixture | Actual browser workflow evidence, experience review, and corrective work when needed. |
| Ambiguous targets | Explicit selection required; unrelated work untouched. |
| Existing checklist adoption | Requirements and reusable work retained; historical checks do not become proof. |
| Actual Ponytail loading | Design/plan/revise/work/verify load the provider; missing dependency is reported. |
| Resume and stale evidence | Interrupted work resumes; relevant changes invalidate affected evidence. |
| Missing copied-DB or UI proof | Acceptance/finish remains incomplete. |
| Material architecture finding | Passing functional tests cannot bypass engineering review. |
| Separate stores/custom schemas | Native resolved paths and artifact conditions respected. |
| Sync/archive and links | Sync succeeds first, full evidence retained, owned links updated, no automatic next work. |

Retain meaningful observed evaluation evidence. The structural validator and prose checks alone do not establish behavioral acceptance. Library fixture tests never qualify the restaurant project's W01 acceptance.

## Initial installation and project adoption

The global installation uses one stable source link, with no duplicate alias. Initialize local source history. Document installation, updates, rollback, removal, and the fact that linked-source edits become globally visible immediately. Validate candidate updates before exposing them to normal use, and check discovery in a fresh session.

The initial `restaurant_data_integrator` handoff includes setup, design/roadmap adoption, and **W01 planning only**:

- Preserve dirty project work and inspect current instructions before bounded changes.
- Create/extend root project instructions from the user's governing requirements and actual conventions; reference them from OpenSpec configuration.
- Reuse accepted operator-experience design, specification, verification matrix, ADR, scenario catalog, and retained evidence.
- Create `docs/development/operator-experience/roadmap.md`, preserving W01–W08 dependencies, R01–R18, and all 118 scenario obligations.
- Mark the former checklist's execution instructions superseded while preserving historical requirements, crosswalks, and receipts. Replace fixed implementation/testing order and automatic-continuation instructions with manually selected changes and required acceptance checks.
- Reconcile actual implementation and retained evidence; do not infer qualification from old running state or checked boxes.
- Prepare and validate **`complete-operator-inspection`** as the OpenSpec change for remaining W01 implementation and qualification.

Stop at the installed and evaluated library, available documentation, adopted roadmap, and reviewable W01 change. The authorized initial handoff does not include W01 product implementation or runtime qualification.

After reviewing that change, the user's continuation command is:

```text
$dev work complete-operator-inspection
```

Instruction-based gates depend on agent adherence. Automated project checks and recorded independent review supplement them; the library makes no claim of an enforcement engine outside those mechanisms.
