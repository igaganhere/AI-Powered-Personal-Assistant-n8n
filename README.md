# 🤖 Personal Assistant Bot — n8n AI Workflow

> A fully self-hosted, multi-modal AI personal assistant built on n8n, accessible via Telegram. Powered by Google Gemini, it manages your emails, contacts, calendar, and research — all through natural conversation, with both text and voice support.

---

## 🌐 Deployment

| Detail | Value |
|---|---|
| Platform | n8n (Self-Hosted) |
| Instance URL | **https://n8n.igaganhere.me/** |
| Access | Authenticated via custom credentials |
| Telegram Bot | **https://t.me/paigaganhere_bot** (Public) |

---

## 🧠 Core Architecture

```
Telegram (Trigger)
       │
       ├── Voice Input → OpenRouter Whisper → Text
       └── Text Input ──────────────────────► Main AI Agent (Google Gemini)
                                                      │
                          ┌───────────────────────────┼───────────────────────────┐
                          │                           │                           │
                   📧 Email Agent              📅 Calendar Tool           🔍 Research Agent
                   + Contacts Tool                                        (SERP + Wikipedia
                                                                           + Hacker News)
                                                      │
                                               ┌──────┴──────┐
                                         Text Output   Voice Output
                                                      ```
                                                      ---

## ⚙️ Workflow Components

### 🔁 Trigger
- **Telegram Bot** — Acts as the entry point for all user interaction. The bot is publicly accessible, meaning anyone can interact with the assistant via Telegram.

### 🧩 Input Modes

| Mode | Description |
|---|---|
| 💬 **Text** | User sends a text message directly through Telegram |
| 🎙️ **Voice** | User sends a voice message → converted to text via **OpenRouter's Whisper model** using the n8n Voice Transfer node |

### 🤖 Main AI Agent
- **Brain:** Google Gemini (Free Tier)
- **Memory:** Window Buffer Memory — retains recent conversation context for coherent, multi-turn interactions
- **Role:** Orchestrates all sub-agents and tools based on user intent

---

## 🛠️ Tools & Sub-Agents

### 1. 👤 Contacts Tool *(Sub-Agent)*
- Fetches and manages contacts via the **Google People API**
- Connected to Google Cloud Console via a custom **HTTPS node** in n8n
- Used by the Email Agent to auto-resolve recipient details

### 2. 📧 Email Agent *(Sub-Agent)*
- Dedicated sub-agent of the Main Agent
- Can **send emails** and **retrieve inbox messages**
- Works with saved contacts or directly with a provided email ID — no contact entry needed
- Powered by **Gmail API** through Google Cloud Console

### 3. 📅 Calendar Tool *(Sub-Agent)*
- Create and delete Google Calendar events on command
- Integrated via **Google Calendar API** through Google Cloud Console
- Directly usable from natural language (e.g., *"Schedule a meeting tomorrow at 3 PM"*)

### 4. 🔍 Research Agent *(Sub-Agent)*
- Dedicated sub-agent built for web research and information lookup
- Integrates three sources:
  - **SERP API** — Real-time web search results
  - **Wikipedia** — Encyclopedic knowledge
  - **Hacker News** — Tech news and discussions

---

## 📤 Output Modes

| Mode | How to Trigger |
|---|---|
| 💬 **Text Response** | Default — agent replies in text |
| 🔊 **Voice Response** | Tell the agent: *"Give me the output in voice"* — a separate voice node generates and sends an audio reply |

---

## 🔐 Authentication & APIs Used

| Service | Auth Method |
|---|---|
| Google Contacts (People API) | Google Cloud Console OAuth / HTTPS node |
| Gmail API | Google Cloud Console OAuth |
| Google Calendar API | Google Cloud Console OAuth |
| SERP API | API Key |
| OpenRouter (Whisper) | API Key via OpenRouter |
| n8n Instance | Custom credentials on self-hosted HTTPS domain |

---

## 🚀 How to Use

1. Open Telegram and search for **https://t.me/paigaganhere_bot**
2. Start a conversation — type or send a voice message
3. Ask anything, for example:
   - *"Send an email to john@example.com saying I'll be late"*
   - *"Create a calendar event for Friday at 5 PM called Team Sync"*
   - *"Research the latest developments in quantum computing"*
   - *"What emails did I receive today?"*
4. To receive a voice reply, simply say: *"Reply in voice"*

---

## 📁 Tech Stack Summary

| Layer | Technology |
|---|---|
| Workflow Automation | n8n (Self-Hosted) |
| AI Model | Google Gemini (Free Tier) |
| Memory | Window Buffer Memory (n8n) |
| Voice-to-Text | OpenRouter — Whisper Model |
| Messaging Interface | Telegram Bot API |
| Email | Gmail API (Google Cloud Console) |
| Contacts | Google People API (Google Cloud Console) |
| Calendar | Google Calendar API (Google Cloud Console) |
| Web Research | SERP API, Wikipedia, Hacker News |

---

## 📌 Notes

- This assistant is self-hosted on a private n8n instance at https://n8n.igaganhere.me/ with secure login.
- The Telegram bot is public — anyone with the bot link can interact with the assistant.
- All Google API integrations are configured through a personal Google Cloud Console project.
- The Whisper voice transcription is handled by OpenRouter's hosted model endpoint.

---


