Please read operational slice (OS):

docs\concepts\execution-observability\011-update-observability-docs-and-smoke.md

Then implement and test the approved plan from the prior analysis.

Use "EC-3 / operational slice / files(4)+test+doc" with CSx(IR)x Cadence

Reference: 
..\epistemic-control\hci-levels.md
..\epistemic-control\hci-cadence\CSx(IR)x.md

Constraints:

* Prefer mechanical, behavior-preserving changes.
* Do not redesign beyond the operational slice.
* Modify no more than 4 implementation files unless the OS explicitly requires more.
* Add or update tests required by the slice.
* Keep changes small and reviewable.
* Preserve existing public behavior except where the OS requires a change.

---

When complete, update:

/PROJECT_STATE.md

and mark the OS document above as implemented.

---

If you find a major issue, blocker, or unsafe ambiguity, stop and create/append it to:

docs\concepts\submission-cli-status\issues.md

---

When finished please estimate the token consumption by this prompt and add a entry to 
..\epistemic-control\usage\<SC>\yyyyMMddhhmmss.md
using the 
..\epistemic-control\usage\prompt-usage-template.md
as a template.  Note your Model is gpt5.3-codex-spark with medium reasoning. See if you can query codex apis for token estimates.

---

After you complete the work, please git commit with a good message.

---

Perform an implementation review based on 
..\epistemic-control\procedures\implementation-review.md
and record results to 
..\epistemic-control\implementation-review\<SC>\yyyyMMdd_hhmmss.md

