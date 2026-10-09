# Native stores, custom schema, conditional artifacts, and gates

Evaluation date: 2026-10-09. Fixture/scorer: `library_documentation`; evaluators: fresh ephemeral Codex CLI sessions, given the candidate path, operation, fixture, and resource boundary without scoring criteria. These are observed behavior evaluations, not wording assertions.

## Identity and isolation

- Candidate: `/private/tmp/dev-command-library-20261009.n2czth/skills/dev/SKILL.md`.
- Raw evidence base: `/private/tmp/dev-library-doc-eval-eudjf4l6/`. All paths below are relative to this base unless stated otherwise.
- Initial candidate per-file SHA-256 identity: `candidate-manifest.json`.
- Native provider: OpenSpec 1.14.1. Python fixture baseline: four passing unittest methods per project. Actual installed Ponytail was read by the judgment evaluators; executed read commands are retained in their JSONL transcripts.
- `XDG_CONFIG_HOME` was `config/` and `XDG_DATA_HOME` was `data/` inside the evidence base. Store registration is retained at `data/openspec/stores/registry.yaml`; no user-wide store registration was used. `HOME` and `CODEX_HOME` were not overridden.
- Initial sandboxed Codex startup failed before any evaluator action with `failed to initialize in-process app-server client: Operation not permitted`; see `results/custom-plan.stderr`. A normally approved escalated launcher then started each evaluator with its own `workspace-write` sandbox, temporary writable root, `--ephemeral`, and no bypass flags. This startup failure is infrastructure evidence, not a product test result.
- During evaluation the parent added process-local `OPENSPEC_TELEMETRY=0` to the entrypoint and OpenSpec discovery guidance after a separate setup test found first-use configuration writes. The changed files were exactly `SKILL.md` and `references/openspec-workflow.md`. Earlier transcripts apply to the initial identity; the read-only status retest applies to `results/status-retest-candidate.json`. Other runtime references were unchanged.
- After these evaluations, the parent corrected `commands.md` so status in an initialized project without an effort/change recommends design or bounded planning instead of another status call. That separately evaluated empty-project routing case is not established by this report. The explicit-target lifecycle and two-change status cases above do not depend on that route.

## Fixture preparation, separate from evaluator actions

The runner created `custom-project/`, `store-project/`, `conditional-project/`, and `gates-project/` from the shared CLI fixture in `tests/scenarios.md`. Each baseline suite passed all four tests before evaluation. Each has a local fixture-only Git baseline; no remote or global Git identity was changed.

Native preparation commands and their exits/receipt paths are retained in `fixture-commands.json`:

```text
openspec init --tools codex                         # each fixture
openspec schema fork spec-driven eval-custom --json # custom-project
openspec schema validate eval-custom
openspec store setup eval-store --path /private/tmp/dev-library-doc-eval-eudjf4l6/planning-store --no-init-git --json
openspec store list --json
openspec context --json --store eval-store
```

All exited 0. Only the fixture's forked schema was edited: task `generates` and apply `tracks` point to `work/steps.md`; the task template remains native. Store context resolves `/private/tmp/dev-library-doc-eval-eudjf4l6/planning-store` with source `store` and ID `eval-store`.

For the ambiguity fixture the runner used native `openspec new change first-scope` and `second-scope`, then created one roadmap for each. The complete 68-file project snapshot, including untracked files and Git metadata, is in `results/gates-before.json`.

## Requests and receipts

Every exact evaluator prompt, including its resource boundary and isolated XDG paths, is retained under `results/<name>-prompt.txt`; tool activity is `results/<name>.jsonl`, final handoff `results/<name>-final.md`, and launcher diagnostics `results/<name>.stderr`. The initial custom planning retry uses `custom-plan-retry.jsonl` and `custom-plan-retry.stderr` with `custom-plan-prompt.txt`.

