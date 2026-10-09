# Installed setup preserves existing project authority

Evaluation date: 2026-10-09. Case: S01 repeated setup with custom schema and existing configuration. Fixture/scorer: `library_documentation`; evaluators: two separate fresh ephemeral Codex sessions. Neither evaluator prompt supplies a candidate skill path or an expected outcome.

## Fixture and identity

Evidence base: `/private/tmp/dev-library-setup-idem-r5npefmi/`. All receipt paths below are relative to that directory. The selected project is `project/`; its initial complete file snapshot is `results/before.json`.

Before evaluation the runner created:

- Existing `AGENTS.md` with original instructions and `ORIGINAL-AGENTS-SENTINEL`.
- `src/example.py` and an unrelated `fixtures/unrelated.txt` sentinel.
- Native OpenSpec initialization with `openspec init --tools codex`.
- A project-local schema fork using `openspec schema fork spec-driven eval-custom --json`.
- Configuration selecting `schema: eval-custom`, original context text, a proposal rule, and apply guidance, each with a distinct sentinel.

Native preparation commands exited 0; their receipts are `results/native-init.txt` and `results/native-fork.txt`. Original authority is retained in `results/original-AGENTS.md` and `results/original-config.yaml`. The schema fork and generated OpenSpec skills are part of the protected project snapshot.

Both evaluators invoke the **globally installed** `$dev`. Its resolved source and exact per-file SHA-256 identity are recorded in `results/installed-identity.json`. OpenSpec config/data are isolated under the evidence base using `XDG_CONFIG_HOME` and `XDG_DATA_HOME`. `HOME` and `CODEX_HOME` are unchanged. No dependencies were installed or globally configured by this test.

## Actual requests

Each fresh session receives `$dev setup`, the concrete temporary project path, a temporary-only write boundary, and the isolated XDG paths. The exact identical prompts are retained in `results/setup-1-prompt.txt` and `results/setup-2-prompt.txt`. No explicit skill file path or hidden answer key is provided.

Raw tool transcripts: `results/setup-1.jsonl` and `results/setup-2.jsonl`. Final handoffs and launcher diagnostics use the corresponding `-final.md` and `.stderr` filenames. Complete post-operation snapshots are `results/after-1.json` and `results/after-2.json`; actual config and instruction contents are also retained after each run.

## Result

**PASS.** Both fresh sessions completed successfully through the installed skill. Executed reads of the resolved installed `dev/SKILL.md` appear in run 1 command `item_3` and run 2 command `item_1`; no candidate path was supplied in either prompt.

Independent scoring parsed the retained YAML using an already installed PyYAML library and compared complete project file digests:

| Check | Observed result |
|---|---|
| First setup mutations | Exactly `AGENTS.md` and `openspec/config.yaml`; a bounded workflow section and references were added. |
| Custom schema | `schema: eval-custom` after both runs; the forked schema and all templates are byte-identical to their initial contents. |
| Existing configuration | Original context text remains intact; original proposal rule and apply guidance remain members of their original fields. Each sentinel occurs exactly once. |
| Existing instructions | Complete original `AGENTS.md` text remains present, with its sentinel occurring once. |
| Unrelated files | Example source, unrelated fixture, generated skills, and every other original project file are unchanged. |
| Second setup | All **36 project files** are byte-identical to the first-run snapshot; no paths were added or removed and no workflow section was duplicated. |
| Native checks | Both sessions inspected the native root and configured schema. The repeated run's native health/schema/template checks passed without creating a change. |

The second evaluator explicitly reported that the existing workflow section and guidance were sufficient and made no edits. Its next action was `$dev design "<goal>"`. Detailed field checks, observed installed-skill read items, and native-command receipts are retained in `results/scorer-result.json` alongside the full before/after snapshots.

## Limits

This is configuration and instruction setup coverage. The fixture has no UI, database, or product acceptance requirement; no application behavior test is needed or claimed. Library discovery and actual instruction loading are assessed from executed tool activity rather than the agent's assertion alone.
