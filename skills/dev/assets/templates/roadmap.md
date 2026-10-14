# <Effort name>: outcome roadmap

## Identity and authority

- Effort ID: `<stable-id>`
- Code repository: `<identity and path base>`
- Canonical design: `<link and current review status>`
- Requirements and acceptance: `<canonical links; preserve requirement/scenario IDs>`
- Authority: this roadmap owns delivery intent; linked OpenSpec tasks own implementation progress, change verification records own change-gate evidence, and qualification records own outcome-gate evidence.

## Outcomes

| Outcome ID | Observable result | Dependencies | Outcome gate | Slices | OpenSpec changes / delivery evidence |
| --- | --- | --- | --- | --- | --- |
| `<M01>` | `<complete user outcome>` | `<none or prerequisite outcome IDs>` | `<project command or scenario set proving the whole outcome>` | `<M01/slice-1 result; M01/slice-2 result; filled by plan>` | `<change links; qualification record once qualified>` |

- Each slice is one change within the [size budget](../../references/commands.md#size-budget); `plan` adds slices here and plans one at a time.
- An outcome is complete only when its qualification record passes; finished slices alone do not qualify it.
- Keep detailed tasks in OpenSpec; do not duplicate task lists or add independent progress percentages.

## Adoption and continuity

Include only when adopting existing work.

- Sources and crosswalk: `<canonical documents and existing mappings; add a mapping only when needed>`
- Verified foundations: `<completed scope with current supporting evidence>`
- Implemented pending verification: `<existing implementation and its acceptance gaps>`
- Remaining scope: `<accepted outcomes still to deliver>`
- Superseded execution instructions: `<previous rules and their replacement; preserve accepted behavior>`
- Historical evidence: `<links to retained results, including failed or superseded receipts>`

## Next selection

- Target: `<explicit/unambiguous outcome or slice, or existing change; list ready choices when selection is unresolved>`
- Readiness: `<satisfied prerequisites and resolved material decisions, or exact blockers>`
- Recommended command: `<one copyable $dev command for the observed state after target selection>`
- Run the next operation only when requested; do not start another outcome automatically.
