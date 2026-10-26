---
type: Architecture Proposal
title: "Building Ingestion and Evacuation Pipeline"
description: "Reusable building preparation and evacuation functions, exposed through an agent-ready FDDE adapter with traceable artifacts and jobs."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Building Ingestion and Evacuation Pipeline

Build reusable **building preparation and evacuation capabilities** and expose them to the FDDE Toolkit. Keep the domain functions and artifacts independent of the toolkit transport and engine wrapper so one implementation supports agent calls, a reference client and minimal review views.

This is a proposed design for multiple connected floors. Start learning with a small floor, then prepare the stairs, landings and complete routes through the discharge level to defined external targets. The hard part is turning an imperfect building record into defensible movement geometry and relationships.

The [delivery plan](three-phase-plan.md) allocates twelve months to one half-time implementer. Core delivery is one agent-ready module, one toolkit binding, one engine and three multi-floor scenarios on a pilot building. Agree integration in Month 1 and prove the callable stair/merge route in Month 2. Learning, testing and documentation are included.

## Stages and outputs

| Stage | Work | Output | Gate before proceeding |
|---|---|---|---|
| 1. Register | Record source owner, permitted use, edition, file hash and supplied dependencies | Intake record and unchanged source files | Scope and source identity are known |
| 2. Obtain IFC | Accept an existing IFC or request an export from the native authoring system | Full source IFC and export settings | File opens; intended floors, units and main elements are present |
| 3. Inspect | Inventory element types, spaces, doors, storeys, properties and missing items | Quality report and agreed selection rules | No silent substitution for missing critical information |
| 4. Extract | Produce task-focused data while retaining its source mapping; optionally produce a smaller IFC for review | Focused IFC, element table, geometry and lineage manifest | Relevant identities, dependencies, relationships and dimensions survive |
| 5. Build and review semantics | Propose spaces, passages, stair landings and directed horizontal/vertical connections | Reviewed topology edition and unresolved-issue list | Complete included routes reach the external targets; each connection has evidence and review status |
| 6. Prepare a scenario | Combine a fixed building edition with population, movement assumptions and explicit changes | Versioned scenario definition and engine input | Graph, geometry and engine configuration represent the same restrictions |
| 7. Run and assess | Execute the selected engine, record failures, compare repeated runs | Trajectories, measurements and experiment report | Reproducibility and validation checks pass for the stated use |
| 8. Serve toolkit comparisons | Return structured measures, artifacts, caveats and data gaps for the FDDE agent and officer | Versioned comparison and draft assessment | Toolkit integration and interpretation checks; results remain simulated |

The [IFC checklist](ifc-data-requirements.md) defines what “relevant” means. A smaller IFC is useful for review/interchange; the simulator will usually need a different representation. **Do not make an IFC subset a compulsory bottleneck if reliable analysis data can be extracted directly from the preserved full IFC.**

## Keep three representations

1. **Source representation:** the original native package, if supplied, and original IFC. A source hash identifies exact bytes; it does not establish correctness.
2. **Reviewed building representation:** extracted elements, floor geometry, identifiers, relationships, evidence and review status. It describes the selected building edition.
3. **Scenario representation:** an independent copy or overlay describing hypothetical occupants, closures and movement rules. It references a specific reviewed edition.

Store all three separately. Reprocessing a new IFC should create a new edition and a change report. Do not silently reuse old door connections, human annotations or scenario mappings when source elements move or disappear.

## The first semantic model

“Semantic” means the data explains what things are and how they relate. Use a narrow **building traversal profile**: enough meaning to answer where movement is possible under stated conditions.

| Record | Minimum proposed fields |
|---|---|
| Building edition | Project/building ID, source file hashes, source revision, schema, included floors, import time, effective-date uncertainty |
| Space | Local stable ID, source locator if available, name, floor, kind, geometry reference and review status |
| Passage | ID, kind, source locator, position, relevant dimensions with units and measurement meaning, evidence |
| Stair connector | Stair-system ID, flight/landing IDs, from/to levels, entrance/exit bindings, dimensions and geometry, movement direction, evidence and review status |
| Directed transition | ID, from-space, to-space, passage ID, movement profile, condition references, evidence and review status |
| Claim or annotation | Subject, property/relation, value, origin, source/evidence, valid time if known, recorded time, reviewer and supersession link |
| Geometry binding | Entity ID, geometry artifact/hash, part locator, units, local frame, transform and transform version |
| Scenario | Reviewed edition, occupants, rule version, changes, engine/profile version, seeds, time origin, horizon and outcome definitions |

Start with JSON files and explicit checks; move to SQLite if editing and queries need it. A knowledge graph is a way of representing objects and relationships, not a requirement to deploy a graph server. The shared profile is compatible in intent with the parent hub's [semantic architecture](https://sgts.gitlab-dedicated.com/wog/htx/egxdata/simulation/research-hub-for-world-model/-/blob/main/panorama/information/semantic-layer-design.md), but this proposal is not yet an implemented API contract.

Use source locators scoped by file/edition plus IFC `GlobalId` where present. Preserve original IDs; maintain separate local IDs for derived spaces. Do not join buildings by room name or assume IDs survive every export. Record split/merge mappings for changed spaces.

### A concrete example

