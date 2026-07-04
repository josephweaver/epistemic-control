# HCI Schema: concept(slice)+ (impl)+

## Purpose

This schema describes a Human-Computer Interaction cadence where a Strategic
Concept is defined first, Operational Slices are defined one prompt at a time,
and approved slices are implemented afterward in order.

Use this cadence when the team needs to understand the shape of the whole
Strategic Concept before implementation begins, while still keeping each slice
small enough for human review.

Use `hci-levels.md` for HCI specification details.

## Notation

```text
concept(slice)+ (impl)+
```

Meaning:

- Define one Strategic Concept.
- Define one or more Operational Slices.
- Define each Operational Slice in its own prompt.
- After the slice set is approved, implement the slices one by one.
- Implementation prompt limits are defined in `hci-levels.md`.

## Phase 1: Strategic Concept Definition

The Strategic Concept definition happens first. It describes the larger system
change without committing to implementation in the same prompt.

Write the Strategic Concept according to:

```text
procedures/strategic-concept-design.md
```

Do not write implementation code while defining the Strategic Concept.

## Phase 2: Operational Slice Definition

After the Strategic Concept is defined, define one or more Operational Slices.

Each slice is defined in a separate prompt. This keeps each slice small enough
to review and gives the human a clear checkpoint before the next slice is
designed.

Design each slice according to:

```text
procedures/operational-slice.md
```

Do not begin implementation until the agreed slice set is ready.

## Phase 3: Implementation

After the agreed slices are ready, implement them in order according to:

```text
procedures/implementation.md
```

This schema adds one sequencing rule on top of the implementation instructions:
finish the slice design phase before starting the implementation phase.
