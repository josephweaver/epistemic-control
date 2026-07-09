Please read operational slice (OS):

docs\concepts\sensitive-variable-propagation\009-concept-closure-and-doc-sync.md

Use "EC-3 / operational slice / files(6)+test+doc" 

Reference: 

..\epistemic-control\hci-levels.md

Your task:

* Implement the OS exactly as specified in the file above.
* Before editing code, read the OS and identify its explicit acceptance criteria. Treat the OS as the implementation contract.
* Keep the implementation narrowly scoped to this OS. Do not implement later slices, adjacent features, or speculative architecture unless this OS explicitly requires them.
* Inspect the current repository state before making changes. Prefer the existing project patterns, naming conventions, validation style, database/migration style, and test structure.
* Implement the required model, schema, parsing, validation, persistence, controller, CLI, or documentation changes only to the extent required by this OS.
* Add or update tests that prove the OS acceptance criteria are satisfied. Include both valid and invalid cases when the OS defines validation behavior.
* Keep changes easy to review. Respect the requested HCI scope and avoid broad refactors.
* If the implementation appears to require more files, larger architectural changes, or behavior not described by the OS, stop and record the issue instead of expanding scope.
* Run the relevant tests for the changed area. Prefer the project’s standard test command when available. If targeted tests are used, record exactly what was run.
* Do not mark the OS as implemented unless the implementation and tests are complete.
* consider using the WSL for GDAL testing.

---

If you find a major issue, blocker, or unsafe ambiguity, stop and create or append it to:

`docs\concepts\<SC_NAME>\issues.md`

Include:

* the OS path;
* the specific blocker or ambiguity;
* why implementation cannot safely continue;
* the smallest decision or follow-up needed to unblock the slice.

---

When complete:

1. Update:

`/PROJECT_STATE.md`

and mark the OS document above as implemented.

2. update the original OS markdown. Update the status to 'implemented'. Create a git commit for the go-etl project only with a concise, descriptive message and push to remote.

3. Estimate the token consumption by this prompt and add an entry to:

`..\epistemic-control\usage\<SC_NAME>\yyyyMMddhhmmss.md`

using:

`..\epistemic-control\usage\prompt-usage-template.md`

as a template.

Record the model as:

`gpt5.4-mini with medium reasoning`

If Codex can query token usage or token-estimate APIs, use them. Otherwise provide a best-effort estimate and clearly mark it as estimated.

4. Perform an implementation review based on:

`..\epistemic-control\procedures\implementation-review.md`

and record the results to:

`..\epistemic-control\implementation-review\<SC_NAME>\yyyyMMdd_hhmmss.md`
