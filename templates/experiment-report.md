---
type: Template
title: "Evacuation Research Experiment Report"
description: "Record an executed experiment, including reproducibility, failed cases, results and limits."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Evacuation Research Experiment Report

**Scenario assessment only; not an approved evacuation plan.** Copy into `local-data/` for actual results. Do not fill measured fields before running the experiment.

## Question and execution

- Question and hypothesis:
- Date and operator:
- Source intake record and hashes:
- Geometry/topology editions and scenario revision:
- Included floors, stair systems, discharge route and external targets:
- Excluded floors/populations and their potential effect on shared stairs:
- Code revision and environment/engine/model versions:
- Module, schema and toolkit adapter versions:
- Toolkit client/harness version; local contract test or actual integration run:
- Job/run IDs, call trace and result artifact references:
- Run command or reproducible procedure:
- Seeds, time step, run horizon and repetitions:
- Hardware and processing time:
- Logs, trajectories and output locations:

## Checks performed

List the source, geometry, semantic, adapter and simulation checks that actually ran, their outcomes, and checks not yet performed. Link to review evidence. State whether this was a tutorial reproduction, synthetic test or real-model research case.

## Results

| Scenario | Attempted runs | Completed | Incomplete | Failed or invalid | People reaching targets and people remaining |
|---|---|---|---|---|---|
| | | | | | |

Define each reported measurement, its units, time origin, counting boundary and aggregation method. Include variation across runs. For incomplete runs, state the censoring horizon and remaining population; do not assign a completed evacuation time.

Report floor-clearance times, external arrivals by origin floor, stair/landing queues and the population remaining on floors or in stairs. Distinguish landing arrival from completion of the declared route. Record the identity/count checks across level transfers and the findings from the stair/merge test cases.

For an integration experiment, record discovery, input validation, job status, retry/cancellation and error-handling outcomes. Check the agent's presented numbers and caveats against the structured comparison and its artifact references.

## Interpretation

- What changed relative to the baseline?
- Is the difference robust to the tested assumptions and seeds?
- Which observations are model outputs rather than real-world evidence?
- What unexpected behaviour or failure occurred?
- What remains uncertain, and what would change the conclusion?
- What cannot be inferred about safety, accessibility or whole-building evacuation?

## Review and next experiment

- Reviewer and scope of review:
- Suitability for the stated research question:
- Reproduction status by a second person:
- Proposed next experiment or data request:
- Restrictions on onward use:
