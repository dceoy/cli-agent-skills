# ai-coding-agent-skills

Agent skills for AI coders

## Overview

This repository provides reusable skills and templates for multiple agent runtimes, backed by a shared `skills/` directory:

- **Claude Code** - Agents in `.claude/agents/`; skills surfaced via `.claude/skills -> ../skills`
- **Codex CLI** - Skills surfaced via `.codex/skills -> ../skills`
- **GitHub Copilot CLI** - Agents/prompts in `.github/agents/`, `.github/prompts/`; skills surfaced via `.github/skills -> ../skills`
- **Gemini CLI** - Skills surfaced via `.claude/skills -> ../skills`

Each skill directory contains a `SKILL.md` documentation file.

## Quick start

1. Clone the repo:

   ```bash
   git clone git@github.com:dceoy/ai-coding-agent-skills.git
   ```

2. Pick a runtime and explore the skills in `skills/` (symlinked into each runtime directory):
   - **Claude Code:** `.claude/agents/` (agent definitions), `.claude/commands/` (command prompts), `.claude/skills -> ../skills`
   - **Codex CLI:** `.codex/skills -> ../skills`, `.codex/prompts/` (prompt files)
   - **Gemini CLI:** `.gemini/commands/` (prompt files)
   - **GitHub Copilot CLI:** `.github/agents/`, `.github/prompts/`, `.github/skills -> ../skills`

3. Open a skill directory and read the `SKILL.md` to learn how to invoke it.

## Skills by runtime

### Claude Code

**Skills** (`skills/`, symlinked into `.claude/skills/`)

- `copilot-ask`, `copilot-exec`, `copilot-review`, `copilot-search` - GitHub Copilot CLI integration
- `codex-ask`, `codex-exec`, `codex-review`, `codex-search` - OpenAI Codex CLI integration
- `gemini-ask`, `gemini-exec`, `gemini-review`, `gemini-search` - Gemini CLI integration
- `gh-issue-close`, `gh-issue-comment`, `gh-issue-create`, `gh-issue-develop`, `gh-issue-edit`, `gh-issue-list`, `gh-issue-reopen`, `gh-issue-view` - GitHub Issues helpers
- `gh-pr-checks`, `gh-pr-checkout`, `gh-pr-close`, `gh-pr-comment`, `gh-pr-create`, `gh-pr-diff`, `gh-pr-edit`, `gh-pr-list`, `gh-pr-merge`, `gh-pr-ready`, `gh-pr-review`, `gh-pr-view` - Pull request helpers

**Agents** (`.claude/agents/`)

- `codex.md` - Unified Codex CLI agent (ask, exec, review, search modes)
- `copilot.md` - Unified Copilot CLI agent (ask, exec, review, search modes)
- `gemini.md` - Unified Gemini CLI agent (ask, exec, review, search modes)
- See [AGENTS.md](./AGENTS.md) for agent documentation

### Codex CLI

**Skills** (`skills/`, symlinked into `.codex/skills/`)

- `claude-ask`, `claude-exec`, `claude-review`, `claude-search` - Claude Code integration (native)
- `copilot-*`, `gemini-*`, `gh-*` - Shared via `skills/`

### GitHub Copilot CLI

**Skills** (`skills/`, symlinked into `.github/skills/`)

- Shared via `skills/`

## Structure

```
.
├── skills/              # Shared skill directories (source of truth for all runtimes)
├── .claude/
│   ├── agents/          # Claude Code agent definitions (codex-*, copilot-*, gemini-*)
│   └── skills -> ../skills
├── .codex/
│   └── skills -> ../skills
├── .github/
│   ├── skills -> ../skills
│   └── workflows/       # CI workflows (ci.yml)
└── ...
```

## Prerequisites

Install and authenticate the required CLI tools before running skills:

- **Claude Code** - For `.claude/` skills, agents, and commands
  - Install: https://claude.com/claude-code
  - Auth: Follow CLI onboarding flow
- **GitHub Copilot CLI** - For `copilot-*` skills
  - Install: https://github.com/features/copilot/cli
  - Auth: `gh auth login` (requires GitHub Copilot subscription)
- **OpenAI Codex CLI** - For `codex-*` skills
  - Install: https://developers.openai.com/codex/cli/
  - Auth: ChatGPT subscription or API key in `~/.codex/config.toml`
- **Gemini CLI** - For `gemini-*` skills

## Usage notes

- Skills do not always auto-run; use your agent's skill invocation flow or ask for the skill explicitly.
- If a skill fails, open its `SKILL.md` and verify prerequisites and command syntax.

## Troubleshooting

**Skill not found**

- Confirm the skill directory exists in the expected runtime location
- Check that skill name matches exactly (case-sensitive)
- Verify the `SKILL.md` documentation is present

**CLI not in PATH**

- Ensure the tool is installed and accessible: `which <tool-name>`
- Add the tool's bin directory to your shell PATH
- Restart your terminal after installation

**Authentication errors**

- Re-run the tool's auth command:
  - Claude Code: Follow onboarding flow
  - Copilot CLI: `gh auth login`
  - Codex CLI: `codex` (follow auth flow) or configure `~/.codex/config.toml`
- Verify active subscription (Copilot, ChatGPT) or API key (Codex)

**Symlink issues**

- Skill directories are shared from `skills/` via symlinks (`.claude/skills`, `.codex/skills`, `.github/skills`)
- If broken, recreate the symlink or ensure `skills/` exists
- On Windows, ensure symlink support is enabled

## Contributing

See `AGENTS.md` for repository guidelines and agent-specific rules.

## License

See `LICENSE` for details.
