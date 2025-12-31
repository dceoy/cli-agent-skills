# Spec Kit Workflow Guide

Comprehensive guide to Spec-Driven Development using Spec Kit skills in this repository.

## What is Spec-Driven Development?

Spec-Driven Development flips traditional software development by starting with **executable specifications** instead of jumping straight to code. It emphasizes:

- **Intent-driven development** - Define requirements before implementation
- **Multi-step refinement** - Structured progression from idea to implementation
- **Technology independence** - Works with any language or framework
- **AI-assisted execution** - Specifications guide AI coding assistants

## Core Workflow Sequence

The canonical Spec Kit workflow follows these phases in order:

```mermaid
flowchart LR
    A[1. Constitution<br/>Principles] --> B[2. Specify<br/>What/Why]
    B --> C{3. Clarify?<br/>Optional}
    C -->|Yes| D[Resolve<br/>Ambiguities]
    C -->|No| E[4. Plan<br/>How]
    D --> E
    E --> F{5. Analyze?<br/>Optional}
    F -->|Yes| G[Validate<br/>Consistency]
    F -->|No| H[6. Tasks<br/>Steps]
    G --> H
    H --> I[7. Implement<br/>Build]

    style A fill:#e1f5ff
    style B fill:#fff4e1
    style C fill:#f0f0f0
    style D fill:#f0f0f0
    style E fill:#ffe1f5
    style F fill:#f0f0f0
    style G fill:#f0f0f0
    style H fill:#e1ffe1
    style I fill:#ffe1e1
```

### Phase-by-Phase Breakdown

| Phase | Command                 | Purpose                                  | Output Files                                                         | Required        |
| ----- | ----------------------- | ---------------------------------------- | -------------------------------------------------------------------- | --------------- |
| 1     | `/speckit.constitution` | Define project principles and governance | `.specify/memory/constitution.md`                                    | First time only |
| 2     | `/speckit.specify`      | Capture feature requirements             | `specs/N-name/spec.md`, branch `N-name`                              | Yes             |
| 3     | `/speckit.clarify`      | Resolve specification ambiguities        | Updated `spec.md`                                                    | Optional        |
| 4     | `/speckit.plan`         | Create technical implementation strategy | `specs/N-name/plan.md`, `research.md`, `data-model.md`, `contracts/` | Yes             |
| 5     | `/speckit.analyze`      | Validate cross-artifact consistency      | Analysis report                                                      | Optional        |
| 6     | `/speckit.tasks`        | Break work into actionable units         | `specs/N-name/tasks.md`                                              | Yes             |
| 7     | `/speckit.implement`    | Execute all tasks to build feature       | Implementation code/files                                            | Yes             |

### Additional Commands

| Command                  | Purpose                               | When to Use                    |
| ------------------------ | ------------------------------------- | ------------------------------ |
| `/speckit.checklist`     | Generate custom validation checklists | Quality assurance at any phase |
| `/speckit.taskstoissues` | Convert tasks to GitHub issues        | Project management integration |

## Detailed Phase Guide

### Phase 1: Establish Principles (`/speckit.constitution`)

**When**: Project initialization or when updating governance rules.

**What it does**:

- Creates versioned project constitution with core principles
- Defines non-negotiable rules (test-first, library architecture, etc.)
- Establishes governance and amendment procedures
- Syncs dependent templates with new principles

**Key points**:

- Run once per project (update as needed with semantic versioning)
- Influences all subsequent specs and plans
- Use MAJOR.MINOR.PATCH versioning for constitution changes

**Example input**:

```
/speckit.constitution

Our project follows:
1. Test-first development (non-negotiable)
2. Library-first architecture (standalone, independently testable)
3. CLI interfaces for all functionality
4. Observability through structured logging
```

**Output**: `.specify/memory/constitution.md` with versioned principles

---

### Phase 2: Specify Requirements (`/speckit.specify`)

**When**: Starting a new feature or enhancement.

**What it does**:

