# HCI Cadence: CSxIxPxVx

## Purpose

This cadence describes a waterfall-style flow:

```text
Strategic Concept -> Operational Slices -> Implementation -> Pull Request / Integration -> Validation
```

Use this cadence when the team wants to complete planning before implementation,
complete implementation before integration, and complete integration before
product validation.

## Notation

```text
CSxIxPxVx
```

Meaning:

- `C`: define one Strategic Concept.
- `Sx`: define one or more Operational Slices.
- `Ix`: implement one or more approved slices.
- `Px`: perform one or more Pull Request / Integration steps.
- `Vx`: perform one or more Validation steps.

## Phase 1: Strategic Concept

Define the Strategic Concept according to:

```text
procedures/strategic-concept-design.md
```

Do not write implementation code during this phase.

## Phase 2: Operational Slices

Define the complete planned slice set according to:

```text
procedures/operational-slice.md
```

Do not begin implementation until the planned slice set is approved.

## Phase 3: Implementation

Implement the approved slices according to:

```text
procedures/implementation.md
```

Implementation should produce code, unit tests, documentation, and local
verification for the approved slices.

## Phase 4: Pull Request / Integration

Merge the implemented work with the project.

Typical work:

- pull request creation
- integration tests
- CI
- branch merge
- code review by teammates

## Phase 5: Validation

Validate the product result after integration.

Typical work:

- functional testing
- user acceptance
- performance checks
- correctness against requirements

## Control Risk

This cadence gives strong up-front planning structure, but it can delay feedback
from implementation and validation.

Use a more interleaved cadence when implementation evidence is likely to change
the slice design.
