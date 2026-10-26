# Building Data Pipeline for Evacuation Research

Turn a building model into understandable, traceable inputs for evacuation scenario experiments.

This is the starting repository for **SUTDProjectBuildingDT**, a spin-off from the World Model Research Hub. It is written for someone new to building models, data pipelines and simulation. The initial deliverable is a learning and implementation plan; **there is no working ingestion pipeline or simulator in this repository yet**.

## What we want to build

A user selects a building model, checks the rooms and connections extracted from it, describes a scenario, and compares simulated movement under different assumptions. The application should show where its information came from and which gaps still need human review.

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
                           Human review of planning options
```

**An important distinction:** BIM describes a way of organising building information, not a single file format. A native authoring file may need an IFC export from its authoring software. An existing IFC file needs checking and extraction, not another generic “BIM conversion”. See [BIM and IFC](docs/primers/bim-and-ifc.md).

## The first useful demonstration

Start with one small floor, a few rooms, a corridor and two candidate exits. Use a synthetic layout first, then one permitted IFC sample.

The demonstration should:

1. Register the input and report missing information.
2. Display extracted spaces, doors, obstacles and their source identifiers.
3. Let a reviewer correct candidate connections without changing the original model.
4. Compare a baseline with an unavailable exit and a different occupancy assumption.
5. Report simulated movement times, queues and people who could not reach a target, alongside the assumptions and limitations.

A floor-level result must say where the simulation stops. Reaching a stair landing is not the same as reaching an external place of safety.

## What the project does not claim

The research application supports **scenario assessment and draft planning options**, not an automatically approved evacuation plan. It does not initially model smoke, heat, emergency communications, assisted evacuation, lifts, multi-floor stair movement or live conditions. Those require additional data, models and validation.

Do not use prototype results to direct a real evacuation or certify a building as safe. [Validation and safety](docs/validation-and-safety.md) explains the review needed before operational use.

## Start here

| If you want to… | Read… |
|---|---|
| Learn from zero | [Learning path](docs/learning-path.md) |
| Understand the proposed system | [Pipeline design](docs/pipeline-design.md) |
| Know which building information matters | [IFC data requirements](docs/ifc-data-requirements.md) |
| Decide what to build first | [Milestones and starter backlog](docs/project-plan.md) |
| Choose tools and find official tutorials | [Tools and learning references](docs/tools-and-references.md) |
| Browse all material | [Documentation index](docs/index.md) |

## Recommended starting approach

Use Python for data processing, IfcOpenShell for IFC inspection, a small reviewed connection graph, and a local interface later. Start with files rather than a server platform. A graph database, large language model, NVIDIA GPU and photorealistic 3D viewer are **not prerequisites** for this first experiment.

JuPedSim is a candidate for learning pedestrian simulation, **not an adopted production evacuation engine**. Its official documentation describes academic intended use and warns about life-safety predictions. The [tool comparison](docs/tools-and-references.md) includes that limitation and a later assessment of a specialist evacuation tool.

## How it relates to Panorama and FDDE

This project can run on its own. Later, Panorama could publish accepted building assets, their versions and reviewed semantic records. The FDDE Toolkit would select those inputs, prepare scenarios, run simulations and present comparisons. Panorama is the aggregation and serving layer, not the simulation engine or the authority approving an evacuation plan.

The [parent Research Hub](https://sgts.gitlab-dedicated.com/wog/htx/egxdata/simulation/research-hub-for-world-model) provides wider context; access to it is not needed to follow this repository. The [pipeline design](docs/pipeline-design.md#future-panorama-and-fdde-handoff) describes the proposed handoff.

## Repository and data rules

- Put real models and run outputs in the ignored `local-data/` directory, following the [data guide](data/README.md). No building data is bundled here.
- Keep original files unchanged. Save corrections and generated outputs separately.
- Use the [intake](templates/model-intake.md), [scenario](templates/scenario.md) and [experiment report](templates/experiment-report.md) templates as the project develops.
- This is a local repository. No remote publication, software installation or external model upload is part of this setup.
- Project licensing and any institutional attribution must be agreed by the owner before external distribution. The folder name does not establish institutional endorsement.

Created: 2026-10-26. See [change history](CHANGELOG.md) and [contributor instructions](AGENTS.md).
