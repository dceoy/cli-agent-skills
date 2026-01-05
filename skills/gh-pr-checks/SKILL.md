---
name: gh-pr-checks
description: View CI/CD check status for a GitHub pull request using gh CLI to monitor build and test results.
allowed-tools: Bash, Read, Grep
---

# GitHub PR Checks

## When to use
- The user asks about CI status or checks on a PR.
- Monitoring build/test results before merge.
- Waiting for checks to complete.

## Inputs to confirm
- PR number, URL, or branch name (or current branch PR).
- Whether to watch/wait for completion.
- Target repo if not current (`--repo OWNER/REPO`).

## Workflow
1) Verify auth:
   ```bash
   gh --version
   gh auth status
   ```
2) View check status:
   ```bash
   gh pr checks 123
   gh pr checks  # current branch PR
   ```
3) Watch checks until completion:
   ```bash
   gh pr checks 123 --watch
   gh pr checks 123 --watch --fail-fast
   ```
4) Get JSON output for scripting:
   ```bash
   gh pr checks 123 --json name,state,conclusion
   ```
5) View only required checks:
   ```bash
   gh pr checks 123 --required
   ```

## Examples
```bash
# Check current PR status
gh pr checks

# Watch until all checks complete
gh pr checks 123 --watch

# Exit on first failure while watching
gh pr checks 123 --watch --fail-fast

# View in browser
gh pr checks 123 --web

# Get JSON with bucket categorization
gh pr checks 123 --json name,state,bucket --jq '.[] | select(.bucket == "fail")'
```

## Flags reference
| Flag | Description |
|------|-------------|
| `--watch` | Watch checks until they finish |
| `--fail-fast` | Exit watch on first failure |
| `-i, --interval` | Refresh interval in seconds (default 10) |
| `--required` | Show only required checks |
| `--json` | Output JSON (fields: bucket, name, state, etc.) |
| `-w, --web` | Open checks in browser |

## Exit codes
- `0`: All checks passed
- `1`: Error occurred
- `8`: Checks still pending

## Notes
- The `bucket` JSON field categorizes state into: pass, fail, pending, skipping, cancel.
- Use `--required` to focus on blocking checks.
- `--watch` is useful in CI scripts waiting for dependent checks.

## References
- GitHub CLI manual: https://cli.github.com/manual/
- `gh pr checks --help`
