# Building Data Pipeline for Evacuation Research

Prepare building data and multi-floor evacuation experiments as reusable capabilities for the FDDE Toolkit.

This is the starting repository for **SUTDProjectBuildingDT**, a spin-off from the World Model Research Hub. It is written for someone new to building models, data pipelines and simulation. The current deliverable is a learning and implementation plan; **there is no working ingestion pipeline, simulator or toolkit adapter in this repository yet**.

## What we want to build

The project has **one implementer working half time for one year**. Its end product is an **agent-ready building ingestion and evacuation module that can be integrated into the FDDE Toolkit**. The toolkit's agent can call documented operations to inspect and prepare a building model, validate scenarios, run multi-floor simulations and retrieve comparisons. Building officers use that workflow to compare occupancy and route changes across floors, shared stairs and exits.

Agent ready means the module has discoverable capabilities, defined inputs and outputs, structured results, clear errors and trackable jobs. The [integration contract](docs/toolkit-integration-contract.md) defines the proposed package and demonstration.

```text
Building model and supporting records
                  |
          Obtain and check IFC
                  |
      Keep the original IFC unchanged
                  |
       Extract the relevant information
          /                       \
Focused IFC for review      Analysis data for computation
                           spaces, openings, walkable areas
                                      |
                           Review meaning and connections
                                      |
                           Define separate scenario copies
                                      |
                           Simulate and compare outcomes
                                      |
                           Versioned tools, jobs and results
                                      |
                           FDDE agent and officer review
```

**An important distinction:** BIM describes a way of organising building information, not a single file format. A native authoring file may need an IFC export from its authoring software. An existing IFC file needs checking and extraction, not another generic “BIM conversion”. See [BIM and IFC](docs/primers/bim-and-ifc.md).

## The first useful demonstration

Use a small fictional floor as a learning exercise, then test a simple layout with two upper floors and a discharge level. The project demonstration uses multiple connected floors from one pilot building, including the stairs and onward routes to defined external targets. Agree the exact floor coverage with the building officer when the model is available.

The demonstration should:

1. Register the input and report missing information.
2. Display extracted spaces, doors, stair flights, landings, obstacles and their source identifiers.
3. Let a reviewer correct connections within and between floors without changing the original model.
4. Compare a baseline with an unavailable exit or stair route and a different distribution of occupants across floors.
5. Report movement times by starting floor, stair queues, merging flows and people who did not reach a target, alongside the assumptions and limitations.
6. Demonstrate the workflow through registered toolkit tools, including scenario checks, run status, result retrieval and an agent-assisted comparison.

The model must retain people as they move between floors and through stairs. Reaching a landing does not count as leaving the building. Record the endpoint and any excluded floors explicitly.

## What the project does not claim

The research application supports **scenario assessment and draft planning options**, not an automatically approved evacuation plan. It does not initially model smoke, heat, emergency communications, assisted evacuation, lifts or live conditions. Those require additional data, models and validation.

Do not use prototype results to direct a real evacuation or certify a building as safe. [Validation and safety](docs/validation-and-safety.md) explains the review needed before operational use.

## Start here

Begin with the [three phase project overview](docs/three-phase-plan.md): build callable preparation capabilities in months 1 to 5, develop and validate the simulation capabilities in months 6 to 9, then package and demonstrate FDDE integration in months 10 to 12. Agree the toolkit interface in Month 1 and test the engine-call route in Month 2. The proposed allocation remains six full-time person-months, with one pilot building, one engine and three scenarios. A dedicated dashboard and second-building trial are stretch goals.

| If you want to… | Read… |
|---|---|
| Understand the three phases and their deliverables | [Three phase project overview](docs/three-phase-plan.md) |
| Understand the agent-ready module and toolkit handoff | [FDDE integration contract](docs/toolkit-integration-contract.md) |
| Learn from zero | [Learning path](docs/learning-path.md) |
| Understand the proposed system | [Pipeline design](docs/pipeline-design.md) |
| Know which building information matters | [IFC data requirements](docs/ifc-data-requirements.md) |
| Decide what to build first | [Milestones and starter backlog](docs/project-plan.md) |
| Choose tools and find official tutorials | [Tools and learning references](docs/tools-and-references.md) |
| Browse all material | [Documentation index](docs/index.md) |

## Recommended starting approach

Use Python for data processing, IfcOpenShell for IFC inspection, a small reviewed connection graph, and a local interface later. Start with files rather than a server platform. A graph database, large language model, NVIDIA GPU and photorealistic 3D viewer are **not prerequisites** for this first experiment.

Use an existing engine that passes the early stair and integration trial. JuPedSim remains a small geometry and movement learning option. The [tool comparison](docs/tools-and-references.md#early-engine-feasibility-check) evaluates multi-floor behaviour and programmatic scenario/run access. Build one set of processing functions with a thin toolkit adapter and a small reference client.

## How it relates to Panorama and FDDE

The module can be tested locally and integrated into the FDDE Toolkit through the agreed adapter. FDDE supplies the agent, orchestration and shared user interface; this project supplies the building preparation and simulation capabilities. Later, Panorama could publish accepted source assets and semantic records for the module to consume. Live Panorama integration is optional; the FDDE integration package is core delivery.

The [parent Research Hub](https://sgts.gitlab-dedicated.com/wog/htx/egxdata/simulation/research-hub-for-world-model) provides wider context; access to it is not needed to follow this repository. The [pipeline design](docs/pipeline-design.md#panorama-and-fdde-handoff) describes the proposed handoff.

## Repository and data rules

- Put real models and run outputs in the ignored `local-data/` directory, following the [data guide](data/README.md). No building data is bundled here.
- Keep original files unchanged. Save corrections and generated outputs separately.
- Use the [intake](templates/model-intake.md), [scenario](templates/scenario.md) and [experiment report](templates/experiment-report.md) templates as the project develops.
- The project repository is [hosted on GitHub](https://github.com/xdatasimulationpms/SUTDProjectBuildingDT). Keep real model inputs and run outputs in their agreed data locations.
- Project licensing and any institutional attribution must be agreed by the owner before external distribution. The folder name does not establish institutional endorsement.

Created: 2026-10-26. See [change history](CHANGELOG.md) and [contributor instructions](AGENTS.md).
