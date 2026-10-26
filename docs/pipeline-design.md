---
type: Architecture Proposal
title: "Building Ingestion and Evacuation Pipeline"
description: "A proposed local pipeline with preserved sources, reviewed traversal semantics and separate simulation scenarios."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Building Ingestion and Evacuation Pipeline

Build a reusable **building preparation pipeline**, then place an evacuation research application on top. Keep the preparation outputs independent of any one simulator so the same reviewed model can support another engine later.

This is a proposed design. Start locally, on one floor, with explicit manual review. The hard part is not displaying a building: it is turning an imperfect building record into defensible movement geometry and relationships.

## Stages and outputs

| Stage | Work | Output | Gate before proceeding |
|---|---|---|---|
| 1. Register | Record source owner, permitted use, edition, file hash and supplied dependencies | Intake record and unchanged source files | Scope and source identity are known |
| 2. Obtain IFC | Accept an existing IFC or request an export from the native authoring system | Full source IFC and export settings | File opens; intended floors, units and main elements are present |
| 3. Inspect | Inventory element types, spaces, doors, storeys, properties and missing items | Quality report and agreed selection rules | No silent substitution for missing critical information |
| 4. Extract | Produce task-focused data while retaining its source mapping; optionally produce a smaller IFC for review | Focused IFC, element table, geometry and lineage manifest | Relevant identities, dependencies, relationships and dimensions survive |
| 5. Build and review semantics | Propose spaces, passages and directed connections; compare with drawings and domain knowledge | Reviewed topology edition and unresolved-issue list | Every included movement connection has evidence and a review status |
| 6. Prepare a scenario | Combine a fixed building edition with population, movement assumptions and explicit changes | Versioned scenario definition and engine input | Graph, geometry and engine configuration represent the same restrictions |
| 7. Run and assess | Execute the selected engine, record failures, compare repeated runs | Trajectories, measurements and experiment report | Reproducibility and validation checks pass for the stated use |
| 8. Review planning options | Explain differences, caveats and data gaps to a domain reviewer | Draft scenario assessment and next actions | Human interpretation; no automatic operational approval |

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
| Directed transition | ID, from-space, to-space, passage ID, movement profile, condition references, evidence and review status |
| Claim or annotation | Subject, property/relation, value, origin, source/evidence, valid time if known, recorded time, reviewer and supersession link |
| Geometry binding | Entity ID, geometry artifact/hash, part locator, units, local frame, transform and transform version |
| Scenario | Reviewed edition, occupants, rule version, changes, engine/profile version, seeds, time origin, horizon and outcome definitions |

Start with JSON files and explicit checks; move to SQLite if editing and queries need it. A knowledge graph is a way of representing objects and relationships, not a requirement to deploy a graph server. The shared profile is compatible in intent with the parent hub's [semantic architecture](https://sgts.gitlab-dedicated.com/wog/htx/egxdata/simulation/research-hub-for-world-model/-/blob/main/panorama/information/semantic-layer-design.md), but this proposal is not yet an implemented API contract.

Use source locators scoped by file/edition plus IFC `GlobalId` where present. Preserve original IDs; maintain separate local IDs for derived spaces. Do not join buildings by room name or assume IDs survive every export. Record split/merge mappings for changed spaces.

### A concrete example

```text
Office A -- passage D1 --> Corridor -- passage D2 --> External target
                                 \-- passage D3 --> Stair landing
```

This diagram describes possible connections, not a safe route. Each arrow needs its own directional conditions. For a given movement profile and scenario, a transition is:

- `eligible`: required checks passed on the selected evidence;
- `blocked`: a known restriction excludes it;
- `unknown`: required evidence is absent, stale or conflicting.

Only eligible transitions enter the default routing calculation. Report the unknown ones separately. An analyst may test an explicitly labelled assumption in a scenario, but must not convert that assumption into a source fact. A connection to a stair landing is outside the first prototype's complete-evacuation claim.

## Geometry preparation needs its own checks

Build local, metre-based floor geometry from the selected storey, preserving the transform back to source coordinates. Inspect nested placements, elevations, openings, walls, columns and furniture. A simple projection of every object onto a plane can block valid doors or combine different floors incorrectly.

Use manual floor annotation as a documented fallback for the first experiment when automatic extraction is unreliable. It remains a derived model with an author, evidence, uncertainty and limitations—not a repaired source IFC.

A room graph alone cannot stop a simulated pedestrian from walking through an unavailable doorway. The engine adapter must apply the same restriction to both navigation choices and movement geometry or validated engine controls. If a closure splits the domain, use an engine-supported treatment or reject the run clearly; do not create an artificial connection merely to satisfy a geometry constraint.

## Proposed application screens

| Screen | What the beginner should be able to do |
|---|---|
| Model intake | Select a local IFC, see its edition, floors and missing-information report |
| Review connections | View a 2D floor overlay; inspect source IDs; accept, reject or flag a candidate connection with a reason |
| Prepare scenario | Choose a reviewed edition; enter occupants and assumptions; select unavailable passages; preview consequences |
| Run and compare | See progress/failures; compare completed and incomplete runs; inspect source and scenario versions |
| Export assessment | Save assumptions, methods, plots, unresolved issues and a reviewer section |

Begin with read-only inspection and a simple table/form for reviewed annotations. Add interactive 3D only after the extraction and topology tests work. An optional agent can later help fill forms and call tested functions; it must not silently approve topology or issue evacuation instructions.

## Reproducible run package

Each run should record the source and derived-file hashes; extraction settings; geometry/topology editions; manual corrections; scenario and movement profile; code revision; environment/engine version; random seeds; time step; stopping condition; logs; outcome metrics; and failures. A completed process is not necessarily a completed evacuation.

The [experiment template](../templates/experiment-report.md) is the initial human-readable record. No job runner or package exporter is implemented yet.

## Future Panorama and FDDE handoff

| Part | Responsibility |
|---|---|
| Building owner or authoring system | Supplies and accounts for the source model and operational records |
| This ingestion pipeline | Produces traceable task derivatives and candidate semantic records, with review gates |
| Panorama | Could register and serve accepted assets, reviewed semantic editions, metadata and access-controlled references |
| FDDE application | Selects a fixed input edition, prepares scenarios, runs analysis and presents comparisons |
| Domain reviewer | Assesses input fitness, assumptions, validation evidence and permitted use |

Propose a future handoff manifest containing an artifact ID/version/hash, download reference, coverage, coordinate information, semantic profile/version, identity mappings, quality issues and licence/access notes. Use a local manifest adapter first. Do not assume Panorama endpoints exist or write directly into its database.

Simulation results and scenario edits may later be registered as **derived research outputs**, never as observed current building state. USD or glTF previews are optional visual derivatives, not substitutes for the IFC/source mapping and movement model.
