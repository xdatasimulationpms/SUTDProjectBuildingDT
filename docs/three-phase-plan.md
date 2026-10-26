---
type: Roadmap
title: "Three Phase Project Overview"
description: "A twelve month plan for one half-time implementer to deliver an agent-ready building ingestion and multi-floor evacuation module for the FDDE Toolkit."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Three Phase Project Overview

Build the project in three phases: **prepare reusable building capabilities, validate evacuation capabilities, then package and demonstrate toolkit integration**. Each phase contributes callable functions and evidence toward the final module.

The end product is an **agent-ready building ingestion and multi-floor evacuation module that can be integrated into the FDDE Toolkit**. The toolkit agent discovers its operations, supplies defined inputs, monitors jobs and retrieves structured results. Building officers are the users of the demonstrated scenario-comparison workflow.

Deliver the reusable module, its toolkit adapter, schemas, discovery manifest, run controls, installation guide and an end-to-end agent-assisted demonstration. The [integration contract](toolkit-integration-contract.md) defines these terms and the proposed operations. A dedicated officer dashboard is optional; the core workflow uses the toolkit's shared interface and a small reference client.

**Confirmed project constraints:** one implementer, twelve calendar months, half-time allocation and a multi-floor final demonstration. This is approximately six full-time person-months of nominal effort, including learning, development, testing, meetings and documentation. The month numbers are relative to the project start; the start date is still open. The phase split below is proposed and depends on the early engine trial and source-model readiness.

## The three phases at a glance

| Phase | Calendar period | Nominal effort at half time | Main deliverable | Completion demonstration |
|---|---|---|---|---|
| 1 Build the preparation capabilities | Months 1 to 5 | 2.5 person-months | Callable model inspection/preparation, connected-floor package, agreed toolkit contract and engine trial | Call preparation from a reference client; inspect source mappings, coverage and issues |
| 2 Build and validate simulation capabilities | Months 6 to 9 | 2 person-months | Scenario validation, tracked multi-floor runs and structured comparisons for three scenarios | Submit and monitor runs through the interface; demonstrate stairs, merging, errors and repeatable outputs |
| 3 Package and demonstrate FDDE integration | Months 10 to 12 | 1.5 person-months | Versioned module, toolkit adapter, discovery metadata, integration evidence and handover | A toolkit agent discovers tools, compares scenarios for a building officer and presents traceable results |

The longer first phase allows time for learning and source-model problems. Agree the toolkit contract in Month 1 and test a small stair simulation through a callable interface in Month 2. Build interfaces alongside the processing functions; Phase 3 packages and proves that integration rather than adding an agent interface to a finished standalone application. Implementation remains sequential for one person.

## Core scope for the year

Start with a fictional floor for learning, then a simple three-level stair model. Core delivery uses multiple occupied floors from one pilot building, including every intermediate landing, the discharge route and defined external targets. Use one existing simulation engine, three initial scenarios and one toolkit integration binding. Manual correction of extracted data is acceptable when its evidence and history are recorded.

The officer describes a planning question through FDDE. The toolkit agent selects a prepared model, identifies coverage and gaps, constructs supported occupancy/route changes, validates scenarios, submits runs and retrieves a comparison. The officer reviews the assumptions and findings. The implementer prepares/reviews model imports, while the module returns the structured data and artifacts required by the toolkit.

Agree the included floors and exit routes with the pilot officer in the first month. If some floors are excluded, state how omitted occupants and their possible stair inflows limit the assessment. Reaching a landing is an intermediate event; a recorded building exit requires reaching the defined endpoint. Report stair travel, queues and merging movement within the same simulation, preserving occupant identity and counts across levels.

### Early engine feasibility check

