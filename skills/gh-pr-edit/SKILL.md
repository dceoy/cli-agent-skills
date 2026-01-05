---
name: gh-pr-edit
description: Edit GitHub pull request metadata (title, body, labels, reviewers, assignees, projects) using gh CLI.
allowed-tools: Bash, Read, Grep
---

# GitHub PR Edit

## When to use

- The user asks to update PR title, body, or metadata.
- Adding or removing labels, reviewers, or assignees.
- Changing base branch or milestone.

## Inputs to confirm

- PR number, URL, or branch name (or current branch PR).
- Changes to apply (title, body, labels, reviewers, etc.).
- Target repo if not current (`--repo OWNER/REPO`).

## Workflow

1. Verify auth:
   ```bash
   gh --version
   gh auth status
   ```
2. View current PR state:
   ```bash
   gh pr view 123 --json title,body,labels,assignees,reviewRequests
   ```
3. Apply edits:

   ```bash
   # Update title and body
   gh pr edit 123 --title "New title" --body "Updated description"

   # Manage labels
   gh pr edit 123 --add-label "bug,priority" --remove-label "triage"

   # Manage reviewers
   gh pr edit 123 --add-reviewer monalisa,hubot
   gh pr edit 123 --remove-reviewer oldreviewer

   # Manage assignees
   gh pr edit 123 --add-assignee "@me" --remove-assignee someone

   # Change base branch
   gh pr edit 123 --base develop
   ```

4. Verify changes:
   ```bash
   gh pr view 123
   ```

## Examples

```bash
# Update title
gh pr edit 123 --title "feat: Add user authentication"

# Add labels and reviewer
gh pr edit 123 --add-label "enhancement" --add-reviewer team-lead

# Assign yourself
gh pr edit 123 --add-assignee "@me"

# Update body from file
gh pr edit 123 --body-file updated-description.md

# Change milestone
gh pr edit 123 --milestone "v2.0"
```

## Flags reference

| Flag                 | Description                   |
| -------------------- | ----------------------------- |
| `-t, --title`        | Set new title                 |
| `-b, --body`         | Set new body                  |
| `-F, --body-file`    | Read body from file           |
| `-B, --base`         | Change base branch            |
| `--add-label`        | Add labels                    |
| `--remove-label`     | Remove labels                 |
| `--add-reviewer`     | Add reviewers                 |
| `--remove-reviewer`  | Remove reviewers              |
| `--add-assignee`     | Add assignees (@me supported) |
| `--remove-assignee`  | Remove assignees              |
| `--add-project`      | Add to projects               |
| `--remove-project`   | Remove from projects          |
| `-m, --milestone`    | Set milestone                 |
| `--remove-milestone` | Remove milestone              |

## Notes

- Without arguments, edits current branch's PR.
- `@me` assigns yourself; `@copilot` supported on GitHub.com.
- Project edits may require `gh auth refresh -s project`.

## References

- GitHub CLI manual: https://cli.github.com/manual/
- `gh pr edit --help`
