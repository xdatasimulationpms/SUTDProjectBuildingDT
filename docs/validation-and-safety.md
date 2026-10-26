---
type: Decision Framework
title: "Validation and Safe Use of Research Results"
description: "Checks required to interpret the prototype and the boundary between research comparisons and operational evacuation planning."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
stale_after: 2027-01-26T00:00:00Z
sources:
  - id: scdf
    resource: https://www.scdf.gov.sg/fire-safety-services-listing/plans-submission-process/performance-based-approach-to-fire-safety-design/performance-based-plan-approval-process
  - id: jupedsim
    resource: https://www.jupedsim.org/stable/disclaimer.html
---
# Validation and Safe Use of Research Results

Status checked: 2026-10-26

The project should produce understandable experiments, not reassuring animations without evidence. **Verification** asks whether the software implements the intended rules. **Validation** asks whether the model is sufficiently representative for the stated use. Both are needed, and neither is achieved by a successful run alone.

## Proposed test ladder

| Level | Example checks | Evidence to keep |
|---|---|---|
| Source integrity | Original hash unchanged; correct edition/floor; supplied dependencies known | Intake record and manifest |
| Information retention | Required elements, relationships and properties survive extraction | Counts, representative comparisons and explicit exclusions |
| Geometry | Units and transforms correct; valid polygons; door openings preserved; no unintended floor overlap | Reference dimensions and floor overlays |
| Semantics | Directed connections correct; source/evidence references present; unknown stays unknown | Small labelled reference topology and reviewer notes |
| Adapter consistency | Scenario restrictions apply to graph and simulator; unsupported cases are rejected | Tests with blocked, unknown and disconnected passages |
| Simulation verification | No unexplained agent creation/loss; boundary restrictions respected; stopping conditions correct | Logs, trajectories and test results |
| Behavioural validation | Compare relevant model outputs with suitable empirical evidence or accepted benchmarks | Dataset/benchmark provenance, calibration choices and held-out evaluation where possible |
| Intended-use review | Results and model omissions appropriate to the decision being considered | Domain review and explicit restrictions on use |

Start the reference topology by hand on the fictional floor. Later, have a building reviewer independently label a small real-model test set. Do not evaluate the extractor only against labels created by the same extraction algorithm.

## Minimum failure cases

1. **Wrong units:** a model expressed in millimetres must not be interpreted as metres.
2. **Missing spaces:** report the gap and stop or use a reviewed fallback; do not silently invent `IfcSpace` records.
3. **False adjacency:** touching room boundaries without a passage must not create a traversal edge.
4. **Floor confusion:** a door near a stair on another level must not become a same-floor shortcut.
5. **Unavailable passage:** changing a scenario cannot leave the doorway usable in the simulator.
6. **Unknown dimension:** missing required clearance cannot become an assumed passing value.
7. **Isolated population:** people with no eligible target route remain counted and visible.
8. **Run limit:** stopping at the configured horizon cannot be reported as complete evacuation.
9. **New edition:** changed or deleted source elements invalidate affected mappings and prompt review.
10. **Repeatability:** a second person can explain and reproduce the accepted case within a documented tolerance.

Choose numeric tolerances with the reviewers before evaluating results. Record why they fit the geometry, model and research question; do not invent a universal “safe” threshold.

## Measurement and uncertainty

Define the counting boundaries, time origin, density/queue measurement method and outcome criteria. Keep failed, invalid, incomplete and completed runs separate. Report how many people reached which targets and how many remained.

Vary uncertain inputs such as population, starting distribution, movement parameters and response assumptions. Keep the seed list and number of repetitions. Check whether the apparent ranking of scenarios changes under plausible assumptions rather than reporting one favoured run.

A second simulator can reveal implementation or modelling differences, but agreement between two simulators is not proof of real-world validity. Calibration on one dataset also does not validate every building or occupant group.

## What the first prototype cannot establish

- It does not model smoke, heat, visibility loss or the time until conditions become untenable.
- Movement-to-target time does not include every detection, alarm, decision and response delay unless those are explicitly modelled.
- Reaching a floor exit or stair landing is not a whole-building evacuation result.
- A generic pedestrian agent does not establish behaviour for mobility limitations, assisted evacuation, groups or emergency responders.
- A static building record does not prove present operating conditions.

Do not derive a safety margin by comparing the movement result with an invented hazard deadline. Hazard and evacuation assessment require an appropriate method and specialist review beyond this prototype.

## Boundary before operational use

JuPedSim's publisher explicitly cautions about academic intended use and the consequences of erroneous life-safety predictions.[^jupedsim] A product investigation must therefore assess engine suitability separately, including model scope, validation evidence, licence, maintenance and support.

In Singapore, SCDF's performance-based fire-safety design process identifies roles for the building owner, Qualified Persons, a Fire Safety Engineer and a peer reviewer, with formal documentation and review steps.[^scdf] That design-approval process is not identical to every evacuation-planning task, but it demonstrates why a research simulation is not an approval route by itself. Consult the appropriate qualified professionals and responsible authorities for the actual intended use.

Before moving beyond research, agree the use case, model coverage, evidence, limitations, review responsibilities and governance for changes. Do not issue live directions, approve a building, or amend an emergency plan automatically.

Every research report should state: **scenario assessment only; not an approved evacuation plan**. Use the [experiment report template](../templates/experiment-report.md).

[^jupedsim]: [JuPedSim disclaimer](https://www.jupedsim.org/stable/disclaimer.html).
[^scdf]: [SCDF performance-based plan approval process](https://www.scdf.gov.sg/fire-safety-services-listing/plans-submission-process/performance-based-approach-to-fire-safety-design/performance-based-plan-approval-process).
