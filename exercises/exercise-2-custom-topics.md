# Exercise 2 — Custom Topics, Entities & Variables

**Difficulty:** 🟡 Medium  
**Estimated time:** 45 minutes  
**Goal:** Design a richer conversation flow that collects structured information from the user using entities and variables, then branches based on the user's answers.

---

## Learning Objectives

By the end of this exercise you will be able to:

- Create a multi-turn topic that asks the user a series of questions.
- Use built-in and custom **entities** to extract and validate information.
- Store responses in **variables** and reference them later in the conversation.
- Add **condition nodes** to branch the conversation based on variable values.
- Use **rich responses** (Adaptive Cards or quick-reply buttons) to improve the UX.

---

## Scenario

You will build a **"Tech Support Triage"** topic. When a user reports a technical problem, the copilot will:

1. Ask what type of issue the user has (hardware, software, or network).
2. Ask for the user's name.
3. Ask for the severity (low, medium, or high).
4. Display a customised summary and next-steps message based on the severity.

---

## Step 1 — Create the Topic

1. In Copilot Studio, go to **Topics** and click **+ New topic** > **From blank**.
2. Name the topic `Tech Support Triage`.
3. Add the following trigger phrases:
   - `I have a tech problem`
   - `Report an issue`
   - `Something is broken`
   - `IT support`
   - `Technical problem`

---

## Step 2 — Ask for the Issue Type (with Quick Replies)

1. Add a **Question** node (click **+** > **Ask a question**).
2. In the question text, type:

   ```
   What type of issue are you experiencing?
   ```

3. Under **Identify**, select **Multiple choice options**.
4. Add the following choices:
   - `Hardware`
   - `Software`
   - `Network`
5. In the **Save response as** field, rename the variable to `IssueType` (click the variable name to edit it).
6. Leave **Skip bot validation** unchecked so the copilot re-prompts if the user's input doesn't match a choice.

> **What's happening?** Copilot Studio creates a variable `Topic.IssueType` and stores the selected choice. The built-in multiple-choice entity restricts valid answers to only the three options.

---

## Step 3 — Ask for the User's Name

1. Add another **Question** node below the first.
2. Question text:

   ```
   What is your name?
   ```

3. Under **Identify**, select **Person name** (a built-in entity that extracts proper names from free text).
4. Save the response as `UserName`.

> **Tip:** If you cannot find the "Person name" entity, use **User's entire response** instead and save it as `UserName`.

---

## Step 4 — Ask for Severity (with an Entity)

1. Add another **Question** node.
2. Question text:

   ```
   How severe is the issue?
   ```

3. Under **Identify**, choose **Multiple choice options** again and add:
   - `Low — I can still work`
   - `Medium — My work is affected`
   - `High — I am completely blocked`
4. Save the response as `Severity`.

---

## Step 5 — Add a Condition Branch

Now you'll route the conversation differently depending on the severity.

1. Add a **Condition** node (click **+** > **Add a condition**).
2. Configure the first branch:
   - Variable: `Topic.Severity`
   - Operator: **is equal to**
   - Value: `High — I am completely blocked`
3. Copilot Studio automatically creates an **All other conditions** branch.

---

## Step 6 — Build the High-Severity Branch

Inside the **High severity** branch:

1. Add a **Message** node with:

   ```
   🚨 Hi {Topic.UserName}! We've flagged your {Topic.IssueType} issue as HIGH severity.
   
   A technician will contact you within 30 minutes.
   Please keep this reference number: #CAS-{system.currentTime}
   ```

   > To insert a variable, type `{` and select the variable from the pop-up, or use the **{x}** variable picker.

2. Add a second **Message** node:

   ```
   While you wait, you can also call our emergency line:
   📞 0800-WORKSHOP (available 24/7)
   ```

---

## Step 7 — Build the Default Branch

Inside the **All other conditions** branch:

1. Add a **Message** node:

   ```
   Thank you, {Topic.UserName}! Your {Topic.IssueType} issue has been logged.
   
   Severity: {Topic.Severity}
   
   A support agent will follow up with you within 4 business hours.
   You can track your ticket at: https://support.example.com
   ```

---

## Step 8 — End the Conversation

After both branches, add an **End conversation** node (click **+** > **End the conversation**) so the topic closes cleanly.

---

## Step 9 — Test the Flow

1. Open the **Test your copilot** panel.
2. Type `I have a tech problem`.
3. When asked for issue type, click (or type) **Software**.
4. Enter your name.
5. Select **High — I am completely blocked** and verify that the urgent response appears.
6. Reset the conversation (click the broom icon 🧹) and repeat with a lower severity to verify the default branch.

> **Expected result:** High-severity path shows the emergency message; all other paths show the standard follow-up message.

---

## Bonus Challenge 🏆

- Add a **third condition branch** specifically for `Medium` severity with a distinct message (e.g. 2-hour response time).
- Create a **custom entity** called `Department` with values like `HR`, `Finance`, `Engineering`, and add a question that uses it.
- Store all collected values in **global variables** (prefix `Global.`) so they persist across topics.

---

## ✅ Exercise Checklist

- [ ] **Tech Support Triage** topic created with at least 5 trigger phrases.
- [ ] Question node uses multiple-choice options for issue type.
- [ ] User's name is captured using the **Person name** entity (or entire response).
- [ ] Severity question uses multiple-choice options.
- [ ] Condition node branches on **High** severity vs all other values.
- [ ] Both branches display a message referencing the `UserName` and `IssueType` variables.
- [ ] Test chat correctly follows both conversation paths.

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Variable picker doesn't show my variable | Make sure you saved the topic; variables from earlier nodes only appear after saving. |
| Condition branch is never triggered | Check that the condition value exactly matches one of the multiple-choice options (case-sensitive). |
| Copilot ignores trigger phrases and opens a different topic | Add more varied trigger phrases; avoid very short or common words that conflict with system topics. |

---

⬅️ **Previous exercise:** [Exercise 1 — Getting Started](exercise-1-getting-started.md)  
➡️ **Next exercise:** [Exercise 3 — Advanced Integrations with Power Automate](exercise-3-advanced-integrations.md)
