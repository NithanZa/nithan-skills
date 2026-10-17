---
name: follow-plan-all
description: Implements every remaining planning-skill phase file in order, then stops. Use when the user asks to finish the plan, do every remaining phase, run the rest of the plan, or implement all phases.
---

# Follow-plan-all

Read the phase files written by the planning skill. Implement each remaining phase in number order. Stop when the feature's unchecked phases are done, or when a phase cannot be finished.

`follow-plan` does one phase and stops. This skill continues.

## Hard rules

- Work remaining phases in number order. Finish one, check it off, then start the next.
- Do not skip an unchecked earlier phase to start a later one.
- Do not create a git commit.
- Do not add a status section to a phase file.
- Do not invent a second plan format. Consume `phase{N}-[phasename].md` files from the plan directory.
- If a written step disagrees with the existing code, stop the run and ask. Do not adapt and continue. Do not implement the step when it fights the repo. Do not start later steps or later phases.

## Find the plan directory

Search in this order:

1. `docs/plan/`
2. `docs/plans/`
3. `plan/`
4. `plans/`
5. Other planning conventions already referenced in the repository, such as `PLAN.md`, `ROADMAP.md`, or `docs/planning/`.

Use a directory that already holds `phase{N}-[phasename].md` files. If several do, pick the one most actively used for this feature. If none exist, stop. Do not create a plan directory.

## Choose the phases

List `phase{N}-[phasename].md` files in the plan directory.

If their feature headings differ, ask which feature. Do not pick one.

If the user names a phase, treat that as the feature to run. If an earlier phase of that feature still has unchecked acceptance criteria, start there and say so.

The run list is every phase file for that feature that still has unchecked acceptance criteria, from lowest number to highest.

If no phase files exist, stop and say so. If every phase file for that feature is already checked, stop and say the plan is complete.

## Read each phase file

A valid phase file has:

- A feature heading
- `## Outcome`
- `## Step-by-step`
- `## Acceptance criteria` with numbered identifiers such as `AC1` and markdown checkboxes, for example `- [ ] AC1: ...`

If any required section is missing or empty, or the acceptance criteria have no identifiers or checkboxes, stop the run on that file. Report which part is unusable. Do not rewrite the phase file. Do not invent acceptance criteria. Do not start later phases. Ignore extra sections.

## Implement one phase, then the next

For each phase on the run list, work its step-by-step list in order.

If the code already does what a step asks, leave it and go to the next step.

A step disagrees with the code when it points at the wrong module, contradicts an existing pattern, or would replace a working approach with a different one. Missing code for a feature the phase adds is not a disagreement.

If a step disagrees, stop the run before changing the approach. Do not adapt the step. Do not implement it as written. Do not start later steps. Do not start the next phase.

Tell the user:

- The phase file and the step number
- What the phase file says to do
- The file path and what the code does now
- The disagreement in one or two sentences

Ask which to do. Follow the step, follow the code, or revise the phase file.

Wait for an answer. Do not choose.

## Tests and acceptance criteria

A phase is done only when every acceptance criterion is met and the project's tests pass.

Find the test command once, from the repository. Check `package.json` scripts, `Makefile`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `README.md`, and CI config. Run that command after each phase.

If no test command is found, do not mark the current phase done. Stop the run. Ask which command to run.

If tests fail, fix failures this phase caused and re-run. If failures are outside this phase, or you cannot get them passing, stop the run. Leave this phase's acceptance criteria unchecked. Leave earlier phases that already passed as they are.

When the phase is done, check off its acceptance criteria, then start the next phase on the run list.

## Record progress

Check off acceptance criteria in a phase file only after that phase is done. Change each `- [ ]` to `- [x]` in one edit. That is the only progress record.

If you stop during a phase, leave that phase file unchanged. Do not check some of its boxes. Do not add notes or a status section.

## Report

Keep the final message short. Do not paste phase files.

For each phase this run finished, one line with the phase filename, that its acceptance criteria are checked, and that the test command passed.

Then say whether the feature's plan is complete or why the run stopped. If it stopped early, say what you need from the user, and say that the current phase file is unchanged.
