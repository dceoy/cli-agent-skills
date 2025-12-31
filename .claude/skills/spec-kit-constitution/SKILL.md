---
name: spec-kit-constitution
description: Create or update the project constitution from interactive or provided principle inputs, ensuring all dependent templates stay in sync. Use when establishing project principles, governance rules, or updating core values. Sets the foundation for all spec-kit workflows.
allowed-tools: Bash, Read, Write, Edit, Grep, Glob
---

# Spec-Kit Constitution

Create or update the project constitution with versioned principles and governance rules. This is a **foundational step** that establishes project values for all spec-kit workflows.

## When to Use

- Starting a new project and defining principles
- Updating project values or governance rules
- User asks to "set up constitution" or "define principles"
- Need to document non-negotiable project rules
- Before creating specs to ensure alignment with project values

## What It Does

Creates/updates `.specify/memory/constitution.md` with:

1. **Project identity** (name, purpose, scope)
2. **Core principles** with rationale (testable, non-negotiable rules)
3. **Governance** (amendment procedure, versioning, compliance)
4. **Version tracking** (semantic versioning for constitution changes)
5. **Template synchronization** (propagates changes to dependent artifacts)

## Prerequisites

- Spec-kit initialized (.specify/ directory exists)
- Run from repository root
- Constitution template exists at `.specify/memory/constitution.md`

## Basic Usage

### Step 1: Load Constitution Template

The constitution is a template with placeholders in square brackets:

```markdown
# Project Constitution v[CONSTITUTION_VERSION]

## Project Identity

**Name:** [PROJECT_NAME]
**Purpose:** [PROJECT_PURPOSE]

## Principles

### [PRINCIPLE_1_NAME]

[PRINCIPLE_1_DESCRIPTION]

**Rationale:** [PRINCIPLE_1_RATIONALE]
```

### Step 2: Collect Values for Placeholders

Values come from:

- **User input** (conversation)
- **Repository context** (README, existing docs)
- **Prior constitution** (if updating)
- **Interactive prompts** (if values missing)

**Special placeholders:**

- `CONSTITUTION_VERSION` - Semantic version (MAJOR.MINOR.PATCH)
- `RATIFICATION_DATE` - Original adoption date (YYYY-MM-DD)
- `LAST_AMENDED_DATE` - Last update date (YYYY-MM-DD, today if changed)

### Step 3: Version Increment Rules

**Semantic versioning:**

- **MAJOR** - Backward incompatible changes (principle removal, governance redefinition)
- **MINOR** - New principle added, materially expanded guidance
- **PATCH** - Clarifications, wording fixes, non-semantic refinements

If version bump type is ambiguous, propose reasoning before finalizing.

### Step 4: Draft Updated Constitution

Replace all placeholders with concrete values:

- No bracketed tokens remaining (except intentionally deferred, explicitly justified)
- Each principle has: succinct name, description (paragraph or bullets), explicit rationale
- Governance section includes: amendment procedure, versioning policy, compliance expectations
- Preserve heading hierarchy, remove template comments once replaced

### Step 5: Consistency Propagation

After updating constitution, validate dependent artifacts:

**Template files to check:**

- `.specify/templates/plan-template.md` - Constitution checks align with updated principles
- `.specify/templates/spec-template.md` - Scope/requirements align with new constraints
- `.specify/templates/tasks-template.md` - Task categorization reflects principle-driven types
- `.specify/templates/commands/*.md` - No outdated agent-specific references

**Documentation to check:**

- `README.md` - References to principles are current
- `docs/quickstart.md` - Guidance reflects updated governance
- Any agent-specific guides

### Step 6: Sync Impact Report

Prepend HTML comment to constitution file with:

```html
<!--
Constitution Version Change: v1.0.0 → v1.1.0

Modified Principles:
- Testing Discipline → Test-First Development (renamed)

Added Sections:
- Observability Principle

Removed Sections:
- (none)

Templates Requiring Updates:
✅ .specify/templates/plan-template.md - Updated
✅ .specify/templates/spec-template.md - Updated
⚠ .specify/templates/tasks-template.md - Pending review

Follow-up TODOs:
- Define [DEPLOYMENT_STRATEGY] placeholder (deferred to v1.2.0)
-->
```

### Step 7: Validation Checklist

Before finalizing:

- [ ] No unexplained bracket tokens remain
- [ ] Version line matches sync report
- [ ] Dates in ISO format (YYYY-MM-DD)
- [ ] Principles are declarative and testable
- [ ] "Should" replaced with MUST/SHOULD with rationale
- [ ] All dependent templates reviewed

### Step 8: Final Output

Write completed constitution to `.specify/memory/constitution.md` and provide summary:

```
Constitution Updated: v1.1.0

Version Change:
- Bump: MINOR (added new observability principle)
- Previous: v1.0.0
- Current: v1.1.0
- Last Amended: 2025-01-15

Changes:
- Added Principle: Observability (all services must emit metrics)
- Updated: Testing Discipline → Test-First Development
- Templates synced: 3/3 ✅

Files Flagged for Manual Review:
- docs/architecture.md - Update observability section

Suggested Commit:
docs: amend constitution to v1.1.0 (add observability principle)

Next: Run spec-kit-specify to create feature specifications aligned with updated principles
```

## Output Format

### Constitution Structure

