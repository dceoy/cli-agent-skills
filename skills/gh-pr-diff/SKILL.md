---
name: gh-pr-diff
description: View the diff of a GitHub pull request using gh CLI to see code changes.
allowed-tools: Bash, Read, Grep
---

# GitHub PR Diff

## When to use
- The user asks to see what changed in a PR.
- Reviewing code changes before merge.
- Getting a list of files changed in a PR.

## Inputs to confirm
- PR number, URL, or branch name (or current branch PR).
- Output format (full diff, name-only, patch).
- Target repo if not current (`--repo OWNER/REPO`).

## Workflow
1) Verify auth:
   ```bash
   gh --version
   gh auth status
   ```
2) View the diff:
   ```bash
   # Full diff
   gh pr diff 123

   # List changed files only
   gh pr diff 123 --name-only

   # Patch format
   gh pr diff 123 --patch
   ```
3) Control color output:
   ```bash
   gh pr diff 123 --color always
   gh pr diff 123 --color never | less
   ```
4) Open in browser for visual diff:
   ```bash
   gh pr diff 123 --web
   ```

## Examples
```bash
# View diff of current branch's PR
gh pr diff

# See only file names changed
gh pr diff 123 --name-only

# Get patch format for applying elsewhere
gh pr diff 123 --patch > changes.patch

# Pipe to less for large diffs
gh pr diff 123 --color always | less -R
```

## Flags reference
| Flag | Description |
|------|-------------|
| `--color` | Color output: always, never, auto (default: auto) |
| `--name-only` | Show only names of changed files |
| `--patch` | Display diff in patch format |
| `-w, --web` | Open diff in browser |

## Notes
- Without arguments, shows diff for current branch's PR.
- Use `--name-only` for quick overview of scope.
- Patch format is useful for cherry-picking or backup.

## References
- GitHub CLI manual: https://cli.github.com/manual/
- `gh pr diff --help`
