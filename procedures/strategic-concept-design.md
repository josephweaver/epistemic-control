# Strategic Concept Design

Last updated: 2026-07-04

## Purpose

This document defines how to create a Strategic Concept.

A Strategic Concept describes a high-level system change. It names the current
state, target state, goals, non-goals, ownership boundaries, and completion
criteria before implementation begins.

Implementation is performed through Operational Slices created according to:

```text
procedures/operational-slice.md
```

## Precision And Language

When explaining current state and target state in chat, be as precise as the
available evidence allows. Avoid jargon, vague labels, and ambiguous words.

Prefer naming the actual capability, package, command, workflow, file, or
behavior being discussed. If a statement is an inference, say that it is an
inference. If evidence is missing, say what evidence is missing.

Documentation may be more detailed than chat, but it should still use precise
language. Do not use broad terms such as "integration", "runtime", "manager",
or "support" unless the document explains exactly what the term means in that
context.

## Directory Structure

Each Strategic Concept lives in its own directory.

```text
docs/
└── concepts/
    └── <concept-name>/
        ├── README.md
        ├── 001-<slice>.md
        ├── 002-<slice>.md
        └── ...
```

The README defines the Strategic Concept.

Each numbered document defines one Operational Slice.

## Lifecycle

Every Strategic Concept follows the same lifecycle.

```text
Idea
    ↓
Strategic Concept (Proposed)
    ↓
Collaborative Planning
    ↓
Strategic Concept (Ready)
    ↓
Operational Slice Creation
    ↓
Implementation
    ↓
Implementation Review
    ↓
Strategic Concept (Implemented)
```

The AI should help move a Strategic Concept through these stages but should
never advance it to **Ready** or **Implemented** without explicit agreement from
the human.

## Status

Every Strategic Concept has one of three states.

```text
Proposed
```

The system change is still being explored. Goals and implementation strategy may
change.

```text
Ready
```

The human and AI agree the Strategic Concept is sufficiently decomposed into
Operational Slices. Implementation may begin.

```text
Implemented
```

All agreed Operational Slices have been completed and accepted.

## Required Sections

### Purpose

Describe the system change being pursued.

The purpose should answer:

```text
What is the project gaining?
```

### Goals

Goals describe what the completed Strategic Concept should accomplish.

Goals should be architectural or product-level, not line-by-line implementation
instructions.

### Non-Goals

Explicitly list things that are not part of the Strategic Concept.

This section prevents scope creep during planning and implementation.

### Architectural Context

Briefly explain where this Strategic Concept belongs.

Reference relevant architecture documents. Avoid duplicating architectural
documentation.

### Current State

Describe the state of the project before work begins.

Include both levels:

- Strategic level: what capability, architecture, ownership boundary, or product
  posture exists today.
- Operational level: what concrete behavior, workflow, command, package,
  integration, or artifact exists today.

The current state should make clear why this Strategic Concept is needed.

### Target State

Describe the state of the project after the Strategic Concept is complete.

Include both levels:

- Strategic level: what capability, architecture, ownership boundary, or product
  posture will exist afterward.
- Operational level: what concrete behavior, workflow, command, package,
  integration, or artifact will exist afterward.

The target state should describe the intended result without collapsing the
Strategic Concept into implementation details.

### Proposed Slices

This section is a planning aid.

It represents the current understanding of the Operational Slices required.

The list is not authoritative. Slices may be added, removed, reordered, merged,
or split during discussion with the human.

### Completion Criteria

Describe what must be true before the Strategic Concept is considered complete.

Examples:

- All agreed Operational Slices are complete.
- Tests pass.
- Public interfaces remain consistent with architecture.
- Documentation describes the new current state.

## Planning Workflow

The AI should guide the human through the planning process.

Typical workflow:

1. Identify the system change.
2. Draft goals.
3. Draft non-goals.
4. Discuss architecture.
5. Brainstorm possible Operational Slices.
6. Refine or reorganize slices.
7. Determine whether additional slices are required.
8. Mark the Strategic Concept as **Ready**.

Only after the Strategic Concept is **Ready** should Operational Slices be
written.

## Relationship To Operational Slice Instructions

Operational Slices are created using:

```text
procedures/operational-slice.md
```

Each Operational Slice should represent one focused implementation task.

## Agent Responsibilities

When assisting with Strategic Concept planning, the AI should:

- Keep the discussion focused on architecture and desired project state.
- Encourage small, concrete Operational Slices.
- Suggest additional slices if important work appears to be missing.
- Compare completed slices with the proposed slice list.
- Notify the human when the agreed scope appears complete.
- Avoid discussing implementation details prematurely.

## Guiding Principle

The Strategic Concept answers:

```text
What system change are we pursuing?
```

Each Operational Slice answers:

```text
What is the next concrete implementation step?
```

The Strategic Concept is complete when both the human and AI agree that the
system change has been decomposed into a coherent set of Operational Slices and
those slices have been completed.
