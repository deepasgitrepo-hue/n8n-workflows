# n8n AI Agent Workflows

A collection of ready-to-import **n8n workflow templates** showcasing practical AI agent use cases — a **Tech Trends Extractor** that curates the latest technology news into a polished webpage, and a **Resume Tailoring Agent** that rewrites resumes to match specific job descriptions.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Workflows](#workflows)
  - [Tech Trends Extractor](#1-tech-trends-extractor)
  - [Resume Tailoring Agent](#2-resume-tailoring-agent)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [Configuration Notes](#configuration-notes)
- [License](#license)

---

## Overview

Both workflows are built on **n8n**, the open-source workflow automation platform, and leverage **OpenRouter** for LLM inference (using free-tier models). They demonstrate how to:

- Build conversational AI agents with tool-calling capabilities inside n8n.
- Integrate external APIs (Tavily search, PDF extraction) as agent tools.
- Generate dynamic HTML output from LLM responses.

---

## Workflows

### 1. Tech Trends Extractor

| Detail | Value |
|---|---|
| **Workflow file** | `Tech Trends_n8n_workflow.json` |
| **LLM model** | `openrouter/free` (via OpenRouter) |
| **External API** | [Tavily Search API](https://tavily.com/) |

**What it does:**
- Accepts a user chat message describing a tech topic of interest.
- An AI agent uses Tavily web search as a tool to find the latest trends and articles.
- A second agent curates the results into a styled HTML page.

**Agent personality:** Friendly, educational, and enthusiastic about automation. Designed to showcase what AI agents within n8n can do — including explaining their own architecture to the user.

---

### 2. Resume Tailoring Agent

| Detail | Value |
|---|---|
| **Workflow file** | `Resume Generator_n8n_workflow.json` |
| **LLM model** | `openrouter/free` (via OpenRouter) |
| **Input** | Job description (chat) + Resume (PDF upload) |

**What it does:**
- Accepts a **job description** via the n8n chat widget.
- Accepts the candidate's **resume as a PDF** file upload.
- Extracts text from the PDF using n8n's built-in PDF extractor.
- A Resume Tailoring Agent rewrites the resume to maximize alignment with the job description, including ATS keyword optimization, bullet-point rewriting, and strategic gap-filling.
- Outputs a fully tailored resume in clean Markdown.

**Sample resumes** for testing are provided in the `sample-resumes/` directory.

---

## Prerequisites

- **n8n** — self-hosted or cloud ([install guide](https://docs.n8n.io/hosting/installation/))
- **OpenRouter API key** — sign up at [openrouter.ai](https://openrouter.ai/) (free tier available)
- **Tavily API key** *(Tech Trends workflow only)* — sign up at [tavily.com](https://tavily.com/)
- **Docker & Docker Compose** *(optional, for self-hosted setup)*

---

## Setup

### 1. Install n8n

```bash
curl -fsSL https://get.n8n.io | sh
```

Or run via Docker Compose — see [Instructions.md](Instructions.md) for detailed configuration.

### 2. Import Workflows

1. Open the n8n editor UI.
2. Go to **Workflows → Import from File**.
3. Import `Tech Trends_n8n_workflow.json` and/or `Resume Generator_n8n_workflow.json`.

### 3. Configure Credentials

After importing, configure the following credentials in n8n:

| Credential | Used by |
|---|---|
| **OpenRouter API** | Both workflows |
| **Tavily API** | Tech Trends Extractor |

### 4. Activate & Run

Toggle the workflow to **Active**, then open the chat widget URL to interact with the agent.

---

## Project Structure

```
n8n/
├── README.md                              # This file
├── Instructions.md                        # Detailed setup notes & agent prompts
├── Tech Trends_n8n_workflow.json          # Tech Trends Extractor workflow
├── Resume Generator_n8n_workflow.json     # Resume Tailoring Agent workflow
└── sample-resumes/                        # Sample PDF resumes for testing
    ├── Alex Turing_resume.pdf
    └── Jordan Patel_resume.pdf
```

---

## Usage

### Tech Trends Extractor

1. Open the chat widget for the Tech Trends workflow.
2. Ask about any technology topic — e.g., *"What are the latest trends in AI agents?"*
3. The agent searches the web, summarizes findings, and generates an HTML page.

### Resume Tailoring Agent

1. Open the chat widget for the Resume Generator workflow.
2. Paste the **job description** into the chat.
3. Upload your **resume PDF** when prompted.
4. Receive a fully rewritten, ATS-optimized resume with tailoring notes.

---

## Configuration Notes

### GitHub Codespaces / Docker

If running through **GitHub Codespaces**, add the following environment variables to your `docker-compose.yml`:

```yaml
environment:
  - N8N_HOST=<your-codespace-url>-5678.app.github.dev
  - N8N_PROTOCOL=https
  - N8N_EDITOR_BASE_URL=https://<your-codespace-url>-5678.app.github.dev
  - WEBHOOK_URL=https://<your-codespace-url>-5678.app.github.dev/
  - N8N_PUSH_BACKEND=sse
  - N8N_PROXY_HOPS=1
```

Replace `<your-codespace-url>` with your actual Codespaces forwarded URL.

### Model Selection

Both workflows default to `openrouter/free`. You can swap to any model available on OpenRouter by editing the **OpenRouter Chat Model** node in each workflow.

---

## License

This project is provided as-is for educational and demonstration purposes.
