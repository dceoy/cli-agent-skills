---
name: gh-pr-list
description: List and filter GitHub pull requests using gh CLI with various filters like state, author, labels, and search queries.
allowed-tools: Bash, Read, Grep
---

# GitHub PR List

## When to use

- The user asks to list pull requests in a repository.
- You need to find PRs by author, label, state, or search query.
- Checking overall PR backlog or finding specific PRs.

## Inputs to confirm

- Filter criteria: state (open/closed/merged/all), author, assignee, labels.
- Search query if advanced filtering needed.
- Target repo if not current (`--repo OWNER/REPO`).
- Output format (table, JSON, web).

## Workflow

1. Verify auth:
   ```bash
   gh --version
   gh auth status
   ```
2. List PRs with filters:
   ```bash
   gh pr list
   gh pr list --state all --limit 50
   gh pr list --author "@me"
   gh pr list --label "bug" --label "priority"
   gh pr list --assignee "@me" --state open
   ```
3. Use search syntax for advanced queries:
   ```bash
   gh pr list --search "status:success review:required"
   gh pr list --search "draft:false review:approved"
   ```
4. Get JSON output for scripting:
   ```bash
   gh pr list --json number,title,state,author --jq '.[] | "\(.number): \(.title)"'
   ```

## Examples

```bash
# List your open PRs
gh pr list --author "@me"

# Find PRs needing review
gh pr list --search "review:required"

# List merged PRs to main
gh pr list --state merged --base main --limit 20

# Get PR numbers and titles as JSON
gh pr list --json number,title,reviewDecision
```

## Flags reference

| Flag             | Description                                       |
| ---------------- | ------------------------------------------------- |
| `-s, --state`    | Filter: open, closed, merged, all (default: open) |
| `-A, --author`   | Filter by author                                  |
| `-a, --assignee` | Filter by assignee                                |
| `-l, --label`    | Filter by label (repeatable)                      |
| `-B, --base`     | Filter by base branch                             |
| `-H, --head`     | Filter by head branch                             |
| `-S, --search`   | Search with GitHub query syntax                   |
| `-L, --limit`    | Max items to fetch (default 30)                   |
| `--json`         | Output specific fields as JSON                    |
| `-w, --web`      | Open list in browser                              |

## References

- GitHub CLI manual: https://cli.github.com/manual/
- Search syntax: https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests
- `gh pr list --help`
