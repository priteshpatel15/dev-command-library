# 2026-10-13 — Speed rules (1.1.0): validation record

## Candidate

- Branch `dev-library-speed` from `c08c494`, worktree `/private/tmp/dev-library-speed`.
- Changed: `SKILL.md`, `references/{commands,engineering-and-verification,openspec-workflow,product-planning,architecture,maintenance}.md`, `assets/templates/{verification,roadmap}.md`, new `assets/templates/outcome-verification.md`, `README.md`, `tests/scenarios.md` (S09).
- Behavioral classification: command behavior and completion rules changed (size budget, ordered work sequence, change map, single review, two-tier gates, new `qualify`, cheaper tested identity).

## Why

Codex session logs for `restaurant_data_integrator` W01/W02 (`~/.codex/sessions/2026/10/08/rollout-…01a11d81….jsonl` and two reviewer subagent sessions) showed: W02 `work` ran 4 h+ with ~6 min of tool execution; a reviewer subagent forked with the whole conversation received 25 follow-ups (34M input tokens); nine full harness runs each stopped at one failing scenario; 47 background polls; a 108-line verification record with hash manifests of 636 files; 14 compactions in one thread with repeated re-reads of all six Ponytail skills. The 1.1.0 rules target each cause.

## Checks executed

| Check | Result |
| --- | --- |
| Frontmatter (`name`, `description`, `metadata.version` 1.1.0) | Inspected; well-formed. `skill-creator` validator not installed on this machine, so no automated format validation was run. |
| Relative links and `#anchors` across `skills/dev/**/*.md`, `README.md`, `tests/*.md` | Script resolved every target file and heading: 0 issues. |
| Command/routing consistency | Every command in `commands.md` has a routing row in `SKILL.md`; `qualify` added to both, to the state table, sequences, README, and architecture lifecycle. |
| Template references | `verification.md` and new `outcome-verification.md` linked from engineering reference and architecture. |

## Not executed

- S09 live scenarios (slice, change map, single review, finish-without-outcome-gate, qualify) and regression reruns of S02/S05/S06 were **not executed** in this validation. First live use on a sliced change is the measurement; record it here when run.
- Claude Code fresh-session discovery of `/dev` was confirmed earlier today for 1.0.4 via the symlink; not repeated for 1.1.0.

## Limitations

- Instruction-only change; no runtime enforces the size budget or single-review rule. Project `AGENTS.md` must name the change-gate fast path and the outcome-gate command for the tiers to work as designed.
