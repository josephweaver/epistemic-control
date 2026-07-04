# HCI Cadence: C(SI)x

## Purpose

This schema describes a Human-Computer Interaction cadence where one Strategic
Concept is developed through repeated Operational Slice design and
implementation pairs.

Use this cadence when implementation evidence may change how later slices should
be designed.

Use `hci-levels.md` for HCI specification details.

## Notation

```text
C(SI)x
```

Meaning:

- Define one Strategic Concept.
- Define one Operational Slice.
- Implement that slice.
- Review and commit the accepted slice.
- Repeat the slice-and-implementation pair until the Strategic Concept is
  complete.

## Phase 1: Strategic Concept Definition

The Strategic Concept definition happens first. It describes the larger system
change without committing to implementation in the same prompt.

Write the Strategic Concept according to:

```text
procedures/strategic-concept-design.md
```

Do not write implementation code while defining the Strategic Concept.

## Phase 2: Slice And Implementation Pairs

After the Strategic Concept is ready, repeat one slice-and-implementation pair
at a time.

For each pair:

1. Define one Operational Slice according to:

   ```text
   procedures/operational-slice.md
   ```

2. Implement only that slice according to:

   ```text
   procedures/implementation.md
   ```

3. Run the narrowest useful verification.
4. Stop for human review.
5. Commit and push the accepted slice before designing or implementing the next
   slice.

All slices for the Strategic Concept stay on one concept branch. Open one pull
request for the complete Strategic Concept after all agreed slices are
implemented.

## Unique Sequencing Rule

This schema allows the next slice to be designed after the previous slice has
been implemented.

Use this when the team expects implementation evidence, test results, or code
shape to affect the next slice's current state, target state, or concept
decision.

Do not design multiple future slices just to create momentum. Each new slice
should be based on the current project state after the previous accepted slice.
