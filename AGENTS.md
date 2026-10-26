# Contributor and Agent Instructions

## Read in order

Read `README.md`, `docs/index.md`, then the documents relevant to the task. This is a documentation-first execution project, not an implemented simulator. Code may be added when requested; do not describe planned features as delivered.

## Preserve meaning and evidence

- Use plain language and explain a technical term before relying on it.
- Separate source findings, proposed designs, assumptions, measured results and owner decisions. Do not invent test outcomes or cite a simulation as an observation of a real building.
- Keep upstream building records unchanged. Retain file hashes, editions, units, coordinate transforms and source element identifiers in derived outputs.
- A native BIM authoring file is not automatically readable by IfcOpenShell. Confirm a supported export route before promising conversion.
- Missing or conflicting connection/access evidence remains `unknown`, never silently traversable.
- A door's nominal dimension is not necessarily usable clear width. Adjacent rooms are not necessarily connected. A closed door leaf is not necessarily an unavailable passage.
- Scenario overrides never overwrite source facts or accepted operational plans.

## Safety and scope

This project supports research and planning comparisons. Do not claim code compliance, accessibility certification, safe evacuation, or authority to issue emergency instructions. Follow `docs/validation-and-safety.md`. A successful render, simulation run or information check is not a safety assessment.

Keep the initial scope to a reviewed single-floor case. Multi-floor movement, lifts, fire/smoke, assisted evacuation and live guidance require explicit new requirements and validation. JuPedSim is an academic experiment candidate, not an approved operational engine.

## Data and dependencies

- No real BIM files, derived building layouts, occupant records, credentials or run outputs in Git by default. Use `local-data/`; `.gitignore` is a convenience, not an access control or backup.
- Do not upload inputs, use paid services or publish a remote without the owner's request.
- A reusable sample needs clear permission and attribution before it is committed. Prefer tiny, independently authored synthetic fixtures.
- When implementation begins, select compatible supported releases, record licences, pin a tested environment and run the documented smoke tests. Do not mix current tutorials with old APIs without checking.
- Start with simple local processing. Add services or GPU dependencies only for a demonstrated need.

## Maintain the documentation

Use relative links, descriptive lower-case kebab-case filenames, and the metadata pattern already used under `docs/`. Keep the index and `CHANGELOG.md` current. Date time-sensitive tool claims and cite primary documentation near consequential claims. Repository proposals are not vendor guarantees.

Before handing over, check internal links and any code/tests added. Report what was actually run and what remains unimplemented. Preserve unrelated user changes. Do not commit or push unless requested.
