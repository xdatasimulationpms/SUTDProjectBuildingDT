---
type: Technology Guide
title: "BIM and IFC Explained"
description: "Building models, exchange formats and the difference between visual geometry and usable building information."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
stale_after: 2027-04-26T00:00:00Z
sources:
  - id: ifc
    resource: https://docs.ifcopenshell.org/introduction/introduction_to_ifc.html
  - id: revit
    resource: https://help.autodesk.com/cloudhelp/2026/ENU/Revit-API-MainReference/files/html/7efa4eb3-8d94-b8e7-f608-3dbae751331d.htm
---
# BIM and IFC Explained

Status checked: 2026-10-26

Think of a building model as a drawing connected to a structured inventory. It may describe a door's shape, identity and properties, together with the building elements around it. For evacuation research, the useful information is not just how the building looks but how its spaces and passages can be interpreted.

## The main terms

| Term | Plain meaning |
|---|---|
| BIM | Building Information Modelling: creating and managing structured information about a built asset |
| Native model | A file maintained by the authoring application, such as a Revit `.rvt` file |
| IFC | Industry Foundation Classes: a standard schema for exchanging building and infrastructure information; commonly stored in a `.ifc` file |
| Element | A described object, such as a wall, door or space |
| Property | Information about an object, such as a name or a dimension |
| Relationship | A link with meaning, such as an element belonging to a storey |
| Schema | Rules defining the available kinds of objects, fields and relationships |
| Mesh | A surface representation made from vertices and faces; useful for display, but not inherently a building information model |

**Source finding:** IFC represents typed objects and relationships, and different schema versions define different details. IfcOpenShell's introduction explains how to inspect those objects rather than treating the file as a picture.[^ifc]

## There are two entry routes

```text
Native authoring file -> supported authoring/export tool -> IFC
Already an IFC file  ------------------------------------> IFC inspection
```

Revit exposes IFC export through its software/API.[^revit] For a native Revit input, request a checked export from someone with the appropriate tool and access. Do not assume that installing IfcOpenShell enables direct conversion of every proprietary BIM file.

An OBJ or glTF file can be useful as a preview or reference, but it may not carry the room and passage information this project needs. A PDF drawing can support manual review; it is not a structured IFC replacement.

## Export is a handover that needs checking

An export can omit linked files, spaces, properties or selected floors. Ask for the model revision, schema, export settings, coordinate system and a reference drawing. Open the result in a viewer and compare representative objects with the intended source.

Do not migrate every source to the newest IFC version automatically. Start with the version actually supplied and supported by the chosen toolchain. Test any conversion for information loss.

“As-built” is a statement about a record, not proof that every door or obstruction still matches the physical building today. The intake record must state what has and has not been checked.

## Why we preserve the full model

This project's evacuation derivative does not need every object in equal detail. However, deleting objects directly from the only source would lose information and make later results difficult to explain. Preserve the source, record the selection, and produce new files.

There are two useful derivatives:

- A **focused IFC**, if needed for handover or visual review.
- An **analysis model**, such as room tables, walkable polygons and a connection graph, for the simulator adapter.

These derivatives serve different purposes. Neither is automatically suitable for evacuation just because it opens successfully.

## A first exercise

Using a permitted example model in a viewer, select one space, one door and one wall. Record their types, names, identifiers and floor. Find the units and check one known dimension. Then answer: “Can I tell which two spaces this door connects, and what evidence supports that answer?”

If the model cannot answer, record the gap. That is a useful finding, not a reason to guess.

Continue with [geometry and semantics](geometry-and-semantics.md). The [reference guide](../tools-and-references.md#bim-and-ifc-learning) links to viewer installation and IFC tutorials.

[^ifc]: [IfcOpenShell introduction to IFC](https://docs.ifcopenshell.org/introduction/introduction_to_ifc.html).
[^revit]: [Autodesk Revit IFC export API reference](https://help.autodesk.com/cloudhelp/2026/ENU/Revit-API-MainReference/files/html/7efa4eb3-8d94-b8e7-f608-3dbae751331d.htm). This is evidence of the export route, not a beginner programming prerequisite.
