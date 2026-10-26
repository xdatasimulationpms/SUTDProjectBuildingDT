---
type: Technology Guide
title: "Tools and Learning References"
description: "A proposed toolchain and early engine checks for a callable multi-floor evacuation module integrated with FDDE."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
stale_after: 2027-01-26T00:00:00Z
sources:
  - id: bonsai
    resource: https://docs.bonsaibim.org/studio/quickstart/installation.html
  - id: ifc-python
    resource: https://docs.ifcopenshell.org/ifcopenshell-python/hello_world.html
  - id: shapely
    resource: https://shapely.readthedocs.io/en/stable/manual.html
  - id: networkx
    resource: https://networkx.org/documentation/stable/tutorial.html
  - id: streamlit
    resource: https://docs.streamlit.io/get-started
  - id: jupedsim
    resource: https://www.jupedsim.org/stable/
  - id: disclaimer
    resource: https://www.jupedsim.org/stable/disclaimer.html
  - id: pathfinder-ifc
    resource: https://www.thunderheadeng.com/docs/2026-1/pathfinder/examples/how-to/ifc-import/
  - id: pathfinder-stairs
    resource: https://www.thunderheadeng.com/docs/2026-1/pathfinder/examples/how-to/create-stairs/
  - id: pathfinder-run
    resource: https://www.thunderheadeng.com/docs/2026-1/pathfinder/simulation/starting/
  - id: anylogic-levels
    resource: https://anylogic.help/markup/level.html
  - id: jupedsim-geometry
    resource: https://www.jupedsim.org/stable/concepts/geometry.html
---
# Tools and Learning References

Status checked: 2026-10-26

Use a small local toolchain first. The roles below are proposed project choices based on the linked primary documentation, not evidence that these packages have been installed or tested together here. Read the matching tutorial when you reach that learning step.

## Proposed toolchain

| Need | Candidate | Role and limit |
|---|---|---|
| Inspect IFC visually | Bonsai in Blender | Examine elements and properties. Follow its supported installation route; do not begin with photorealistic rendering.[^bonsai] |
| Extract IFC records | Python and IfcOpenShell | Read entities and relationships; use geometry processing when needed. Not a universal native-BIM converter.[^ifc-python] |
| Produce an IFC subset | IfcPatch | Test a separate focused IFC; verify information retention using the [requirements checklist](ifc-data-requirements.md) |
| Work with floor polygons | Shapely | Planar geometry operations. Select the floor and coordinate frame first; it does not infer correct building semantics.[^shapely] |
| Explore connectivity | NetworkX | Graph nodes, edges and queries. The reviewer and rules determine which edges are valid.[^networkx] |
| Store the first records | JSON, optionally SQLite later | Keep it local and inspectable. No graph server or cloud object store required initially |
| Learn movement simulation | JuPedSim | Python interface with a C++ simulation core; useful for controlled research exercises. Academic intended-use warning applies.[^jupedsim][^disclaimer] |
| Run the multi-floor pilot | An existing engine passing the Month 2 trial | Assess Pathfinder and any suitable available AnyLogic model/licence; establish stairs, merging, structured scenario inputs and result access before selecting |
| Expose toolkit capabilities | One thin adapter matching the FDDE interface | Follow the [integration contract](toolkit-integration-contract.md); agree the binding in Month 1 and reuse common processing functions |
| Support model review | Small reference client; optional Streamlit views | Forms and plots can support data review. A dedicated officer dashboard is optional.[^streamlit] |

Review each dependency's exact release, platform support, licence and maintenance status when implementation begins. A documentation version is not proof that the corresponding package combination is compatible. No package versions are pinned yet because no environment has been tested.

## Hardware for the first experiment

**Planning recommendation, not a benchmark:** start extraction and learning on a recent laptop or desktop with approximately 16 GB RAM or more and local SSD space. For the multi-floor engine, confirm its supported operating system, graphics and memory requirements during the Month 2 trial. Use a small connected-floor sample to measure resource needs before buying hardware. A CUDA workflow is not a project requirement.

Measure IFC processing time, peak memory, simulation run time and output size on the actual sample. Use those measurements to decide whether a workstation is needed. GPU rendering and robotics/sensor simulation are separate later requirements, not reasons to start with Isaac Sim for this task.

## Early engine feasibility check

