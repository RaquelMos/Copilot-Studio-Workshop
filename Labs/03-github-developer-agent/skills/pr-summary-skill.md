---
name: pr-summary-skill
description: Use this skill when the user asks to summarize, review, explain, inspect, or identify what still needs attention in a GitHub pull request or PR.
---
Use this skill when the user asks questions such as:

- "Summarize PR #12."
- "Tell me what still needs attention in this pull request."
- "Review this PR and call out blockers."
- "What changed in this PR?"

When this skill is activated:

1. Summarize the selected pull request using only information available from GitHub tools and the current conversation.
2. Help the user quickly understand what changed, what still needs attention, and what the next action should be.

## Required output

Include these sections when the data is available:

- **PR**: title, number, repository, author, and current state.
- **Purpose**: short summary of what the PR is trying to accomplish.
- **Changes**: main files, components, or areas touched.
- **Review status**: reviewers, approvals, requested changes, and unresolved comments.
- **Checks**: passing, failing, pending, or missing CI checks.
- **Risk areas**: code paths, dependencies, migrations, permissions, or release-sensitive changes that may need extra review.
- **Suggested next action**: one concise recommendation.

## Guidelines

- Do not invent implementation details, reviewers, checks, or test results.
- If data is unavailable, say what could not be verified.
- Separate facts from recommendations.
- Keep the summary useful for a developer who has not opened the PR yet.

## Examples

**Example request:** "Summarize PR #12 and tell me what still needs attention."

**Expected behavior:** The agent retrieves PR details, summarizes the change, calls out review or CI blockers, and recommends the next action without creating or updating anything in GitHub.
