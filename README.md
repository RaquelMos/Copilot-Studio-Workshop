# Copilot Studio Workshop

A hands-on workshop that takes you from the fundamentals of Microsoft Copilot Studio to advanced integrations — no prior bot-building experience required.

---

## Table of Contents

1. [What is Copilot Studio?](#what-is-copilot-studio)
2. [Key Concepts](#key-concepts)
3. [Architecture Overview](#architecture-overview)
4. [Common Use Cases](#common-use-cases)
5. [Prerequisites](#prerequisites)
6. [Exercises](#exercises)

---

## What is Copilot Studio?

**Microsoft Copilot Studio** (formerly Power Virtual Agents) is a low-code/no-code platform that lets organizations build, test and publish AI-powered conversational agents — called *copilots* — without writing a single line of back-end code.

Copilot Studio combines:

- A **graphical conversation designer** for building topic flows with a drag-and-drop canvas.
- **Built-in Natural Language Understanding (NLU)** so the copilot can interpret what a user types in free-form text.
- **Generative AI capabilities** powered by Azure OpenAI, allowing the copilot to answer questions from documents, SharePoint sites and other knowledge sources automatically.
- **Deep integration with Microsoft 365 and Power Platform** (Power Automate, Dataverse, Teams, etc.).

---

## Key Concepts

| Term | Description |
|------|-------------|
| **Copilot** | The conversational agent you build and publish. Previously called a "bot". |
| **Topic** | A self-contained conversation thread triggered by specific user phrases or intents. |
| **Trigger Phrases** | Example sentences that teach the NLU when to activate a topic (e.g. *"What are your opening hours?"*). |
| **Node** | A single step inside a topic — can be a message, a question, a condition branch, an action call, etc. |
| **Entity** | A reusable piece of information the copilot can extract from user input (e.g. a date, a product name, a city). |
| **Action** | A call to an external system, typically a Power Automate cloud flow, an HTTP connector, or an AI Builder model. |
| **Variable** | A named slot that stores a value during a conversation (topic-scoped or globally scoped). |
| **Knowledge Source** | A document, website, SharePoint library, or Dataverse table the copilot can query for generative answers. |
| **Channel** | The surface where the copilot is published — Teams, a website widget, Slack, SMS, etc. |
| **Environment** | A Power Platform container that groups copilots, flows, and data together for a specific purpose or team. |

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
3. The topic executes its nodes in order — asking questions, evaluating conditions, storing values in variables.
4. If external data is needed, an **Action** node triggers a **Power Automate flow** which calls the target system and returns results.
5. The copilot sends the final response back to the user.

---

## Common Use Cases

- **IT Help Desk** — password resets, software requests, ticket creation in ServiceNow/Jira.
- **HR Self-Service** — answering policy questions, submitting leave requests, onboarding guides.
- **Customer Support** — FAQs, order tracking, appointment booking.
- **Internal Knowledge Base** — querying documents stored in SharePoint or OneDrive with generative AI.
- **Field Operations** — filling out forms and retrieving data while offline (via Teams mobile).

---

## Prerequisites

Before starting the exercises, make sure you have:

- [ ] A **Microsoft 365** account with access to [make.powerapps.com](https://make.powerapps.com) or [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com).
- [ ] A **Power Platform environment** where you have the *Environment Maker* role.
- [ ] A modern web browser (Edge or Chrome recommended).
- [ ] (Optional — Exercise 3 only) A free account on any public REST API such as [OpenWeatherMap](https://openweathermap.org/api) or access to a SharePoint site.

---

## Exercises

The exercises below are ordered from **beginner to advanced**. Complete them in sequence for the best learning experience.

| # | Title | Difficulty | Skills Practised |
|---|-------|-----------|-----------------|
| 1 | [Getting Started — Your First Copilot](exercises/exercise-1-getting-started.md) | 🟢 Easy | Creating a copilot, adding topics, testing |
| 2 | [Custom Topics, Entities & Variables](exercises/exercise-2-custom-topics.md) | 🟡 Medium | Conversation design, entities, conditions, variables |
| 3 | [Advanced Integrations with Power Automate](exercises/exercise-3-advanced-integrations.md) | 🔴 Hard | Power Automate flows, HTTP connectors, knowledge sources |

---

## Additional Resources

- [Microsoft Copilot Studio documentation](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)
- [Power Platform learning paths on Microsoft Learn](https://learn.microsoft.com/en-us/training/powerplatform/)
- [Copilot Studio community forums](https://powerusers.microsoft.com/t5/Microsoft-Copilot-Studio/ct-p/PVACommunity)
