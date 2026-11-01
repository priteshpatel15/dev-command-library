# Installation and project adoption evidence

Observed 2026-10-09. This report records library installation and planning validation, not application acceptance.

## Library identity and installation

- Runtime package: 11 files under `skills/dev`.
- SHA-256 of the JSON-serialized sorted relative-path/content-hash map: `7ae5f763eba24a29c1b693f5dc34b9afcebac948dcd785f51837919d7b1a37f0`. Serialization uses Python `json.dumps(map, sort_keys=True)` with default separators.
- Source: `<repo-root>`.
- Single global symlink: `~/.agents/skills/dev` → source `skills/dev`. No second `dev` link was installed under `.codex/skills`.
- Existing skill-creator `quick_validate.py` returned `Skill is valid!` for the staged and installed package. Local Markdown link checks passed. This is structure validation, not a behavioral guarantee.

## Fresh installed-session observations

Raw evidence base: `/private/tmp/dev-installed-discovery.HXt9bD/`. Each evaluator was a fresh ephemeral Codex CLI process; initial status/final status used a read-only child sandbox, setup used workspace-write. The outer startup had approved local IPC access; no sandbox-bypass flag was used.

1. `status-prompt.txt`, `status-events.jsonl`, `status-last.txt`: the fresh catalog exposed `~/.agents/skills/dev/SKILL.md`; actual executed read commands loaded that entry. Native root checks used process-local telemetry disable and correctly reported the empty fixture as uninitialized. No explicit candidate path was supplied.
2. `setup-prompt.txt`, `setup-events.jsonl`, `setup-last.txt`: globally discovered setup generated the six native OpenSpec workflows, bounded AGENTS/configuration, and healthy native configuration in the unrelated temporary project. Native OpenSpec used fixture-local XDG configuration/data paths. No product code/design/change was requested or generated. Follow-up status observed zero specs/changes.
3. The first setup handoff suggested status immediately after reporting status. The command reference was clarified to recommend design for an initialized empty project, or plan for an already bounded request. `final-status-prompt.txt`, `final-status-events.jsonl`, `final-status-last.txt` record the fresh installed retest: it reported initialized/no effort and suggested `$dev design "<product goal>"`. No app tests or services were run.

Fresh local OpenSpec integration files were verified by native initialization/configuration checks. The global skill itself was directly discovered in new sessions; this report does not infer discovery merely from symlink existence.

## Current-project adoption

Target/path base: `<existing-project>`.

- Root `AGENTS.md` now records the required engineering/Ponytail/test/telemetry/UI/copied-DB contract and actual local conventions. OpenSpec config references it while retaining `spec-driven`.
- `docs/development/operator-experience/roadmap.md` adopts the existing design/spec/verification/catalog and W01–W08 dependencies. It creates no duplicate product design.
- Automated catalog comparison proves all 118 primary V assignments exactly match their existing workflow owners, without duplication or omission, and the catalog retains all R01–R18. Cross-cutting workflow gates and the full legacy crosswalk remain authoritative by reference.
- Old execution instructions are explicitly superseded; historical acceptance/evidence remains. Terminal run07 failure supersedes stale running labels. No passing W01 acceptance was invented.
- Native CLI scaffolded `openspec/changes/complete-operator-inspection/`; proposal, operator-inspection delta, technical design and tasks were authored using native instructions. `openspec validate complete-operator-inspection --strict --json --no-interactive` passed with zero issues.
- All 17 task checkboxes remain unchecked. Native planning completion is explicitly not implementation/verification completion.
- Independent source/document review found two gaps, both corrected: display filters must retain authorized cross-period related evidence; W01 must measure the accepted performance budgets/reference conditions. The reviewer then found no remaining material planning gap.
- Local link verification checked 242 document links with no broken target, including existing historical receipts. Product acceptance was not run.

The reviewable next product operation is `$dev work complete-operator-inspection` after reviewing the prepared change. The existing browser failure and all W01 runtime qualification remain open. No product source, DB data, or live application service was modified by the adoption.

## Confidence boundaries

| Retained report | Scope |
| --- | --- |
| [CLI and planning](2026-10-09-cli-forward.md) | Setup, status, design, revision, plan, work, verify, finish and actual Ponytail loading. |
| [UI acceptance](2026-10-09-ui.md) | Actual browser workflows, responsive experience and corrective TDD in an isolated fixture. |
| [Native stores and schemas](2026-10-09-store-and-gates.md) | Custom artifact paths, separate planning store, documentation-only changes and selection/completion gates. |
| [Stale evidence](2026-10-09-stale.md) | Refusal to archive source changed after verification. |
| [Negative acceptance gates](2026-10-09-negative-gates.md) | Mandatory UI skips, missing copied-DB identity and unresolved architecture findings. |
| [Repeated installed setup](2026-10-09-setup-idempotence.md) | Preservation of existing instructions, schema and configuration across fresh sessions. |

These reports' exact observed scopes and limitations are authoritative. Temporary raw transcripts may not survive system cleanup; these retained summaries and reproducible scenarios provide the durable reference. No library fixture result qualifies W01, a positive copied-database environment, production, or customer financial approval.
