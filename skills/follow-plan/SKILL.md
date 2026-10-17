---
name: follow-plan
description: Implements one planning-skill phase file in the current repository, then stops so a person can review. Use when the user asks to follow the plan, implement a phase, do the next phase, execute phase N, or work through a phase file under the plan directory.
---

# Follow-plan

Read one phase file written by the planning skill. Implement that phase only. Stop.

## Hard rules

- One phase per run. If the user names a phase, do that phase only.
- Do not start the next phase in the same run.
- Do not create a git commit.
- Do not add a status section to the phase file.
- Do not invent a second plan format. Consume `phase{N}-[phasename].md` files from the plan directory.
- If a written step disagrees with the existing code, stop and ask. Do not adapt and continue. Do not implement the step when it fights the repo. Do not continue with later steps.

## Find the plan directory

Search in this order:

1. `docs/plan/`
2. `docs/plans/`
3. `plan/`
4. `plans/`
5. Other planning conventions already referenced in the repository, such as `PLAN.md`, `ROADMAP.md`, or `docs/planning/`.

Use a directory that already holds `phase{N}-[phasename].md` files. If several do, pick the one most actively used for this feature. If none exist, stop. Do not create a plan directory.

## Choose the phase

If the user names a phase by number, filename, or title, open that phase file only.

If that name matches more than one phase file, list the matches and stop.

If the named phase file is missing, list the phase files that exist and stop.

If the named phase already has every acceptance criterion checked, say so and stop. Do not redo it unless the user asks to redo it.

If they do not name a phase:

1. List `phase{N}-[phasename].md` files in the plan directory.
2. If their feature headings differ, ask which feature. Do not pick one.
3. Take the lowest-numbered phase file for that feature that still has unchecked acceptance criteria.

If no phase files exist, stop and say so. If every phase file has every acceptance criterion checked, stop and say the plan is complete.

## Read the phase file

A valid phase file has:

- A feature heading
- `## Outcome`
- `## Step-by-step`
- `## Acceptance criteria` with numbered identifiers such as `AC1` and markdown checkboxes, for example `- [ ] AC1: ...`

If any required section is missing or empty, or the acceptance criteria have no identifiers or checkboxes, stop. Report which part is unusable. Do not rewrite the phase file to fit the template. Do not invent acceptance criteria. Ignore extra sections.

## Implement

Work the step-by-step list in order.

If the code already does what a step asks, leave it and go to the next step.

A step disagrees with the code when it points at the wrong module, contradicts an existing pattern, or would replace a working approach with a different one. Missing code for a feature the phase adds is not a disagreement.

If a step disagrees, stop before changing the approach. Do not adapt the step. Do not implement it as written. Do not start later steps.

Tell the user:

- The step number and what the phase file says to do
- The file path and what the code does now
- The disagreement in one or two sentences

Ask which to do. Follow the step, follow the code, or revise the phase file.

Wait for an answer. Do not choose.

## Tests and acceptance criteria

A phase is done only when every acceptance criterion is met and the project's tests pass.

Find the test command from the repository. Check `package.json` scripts, `Makefile`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `README.md`, and CI config. Run the command you find.

If no test command is found, do not mark the phase done. Report that no test command was found and ask which command to run.

If tests fail, fix failures this phase caused and re-run. If failures are outside this phase, or you cannot get them passing, stop. Leave acceptance criteria unchecked.

## Record progress

Check off acceptance criteria in the phase file only after the phase is done. Change each `- [ ]` to `- [x]` in one edit. That is the only progress record.

If you stop before the phase is done, leave the phase file unchanged. Do not check some boxes. Do not add notes or a status section.

## Report

Keep the final message short. Do not paste the phase file. Do not name or start the next phase.

Include:

- The phase file you used
- One sentence on what changed
- Whether acceptance criteria were checked
- The test command and whether it passed
- That this run stops here

If you stopped early, say why and what you need from the user. Say that the phase file is unchanged.
