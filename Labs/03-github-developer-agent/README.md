# Exercise 3 - GitHub Developer Agent

**Goal:** Build a Copilot Studio agent connected to GitHub that can answer questions about repositories, pull requests, and issues using GitHub connector tools and developer-focused skills.

---

## Scenario

You work at **Contoso's engineering team**, where developers often need quick answers about open pull requests, active issues, blockers, and recent repository activity. Instead of switching between GitHub tabs, Teams messages, and project boards, the team wants a developer assistant that can inspect GitHub and help with routine actions.

You will build a **GitHub Developer Agent** that:

1. Connects to GitHub and answers questions about repositories, pull requests, issues, branches, commits, and review status.
2. Summarizes PRs and issues so developers can quickly understand changes, blockers, owners, and next steps.
3. Uses tools and skills to retrieve GitHub data and produce useful developer summaries.
4. Keeps write actions out of scope for the workshop, while showing how they could be added later with approvals and workflows.

By the end of the exercise you will have a GitHub-connected developer assistant that can inspect engineering work and help teams act faster without leaving Copilot Studio.

---

## Step 1 - Sign in to Copilot Studio
1. Open your browser and go to [https://copilotstudio.microsoft.com](https://copilotstudio.microsoft.com).
2. Sign in with your Microsoft 365 work or school account.
3. You should see something similar to the below image:

![Copilot Studio main screen](../images/main-screen.png)

---

## Step 2 - Create the GitHub Developer Agent

1. On the Copilot Studio home page, click **Agent**.
2. Set:
   - **Name:** `GitHub Developer Agent`
   - **Instructions:**
      ```text
      You are Contoso's GitHub developer assistant.

      Your job is to help developers understand and act on GitHub repository work. You can answer questions about:
      - Pull requests
      - Issues
      - Branches
      - Commits
      - Review status
      - Labels, assignees, milestones, and blockers

      Skill routing rules:
      - If the user asks to summarize, review, explain, or identify what still needs attention in a pull request, use the PR Summary Skill.
      - If the user asks to classify, prioritize, label, assign, or triage issues, use the Issue Triage Skill.
      - Always fetch the relevant GitHub data with tools before using a skill. Skills format and reason over the tool results; they do not replace tool calls.

      When answering questions:
      - Use GitHub data from the connected tools.
      - Be concise and structured.
      - Include repository, PR, issue, or branch names when relevant.
      - Clearly separate facts from recommendations.
      - If you cannot access the requested repository or item, say so clearly.

      This workshop is read-only. Do not create, update, comment, label, assign, close, merge, or delete GitHub items in this lab.
      If the user asks for a write action, explain that write actions are out of scope for the workshop and can be implemented later with GitHub connector actions or agent flows plus approval gates.
      ```
   - **Model**: choose whichever model you prefer.
---

## Step 3 - Connect GitHub Tools

1. In the **Tools** section, click on the symbol **+**.
2. Add the GitHub connector actions below:
   - Get a pull request
   - Find issues by state and keyword
3. Complete GitHub sign-in if prompted.
4. Confirm the tools appear under Tools.

---

## Step 4 - Add Developer Skills

Create or configure skills that help the agent package GitHub data into useful developer outputs.

1. Go to **Skills** on the right side, and click on the **+** symbol.
2. Drag the skill files from `Labs/03-github-developer-agent/skills` into the skill window.
3. Add these skills:
   - **PR Summary Skill**: `skills/pr-summary-skill.md` summarizes purpose, changed files, risk areas, test notes, reviewers, and open comments.
   - **Issue Triage Skill**: `skills/issue-triage-skill.md` classifies issues by bug, feature request, documentation, support, or question; suggests priority and owner.
4. Return to **Instructions** and confirm the skill routing rules from Step 2 are included.
5. Publish the agent after adding the skills.

---

## Step 5 - Test and Validate

1. Open the preview canvas for **GitHub Developer Agent**.
2. Ask repository questions, for example:
   - `What pull requests are open in the RaquelMos/Copilot-Studio-Workshop repo?`
   - `Which issues are assigned to me?`
3. Test issue triage, for example:
   - `Find open bug issues and suggest which one should be handled first.`

Validation checklist:
- The agent can answer questions about PRs, issues, and repository status.
- The agent uses GitHub tool data instead of inventing repository details.
- Developer skills produce structured summaries and recommendations.

---

## Next steps - out of scope for this workshop

This lab focuses on reading GitHub data and producing useful developer summaries. You could enrich this use case later by adding the capability to create and update issues or pull requests.

Possible next steps:

- **Update issues and pull requests via workflows**: Copilot Studio can call agent flows as tools. Those flows can wrap GitHub update actions with validation, approval, logging, and company-specific guardrails.
- **Create issues directly**: the GitHub connector includes a **Create an issue** action for creating issues in a specific repository.
- **Create pull requests directly**: the GitHub connector includes a **Create a pull request** action for opening a pull request from a source branch into a target branch.
- **Request reviewers or manage review workflow**: GitHub actions can request reviewers for a pull request, which could be exposed as an approval-gated developer command.
- **React to GitHub events**: GitHub triggers such as new or updated pull requests and assigned issues can start workflows that notify teams, summarize changes, or prepare triage suggestions.

These actions are not included in this workshop because write operations require extra setup, permissions, and governance decisions. For a safe demo environment, we keep this lab focused on read-only GitHub inspection, summaries, and recommendations.

---

## What have we learned

In this exercise you have:

- Created a GitHub-connected developer assistant in Copilot Studio.
- Added tools to inspect repositories, pull requests, issues, and review state.
- Added developer-focused skills for PR summaries, issue triage.
