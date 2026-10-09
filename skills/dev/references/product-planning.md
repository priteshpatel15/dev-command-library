# Product design and roadmap

## Purpose and use

- Use for `$dev design` and `$dev revise --effort`.
- Define the product experience and delivery outcomes; each selected OpenSpec change owns its detailed technical solution and tasks.
- Load and apply actual Ponytail through [command routing](../SKILL.md#command-routing); honor its loading and override rules.
- Apply [engineering requirements](engineering-and-verification.md) to architectural decisions and acceptance.
- Design does not require OpenSpec initialization or invoke `specify-product` / `develop-product` workflows.

## Inputs

- User goal, selected effort, or revision feedback.
- Target repository, governing instructions, and current product behavior.
- Existing design, requirements, scenarios, decisions, roadmap, and delivery evidence.
- Constraints, accepted scope, and unresolved material decisions.

## Discovery

- Inspect relevant source, interfaces, tests, configuration, and retained evidence.
- Trace affected user actions to actual interfaces and data effects before proposing reuse or replacement.
- Distinguish observed behavior, accepted requirements, and proposed changes.
- Ask about unresolved choices that materially affect scope, behavior, or acceptance; record routine defaults as proposals.

## Product design

- Define the goal, users, operating context, observable success, and scope boundaries.
- Describe complete supported journeys and relevant empty, loading, error, permission, and recovery states.
- Specify data effects, compatibility, accessibility, and other accepted quality requirements.
- Identify meaningful module/component ownership, dependency direction, and evidence-backed reuse opportunities.
- Preserve requirement/scenario IDs and define observable acceptance outcomes.
- Record accepted decisions, justified deferrals, and material open questions; deferral does not remove an accepted requirement.
- Add screens, interaction examples, or diagrams when they clarify behavior.

## Outcome roadmap

- Give each outcome a stable ID, observable result, dependencies, acceptance boundary, and links to its OpenSpec changes.
- Prefer complete user outcomes over separate frontend/backend phases.
- Allow several bounded changes for a large outcome; detail only the next selected change through `$dev plan`.
- Mark an outcome ready only when prerequisites are satisfied and material decisions are resolved.
- When several outcomes qualify, use an explicit or unambiguous conversation selection; otherwise ask.
- Keep delivery intent in the roadmap, implementation tasks in OpenSpec, and acceptance proof in verification records.
- Link verified delivery evidence; claim an outcome complete only when its full acceptance boundary is covered.
- Do not duplicate task checklists or invent independent completion percentages.

## Outputs

- Reuse suitable canonical documents; create only missing artifacts.
- Default design: `docs/development/<effort-id>/design.md`, using the [design template](../assets/templates/design.md).
- Default roadmap: `docs/development/<effort-id>/roadmap.md`, using the [roadmap template](../assets/templates/roadmap.md).
- Adapt templates to the effort; omit inapplicable sections and link existing requirements rather than copying them.
- Keep design and roadmap links explicit about the target repository and path base.

## Adopt an existing effort

- Identify canonical documents, code, tests, and retained evidence; preserve accepted IDs, scenarios, dependencies, and reusable implementation.
- Add a crosswalk only when needed to connect old groups to roadmap outcomes; reuse existing crosswalks.
- Classify work as verified, implemented pending verification, or remaining using actual source and evidence.
- Never treat checkmarks, prototypes, process labels, or mock-only results as integrated acceptance.
- Preserve existing designs and completed work; adoption normally adds a missing roadmap rather than recreating the effort.
- Name superseded execution instructions and their replacement; retain historical requirements and evidence.
- Keep one current delivery authority; legacy automatic-continuation rules must not expand the selected scope.
- Preserve protected or hash-approved source packages; propose an explicit amendment when a change is needed.

## Effort revision

- Update only the selected canonical design/roadmap within the authorized feedback scope.
- Preserve accepted behavior and acceptance unless the user explicitly changes them.
- Identify affected OpenSpec changes and potentially stale implementation/evidence; report impacts without editing their artifacts implicitly.
- Use separately selected change revision for detailed technical decisions, task reopening, and evidence invalidation.
- Do not imply automatic import/export with `specify-product` packages or bypass their approval process.

## Handoff to plan

- Present exact artifact paths, unresolved material decisions, and one next command; stop for review without implementing.
- After review, recommend `$dev plan <effort-id>/<outcome-id>` for one selected outcome; run plan only when requested.
- Let plan read the source documents directly and link the effort/outcome and target repository in the native change; do not create a prompt packet.
- If OpenSpec is absent, direct to `$dev setup` before plan; do not initialize it implicitly.
- Allow a clear, bounded standalone fix to enter plan without creating a product design or roadmap.