- Creates feature branch (e.g., `1-user-auth`)
- Generates structured spec from natural language description
- Defines user stories with priorities (P1, P2, P3)
- Documents acceptance criteria and success metrics
- Identifies assumptions and constraints
- Creates quality validation checklist

**Key points**:

- Focus on **WHAT** and **WHY**, not HOW
- Written for business stakeholders, not developers
- No tech stack, APIs, or implementation details
- Maximum 3 `[NEEDS CLARIFICATION]` markers
- Success criteria must be measurable and technology-agnostic

**Example input**:

```
/speckit.specify Add user authentication with email/password login, password reset, and session management
```

**Output**:

- Branch: `1-user-auth`
- `specs/1-user-auth/spec.md`
- `specs/1-user-auth/checklists/requirements.md`

---

### Phase 3: Clarify Ambiguities (`/speckit.clarify`) [Optional]

**When**: After specify, when specification has unresolved questions.

**What it does**:

- Identifies underspecified areas in the spec
- Asks up to 5 targeted clarification questions
- Updates spec with user's answers
- Removes `[NEEDS CLARIFICATION]` markers

**Key points**:

- Optional but recommended if spec has ambiguities
- Interactive question-answer flow
- Ensures spec completeness before planning

**Example interaction**:

```
/speckit.clarify

Agent asks:
Q1: Should password reset links expire? [Yes - 24h / Yes - 1h / No expiration]
Q2: Maximum login attempts before lockout? [3 attempts / 5 attempts / No limit]

User responds:
Q1: Yes - 1h
Q2: 5 attempts
```

**Output**: Updated `specs/N-name/spec.md` with clarifications

---

### Phase 4: Plan Implementation (`/speckit.plan`)

**When**: After specification is complete and clear.

**What it does**:

- Creates technical implementation strategy
- Chooses tech stack and architecture
- Defines data models and API contracts
- Validates against constitution principles
- Generates research on unknowns
- Updates agent context with new technologies

**Key points**:

- First phase where HOW is addressed
- Constitution compliance is validated
- Research resolves technical unknowns
- Creates contracts (OpenAPI, GraphQL schemas)

**Example input**:

```
/speckit.plan I'm building with Node.js, Express, PostgreSQL, and JWT for auth
```

**Output**:

- `specs/N-name/plan.md`
- `specs/N-name/research.md`
- `specs/N-name/data-model.md`
- `specs/N-name/contracts/*.yaml` or `*.graphql`
- `specs/N-name/quickstart.md`
- Updated agent context files

---

### Phase 5: Validate Consistency (`/speckit.analyze`) [Optional]

**When**: After tasks are generated, before implementation.

**What it does**:

- Cross-checks spec, plan, and tasks for consistency
- Identifies gaps or contradictions
- Validates completeness and quality
- Provides analysis report

**Key points**:

- Quality assurance checkpoint
- Non-destructive (read-only analysis)
- Catches issues before coding begins

**Example input**:

```
/speckit.analyze
```

**Output**: Analysis report highlighting issues or confirming readiness

---

### Phase 6: Generate Tasks (`/speckit.tasks`)

**When**: After planning is complete.

**What it does**:

- Breaks plan into dependency-ordered tasks
- Creates actionable work items with clear descriptions
- Identifies task dependencies and prerequisites
- Categorizes tasks by type (setup, feature, test, docs)

**Key points**:

- Tasks are ordered by dependencies
- Each task is independently actionable
- Clear acceptance criteria per task

**Example input**:

```
/speckit.tasks
```

**Output**: `specs/N-name/tasks.md` with ordered task list

---

### Phase 7: Execute Implementation (`/speckit.implement`)

**When**: After all planning artifacts are ready.

**What it does**:

- Reads spec, plan, and tasks
- Executes each task in dependency order
- Writes code, tests, and documentation
- Validates against acceptance criteria
- Runs tests and builds

**Key points**:

- Final execution phase
- Follows all prior guidance and constraints
- Validates implementation against spec

