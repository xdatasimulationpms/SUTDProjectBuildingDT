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

The final demonstration is an agent-ready module in the FDDE Toolkit and covers multiple floors. After the first floor exercise, add another occupied floor, a shared stair and a discharge route. Then learn to call preparation/simulation functions with defined inputs and receive structured outputs.

## Learn in this order

This project has one contributor working half time over twelve months. Begin with the introductory exercises during the first calendar month and continue learning within each phase. Review progress through the small outputs below, especially if programming is new.

| Step | Read and try | Small output | Ready to move on when… |
|---|---|---|---|
| Understand building records | [BIM and IFC](primers/bim-and-ifc.md); official IFC introduction in the [reference list](tools-and-references.md#bim-and-ifc-learning) | Labelled drawing and a list of source file types | You can explain why a 3D mesh alone does not tell us which rooms connect |
| Learn basic software habits | [Software basics](primers/software-basics.md); introductory Python and Git links | A tiny script that reads a fictional JSON room list and prints its names | You can run it twice, explain the output and inspect changes in Git |
| Inspect a building model | Bonsai installation guide and IfcOpenShell introduction | An [intake record](../templates/model-intake.md) for a permitted sample, plus counts of spaces and doors | You can select an element, find its source identifier and identify the model's units |
| Understand connections | [Geometry and semantics](primers/geometry-and-semantics.md) | A reviewed table of rooms, landings, passages and stair connections across the fictional levels | You can trace a complete route and explain blocked and unknown connections |
| Try movement simulation | [Pedestrian simulation](primers/pedestrian-simulation.md); JuPedSim getting-started example | One local tutorial run and an [experiment report](../templates/experiment-report.md) | You can distinguish the inputs you supplied from the outputs the model produced |
| Prove the multi-floor route | [Engine feasibility check](tools-and-references.md#early-engine-feasibility-check), completed by Month 2 | A small shared-stair model and a tested scenario/run/result interface in an existing engine | You can trace stair travel and merging, preserve occupant counts and show how the app will supply inputs |
| Understand a toolkit module | [FDDE integration contract](toolkit-integration-contract.md); [software basics](primers/software-basics.md#how-the-toolkit-agent-uses-a-module) | An example request, validated response and tracked job; agree the binding in Month 1 | You can explain what the toolkit agent calls and how it learns whether work succeeded or needs input |
| Join the parts | [Pipeline design](pipeline-design.md), [IFC requirements](ifc-data-requirements.md) | A proposed mapping from IFC elements to the reviewed floor model | You can show what is extracted, what is inferred and what needs a reviewer |

The full sequence supports the project over time; it is not all due in the first month. Begin with building concepts, Python and a simple function-call example. Learn the IFC and simulation tools as their phases approach, keeping their interfaces defined as they are built.

## Five introductory learning sessions

1. Read the overview. Sketch the fictional floor, then its connection to another floor and the building discharge. Write three questions a building officer should be able to explore with the application.
2. Learn files, folders, variables, lists and dictionaries. Run a tiny Python program.
3. Learn JSON and Git changes. Keep all fictional dimensions explicitly labelled as made up.
4. Choose a supported Python environment and an IFC viewer, seeking technical help if available. Use the installation guides and record any installation problems.
5. Inspect a permitted IFC sample if one is available. Otherwise, finish the paper topology exercise and request a model using the intake template.

Spread these sessions over the half-time allocation and repeat exercises as needed. The [first sprint](project-plan.md#first-sprint-proposal) limits the first two calendar weeks to the core introductory tasks.

## What to ask a mentor

- **BIM reviewer:** Does the IFC represent the intended revision? Are the floors, openings, stair flights, landings and discharge route complete? Which dimensions can we trust for this task?
- **Software or toolkit contact:** Which interface can the toolkit register? How are schemas, caller context, jobs and deployment handled? Can the same input reproduce the same artifacts?
- **Evacuation specialist:** Which stair and merging behaviours matter? What evidence is needed for the selected multi-floor comparison and its interpretation?

One person owns the implementation. The contacts above provide occasional review or advice where available; they are not assumed to contribute development capacity. Record unresolved questions when support is unavailable and reflect those gaps in the scope of the demonstration.

## Avoid these early distractions

Focus on tested preparation and simulation functions, then expose them through the existing toolkit's agent. A general building ontology, a new agent framework, a polished 3D city and a dedicated dashboard add work beyond the core module. First prove that a passage is mapped correctly and that a structured scenario call changes its availability consistently.

Next: [Milestones and starter backlog](project-plan.md).
