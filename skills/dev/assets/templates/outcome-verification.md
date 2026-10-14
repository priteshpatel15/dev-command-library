# <Effort>/<Outcome>: qualification

## Result

- Result: `<qualified / failed / blocked>`
- Assessed at: `<timestamp and timezone>`
- Target repository/worktree: `<identity>`; path bases: `<bases>`
- Outcome gate: `<command or scenario set named in the roadmap / AGENTS.md>`
- Slices: `<each finished change name and archive path>`

## Tested identity

- HEAD: `<git rev-parse HEAD>`
- Diff hash: `<git diff HEAD | shasum>`
- Untracked hash: `<git ls-files --others --exclude-standard | sort | shasum>`

## Outcome gate run

| Stage | Result | Receipt |
| --- | --- | --- |
| `<migrations / fixtures / units / postgres / builds / browser / preservation>` | `<passed n / failed n / skipped>` | `<harness-owned path>` |

- Command: `<exact command, started/finished, exit code>`
- Copied-database proof: `<manifest, database identity, clone marker, connection identities per process>`
- Browser matrix: `<devices, accessibility/zoom/motion states covered; failures by scenario ID>`
- Preservation and isolation: `<independent assertions and results>`

## Defects

| Scenario / requirement | Observed | Routed to |
| --- | --- | --- |
| `<ID>` | `<failure with receipt>` | `$dev plan "<defect>"` |

## Next action

- `<one copyable $dev command: the first defect's plan, or the next ready outcome>`
