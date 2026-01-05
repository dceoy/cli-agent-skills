---
name: gh-pr-checkout
description: Check out a GitHub pull request locally using gh CLI to review or test changes.
allowed-tools: Bash, Read, Grep
---

# GitHub PR Checkout

## When to use

- The user asks to check out a PR locally.
- You need to test or review PR changes on your machine.
- Switching between PRs for code review.

## Inputs to confirm

- PR number, URL, or branch name.
- Custom local branch name (optional).
- Target repo if not current (`--repo OWNER/REPO`).

## Workflow

1. Verify auth and git status:
   ```bash
   gh --version
   gh auth status
   git status
   ```
2. Check out the PR:
   ```bash
   gh pr checkout 123
   gh pr checkout https://github.com/OWNER/REPO/pull/123
   gh pr checkout feature-branch
   ```
3. Use options as needed:

   ```bash
   # Custom local branch name
   gh pr checkout 123 --branch my-review-branch

   # Force update existing branch
   gh pr checkout 123 --force

   # Detached HEAD (no local branch)
   gh pr checkout 123 --detach
   ```

4. After checkout, verify:
   ```bash
   git branch --show-current
   git log --oneline -5
   ```

## Examples

```bash
# Check out PR #123
gh pr checkout 123

# Check out with custom branch name
gh pr checkout 123 --branch review-feature-x

# Force refresh an already checked out PR
gh pr checkout 123 --force

# Interactive selection from recent PRs
gh pr checkout
```

## Flags reference

| Flag                   | Description                                   |
| ---------------------- | --------------------------------------------- |
| `-b, --branch`         | Local branch name (default: head branch name) |
| `--detach`             | Checkout with detached HEAD                   |
| `-f, --force`          | Reset existing local branch to PR state       |
| `--recurse-submodules` | Update submodules after checkout              |

## Notes

- Without arguments, interactively select from recent PRs.
- The `--force` flag is useful when PR has been updated.
- Use `--detach` for quick inspection without creating a branch.

## References

- GitHub CLI manual: https://cli.github.com/manual/
- `gh pr checkout --help`