| Request name | Operation given to the fresh evaluator |
|---|---|
| `custom-plan` | Use schema `eval-custom` for `$dev plan "Fix whitespace normalization so repeated spaces, tabs, and newlines become one hyphen; preserve Unicode and empty-input behavior through both existing callers"`. |
| `store-plan` | Use registered store `eval-store`, code repository `store-project`, and `$dev plan "Normalize article whitespace: every run of whitespace becomes one hyphen; preserve Unicode, outer trimming and empty behavior through existing callers"`. |
| `conditional-plan` | `$dev plan "Document existing CLI usage in README.md, including the current basic Hello World example and stderr telemetry. This documentation-only change must preserve all observable application behavior."` |
| `ambiguity-work` | `$dev work` in the two-change fixture. |
| `gates-status` | `$dev status` in a fresh session against that same fixture. |
| `gates-finish` | `$dev finish first-scope` with no implementation/acceptance evidence. |
| `custom-work` | A separate explicit `$dev work fix-slug-whitespace-normalization` after its prepared plan. |
| `store-work` | A separate explicit `$dev work normalize-article-whitespace`, retaining `eval-store` and the concrete target code repository. |
| `custom-finish` | A separate explicit `$dev finish fix-slug-whitespace-normalization` after completed work. |
| `store-finish` | A separate explicit `$dev finish normalize-article-whitespace`, retaining the registered store and target code repository. |
| `status-retest` | `$dev status` with the updated candidate and fresh `read-only-config/`, `read-only-data/` paths. No telemetry override was supplied by the runner. |

## Observed results

### Custom schema planning — PASS

Native strict validation passed. The evaluator created `custom-project/openspec/changes/fix-slug-whitespace-normalization/work/steps.md`; no shadow `tasks.md` exists. It read the actual custom task instructions and omitted conditional `design.md` for the small fix, honestly reporting native status as 3/4 artifacts. Source/tests remained unchanged at the planning boundary (`results/custom-project-after-plan-source-diff.txt`, exit 0).

Actual Ponytail read: `custom-plan-retry.jsonl`, command item `item_3`. Final native validation: command item `item_34`.

### Separate-store planning — PASS

Proposal, behavioral specs, technical design, tasks, and native metadata were created under `planning-store/openspec/changes/normalize-article-whitespace/`. Planning records the concrete code repository separately. No corresponding change was created in `store-project/openspec/changes/`. Native strict validation and all four baseline tests passed; the evaluator explicitly did not claim the missing regression behavior was qualified. Source/tests remained unchanged after planning (`results/store-project-after-plan-source-diff.txt`, exit 0).

Actual Ponytail read: `store-plan.jsonl`, command item `item_2`. Final native validation: command item `item_40`.

### Conditional documentation planning — PASS

The evaluator created `conditional-project/openspec/changes/document-cli-usage/` with proposal/tasks and native metadata containing `skip_specs: true`. It created neither invented behavioral specs nor unnecessary technical design. Native strict validation passed; the final handoff stated that the omitted design still appears incomplete in native status. README and product source/tests were not edited during planning. The existing four tests and actual Hello World CLI output were checked.

Actual Ponytail reads: `conditional-plan.jsonl`, command items `item_4` and `item_6`. Final native validation: command item `item_22`. This is a conditional-artifact planning result, not implementation/archival of the documentation change.

### Ambiguity, read-only status, and missing-evidence finish — PASS

The untargeted work evaluator named both candidates and requested selection. It did not select the newest or begin either scope. The fresh status session reported both incomplete plans and exact next plan commands. The negative finish evaluator found only a scaffold, refused archive, and directed to planning.

The full 68-file digest maps are identical before and after ambiguity/status (`results/gates-after-status.json`) and after negative finish (`results/gates-after-negative-finish.json`). Both changes remain active; archive contains only the original `.gitkeep`. These results establish no-write behavior and a missing-evidence gate, not stale-evidence or positive database acceptance.

### Updated-candidate first-use status — PASS

The fresh `status-retest` evaluator itself supplied `OPENSPEC_TELEMETRY=0` to native context, list, and both change-status calls (command items `item_7`, `item_8`, `item_10`, `item_11`). The runner had deliberately removed that variable from its inherited environment. All calls exited 0. The full 68-file project snapshot stayed identical, and neither previously nonexistent `read-only-config/` nor `read-only-data/` was created. See `results/status-retest-after.json` and the actual command transcript.

### Custom task-path work — PASS

The fresh work evaluator loaded actual Ponytail (`custom-work.jsonl`, command `item_1`), used native apply with `eval-custom`, and completed all six tasks in `work/steps.md`. It reproduced seven domain whitespace failures, then the corresponding caller failures, before the one-line domain fix. It preserved CLI/preview/application interfaces, import boundaries, empty-input behavior, Unicode behavior, and private telemetry. Final suite: seven methods passing, covering 18 title cases across the four existing paths. An independent scorer rerun also passed all seven methods and additional mixed-whitespace/Unicode, whitespace-only, and unchanged-hyphen assertions (`results/custom-scorer-tests.txt`, `results/custom-scorer-edges.txt`).

