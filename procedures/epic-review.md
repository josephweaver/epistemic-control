Review Process:

Perform a high-fidelity implementation review of the current feature.

Goal:
Help me understand exactly what was implemented, what changed, and whether it matches the epic design.

Please do the following:

1. Read the relevant epic/design docs first.
2. Inspect the actual git diff of this branch against main.
3. Summarize the implementation in execution order, not file order.
4. for each  new or changed public API, struct, function, table, config field, CLI flag, or test do the following
    - For each change, explain:
        - What it does
        - Why it appears to exist
        - What assumptions it encodes
        - What could break if the assumption is wrong
    - Compare the implementation against the epic:
        - Fully implemented
        - Partially implemented
        - Not implemented
        - Implemented differently than specified
    - Trace one concrete example through the new code path.
    - List edge cases covered by tests.
    - List edge cases not covered by tests.
    - Point out any ambiguity, hidden coupling, naming confusion, or future maintenance risk.
11. End with:
   - “What I should understand before moving on”
   - “Questions I should answer”
   - “Recommended next test or tiny experiment”

Also quiz me with 5 short questions that would reveal whether I actually understand this feature.

Important constraints:
- Do not praise the implementation.
- Do not rewrite code unless I explicitly ask.
- Do not assume the design intent; cite the file, function, or doc section that supports each claim.
- Prefer concrete observations over general advice.
- If something is unclear, say exactly what evidence is missing.
