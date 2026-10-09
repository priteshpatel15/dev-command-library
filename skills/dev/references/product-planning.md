# Product design and roadmap

Read with actual Ponytail and the relevant command contract. Use the useful product-definition concepts from `specify-product`: purpose, people, journeys, constraints, acceptance and delivery outcomes. This library does not invoke its compiler, hash-approval runtime, program manifests, execution packets or `develop-product` handoff. Keep that original skill intact.

## Design a new effort

Inspect the current product where one exists. Trace the relevant user actions to actual interfaces and data effects before declaring reuse or replacement. Distinguish observed behavior from proposed behavior.

Clarify decisions that materially change the product or acceptance. State routine defaults. Record:

- Goal, users, operating context, success criteria and explicit boundaries.
- Complete user journeys and observable outcomes, including important empty/loading/error/permission/recovery states.
- Supported behavior, data effects, compatibility and accessibility expectations.
- Meaningful component boundaries, ownership and dependency constraints; reuse opportunities grounded in the project.
- Acceptance outcomes and any unresolved material decisions.

Use [the design template](../assets/templates/design.md) when no equivalent canonical document exists. Adapt sections to the actual effort; omit inapplicable ceremony. Screens, interaction examples and diagrams belong here when they clarify decisions. Do not prescribe exact implementation tasks for the whole roadmap.

Ponytail at design asks whether proposed complexity is necessary to the requested experience. It can identify optional/deferred ideas; it cannot silently remove accepted requirements. Clean Architecture does not imply a new service, package or interface for each noun.

## Roadmap

Use [the roadmap template](../assets/templates/roadmap.md). Give each outcome a stable ID, an observable result, dependencies, acceptance boundary and change links. Prefer complete user outcomes over isolated frontend/backend phases. A large outcome can need several bounded OpenSpec changes. Plan detailed work only for the next selected change.

Readiness means prerequisites are satisfied and material decisions for that slice are resolved. Several ready outcomes require explicit selection when no conversation target disambiguates. A direct bounded bug can bypass product documents and enter plan.

The roadmap owns delivery intent and dependencies. Native tasks own implementation progress. Verification owns evidence. Do not duplicate checklists or invent independent completion percentages. A delivery note links verified change evidence; an outcome is complete only when its entire acceptance boundary is covered.

## Adopt an existing effort

1. Identify canonical design, requirements, acceptance matrix, decisions, code, tests and retained receipts. Record their paths; don't copy their full contents into new documents.
2. Preserve accepted IDs, scenarios, dependencies and reusable implementation. Build a crosswalk only where needed to map old groups to outcome IDs; retain existing crosswalks by reference.
3. Classify work as verified, implemented pending verification, or remaining from actual source and evidence. A checkmark, old process label, prototype or passing mock suite does not prove current integrated acceptance.
4. Create only missing roles, normally a new roadmap referencing the existing design. Keep approved or hash-governed source packages intact; an intentional amendment is separate from importing delivery links.
5. Explicitly identify superseded execution directions and their replacement. Preserve historical requirements and receipts. Avoid leaving two documents claiming to be the current execution authority. Never let legacy automatic continuation expand a new single-change request.
6. Select one bounded remaining outcome for plan. Do not restart completed work to change its document format.

## Revisions

Product-level feedback updates the selected canonical design/roadmap and identifies affected active change plans. Preserve acceptance unless the user explicitly changes it. Technical decisions within accepted behavior stay in the change's technical design.

When source documents are protected by another approval process, propose an explicit amendment instead of rewriting them through adoption. Do not imply that OpenSpec automatically exports or imports a `specify-product` package.

## Handoff to plan

The roadmap row and linked product design are the inputs; the user need only name the outcome. Plan reads the source files directly. The resulting native proposal links its effort/outcome and code repository. No copy-paste prompt packet or new controller is required.