Multiple floors and FDDE integration are part of the confirmed final deliverable. Agree the toolkit contract in Month 1, then test the callable engine route in **Month 2**, alongside IFC inspection, using two upper levels and a shared stair. Select one engine after the trial; the table is a shortlist rather than a commitment to implement several engines.

| Candidate | Source finding | Proposed assessment |
|---|---|---|
| Pathfinder | Official examples demonstrate IFC-derived floors/doors/stairs and a multi-floor stair layout. Its run documentation describes batch/command-line execution.[^pathfinder-ifc][^pathfinder-stairs][^pathfinder-run] | A useful first specialist trial if access is available. Test scenario parameter changes, source-ID mapping and result retrieval as well as execution |
| AnyLogic | Its official level documentation describes multiple levels and pedestrian transitions using target lines and `PedChangeLevel`.[^anylogic-levels] | Assess reuse if a suitable model and licence are available. A level-change block alone does not establish stair travel, capacity or merging behaviour; demonstrate the full model and callable module interface |
| JuPedSim | The geometry reference describes a planar walkable polygon and connected union.[^jupedsim-geometry] | Retain for introductory movement experiments. That documented geometry does not by itself establish a multi-floor stair/merge implementation; it is not the assumed core engine |

For a one-person, half-time project, reuse an engine with the required behaviour. A custom stair model or coordination layer between separate floor simulators would become a substantial additional research task.

The trial must demonstrate:

1. Travel through stair flights and landings with explicit geometry and movement parameters, rather than an instantaneous floor jump.
2. People from different floors sharing the stair and interacting at a landing.
3. Persistent occupant IDs and correct counts while moving between levels.
4. An exit or stair-route restriction, with people who cannot reach a target still reported.
5. A reference client supplying structured population/availability settings, receiving a job reference, obtaining status and retrieving results through the agreed contract. Record every manual model-preparation step.
6. Available licence terms, platform and deployment arrangements for module execution in the toolkit environment.

For Pathfinder, command-line execution of a prepared file does not by itself prove that arbitrary model edits can be automated. Demonstrate the supported route for producing the selected scenario files. For AnyLogic, similarly verify the chosen edition and model's input/output interface and any export rights. No engine or licence has been selected or installed here.

Record the findings and choose the simplest workable adapter. If required access or functionality is unavailable, resolve that dependency and revise the schedule early; a single-floor result does not satisfy the final requirement.

Confirm engine unattended execution, restart/failure reporting and cancellation behaviour before relying on them in the agent-facing job contract. Toolkit discovery, input/output schemas, job controls and integration acceptance are defined in the [module contract](toolkit-integration-contract.md). A successful engine run is only one part of that acceptance.

## Programming and version control

