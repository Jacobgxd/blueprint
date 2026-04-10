# blueprint
this is agent workflow for MVP development

README.md
Blueprint — 57Blocks Agentic Engineering OS
Blueprint is a Context-First Agentic Engineering OS built for 57Blocks. It orchestrates a structured multi-agent dialogue before a single line of code is written, producing a Unified Context Package (.blueprint/) that serves as the single source of truth for all downstream execution.

Operating philosophy: Define → Verify → Implement → Iterate. Not Generate → Patch → Patch → Rewrite.

🗂️ Project Structure
.blueprint/                  # Unified Context Package (source of truth for AI)
├── CONTEXT.md               # AI entry point — read this first before any command
├── PRD_V{N}.md              # Product requirements (versioned)
├── UI_Spec.md               # UI specifications
├── Tech_Spec.md             # Technical architecture & implementation spec
├── Test_Spec.md             # Test strategy & acceptance criteria
└── mockup/                  # Runnable static mockup (React + Vite)

reports/                     # Execution records (evidence, not specs)
├── mockup-reviews/          # Versioned mockup review reports
├── test-runs/               # Test run reports with evidence
└── verify/                  # Global Verifier cross-document reports

plans/                       # Development plans (one per feature)
issues/                      # Issue tracking

.cursor/
└── commands/                # All agent commands (see commands/README.md)
🔄 The Agent Pipeline
── DEFINE ────────────────────────────────────────────────────────
  /create-prd          PM Agent       →  .blueprint/PRD_V{N}.md
  /create-ui-spec      Design Agent   →  .blueprint/UI_Spec.md
  /create-mockup       Mockup Agent   →  .blueprint/mockup/
  /review-mockup       Review Agent   →  reports/mockup-reviews/   ⟲ loop until approved
  /create-tech-spec    Dev Agent      →  .blueprint/Tech_Spec.md
  /create-test-spec    QA Agent       →  .blueprint/Test_Spec.md   ← before coding
  /verify              Global Verify  →  reports/verify/

── IMPLEMENT ─────────────────────────────────────────────────────
  /create-plan         Plan Agent     →  plans/[feature].md
  /execute             Exe Agent      →  (reads all .blueprint/ as mission briefing)
  /review              Review Agent   →  code quality + drift detection
  /test                Test Agent     →  reports/test-runs/
⚡ Quick Start
New project
1. Read .blueprint/CONTEXT.md to understand current state
2. Run /create-prd  — generate product requirements
3. Follow the pipeline above, step by step
4. Never skip /verify before /create-plan
New iteration on existing project
1. Read .blueprint/CONTEXT.md
2. Run /create-prd in iteration mode — updates PRD_V{N}.md with new iteration
3. Update downstream docs as needed (UI Spec, Tech Spec, Test Spec)
4. Run /verify to check cross-document consistency
5. Run /create-plan and /execute
🔑 Key Design Decisions
Why .blueprint/ instead of docs/
All specification documents live in .blueprint/ to signal their role: they are machine-readable context, not just human documentation. Every agent reads from here before doing anything.

Why Test Spec before coding
/create-test-spec runs after Tech Spec is approved and before /execute. This makes the acceptance criteria a constraint on coding, not a post-hoc check. The Exe Agent reads the Test Spec as part of its Mission Briefing.
