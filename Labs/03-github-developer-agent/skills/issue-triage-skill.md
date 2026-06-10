---
name: issue-triage-skill
description: Use this skill when the user asks to triage, classify, prioritize, label, assign, compare, or recommend next actions for GitHub issues.
---
Use this skill when the user asks questions such as:

- "Triage these open issues."
- "Which bug should we handle first?"
- "Suggest labels and owners for these issues."
- "Classify issue #18."

When this skill is activated:

1. Review the selected issue or set of issues using GitHub tool data.
2. Classify each issue and recommend practical triage actions.

## Required output

For each issue, include:

- **Issue**: title, number, repository, author, and current state.
- **Category**: bug, feature request, documentation, support, question, or task.
- **Priority suggestion**: high, medium, or low, with a short reason.
- **Suggested owner**: person or team if there is enough evidence.
- **Suggested labels**: labels that would help route or track the issue.
- **Next action**: one concrete action, such as request logs, assign an owner, reproduce the bug, or link to an existing issue.

## Guidelines

- Do not close, assign, label, or comment on issues without explicit user approval.
- If multiple issues appear related, mention possible duplicates but do not mark them as duplicates automatically.
- If the issue lacks enough information, recommend the missing details to request.
- Keep recommendations short and developer-focused.

## Examples

**Example request:** "Find open bug issues and suggest which one should be handled first."

**Expected behavior:** The agent reviews the issue list, classifies likely bugs, explains which appears most urgent, and asks for approval before applying labels, assignments, or comments.
