Please read operational slice (OS):

docs\concepts\data-assets-and-materialized-outputs\011-fake-hpcc-artifact-and-data-asset-smoke-path.md

Analyze the operational slice and produce a concise implementation plan only for gpt5.3-codex-spark.

Use "EC-3 / operational slice / files(10)+test+doc" with CSx(IR)x Cadence

Reference: 
..\epistemic-control\hci-levels.md
..\epistemic-control\hci-cadence\CSx(IR)x.md

Your task:

1. Identify the exact implementation objective.
2. Identify required tests.
3. Identify required documentation updates.
4. Identify any ambiguity, missing prerequisite, or invariant that could make implementation unsafe.

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
as a template. Note your Model is gpt5.4-mini with medium reasoning.  See if you can query codex apis for token estimates.

