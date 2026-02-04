---
name: code-review
description: Perform comprehensive code review on a pull request, checking for bugs, AGENTS.md/CLAUDE.md compliance, and historical context issues.
---

# Code Review Skill

Provide thorough, multi-agent code review for pull requests with high-confidence issue detection.

## When to Use

- Reviewing a pull request before merge.
- Checking code changes for bugs and AGENTS.md/CLAUDE.md compliance.
- Validating that changes align with historical context and existing code comments.

## Inputs

- Pull request URL or number (required).
- Repository context with AGENTS.md/CLAUDE.md files.

If the pull request is not specified, ask for it before proceeding.

## Workflow

1. **Eligibility Check** (fast agent): Verify the PR is eligible for review:
   - Not closed
   - Not a draft
   - Not automated or trivially simple
   - No prior code review from this tool

2. **Gather AGENTS.md/CLAUDE.md Files** (fast agent): Collect paths to relevant guideline files:
   - Root AGENTS.md or CLAUDE.md (if exists)
   - AGENTS.md/CLAUDE.md files in directories modified by the PR

3. **Summarize Changes** (fast agent): View the PR and return a summary of the change.

4. **Parallel Code Review** (5 default agents): Each agent reviews independently and returns issues with reasons:
   - **Agent 1**: Audit changes for AGENTS.md/CLAUDE.md compliance
   - **Agent 2**: Shallow scan for obvious bugs (focus on large issues, avoid nitpicks)
   - **Agent 3**: Review git blame and history for context-aware bug detection
   - **Agent 4**: Check previous PRs touching these files for relevant comments
   - **Agent 5**: Verify changes comply with guidance in code comments

5. **Score Issues** (fast agents, parallel): For each issue found, score confidence (0-100):
   - **0**: False positive, doesn't stand up to scrutiny
   - **25**: Might be real, couldn't verify, stylistic without AGENTS.md/CLAUDE.md backing
   - **50**: Verified real but may be a nitpick or rare
   - **75**: Double-checked, very likely real, important impact or AGENTS.md/CLAUDE.md-mentioned
   - **100**: Absolutely certain, will happen frequently, evidence confirms

6. **Filter Issues**: Keep only issues with score >= 80.

7. **Re-check Eligibility** (fast agent): Confirm PR is still eligible for review.

8. **Post Comment**: Use `gh pr comment` to post results to the PR.

## False Positive Guidelines

Exclude these from reported issues:

- Pre-existing issues (not introduced by the PR)
- Apparent bugs that aren't actually bugs
- Pedantic nitpicks a senior engineer wouldn't flag
- Issues caught by linters, typecheckers, or compilers
- General code quality issues unless required in AGENTS.md/CLAUDE.md
- AGENTS.md/CLAUDE.md issues explicitly silenced in code
- Intentional functionality changes related to the broader change
- Real issues on lines not modified by the PR

## Output Format

### When Issues Found

```markdown
### Code review

Found N issues:

1. <brief description> (AGENTS.md/CLAUDE.md says "<relevant quote>")

<link to file and line with full sha1 + line range>

2. <brief description> (some/other/AGENTS.md says "<...>")

<link to file and line with full sha1 + line range>

Generated with [Claude Code](https://claude.ai/code)

<sub>- If this code review was useful, please react with thumbs up. Otherwise, react with thumbs down.</sub>
```

### When No Issues Found

```markdown
### Code review

No issues found. Checked for bugs and AGENTS.md/CLAUDE.md compliance.

Generated with [Claude Code](https://claude.ai/code)
```

## Link Format Requirements

When linking to code:

- Use full git SHA (not `$(git rev-parse HEAD)`)
- Format: `https://github.com/owner/repo/blob/<full-sha>/path/file.ext#L<start>-L<end>`
- Include at least 1 line of context before and after
- Repo name must match the PR's repository

## Constraints

- Do not run builds, typechecks, or tests (CI handles these).
- Use `gh` CLI for all GitHub interactions.
- Create a todo list before starting.
- Cite and link every reported issue.
- Keep output brief, avoid emojis in comments.

## Outputs

- Comment posted to the pull request with review results.
