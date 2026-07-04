# Human-AI Coding Interaction (HCI) Specification v2

## Overview

An HCI specification defines three independent dimensions:

```text
EC Level / Objective Scope / Change Budget
```

Example:

```text
EC-3 / feature / file(1)+test+doc
```

Meaning:

* Human defines the objective and supervises AI-proposed planning.
* AI is working toward a single feature.
* AI may modify one production code file.
* AI may also modify associated tests and documentation.
* AI must stop and report before continuing.

---

# 1. Epistemic Control (EC)

Epistemic Control defines who decides what the project works on next.

EC is primarily about planning authority: who identifies the next objective, subproblem, design direction, and implementation direction. It is not primarily about who types the code or runs the tests.

A human can delegate implementation to AI while retaining high epistemic control. A human can also understand generated code while having lower epistemic control if the AI selected the next subproblem.

## EC-5: Human Controlled

### Human Role

* Determines objectives.
* Determines subproblems.
* Determines design.
* Determines implementation details.
* Determines exact edits.

### AI Role

* Answers questions.
* Reviews code when requested.
* Generates tightly specified snippets when requested.

Human directly controls both planning and execution details. AI mainly supports understanding, review, or narrowly specified implementation fragments.

---

## EC-4: Human Directed

### Human Role

* Determines the next subproblem to solve.
* Retains planning authority.
* Decides when constraints require changing the plan.

### AI Role

* Provides status.
* Identifies constraints.
* Provides technical advice.
* Suggests alternatives.
* Supports implementation.

AI may implement, test, explain, or recommend, but the human decides what the project works on next.

Example interaction:

```text
Human: What are we working on next?
AI: We need to start workers on the HPCC.
Human: Ok, let's create an SSH communication layer.
AI: The Dockerized Slurm environment does not have an SSH layer to test against.
Human: Ok, then let's update our Dockerized Slurm environment and install an SSH server.
```

Key test:

```text
Could the human identify the next subproblem before the AI proposed it?
```

---

## EC-3: Human Supervised Planning

### Human Role

* Defines the objective.
* Approves, rejects, or revises the AI's proposed plan.
* Maintains review authority over implementation direction.

### AI Role

* Proposes subproblems.
* Proposes implementation direction.
* Implements approved work when permitted.
* Reports impacts, risks, and test results when requested.

Key distinction from EC-4: at EC-3 the AI helps choose the next subproblem.

---

## EC-2: Human Intended Autonomy

### Human Role

* Specifies outcome and constraints.
* Reviews milestones.

### AI Role

* Decomposes the work into intermediate objectives.
* Plans the implementation sequence.
* Executes the work.
* Maintains tests and documentation when permitted.

Human intends the result and bounds the work, while AI determines the intermediate plan and execution sequence.

---

## EC-1: Human Reviewed Autonomy

### Human Role

* Reviews completed results.
* Accepts or rejects results.

### AI Role

* Determines project direction.
* Determines implementation strategy.
* Plans, implements, and tests the work.

Human evaluates completed work rather than directing the project as it proceeds.

---

## EC-0: Fully Autonomous

### Human Role

* Provides only a mission or desired outcome.

### AI Role

* Determines objectives.
* Determines next actions.
* Determines design.
* Determines implementation.
* Determines tests.
* Determines validation.

Human acts only as stakeholder.

---

EC is independent of Objective Scope and Change Budget. For example, `EC-4 / feature / file(1)+test+doc` can allow AI implementation while the human retains planning authority, and `EC-2 / function / file(1)` can give AI authority to choose the intermediate plan within a narrow change budget.

---

# 2. Objective Scope

Objective Scope describes what the AI is attempting to accomplish.

It does NOT describe how much code may be modified.

---

## line

One source line.

---

## block

One contiguous code block.

Examples:

* if statement
* loop
* match branch

---

## function

One function or method.

Examples:

```python
def tokenize(...)
```

```go
func ProcessJob(...)
```

---

## class

One class, struct, or equivalent type.

Examples:

```python
class Tokenizer
```

```go
type Worker struct
```

---

## module

One cohesive software module.

Examples:

```text
tokenizer
parser
database
scheduler
```

A module may span multiple files.

---

## feature

One user-visible capability.

Examples:

```text
OAuth Login
Export to CSV
Password Reset
Raster Import
```

A feature may span multiple modules and files.

---

## application

One executable application or service.

Examples:

```text
frontend
controller
worker
```

---

## system

Multiple cooperating applications.

Examples:

```text
controller + worker
frontend + backend
ETL platform
```

---

## project

An entire software project.

Examples:

```text
QSmith
Kingdom of Illusions
Replication Core
```

---

## repository

Entire repository, including all projects.

---

# 3. Change Budget

Change Budget defines how much code may be modified before review or completion.

