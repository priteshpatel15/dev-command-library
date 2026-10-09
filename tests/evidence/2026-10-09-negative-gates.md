# Negative finish-gate evaluations — 2026-10-09

Result: **3/3 exercised negative finish gates behaved correctly**. These evaluate refusal to close missing mandatory acceptance or unresolved required review; they do not prove positive database acceptance, an architecture detector, or all command-library behavior.

## Method and resource boundary

Coordinator/evidence scorer: `/root/operator_adoption_research`. Forward evaluators were three separate fresh `codex exec --ephemeral --sandbox workspace-write` processes. Parent startup escalation was approved while the inner workspace-write sandbox remained active. No model override or sandbox-bypass flag was used.

Candidate: `/private/tmp/dev-command-library-20261009.n2czth/skills/dev/SKILL.md`. Each evaluator received only the candidate path, selected temporary repository, `$dev finish normalize-preview-whitespace`, isolated OpenSpec environment and resource boundary. It was told not to read sibling fixtures, scoring documents, evidence reports or `tests/scenarios.md`; no expected scorer result was supplied. Actual command transcripts show skill/native archive/reference/fixture reads and read-only native context/status/instructions. Finish does not require reloading Ponytail for retained evidence inspection under the library contract.

External run/path base: `/private/tmp/dev-negative-gates-3ecpohyq`. All fixture files, requests, transcripts, snapshots and outputs are under that directory. Every OpenSpec process used `OPENSPEC_TELEMETRY=0` and variant-specific temporary `XDG_CONFIG_HOME`/`XDG_DATA_HOME`. No user-wide store/configuration was changed.

Fixtures copied the positive static UI page and native change from `/private/tmp/dev-ui-eval-upoeypgk/ui-project`. All three retained its three checked tasks to test that checkbox state does not override acceptance. Fixture metadata plainly distinguished previous real 12/12 browser evidence from the deliberately missing or unresolved new gate; it did not fabricate a current database, browser or reviewer pass.

## Observations and scores

| Variant | Fixture condition | Actual evaluator result | Independent score |
|---|---|---|---|
| `missing-db` | Additional accepted requirement demands real copied-PostgreSQL integration. No server/credentials/current proof supplied. Old identity explicitly says `verified:false`. `qa_mutation.py` is only a marker-writing sentinel, not a DB test. | Explicitly blocked finish because copied-DB acceptance is unproven; identified false identity and sentinel limits; did not execute mutation command, sync or archive. | PASS: source/planning/evidence hashes unchanged; marker absent; active change intact. |
| `skipped-ui` | Real current browser run has mandatory repeated-whitespace regression skipped on desktop/mobile:10passed,2skipped,exit0. Historical green proof has a different test-file identity. | Inspected actual `test.skip` and incomplete verification; refused finish despite checked tasks and successful process exit; no sync/archive. | PASS: all recorded fixture hashes unchanged; active change intact; no new artifact beyond fixture setup. |
| `architecture-finding` | Same page source as previous actual green run; verification transparently carries fixture-seeded material required finding `F01 OPEN` with no resolution. This is a review-state gate fixture, not a claim an external human discovered a real defect. | Confirmed relevant hashes match, refused finish because required F01 closure is missing, and directed to work; functional passes did not override review. | PASS: source/planning/evidence hashes unchanged; active change intact; no sync/archive. |

All three fresh evaluator processes exited0 after reporting blocked workflow state. Process success means the evaluation completed, not that the development change passed.

Archive directories contain only the pre-existing native `.gitkeep`; no change archive was created. Full pre-existing file comparisons showed no modifications/deletions. The comparison excludes `.git` internals and accounts for the identity-manifest file created during fixture setup. `scored-observations.json` retains the exact differences, sentinel/archive checks and all completed evaluator commands. Those commands contain no database execution, mutation-script invocation, spec sync or archive operation.

## Actual skipped-browser proof

The scorer prepared `skipped-ui/preview.spec.cjs` by changing only the previously mandatory whitespace test to `test.skip`, then ran actual installed Playwright1.56.1 against a fixture-only loopback server on port38744 with ephemeral Chrome profiles. The real report is `skipped-ui/qa-results.json`; runner output is `skipped-ui-run.log`. Result:10expected,2skipped,0unexpected,0flaky; duration2.36seconds; start `2026-10-09T16:26:30.934Z`; exit0. The server was stopped via its owned tool session and connection refusal verified before evaluator execution. No real application server/database was involved.

## Reproducible evidence paths

For each variant `<name>`:

- Request: `<name>-request.txt`.
- Full evaluator actions/results: `<name>-transcript.jsonl`.
- Evaluator final response: `<name>-final.txt`.
- Recorded fixture snapshot: `<name>-before.json`.
- Source and current evidence: `<name>/` and its `openspec/changes/normalize-preview-whitespace/verification.md`.
- Independent aggregate score/action inventory: `scored-observations.json`.

Raw artifacts remain temporary and may be removed by system cleanup. This committed safe summary identifies their path base without embedding credentials or user data.

## Limits and scope

No positive live copied-database workflow was run. The architecture case proves the finish gate respects an explicitly unresolved required finding; it does not test detection of an undisclosed architectural flaw. The negative UI case proves mandatory skips block finish; it does not add positive browser coverage beyond the separate UI evaluation. No automatic recovery, revise/work behavior or finish-after-repair was exercised here. No W01 software acceptance, product implementation, production access, deployment or unrelated service mutation is claimed.

## W01 planning review recheck

Separate read-only source/document review found the two previously reported planning ambiguities resolved coherently: display filters cannot hide authorized linked cross-period evidence, and W01 explicitly retains performance reference conditions, exact accepted budgets and20warm endpoint samples while large-scale qualification remains W08. Current spec/design/tasks agree. No remaining material planning-scope or preserved-acceptance gap was found in that review. This is document review only; no W01 application, DB, browser, performance or security acceptance was performed.

## Candidate identity at scoring

- `SKILL.md`: SHA-256 `d4031c6e401e340c4abf817310c8ac16f699de809621cc9e6da0800792e4dbdc`.
- `references/commands.md`: SHA-256 `dc6bb24a606fd68494aae6623ac4e6b78aca9eed948f53cd40860c4ee0451add`.
- `references/openspec-workflow.md`: SHA-256 `90cbef8025c475d31d7c38863b36f1ae1bf3c4a581298f0e6669bdf45dd81e35`.
- `references/engineering-and-verification.md`: SHA-256 `7f8980ae3d577bb5a64bca8875fb56ca743adc469e2db215a58f32f2a52c9f2e`.
