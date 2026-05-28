# Exercise 1 — Getting Started: Your First Copilot

**Difficulty:** 🟢 Easy  
**Estimated time:** 30 minutes  
**Goal:** Create a copilot from scratch, add a custom welcome message and a simple FAQ topic, then test the conversation in the built-in test canvas.

---

## Learning Objectives

By the end of this exercise you will be able to:

- Navigate the Copilot Studio interface.
- Create a new copilot and configure basic settings.
- Edit the default greeting topic.
- Create a new topic with trigger phrases and message nodes.
- Test a copilot using the built-in test canvas.

---

## Step 1 — Sign in to Copilot Studio

1. Open your browser and go to [https://copilotstudio.microsoft.com](https://copilotstudio.microsoft.com).
2. Sign in with your Microsoft 365 work or school account.
3. If prompted, select the **Power Platform environment** you want to use from the environment picker in the top-right corner.

> **Tip:** If you do not see an environment, ask your administrator to assign you the *Environment Maker* role, or use the default environment.

---

## Step 2 — Create a New Copilot

1. On the Copilot Studio home page, click **+ Create a copilot** (or **New copilot** depending on your version).
2. Fill in the details:
   - **Name:** `Workshop Helper`
   - **Language:** English (United States)
   - Leave all other settings as default.
3. Click **Create**.  
   Copilot Studio will provision the copilot — this usually takes less than a minute.

---

## Step 3 — Edit the Greeting Topic

The copilot ships with a built-in **Greeting** topic that fires when a user first opens the chat.

1. In the left navigation, click **Topics**.
2. Locate the **Greeting** topic under *System topics* and click on it.
3. The conversation canvas opens. You will see a **Message** node with default text.
4. Click inside the message text box and replace the default text with:

   ```
   Hello! 👋 Welcome to the Copilot Studio Workshop.
   I'm Workshop Helper. How can I assist you today?
   ```

5. Click **Save** (top-right corner).

---

## Step 4 — Create a New FAQ Topic

1. Click **Topics** in the left navigation, then click **+ New topic** > **From blank**.
2. In the **Name** field at the top, type `Workshop FAQ`.
3. In the **Trigger phrases** panel on the left, add the following phrases one by one (press **Enter** or click **+ Add** after each):
   - `What is Copilot Studio?`
   - `Tell me about Copilot Studio`
   - `What can this copilot do?`
   - `Help`
4. On the canvas, click the **+** icon below the Trigger node to add a new node. Select **Send a message**.
5. Type the following in the message box:

   ```
   Copilot Studio is Microsoft's low-code platform for building AI-powered
   conversational agents. In this workshop you'll learn how to:
   ✅ Create topics and conversation flows
   ✅ Use entities and variables
   ✅ Integrate with Power Automate and external APIs
   
   Feel free to ask me anything!
   ```

6. Click **Save**.

---

## Step 5 — Test Your Copilot

1. Click **Test your copilot** in the bottom-left corner of the screen to open the test chat panel.
2. Type `Hello` and press **Enter**. You should see your customised greeting.
3. Type `What is Copilot Studio?` and press **Enter**. You should see the FAQ response you just created.
4. Try a phrase variant such as `Help` or `Tell me about Copilot Studio` — the NLU engine should still trigger the correct topic.

> **Expected result:** The copilot responds correctly to all tested phrases.

---

## Step 6 — Publish Your Copilot (Optional)

1. Click **Publish** in the left navigation.
2. Click the **Publish** button and confirm the dialog.
3. Once published, your copilot is available for further channel configuration (e.g. adding it to a Teams chat).

> Publishing is optional for this exercise, but it is required before configuring external channels.

---

## ✅ Exercise Checklist

- [ ] Copilot named **Workshop Helper** created successfully.
- [ ] Greeting message updated with custom welcome text.
- [ ] **Workshop FAQ** topic created with at least 4 trigger phrases.
- [ ] FAQ message node displays a multi-line response.
- [ ] Test chat correctly triggers both the greeting and the FAQ topic.

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Copilot creation is stuck or fails | Refresh the page and try again; check that your environment has available capacity. |
| Test chat doesn't trigger your topic | Ensure you saved the topic and that trigger phrases are meaningful and varied. |
| "Couldn't reach the server" error | Check your internet connection and that your account has the correct licence. |

---

➡️ **Next exercise:** [Exercise 2 — Custom Topics, Entities & Variables](exercise-2-custom-topics.md)