| Official reference | What to learn | Small exercise |
|---|---|---|
| [Python for beginners](https://www.python.org/about/gettingstarted/) | Follow the route for people entirely new to programming | Read and print a fictional room list |
| [Pro Git introduction](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) | Why changes are recorded and how local history differs from a remote | Inspect a change without uploading anything |
| [Streamlit getting started](https://docs.streamlit.io/get-started) | Local forms and data display, after basic Python | Display the fictional room list; do not deploy it to a public service |

## BIM and IFC learning

| Official reference | What to learn | Small exercise |
|---|---|---|
| [IfcOpenShell introduction to IFC](https://docs.ifcopenshell.org/introduction/introduction_to_ifc.html) | Entities, attributes, relationships and schema versions | Identify a space, door and wall in a permitted model |
| [Bonsai installation](https://docs.bonsaibim.org/studio/quickstart/installation.html) | Supported route for installing the visual authoring/review tool | Open a local IFC and inspect one object's properties |
| [IfcOpenShell Python introduction](https://docs.ifcopenshell.org/ifcopenshell-python/hello_world.html) | Open and query an IFC programmatically | Count selected element types without changing the file |
| [IfcOpenShell geometry processing](https://docs.ifcopenshell.org/ifcopenshell-python/geometry_processing.html) | How geometry can be obtained from IFC | Inspect one object's geometry and placement with a mentor |
| [IfcPatch ExtractElements](https://docs.ifcopenshell.org/autoapi/ifcpatch/recipes/ExtractElements/index.html) | Producing a subset as a new IFC | Compare the selected elements and dependencies before/after |
| [buildingSMART IDS](https://github.com/buildingSMART/IDS) and [IfcTester](https://docs.ifcopenshell.org/ifctester.html) | Expressing and checking information requirements | Later: require one agreed property and test a missing-property case |

If a tutorial offers a downloadable model, check its use and redistribution terms before downloading or committing it. A publicly accessible example is not automatically cleared for redistribution.

## Geometry and semantics learning

| Official reference | What to learn | Small exercise |
|---|---|---|
| [Shapely manual](https://shapely.readthedocs.io/en/stable/manual.html) | Polygons, intersections and validity in a plane | Draw a fictional walkable region with one obstacle |
| [NetworkX tutorial](https://networkx.org/documentation/stable/tutorial.html) | Nodes, directed edges and attributes | Represent two rooms and a corridor; remove one connection |
| [OGC IndoorGML overview](https://www.ogc.org/announcement/ogc-publishes-indoorgml-2-0-part-1-conceptual-model-standard/) | Indoor spaces, connectivity and navigation context | Explain adjacency versus traversal without implementing the whole standard |

## Simulation learning

| Official reference | What to learn | Small exercise |
|---|---|---|
| [JuPedSim getting started](https://www.jupedsim.org/stable/notebooks/getting_started.html) | A complete small research simulation | Reproduce the tutorial locally and record the environment |
| [JuPedSim geometry](https://www.jupedsim.org/stable/concepts/geometry.html) | Walkable regions and obstacles | Test a valid region and an unsupported disconnected case |
| [JuPedSim routing](https://www.jupedsim.org/stable/concepts/routing.html) | Stages, journeys, transitions and exit events | Identify precisely when a person is removed from the model |
| [JuPedSim disclaimer](https://www.jupedsim.org/stable/disclaimer.html) | Intended use and responsibility | Explain why a tutorial run is not a safety prediction |
| [Pathfinder IFC tutorial](https://www.thunderheadeng.com/docs/2026-1/pathfinder/examples/how-to/ifc-import/) | A specialist import workflow | Identify where floors, doors or stairs need manual correction |
| [Pathfinder stair tutorial](https://www.thunderheadeng.com/docs/2026-1/pathfinder/examples/how-to/create-stairs/) | A connected multi-floor example | Use as a starting point for the early engine trial, where access is available |
| [Pathfinder run documentation](https://www.thunderheadeng.com/docs/2026-1/pathfinder/simulation/starting/) | Batch and command-line execution | Test preparation and execution of the chosen scenario files and retrieval of outputs |
| [AnyLogic levels](https://anylogic.help/markup/level.html) | Levels and pedestrian transfer points | If available, demonstrate stair movement and merging in a complete model, not just a level transition |

For professional context, see [SCDF's performance-based plan approval process](https://www.scdf.gov.sg/fire-safety-services-listing/plans-submission-process/performance-based-approach-to-fire-safety-design/performance-based-plan-approval-process). It is background on the regulated design process, not a substitute for the domain review described in [validation and safety](validation-and-safety.md).

[^bonsai]: [Bonsai installation documentation](https://docs.bonsaibim.org/studio/quickstart/installation.html).
[^ifc-python]: [IfcOpenShell Python introduction](https://docs.ifcopenshell.org/ifcopenshell-python/hello_world.html).
[^shapely]: [Shapely manual](https://shapely.readthedocs.io/en/stable/manual.html).
[^networkx]: [NetworkX tutorial](https://networkx.org/documentation/stable/tutorial.html).
[^streamlit]: [Streamlit getting started](https://docs.streamlit.io/get-started).
[^jupedsim]: [JuPedSim documentation](https://www.jupedsim.org/stable/).
[^disclaimer]: [JuPedSim intended-use disclaimer](https://www.jupedsim.org/stable/disclaimer.html).
[^pathfinder-ifc]: [Pathfinder IFC import example](https://www.thunderheadeng.com/docs/2026-1/pathfinder/examples/how-to/ifc-import/).
[^pathfinder-stairs]: [Pathfinder multi-floor stair example](https://www.thunderheadeng.com/docs/2026-1/pathfinder/examples/how-to/create-stairs/).
[^pathfinder-run]: [Pathfinder starting and managing simulations](https://www.thunderheadeng.com/docs/2026-1/pathfinder/simulation/starting/).
[^anylogic-levels]: [AnyLogic level reference](https://anylogic.help/markup/level.html).
[^jupedsim-geometry]: [JuPedSim geometry concepts](https://www.jupedsim.org/stable/concepts/geometry.html).
