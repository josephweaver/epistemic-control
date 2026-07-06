Please read operational slice (OS):

docs\concepts\dependency-aware-workflows\010-propagate-step-and-workflow-failure.md
Analyze the operational slice and produce a concise implementation plan only.

Use "EC-3 / operational slice / files(4)+test+doc" with CSx(IR)x Cadence

Reference: 
..\epistemic-control\hci-levels.md
..\epistemic-control\hci-cadence\CSx(IR)x.md

Your task:

1. Identify the exact implementation objective.
2. Identify the likely files to modify, maximum 4 implementation files unless the OS explicitly requires more.
3. Identify required tests.
4. Identify required documentation updates.
5. Identify any ambiguity, missing prerequisite, or invariant that could make implementation unsafe.

Do not modify files yet.

---

If the slice is ready for implementation, end with:

READY FOR SPARK IMPLEMENTATION

---

If not ready, explain the blocker and create/append the issue to:

docs\concepts\execution-observability\issues.md

---

When finished please estimate the token consumption by this prompt and add a entry to 
..\epistemic-control\usage\<SC>\yyyyMMddhhmmss.md
using the 
..\epistemic-control\usage\prompt-usage-template.md
as a template. Note your Model is gpt5.4-mini iwith medium reasoning.  See if you can query codex apis for token estimates.

