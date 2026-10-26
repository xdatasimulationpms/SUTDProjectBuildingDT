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
| Geometry | Correct floor elevations, transforms, openings, stairs and landings; complete discharge routes | Reference dimensions, per-floor overlays and stair-route inspection |
| Semantics | Correct horizontal and vertical connections, evidence and explicit unknowns | Labelled reference topology including complete stair routes |
| Adapter consistency | Scenario restrictions apply to graph and simulator; unsupported cases are rejected | Tests with blocked, unknown and disconnected passages |
| Simulation verification | No unexplained agent creation/loss during floor transfer; no instant stair jumps; restrictions and stopping conditions correct | Logs, per-occupant traces and counts across floors/stairs |
| Behavioural validation | Assess stair travel and merging, alongside suitable empirical/reference evidence for the selected movement model | Benchmark provenance, calibration choices and held-out evaluation where possible |
| Intended-use review | Results and model omissions appropriate to the decision being considered | Domain review and explicit restrictions on use |
| Toolkit contract | Valid/invalid tool inputs, structured outputs, jobs, retries, cancellation, errors and artifact access | Contract tests, tested module/adapter versions and reference-client traces |
| Agent-assisted integration | Toolkit discovers tools, runs a supported comparison and presents returned measurements accurately | Actual toolkit integration trace, artifact references and officer feedback |

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
11. **Stair mapping:** wrong elevation, missing flight or swapped landing must not create a valid route; arrival at a landing must not remove an occupant as a building exit.
12. **Transfer accounting:** an occupant retains identity and origin floor while moving through stairs; no person is duplicated, lost or counted as exited twice.
13. **Merging:** compare a shared-stair example with one floor feeding it and with multiple floors feeding it; inspect trajectories, queues and sensitivity to arrivals. Do not assume that a realistic-looking queue validates the model.
14. **Endpoint coverage:** every reported external arrival corresponds to the declared target; any excluded floors or missing stair demand are visible in the assessment.

Choose numeric tolerances with the reviewers before evaluating results. Record why they fit the geometry, model and research question; do not invent a universal “safe” threshold.

The [FDDE contract](toolkit-integration-contract.md#acceptance-demonstration) adds integration checks. Duplicate submission should return the existing job, stale validation should be rejected, and cancellation is reported complete only after confirmation. A local reference-client test establishes contract behaviour; a real toolkit run establishes the tested integration. Neither replaces the movement-model evidence above.

## Measurement and uncertainty

Define the counting boundaries, time origin, density/queue measurement method and outcome criteria. Keep failed, invalid, incomplete and completed runs separate. Report how many people reached which external targets and how many remained on floors or in stairs. Preserve origin-floor labels for completed and incomplete journeys.

Distinguish floor clearance, stair entry, stair discharge and external-target arrival. A cleared office floor may still have its occupants queued in a stair. For core scenarios with a fixed initial population, check that initial occupants equal people remaining in the model plus recorded external arrivals at every reporting step.

Vary uncertain inputs such as population, starting distribution, movement parameters and response assumptions. Keep the seed list and number of repetitions. Check whether the apparent ranking of scenarios changes under plausible assumptions rather than reporting one favoured run.

A second simulator can reveal implementation or modelling differences, but agreement between two simulators is not proof of real-world validity. Calibration on one dataset also does not validate every building or occupant group.

## What the first prototype cannot establish

- It does not model smoke, heat, visibility loss or the time until conditions become untenable.
- Movement-to-target time does not include every detection, alarm, decision and response delay unless those are explicitly modelled.
- Reaching a floor exit or stair landing is an intermediate result. The multi-floor demonstration must continue to its declared external targets and identify any omitted floors or populations.
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
