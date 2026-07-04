# HCI Schema: epic(feature)+ (Impl)+

## Purpose

This schema describes a Human-Computer Interaction cadence where an epic is
defined first, feature slices are defined one prompt at a time, and approved
feature slices are implemented afterward in order.

Use this cadence when the team needs to understand the shape of the whole epic
before implementation begins, but still wants each feature slice to remain small
enough for human review.

## Notation

```text
epic(feature)+ (Impl)+
```

Meaning:

- Define one epic.
- Define one or more feature slices.
- Define each feature slice in its own prompt.
- After the feature-slice set is approved, implement the feature slices one by
  one.
- A single feature implementation may use more than one prompt when required by
  the active HCI budget.

## Phase 1: Epic Definition

The epic definition happens first. It describes the larger outcome without
committing to implementation in the same prompt.

Write the epic according to:

```text
procedures/epic.md
```

Do not write implementation code while defining the epic.

## Phase 2: Feature Slice Definition

After the epic is defined, define one or more feature slices.

Each feature slice is defined in a separate prompt. This keeps each slice small
enough to review and gives the human a clear checkpoint before the next slice is
designed.

Design each feature slice according to:

```text
procedures/epic-slice.md
```

Do not begin implementation until the agreed feature-slice set is ready.

## Phase 3: Implementation

After the agreed feature slices are ready, implement them in order according to:

```text
procedures/implementation.md
```

This schema adds one sequencing rule on top of the implementation instructions:
finish the feature-slice design phase before starting the implementation phase.
