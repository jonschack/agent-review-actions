# Agent Skills and Capabilities

## Overview

This document describes the skills and capabilities available to AI agents operating in this repository.

## GitHub API Skills

### Pull Request Operations
- `gh pr create` — Create a new pull request
- `gh pr edit` — Modify PR metadata (labels, reviewers, etc.)
- `gh pr comment` — Add comments to a PR
- `gh pr review` — Submit a review
- `gh pr diff` — Get the diff for a PR
- `gh pr merge` — Merge a PR (requires human approval)

### Issue Operations
- `gh issue create` — Create a new issue
- `gh issue comment` — Comment on an issue
- `gh issue edit` — Modify issue metadata

### Repository Operations
- `gh api` — Make arbitrary GitHub API calls
- `actions/checkout` — Clone repository
- `git push` — Push commits to branches

## Agent-Specific Skills

### GitHub Copilot
- Native PR review via reviewer assignment
- Responds to `@copilot` mentions in comments
- Can be triggered via issue assignment
- Automatically addresses feedback when mentioned

### OpenAI Codex
- Invoked via `openai/codex-action` GitHub Action
- Accepts natural language prompts
- Returns structured responses
- Can execute multi-step coding tasks

### Google Jules
- Invoked via `google-labs-code/jules-action` GitHub Action
- Operates asynchronously in cloud VMs
- Produces complete code changes with reasoning
- Supports audio changelog generation

## Workflow Skills

### State Management
- Label-based state tracking (`review-iteration-N`)
- Concurrency groups for preventing race conditions
- Job outputs for passing data between steps

### Notifications
- PR comments for agent communication
- GitHub annotations (notice, warning, error)
- Label changes for visual status

### Data Processing
- JSON parsing with `jq`
- Node.js scripts for complex logic
- Shell scripts for simple operations

## Available Actions

### First-Party
- `actions/checkout@v4` — Repository checkout
- `actions/setup-node@v4` — Node.js setup
- `github/codeql-action` — Security scanning

### Third-Party Agent Actions
- `openai/codex-action@v1` — OpenAI Codex integration
- `google-labs-code/jules-action@v1` — Google Jules integration
- `qodo-ai/pr-agent@main` — Alternative PR review agent

## Limitations

### Rate Limits
- GitHub API: 5000 requests/hour (authenticated)
- OpenAI API: Varies by plan
- Google API: Varies by plan

### Permissions
- Agents cannot bypass branch protection
- Agents cannot approve their own PRs
- Agents cannot merge without human approval

### Scope
- Agents operate only within this repository
- Agents cannot access external systems
- Agents cannot modify repository settings

---

For agent guidelines and forbidden patterns, see [AGENTS.md](AGENTS.md).