Budget limits are independent of Objective Scope.

For example:

```text
EC-3 / feature / file(1)+test+doc
```

means:

* Objective is a feature.
* Only one production file may be changed before stopping.

---

## file(N)

Maximum number of production code files that may be modified.

Examples:

```text
file(1)
file(3)
file(10)
```

Examples:

```text
file(1)
```

One production file.

```text
file(3)
```

Up to three production files.

---

## loc(N)

Approximate limit on changed lines of code.

Examples:

```text
loc(50)
loc(150)
loc(500)
```

Used to limit review burden.

---

## function(N)

Maximum number of functions modified.

Examples:

```text
function(1)
function(5)
```

---

## module(N)

Maximum number of modules modified.

Examples:

```text
module(1)
module(3)
```

---

# Budget Modifiers

Budget modifiers do not count against primary production-code budgets.

---

## +test

AI may modify tests associated with modified production code.

Examples:

```text
file(1)+test
file(3)+test
```

If one production file is modified, corresponding test files may also be updated.

Test files do not count toward file(N).

---

## +doc

AI may modify supporting documentation associated with modified production code.

Examples:

* README.md
* DESIGN.md
* ARCHITECTURE.md
* API documentation

Documentation files do not count toward file(N).

## +cleanup

AI may make bounded follow-up edits outside the primary production-code budget when those edits are required to preserve consistency after an approved change.

Cleanup edits are allowed only when they are a direct consequence of the approved objective.

Allowed cleanup includes:

* Updating call sites after a function signature change.
* Updating interface implementations after an interface change.
* Updating imports after code is moved or extracted.
* Updating mocks, stubs, or fixtures affected by the change.
* Updating dependency injection or wiring required by the change.
* Fixing compile errors caused by the approved change.
* Updating tests affected by the approved change.

Cleanup does not include:

* Opportunistic refactoring.
* Unrelated bug fixes.
* Style-only rewrites.
* Adding new features.
* Redesigning adjacent modules.
* Expanding the original objective.

Cleanup test:

```text
If the approved change were reverted, would this cleanup edit still be necessary?
```

If the answer is no, the edit may qualify as cleanup.

If the answer is yes, the edit is outside cleanup scope and requires review or a new HCI specification.

Cleanup files do not count against file(N), but AI must report all cleanup files modified and explain why each was necessary.

---

## +newfile

AI may create new files required to support the approved objective.

New files do not count against file(N) when they primarily contain newly introduced types, interfaces, structs, classes, adapters, tests, or documentation created as part of the approved design.

Allowed new files include:

* New class, struct, or interface files.
* New adapter or implementation files.
* New test files.
* New documentation files.
* New configuration templates directly required by the approved change.

For example:

```text
EC-3 / feature / file(1)+test+doc+cleanup+newfile
```

may allow AI to modify one existing production file while also creating files such as:

```text
target_environment.go
local_environment.go
target_environment_test.go
```

New files are exempt only when they support the approved objective. They may not be used to smuggle in unrelated functionality.

AI must report all new files created and explain their purpose.


---

# Examples

## Human-Directed Operational Slice

```text
EC-4 / feature / file(3)+test+doc
```

Meaning:

* Human identifies the next subproblem.
* AI provides constraints, options, implementation support, and test results.
* AI may modify up to three production files.
* AI may update associated tests and documentation.
* Human redirects the plan when new constraints appear.

Example:

```text
Human: Let's add the SSH communication layer next.
AI: The Dockerized Slurm environment does not have an SSH server to test against.
Human: Then update the Dockerized Slurm environment first so we can test SSH worker startup.
```

---

## One-File-Test-Report

```text
EC-3 / feature / file(1)+test+doc
```

Meaning:

* Work toward one feature.
* Modify one production file.
* Update tests and docs as needed.
* Review the AI-proposed plan.
* Report results.
* Stop for review.

---

## Three-File Operational Slice

```text
EC-3 / feature / file(3)+test+doc
```

Meaning:

* Work toward one feature.
* Modify up to three production files.
* Update tests and docs as needed.
* Review the AI-proposed plan.
* Stop for review.

---

## Autonomous Module Development

```text
EC-2 / module / file(10)+test+doc
```

Meaning:

* Build or modify one module.
* Up to ten production files may change.
* Human reviews milestones.

---

## Autonomous Project Refactor

```text
EC-1 / project / file(25)+test+doc
```

Meaning:

* AI may operate anywhere within the project.
* Up to twenty-five production files may change.
* Human reviews completed work.

---

## Repository-Wide Autonomous Operation

```text
EC-0 / repository / file(100)+test+doc
```

Meaning:

* AI operates across the repository.
* Large-scale changes permitted.
* Human acts primarily as stakeholder.

```
```
