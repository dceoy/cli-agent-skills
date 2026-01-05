---
name: gh-pr-comment
description: Add, edit, or delete comments on a GitHub pull request using gh CLI.
allowed-tools: Bash, Read, Grep
---

# GitHub PR Comment

## When to use
- The user asks to comment on a PR.
- Posting status updates or feedback on a PR.
- Editing or deleting previous comments.

## Inputs to confirm
- PR number, URL, or branch name (or current branch PR).
- Comment body text or file.
- Whether to edit or delete last comment.

## Workflow
1) Verify auth:
   ```bash
   gh --version
   gh auth status
   ```
2) Post a comment:
   ```bash
   gh pr comment 123 --body "LGTM! Ready for merge."
   gh pr comment 123 --body-file review-notes.md
   ```
3) Edit or delete your last comment:
   ```bash
   gh pr comment 123 --edit-last --body "Updated: addressed concerns"
   gh pr comment 123 --delete-last --yes
   ```
4) Open editor or browser:
   ```bash
   gh pr comment 123 --editor
   gh pr comment 123 --web
   ```

## Examples
```bash
# Quick comment
gh pr comment 123 --body "Testing this now."

# Comment from file
gh pr comment 123 --body-file feedback.md

# Edit last comment
gh pr comment 123 --edit-last --body "Actually, found one more issue."

# Delete last comment
gh pr comment 123 --delete-last --yes

# Comment on current branch's PR
gh pr comment --body "Addressed review feedback."
```

## Flags reference
| Flag | Description |
|------|-------------|
| `-b, --body` | Comment body text |
| `-F, --body-file` | Read body from file (use "-" for stdin) |
| `--edit-last` | Edit your last comment |
| `--delete-last` | Delete your last comment |
| `--create-if-none` | Create comment if none exists (with --edit-last) |
| `--yes` | Skip delete confirmation |
| `-e, --editor` | Open editor to write comment |
| `-w, --web` | Open browser to write comment |

## Notes
- Without `--body` or `--body-file`, opens interactive prompt.
- Only your own comments can be edited/deleted.
- Use `--create-if-none` with `--edit-last` for idempotent updates.

## References
- GitHub CLI manual: https://cli.github.com/manual/
- `gh pr comment --help`
