---
name: gh-issue-list
description: List and filter GitHub issues using gh CLI with various filters like state, author, labels, milestone, and search queries.
allowed-tools: Bash, Read, Grep
---

# GitHub Issue List

## When to use

- The user asks to list issues in a repository.
- Finding issues by author, label, milestone, or state.
- Reviewing issue backlog or triaging.

## Inputs to confirm

- Filter criteria: state (open/closed/all), author, assignee, labels, milestone.
- Search query if advanced filtering needed.
- Target repo if not current (`--repo OWNER/REPO`).
- Output format (table, JSON, web).

## Workflow

1. Verify auth:
   ```bash
   gh --version
   gh auth status
   ```
2. List issues with filters:
   ```bash
   gh issue list
   gh issue list --state all --limit 50
   gh issue list --author "@me"
   gh issue list --label "bug" --label "priority"
   gh issue list --assignee "@me" --state open
   gh issue list --milestone "v2.0"
   ```
3. Use search syntax for advanced queries:
   ```bash
   gh issue list --search "no:assignee sort:created-asc"
   gh issue list --search "is:open label:bug -label:wontfix"
   ```
4. Get JSON output for scripting:
   ```bash
   gh issue list --json number,title,state,labels --jq '.[] | "\(.number): \(.title)"'
   ```

## Examples

```bash
# List your assigned issues
gh issue list --assignee "@me"

# Find unassigned bugs
gh issue list --label "bug" --search "no:assignee"

# List issues in a milestone
gh issue list --milestone "Release 1.0"

# Get issues as JSON
gh issue list --json number,title,state,assignees

# Open issue list in browser
gh issue list --web
```

## Flags reference

| Flag              | Description                               |
| ----------------- | ----------------------------------------- |
| `-s, --state`     | Filter: open, closed, all (default: open) |
| `-A, --author`    | Filter by author                          |
| `-a, --assignee`  | Filter by assignee                        |
| `-l, --label`     | Filter by label (repeatable)              |
| `-m, --milestone` | Filter by milestone name or number        |
| `--mention`       | Filter by mentioned user                  |
| `-S, --search`    | Search with GitHub query syntax           |
| `-L, --limit`     | Max items to fetch (default 30)           |
| `--json`          | Output specific fields as JSON            |
| `-w, --web`       | Open list in browser                      |

## References

- GitHub CLI manual: https://cli.github.com/manual/
- Search syntax: https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests
- `gh issue list --help`
