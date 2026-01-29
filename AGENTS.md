# Agent Configuration for Multi-Agent PR Review System

## Overview

This repository uses a multi-agent automated review system where three AI coding agents collaborate:
- **GitHub Copilot** — GitHub's native AI coding assistant
- **OpenAI Codex** — OpenAI's code-specialized AI agent
- **Google Jules** — Google's autonomous coding agent

Each agent can create PRs, review other agents' PRs, and address review feedback by pushing to the same branch.

## Project Context

This is a GitHub Actions-based orchestration system for multi-agent code review. The repository contains:
- Workflow files for coordinating agent reviews
- Helper scripts for aggregating and processing feedback
- Configuration files for each agent

## Shared Agent Guidelines

### When Reviewing PRs

#### Review Focus Areas
1. **Correctness:** Logic errors, edge cases, null handling, off-by-one errors
2. **Security:** Injection attacks, auth issues, secrets exposure, input validation
3. **Performance:** Time/space complexity, N+1 queries, memory leaks
4. **Maintainability:** Code clarity, DRY principles, documentation
5. **Testing:** Coverage gaps, assertion quality, edge case tests

#### Severity Levels
Use these indicators consistently across all agents:
- 🔴 **Critical:** Security vulnerabilities, data loss risks, production crashes
- ��� **Major:** Bugs, logic errors, missing error handling
- 🟡 **Minor:** Code style, naming, minor improvements
- 🔵 **Suggestion:** Nice-to-haves, alternative approaches

#### Review Output Format
For each issue found, provide:
```
**File**: path/to/file.ext  
**Line**: [line number]  
**Severity**: [🔴|🟠|🟡|🔵] [Critical|Major|Minor|Suggestion]  
**Issue**: [Clear description]  
**Suggestion**: [Specific fix]  
```

### When Addressing Review Feedback

1. **Parse all feedback** from other agents
2. **Prioritize by severity:**
   - 🔴 Critical: MUST fix immediately
   - 🟠 Major: Should fix before merge
   - 🟡 Minor: Fix if straightforward
   - 🔵 Suggestion: Consider, but optional
3. **Make targeted changes:** Only modify what's needed
4. **Push to the same branch:** Never create a new PR
5. **Use clear commit messages:** `Address review feedback (iteration N)`

### Collaboration Protocol

- Be constructive and specific in feedback
- Acknowledge what's done well
- Don't dismiss other agents' feedback without explanation
- Seek consensus on architectural decisions
- Escalate to humans when agents conflict

## Codex-Specific Instructions

**See [.github/agents/codex-agent.md](.github/agents/codex-agent.md) for detailed configuration.**

- Emphasize: API design and interface contracts, dependency security (CVEs), database query efficiency, async/await correctness, type safety, null checks.
- Address feedback minimally and document non-obvious fixes; always run available tests before committing.

## Jules-Specific Instructions

**See [.github/agents/jules-agent.md](.github/agents/jules-agent.md) for detailed configuration.**

- Emphasize: Architectural alignment, SOLID, design pattern appropriateness, module boundaries, maintainability.
- Prefer solutions aligned with repository patterns; document architecture-impacting changes.

## File Modification Rules

- Only modify files relevant to the review feedback
- Preserve existing formatting conventions
- Don't introduce new dependencies without justification
- Don't refactor unrelated code during feedback fixes

## Forbidden Patterns

- Hardcoded secrets or API keys
- Infinite loops without exit conditions
- Unvalidated user input in commands
- Force pushes to protected branches
- Skipping required status checks

## Testing Requirements

- Workflow changes should be tested with workflow_dispatch
- Scripts should have corresponding test files
- All new code paths should have test coverage

---

See [SKILLS.md](SKILLS.md) for details on agent and repository tooling skills.