---
type: Roadmap
title: "Milestones and Starter Backlog"
description: "A staged route from beginner learning to a reviewed single-floor scenario demonstration."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Milestones and Starter Backlog

Deliver a narrow end-to-end result before expanding to a complete building. The milestones below are proposed gates, not scheduled commitments. Set dates after confirming contributor availability, a usable model and review support.

## What success looks like

A new contributor can take a permitted IFC, identify the selected floor, explain how its movement model was derived, compare three scenarios, and hand another person the records needed to reproduce and critique the experiment. Important gaps remain visible.

## Delivery milestones

| Milestone | Deliverable | Demonstration or acceptance gate |
|---|---|---|
| M0 Learn and define the case | Completed introductory exercises, one fictional floor, named technical and domain reviewers | Contributor explains BIM/IFC, source versus scenario, and the difference between connectivity and safety |
| M1 Register and inspect IFC | Local input registration, element inventory and quality report | Same input gives repeatable counts; wrong file type and missing units/coverage produce clear errors or review flags |
| M2 Prepare one floor | Source-linked elements, local floor geometry and optional focused IFC | Known dimensions and representative openings match the reviewed reference; exclusions and manual corrections are recorded |
| M3 Review connections | Spaces, passages, directed transitions, evidence and a simple review interface | Known routes pass; a blocked passage is excluded; unknown evidence stays unknown; no cross-floor shortcut appears |
| M4 Compare scenarios | Tested engine adapter, baseline and two variants, repeatable run reports | Restrictions agree in topology and movement; incomplete runs retain unserved people; findings include uncertainty and assumptions |
| M5 Package the research demonstration | Simple local application, reproducible workflow and handover guide | A second person repeats the case from a clean environment and explains the model's limits |
| Later gate | Multi-floor/assisted movement, hazard coupling or operational-product investigation | Requirements, engine fit, licences, validation evidence and qualified review agreed before implementation |

M1 and M2 may expose problems that require a better IFC export. That is a legitimate project outcome. Do not hide missing geometry with invented building facts to keep to a date.

## First sprint proposal

Treat this as a learning and feasibility sprint. A **spike** is a short investigation that ends in a finding, small demonstration or recommendation, rather than production code.

| Task | Kind | Output and completion test |
|---|---|---|
| Explain the pipeline using a fictional floor | Learning | A diagram and three bounded research questions; mentor checks the explanation |
| Establish a simple local Python workflow | Spike | Read a fictional JSON record and run a small failing/passing test; record environment details |
| Obtain one permitted IFC and supporting drawing | Dependency | Intake record with source owner, revision, schema, use permission and known omissions |
| Compare the viewer and programmatic inventory | Spike | Inspect spaces/doors in Bonsai and count them with IfcOpenShell; explain differences |
| Test one extraction on a copy | Spike | Compare selected objects and dependencies before/after; report whether a focused IFC is reliable |
| Annotate a tiny topology manually | Spike | A few spaces and passages with source/evidence references and review states |
| Review intended use and engine choice | Decision preparation | Record academic experiment scope, later product requirements and unresolved suitability questions |

Do not promise the full application in this sprint. The exit criteria are: the contributor has a repeatable environment, the team knows whether the sample is usable, and the next implementation task is bounded.

## Sample implementation backlog

All items are initially unstarted. Order them after the spikes; keep acceptance tests with the work item.

| ID | Proposed task | Acceptance example |
|---|---|---|
| B01 | Input manifest and file fingerprint | Same bytes produce the same hash; missing/unsupported input is reported |
| B02 | IFC inventory report | Schema, units, storeys and relevant element counts are visible; missing spaces are explicit |
| B03 | Versioned selection rules | Chosen/excluded elements and reasons can be reproduced |
| B04 | Floor geometry and source overlay | Scale, floor and door locations agree with reviewed references; invalid geometry blocks downstream use |
| B05 | Reviewed semantic records | Candidate and accepted connections are separate; correction history is retained |
| B06 | Connectivity checks | Test blocked, unknown, one-way and disconnected cases; retain all affected populations |
| B07 | Scenario definition | References fixed building/rule versions; rejects invalid references and unsupported features |
| B08 | First engine adapter | Uses tested geometry and routing; applies scenario restrictions consistently; reports unsupported cases |
| B09 | Batch run and measurement | Records versions/seeds; separates completed, censored, failed and invalid runs |
| B10 | Local review and comparison screens | A reviewer can inspect source links, change only a scenario and export its assessment |
| B11 | Reproduction guide | Another contributor repeats the accepted small example without hidden local state |

## Questions to resolve before choosing dates

- What authoring format and IFC schema will the first building provide?
- Are spaces, openings, linked models and a matching reference drawing available?
- Is the goal academic exploration, internal planning support, or an eventual operational/commercial product?
- Who can review building semantics, and who can review evacuation assumptions and results?
- Which operating system and package releases will the contributor use?
- What counts as the target: leaving a room, leaving a floor, leaving the building or reaching an assessed external destination?
- Which minimum validation evidence is required before showing results beyond the project team?

## Risks to watch early

| Risk | Early signal | Response |
|---|---|---|
| Unusable export | Missing spaces or openings; inconsistent floor coordinates | Ask for corrected export or use reviewed manual annotation with stated limits |
| Incorrect connections | Doors assigned to the wrong room or floor | Small labelled reference set; require human review before publication |
| Misleading simulation | All agents disappear at a floor target labelled “safe” | Define outcomes and simulation boundary before building plots |
| Excessive beginner workload | Many tools installed but no repeatable small output | Return to one exercise; schedule mentor support |
| Engine mismatch | Required stairs, assistance or operational use unsupported | Stop scope expansion; compare engines on the actual requirement |
| Non-reproducible result | Model/version/parameters missing | Make run manifests and test fixtures part of acceptance |

Next: [validation and safety](validation-and-safety.md).
