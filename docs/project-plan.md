---
type: Roadmap
title: "Milestones and Starter Backlog"
description: "Implementation tasks for one half-time contributor delivering an agent-ready building and evacuation module for FDDE over twelve months."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Milestones and Starter Backlog

Deliver an agent-ready building ingestion and multi-floor evacuation module for FDDE within **twelve calendar months, with one person working half time**. The nominal six full-time person-months include learning, implementation, testing, feedback and documentation. Building-officer scenario comparison is the integration use case. The [module contract](toolkit-integration-contract.md) defines discovery, operations, jobs, outputs and acceptance.

The [three phase project overview](three-phase-plan.md) provides the overall delivery structure. This page contains the implementation detail beneath it:

| Phase and target period | Milestones | Backlog |
|---|---|---|
| 1 Build preparation capabilities, months 1 to 5 | M0 to M3; contract in Month 1 and engine feasibility by Month 2 | B01 to B06, B14 and early B16 |
| 2 Build and validate simulation capabilities, months 6 to 9 | M4 | B07 to B09, B15 and B17 |
| 3 Package and demonstrate FDDE integration, months 10 to 12 | M5 | B10 to B12 and B16 to B18; B13 is stretch |

## What success looks like

The toolkit discovers the packaged module and calls its documented operations. Its agent can validate and run supported scenarios, monitor jobs and retrieve structured comparisons on the prepared multi-floor model. A building officer interprets the assumptions and results through the toolkit workflow. Installation, contract tests and recorded integration evidence support handover.

## Delivery milestones

| Milestone | Deliverable | Demonstration or acceptance gate |
|---|---|---|
| M0 Learn and define the case | Introductory exercises, officer use case, toolkit interface agreement and available review contacts | Contributor explains the domain; discovery, schema, caller context and deployment expectations are recorded in Month 1 |
| M1 Register and inspect IFC | Local input registration, element inventory and quality report | Same input gives repeatable counts; wrong file type and missing units/coverage produce clear errors or review flags |
| M1a Prove callable multi-floor engine route by Month 2 | Stair/merge model, structured scenario input, job reference/status and result retrieval | Existing engine behaviour and callable execution route work from a reference client; licence/platform and selected toolkit binding are recorded |
| M2 Prepare connected floors | Source-linked floor geometry, stairs, landings, discharge routes and optional focused IFC | Elevations, dimensions and representative passages match reviewed references; every included route remains complete |
| M3 Review connections and expose preparation | Connected-floor model, evidence, schemas, preparation operations and a small review client | Routes and review status are checked; callers receive versioned artifacts and structured readiness findings |
| M4 Validate simulation capabilities | One engine adapter, tracked jobs, baseline and variants, structured measurements/comparisons | Stair/merge evidence and population checks pass; invalid requests, cancellation and duplicate submission behave as documented |
| M5 Package and demonstrate FDDE integration | Installable module, discovery manifest, one adapter, integration tests, agent-assisted pilot and handover | Actual toolkit discovers tools and completes the scenario workflow; officer interpretation matches the returned measures and limits |
| Later gate | Assisted movement, lifts, hazard coupling or operational-product investigation | Additional requirements, engine fit, effort and validation evidence agreed before implementation |

M1 and M2 may expose problems that require a better IFC export. That is a legitimate project outcome. Do not hide missing geometry with invented building facts to keep to a date.

## First sprint proposal

Treat the first two calendar weeks as a learning and feasibility sprint. At half time, this is approximately one full-time week of effort. A **spike** is a short investigation that ends in a finding, small demonstration or recommendation, rather than production code. Complete the core tasks below sequentially; the remaining spikes feed the rest of Phase 1.

| Priority and task | Kind | Output and completion test |
|---|---|---|
| Core: explain the pipeline using a fictional floor | Learning | A drawing and three proposed officer questions; review the explanation with available support |
| Core: establish a simple local Python workflow | Spike | Read a fictional JSON record and run a small failing/passing check; record environment details |
| Core: request a model and confirm a pilot contact | Dependency | A request for the IFC and matching drawing; record available source information and the next follow-up |
| Core discovery: identify the toolkit integration contact | Dependency | Record the supported tool registration/transport, deployment target and who can enable integration testing; settle the contract during Month 1 |
| Next: compare the viewer and programmatic inventory | Spike | Inspect spaces/doors in the received sample and count them with IfcOpenShell; explain differences |
| Next: test one extraction on a copy | Spike | Compare selected objects and dependencies before/after; report whether a focused IFC is reliable |
| Next: annotate a tiny topology manually | Spike | A few spaces and passages with source/evidence references and review states |
| By Month 2: prove stairs and callable execution | Feasibility spike | Two upper floors and a discharge level; reference client supplies a scenario, obtains job status and retrieves results through the selected interface |

