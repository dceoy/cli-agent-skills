---
name: gh-issue-reopen
description: Reopen a closed GitHub issue using gh CLI, optionally with a comment explaining why.
allowed-tools: Bash, Read, Grep
---

# GitHub Issue Reopen

## When to use

- The user asks to reopen a closed issue.
- Issue was closed prematurely or needs more work.
- Bug reoccurred after being marked fixed.

## Inputs to confirm

- Issue number or URL.
- Optional reopening comment.
- Target repo if not current (`--repo OWNER/REPO`).

## Workflow

1. Verify auth:
   ```bash
   gh --version
   gh auth status
   ```
2. Check issue current state:
   ```bash
   gh issue view 123 --json number,title,state,stateReason
   ```
3. Reopen the issue:
   ```bash
   gh issue reopen 123
   gh issue reopen 123 --comment "Reopening: bug reoccurred in v2.1"
   ```
4. Verify reopening:
   ```bash
   gh issue view 123 --json state
   ```

## Examples

```bash
# Simple reopen
gh issue reopen 123

# Reopen with explanation
gh issue reopen 123 --comment "Issue still reproducible on latest version."

# Reopen by URL
gh issue reopen https://github.com/owner/repo/issues/123
```

## Flags reference

| Flag            | Description             |
| --------------- | ----------------------- |
| `-c, --comment` | Add a reopening comment |

## Notes

- Only closed issues can be reopened.
- Adding a comment helps track why the issue was reopened.
- Arguments accept issue number or URL.

## References

- GitHub CLI manual: https://cli.github.com/manual/
- `gh issue reopen --help`
