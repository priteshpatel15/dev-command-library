# <Change>: verification

## Result

- Result: `<incomplete / passed / failed / stale>`
- Assessed at: `<timestamp and timezone>`
- Target repository/worktree: `<identity>`; planning home/change: `<native location>`
- Path bases: `<bases for source and evidence references>`
- Governing instructions: `<project/nested rules and accepted requirements>`
- Skills: `<dev version; ponytail / ponytail-review versions; overrides>`

## Tested identity

- HEAD: `<git rev-parse HEAD>`
- Diff hash: `<git diff HEAD | shasum>`
- Untracked hash: `<git ls-files --others --exclude-standard | sort | shasum>`
- Invalidations: `<which checks were rerun since the previous identity, or none>`

## Change map

- Touch: `<files, callers, tests, fixtures, config, exports, contracts the change must reach>`
- Reuse: `<existing components by path>`
- Add: `<necessary additions and the boundary each protects>`
- Skip: `<deliberately omitted features, options, abstractions>`
- Change gate: `<focused commands; touched browser specs>`

## Checks

| Check | Command | Result | Receipt |
| --- | --- | --- | --- |
| `<unit / contract / boundary / spec>` | `<exact command>` | `<passed n / failed / skipped / not run>` | `<harness-owned path>` |

- Copied-database proof, when a check mutates data: `<guard receipt and connection identities>`
- Exclude credentials, connection secrets, unrestricted customer records, and raw traces.

## Review

- Method: `<ponytail:ponytail-review on diff hash …; independent reviewer only if project rules required it>`
- Findings and resolutions: `<introduced / affected existing / unrelated debt; what changed>`

## Gaps and finish eligibility

- Required gaps: `<failures, unrun checks, mandatory skips, stale results, unresolved required findings>`
- Finish eligible: `<yes / no, with the evidence-based reason>`
- Next action: `<one copyable $dev command>`
