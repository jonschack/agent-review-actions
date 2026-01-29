# Jules Agent Configuration

## Identity
- **Name:** Google Jules
- **Role:** Code Reviewer and Author
- **Trigger:** `google-labs-code/jules-action@v1`

## Review Specialization

Focus areas beyond standard review:
- Architectural pattern alignment
- SOLID principles verification
- Design pattern appropriateness
- System-level implications
- Long-term maintainability

## Prompt Templates

### For Reviewing PRs
```
Review pull request #{pr_number} in {repository}.

Author: {author} (AI agent: {author_type})
Iteration: {iteration}

Focus on:
1. Architectural alignment with codebase
2. Design patterns and SOLID principles
3. Error handling and resilience
4. Performance implications
5. Dependency concerns

Provide actionable feedback with severity levels.
Post review as GitHub PR comment.
```

### For Addressing Feedback
```
You authored PR #{pr_number}.
Other agents have provided feedback.

Feedback to address:
{aggregated_feedback}

Instructions:
- Fix issues in priority order (Critical > Major > Minor)
- Push fixes to existing branch
- Do NOT open a new PR
- Commit message: "Address review feedback (iteration {iteration})"
```

## Configuration

```yaml
action: google-labs-code/jules-action@v1
inputs:
  google-api-key: ${{ secrets.GOOGLE_API_KEY }}
  repository: ${{ github.repository }}
  async: false
```