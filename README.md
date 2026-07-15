# AI Email Classifier & Auto-Responder (n8n + Ollama)

An n8n automation that watches a Gmail inbox, classifies every incoming email with a locally hosted LLM, logs it to Google Sheets, and prepares a draft reply — all running on a self-hosted server at zero API cost.

Built during the Digital Marketing course (B3E4500101) at Tokyo International University.

## What it does

1. **Gmail Trigger** — fires automatically whenever a new email arrives
2. **Code node** — cleans and prepares the email text for the AI
3. **Text Classifier (Ollama)** — sorts each email into **Inquiry** or **Complaint**
4. **Routing by category:**
   - Inquiries → logged to a Google Sheet and a reply **draft** is created in Gmail
   - Complaints → logged to a separate sheet tab and a notification message is sent

The AI never sends anything by itself — drafts wait for human review, which keeps a human in the loop.

## Tech stack

- **n8n** (self-hosted on a VPS with Docker + Caddy)
- **Ollama** running qwen2.5 locally — no OpenAI costs
- **Gmail API** (OAuth2) for triggers, drafts, and messages
- **Google Sheets API** (OAuth2) for logging

## Skills demonstrated

- Event-driven automation (email trigger instead of manual execution)
- LLM text classification with a small local model
- Human-in-the-loop design (AI drafts, human approves)
- OAuth2 credential setup across Google services
- Self-hosting n8n and Ollama on a memory-constrained VPS

## How to run

1. Import `email-assistant-basic.json` into an n8n instance (v1.60+)
2. Connect your own Gmail OAuth2 and Google Sheets OAuth2 credentials
3. Point the Ollama node at your Ollama server and pull a model, e.g. `ollama pull qwen2.5:1.5b`
4. Replace `YOUR_SPREADSHEET_ID` in the Sheets nodes with your own sheet
5. Activate the workflow — it runs automatically on new emails