**Example input**:

```
/speckit.implement
```

**Output**: Fully implemented feature with code, tests, docs

---

## Workflow Scenarios

### Greenfield Development (0-to-1)

**Scenario**: Building a new project from scratch.

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant SK as Spec Kit
    participant Repo as Repository

    Note over Dev,Repo: PROJECT SETUP (Once)
    Dev->>SK: /speckit.constitution
    SK->>Repo: .specify/memory/constitution.md

    Note over Dev,Repo: FEATURE 1
    Dev->>SK: /speckit.specify "User Authentication"
    SK->>Repo: specs/1-user-auth/spec.md + branch
    Dev->>SK: /speckit.clarify (optional)
    SK->>Repo: Updated spec.md
    Dev->>SK: /speckit.plan "Node.js + JWT"
    SK->>Repo: plan.md, research.md, contracts/
    Dev->>SK: /speckit.tasks
    SK->>Repo: tasks.md
    Dev->>SK: /speckit.implement
    SK->>Repo: src/auth/* + tests

    Note over Dev,Repo: FEATURE 2
    Dev->>SK: /speckit.specify "Payment Processing"
    SK->>Repo: specs/2-payment/spec.md + branch
    Note right of SK: Repeat workflow...
```

**Key characteristic**: Start with constitution, build incrementally feature-by-feature.

---

### Brownfield Enhancement (Adding to Existing Code)

**Scenario**: Adding new features to an existing codebase.

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant SK as Spec Kit
    participant Existing as Existing Code
    participant New as New Feature

    Dev->>SK: /speckit.constitution (if needed)
    Note right of SK: Define principles for new work

    Dev->>SK: /speckit.specify "New Dashboard"
    Note right of SK: References existing patterns
    SK->>New: spec.md (with integration notes)

    Dev->>SK: /speckit.plan
    SK->>Existing: Analyze existing architecture
    SK->>New: plan.md (integration strategy)

    Dev->>SK: /speckit.analyze
    SK->>Existing: Validate compatibility
    SK-->>Dev: Compatibility report

    Dev->>SK: /speckit.tasks
    SK->>New: tasks.md (incremental changes)

    Dev->>SK: /speckit.implement
    SK->>Existing: Update existing files
    SK->>New: Add new files
```

**Key characteristic**: Plan considers existing architecture and integration points.

---

### Creative Exploration (Parallel Approaches)

**Scenario**: Testing multiple technical approaches for the same feature.

```mermaid
flowchart TD
    A[Specify Feature Once] --> B{Plan Options}

    B -->|Approach A| C1[Plan: React + REST]
    B -->|Approach B| C2[Plan: Vue + GraphQL]
    B -->|Approach C| C3[Plan: Svelte + tRPC]

    C1 --> D1[Generate: research.md<br/>contracts/rest-api.yaml]
    C2 --> D2[Generate: research.md<br/>contracts/schema.graphql]
    C3 --> D3[Generate: research.md<br/>contracts/trpc-routes.ts]

    D1 --> E{Compare &<br/>Decide}
    D2 --> E
    D3 --> E

    E -->|Choose Best| F[Selected Approach]
    F --> G[Generate Tasks]
    G --> H[Implement]

    style A fill:#fff4e1,stroke:#cc6600,stroke-width:3px
    style B fill:#e1f5ff,stroke:#0066cc
    style C1 fill:#ffe1f5
    style C2 fill:#ffe1f5
    style C3 fill:#ffe1f5
    style E fill:#ffffcc,stroke:#cccc00,stroke-width:3px
    style F fill:#e1ffe1,stroke:#00cc66,stroke-width:3px
    style H fill:#ffe1e1,stroke:#cc0000,stroke-width:3px
```

**Key characteristic**: Same spec, multiple plans, comparative evaluation.

---

## Command Chaining & Dependencies

Commands build on each other sequentially:

```mermaid
graph TD
    CONST[Constitution<br/>Project Principles]
    SPEC[Specify<br/>Feature Requirements]
    CLAR[Clarify<br/>Resolve Ambiguities]
    PLAN[Plan<br/>Technical Design]
    ANAL[Analyze<br/>Validate Artifacts]
    TASK[Tasks<br/>Work Breakdown]
    IMPL[Implement<br/>Execute Build]
    CHECK[Checklist<br/>Quality Gates]

    CONST -->|Required| SPEC
    SPEC -->|Optional| CLAR
    SPEC -->|Skip Clarify| PLAN
    CLAR -->|After Clarification| PLAN
    PLAN -->|Required| TASK
    TASK -->|Optional| ANAL
    TASK -->|Skip Analysis| IMPL
    ANAL -->|After Validation| IMPL

    SPEC -.->|Anytime| CHECK
    PLAN -.->|Anytime| CHECK
    TASK -.->|Anytime| CHECK

    style CONST fill:#e1f5ff,stroke:#0066cc,stroke-width:3px
    style SPEC fill:#fff4e1,stroke:#cc6600,stroke-width:3px
    style CLAR fill:#f0f0f0,stroke:#666,stroke-width:2px,stroke-dasharray: 5 5
    style PLAN fill:#ffe1f5,stroke:#cc0066,stroke-width:3px
    style ANAL fill:#f0f0f0,stroke:#666,stroke-width:2px,stroke-dasharray: 5 5
    style TASK fill:#e1ffe1,stroke:#00cc66,stroke-width:3px
    style IMPL fill:#ffe1e1,stroke:#cc0000,stroke-width:3px
    style CHECK fill:#ffffcc,stroke:#cccc00,stroke-width:2px,stroke-dasharray: 5 5
```

**Critical dependencies**:

- Constitution must exist before first specify
- Specify must complete before plan
- Plan must complete before tasks
- Tasks must complete before implement
- Clarify can run after specify, before plan
- Analyze can run after tasks, before implement
- Checklist can run at any phase for quality validation

## File Structure After Full Workflow

```mermaid
graph TD
    ROOT[Repository Root]

    ROOT --> SPECIFY[.specify/]
    SPECIFY --> MEM[memory/]
    SPECIFY --> TMPL[templates/]
    MEM --> CONST[constitution.md<br/>Phase 1]
    TMPL --> SPEC_TMPL[spec-template.md]
    TMPL --> PLAN_TMPL[plan-template.md]
    TMPL --> TASK_TMPL[tasks-template.md]

    ROOT --> SPECS[specs/]
    SPECS --> FEAT1[1-user-auth/]
    FEAT1 --> SPEC_MD[spec.md<br/>Phase 2]
    FEAT1 --> PLAN_MD[plan.md<br/>Phase 4]
    FEAT1 --> RESEARCH[research.md<br/>Phase 4]
    FEAT1 --> DATA[data-model.md<br/>Phase 4]
    FEAT1 --> TASKS[tasks.md<br/>Phase 6]
    FEAT1 --> QUICK[quickstart.md<br/>Phase 4]
    FEAT1 --> CONTRACTS[contracts/]
    FEAT1 --> CHECKS[checklists/]
    CONTRACTS --> API[auth-api.yaml<br/>user-schema.graphql]
    CHECKS --> REQ[requirements.md]

    ROOT --> SRC[src/]
    SRC --> AUTH[auth/]
    SRC --> TESTS[tests/]
    AUTH --> LOGIN[login.js]
    AUTH --> SESSION[session.js]
    AUTH --> RESET[password-reset.js]
    TESTS --> AUTH_TEST[auth.test.js]

    style CONST fill:#e1f5ff,stroke:#0066cc,stroke-width:2px
    style SPEC_MD fill:#fff4e1,stroke:#cc6600,stroke-width:2px
    style PLAN_MD fill:#ffe1f5,stroke:#cc0066,stroke-width:2px
    style TASKS fill:#e1ffe1,stroke:#00cc66,stroke-width:2px
    style AUTH fill:#ffe1e1,stroke:#cc0000,stroke-width:2px
    style TESTS fill:#ffe1e1,stroke:#cc0000,stroke-width:2px
```

**Text view**:

```
.specify/
├── memory/
│   └── constitution.md           # Project principles (Phase 1)
└── templates/
    ├── spec-template.md
    ├── plan-template.md
    └── tasks-template.md

specs/
└── 1-user-auth/                  # Feature directory
    ├── spec.md                   # Requirements (Phase 2)
    ├── plan.md                   # Technical plan (Phase 4)
    ├── research.md               # Technical research (Phase 4)
    ├── data-model.md             # Entity definitions (Phase 4)
    ├── tasks.md                  # Work breakdown (Phase 6)
    ├── quickstart.md             # Implementation guide (Phase 4)
    ├── contracts/                # API schemas (Phase 4)
    │   ├── auth-api.yaml
    │   └── user-schema.graphql
    └── checklists/               # Quality validation
        └── requirements.md       # Spec validation (Phase 2)

src/                              # Implementation (Phase 7)
├── auth/
│   ├── login.js
│   ├── session.js
│   └── password-reset.js
└── tests/
    └── auth.test.js
```

## Best Practices

### Do's

- **Follow the sequence**: Each phase builds on the previous
- **Constitution first**: Establish principles before first feature
- **Clarify early**: Resolve ambiguities before planning
- **Validate often**: Use analyze and checklist commands
- **Document assumptions**: Make informed guesses, note them in spec
- **Prioritize stories**: Use P1/P2/P3 for user stories (most critical first)
- **Keep specs technology-agnostic**: No implementation details in spec.md

### Don'ts

- **Don't skip specify**: Even small features benefit from structured specs
- **Don't put tech in specs**: Framework choices belong in plan, not spec
- **Don't create circular dependencies**: Tasks must be orderable
- **Don't ignore constitution**: All plans must validate against principles
- **Don't over-clarify**: Maximum 3 `[NEEDS CLARIFICATION]` markers
- **Don't skip tests**: Constitution typically mandates test-first

## Troubleshooting

### "No constitution found"

**Solution**: Run `/speckit.constitution` first (project initialization).

### "Spec has too many [NEEDS CLARIFICATION] markers"

**Solution**: Make informed guesses for non-critical items, document assumptions. Only flag critical decisions.

### "Plan violates constitution principles"

**Solution**: Revise plan to align with constitution or justify exception with explicit rationale.

### "Tasks have circular dependencies"

**Solution**: Review task dependencies, break circular chains by introducing intermediate tasks.

### "Implementation doesn't match spec"

**Solution**: Validate spec and plan first with `/speckit.analyze` before implementing.

## Integration with AI Coding Assistants

Spec Kit works with multiple AI agents:

- **Claude Code** - Uses `.claude/skills/speckit-*` and `.claude/commands/speckit.*`
- **Codex CLI** - Uses `.codex/skills/speckit-*` and `.codex/prompts/speckit.*`
- **GitHub Copilot** - Via custom slash commands
- **Others** - Cursor, Windsurf, Amazon Q, Gemini, etc.

Each agent runtime may have slight variations in invocation, but the workflow sequence remains consistent.

## Related Documentation

- **README.md** - Repository overview and quick start
- **AGENTS.md** - Guidelines for editing agent definitions and skills
- **.claude/skills/speckit-\*/SKILL.md** - Individual skill documentation
- **.specify/templates/** - Template files used by commands
- **github.com/github/spec-kit** - Official Spec Kit toolkit

## Getting Help

- Check individual `SKILL.md` files for command-specific help
- Review template files in `.specify/templates/` for structure
- See the official Spec Kit repository for canonical documentation
- Use `/speckit.clarify` when specifications are unclear
- Use `/speckit.analyze` to validate workflow artifacts

---

**Version**: 1.0.0 | **Last Updated**: 2025-12-31
