# Copilot Studio Workshop

A hands-on workshop that takes you from the fundamentals of Microsoft Copilot Studio to advanced integrations - no prior bot-building experience required.

---

## Table of Contents

1. [What is Copilot Studio?](#what-is-copilot-studio)
2. [Architecture Overview](#architecture-overview)
3. [Common Use Cases](#common-use-cases)
4. [Prerequisites](#prerequisites)
5. [Exercises](#exercises)

---

## What is Copilot Studio?

**Microsoft Copilot Studio** is an end-to-end conversational AI product for building your own agent or extending Microsoft Copilot with generative AI, large language models and your data.

Copilot Studio combines:

- A **graphical conversation designer** for building topic flows with a drag-and-drop canvas.
- **Built-in Natural Language Understanding (NLU)** so the copilot can interpret what a user types in free-form text.
- **Generative AI capabilities** powered by Azure OpenAI, allowing the copilot to answer questions from documents, SharePoint sites and other knowledge sources automatically.
- **Deep integration with Microsoft 365 and Power Platform** (Power Automate, Dataverse, Teams, etc.).

---

## Architecture Overview

```
User (Teams / Web / Mobile)
        │
        ▼
  ┌─────────────────────────────────┐
  │        Copilot Studio           │
  │  ┌──────────┐  ┌─────────────┐  │
  │  │  Topics  │  │  Knowledge  │  │
  │  │  & Nodes │  │   Sources   │  │
  │  └────┬─────┘  └──────┬──────┘  │
  │       │               │         │
  │       ▼               ▼         │
  │  ┌─────────────────────────┐    │
  │  │   NLU / Generative AI   │    │
  │  │  (Azure OpenAI Service) │    │
  │  └────────────┬────────────┘    │
  └───────────────┼─────────────────┘
                  │
        ┌─────────▼──────────┐
        │   Power Automate   │
        │   (Cloud Flows)    │
        └─────────┬──────────┘
                  │
     ┌────────────▼────────────┐
     │  External Systems       │
     │  (APIs, Dataverse,      │
     │   SharePoint, ERP, etc.)│
     └─────────────────────────┘
```

### How a conversation flows

1. The user sends a message on any configured channel.
2. Copilot Studio's NLU engine matches the message to the best-fitting **topic** (or falls back to a generative answer from knowledge sources).
3. The topic executes its nodes in order - asking questions, evaluating conditions, storing values in variables.
4. If external data is needed, an **Action** node triggers a **Power Automate flow** which calls the target system and returns results.
5. The copilot sends the final response back to the user.

---

## Common Use Cases

- **IT Help Desk** - password resets, software requests, ticket creation in ServiceNow/Jira.
- **HR Self-Service** - answering policy questions, submitting leave requests, onboarding guides.
- **Customer Support** - FAQs, order tracking, appointment booking.
- **Internal Knowledge Base** - querying documents stored in SharePoint or OneDrive with generative AI.
- **Field Operations** - filling out forms and retrieving data while offline (via Teams mobile).

---

## Prerequisites

Before starting the exercises, make sure you have:

- [ ] A **Microsoft 365** account with access to [make.powerapps.com](https://make.powerapps.com) or [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com).
- [ ] A **Power Platform environment** where you have the *Environment Maker* role.
- [ ] A modern web browser (Edge or Chrome recommended).


---

## Exercises

| # | Title | Skills Practised |
|---|-------|-----------------|
| 1 | [Getting Started - Your First Copilot](exercises\exercise 1 - Onboarding\exercise-1-getting-started.md)| Creating a copilot, adding tools, skills, testing |
---

## Additional Resources

- [Microsoft Copilot Studio documentation](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)
- [Power Platform learning paths on Microsoft Learn](https://learn.microsoft.com/en-us/training/powerplatform/)
- [Copilot Studio community forums](https://powerusers.microsoft.com/t5/Microsoft-Copilot-Studio/ct-p/PVACommunity)
