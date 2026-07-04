# Implementation

Last updated: 2026-07-04

## Purpose

This document defines how to implement approved epic feature slices.

Implementation begins only after the epic and its feature slices have been
designed and accepted. Epic writing is governed by `epic.md`. Feature
slice design is governed by `epic-slice.md`.

## Precision And Language

When explaining current state and target state in chat, be as precise as the
available evidence allows. Avoid jargon, vague labels, and ambiguous words.

Prefer naming the actual branch, feature slice, file, type, function, command,
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

Once the human selects an EC level for a chain of feature implementations, keep
using that same EC level for each feature in the chain.

For example, if implementation begins under:

```text
EC-3 / feature / file(1)+test+doc
```

then later feature slices in the same implementation chain also use `EC-3`
unless the human explicitly selects a different EC level.

The objective scope, change budget, and modifiers may be restated or narrowed
for a specific feature if the human chooses, but the EC level should not drift
implicitly.

## Epic Implementation Start

At the start of implementing an epic, create a branch with a clear name derived
from the epic.

Use a branch name that communicates the epic scope, such as:

```text
epic/<short-epic-name>
```

Before changing implementation code, explain:

- The current state of the epic at a high level.
- The target state of the epic at a high level.
- The first feature slice to implement.
- What the current state is for that first feature.
- What the first feature will change.
- The active HCI specification.

Then wait for the human to say:

```text
next
```

Do not begin implementation until the human gives that command.

## Implementation Inputs

Before implementing a feature slice, read:

- The epic README.
- The approved feature-slice file.
- The files listed in the slice's `Required Context`.
- Any additional files only when needed to understand compile errors, test
  failures, or direct call-site cleanup.

Do not broaden context just because the repository is available.

## Feature Implementation Loop

Implement approved feature slices one by one.

For each feature slice:

1. Confirm the active HCI specification.
2. Read the approved slice.
3. Identify whether the slice updates an existing concept or adds a new concept.
4. Respect the allowed production files, test files, and out-of-scope list.
5. Implement only the current feature slice.
6. Run the narrowest useful verification.
7. Report changed files, reason, test command, result, and remaining work.
8. Stop for review when the slice is complete or the prompt budget is exhausted.

Do not begin the next feature slice until the current feature slice is complete
and accepted.

The normal command progression is:

```text
introduce feature -> wait for "next"
"next" -> implement within the active budget -> report
"next" -> continue same feature if incomplete
"commit" -> commit and push completed accepted feature slice
introduce next feature -> wait for "next"
```

If the feature slice is incomplete after a prompt-sized implementation, clearly
say that it is not done. Report:

- What current state now exists after the partial implementation.
- What target state remains for the next prompt-sized portion.
- Which file, concept, or behavior should be handled next.

When the feature slice is complete, do not immediately commit. Tell the human
the feature is complete and wait for:

```text
commit
```

When the human says `commit`, commit the current accepted feature-slice changes
with a clear message and push the epic branch to the remote feature branch.

After the commit and push, introduce the next feature slice by explaining:

- The current state after the committed feature.
- What the next feature will change.
- The intended implementation approach at a high level.

Then wait for the human to say `next`.

## Multi-Prompt Feature Implementation

A feature slice may require more than one prompt when the active change budget
is smaller than the full implementation.

When this happens:

- Keep the same feature slice active.
- Keep the same EC level.
- Change only the next prompt-sized portion.
- Run the narrowest useful verification after each prompt-sized portion.
- Report what remains.
- Continue only when the human asks to continue, such as by saying `next`.

Do not represent a partially implemented feature slice as complete.

## File Organization During Implementation

Follow the concept decision in the feature-slice file.

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

Cleanup must be a direct consequence of the approved feature implementation.
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

New files must support the approved feature slice. They may not be used to add
unrelated functionality.

## Commit Boundary

Do not commit immediately after making implementation changes.

Leave the current prompt's implementation work uncommitted for human review. A
completed feature slice is committed only when the human says:

```text
commit
```

Commit only the accepted slice changes with a clear commit message.

Do not include unrelated worktree changes in the commit.

After committing a feature slice, push the epic branch to the remote feature
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
Recommended next implementation step or next feature slice.
```

If cleanup files or new files were modified, explain why each qualified under
the active HCI specification.

## Completion

A feature slice is complete only when:

- The approved target state exists.
- Acceptance criteria are satisfied.
- The narrowest useful verification has passed, or any remaining test gap is
  reported.
- Required documentation has been updated.
- The human has reviewed and accepted the result.

The implementation chain is complete only when all approved feature slices are
complete.

When all feature slices are exhausted, clearly say that there are no more
features in the approved epic implementation chain.

Then offer to:

- Commit any final accepted slice if it has not already been committed.
- Push the epic branch.
- Create a pull request.
- Merge the epic branch into `main` after review/approval.

After the epic is merged or otherwise closed, perform an epistemic review using:

```text
epic-review.md
```