```text
Upper-floor office -> corridor -> landing
                                    |
                               stair flight
                                    |
Lower-floor office -> corridor -> landing  <- flows merge here
                                    |
                               stair flight
                                    |
Discharge-level corridor -> building exit -> defined external target
```

This diagram describes possible connections, not a safe route. Each arrow needs its own directional conditions. For a given movement profile and scenario, a transition is:

- `eligible`: required checks passed on the selected evidence;
- `blocked`: a known restriction excludes it;
- `unknown`: required evidence is absent, stale or conflicting.

Only eligible transitions enter the default routing calculation. Report the unknown ones separately. An analyst may test an explicitly labelled assumption in a scenario, but must not convert that assumption into a source fact. Landing arrival is an intermediate event; count a building exit only at the stated external endpoint.

Represent every relevant flight and landing, including intermediate landings without a room connection. A coarse floor-to-floor graph edge may support discovery, but the simulation also needs the connector geometry, travel behaviour, usable dimensions and merging constraints. Keep floor space, stair system and landing identities distinct.

## Geometry preparation needs its own checks

Build local, metre-based geometry for each included storey, preserving its transform into a common building frame and back to source coordinates. Inspect nested placements, floor/landing elevations, openings, walls, columns and furniture. Keep the stair geometry and vertical connections between the floor representations. A simple projection of every object onto one plane can block valid doors or combine different floors incorrectly.

Use manual floor annotation as a documented fallback for the first experiment when automatic extraction is unreliable. It remains a derived model with an author, evidence, uncertainty and limitations—not a repaired source IFC.

A room graph alone cannot stop a simulated pedestrian from walking through an unavailable doorway. The engine adapter must apply the same restriction to both navigation choices and movement geometry or validated engine controls. If a closure splits the domain, use an engine-supported treatment or reject the run clearly; do not create an artificial connection merely to satisfy a geometry constraint.

Run the included floors and shared stairs as one interacting system. Independent floor runs combined afterwards omit competition for the shared stair and cannot establish the multi-floor result. Use the engine's supported stair representation and check the mapping of dimensions, direction, movement parameters and occupancy.

Preserve occupant identity and starting floor through every transfer. For the static-population core scenarios, initial population must equal people still in the model plus recorded external arrivals. People with no eligible route remain part of the remaining population. If floors are excluded, record omitted demand and possible effects on shared stairs.

## Toolkit operations and review views

The [integration contract](toolkit-integration-contract.md) defines the proposed inspection, preparation, scenario validation, run submission, status/cancellation, comparison and artifact operations. The toolkit supplies the agent and orchestration. Return structured errors and stable artifact/job references so the caller can handle missing data or long-running work.

Keep processing callable without a graphical interface. A minimal reference client exercises the same functions. These views support model review or the toolkit workflow; a separate dashboard is optional.

| Screen | Who uses it and what they should be able to do |
|---|---|
| Model intake | Implementer: select a local IFC and inspect its edition, floors and missing-information report |
| Review connections | Implementer with available building input: switch floors, trace stair routes, inspect source IDs and record decisions |
| Prepare scenario | Building officer: choose a prepared edition, enter occupancy by floor and select unavailable door or stair routes |
| Run and compare | Building officer: compare floor clearance, stair queues and external arrivals; inspect coverage and assumptions |
| Export assessment | Building officer: save scenario assumptions, findings, plots and unresolved issues for review |

Begin with inspection and a small review table for annotations. The FDDE agent calls registered capabilities to assemble supported scenarios and obtain results. Model acceptance and scenario changes follow their recorded review states; tool descriptions and schemas do not let an agent manufacture accepted building evidence.

The module and one FDDE adapter are core scope. A dedicated application interface, live Panorama asset adapter and a second-building trial are stretch goals. Use the existing toolkit interface to demonstrate the officer use case.

## Reproducible run package

Each run should record the source and derived-file hashes; extraction settings; geometry/topology editions; manual corrections; scenario and movement profile; code revision; environment/engine version; random seeds; time step; stopping condition; logs; outcome metrics; and failures. A completed process is not necessarily a completed evacuation.

The [experiment template](../templates/experiment-report.md) is the initial human-readable record. No job runner or package exporter is implemented yet.

## Panorama and FDDE handoff

| Part | Responsibility |
|---|---|
| Building owner or authoring system | Supplies and accounts for the source model and operational records |
| This module | Produces traceable task derivatives and semantic records; exposes validation, simulation jobs and structured comparisons through the toolkit adapter |
| Panorama | Could register and serve accepted assets, reviewed semantic editions, metadata and access-controlled references |
| FDDE Toolkit | Discovers and calls module operations with user context; orchestrates scenarios and presents returned comparisons through its agent and interface |
| Domain reviewer | Assesses input fitness, assumptions, validation evidence and permitted use |

The core integration package declares module capabilities, schemas, engine/resource requirements, validation limits and installation/registration details. Pin the input and output editions in each job, and test the adapter with the actual FDDE harness. This is the final Phase 3 deliverable.

For a future live Panorama asset handoff, use artifact IDs/versions/hashes, coverage, frames, semantic profile, identity mappings, quality and access notes. Registered local artifacts support initial development; live Panorama endpoints are not assumed.

Simulation results and scenario edits may later be registered as **derived research outputs**, never as observed current building state. USD or glTF previews are optional visual derivatives, not substitutes for the IFC/source mapping and movement model.
