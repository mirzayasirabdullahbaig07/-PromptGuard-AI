# 🛡️ PromptGuard — AI Prompt Security Platform

> Real-time AI prompt threat detection powered by RAG, Groq, and llama-3.3-70b-versatile.

![PromptGuard](https://img.shields.io/badge/Model-llama--3.3--70b--versatile-red?style=flat-square)
![Groq](https://img.shields.io/badge/Inference-Groq-orange?style=flat-square)
![Embeddings](https://img.shields.io/badge/Embeddings-nomic--embed--text--v1__5-blue?style=flat-square)
![Deployment](https://img.shields.io/badge/Deploy-Netlify-00AD9F?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## 📌 Overview

**PromptGuard** is a single-file AI security platform that scans user prompts in real-time and classifies them as **SAFE**, **SUSPICIOUS**, or **DANGEROUS**. It uses Retrieval-Augmented Generation (RAG) to ground every verdict in your own security policy — uploading your rules once lets the system cite the exact policy clause violated in each scan.

Built entirely in vanilla HTML/CSS/JS with zero dependencies, it deploys to Netlify in under 60 seconds.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔍 **Real-time Prompt Scanning** | Classifies any prompt instantly with threat type, severity, and confidence |
| 📚 **RAG-powered Policy Grounding** | Embeds your security policy and retrieves relevant chunks via cosine similarity |
| 🤖 **llama-3.3-70b-versatile** | State-of-the-art LLM analysis running on Groq's ultra-fast inference API |
| 🧮 **768-dim Vector Embeddings** | Uses `nomic-embed-text-v1_5` for high-quality semantic search |
| 💬 **Policy Q&A Chatbot** | Ask natural language questions about your AI governance rules |
| 📊 **Scan History & Stats** | Tracks all scans with verdicts, timestamps, and RAG grounding status |
| ⚡ **Zero Dependencies** | Pure HTML/CSS/JS — no build step, no framework, no npm install |

---

## 🚨 Threat Detection Categories

- **Prompt Injection** — Hidden instructions that attempt to override system rules
- **Jailbreak** — Role-play or fictional framing used to bypass safety guidelines
- **Data Exfiltration** — Requests to extract API keys, credentials, or context data
- **Social Engineering** — Emotional manipulation to extract sensitive information
- **Policy Bypass** — Attempts to circumvent your organization's AI usage policy
- **PII Exposure** — Prompts containing or requesting personally identifiable information

---

## 🏗️ Architecture

```
User Prompt
     │
     ▼
┌─────────────────────────────────────┐
│         RAG Retrieval Layer         │
│  Query → nomic-embed-text (768-dim) │
│  → Cosine Similarity → Top-K Chunks │
└─────────────────────────────────────┘
     │  Relevant Policy Context
     ▼
┌─────────────────────────────────────┐
│      llama-3.3-70b-versatile        │
│         (via Groq API)              │
│  Structured JSON verdict output     │
└─────────────────────────────────────┘
     │
     ▼
  SAFE / SUSPICIOUS / DANGEROUS
  + Threat Type + Severity + Policy Citation
```

---

## 🚀 Getting Started

### Prerequisites

- A free [Groq API key](https://console.groq.com) — takes ~30 seconds to create

### Setup

**1. Clone the repository**
```bash
git clone https://github.com/your-username/promptguard.git
cd promptguard
```

**2. Add your Groq API key**

Open `index.html` and replace the placeholder on this line:
```javascript
const GROQ_KEY = "YOUR_GROQ_API_KEY_HERE";
```

**3. Open in browser**
```bash
# Just open the file — no server needed
open index.html
```

That's it. No `npm install`, no build step.

---

## ☁️ Deploy to Netlify

```
1. Push the repository to GitHub
2. Go to netlify.com → "Add new site" → "Import from Git"
3. Select your repo — Netlify auto-detects the HTML file
4. Click Deploy
```

Your site is live in under 60 seconds. Set the `GROQ_KEY` as a Netlify environment variable if you want to avoid committing it.

---

## 🗂️ Project Structure

```
promptguard/
│
├── index.html          # Entire application — UI, logic, RAG pipeline
└── README.md           # This file
```

---

## 📖 Usage Guide

### 1 — Scan a Prompt
Paste any AI prompt into the text area and click **Analyze prompt**. Use the sample chips to quickly load example attacks (injection, jailbreak, exfiltration, social engineering).

### 2 — Build a Knowledge Base (RAG)
Go to the **Knowledge base** tab. Choose a built-in policy template:
- **OWASP LLM Top 10** — industry-standard LLM security rules
- **Corporate AI Policy** — enterprise AI usage guidelines
- **Healthcare / HIPAA** — PHI and compliance requirements

Or paste your own custom policy text. Click **Build knowledge base** — the system embeds every chunk into 768-dimensional vectors using `nomic-embed-text-v1_5`. Once built, all future scans are grounded in your policy.

### 3 — Policy Chat
Go to the **Policy chat** tab and ask natural language questions like:
- *"What does our policy say about API keys in prompts?"*
- *"Which OWASP rule covers jailbreak attempts?"*
- *"What are the penalties for a data exfiltration attempt?"*

Responses are semantically retrieved from your knowledge base and answered by the LLM.

### 4 — Review History
The **History** tab shows all past scans with verdicts, timestamps, and whether RAG grounding was active. Click any entry to re-analyze it.

---

## 🔧 Tech Stack

| Layer | Technology |
|---|---|
| **LLM** | Meta llama-3.3-70b-versatile |
| **Inference** | Groq API |
| **Embeddings** | nomic-embed-text-v1_5 (768-dim) |
| **Vector Search** | In-browser cosine similarity |
| **Frontend** | Vanilla HTML / CSS / JavaScript |
| **Deployment** | Netlify |

---

## 👥 Team

| Name | Role | Handle |
|---|---|---|
| Mirza Yasir Abdullah Baig | Project Lead | @mirzayasirabdullahbaig |
| Sadia Usman | AI Engineer | @Frost_Flashlog3 |
| Nazish Javeed | Backend Developer | @Nazishjaveed |
| Hira Mujeeb | UI/UX Developer | @Mystic_Tintp1t7 |
| Hamna Munir | Security Analyst | @HamnaMunir |

---

## ⚙️ Configuration

| Variable | Location | Description |
|---|---|---|
| `GROQ_KEY` | `index.html` line ~180 | Your Groq API key |
| `BATCH` | `buildKB()` function | Embedding batch size (default: 8) |
| `k` in `retrieve()` | `analyze()` / `sendChat()` | Number of retrieved chunks (default: 3–4) |
| `maxTokens` | `groqChat()` | Max LLM output tokens (default: 600) |

---

## 🔒 Security Notes

- **Never commit your Groq API key** to a public repository. Use environment variables or Netlify's secret management.
- All vector search and chunking happens **client-side in the browser** — your policy text is never sent to any server other than Groq's embedding API.
- The app makes direct browser-to-Groq API calls. For production use, consider proxying through a backend to keep the API key server-side.

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🙏 Acknowledgements

- [Groq](https://groq.com) — for blazing-fast LLM inference
- [Meta AI](https://ai.meta.com) — for the llama-3.3-70b-versatile model
- [Nomic AI](https://nomic.ai) — for the nomic-embed-text embedding model
- [OWASP](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — for the LLM Top 10 security framework
