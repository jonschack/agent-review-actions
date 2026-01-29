# Multi-Agent Orchestrator Configuration

## Overview

The orchestrator coordinates reviews between Copilot, Codex, and Jules.

## State Machine

```
CREATED → REVIEWING → AGGREGATING → ADDRESSING → RE-REVIEWING → COMPLETE/ESCALATED
```

## Labels for State Tracking

| Label                     | Meaning                       |
|---------------------------|-------------------------------|
| `review-iteration-N`      | Current review iteration      |
| `copilot-reviewed-iter-N` | Copilot completed review      |
| `codex-reviewed-iter-N`   | Codex completed review        |
| `jules-reviewed-iter-N`   | Jules completed review        |
| `addressing-feedback`     | Author fixing issues          |
| `needs-human-review`      | Escalated to human            |
| `ready-for-human-review`  | Consensus reached             |
| `agent-review-conflict`   | Agents disagree               |

## Configuration

```yaml
max_iterations: 3
review_delay_seconds: 30
parallel_reviews: 2
escalation_threshold: 3
```

## Workflow Triggers

- `pull_request: [opened, ready_for_review, synchronize]`
- `pull_request_review: [submitted]`
- `issue_comment: [created]` (for @mentions)

## Error Handling

- Agent timeout: Retry with backoff, continue with others
- Empty response: Treat as "no issues found"
- Rate limit: Add delays, reduce parallelism
- Conflict: Escalate to human review

---

**See [AGENTS.md](../../AGENTS.md) for agent guidelines and review standards. See [SKILLS.md](../../SKILLS.md) for skills and capabilities documentation.**