The change's `verification.md` records actual RED/GREEN logs, source/test/configuration identities, acceptance mapping, and semantic review. Raw logs use the explicitly based path `custom-project/artifacts/development/fix-slug-whitespace-normalization/work-20261009/`. No shadow `tasks.md` was created. Native strict validation passed. `.gitignore` excludes the owned raw evidence directory; product implementation remains the shared normalization expression and its tests.

### Separate-store work — PASS

The fresh work evaluator loaded actual Ponytail (`store-work.jsonl`, command `item_5`) and resolved five tasks from `eval-store`. Product implementation and tests changed only in `store-project`; tasks and `verification.md` stayed under `planning-store`. Source implementation is the same single shared normalization expression.

Before the fix, the recorded full RED run had 144 expected failing subtests (108 domain/application/preview, 36 CLI); unchanged compatibility, import boundaries, help, and argument errors passed. After the fix all ten test methods passed, covering 15 title cases, all 29 whitespace characters recognized by the fixture's Python runtime, all callers, exact stdout, private JSON telemetry, help, and argument errors. An independent scorer rerun passed all ten methods plus additional required edge cases (`results/store-scorer-tests.txt`, `results/store-scorer-edges.txt`).

The retained report declares repository and evidence path bases, code/test/configuration/accepted-artifact hashes, RED/GREEN commands/results, and actual engineering review. Raw evidence is under `results/store-work-normalize-article-whitespace/`. All five task criteria are marked complete; native apply reports `all_done`. That status was corroborated by the recorded checks rather than treated as sufficient proof.

### Custom and separate-store finish — PASS

Both fresh finish sessions checked current recorded file identities and evidence before synchronization. The store evaluator also reran its ten-method suite. Each presented the concrete sync summary and treated the explicitly requested `$dev finish` operation as authorization for its documented sync/archive action. No additional permission question was asked or fabricated; there was no unresolved material choice. The custom evaluator acknowledged the deliberately omitted conditional design and used its accepted rationale.

Actual event order is retained in `results/sync-archive-order.json`. Custom main-spec write was `item_23`, successful strict validation `item_25`, then archive move `item_27`. Store main-spec creation was `item_29`, successful main-spec strict validation `item_30`, then archive move `item_32`. Later validation also passed. The complete change directories moved, retaining all native metadata and verification reports.

The scorer independently verified:

| Fixture | Result |
|---|---|
| Custom schema | Archive at `custom-project/openspec/changes/archive/2026-10-09-fix-slug-whitespace-normalization/`; five files retained; `work/steps.md` exists and no shadow `tasks.md`; main spec contains exactly the same four requirement blocks and 16 scenarios. |
| Separate store | Archive at `planning-store/openspec/changes/archive/2026-10-09-normalize-article-whitespace/`; six files retained; main spec contains exactly the same five requirement blocks and 17 scenarios; no corresponding main spec/change was created under the code repository. |

Both active change paths are absent after archive. Scorer `openspec validate --all --strict --json --no-interactive` calls exited 0, with `--store eval-store` for the separate-store case. Source/evidence path bases in archived verification still point to the unchanged target repository and retained raw results. Native change-relative links remain valid. See `results/scorer-archive-checks.json`, both `<project>-scorer-native-validation.txt` files, and the finish transcripts/final handoffs.

Overall S07 custom-task and separate-store lifecycle cases passed through planning, test-first work, current verification, successful sync, and archive. The bounded documentation case passed conditional-artifact planning only. S03 ambiguity/status and the missing-evidence negative finish case passed independently; they do not substitute for other adoption, stale-evidence, UI, or database scenarios.

## Limits

These fixtures have no UI or database. This report supplies no browser, copied-database, restaurant-project, or production acceptance claim. Temporary raw evidence paths are local to this evaluation environment. No global `dev` discovery/installation is established by explicit candidate-path invocation.

The custom fixture was subsequently reused for the [stale-evidence negative evaluation](2026-10-09-stale.md). Its successful archive snapshot is preserved at `results/stale-original-archive/`, and its active source was intentionally regressed after the positive results above. Those earlier results are historical evidence, not a claim that the subsequently modified fixture still passes. The separate-store fixture remains unchanged by that negative case.
