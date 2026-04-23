# Blueprint Playbook

A practical operator's guide for Blueprint users. This document focuses on answering three questions:

1. What Blueprint is and what kinds of problems it is designed to solve
2. How to bring Blueprint into a specific Cursor project and use it there
3. Given different project states, which command you should start with

---

## 0. Project Overview

Blueprint is a Context-First Agentic Engineering OS designed to run inside the Cursor Agent workflow. Its core idea is not to have the Agent start coding immediately, but to first use a set of structured documents and commands to clarify requirements, design, technical plans, and testing boundaries before moving into implementation.

The key philosophy of Blueprint is:

**Define → Verify → Implement → Iterate**

instead of:

**Generate → Patch → Patch → Rewrite**

In Blueprint, the `.blueprint/` directory serves as the Agent's unified context package and the single source of truth for all downstream execution. Common core artifacts include:

- `PRD_V{N}.md`: Product requirements
- `mockup/index.html`: A runnable mockup
- `UI_Spec.md`: UI specifications distilled from the confirmed mockup
- `Tech_Spec.md`: Technical specification
- `Test_Spec.md`: Test specification

This workflow is especially suitable for the following kinds of work:

- Net-new projects or MVPs starting from zero
- Projects that already have a PRD but need to move quickly into design and technical planning
- Existing codebases where new requirements and iterations should be brought into a unified, standards-driven workflow

Blueprint is still actively evolving. Its command design, template structure, workflow details, and best practices will continue to improve through real project usage. Team members are encouraged to share feedback, contribute examples, and refine prompts and document templates so the system becomes more stable and effective over time.

---

## 1. Getting the Project

Blueprint repository:

