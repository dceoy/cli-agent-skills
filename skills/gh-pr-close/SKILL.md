---
name: gh-pr-close
description: Close a GitHub pull request using gh CLI, optionally with a comment and branch deletion.
allowed-tools: Bash, Read, Grep
---

# GitHub PR Close

## When to use
- The user asks to close a PR without merging.
- PR is abandoned, superseded, or no longer needed.
- Cleaning up stale PRs.

## Inputs to confirm
- PR number, URL, or branch name.
- Whether to delete the associated branch.
- Optional closing comment.
- Target repo if not current (`--repo OWNER/REPO`).

## Workflow
1) Verify auth:
   ```bash
   gh --version
   gh auth status
   ```
2) Check PR state first:
   ```bash
   gh pr view 123 --json number,title,state,headRefName
   ```
3) Close the PR:
   ```bash
   gh pr close 123
   gh pr close 123 --comment "Closing: superseded by #456"
   gh pr close 123 --delete-branch
   ```
4) Verify closure:
   ```bash
   gh pr view 123 --json state,closedAt
   ```

## Examples
```bash
# Close PR without comment
gh pr close 123

# Close with explanation
gh pr close 123 --comment "No longer needed after refactoring."

# Close and delete branch
gh pr close 123 --delete-branch --comment "Superseded by #200"
```

## Flags reference
| Flag | Description |
|------|-------------|
| `-c, --comment` | Leave a closing comment |
| `-d, --delete-branch` | Delete local and remote branch after close |

## Notes
- Closed PRs can be reopened with `gh pr reopen`.
- Use `--delete-branch` to clean up feature branches.
- Arguments accept number, URL, or branch name.

## References
- GitHub CLI manual: https://cli.github.com/manual/
- `gh pr close --help`
