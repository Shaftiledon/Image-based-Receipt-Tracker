# 🧾 AI-Powered Expense Tracker Agent

> **An automated workflow that monitors emails, extracts data from receipt images using Computer Vision (GPT-4o), and updates a financial database in real-time.**

---

## 🎥 Demo
[**Watch the System in Action (Loom Video)**](PASTE_YOUR_LOOM_LINK_HERE)

![Workflow Screenshot]<img width="1398" height="696" alt="Screenshot 2026-01-02 at 13 46 06" src="https://github.com/user-attachments/assets/68299c6d-7f7c-4e06-820e-4397471ff7db" />
e.png)
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

This is a great move. A README isn't just a description; it is your sales pitch to a potential employer or client. It explains **how you think** and **how you solve problems**.

Here is a professional, "Case Study" style template for your README. You can copy-paste this directly into GitHub and just fill in the bracketed info.

---

### **Copy & Paste This Template**

```markdown
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

```

### 2. Secure Authentication

**Challenge:** Connecting a self-hosted automation tool to Google Sheets securely.
**Solution:** Instead of using basic API keys, I set up a project in **Google Cloud Console**, enabled the Drive/Sheets APIs, and generated **OAuth2 Credentials** to ensure secure, scoped access to specific spreadsheets.

---

## 🚀 How to Use

1. Import the `workflow.json` file into your n8n instance.
2. Set up your credentials for:
* **OpenAI** (API Key)
* **Google Sheets** (OAuth2 Client ID/Secret)
* **IMAP** (Email Server Settings)


3. Update the `Sheet ID` in the Google Sheets node.
4. Activate the workflow!

---

## 👤 Author

**[Your Name]**

* [Portfolio Website](https://www.google.com/search?q=https://www.oshiafi-domain.win)
* [LinkedIn](https://www.google.com/search?q=Your_LinkedIn_URL)

```

---

### **Why this structure works:**
1.  **The "Hook" (Top Block):** A busy CEO or CTO can read the first 3 lines and know exactly what this is.
2.  **The Architecture (Solution):** By listing steps (Trigger -> Vision -> Cleaning), you prove you understand **system design**, not just copy-pasting code.
3.  **The "Key Technical Challenges" (Crucial):** This is the most important part. It shows you faced bugs (like the JSON errors we fixed) and wrote *code* to solve them. This separates "Prompt Engineers" from "Automation Engineers."

**Tip:** Take a screenshot of your colorful n8n workflow nodes and put it right under the "Demo" section. Visuals make GitHub repos pop!

```
