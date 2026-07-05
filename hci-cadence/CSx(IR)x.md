# HCI Cadence: CSx(IR)x

## Summary

`CSx(IR)x` is an Epistemic Control development cadence that separates **design** from **implementation** while coupling every implementation with an immediate **Implementation Review**.

The cadence recognizes that design knowledge is relatively stable, while implementation knowledge decays rapidly. By performing an epistemic review immediately after each implementation, developer understanding is consolidated before context is lost.

This cadence is intended for AI-assisted software development where maintaining human understanding is as important as producing working code.

---

# Cadence

```
CSx(IR)x
```

Equivalent workflow:

```
Concept
    ↓
Operational Slice Design (all slices)

Then for each slice:

Implementation
        ↓
Implementation Review
```

---

# Meaning

| Symbol | Meaning |
|---------|---------|
| **C** | Strategic Concept development. Define the overall objective, architecture, constraints, and success criteria. |
| **S** | Operational Slice design. Break the Strategic Concept into a complete set of small, independently implementable slices with clear acceptance criteria. |
| **I** | Implement a single Operational Slice. Documentation and unit tests are considered part of implementation. |
| **R** | Perform an immediate epistemic Implementation Review to reconstruct understanding of the completed implementation. |
| **x** | Repeat. |

---

# Workflow

```
                 Strategic Concept
                        │
                        ▼
        +-------------------------------+
        | Design Operational Slices     |
        | 001                           |
        | 002                           |
        | 003                           |
        | ...                           |
        | N                             |
        +-------------------------------+

                        │
                        ▼

        Slice 001
        ┌─────────────────────┐
        │ Implement           │
        └─────────┬───────────┘
                  ▼
        ┌─────────────────────┐
        │ Review              │
        └─────────┬───────────┘
                  ▼

        Slice 002
        ┌─────────────────────┐
        │ Implement           │
        └─────────┬───────────┘
                  ▼
        ┌─────────────────────┐
        │ Review              │
        └─────────┬───────────┘
                  ▼

               ...

                  ▼

        Slice N
        ┌─────────────────────┐
        │ Implement           │
        └─────────┬───────────┘
                  ▼
        ┌─────────────────────┐
        │ Review              │
        └─────────────────────┘
```

---

# Rationale

Traditional AI-assisted development often follows:

```
C(SI)x
```

or

```
C(SIR)x
```

where design and implementation are interleaved.

In contrast, `CSx(IR)x` deliberately front-loads the design effort. All Operational Slices are designed before implementation begins.

This provides several advantages:

- Architectural consistency across slices.
- Early discovery of ambiguities.
- Reduced implementation drift.
- Simpler implementation prompts.
- Lower token consumption during implementation.

Implementation then proceeds one Operational Slice at a time.

Immediately after each implementation, an epistemic review is performed before moving to the next slice.

This review consolidates developer understanding while implementation context is still fresh.

---

# Implementation Review

Every completed Operational Slice should immediately execute the procedure:

```
procedures/implementation-review.md
```

The review should reconstruct the implementation by answering questions such as:

- What requirements were implemented?
- Which files changed?
- Why were those files modified?
- What algorithms were introduced?
- What invariants were added?
- What assumptions were made?
- Which tests verify correctness?
- What follow-up work remains?

The objective is not simply to evaluate code quality, but to increase the developer's understanding of the implementation.

---

# Example Timeline

```
Week 1

Concept
Design Slice 001
Design Slice 002
Design Slice 003
Design Slice 004

Week 2

Implement 001
Review 001

Implement 002
Review 002

Implement 003
Review 003

Implement 004
Review 004
```

---

# Typical Codex Prompt

```
Please read:

docs/concepts/<concept>/<slice>.md

Implement using:

EC-3
Operational Slice
Files(3) + Tests + Docs

When implementation is complete:

Execute CSx(IR)x

using

procedures/implementation-review.md

Update:

- PROJECT_STATE.md
- Operational Slice document
- usage-report.md

If any blocking issues or ambiguities are discovered, append them to issues.md.
```

---

# Benefits

Compared to implementation-only workflows, `CSx(IR)x` provides:

- Higher Epistemic Control
- Better long-term retention
- Faster onboarding after interruptions
- Earlier detection of implementation drift
- Reduced accumulation of misunderstood AI-generated code
- Improved confidence when modifying existing implementations
- A structured, repeatable development process suitable for long-lived AI-assisted software projects