Please read operational slice (OS):

docs\concepts\geospatial-worker-plugins\010-cdl-yanroy-fixture-workflow-and-docs.md

Then implement and test the approved plan from the prior analysis.

Use "EC-3 / operational slice / files(4)+test+doc+newfiles+cleanup" 

Reference: 
..\epistemic-control\hci-levels.md

Constraints:

* Prefer mechanical, behavior-preserving changes.
* Do not redesign beyond the operational slice.
* Add or update tests required by the slice.
* Keep changes small and reviewable.
* Preserve existing public behavior except where the OS requires a change.
* consider testing GDAL component in the WSL environment.

---

When complete, update:

/PROJECT_STATE.md

and mark the OS document above as implemented.

---

If you find a major issue, blocker, or unsafe ambiguity, stop and create/append it to:

docs\concepts\<SC>\issues.md
>
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

