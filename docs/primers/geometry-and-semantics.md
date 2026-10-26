---
type: Technology Guide
title: "Geometry and Building Semantics Explained"
description: "How shapes, connections and contextual rules become a useful building traversal model."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
stale_after: 2027-04-26T00:00:00Z
sources:
  - id: indoor
    resource: https://www.ogc.org/announcement/ogc-publishes-indoorgml-2-0-part-1-conceptual-model-standard/
---
# Geometry and Building Semantics Explained

Status checked: 2026-10-26

A building picture shows shapes. An evacuation application also needs to know what those shapes represent, which places connect, and whether a connection can be used under a particular set of assumptions.

## Three different questions

| Layer | Question | Example |
|---|---|---|
| Geometry | Where is it and what shape is it? | A corridor polygon and a doorway opening |
| Topology | What connects to what? | Office A connects to Corridor C through Door D |
| Operational meaning | Who can use that connection, in which direction and under what conditions? | D is unavailable in this scenario; stairs are excluded for a particular movement profile |

Two rooms sharing a wall are **adjacent**. They are not necessarily **connected**. A connection is not necessarily usable in both directions or for every person. A space described as one room can also contain partitions that split its internal walking area.

OGC's IndoorGML 2.0 Part 1 distinguishes a core indoor-space model from a navigation extension.[^indoor] This is a useful conceptual reference. The small model proposed here is not an implementation or conformance claim for the full standard.

## A graph is a useful way to write connections down

A graph has **nodes** for things and **edges** for relationships. We can represent spaces as nodes and directed movement connections as edges. The doorway itself remains a separate object so several rules or records can refer to it.

For a fictional floor:

| From | Through | To | Scenario status | Reason |
|---|---|---|---|---|
| Office A | Door D1 | Corridor C | Eligible | Reviewed connection and required checks pass |
| Corridor C | Door D2 | Target E1 | Blocked | This scenario makes D2 unavailable |
| Corridor C | Door D3 | Target E2 | Unknown | Required clearance has not been established |

These are teaching examples, not records of a real building. With D2 blocked and D3 unknown, the model has no established eligible path to a target. It must report that outcome rather than invent a route.

A graph can be stored as ordinary tables or JSON. A graph database may help later with complex queries, but it does not decide which connections are true. Start with a narrow model that answers the project's questions, not a universal vocabulary for everything in a building.

## Connections between floors

For the multi-floor project, represent stair landings as places and flights as connections between the relevant landings. Keep the stair system's identity so the model can recognise that different floors share it. Record the served floors, elevation change, usable geometry, direction and evidence for each connection.

A graph edge saying “Floor 2 connects to Floor 1” is useful for finding candidate routes, but the simulator also needs the intervening flights and landings. It must represent travel and the interaction between people already descending and those joining from a lower floor.

Review the full route through the discharge level and building exit to the stated external target. A landing or a staircase label is not an endpoint. Floors lying above one another must remain spatially distinct even when their plan shapes overlap.

## Meaning needs context and evidence

For each important statement, record:

- **Subject and meaning:** which object, which property or relationship, and what value.
- **Origin:** source assertion, geometric derivation, reviewed observation or hypothetical scenario input.
- **Evidence:** file/element reference, drawing, inspection or reviewer note.
- **Time:** source edition, applicable time if known, and when the statement was recorded.
- **Review:** unresolved, accepted for the stated use, rejected or superseded.

“This door exists in IFC revision 3” and “this door is available at 10:00 today” are different claims. New import time does not make old availability evidence current.

## Rules must be explicit

A **movement profile** is a defined set of requirements, such as a research walking profile. A passage can be `eligible`, `blocked` or `unknown` for that profile. Eligibility is a result of specified checks, not a claim that the route is safe.

Use clear meanings for door state. A closed leaf may be openable. An unavailable, locked or obstructed passage has different implications. Do not use one vague “closed” flag for all of them.

Add a step-free or assisted-movement profile only after identifying the dimensions, equipment, assistance and behaviour needed to model it. Simply slowing an ordinary pedestrian agent does not establish accessibility.

## The graph and the floor must agree

The graph identifies permitted connections. The simulator also needs continuous walking areas, passage locations and obstacles. Deleting an edge without restricting the simulator can leave people walking through the doorway anyway.

Conversely, a graph may say that a route exists while the geometry contains a gap or an obstacle. Test both directions: every permitted transition needs valid geometry, and every traversable opening needs the right semantic rules.

## A first exercise

Draw the fictional floor from the [learning path](../learning-path.md). Make a connection table. Change one passage to blocked and one to unknown. List the affected rooms, then check the drawing for any physical route that the table missed.

The [pipeline design](../pipeline-design.md#the-first-semantic-model) turns this exercise into proposed data records.

[^indoor]: [OGC announcement of IndoorGML 2.0 Part 1](https://www.ogc.org/announcement/ogc-publishes-indoorgml-2-0-part-1-conceptual-model-standard/).