By the end of Month 2, demonstrate two upper floors feeding a shared stair and an external target at discharge level. Check stair travel, landing queues, population accounting and a route restriction. A reference client must supply structured scenario values, launch work, obtain its status and retrieve results through the agreed contract. Confirm the engine licence/platform and the toolkit binding. See the [engine assessment](tools-and-references.md#early-engine-feasibility-check).

Use an existing engine that supports the required behaviour. Developing a new crowd solver or a custom coupling between independent floor simulators would add substantial work to this allocation. If the trial fails, resolve the engine, access or integration issue and revise the schedule; the final demonstration still requires multiple floors.

## Phase 1 Build the preparation capabilities

The first phase establishes what the building data can reliably tell us. A beginner learns the required concepts while implementing a small, inspectable workflow.

### Work to deliver

1. Learn the basics through the [guided exercises](learning-path.md). Agree officer planning questions, a sample model and the toolkit's discovery/execution interface in Month 1.
2. Register the supplied source model and obtain a checked IFC export if the input is a native authoring file.
3. Inspect the model's floors, elevations, units, spaces, openings, stairs, landings and obstacles. Produce a report of missing or ambiguous information and complete the early engine trial.
4. Extract the information needed for the chosen area, preserving source identifiers and coordinate mappings. Produce a focused IFC where useful for review or exchange.
5. Add a small semantic model: rooms, corridors, doors, stair flights, landings, external targets and reviewed connections within and between floors.
6. Expose inspection/preparation through the versioned contract, with source references, coverage and quality findings. Use a small review table and floor views to inspect and correct the data.

The detailed information selection is in [IFC data requirements](ifc-data-requirements.md). Manual annotation is acceptable for the first example when recorded clearly; measure the manual effort so later automation targets the right problems.

### Deliverables and acceptance

Deliver callable inspection/preparation functions, an intake/quality report, relevant geometry, source mappings, reviewed connections and a reference client. A reviewer should be able to trace each relevant object to its source. The toolkit consumer should receive model references and machine-readable findings.

Demonstrate connectivity from each included occupied floor through the reviewed stairs to the selected external targets. This checks the prepared relationships; detailed pilot-building movement comparisons come in Phase 2.

**Before Phase 2:** accept the connected-floor geometry, stair dimensions and relationships for the stated experiment, and record a feasible engine/integration route. Keep corrections, outstanding gaps and any need for a better export visible.

## Phase 2 Build and validate simulation capabilities

The second phase connects the prepared building to a pedestrian simulation engine and investigates how different assumptions affect the outcome.

### Work to deliver

1. Define the research question, population, movement assumptions, target locations and what constitutes a completed run.
2. Extend the engine adapter proven in Phase 1 to the pilot building, including stair flights, landings and routes through the discharge level.
3. Create three initial scenarios: a baseline, the same case with an exit or stair route unavailable, and a case with changed occupancy by floor. Keep the input editions and other assumptions fixed when isolating a change.
4. Check reviewed connections, stair behaviour, merging flows and restrictions. Account for occupants who remain on floors, wait in stairs or have no eligible route.
5. Compare repeated runs and vary uncertain assumptions. Define per-origin-floor arrival times, floor-clearance times, stair/landing queues, exit throughput and people remaining across the whole included model.
6. Review results against small known cases and appropriate reference evidence, recording where the model is useful and where it remains uncertain.
7. Expose scenario validation, run submission/status/cancellation and structured comparison through the contract. Record durable job references, errors, input versions and retry behaviour as the functions are built.

### Deliverables and acceptance

Deliver a working engine adapter, callable scenario/run/comparison operations, schemas, versioned scenarios, tracked jobs and experiment evidence. Repeat the examples from saved inputs and identify all relevant versions. Exercise invalid inputs, duplicate submission, cancellation and incomplete results alongside the movement checks.

Demonstrate that a route restriction changes both the allowed route and simulated movement, and that flows from different floors interact at shared landings. Incomplete and unsuccessful runs remain visible. Count an occupant as exited only at the defined external target; floor-clearance and stair-entry events have separate meanings. The [validation guide](validation-and-safety.md) defines the required checks.

**Before Phase 3:** demonstrate the agreed comparison to the pilot officer and confirm that the tested outputs answer the selected questions. Freeze the supported model and scenarios for the application pilot; estimate additional requirements separately.

## Phase 3 Package and demonstrate FDDE integration

The third phase makes the tested capabilities installable and discoverable in the FDDE Toolkit. Demonstrate the agent-assisted officer workflow and reserve time to correct integration and interpretation problems.

### Work to deliver

1. Package the module, its discovery manifest, versioned input/output schemas and one adapter for the agreed toolkit interface.
2. Complete installation/configuration, artifact retrieval, job controls, error handling and compatibility checks against the target harness.
3. Supply tool-use descriptions and examples so the existing toolkit agent can choose supported operations and identify missing information.
4. Demonstrate the agent discovering the module, constructing and validating supported scenarios, monitoring runs and returning a structured comparison with artifacts.
5. Pilot that workflow with a building officer, check the explanation against the returned measurements and correct the most important problems.
6. Deliver reproducible installation, contract tests, a reference client, troubleshooting and a maintainer handover. Keep optional dedicated UI work behind integration acceptance.

### Deliverables and acceptance

Deliver the module/integration package, registration configuration, test evidence, pilot findings and handover. Demonstrate the agreed toolkit discovering and calling the module end to end. The officer must be able to interpret floor clearance, stair queues and building exits from the toolkit's comparison and assessment artifacts. A reference-client test alone establishes local contract behaviour; actual toolkit integration requires its own demonstration.

The prototype produces draft planning assessments for review. Progress toward an operational evacuation product depends on the intended use and the validation requirements in the [existing framework](validation-and-safety.md#boundary-before-operational-use).

### Relationship to Panorama

Prepare an export package for building assets, versions, semantic records and quality information. The [pipeline architecture](pipeline-design.md#panorama-and-fdde-handoff) defines the ownership: Panorama may serve accepted assets; FDDE orchestrates the module's preparation and simulation capabilities.

Keep the asset handoff documented. Live Panorama ingestion/serving is a stretch goal; the FDDE module integration is core. The module can consume registered local references during development and adopt a Panorama asset adapter later.

## Monthly delivery checkpoints

| Month | Main focus | Visible output |
|---|---|---|
| 1 | Learn, frame the use case and agree integration | Fictional floor, pilot scope, sample request and agreement on module discovery, schemas, toolkit binding and deployment target |
| 2 | Inspect IFC and prove the callable engine route | Intake report plus a three-level stair/merge example; reference client supplies a scenario, obtains a job reference and retrieves results |
| 3 | Extract the connected floors and stair geometry | Floor overlays, elevations, stair/landing dimensions, source mappings and selection rules |
| 4 | Add and review building relationships | Complete routes from occupied floors through stairs to external targets, with ambiguity checks |
| 5 | Complete preparation capabilities | Callable inspection/preparation, schemas, connected-floor package and reference-client examples |
| 6 | Extend the proven adapter to the pilot building | One continuous model of floor movement, shared stairs, merging and discharge |
| 7 | Run the baseline through module operations | Scenario validation, durable run/status records and defined clearance, queue and exit measurements |
| 8 | Add comparisons and job controls | Route/occupancy variants, structured comparisons, cancellation/retry checks and occupant accounting |
| 9 | Validate and stabilise the module contract | Stair/merge evidence, schema/error tests, versioned outputs and agreement on pilot measures |
| 10 | Package and register the integration | Installable module, discovery manifest, one toolkit adapter and compatibility checks |
| 11 | Demonstrate agent-assisted comparison | Actual toolkit workflow, officer feedback and a prioritised correction list |
| 12 | Fix issues and hand over | Repeatable installation, integration evidence, tool-use examples and maintainer guide |

These are delivery targets. Review them monthly. Model readiness, engine access, the toolkit interface and access for integration testing are dependencies. The nominal six person-months include learning and corrections. Reduce optional dashboard or live Panorama work if needed; the reusable module and FDDE adapter remain core.

## People and scheduling

One person owns learning, data preparation, implementation, testing and documentation. Plan one main work item at a time and carry review feedback into that person's workload.

Occasional input from a building officer, model owner and relevant technical or evacuation specialist is useful for clarifying requirements and reviewing results. Their availability is a project dependency, not additional development capacity. If review input is unavailable, record the gap and limit what the demonstration claims.

Allow learning, review, documentation and bug fixing within each phase. A toolkit owner/contact is needed to agree discovery, caller context and deployment, and to enable integration testing. That contact is a dependency, not another implementer. Use one domain implementation and one toolkit binding, with a small reference client for development.

## Stretch goals after the core workflow

- Trial the importer on a second permitted IFC and record what needs manual correction.
- Add a live Panorama asset adapter.
- Build a dedicated officer dashboard beyond the existing toolkit interface and minimal review views.
- Extend beyond the agreed pilot floor coverage or add more complex movement cases after an effort assessment.

A generic BIM converter, multiple simulation engines, live sensor feeds and detailed hazard simulation are later extensions. They are not included in the six person-month core allocation.

## How this maps to the detailed backlog

| Phase | Existing milestones | Main backlog items |
|---|---|---|
| 1 Build the preparation capabilities | M0 to M3, including the Month 2 feasibility gate | B01 to B06, B14 and early B16: ingestion, connected floors, callable engine route and integration contract |
| 2 Build and validate simulation capabilities | M4 | B07 to B09, B15 and B17: scenarios, engine adapter, measurements, validation and jobs |
| 3 Package and demonstrate FDDE integration | M5 | B10 to B12 and B16 to B18: toolkit adapter, discovery, contract/integration tests and agent-assisted pilot; B13 is stretch |

See [milestones and starter backlog](project-plan.md) for implementation tasks and acceptance examples.

## Choices for the next refinement

- Confirm the project start month and how the half-time allocation will be protected.
- Identify the first building model, included floors, stair routes, external endpoints and building officer available for feedback.
- Confirm which suitable engine and automation licence/platform are available for the early trial.
- Confirm the toolkit's supported discovery/execution interface, deployment target and integration contact in Month 1.

The final module must be integratable with FDDE and agent ready. Building officers remain the demonstrated users, and multiple floors, twelve months and one half-time implementer remain confirmed. The remaining choices set the binding, calendar dates and pilot coverage.