```markdown
# Project Constitution v1.0.0

**Ratified:** 2025-01-01
**Last Amended:** 2025-01-15

## Project Identity

**Name:** MyProject
**Purpose:** Enable rapid feature development with quality
**Scope:** Web application and REST API

## Principles

### 1. Test-First Development

All features MUST have automated tests written before implementation.

**Rationale:** Prevents regressions, ensures requirements clarity, enables confident refactoring.

### 2. API-First Design

All data access MUST occur through documented REST APIs.

**Rationale:** Enables frontend/backend separation, supports mobile clients, facilitates testing.

### 3. Observability

All services MUST emit structured logs, metrics, and traces.

**Rationale:** Enables rapid incident response, performance optimization, capacity planning.

## Governance

### Amendment Procedure

1. Propose change via pull request with rationale
2. Team review and discussion
3. Approval requires consensus
4. Increment version per semantic versioning
5. Update all dependent templates

### Versioning Policy

- **MAJOR:** Breaking governance changes
- **MINOR:** New principles added
- **PATCH:** Clarifications only

### Compliance Review

- Quarterly review of adherence
- Annual constitution review for relevance
- Violations require remediation plan
```

## Best Practices

✅ **DO:**

- Keep principles concise and testable
- Provide clear rationale for each principle
- Use semantic versioning strictly
- Sync all dependent templates
- Document deferred placeholders

❌ **DON'T:**

- Leave unexplained placeholders
- Skip version increment
- Forget to update dependent artifacts
- Make principles vague or aspirational
- Skip rationale explanations

## Example Workflow

```
User: "Set up constitution for my e-commerce project with focus on security and performance"

1. Load constitution template from .specify/memory/constitution.md

2. Collect values:
   - PROJECT_NAME: E-Commerce Platform
   - PROJECT_PURPOSE: Secure, fast online shopping
   - PRINCIPLE_1_NAME: Security First
   - PRINCIPLE_1_DESCRIPTION: All data in transit encrypted, sensitive data at rest encrypted
   - PRINCIPLE_2_NAME: Performance Budget
   - PRINCIPLE_2_DESCRIPTION: Page load < 2s, API response < 500ms

3. Set governance:
   - Amendment requires security team approval
   - Quarterly compliance review mandatory

4. Version: 1.0.0 (initial)
   - RATIFICATION_DATE: 2025-01-15
   - LAST_AMENDED_DATE: 2025-01-15

5. Write constitution to .specify/memory/constitution.md

6. Sync templates:
   - Update plan-template.md to include security checklist
   - Update spec-template.md to require performance criteria
   - Update tasks-template.md to include security review tasks

7. Output summary:
   - Constitution created: v1.0.0
   - 2 core principles defined
   - 3 templates updated
   - Ready for spec-kit-specify
```

## Version Management

### When to Increment

**MAJOR (1.0.0 → 2.0.0):**

- Remove existing principle
- Change governance model fundamentally
- Invalidate existing specs/plans

**MINOR (1.0.0 → 1.1.0):**

- Add new principle
- Expand existing principle materially
- Add new governance section

**PATCH (1.0.0 → 1.0.1):**

- Fix typos
- Clarify wording
- Update examples

### Version History Tracking

Each amendment adds entry to sync impact report (as HTML comment at top).

## Principle Guidelines

### Writing Good Principles

**Components:**

1. **Name** - Concise, memorable (2-5 words)
2. **Description** - Specific, testable rule (use MUST/SHOULD/MAY)
3. **Rationale** - Why this matters (1-2 sentences)

**Examples:**

✅ **Good:**

```markdown
### API-First Design

All data access MUST occur through documented REST APIs with OpenAPI specs.

**Rationale:** Enables frontend/backend team independence, supports future mobile apps, facilitates contract testing.
```

❌ **Bad:**

```markdown
### Good APIs

We should try to make good APIs.

**Rationale:** APIs are important.
```

## Dependent Template Sync

### Templates Affected by Constitution

**plan-template.md:**

- Constitution compliance checklist
- Principle-specific validation steps

**spec-template.md:**

- Required sections per principles
- Acceptance criteria templates

**tasks-template.md:**

- Task categories aligned with principles
- Review/validation tasks

**commands/\*.md:**

- Governance references
- Compliance automation

### Sync Process

For each template:

1. Read current version
2. Identify sections referencing principles
3. Update to match new/changed principles
4. Verify no obsolete principle references remain
5. Mark in sync report (✅ updated or ⚠ pending)

## Deferred Placeholders

If critical information is missing:

```markdown
## Deployment

**Strategy:** TODO(DEPLOYMENT_STRATEGY): Define CI/CD pipeline requirements

**Rationale:** Deferred until infrastructure team provides constraints
```

Document in sync impact report under "Follow-up TODOs".

## Next Steps

After creating/updating constitution:

- **Specify** features with `spec-kit-specify` (aligned with principles)
- **Plan** implementations with `spec-kit-plan` (validates against constitution)
- **Review** existing specs for compliance with new principles

## Related Skills

- **spec-kit-specify** - Creates specs aligned with constitution
- **spec-kit-plan** - Validates plans against constitution
- **spec-kit-analyze** - Checks constitution compliance

## Common Issues

**Missing rationale:**

```
Each principle requires explicit rationale - why is this non-negotiable?
```

**Vague principles:**

```
Replace "should be fast" with measurable target: "API response < 500ms p95"
```

**Forgotten template sync:**

```
Warning: plan-template.md still references removed principle "X"
Update template to remove obsolete references
```

## Tips for Effective Constitutions

1. **Start small** - 3-5 core principles initially
2. **Make testable** - Each principle should be verifiable
3. **Version strictly** - Follow semantic versioning rules
4. **Sync religiously** - Keep all templates aligned
5. **Review regularly** - Quarterly compliance + annual relevance check

---

**Remember**: The constitution is the foundation. All specs, plans, and tasks derive validation from these principles. Keep it concise, testable, and current.
