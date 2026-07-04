# HCI Cadence: (C-S-I)x

## Purpose

This cadence describes what is commonly called vibe coding: repeated
implementation activity where a Strategic Concept or Operational Slice may be
added when useful, but neither is required before each implementation pass.

Use this label when the session is intentionally exploratory and the human
accepts that the work may discover its own direction as code is written.

## Notation

```text
(C-S-I)x
```

Meaning:

- Repeat one or more exploratory passes.
- In each pass, optionally define or revise a Strategic Concept.
- In each pass, optionally define or revise an Operational Slice.
- In each pass, perform one Implementation.
- Let the next edit be guided by immediate feedback, visible code shape, runtime
  behavior, or the human's next instruction.
- Do not require a Strategic Concept document before starting.
- Do not require an Operational Slice document before starting.

## Control Risk

This cadence has higher epistemic-control risk than concept-and-slice cadences.

Common risks:

- The target state is vague.
- The stopping point is unclear.
- The code may grow around local momentum instead of an agreed design.
- Review may become harder because the rationale for each edit is not recorded
  before implementation.

## Required Guardrails

Even in `(C-S-I)x`, use:

```text
hci-levels.md
```

for the active HCI specification.

Before editing, state the immediate current state and the next concrete change.

After each implementation pass, report:

- What changed.
- Why it changed.
- What test or command ran.
- Whether the result passed.
- What uncertainty remains.

## When To Stop

Stop and switch to a concept-and-slice cadence when:

- The work starts touching multiple responsibilities.
- A new concept needs its own file or package.
- The target state becomes important enough to preserve in documentation.
- The human asks for a plan, concept, slice, or review boundary.
- The implementation starts producing surprises that need architectural
  explanation.
