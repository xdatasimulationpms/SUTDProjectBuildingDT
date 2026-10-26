---
type: Template
title: "Evacuation Research Scenario"
description: "Define a reproducible experiment without changing the source building record."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Evacuation Research Scenario

Copy this template into `local-data/`. This is a planning record, not an executable simulator configuration or approved evacuation plan.

## Question and boundaries

- Scenario name and revision:
- Research question:
- Baseline scenario being compared:
- Included building edition, occupied floors, intermediate levels and areas:
- Included stair systems, flights, landings and route through the discharge level:
- Excluded floors/populations and their possible effects on shared stairs:
- Simulation target definition and what happens beyond it:
- Explicitly excluded behaviours, floors and hazards:

## Fixed inputs

| Input | Version or value and rationale |
|---|---|
| Source/model hashes | |
| Reviewed geometry and topology editions | |
| Movement profile and rules version | |
| Number and initial location of people on each floor | |
| Population and movement assumptions with evidence | |
| Route choice and knowledge assumptions | |
| Stair travel, direction and merging assumptions; evidence and engine mapping | |
| Response delays and time origin | |
| Engine, model, adapter and environment versions | |
| Seeds, time step, maximum run time and repetitions | |
| Outcome measures and comparison method | |

## Scenario changes

| Object or parameter | Baseline | Changed value | Assumption or evidence | How enforced in the engine |
|---|---|---|---|---|
| | | | | |

Use precise passage meanings: unavailable for use, leaf closed but openable, direction restricted, or unknown. State whether changes are static before the run; dynamic changes are outside the first prototype unless specifically implemented and tested.

## Checks before running

- [ ] All references point to the selected editions.
- [ ] Graph and simulator represent the same restrictions.
- [ ] Unknown required conditions are excluded or explicitly tested as separate assumptions.
- [ ] Initial people, stairs, landings and external target areas are valid for the engine.
- [ ] Every included occupied floor has a reviewed complete route or an explicitly reported no-route outcome.
- [ ] Floor clearance, stair entry/discharge and external arrival have separate definitions.
- [ ] Occupant identity and starting floor persist across level transfers; static-population counts balance.
- [ ] Isolated people, unsupported geometry and out-of-scope features are reported.
- [ ] Completion, incompletion and failure criteria are defined.
- [ ] Reviewer has checked the scenario for the stated research purpose.

Reviewer, date and unresolved questions:
