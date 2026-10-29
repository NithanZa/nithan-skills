---
name: planning
description: Create cohesive, repo-aware feature plans as phased markdown files under the project's plan directory.
---

## Purpose

When a user asks to plan a feature:
1. Locate the project's existing plan directory.
2. Inspect the repository to understand its architecture, patterns, and conventions.
3. Break the feature into actionable, testable phases.
4. Write one markdown file per phase in the plan directory.

---

## When to use

Use this skill when the user asks for:
- planning a feature
- breaking down implementation steps
- writing a phased roadmap
- creating plan/phase docs
- how to implement something in the repo

Do **not** use it for:
- very small tasks
- purely conceptual brainstorming without repo integration

---

## Inputs

Prefer to infer from the repository rather than asking the user.

Inspect the repo to understand:
- stack and frameworks
- project structure and conventions
- patterns for APIs/services/database/config/testing
- similar existing features

From the request, identify:
- feature name
- intended behavior or user flow
- constraints
- what "done" looks like

---

## Step 1: Find the plan directory

Check for an existing plan directory in this order:

1. `/docs/plan/`
2. `/docs/plans/`
3. `/plan/`
4. `/plans/`
5. Other planning conventions referenced in the repository, such as `PLAN.md`, `ROADMAP.md`, or `docs/planning/`.

Rules:
- **If one exists, use it.**
- **If multiple exist**, choose the one most actively used or relevant to the feature.
- **If none exist**, create `/docs/plans/initial-plan` or whatever folder name would suit best.
- Follow existing organization and naming conventions whenever possible.

---

## Step 2: Inspect the project

Before planning, examine enough of the repository to understand how the feature fits into the existing system.

At minimum:
- Read `README.md` and relevant project documentation.
- Understand the directory structure and architecture.
- Identify relevant components, routes, services, APIs, and database models.
- Inspect similar existing features and reusable utilities.
- Check relevant dependencies, tests, and configuration.

Rules:
- **Build on existing architecture** rather than introducing unnecessary alternatives.
- Prefer existing libraries, components, and patterns.
- Reference actual file paths and modules where useful.
- Consider how the feature affects other parts of the project.
- Do not make assumptions about code that can be inspected.

---

## Step 3: Create phased plan files

Break the feature into logical implementation phases.

### Phasing rules

- Each phase should have a clear outcome and verifiable completion criteria.
- Order phases by dependencies so they can be implemented sequentially.
- Keep each phase focused and reasonably self-contained.
- Avoid unnecessary phases or excessive fragmentation.
- Include testing, error handling, security, and integration where relevant.
- Ensure the final phase results in a complete, working feature.

### File naming

Each phase must be stored in a separate markdown file:

`phase{N}-[phasename].md`

Where:
- `{N}` is the phase number, starting at 1.
- `[phasename]` is a short, descriptive kebab-case name.

Examples:
- `phase1-data-model.md`
- `phase2-backend-api.md`
- `phase3-frontend-integration.md`
- `phase4-testing-polish.md`

Store all phase files in the detected plan directory.

---

## Required file template

Every phase file must follow this structure:

### `phase{N}-[phasename].md`

```md
# [Feature]

## Outcome

Describe the specific result this phase should achieve.

## Step-by-step

1. Describe the first implementation step, referencing relevant files/modules.
2. Describe the next step and how it integrates with existing functionality.
3. Continue with concrete, ordered implementation instructions.

## Acceptance criteria

- [ ] AC1: Specific, verifiable requirement.
- [ ] AC2: Specific, verifiable requirement.
- [ ] AC3: Specific, verifiable requirement.
```

### Template rules

- Use the same feature name in the `# [Feature]` heading across all phase files.
- **Outcome** describes what should be working after the phase.
- **Step-by-step** contains concrete, sequential implementation instructions.
- **Acceptance criteria** uses numbered AC identifiers (`AC1`, `AC2`, etc.) with markdown checkboxes.
- Acceptance criteria must be objectively testable, not vague.
- Include relevant file paths, functions, components, or APIs when known.
- Do not add unnecessary sections unless required by existing project conventions.

---

## Planning quality

Every plan should be:

- **Cohesive:** Fits naturally into the existing project architecture.
- **Concrete:** Gives implementation-ready instructions rather than generic advice.
- **Incremental:** Each phase builds logically on previous phases.
- **Minimal:** Avoids overengineering and unnecessary dependencies.
- **Complete:** Covers the feature end-to-end, including relevant edge cases.
- **Testable:** Defines clear acceptance criteria for every phase.

When relevant, account for:
- Authentication, authorization, and input validation.
- Database migrations and backward compatibility.
- Loading, empty, and error states.
- Unit and integration testing.
- Performance and accessibility.
- Deployment, configuration, and documentation.

Only include considerations relevant to the feature.

---

## Step 4: Verify the plan

Before finishing:
1. Confirm that all requested functionality is covered.
2. Check that phases follow the correct dependency order.
3. Ensure instructions align with actual repository patterns.
4. Remove duplicated steps or unnecessary complexity.
5. Confirm every phase has measurable acceptance criteria.
6. Verify all phase files are saved in the correct directory.

---

## Output

After creating the files, briefly report:
- The plan directory used.
- The phase files created.
- A one-sentence summary of each phase.

Do not repeat the full contents of the files unless requested.

If repository access is unavailable, provide a best-effort plan based on available context and clearly distinguish assumptions from verified project details.