- [Blueprint GitHub Repository](https://github.com/Jacobgxd/blueprint/tree/main)

The recommended way to get the full repository is with `git clone`:

```bash
git clone https://github.com/Jacobgxd/blueprint.git
```

You can also download the ZIP and extract it manually, but Git is recommended so you can easily sync future Blueprint updates.

After downloading the repo, pay special attention to the following directories and files:

- `.cursor/commands/`: Definitions for all Agent commands
- `.cursor/skills/`: Supporting skills, especially design-related capabilities
- `.blueprint/`: The specification document area and the Agent's primary context source
- `plans/`: Development plans
- `issues/`: Problem and requirement records
- `reports/`: Output reports for review, verify, test, and similar steps
- `START_HERE.md`: Quick onboarding for new users
- `QUICK_REFERENCE.md`: Command and path cheat sheet

One important clarification: Blueprint is not a standalone application. It is a reusable Agent workflow template meant to be embedded into an actual business project.

---

## 2. Using the Project

### 2.1 Prerequisites

Before using Blueprint, it helps to align on the following assumptions:

- All conversations are assumed to happen in **Cursor Agent mode**
- Blueprint should be placed in the **root directory of your actual project**
- That project can be either a brand-new project or an existing one
- Before starting any new task, read `.blueprint/CONTEXT.md` first
- The goal of Blueprint is not to replace human judgment, but to keep the Agent working under a single shared context so rework, omissions, and implementation drift are reduced

If this is your first time adopting Blueprint, it is recommended that you at least read these three files first:

- `START_HERE.md`
- `QUICK_REFERENCE.md`
- `.cursor/commands/README.md`

### 2.2 Integration Approaches

The recommended way to use Blueprint is not to study it in isolation in a separate repository, but to integrate it into the actual project you want to build.

There are two typical integration approaches:

#### Approach A: For a brand-new project

Best for:

- Starting a new product or MVP from scratch
- Situations where requirements, design, and implementation boundaries have not yet been systematically organized
- Teams that want to establish a unified specification base before pushing design and engineering forward

Common approach:

1. Put the required Blueprint directories and command files into the root of the new project
2. Start maintaining project state from `.blueprint/CONTEXT.md`
3. Based on the current state, begin with either `/create-prd` or `/create-mockup`

#### Approach B: For an existing project

Best for:

- Existing code repositories that need to absorb new requirements or iterations
- Projects that already have partial documentation, PRDs, designs, or technical implementation
- Teams that want future work to follow a unified spec-driven workflow

Common approach:

1. Bring Blueprint's directory structure and command files into the root of the existing project
2. Fill in missing key documents under `.blueprint/` based on the materials you already have
3. Continue from the command that best matches the current project state instead of forcing a restart from step one

If the existing project already has its own `.cursor/` configuration, review the differences first and merge selectively instead of overwriting your team's current setup directly.

### 2.3 Usage Scenarios

Below are four of the most common starting scenarios. The core principle is: **do not always start from the first step; start from the most complete point in your current materials.**

#### Scenario 1: A project starting from zero

Preconditions:

- No formal PRD exists yet
- No confirmed design exists yet
- No technical or test specification exists yet

Recommended starting point:

- `/create-prd`

Best for:

- You only have a product idea, or the requirement is still rough
- You need to first clarify users, goals, scope, flows, and constraints
- You want all downstream design and engineering work to be grounded in a unified PRD

Recommended path:

```text
/create-prd
→ /create-mockup
→ /review-mockup
→ /create-ui-spec
→ /create-tech-spec
→ /create-test-spec
→ /verify
→ /create-plan
→ /execute
```

#### Scenario 2: You already have a PRD and can start directly from Mockup

Preconditions:

- A relatively clear PRD already exists
- There is not yet a confirmed page structure or design direction

Recommended starting point:

- `/create-mockup`

Best for:

- Product requirements are already clear
- You want to validate layout, information hierarchy, and interaction direction first
- You want to see a runnable page before distilling a UI specification

Recommended path:

```text
/create-mockup
→ /review-mockup
→ /create-ui-spec
→ /create-tech-spec
→ /create-test-spec
→ /verify
```

#### Scenario 3: You already have PRD, Mockup, and UI Spec, and can start from Tech Spec

Preconditions:

- Product requirements are basically stable
- A confirmed mockup already exists
- The UI specification has already been created

Recommended starting point:

- `/create-tech-spec`

Best for:

- The design direction has already been confirmed
- You now need to translate requirements and design into an engineering-ready plan
- You need to define technical choices, module boundaries, API design, directory structure, and implementation boundaries

Recommended path:

```text
/create-tech-spec
→ /create-test-spec
→ /verify
→ /create-plan
→ /execute
```

#### Scenario 4: You already have a complete codebase and want to create a new requirement or log an issue

Preconditions:

- A runnable project and existing codebase already exist
- The current work is an incremental iteration, not a zero-to-one startup

Recommended starting point:

- `/issue`

Best for:

- You want to record a bug, requirement, optimization, or refactor opportunity
- You want to describe the problem clearly first before deciding whether to enter the full Blueprint workflow
- You want to capture the new item under `issues/` for future planning or expansion

There are two recommended paths:

**Lightweight path**

```text
/issue
→ Evaluate impact scope
→ Use /create-plan if needed
→ /execute
```

**Standard iteration path**

```text
/issue
→ /create-prd (update in iteration mode)
→ If page changes are involved, continue with /create-mockup → /create-ui-spec
→ /create-tech-spec
→ /create-test-spec
→ /verify
→ /create-plan
→ /execute
```

### 2.4 Command Guide, Usage Notes, and Recommended Models

Model recommendations should not be interpreted mechanically as "this command can only use one model." They should be chosen based on task type:

- Requirement analysis, document generation, and cross-document alignment: prefer models with strong long-context handling and structured writing ability
- Code implementation, refactoring, and precise edits: prefer models with strong engineering execution ability
- Mockup generation, design review, and UI rule distillation: prefer models that are more sensitive to design expression and overall consistency

Recommendations for each command are listed below.

#### `/create-prd`

Purpose:

- Organize an idea into a structured PRD that becomes the source document for the downstream workflow

Inputs:

- Product goals
- User roles
- Core flows
- Boundary conditions
- Existing business context

Output:

- `.blueprint/PRD_V{N}.md`

Recommended model:

- Prefer a model that is strong at long-form organization, requirement abstraction, and structured writing
- If the material set is large or the requirements are complex, prefer a model with stronger long-context capability
- Recommended model: GPT 5.4

#### `/create-mockup`

Purpose:

- Generate a runnable static mockup based on the current PRD

Inputs:

- Current active PRD
- Brand direction
- Reference products
- Style preferences

Output:

- `.blueprint/mockup/index.html`

Recommended model:

- Prefer a model that is strong at frontend generation, page structure organization, and visual expression
- If the task involves substantial design judgment, consider pairing it with a more design-sensitive model
- Recommended model: Sonnet 4.6

#### `/review-mockup`

Purpose:

- Check whether the mockup covers the requirements and whether its hierarchy, visuals, and interaction expression are consistent

Inputs:

- Mockup
- Optionally combined with PRD and UI Spec

Output:

- `reports/mockup-reviews/`

Recommended model:

- Prefer a model with stronger critical review, comparative checking, and issue-finding ability
- Recommended model: GPT 5.4

#### `/create-ui-spec`

Purpose:

- Distill structured UI specifications from the confirmed mockup
- Generate `design-system.html` at the same time

Inputs:

- Current active PRD
- Confirmed mockup

Outputs:

- `.blueprint/UI_Spec.md`
- `.blueprint/mockup/design-system.html`

Recommended model:

- Prefer a model with strong long-form structuring and design-rule abstraction ability
- Recommended model: Sonnet 4.6

#### `/create-tech-spec`

Purpose:

- Convert PRD, Mockup, and UI Spec into an engineering-ready technical specification

Inputs:

- PRD
- UI Spec
- Mockup

Output:

- `.blueprint/Tech_Spec.md`

Recommended model:

- Prefer a model with strong engineering reasoning, architecture breakdown, and module planning ability
- Recommended model: Opus

#### `/create-test-spec`

Purpose:

- Define the testing strategy, acceptance criteria, and test boundaries before development begins

Inputs:

- PRD
- UI Spec
- Tech Spec

Output:

- `.blueprint/Test_Spec.md`

Recommended model:

- Prefer a model that is logically rigorous, coverage-aware, and strong at test design
- Recommended model: Opus

#### `/verify`

Purpose:

- Check whether PRD, Mockup, UI Spec, Tech Spec, and Test Spec are consistent with one another

Inputs:

- All Blueprint documents listed above

Output:

- `reports/verify/`

Recommended model:

- Prefer a model with strong long-context comparison and contradiction detection ability
- Recommended model: GPT 5.4

#### `/create-plan`

Purpose:

- Generate a development plan and implementation order based on the full set of specification documents

Inputs:

- Blueprint documents that have passed verify

Output:

- `plans/[feature].md`

Recommended model:

- Prefer a model that is strong at task decomposition, dependency ordering, and execution planning
- Recommended model: Opus

#### `/execute`

Purpose:

- Perform real implementation based on the Plan and Mission Briefing

Inputs:

- Plan
- Tech Spec
- UI Spec
- Mockup
- Test Spec

Output:

- Code implementation

Recommended model:

- Prefer a model with strong engineering execution and precise code-editing ability
- Recommended model: Sonnet

Special note:

- Mission Briefing must be completed before `/execute`
- If specification conflicts are discovered during implementation, pause and resolve them at the document layer instead of guessing

#### `/review`

Purpose:

- Review the implementation result from both code quality and spec-drift perspectives

Inputs:

- Current code
- PRD
- UI Spec
- Tech Spec

Output:

- Review conclusions and fix recommendations

Recommended model:

- Prefer a model with strong review ability and a good eye for omissions and risks

#### `/test`

Purpose:

- Execute tests according to the Test Spec and output verifiable results

Inputs:

- Test Spec
- Current implementation

Output:

- `reports/test-runs/`

Recommended model:

- Prefer a model that is stable in execution and well-suited for step-by-step verification and evidence capture

#### Tooling commands (Composer is recommended across the board for speed and lower cost)

`/explore`

- Used to understand the current code structure and impact scope before implementation
- Useful for quickly building context before coding begins

`/document`

- Used to update explanatory materials after code or document changes

`/peer-review`

- Used for cross-model review to reduce bias from any single model

`/issue`

- Used to quickly record bugs, requirements, refactor opportunities, or issue signals

`/learn`

- Used to switch the current conversation into explanation/teaching mode

### 2.5 Recommended Working Style

The following is one of the most reliable working styles in practice:

1. Read `.blueprint/CONTEXT.md` first and confirm where the project currently is in the workflow
2. Choose the starting command that best matches the current state of your materials
3. After each step, update the context and relevant documents promptly
4. For design work, confirm the mockup first, then distill the UI Spec
5. For development work, do not skip `Test_Spec` or `/verify`
6. Before `/execute`, make sure Plan, Tech Spec, UI Spec, Mockup, and Test Spec are aligned

---

## 3. Best Practices and Notes

### 3.1 Do not assume you should always start from step one

The correct way to use Blueprint is not to mechanically run the full pipeline every time, but to choose the most suitable entry point based on the current project state. The more complete your materials already are, the later in the flow you should start.

### 3.2 Confirm the Mockup first, then distill the UI Spec

Blueprint currently emphasizes a Mockup-first workflow. Do not rush into writing `UI_Spec.md` before the visual result has been confirmed, or you risk turning guesses into standards.

### 3.3 `Test_Spec` must be created before development

`/create-test-spec` is not a document you add after development. It defines acceptance boundaries before coding begins, so the testing standard becomes an implementation constraint rather than an after-the-fact check.

### 3.4 Do not skip `/verify`

The later cross-document contradictions are found, the higher the cost. `/verify` is the cheapest point to detect problems, especially before entering `/create-plan` and `/execute`.

### 3.5 Do not force implementation when `/execute` finds conflicts

If you find conflicts among PRD, Mockup, UI Spec, Tech Spec, or Test Spec during implementation, pause and clarify the issue at the document layer instead of letting the Agent make hidden assumptions.

### 3.6 Treat `.blueprint/CONTEXT.md` as the entry point for each conversation

When a conversation gets long and the context becomes complex, you can start a fresh chat with only `.blueprint/CONTEXT.md` as the entry point so the Agent can recover the current project state faster.

---

## 4. Frequently Asked Questions

### Q1: Can Blueprint only be used for new projects?

No. Blueprint is equally suitable for iterations on existing projects. For older projects, common starting points are `/issue`, `/create-prd` in iteration mode, or even starting directly from `/create-tech-spec` to fill in missing specifications.

### Q2: I already have a PRD. Do I still need `/create-prd`?

Not necessarily. If the existing PRD is already clear enough, you can start directly from `/create-mockup`. If the PRD quality is only average or its structure needs rework, use `/create-prd` first to reorganize and version it.

### Q3: Do I have to run the full Define stage every time?

Not necessarily. The Blueprint principle is to continue from the current project state, not to regenerate materials that already exist and have been confirmed.

### Q4: Why not just let the Agent write code directly?

Without a unified context, the Agent will often fill in assumptions around requirements, design, technical boundaries, and acceptance criteria on its own, which leads to frequent rework. The value of Blueprint is that it aligns the definition first, then moves into implementation.

### Q5: Are `/issue` and `create-issue` the same thing?

Follow the current public command definitions in the repository. As of now, the issue-recording command is `/issue`. If `create-issue` appeared in earlier discussions or internal shorthand, formal documentation should still standardize on `/issue` to avoid confusion.

---

## 5. Recommended Reading Order

If you are using Blueprint for the first time, the recommended reading order is:

1. `README.md`: Understand Blueprint's positioning and end-to-end flow
2. `START_HERE.md`: Build a quick mental model of how to use it
3. `QUICK_REFERENCE.md`: Check command and path cheat sheets
4. `.cursor/commands/README.md`: Read the detailed command descriptions
5. `Blueprint_playbook.md`: Decide your starting point and usage pattern based on the current project state

---

## 6. One-Sentence Summary

The goal of Blueprint is not to "help the Agent generate code faster," but to "help the Agent work inside a more stable, more consistent, and more verifiable context."

When you are not sure where to start, read `.blueprint/CONTEXT.md` first and ask yourself:

**What materials do I already have, and what is the most reasonable next command?**
