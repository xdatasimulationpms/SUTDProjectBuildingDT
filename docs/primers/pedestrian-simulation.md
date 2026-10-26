---
type: Technology Guide
title: "Pedestrian Simulation Explained"
description: "Movement models, scenario inputs, outcome measurements and the limits of evacuation experiments."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
stale_after: 2027-04-26T00:00:00Z
sources:
  - id: geometry
    resource: https://www.jupedsim.org/stable/concepts/geometry.html
  - id: routing
    resource: https://www.jupedsim.org/stable/concepts/routing.html
  - id: disclaimer
    resource: https://www.jupedsim.org/stable/disclaimer.html
---
# Pedestrian Simulation Explained

Status checked: 2026-10-26

A pedestrian simulator moves virtual people according to a mathematical model and supplied assumptions. It can help compare congestion and movement patterns. It does not observe what real people will definitely do.

## Pathfinding and simulation answer different questions

- **Pathfinding:** Is there an allowed route, and which route should be selected under a stated rule?
- **Pedestrian simulation:** What movement and interactions arise when a defined population follows the model over time?
- **Evacuation assessment:** What do these results mean when combined with response delays, hazards, human factors, building conditions and appropriate professional judgement?

Finding a short route does not establish a fast or safe evacuation. A bottleneck or changed route choice can affect the outcome even when everyone has a path.

## What you supply

| Input | Questions to answer |
|---|---|
| Walkable geometry | What floor region is included, and which obstacles and openings are represented? |
| Population | How many people, where do they start, and how were those assumptions chosen? |
| Movement model | Which model and parameters are used? What behaviours does it omit? |
| Route choice | Which targets or waypoints do people follow, and what do they know? |
| Scenario changes | Which passages are unavailable? Are changes static or time-dependent? |
| Timing | Does time start at movement initiation or alarm? Are response delays included? |
| Execution settings | What are the time step, random seeds and maximum run time? |

The first prototype should use **static scenario changes before the run**. Live closures, dynamic hazards and adaptive instructions add another class of timing and control problems.

## What JuPedSim can teach us

JuPedSim's geometry documentation uses a two-dimensional walkable polygon with obstacle holes, and requires a connected union for the described geometry construction.[^geometry] Its routing model provides stages, journeys and transitions. An exit stage removes agents from the simulation; that software event is not itself evidence that they reached safety.[^routing]

This makes a small floor a useful learning case. It also creates a design check: when a closure splits the floor into disconnected pieces, the adapter cannot simply pass invalid geometry through or pretend the pieces are connected. Preserve the isolated population in the report; reject or handle the case with a tested approach.

**Intended-use limitation:** JuPedSim's official disclaimer describes academic use and warns that its predictions may be unsuitable for life-safety conclusions.[^disclaimer] Use it to learn and test research methods. Do not treat it as the default engine for an operational evacuation product without a separate suitability, validation, licensing and support review.

## Compare scenarios carefully

Start with a baseline, the same case with one passage unavailable, and a case with changed occupancy. Keep the building edition and other assumptions fixed when making a controlled comparison. Reuse a documented seed list where appropriate, while recognising that different algorithms or environments can still produce differences.

Report distributions across repeated runs rather than presenting one random run as a prediction. An initial batch of ten seeds can exercise the reporting workflow, but it is not a statistical assurance rule. Determine the needed replication and sensitivity analysis with the reviewer.

## Read the results honestly

Useful measures include people remaining over time, target arrival times, passage throughput, queues and unserved populations. Define each measure: where it is measured, over what interval, using what spatial area or counting rule.

If people remain when the run stops, report a censored or incomplete result. Do not report the stopping time as a completed evacuation time or drop the unsuccessful people from the summary. A crowded animation alone is not a validated density measurement.

The first-floor experiment measures **movement to defined model targets**. It does not compute the entire time from fire development or alarm to safety, and it does not model smoke or heat. Do not label its output “safe evacuation time”.

## A first exercise

Run the official getting-started example linked in [tools and references](../tools-and-references.md#simulation-learning). Record its original assumptions. Change one input, rerun, and explain the difference without asserting that it predicts a real building. Use the [experiment report](../../templates/experiment-report.md).

Continue with [validation and safety](../validation-and-safety.md).

[^geometry]: [JuPedSim geometry concepts](https://www.jupedsim.org/stable/concepts/geometry.html).
[^routing]: [JuPedSim routing concepts](https://www.jupedsim.org/stable/concepts/routing.html).
[^disclaimer]: [JuPedSim disclaimer](https://www.jupedsim.org/stable/disclaimer.html).
