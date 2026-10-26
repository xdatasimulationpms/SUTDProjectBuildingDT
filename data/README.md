# Local Data and Reproducibility

This repository contains no building models or simulation results. Store real inputs and outputs outside tracked documentation, for example in the ignored `local-data/` directory at the repository root.

Create the following directories when needed; they are a proposed layout, not existing data:

```text
local-data/
  building-example/
    source/                 unchanged native packages and supplied IFC
    intake/                 provenance, permissions and quality findings
    derived/edition-001/    focused IFC, geometry, tables and file hashes
    reviews/                annotations, evidence and correction history
    scenarios/              hypothetical changes and fixed input references
    runs/                   engine inputs, trajectories, logs and reports
```

## Handling rules

- Preserve original files. Derive new editions; never overwrite the only source.
- Keep complete local manifests with hashes, source IDs, units, transforms, tool versions and processing settings.
- Record whether source and derived data may be shared. A public tutorial sample still needs its licence checked before redistribution.
- Do not upload building models or results simply to make a viewer or tutorial work. Prefer local processing unless the owner requests otherwise.
- Back up needed local data through an agreed method. Git does not back up ignored files.
- Check the selected files before committing. `.gitignore` does not remove already tracked files and cannot stop a separate upload tool.

## Sharing a repeatable project later

Separate the reproducible **method** from access to a particular building. Publish code, tested dependency versions, schemas, settings, documented commands and small independently authored synthetic test fixtures when approved. Describe how another contributor can supply their own IFC and run the same checks.

A real-model package can be shared separately only under its agreed permissions. Keep its input requirements and known limitations in the method documentation so the project remains useful without access to that building.
