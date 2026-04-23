
# Blueprint — 57Blocks Agentic Engineering OS

Blueprint is a Context-First Agentic Engineering OS built for 57Blocks. It orchestrates a structured multi-agent dialogue before a single line of code is written, producing a **Unified Context Package** (`.blueprint/`) that serves as the single source of truth for all downstream execution.

The current design workflow is **PRD-first, mockup-first, spec-after-validation**: start from an existing PRD, generate and iterate the mockup directly, then extract `UI_Spec.md` and `design-system.html` from the confirmed visual result.

**Operating philosophy**: Define → Verify → Implement → Iterate. Not Generate → Patch → Patch → Rewrite.

---

## 🗂️ Project Structure

```
.blueprint/                  # Unified Context Package (source of truth for AI)
├── CONTEXT.md               # AI entry point — read this first before any command
├── PRD.md / PRD_V{N}.md     # Active product requirements
├── UI_Spec.md               # UI specifications distilled from confirmed mockup
├── Tech_Spec.md             # Technical architecture & implementation spec
├── Test_Spec.md             # Test strategy & acceptance criteria
└── mockup/                  # Runnable static mockup assets
    ├── index.html           # Confirmed mockup (single HTML preferred)
    ├── design-system.html   # Visual design-system preview generated with UI Spec
    └── design-notes.md      # Optional design iteration notes

reports/                     # Execution records (evidence, not specs)
├── mockup-reviews/          # Versioned mockup review reports
├── test-runs/               # Test run reports with evidence
└── verify/                  # Global Verifier cross-document reports

plans/                       # Development plans (one per feature)
issues/                      # Issue tracking

.cursor/
└── commands/                # All agent commands (see commands/README.md)
```

---

## 🔄 The Agent Pipeline

```
── DEFINE ────────────────────────────────────────────────────────
  /create-prd          PM Agent       →  .blueprint/PRD_V{N}.md     (optional if no PRD yet)
  /create-mockup       Mockup Agent   →  .blueprint/mockup/index.html
  /review-mockup       Review Agent   →  reports/mockup-reviews/    ⟲ loop until approved
  /create-ui-spec      Design Agent   →  .blueprint/UI_Spec.md
                                        + .blueprint/mockup/design-system.html
  /create-tech-spec    Dev Agent      →  .blueprint/Tech_Spec.md
  /create-test-spec    QA Agent       →  .blueprint/Test_Spec.md   ← before coding
  /verify              Global Verify  →  reports/verify/

── IMPLEMENT ─────────────────────────────────────────────────────
  /create-plan         Plan Agent     →  plans/[feature].md
  /execute             Exe Agent      →  (reads all .blueprint/ as mission briefing)
  /review              Review Agent   →  code quality + drift detection
  /test                Test Agent     →  reports/test-runs/
```

---

## ⚡ Quick Start

### New project

If you already have a PRD, start from `/create-mockup`.

```
1. Read .blueprint/CONTEXT.md to understand current state
2. If PRD does not exist, run /create-prd first
3. Run /create-mockup from the active PRD and iterate until approved
4. Run /create-ui-spec to distill UI_Spec.md + design-system.html
5. Never skip /verify before /create-plan
```

### New iteration on existing project

```
1. Read .blueprint/CONTEXT.md
2. Run /create-prd in iteration mode — updates PRD_V{N}.md with new iteration
3. Rebuild or adjust mockup if the change affects visual structure or UX flow
4. Re-run /create-ui-spec when the confirmed mockup changes
5. Update downstream docs as needed (Tech Spec, Test Spec)
6. Run /verify to check cross-document consistency
7. Run /create-plan and /execute
```

---

## 🔑 Key Design Decisions

**Why `.blueprint/` instead of `docs/`**
All specification documents live in `.blueprint/` to signal their role: they are machine-readable context, not just human documentation. Every agent reads from here before doing anything.

**Why Test Spec before coding**
`/create-test-spec` runs after Tech Spec is approved and before `/execute`. This makes the acceptance criteria a constraint on coding, not a post-hoc check. The Exe Agent reads the Test Spec as part of its Mission Briefing.

**Why Mockup comes before UI Spec**
The mockup is now the primary design exploration surface. Instead of writing a speculative UI spec first, Blueprint validates the actual page feel, hierarchy, information density, and interaction direction in the browser, then distills the confirmed result into `UI_Spec.md`.

**Why `design-system.html` is generated with UI Spec**
`UI_Spec.md` is the structured handoff document; `design-system.html` is the visual preview of the same tokens, components, and rules. Together they reduce ambiguity for both developers and reviewers.

**Why `ui-ux-pro-max` is part of the workflow**
The `.cursor/skills/ui-ux-pro-max/` skill is used during mockup generation and UI spec distillation to improve design-system recommendations, visual direction, typography, UX patterns, and anti-pattern detection. It assists the process, but the confirmed mockup remains the final visual authority.

**Why `/verify` exists**
Before any code is written, all five specification documents (PRD, UI Spec, Tech Spec, Test Spec, Mockup) must be consistent with each other. `/verify` catches contradictions at the cheapest possible moment — before implementation begins.

**Why PRD is versioned (PRD_V1.md, PRD_V2.md)**
Each major version file is cumulative: it contains the full "current state" section (what AI reads when coding) plus an "iteration history" section (why decisions were made). This gives AI agents full context without requiring them to piece together multiple files.

**Why `/execute` has a mandatory Mission Briefing**
The Exe Agent reads Tech Spec, UI Spec, mockup, and Test Spec before touching any code. This is the primary mechanism preventing implementation drift. If the implementation conflicts with any spec, the agent stops and reports — it does not make assumptions.

---

## 📋 Commands at a Glance

| Command | Agent | Output |
|---------|-------|--------|
| `/create-prd` | PM Agent | `.blueprint/PRD_V{N}.md` |
| `/create-mockup` | Mockup Agent | `.blueprint/mockup/index.html` |
| `/review-mockup` | Review Agent | `reports/mockup-reviews/` |
| `/create-ui-spec` | Design Agent | `.blueprint/UI_Spec.md` + `.blueprint/mockup/design-system.html` |
| `/create-tech-spec` | Dev Agent | `.blueprint/Tech_Spec.md` |
| `/create-test-spec` | QA Agent | `.blueprint/Test_Spec.md` |
| `/verify` | Global Verifier | `reports/verify/` |
| `/create-plan` | Plan Agent | `plans/[feature].md` |
| `/execute` | Exe Agent | source code |
| `/review` | Review Agent | drift + quality report |
| `/test` | Test Agent | `reports/test-runs/` |
| `/explore` | — | impact analysis |
| `/document` | — | updated docs |
| `/peer-review` | — | cross-model review |
| `/issue` | — | `issues/[issue].md` |
| `/learn` | — | explanation |

Full command documentation: `.cursor/commands/README.md`

---

## 🛠️ Customization

All agent behavior is defined in `.cursor/commands/*.md`. Each file contains the full system prompt for that agent. Edit them to adjust behavior for specific project types, tech stacks, or team conventions.

For design-heavy projects, also review `.cursor/skills/ui-ux-pro-max/SKILL.md`. It is the built-in design intelligence layer used by `/create-mockup` and `/create-ui-spec`.

When modifying commands, remember to keep the Step 0 context-reading sections intact — they are what give agents the cross-document awareness that prevents drift.

