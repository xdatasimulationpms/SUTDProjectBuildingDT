---
type: Data Contract
title: "IFC Information Needed for Evacuation Experiments"
description: "A proposed intake and extraction checklist for a reviewed single-floor movement model."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
stale_after: 2027-04-26T00:00:00Z
sources:
  - id: extraction
    resource: https://docs.ifcopenshell.org/autoapi/ifcpatch/recipes/ExtractElements/index.html
  - id: ids
    resource: https://github.com/buildingSMART/IDS
---
# IFC Information Needed for Evacuation Experiments

Status checked: 2026-10-26

Extract information for a defined question, not simply “all geometry” or “only doors”. The first question is: **which reviewed spaces can reach the chosen floor targets, and how does a stated scenario change movement?**

The following is a proposed selection policy, not a universal IFC export specification. Confirm the actual schema, authoring conventions and model quality before implementing it.

## Retain or explicitly account for these records

| Information | Typical IFC starting point | Why it matters and what to check |
|---|---|---|
| Project and spatial hierarchy | `IfcProject`, `IfcSite`, `IfcBuilding`, `IfcBuildingStorey` | Identify the correct building and floor. Retain decomposition, containment and required context |
| Rooms and other spaces | `IfcSpace`; available space-boundary relationships | Candidate navigable regions. Some exports omit spaces or have incomplete boundaries; report this rather than inventing rooms |
| Doors and openings | `IfcDoor`, `IfcOpeningElement`, filling/voiding relationships | Find candidate passages. Retain the host and opening information needed to interpret them |
| Barriers | Walls, columns, relevant railings and other physical obstacles | Bound the movement area. Include relevant class subtypes and review generic proxy elements, not just one exact class name |
| Floors and levels | Relevant slabs, storey elevations and placements | Establish the walking plane and avoid combining objects on different levels |
| Vertical connectors | Stairs, stair flights, ramps and relevant landing elements | Retain and mark them even when movement beyond the floor is out of scope. A stair cannot become a flat corridor by projection |
| Significant furnishings | Relevant furnishing/proxy elements or reviewed supplementary annotations | Tables, cabinets and other objects may obstruct movement. Decorative appearance is not needed, but obstacle footprint can be |
| Identity and properties | `GlobalId` where present, names, types, classifications, relevant property sets and quantities | Keep traceability. An IFC property value still needs a clear definition and source edition |
| Geometric dependencies | Placements, representation contexts, units, shapes and referenced geometry | A selection is not usable if the geometry's supporting records are lost |

Not every export represents a physical object with the expected class. Inventory the sample first and review exclusions. Do not assume `IfcBuildingElementProxy` is irrelevant clutter.

## Obtain or review outside IFC

| Required meaning | Why an IFC element is insufficient | Initial treatment |
|---|---|---|
| Which spaces a passage actually connects | Proximity or a shared boundary does not establish traversal | Candidate extraction followed by a labelled visual review |
| Clear opening width | A door's nominal overall width may include geometry that does not represent usable clearance | Record measurement meaning, units and evidence; leave unknown if unverified |
| Whether a passage may be used | Geometric presence does not establish current availability or permission | Reviewed operating record or explicit scenario assumption |
| Occupant count and location | Room area does not prove actual occupancy | User-supplied scenario population with rationale |
| Movement and response behaviour | The building model does not establish individual behaviour | Declared research assumptions or appropriately sourced data |
| Exit destination | A label saying “exit” does not prove arrival at a place of safety | Domain review and a defined simulation boundary |
| Mobility support | A stair or ramp label does not establish suitability for every occupant | Separate movement profiles; defer unsupported cases |
| Time validity | Receipt/export time is not necessarily the date every fact became true | Keep source revision, receipt time and effective-time uncertainty separately |

## What can be left out initially

Decorative textures, detailed rendering materials, procurement costs and unrelated service-system details can normally be omitted from the first movement derivative **after a relevance review**. Retain the original model so later questions can use them.

Do not indiscriminately remove furniture, services, fire doors or structural objects: some affect clearance, connectivity or the meaning of a route. Fire compartments and fire-protection systems belong in later hazard-aware scope if needed; their omission must be visible, not interpreted as proof that hazards are absent.

## Producing a focused IFC

**Source finding:** IfcPatch's `ExtractElements` recipe selects elements from an IFC and writes a separate IFC. Its documentation also warns that assuming asset names are unique can mix up assets when names are reused.[^extraction]

**Proposed workflow:** select the floor and relevant objects, retain the necessary dependencies and relationships, then reopen and compare the result. Treat preservation of spaces, openings, properties, containment and identity as acceptance tests, not a blanket guarantee from one extraction command. Maintain a kept/excluded inventory with reasons.

The analysis model can be extracted directly from the full IFC if the subset is not yet reliable. Do not delete the source to save space or call a mesh export an IFC-equivalent replacement.

## Information checks and geometry checks are different

buildingSMART's Information Delivery Specification (IDS) is a machine-interpretable way to express information requirements for BIM/IFC.[^ids] Later, use it for suitable requirements such as required classifications or properties. Passing an information check does not establish correct passage geometry, navigability or evacuation suitability; those need separate tests.

## Acceptance checklist for one floor

- [ ] Source revision, file hash, schema and export settings recorded.
- [ ] Intended building/floor, units and coordinate frame confirmed against a known reference.
- [ ] Required element counts and a sampled source-to-output comparison recorded.
- [ ] Spaces, obstacles and openings visually checked on the same floor overlay.
- [ ] Every included passage has a source mapping or a documented manual annotation.
- [ ] Missing rooms, unexplained gaps, ambiguous widths and unsupported objects listed.
- [ ] Focused IFC, if produced, reopens and passes the agreed retention checks.
- [ ] Excluded content and all manual fixes recorded; source remains unchanged.
- [ ] BIM reviewer signs off fitness for this specific experiment, not universal model correctness.

Use the [model intake template](../templates/model-intake.md) to capture the result.

[^extraction]: [IfcPatch ExtractElements reference](https://docs.ifcopenshell.org/autoapi/ifcpatch/recipes/ExtractElements/index.html).
[^ids]: [buildingSMART IDS specification repository](https://github.com/buildingSMART/IDS).
