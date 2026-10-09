# Explicit skill routing validation — 2026-10-09

- Baseline: `0ef3091b490a06e4833ca656dec5a8ca36f8be78`; clean source at inspection.
- Candidate: `/private/tmp/dev-skill-routing-1wo94pps/dev`, metadata version `1.0.4`.
- Scope: explicit per-command Ponytail/OpenSpec selection and consistent reference boundaries. No executable or product changes.

## Observed checks

- PASS — `.venv/bin/python /Users/po/.codex/skills/.system/skill-creator/scripts/quick_validate.py /private/tmp/dev-skill-routing-1wo94pps/dev` from the product repository; exit 0, `Skill is valid!`.
- PASS — one-off Python inspection resolved all 39 package-local Markdown links and heading anchors.
- PASS — every routed skill exists and its YAML name matches: six OpenSpec skills and Ponytail core/review. OpenSpec files were read from the product's `.agents/skills`; Ponytail files were read from the installed plugin catalog location.
- PASS — `OPENSPEC_TELEMETRY=0 openspec --version` returned `1.14.1`; current help and native skill instructions support the mapped operations.
- PASS — candidate comparison identified only the three intended package files below; other package files are byte-identical to baseline.
- PASS — independent static review by `/root/command_library_review`: exact skills, conditional exploration, Ponytail overrides/review freshness, evidence-only verification, effort revision scope, and archive-owned synchronous synchronization.
- Resolved finding — qualified task reopening/evidence invalidation as change-level revision only. Effort revision reports impacts for separately selected changes. Reviewer confirmed the correction.

## Candidate identities

Paths below are relative to `skills/dev/` in the source repository.

| File | SHA-256 |
| --- | --- |
| `SKILL.md` | `a15d4d01503a8538199329a972f37aa8beadc178c4a9351cadcc322054cb74ab` |
| `references/engineering-and-verification.md` | `7ee8f52fcbb0195baf16d7d0b7e1d4b016f4ff6c31a8a9ccafd0dbe978fb359d` |
| `references/openspec-workflow.md` | `d739825840bbc2bb8d7841d7728e21d46a9bcfc24a336fc1dac84e6146a7f957` |

## Limits

- No fresh-session discovery or complete plan/work/verify/finish behavioral evaluation was run for this instruction update. Static review does not establish runtime behavior.
- No product, browser, or database tests were run; this update changes skill instructions only.
- These are instruction-based routing requirements, not an executable enforcement mechanism. Agents must load the actual installed skills; stale sessions may need a fresh skill load.
- Existing lifecycle evidence remains historical and is not relabeled as testing this candidate.
