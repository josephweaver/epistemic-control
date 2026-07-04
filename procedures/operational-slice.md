# Operational Slice

Last updated: 2026-07-04

## Purpose

This document defines how to create an Operational Slice.

An Operational Slice is one bounded implementation task inside a Strategic
Concept. It should provide enough context for Codex or another coding agent to
make a focused change without reading the whole repository.

## Precision And Language

When explaining an Operational Slice's current state and target state in chat,
be as precise as the available evidence allows. Avoid jargon, vague labels, and
ambiguous words.

Prefer naming the actual type, function, command, config field, file, package,
test, or behavior involved. If a statement is an inference, say that it is an
inference. If evidence is missing, say what evidence is missing.

Documentation may be more detailed than chat, but it should still use precise
language. Do not use broad terms such as "integration", "runtime", "manager",
or "support" unless the slice explains exactly what the term means in that
context.

## Core Rule

The human must be able to state the desired action concretely.

Good:

```text
Add CopyInto behavior to SSHTransport.
```

Bad:

```text
Improve SSH support.
```

If the request is vague, first create or update the Strategic Concept README. Do
not create Operational Slices until the human and AI can state a concrete action.

## Directory Layout

Strategic Concept directories live under:

```text
docs/concepts/<concept-name>/
```

Each Strategic Concept folder should contain:

```text
README.md
001-<slice-name>.md
002-<slice-name>.md
003-<slice-name>.md
```

Example:

```text
docs/concepts/ssh-transport/
  README.md
  001-sshtransport-config.md
  002-sshtransport-connect.md
  003-sshtransport-copyinto.md
```

The Strategic Concept README is broad. Individual Operational Slices are narrow.

## Slice Creation Process

Slice creation is interactive.

The AI must not immediately commit a slice from a vague request. Instead, the
human and AI should work through the scope until both agree on:

- Objective
- Current state
- Target state
- Concept decision
- Allowed files
- Tests
- Out of scope
- Acceptance criteria
- Notes

Only after agreement should the slice be committed to the repository.

## Slice Template

```markdown
# <NNN> <Slice Title>

Status: proposed

## Objective

<One or two sentences describing the concrete behavior to add or change.>

## Current State

<What exists before this slice begins. Include the relevant implementation
detail needed to understand the change.>

## Target State

<What will exist after this slice is complete. Include the expected production,
test, or documentation artifacts.>

## Concept Decision

<Say whether this slice adds a new concept or updates an existing concept. If it
adds a new concept, say whether that concept needs its own file and why.>

## Required Context

Read these files first:

- <Strategic Concept README or architecture document>
- <relevant production file>
- <relevant test file>

Do not read unrelated files unless test failures directly require it.

## Allowed Production Files

- <path/to/file.go>

## Allowed Test Files

- <path/to/file_test.go>

## Out Of Scope

- <explicit non-goal>
- <explicit non-goal>
- <explicit non-goal>

## Acceptance Criteria

- <observable behavior>
- <observable behavior>
- <observable behavior>

## Notes

- <implementation hint, architectural constraint, or sequencing note>
```

## Required Fields

### Objective

The objective is the most important part of the slice.

It must describe a concrete action.

Good:

```text
Add CopyInto behavior to SSHTransport so the transport can copy a local file into a remote path over SFTP.
```

Bad:

```text
Improve SSH support.
```

### Current State

The current state describes what exists before this slice begins.

Unlike a Strategic Concept's current state, a slice's current state may include
bounded implementation detail. It should explain enough of the present code
shape for a coding agent to make the change without rediscovering the design.

Include details such as:

- The existing type, function, command, config field, file, or package being
  changed.
- The behavior that currently exists.
- The limitation or mismatch the slice addresses.
- Any nearby tests that describe the current behavior.

Avoid broad repository summaries. The current state should be local to the
slice.

### Target State

The target state describes what will exist after this slice is complete.

At the slice level, target state should begin to name implementation artifacts.
It may identify the concrete production file, type, function, test, command
behavior, or documentation update that will prove the slice exists.

The target state should be specific enough to guide implementation, but it
should not prescribe every line of code.

### Concept Decision

Before finalizing a slice, decide whether the work adds a new concept or updates
an existing concept.

If the slice updates an existing concept, prefer the file or package that
already owns that concept.

If the slice adds a new concept, decide whether the concept needs its own file.
A new file is usually justified when:

- The new concept has its own struct or interface.
- The new concept has a meaningful set of methods or helper functions.
- Keeping it in an existing file would mix unrelated responsibilities.
- The new concept is likely to be tested or reasoned about independently.
- Two structs would otherwise share one file while owning separate behavior.

A new file is not justified merely because the slice is new. Keep small helper
functions near the concept they support when they do not form a separate
concept.

### Required Context

This section controls context size.

It tells the coding agent what to read before implementing. Keep this list
short.

Avoid telling the agent to read the whole repository.

### Allowed Production Files

This is the slice's production-file boundary.

The coding agent may modify only these production files unless it reports that
the slice cannot be completed within the approved boundary.

### Allowed Test Files

The coding agent may modify only these test files unless it reports that the
slice cannot be tested within the approved boundary.

### Out Of Scope

This prevents scope creep.

Include anything tempting but not part of the current slice.

### Acceptance Criteria

Acceptance criteria define what must be true when the slice is complete.

They should describe observable behavior, not implementation preference.

### Notes

Notes may include architectural constraints, sequencing details, or
implementation hints.

Use notes to prevent known mistakes without over-specifying implementation.

## Slice Rules

1. Build slices one by one.
2. Do not create broad slices from vague goals.
3. Every slice belongs to a Strategic Concept folder.
4. Every Strategic Concept folder has a README.
5. Every slice has a concrete objective.
6. Every slice describes the current state before implementation.
7. Every slice describes the target state after implementation.
8. Every slice decides whether it adds a new concept or updates an existing one.
9. Every slice has allowed production files and test files.
10. Every slice has explicit out-of-scope boundaries.
11. Every slice has acceptance criteria.
12. Do not include EC mode in slice files. Creating the slice is the
    user-specified planning action.
13. Do not commit the slice until the human and AI agree on the final scope.

## Agent Behavior

When asked to create a slice, the agent should:

1. Ask the human for the concrete action if the request is vague.
2. Identify or propose the Strategic Concept folder.
3. Check whether the Strategic Concept README exists.
4. Draft the slice.
5. Review the objective, current state, target state, concept decision, allowed
   files, tests, out of scope, and acceptance criteria with the human.
6. Revise until agreed.
7. Commit the slice only after agreement.

## Completion Check

Before creating a new slice, the AI should compare the completed slices with the
Strategic Concept's proposed slices.

If the goals of the Strategic Concept appear to have been achieved, the AI
should suggest that no additional slices are necessary and recommend reviewing
the Strategic Concept for completion instead of automatically creating another
slice.

## Summary

Strategic Concept READMEs describe broad system change.

Operational Slices describe bounded implementation actions.

A good slice lets Codex perform a focused change without loading the whole
project into context.
