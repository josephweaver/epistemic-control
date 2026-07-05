# HCI Cadence: C(SIR)x

## Summary

`C(SIR)x` extends the Epistemic Control cadence by making **Implementation Review** a first-class activity immediately following implementation.

The intent is to minimize knowledge decay by reviewing each completed implementation while the AI still has fresh context and before the developer begins the next Operational Slice.

This cadence is recommended whenever implementation is primarily AI-assisted.

---

## Cadence

```
C → ( S → I → R ) ×
```

where:

| Symbol | Meaning |
|---------|---------|
| **C** | Concept formation. Define the overall Strategic Concept and objectives. |
| **S** | Operational Slice design. Produce a small, self-contained implementation specification with explicit acceptance criteria. |
| **I** | Implementation. AI (or human) implements exactly one Operational Slice. Documentation and unit tests are considered part of implementation. |
| **R** | Implementation Review. Perform a structured epistemic review immediately after implementation to reconstruct understanding of what was built and why. |
| **×** | Repeat for every Operational Slice until the Strategic Concept is complete. |

---

## Workflow

```
Strategic Concept

        │
        ▼
+-------------------+
| Operational Slice |
+-------------------+
        │
        ▼
+-------------------+
| Implementation    |
+-------------------+
        │
        ▼
+-------------------+
| Implementation    |
| Review            |
+-------------------+
        │
        ▼
repeat
```

---

## Purpose

Traditional AI-assisted development often follows:

```
C(SI)x
```

where implementation proceeds directly into the next slice.

Unfortunately, developer understanding tends to decay rapidly because attention shifts immediately to the next task.

`C(SIR)x` intentionally inserts a review phase before moving on.

The review reconstructs the implementation from the finished code rather than from the AI conversation, helping the developer build durable mental models of the system.

---

## Objectives of the Review

The review should answer questions such as:

- What was actually implemented?
- Which requirements from the Operational Slice were satisfied?
- Which source files changed?
- Why were those files selected?
- What invariants were introduced?
- What assumptions were made?
- What important algorithms or data structures were added?
- What tests demonstrate correctness?
- What technical debt or follow-up work remains?

The goal is not code critique alone—it is developer comprehension.

---

## Recommended Procedure

After every completed Operational Slice, execute:

```
procedures/implementation-review.md
```

This procedure performs a structured reconstruction of the implementation and records any knowledge gaps before beginning the next slice.

---

## Benefits

Compared with `C(SI)x`, this cadence provides:

- Higher Epistemic Control
- Better long-term retention
- Easier onboarding after interruptions
- Faster future modifications
- Earlier detection of implementation drift
- Lower risk of accumulating misunderstood AI-generated code

---

## Typical Codex Prompt

```
Please read:

docs/concepts/<concept>/<slice>.md

Implement using:

EC-3
Operational Slice
Files(3) + Tests + Docs

When implementation is complete, immediately perform

C(SIR)x

using

procedures/implementation-review.md

Update:

- PROJECT_STATE.md
- Operational Slice document
- usage-report.md

If any blocking issues or ambiguities are discovered, append them to issues.md.
```

---

## When to Use

`C(SIR)x` is recommended for:

- AI-assisted implementation
- Research software
- Safety-critical software
- Large multi-session projects
- Projects emphasizing developer understanding over raw implementation speed

It may be unnecessary for exploratory prototypes or disposable code where long-term comprehension is not a primary objective.