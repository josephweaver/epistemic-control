# Implementation

Last updated: 2026-07-04

## Purpose

This document defines how to implement approved Operational Slices.

Implementation begins only after the Strategic Concept and its Operational
Slices have been designed and accepted. Strategic Concept writing is governed by
`strategic-concept-design.md`. Operational Slice design is governed by
`operational-slice.md`.

## Precision And Language

When explaining current state and target state in chat, be as precise as the
available evidence allows. Avoid jargon, vague labels, and ambiguous words.

Prefer naming the actual branch, Operational Slice, file, type, function, command,
test, or behavior involved. If a statement is an inference, say that it is an
inference. If evidence is missing, say what evidence is missing.

Implementation reports should be concise, but they must not hide uncertainty
behind broad terms such as "integration", "runtime", "manager", or "support".
Use those terms only when the report says exactly what changed.

## HCI Selection

Before implementation begins, the human must select an HCI specification from:

```text
hci-levels.md
```

The selected specification has three parts:

```text
EC Level / Objective Scope / Change Budget
```

Example:

```text
EC-3 / feature / file(1)+test+doc+cleanup
```

If no HCI specification is selected, the AI must ask for one before changing
production or test code.

## EC Continuity

Once the human selects an EC level for a chain of slice implementations, keep
using that same EC level for each slice in the chain.

For example, if implementation begins under:

```text
EC-3 / feature / file(1)+test+doc
```

then later Operational Slices in the same implementation chain also use `EC-3`
unless the human explicitly selects a different EC level.

The objective scope, change budget, and modifiers may be restated or narrowed
for a specific slice if the human chooses, but the EC level should not drift
implicitly.

## Strategic Concept Implementation Start

At the start of implementing a Strategic Concept, create a branch with a clear
name derived from the Strategic Concept.

Use a branch name that communicates the Strategic Concept scope, such as:

```text
concept/<short-concept-name>
```

Before changing implementation code, explain:

- The current state of the Strategic Concept at a high level.
- The target state of the Strategic Concept at a high level.
- The first Operational Slice to implement.
- What the current state is for that slice.
- What the slice will change.
- The active HCI specification.

Then wait for the human to say:

```text
next
```

Do not begin implementation until the human gives that command.

## Implementation Inputs

Before implementing an Operational Slice, read:

- The Strategic Concept README.
- The approved Operational Slice file.
- The files listed in the slice's `Required Context`.
- Any additional files only when needed to understand compile errors, test
  failures, or direct call-site cleanup.

Do not broaden context just because the repository is available.

## Slice Implementation Loop

Implement approved Operational Slices one by one.

For each Operational Slice:

1. Confirm the active HCI specification.
2. Read the approved slice.
3. Identify whether the slice updates an existing concept or adds a new concept.
4. Respect the allowed production files, test files, and out-of-scope list.
5. Implement only the current Operational Slice.
6. Run the narrowest useful verification.
7. Report changed files, reason, test command, result, and remaining work.
8. Stop for review when the slice is complete or the prompt budget is exhausted.

Do not begin the next Operational Slice until the current Operational Slice is
complete and accepted.

The normal command progression is:

```text
introduce slice -> wait for "next"
"next" -> implement within the active budget -> report
"next" -> continue same slice if incomplete
"commit" -> commit and push completed accepted Operational Slice
introduce next slice -> wait for "next"
```

If the Operational Slice is incomplete after a prompt-sized implementation, clearly
say that it is not done. Report:

- What current state now exists after the partial implementation.
- What target state remains for the next prompt-sized portion.
- Which file, concept, or behavior should be handled next.

When the Operational Slice is complete, do not immediately commit. Tell the human
the slice is complete and wait for:

```text
commit
```

When the human says `commit`, commit the current accepted slice changes with a
clear message and push the concept branch to the remote branch.

After the commit and push, introduce the next Operational Slice by explaining:

- The current state after the committed slice.
- What the next slice will change.
- The intended implementation approach at a high level.

Then wait for the human to say `next`.

## Multi-Prompt Slice Implementation

An Operational Slice may require more than one prompt when the active change
budget is smaller than the full implementation.

When this happens:

- Keep the same Operational Slice active.
- Keep the same EC level.
- Change only the next prompt-sized portion.
- Run the narrowest useful verification after each prompt-sized portion.
- Report what remains.
- Continue only when the human asks to continue, such as by saying `next`.

Do not represent a partially implemented Operational Slice as complete.

## File Organization During Implementation

Follow the concept decision in the Operational Slice file.

If the slice updates an existing concept, prefer the file or package that
already owns that concept.

If the slice adds a new concept, create a new file when the new concept has its
own responsibility, struct, interface, method set, or independent test surface.

Avoid cramming implementation into one file to fit a prompt. The active budget
limits how much may change in one prompt; it does not require unrelated concepts
to share a file.

## Cleanup

Cleanup edits are allowed only when the active HCI specification includes
`+cleanup`.

Cleanup must be a direct consequence of the approved slice implementation.
Use the cleanup test from `hci-levels.md`:

```text
If the approved change were reverted, would this cleanup edit still be necessary?
```

If the answer is no, the cleanup may qualify.

If the answer is yes, the edit is outside cleanup scope and requires review or a
new HCI specification.

## New Files

New files are allowed only when the active HCI specification includes
`+newfile`, or when the approved slice explicitly identifies a documentation or
planning artifact to create.

New files must support the approved Operational Slice. They may not be used to
add unrelated functionality.

## Commit Boundary

Do not commit immediately after making implementation changes.

Leave the current prompt's implementation work uncommitted for human review. A
completed Operational Slice is committed only when the human says:

```text
commit
```

Commit only the accepted slice changes with a clear commit message.

Do not include unrelated worktree changes in the commit.

After committing an Operational Slice, push the concept branch to the remote
branch.

## Required Implementation Report

After each implementation prompt, report:

```text
MODE
<active HCI specification>

CHANGED
- production files
- cleanup files
- test files
- documentation files
- new files

WHY
Reason for the change.

TEST RUN
Command executed.

RESULT
pass/fail/not run

NEXT
Recommended next implementation step or next Operational Slice.
```

If cleanup files or new files were modified, explain why each qualified under
the active HCI specification.

## Completion

An Operational Slice is complete only when:

- The approved target state exists.
- Acceptance criteria are satisfied.
- The narrowest useful verification has passed, or any remaining test gap is
  reported.
- Required documentation has been updated.
- The human has reviewed and accepted the result.

The implementation chain is complete only when all approved Operational Slices
are complete.

When all Operational Slices are exhausted, clearly say that there are no more
slices in the approved Strategic Concept implementation chain.

Then offer to:

- Commit any final accepted slice if it has not already been committed.
- Push the concept branch.
- Create a pull request.
- Merge the concept branch into `main` after review/approval.

After the Strategic Concept is merged or otherwise closed, perform an epistemic
review using:

```text
implementation-review.md
```
