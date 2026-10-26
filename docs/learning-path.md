---
type: Technology Guide
title: "Learning Path for Building Evacuation Research"
description: "A practical starting sequence for a contributor with no prior BIM or simulation experience."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Learning Path for Building Evacuation Research

The goal is not to master every tool before starting. Learn enough at each step to produce something small that another person can inspect. Begin with a fictional floor plan; do not begin by automating a whole building.

## Your first session

Read the [project overview](../README.md) and [BIM and IFC primer](primers/bim-and-ifc.md). Draw two rooms, a corridor and two exits on paper. Mark which rooms share a wall, then mark which actually have a doorway between them. Those are different facts.

Explain the project back in these terms: “We keep the building record, extract the relevant information, check the connections, and simulate separate scenarios.” If that is clear, move on.

## Learn in this order

The effort ranges below are planning allowances for guided learning, not a delivery promise. A contributor learning programming for the first time may need longer.

| Step | Read and try | Small output | Ready to move on when… |
|---|---|---|---|
| Understand building records | [BIM and IFC](primers/bim-and-ifc.md); official IFC introduction in the [reference list](tools-and-references.md#bim-and-ifc-learning) | Labelled drawing and a list of source file types | You can explain why a 3D mesh alone does not tell us which rooms connect |
| Learn basic software habits | [Software basics](primers/software-basics.md); introductory Python and Git links | A tiny script that reads a fictional JSON room list and prints its names | You can run it twice, explain the output and inspect changes in Git |
| Inspect a building model | Bonsai installation guide and IfcOpenShell introduction | An [intake record](../templates/model-intake.md) for a permitted sample, plus counts of spaces and doors | You can select an element, find its source identifier and identify the model's units |
| Understand connections | [Geometry and semantics](primers/geometry-and-semantics.md) | A hand-reviewed space and passage table for the fictional floor | You can explain an unavailable connection and one that remains unknown |
| Try movement simulation | [Pedestrian simulation](primers/pedestrian-simulation.md); JuPedSim getting-started example | One local tutorial run and an [experiment report](../templates/experiment-report.md) | You can distinguish the inputs you supplied from the outputs the model produced |
| Join the parts | [Pipeline design](pipeline-design.md), [IFC requirements](ifc-data-requirements.md) | A proposed mapping from IFC elements to the reviewed floor model | You can show what is extracted, what is inferred and what needs a reviewer |

Allow roughly two weeks for an initial guided pass, then reassess from the outputs rather than the elapsed time. It is fine to spend the first week on the first two steps.

## A useful first week

1. **Day 1:** Read the overview. Sketch the fictional floor. Write three questions the future application should answer.
2. **Day 2:** Learn files, folders, variables, lists and dictionaries. Run a tiny Python program. No IFC installation is needed yet.
3. **Day 3:** Learn JSON and Git changes. Keep all fictional dimensions explicitly labelled as made up.
4. **Day 4:** With a technical mentor, choose a supported Python environment and an IFC viewer. Use the installation guides, not an old copied command list.
5. **Day 5:** Inspect a permitted IFC sample if one is available. If not, finish the paper topology exercise and request a model using the intake template. Do not turn missing source data into a guessed building model.

## What to ask a mentor

- **BIM reviewer:** Does the IFC represent the intended revision? Were spaces, openings and linked models included? Which dimensions can we trust for this task?
- **Software mentor:** Are the environment and package versions compatible? Can the same input reproduce the same derived files? Are errors visible?
- **Evacuation specialist:** Which questions and occupant behaviours matter? What evidence and validation would be needed before anyone could use a result for planning?

These are responsibilities, not three required full-time posts. A beginner can own the implementation with scheduled review support; they should not be expected to certify geometry or life-safety behaviour alone.

## Avoid these early distractions

Do not start with a universal building knowledge graph, an AI planning agent, a polished 3D city, Kubernetes, GPU rental or live sensor integration. First prove that a single door is mapped correctly and that changing its scenario availability changes both route eligibility and the simulator's permitted movement.

Next: [Milestones and starter backlog](project-plan.md).
