# HCI Cadence: C((SxIx)PC)x

## Purpose

This cadence describes a scrum-style flow where a Strategic Concept frames the
work, a sprint-like cycle implements several slices, the work is integrated, and
the Strategic Concept is revisited before the next cycle.

Use this cadence when the team expects repeated planning and delivery cycles,
with each cycle producing integrated project changes before the next cycle is
planned.

## Notation

```text
C((SxIx)PC)x
```

Meaning:

- `C`: define or revise one Strategic Concept.
- `Sx`: define one or more Operational Slices for the cycle.
- `Ix`: implement one or more approved slices for the cycle.
- `P`: perform Pull Request / Integration for the cycle.
- `C`: revisit the Strategic Concept after integration.
- outer `x`: repeat the whole cycle one or more times.

## Cycle

Each cycle follows this shape:

```text
Strategic Concept -> Operational Slices -> Implementation -> Pull Request / Integration -> Strategic Concept Review
```

The second `C` is not a new unrelated Strategic Concept. It is a review and
revision point for the active Strategic Concept after integration evidence is
available.

## Phase 1: Strategic Concept

Define or revise the Strategic Concept according to:

```text
procedures/strategic-concept-design.md
```

## Phase 2: Operational Slices

Define the cycle's Operational Slices according to:

```text
procedures/operational-slice.md
```

The slice set should be small enough to integrate in one cycle.

## Phase 3: Implementation

Implement the approved slices according to:

```text
procedures/implementation.md
```

Implementation should produce code, unit tests, documentation, and local
verification for the approved slices.

## Phase 4: Pull Request / Integration

Merge the cycle's implemented work with the project.

Typical work:

- pull request creation
- integration tests
- CI
- branch merge
- code review by teammates

## Phase 5: Strategic Concept Review

After integration, revisit the Strategic Concept.

Ask:

- Did implementation evidence change the current state?
- Did integration reveal new constraints?
- Did the target state change?
- Are more Operational Slices needed?
- Should the Strategic Concept be marked implemented?

## Control Risk

This cadence can preserve feedback better than waterfall, but it can also blur
cycle boundaries if the team keeps adding slices without integration.

Keep each cycle small enough that the Strategic Concept review is based on
integrated evidence, not only local implementation progress.