The first sprint is complete when the contributor can explain the small case, run the initial Python exercise and identify the model and user inputs still needed. Inspecting and preparing the supplied IFC continues through Phase 1.

## Sample implementation backlog

All items are initially unstarted. Order them after the spikes; keep acceptance tests with the work item.

| ID | Proposed task | Acceptance example |
|---|---|---|
| B01 | Input manifest and file fingerprint | Same bytes produce the same hash; missing/unsupported input is reported |
| B02 | Callable IFC inspection | Return versioned inventory/quality artifacts with explicit missing information and coverage |
| B03 | Versioned selection rules | Chosen/excluded elements and reasons can be reproduced |
| B04 | Connected-floor geometry and source overlays | Check each floor's elevation, stairs, landings, passages and complete discharge route; invalid geometry blocks downstream use |
| B05 | Reviewed semantic records | Review horizontal and vertical connections separately; retain evidence and correction history |
| B06 | Connectivity checks | Check routes from all included occupied floors to external targets, including blocked/unknown stair connections and isolated populations |
| B07 | Scenario definition and validation operation | Bind typed parameters and validation to fixed input/engine editions; reject invalid references and unsupported settings |
| B08 | Multi-floor engine adapter | Connect the full selected model; preserve occupant identity, stair interactions and scenario restrictions |
| B09 | Callable runs and structured measurements | Return run references and measures with units, coverage and scenario outcomes; retain incomplete/failed runs and versioned artifacts |
| B10 | Reference client and toolkit result presentation | Same operations serve the test client and toolkit; officer can inspect source links, assumptions and comparison artifacts |
| B11 | Installation and maintainer guide | Repeat package installation, engine configuration, registration and example calls from the guide |
| B12 | Agent-assisted officer pilot | Toolkit agent discovers tools, validates scenarios, submits/monitors runs and explains measured comparisons; record officer feedback and interpretation errors |
| B13 stretch | Trial a second permitted IFC model | After the core pilot, document import effort, required corrections and building-specific changes; update the reuse guide |
| B14 Phase 1 | Early engine and integration feasibility | By Month 2, show the stair/merge example through structured calls, job/status/result references and a reference client; record binding and engine access |
| B15 Phase 2 | Stair and merging validation | Test travel, merging, restrictions and count conservation across levels; verify that landing arrival does not count as building exit |
| B16 Phases 1 and 3 | Module contract, schemas and discovery adapter | Agree contract in Month 1; deliver one toolkit binding, versioned schemas, capabilities, engine limits and registration configuration |
| B17 Phase 2 | Persistent jobs, cancellation and retry behaviour | Persist jobs; reconcile interruption; duplicate submission returns the original run; cancellation reflects actual worker state |
| B18 Phase 3 | Contract and integration acceptance | Exercise valid/invalid inputs, failed/censored runs, incompatible comparisons and the real toolkit workflow; record tested versions and evidence |

## Questions to refine the delivery targets

- What is the start month, and how will the half-time allocation be scheduled?
- What authoring format and IFC schema will the first building provide?
- Are spaces, openings, linked models and a matching reference drawing available?
- Which planning questions should the building officer answer with the first tool?
- Who can review building semantics, and who can review evacuation assumptions and results?
- Which operating system and package releases will the contributor use?
- Which occupied floors, stair routes, discharge level and external endpoints belong in the pilot? What is omitted?
- Which existing engine and automation licence are available for the Month 2 trial?
- Which discovery/transport and deployment interface does the FDDE Toolkit support, and who can enable registration and integration testing?
- Which minimum validation evidence is required before showing results beyond the project team?

## Risks to watch early

| Risk | Early signal | Response |
|---|---|---|
| Unusable export | Missing spaces or openings; inconsistent floor coordinates | Ask for corrected export or use reviewed manual annotation with stated limits |
| Incorrect connections | Doors assigned to the wrong room or floor | Small labelled reference set; require human review before publication |
| Misleading simulation | All agents disappear at a floor target labelled “safe” | Define outcomes and simulation boundary before building plots |
| Excessive beginner workload | Many tools installed but no repeatable small output | Return to one exercise; schedule mentor support |
| Engine or integration mismatch | Stair/merge behaviour or officer-app parameter/run access cannot be demonstrated | Resolve engine/access and revise the schedule at Month 2; keep multi-floor delivery in core scope |
| Toolkit interface arrives late | Discovery, caller context or deployment assumptions remain unconfirmed | Agree a small contract in Month 1; use a reference client early and reserve access to the actual toolkit for integration acceptance |
| Non-reproducible result | Model/version/parameters missing | Make run manifests and test fixtures part of acceptance |

Next: [validation and safety](validation-and-safety.md).
