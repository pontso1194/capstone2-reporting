# 🤖 AI-Powered Weekly Business Report Generation (n8n & Gemini)

This project demonstrates a robust, scheduled automation built using n8n to connect business metrics and leverage AI (Google Gemini) for automatic report generation, ensuring stable delivery via email.

---

## 1. Project Overview & Use-Case

### 💡 Identified Business Problem & AI Augmentation

| Property | Description |
| :--- | :--- |
| **Business Problem** | Manual process of collecting metrics, analyzing trends, and writing weekly narrative reports—a process that is slow and error-prone. |
| **AI Augmentation** | The AI (Gemini) takes raw, structured metrics, performs instant analysis (identifies trends, peaks), and **generates a complete, narrative report draft** directly in **HTML format**. |
| **Tech Stack** | **n8n** (Orchestration), **Google Gemini** (AI), **JavaScript** (Data Prep), **Google Sheets** (Data Source), **Email/SMTP** (Delivery). |

---

## 2. Workflow Concept & Data Flow

The workflow is a scheduled, linear process designed to convert raw metrics into a professional, HTML-formatted report.

| Step | Component | Action/Data Flow |
| :--- | :--- | :--- |
| **1. Trigger** ⏰ | **Schedule Node** | Initiates the workflow weekly at a set time. |
| **2. Data Pull** 🗄️ | **Data Source Node** | Retrieves structured performance metrics (Sales, Traffic). |
| **3. Data Prep** 📝 | **Code Node** | Aggregates the metrics into a single, clean text/JSON block for the AI prompt. |
| **4. AI Logic** 🧠 | **Google Gemini Node** | Analyzes the data and generates a full report draft in **HTML**. |
| **5. Validation** ❓ | **IF Node** | Checks if the AI generated any content before sending the email. |
| **6. Output** 📧 | **Email Node** | Sends the finalized HTML report to stakeholders. |

---

## 3. Core Implementation Details

### 🧠 AI Prompt & Logic

The core of the project is the Gemini prompt, engineered to produce reliable, formatted output:

1.  **Direct HTML Output:** The prompt explicitly mandates **HTML formatting** to bypass issues with Markdown rendering in email clients.
2.  **Persona:** The AI is instructed to act as an "Expert Business Analyst" to ensure a professional tone.

```markdown
# AI Prompt Key Instruction
"...The report must be formatted using clean, standard HTML for direct email embedding. Do not use Markdown syntax. Use appropriate tags like <h1>, <h2>, and <table>."

🛡️ Stability and Validation
The workflow is designed for robustness:NodeFunctionRationale
**IF Node ❓** Checks if $json.text (AI Output) is not empty.Prevents blank emails from being sent to executives.
**Fallback Node 🚨** Sends an immediate Slack/Email alert on the False path.Ensures the team is notified instantly if the automation fails, enabling quick manual intervention.
**Node Retries** Configured on the Data Source, Gemini, and Email Nodes.Handles transient failures (network errors, rate limits) without stopping the workflow.

Getting Started
Download the Blueprint: Download the AI-Powered-Report-Generation.json file from this repository.

Import: Import the JSON file directly into your self-hosted or cloud n8n instance.

Credentials: Update the credentials for the Data Source Node, Google Gemini Node, and the Email Node with your specific API keys and accounts.

Run: Manually execute the workflow once to confirm all connections are working before letting the Schedule Node take over.
