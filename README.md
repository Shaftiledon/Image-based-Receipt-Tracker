# 🧾 AI-Powered Expense Tracker Agent

> **An automated workflow that monitors emails, extracts data from receipt images using Computer Vision (GPT-4o), and updates a financial database in real-time.**

---

## 🎥 Demo
[**Watch the System in Action (Loom Video)**](PASTE_YOUR_LOOM_LINK_HERE)

![Workflow Screenshot](Add_A_Screenshot_Of_Your_n8n_Workflow_Here.png)
*(Screenshot of the n8n automation flow)*

---

## 🔴 The Problem
Managing expenses manually is a bottleneck for businesses and individuals.
* **Time Loss:** Manually typing date, vendor, and total for every receipt takes hours per month.
* **Human Error:** It is easy to mistype a number or categorize an item incorrectly.
* **Lost Data:** Receipts often get buried in email inboxes and forgotten until tax season.

## 🟢 The Solution
I built an autonomous **AI Agent** that functions as a personal bookkeeper. It runs 24/7 on a self-hosted instance of n8n.

**How it works:**
1.  **Trigger:** The system monitors an inbox via IMAP for emails containing specific keywords ("receipt", "invoice", "expense").
2.  **Vision Analysis:** It passes email attachments (images/PDFs) to **OpenAI (GPT-4o)** with a strict system prompt to extract key data points.
3.  **Data Cleaning:** A custom **JavaScript** node parses the AI's response, handling structural inconsistencies (e.g., nested JSON, markdown formatting) to ensure 100% reliability.
4.  **Database Entry:** The clean structured data is authenticated via **Google Cloud OAuth2** and appended to a **Google Sheet**.

---

## 🛠️ Tech Stack
* **Orchestration:** [n8n](https://n8n.io/) (Self-Hosted)
* **AI & Vision:** OpenAI GPT-4o
* **Scripting:** JavaScript (Node.js for data transformation)
* **Database:** Google Sheets API
* **Auth:** Google Cloud Console (OAuth2)

---

## 🧠 Key Technical Challenges & Solutions

### 1. Handling Unpredictable AI Outputs
**Challenge:** The AI model would occasionally wrap the JSON output in Markdown code blocks (```json) or nest the data inside different object keys (`content` vs `output` vs `message`), causing the automation to break.

**Solution:** I wrote a custom **Universal Parsing Script** in the Function node. It acts as a robust middleware that:
* Recursively searches the input object for the data payload.
* Strips Markdown formatting using Regex.
* Validates the JSON structure before passing it to the database.

```javascript
// Example of the logic used
const cleanText = rawText.replace(/```json/g, '').replace(/```/g, '').trim();
return JSON.parse(cleanText);
