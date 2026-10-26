---
type: Technology Guide
title: "Tools and Learning References"
description: "A small proposed toolchain, official learning links and later engine choices for building evacuation research."
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
| Build simple local screens | Streamlit, after the data workflow works | Candidate for forms, tables and plots. Review editing needs before committing to a more elaborate floor editor.[^streamlit] |

Review each dependency's exact release, platform support, licence and maintenance status when implementation begins. A documentation version is not proof that the corresponding package combination is compatible. No package versions are pinned yet because no environment has been tested.

## Hardware for the first experiment

**Planning recommendation, not a benchmark:** start with an ordinary recent laptop or desktop, approximately 16 GB RAM or more and local SSD space. More memory may help with large IFC models, but reduce to a small reviewed floor before buying hardware. The proposed extraction, graph and small pedestrian experiments do not need a CUDA workflow or an NVIDIA GPU. A viewer still needs a graphics environment supported by its application.

Measure IFC processing time, peak memory, simulation run time and output size on the actual sample. Use those measurements to decide whether a workstation is needed. GPU rendering and robotics/sensor simulation are separate later requirements, not reasons to start with Isaac Sim for this task.

## A second engine to assess later

**Pathfinder is a candidate comparison, not a selected dependency.** Its vendor tutorial demonstrates IFC import and extraction of floors, doors and stairs, while also showing manual cleanup of misinterpreted objects.[^pathfinder-ifc] A separate tutorial demonstrates multi-floor stairs.[^pathfinder-stairs]

That makes it worth assessing when the project needs multi-floor evacuation workflows or a comparison against a specialist tool. Evaluate trial/licence terms, supported platforms, automation, input/output access, validation documentation and technical support before procurement. No paid software has been purchased or installed here. Import success in any tool does not certify the scenario or building.

Keep a research adapter and an eventual product engine decision separate. Product requirements may favour adapting a specialist engine rather than writing all evacuation behaviour ourselves.

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
| [Pathfinder IFC tutorial](https://www.thunderheadeng.com/docs/2026-1/pathfinder/examples/how-to/ifc-import/) | An alternative specialist import workflow | Review the cleanup requirements before considering a trial |

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
