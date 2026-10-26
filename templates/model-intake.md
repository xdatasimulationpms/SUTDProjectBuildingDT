---
type: Template
title: "Building Model Intake Record"
description: "Record source identity, export settings, coverage, quality issues and fitness for a specific experiment."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Building Model Intake Record

Copy this template into the project's ignored `local-data/` area for a real building. Leave unknown fields explicitly unknown rather than guessing.

## Purpose and source

| Field | Entry |
|---|---|
| Research question and intended use | |
| Building and selected floor/area | |
| Source owner and reviewer | |
| Permission and redistribution limits | |
| Native model filename and revision, if supplied | |
| IFC filename and file hash | |
| IFC schema and export software/version | |
| Export settings, linked models and omitted content | |
| Source revision/effective date, if known | |
| Received/imported at | |
| Supporting drawing or other review evidence | |

## Spatial checks

| Check | Finding and evidence |
|---|---|
| Intended floors and storeys present | |
| Units and a known reference dimension | |
| Coordinate frame, origin and any georeferencing | |
| Floor elevations and nested placements | |
| Spaces, doors, openings and major obstacles | |
| Ambiguous proxy or misclassified elements | |
| Missing relationships or properties | |

## Extraction and review

Record selection rules, output hashes, kept/excluded counts, sampled comparisons and any manual correction. State whether a focused IFC was produced and reopened successfully. Record the source locator for every reviewed example.

List unresolved issues with severity, affected area, owner and next action. Separate “file opens” from “fit for this experiment”.

## Outcome

- Review result: not reviewed / accepted for stated experiment / accepted with listed limits / rejected.
- Reviewer and date:
- Coverage and limits:
- Required follow-up:

Acceptance here is about input fitness for a research experiment, not building safety approval.
