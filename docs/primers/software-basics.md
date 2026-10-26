---
type: Technology Guide
title: "Software Basics for This Project"
description: "The small set of programming and data practices needed before building the pipeline."
generated: { by: openai/codex, at: 2026-10-26T00:00:00Z }
status: draft
---
# Software Basics for This Project

You do not need to become an expert in every part of software development. Begin by learning to read data, transform it without losing the original, and test that the transformation did what you intended.

## Words you will encounter

| Term | Meaning here |
|---|---|
| Repository | The project folder and its version history |
| Git | A tool that records selected changes to project files |
| Commit | A named local snapshot of changes; it is not an upload |
| Remote and push | A remote is another repository; pushing sends commits there |
| Python | The proposed programming language for extraction and experiments |
| Script | A saved program you can run again |
| Package | Reusable code maintained by another project |
| Virtual environment | A project-specific place for Python packages, separate from other projects |
| JSON | A text format for structured data, using named fields, lists and values |
| API | A defined way for one piece of software to request something from another |
| Toolkit adapter | A small layer that maps the toolkit's calls to this project's functions |
| Schema | A machine-readable definition of allowed fields, types and required values |
| Job | A tracked piece of work that may continue after the initial call returns |
| Module manifest | A description of the module's capabilities, version, inputs, outputs and requirements |
| Test | A check that compares software behaviour with an expected result |
| Hash | A fingerprint used to check whether a file's bytes changed |

## A tiny data example

This is fictional teaching data, not a simulator input contract:

```json
{
  "example_only": true,
  "floor": "fictional-ground-floor",
  "spaces": [
    {"id": "room-a", "name": "Office A"},
    {"id": "corridor-c", "name": "Corridor C"}
  ],
  "candidate_connections": [
    {
      "from": "room-a",
      "to": "corridor-c",
      "through": "door-d1",
      "review_status": "unreviewed"
    }
  ]
}
```

A first Python exercise is to load this data, print the two space names, and check that the connection references existing spaces. Do not make an unreviewed connection usable merely because its IDs are valid.

## Learn these programming concepts first

1. Variables, strings, numbers and true/false values.
2. Lists and dictionaries, which resemble the example above.
3. Loops for processing each element, and functions for repeatable operations.
4. Reading files without altering them, writing results to a different location, and handling errors.
5. Small tests, including cases that should fail.

The [official beginner links](../tools-and-references.md#programming-and-version-control) include material for people new to programming. A tutorial written for experienced developers may move too quickly; start with the beginner route.

## A working habit for every change

Read the input → state the expected output → make one small change → run the check → inspect the difference → record what happened.

For example, a test might require every transition to refer to an existing passage. Another should require a missing width to stay unknown rather than becoming zero or a guessed default.

Git tracks selected files, not everything on the computer. Before a commit, inspect which files are included. Keep real building inputs and generated layouts under the ignored `local-data/` directory. An ignore rule does not remove a file already committed and does not protect data uploaded through another tool.

## Installation comes after choosing a small exercise

The [agent module explanation](#how-the-toolkit-agent-uses-a-module) describes how these software habits support FDDE integration.

For now, the repository can be read without installing anything. When coding begins, agree a supported Python version and compatible package releases, create an environment and record exact versions after a successful smoke test. Do not start by installing every tool in the reference list.

The first smoke tests should be: read a tiny JSON file; open one IFC and count elements; run one small pedestrian tutorial. Test these separately before joining them. The project does not yet supply installation scripts or an application launch command.

## How the toolkit agent uses a module

The officer asks a planning question. The FDDE agent selects a named operation and supplies structured arguments, such as a model reference and occupants per floor. The module validates those fields, runs the appropriate processing function and returns structured results or a clear error.

For a long simulation, the first response contains a job reference. The toolkit can ask for its status and retrieve result artifacts when it finishes. The module must distinguish an engine failure, an unfinished scenario and a completed run.

Agent readiness comes from those defined operations, schemas, results and tested failure behaviour. The FDDE Toolkit supplies the conversational agent. This project supplies the reliable functions and integration package described in the [contract](../toolkit-integration-contract.md).
