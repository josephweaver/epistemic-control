# HCI Cadence Filename Convention

HCI cadence filenames use compact shorthand for Strategic Concept, Operational
Slice, Implementation, Review, Pull Request / Integration, and Validation
sequencing.

## Tokens

`C` = Strategic Concept

> What are we trying to build?

`S` = Operational Slice

> What coherent capability are we implementing next?

`I` = Implementation

Produce the slice.

- code
- unit tests
- documentation
- local verification

`R` = Epistemic Review

Close the gap between AI implementation and programmer understanding.

Review is not only code review. It verifies that the human can explain,
navigate, debug, and safely modify what was implemented.

- AI code review
- architecture review
- implementation walkthrough
- human understanding
- prediction before explanation
- "Do I understand what just happened?"

`P` = Pull Request / Integration

Merge with the project.

- integration tests
- CI
- branch merge
- code review by teammates

`V` = Validation

Validate the product.

- functional testing
- user acceptance
- performance
- correctness against requirements

## Operators

- Parentheses group steps that repeat together.
- Lowercase `x` means one or more repetitions of the preceding token or
  parenthesized group.
- A hyphen `-` means zero or one instance of the preceding token or
  parenthesized group.

## Examples

```text
CSxIx.md
```

Meaning:

- Define one Strategic Concept.
- Define one or more Operational Slices.
- After slice design is complete, implement one or more approved slices.

```text
C(SI)x.md
```

Meaning:

- Define one Strategic Concept.
- Repeat an Operational Slice plus Implementation pair one or more times.

```text
C(SI)x(R).md
```

Meaning:

- Define one Strategic Concept.
- Repeat an Operational Slice plus Implementation pair one or more times.
- Perform one Review after the repeated slice-implementation work is complete.

```text
(C-S-I)x (vibe).md
```

Meaning:

- Repeat one or more exploratory passes.
- In each pass, optionally define or revise a Strategic Concept.
- In each pass, optionally define or revise an Operational Slice.
- In each pass, perform one Implementation.
- This is the cadence commonly called vibe coding.

```text
CSxIxPxVx (waterfall).md
```

Meaning:

- Define one Strategic Concept.
- Define one or more Operational Slices.
- Implement one or more approved slices.
- Perform one or more Pull Request / Integration steps.
- Perform one or more Validation steps.
- This is a waterfall-style cadence.

```text
C((SxIx)PC)x (scrum).md
```

Meaning:

- Define or revise one Strategic Concept.
- Define and implement one or more Operational Slices in a cycle.
- Perform Pull Request / Integration for the cycle.
- Revisit the Strategic Concept after integration.
- Repeat the cycle one or more times.
- This is a scrum-style cadence.

## Naming Rule

Use the compact filename for the cadence and put the readable title inside the
document.

Examples:

- `CSxIx.md` has title `HCI Cadence: CSxIx`.
- `C(SI)x.md` has title `HCI Cadence: C(SI)x`.
- `C(SI)x(R).md` has title `HCI Cadence: C(SI)x(R)`.
- `(C-S-I)x (vibe).md` has title `HCI Cadence: (C-S-I)x`.
- `CSxIxPxVx (waterfall).md` has title `HCI Cadence: CSxIxPxVx`.
- `C((SxIx)PC)x (scrum).md` has title `HCI Cadence: C((SxIx)PC)x`.

## When To Use

| Cadence | Use When |
| --- | --- |
| `(C-S-I)x` | Exploratory local coding. |
| `C(SI)x` | Learning from each slice before designing the next. |
| `CSxIx` | Planning slices first, then implementing. |
| `CSxIxPxVx` | Waterfall. |
| `C((SxIx)PC)x` | Scrum-like cycles. |
