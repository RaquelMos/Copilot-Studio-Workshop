# Exercise 3 — Advanced Integrations with Power Automate

**Difficulty:** 🔴 Hard  
**Estimated time:** 60–75 minutes  
**Goal:** Connect your copilot to an external data source using Power Automate, call a public REST API, and enable generative AI answers from a knowledge source.

---

## Learning Objectives

By the end of this exercise you will be able to:

- Call a **Power Automate cloud flow** from a Copilot Studio topic using an Action node.
- Pass input variables from the copilot to a flow, and receive output variables back.
- Consume a **public REST API** (OpenWeatherMap) from within a cloud flow.
- Surface the API result dynamically in the copilot conversation.
- Add a **knowledge source** (SharePoint site or uploaded document) and enable generative AI answers.

---

## Prerequisites

- Completed [Exercise 1](exercise-1-getting-started.md) and [Exercise 2](exercise-2-custom-topics.md).
- A free **OpenWeatherMap** API key (sign up at [https://openweathermap.org/api](https://openweathermap.org/api) — the free tier is sufficient).  
  Alternatively, your trainer may provide a shared API key for the workshop.
- (Optional — Part B) Access to a SharePoint site with at least one document.

---

## Part A — Live Weather via Power Automate

### Step 1 — Create the Power Automate Flow

1. Open [https://make.powerautomate.com](https://make.powerautomate.com) in a new browser tab.
2. Ensure you are in the **same environment** as your Copilot Studio copilot.
3. Click **+ Create** > **Instant cloud flow**.
4. Name the flow `Get Weather for City`.
5. Under **Choose how to trigger this flow**, select **PowerApps (V2)** and click **Create**.

#### Add an Input Parameter

6. In the trigger card, click **+ Add an input** > **Text**.
7. Name the input `City`.

#### Call the OpenWeatherMap API

8. Click **+ New step** and search for **HTTP**.
9. Select the **HTTP** action (under the *HTTP* connector — not *HTTP with Azure AD*).
10. Configure the action:
    - **Method:** `GET`
    - **URI:**
      ```
      https://api.openweathermap.org/data/2.5/weather?q=@{triggerBody()['text_City']}&appid=YOUR_API_KEY&units=metric
      ```
      Replace `YOUR_API_KEY` with your OpenWeatherMap API key.
    - Leave all other fields empty.

#### Parse the JSON Response

11. Click **+ New step** > search for **Parse JSON**.
12. Configure:
    - **Content:** `Body` (from the HTTP step — use the dynamic content picker).
    - **Schema:** Click **Generate from sample** and paste this sample JSON response:
      ```json
      {
        "name": "London",
        "main": {
          "temp": 18.5,
          "humidity": 72
        },
        "weather": [
          {
            "description": "light rain"
          }
        ]
      }
      ```
    - Click **Done**.

#### Return Values to the Copilot

13. Click **+ New step** > search for **Return value(s) to PowerApps**.  
    *(If you cannot find it, search for "Respond to a PowerApp or flow".)*
14. Add the following output parameters using **+ Add an output** > **Text** for each:
    - Name `CityName`, value: `name` (from Parse JSON dynamic content).
    - Name `Temperature`, value: `temp` (from Parse JSON > main > temp).
    - Name `Humidity`, value: `humidity` (from Parse JSON > main > humidity).
    - Name `Description`, value: `description` (from Parse JSON > weather > description).
15. Click **Save** and close the Power Automate tab.

---

### Step 2 — Create the Weather Topic in Copilot Studio

1. Switch back to Copilot Studio and go to **Topics** > **+ New topic** > **From blank**.
2. Name the topic `Weather Check`.
3. Add trigger phrases:
   - `What's the weather?`
   - `Weather forecast`
   - `Is it raining?`
   - `Tell me the weather in`
   - `Current temperature`

---

### Step 3 — Ask for the City

1. Add a **Question** node.
2. Question text:

   ```
   Which city would you like the weather for?
   ```

3. Under **Identify**, select **City** (built-in geography entity).  
   If it doesn't appear, select **User's entire response**.
4. Save the response as `CityInput`.

---

### Step 4 — Call the Power Automate Flow

1. Add an **Action** node (click **+** > **Call an action** > **Create a flow** if you haven't already, or choose **Call an action** and select your `Get Weather for City` flow).
2. Map the input:
   - Flow input `City` → Copilot variable `Topic.CityInput`
3. The node will expose output variables. Rename them if needed:
   - `CityName`, `Temperature`, `Humidity`, `Description`

---

### Step 5 — Display the Weather Result

1. Add a **Message** node after the Action node:

   ```
   Here is the current weather for {Topic.CityName}:
   
   🌡️ Temperature: {Topic.Temperature}°C
   💧 Humidity: {Topic.Humidity}%
   🌤️ Conditions: {Topic.Description}
   ```

2. Add an **End conversation** node.
3. Click **Save**.

---

### Step 6 — Test the Integration

1. Open the test chat panel.
2. Type `What's the weather?`.
3. Enter a city name (e.g. `Lisbon` or `London`).
4. Verify that the copilot returns live weather data.

> **Expected result:** The copilot displays temperature, humidity and conditions retrieved in real time from the OpenWeatherMap API.

> **Note:** The first call may take a few seconds because Power Automate flows have a cold-start delay in the free tier.

---

## Part B — Generative AI from a Knowledge Source

In this part, you will add a document or SharePoint site as a knowledge source so the copilot can answer questions it wasn't explicitly programmed to handle.

### Step 7 — Add a Knowledge Source

#### Option A — Upload a Document

1. In Copilot Studio, go to **Knowledge** in the left navigation.
2. Click **+ Add knowledge** > **Files**.
3. Upload any PDF or Word document relevant to your use case (e.g. a company FAQ, product brochure, or the workshop theory notes from this repository's README).
4. Wait for the document to finish indexing (a green tick appears when ready).

#### Option B — Connect a SharePoint Site

1. Click **+ Add knowledge** > **SharePoint**.
2. Enter the URL of your SharePoint site (e.g. `https://contoso.sharepoint.com/sites/HR`).
3. Click **Add** and wait for indexing to complete.

---

### Step 8 — Enable Generative Answers

1. Go to **Settings** (gear icon) > **Generative AI**.
2. Make sure **Allow the copilot to use knowledge sources** is toggled **On**.
3. Optionally, enable **Generative mode** under **How should your copilot decide how to respond?** — this lets the copilot answer from knowledge sources even when no topic matches.

---

### Step 9 — Test Generative Answers

1. Open the test chat panel.
2. Ask a question that can be answered from your uploaded document (e.g. if you uploaded a company policy PDF, ask `What is the remote work policy?`).
3. Verify that the copilot provides a grounded answer citing the document, rather than an "I don't know" fallback.

> **Expected result:** The copilot answers questions from the knowledge source with relevant citations.

---

## Bonus Challenges 🏆

- **Error handling:** In the Weather topic, add a **Condition** node that checks whether `Topic.Temperature` is empty (which happens when the city is not found) and displays a friendly error message.
- **Adaptive Card:** Replace the plain text weather message with an Adaptive Card that includes an icon and styled layout. Use [https://adaptivecards.io/designer/](https://adaptivecards.io/designer/) to design it.
- **Authentication:** Restrict the copilot to authenticated users only by enabling **Azure AD authentication** under *Settings > Security > Authentication*.
- **Teams deployment:** Publish the copilot to Microsoft Teams and test it from the Teams client.

---

## ✅ Exercise Checklist

**Part A — Power Automate Integration**
- [ ] `Get Weather for City` cloud flow created and saved.
- [ ] HTTP action calls the OpenWeatherMap API with the city as a query parameter.
- [ ] Parse JSON action extracts temperature, humidity and description.
- [ ] Flow returns at least three output variables to the copilot.
- [ ] `Weather Check` topic created with at least 5 trigger phrases.
- [ ] Question node captures the city name.
- [ ] Action node calls the flow and maps input/output variables.
- [ ] Message node displays the live weather data.
- [ ] Test chat returns real weather data for at least two different cities.

**Part B — Knowledge Source**
- [ ] At least one knowledge source (document or SharePoint) added and indexed.
- [ ] Generative answers enabled in Settings.
- [ ] Test chat answers a question from the knowledge source with a grounded response.

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| HTTP action returns a 401 error | Check that your OpenWeatherMap API key is correct and active (activation can take up to 2 hours on a new free account). |
| Flow outputs are empty in the copilot | Ensure the **Return value(s) to PowerApps** step names exactly match what the copilot expects; check for typos. |
| Action node is greyed out in the topic | Make sure both the flow and the topic are in the same Power Platform environment. |
| Generative answers toggle is missing | Your organization may have disabled generative AI features; ask your Power Platform administrator. |
| Knowledge source shows "Failed" status | The document format may not be supported. Stick to PDF, Word (.docx) or plain text files under 512 MB. |

---

⬅️ **Previous exercise:** [Exercise 2 — Custom Topics, Entities & Variables](exercise-2-custom-topics.md)  
🏠 **Back to workshop overview:** [README](../README.md)
