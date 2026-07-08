# EC Implementation Review Template

Use this prompt to review an implemented Strategic Concept / Operational Slice in a way that supports Epistemic Control.

The review should explain the implementation through **data objects, state transitions, preconditions, invariants, code paths, and tests** before discussing files in isolation.

---

## Review Process

Perform a high-fidelity implementation review of the current feature.

## Goal

Help me understand exactly what was implemented, what changed, and whether it matches the Strategic Concept and Operational Slice design.

The review should be organized around this principle:

```text
Data objects are nouns.
State transitions are verbs.
Preconditions are when the verb is allowed.
Invariants are the grammar that must remain true.
Tests are evidence that the sentence behaves correctly.
```

---

## 1. Read the Intended Design First

Before inspecting the code, read the relevant Strategic Concept and Operational Slice documents.

Identify:

- The Strategic Concept being implemented.
- The Operational Slice being implemented.
- The exact stated objective of the slice.
- The HCI / EC budget, if one is specified.
- Any explicit constraints, non-goals, or stop conditions.

Do not infer design intent unless it is supported by a cited document section, file, function, test, or diff hunk.

If design intent is unclear, say exactly what evidence is missing.

---

## 2. Build the EC Object / Transition Map

Before reviewing changed files, identify the core system sentence or sentences implemented by this slice.

Use this form:

```text
<DATA OBJECT> transitions from <STATE A> to <STATE B>
when <PRECONDITION>,
by <OPERATION>,
while preserving <INVARIANT>.
```

For each system sentence, list:

- Persistent data objects involved.
- In-memory data objects involved.
- Config objects involved.
- External artifacts involved.
- State before the transition.
- State after the transition.
- Preconditions required for the transition.
- Invariants that must remain true.
- Failure states or invalid transitions.
- What evidence in the docs or code supports this sentence.

If the slice does not define a clear object transition, say so and explain whether the implementation is instead structural, configurational, cleanup-oriented, or preparatory.

---

## 3. Inspect the Actual Git Diff

Inspect the actual git diff of this branch against `main`.

Summarize:

- Files changed.
- Files added.
- Files deleted.
- Production code files changed.
- Test files changed.
- Documentation files changed.
- Configuration files changed.
- Generated files, fixtures, migrations, or scripts changed.

Then compare the diff against the stated HCI / EC budget.

Important budget interpretation:

- A change budget is a **per-prompt review budget**, not a whole-feature budget and not a whole-chat-session budget.
- If the implementation spans more than one budgeted slice, identify which slice this review appears to cover.
- If the model exceeded the stated budget, identify the files that exceed it.
- If the model used `+newfile`, explain whether the new files make the work explicitly better organized as separate files.
- If the model used `+config`, explain which configuration files changed and how they are associated with the approved work.
- If the model used `+cleanup`, explain which cleanup edits were direct consequences of the approved change.

---

## 4. Review in Transition Order, Not File Order

Summarize the implementation in execution order / transition order, not file order.

For each transition or operation, explain:

- What object enters the operation.
- What state the object is in before the operation.
- What condition allows the operation to proceed.
- What code performs the operation.
- What state the object is in afterward.
- What invariant is preserved or created.
- What happens if the operation fails.
- What evidence supports each claim.

Avoid vague phrases like “handles the workflow” unless you identify the exact object, state, transition, and code path.

---

## 5. Review Each Changed Surface

For each new or changed public API, struct, function, table, migration, view, config field, CLI flag, test, fixture, or documented behavior, explain:

### Change

- What changed.
- Where it changed.
- Whether it is new, modified, removed, or renamed.

### Role in the Object / Transition Model

- Which data object it affects.
- Which transition it participates in.
- Which precondition it checks, creates, or assumes.
- Which invariant it preserves or risks violating.

### Purpose and Assumptions

- What it does.
- Why it appears to exist.
- What assumptions it encodes.
- What could break if the assumption is wrong.

### Design Match

Compare the implementation against the Strategic Concept and Operational Slice:

- Fully implemented.
- Partially implemented.
- Not implemented.
- Implemented differently than specified.

For anything partially implemented or implemented differently, identify:

- The exact difference.
- Whether the difference appears intentional.
- What evidence supports that conclusion.
- What evidence is missing.

---

## 6. Trace One Concrete Example Through the New Code Path

Trace one concrete example through the implementation.

Use an example that exercises the main object transition.

For the trace, show:

- Initial input or starting state.
- Persistent records involved.
- In-memory objects created or modified.
- Config values used.
- Functions called in order.
- State transitions that occur.
- Outputs, side effects, or artifacts produced.
- Final state.
- What would happen if a key precondition failed.

Use specific names from the implementation when available.

---

## 7. Test Coverage Review

List edge cases covered by tests.

For each covered edge case, identify:

- The test name.
- What object or transition it exercises.
- What invariant it proves.
- What failure it would catch.

List edge cases not covered by tests.

For each missing edge case, identify:

- The object or transition at risk.
- The precondition or invariant that is untested.
- The likely failure mode.
- Whether the missing test blocks confidence in moving on.

Also identify whether the tests are:

- Unit tests.
- Integration tests.
- Migration/schema tests.
- CLI tests.
- End-to-end tests.
- Smoke tests.
- Documentation-only examples.

---

## 8. Hidden Coupling, Ambiguity, and Maintenance Risk

Point out any:

- Ambiguous object ownership.
- Hidden state transitions.
- State represented in multiple places.
- Derived state persisted unnecessarily.
- Persisted state that should perhaps be derived.
- Naming confusion.
- Implicit coupling between files or modules.
- Config assumptions.
- Migration/versioning risks.
- Retry, crash, restart, or idempotency risks.
- Logging, redaction, or sensitive-value risks.
- Future maintenance risks.

For each risk, explain:

- Where the risk appears.
- Which object or transition it affects.
- What could break.
- What evidence supports the concern.
- Whether it needs action now or can be deferred.

---

## 9. Budget and Slice Fit

Evaluate whether the implementation fits the intended HCI / EC slice.

Answer:

- Did the work stay within the stated budget?
- Did it modify only the intended production files?
- Were tests, docs, cleanup, new files, or config changes allowed by modifiers?
- Did any changes appear unrelated to the approved objective?
- If the work should have been sliced into multiple prompts, what should the slices have been?

If the implementation is too large for one review, propose consecutive review slices using this form:

```text
Review Slice 1: <object / transition / files>
Review Slice 2: <object / transition / files>
Review Slice 3: <object / transition / files>
```

Each slice should be small enough for the human to review before saying `next`.

---

## 10. Final EC Summary

End with these sections:

### What I should understand before moving on

List the minimum object / transition / invariant facts I need to understand before continuing.

### Questions I should answer

List open questions that affect correctness, review confidence, or the next slice.

### Recommended next test or tiny experiment

Recommend one concrete test, command, or experiment that would most improve confidence.

### Five short quiz questions

Quiz me with 5 short questions that would reveal whether I actually understand this feature.

The questions should focus on:

- Data objects.
- State transitions.
- Preconditions.
- Invariants.
- Failure behavior.

---

## Important Constraints

- Do not praise the implementation.
- Do not rewrite code unless I explicitly ask.
- Do not assume the design intent; cite the file, function, doc section, test, or diff hunk that supports each claim.
- Prefer concrete observations over general advice.
- If something is unclear, say exactly what evidence is missing.
- Review execution behavior before file organization.
- Explain prose rationale only after identifying the objects, transitions, preconditions, and invariants.
- Treat data objects as the nouns and transitions as the verbs.
