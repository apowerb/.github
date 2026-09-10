<div align="center">

# apowerb

**The open-source agentic framework to build, orchestrate, and operate production AI agents.**

[![Documentation](https://img.shields.io/badge/docs-apowerb.com-blue?style=for-the-badge&logo=googledocs&logoColor=white)](https://docs.apowerb.com/)
[![PyPI version](https://img.shields.io/pypi/v/apowerb?style=for-the-badge&logo=pypi&logoColor=white)](https://pypi.org/project/apowerb/)
[![Python](https://img.shields.io/badge/Python-3.12%20%7C%203.13-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-Apache_2.0-green.svg?style=for-the-badge)](LICENSE)
[![Discord](https://img.shields.io/badge/Community-Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/channels/1470717940075597896)

<p align="center">
  <a href="https://docs.apowerb.com/">Documentation</a> •
  <a href="https://docs.apowerb.com/quickstart">Quickstart</a> •
  <a href="https://docs.apowerb.com/api-reference/introduction">API Reference</a> •
  <a href="https://docs.apowerb.com/deployment/dockercompose">Deployment</a> •
  <a href="https://thaink2.com">thaink2</a>
</p>

</div>

---

## ⚡ Overview

**apowerb** (by [thaink2](https://thaink2.com)) is an open-source agentic platform and developer framework designed to build, run, and scale AI agents. It bridges the gap between raw LLMs and enterprise execution by combining declarative database-backed agent state, **Google ADK** execution, and **LiteLLM** multi-model interoperability.

The framework ships as a Python package providing:
- 🚀 **A high-performance FastAPI server** serving REST endpoints and SSE streams.
- 💻 **A Typer-powered CLI** for running, testing, and managing local workflows.
- 🖥️ **A companion web UI ([`apowerb-ui`](https://github.com/apowerb/apowerb-ui))** built with Next.js for visual prompt authoring, monitoring, and debugging.

---

## 🧩 Architectural Foundations

```
 ┌────────────────────────────────────────────────────────┐
 │                      Clients / UI                      │
 │    Next.js UI (apowerb-ui)  •  Typer CLI  •  REST/SSE  │
 └──────────────────────────┬─────────────────────────────┘
                            │
 ┌──────────────────────────▼─────────────────────────────┐
 │                FastAPI Orchestrator Layer               │
 │  • Agent Module Materialization   • Webhooks (Pub/Sub) │
 │  • Cron / Event Scheduler         • SSE Output Stream  │
 └──────────────────────────┬─────────────────────────────┘
                            │
 ┌──────────────────────────▼─────────────────────────────┐
 │               Execution Engine (Google ADK)            │
 │  • Base      • Parallel       • Sequential     • Loop  │
 │  • Hierarchical Sub-Agents    • Human-in-the-loop      │
 └─────────────┬───────────────────────────┬──────────────┘
               │                           │
 ┌─────────────▼─────────────┐   ┌─────────▼──────────────┐
 │   LiteLLM Model Router    │   │  Tool Integrations (24+)│
 │ OpenAI, Anthropic, Gemini │   │ M365, Google, SQL, RAG │
 └───────────────────────────┘   └────────────────────────┘
```

---

## 🚀 Key Capabilities

### 1. Advanced Agent Orchestration
Choose from four built-in execution patterns depending on task complexity:
- **`base`**: Single-turn and direct conversational agents with tool execution.
- **`sequential`**: Step-by-step pipelines passing context down deterministic stages.
- **`parallel`**: Concurrent branch execution aggregating results for low-latency synthesis.
- **`loop`**: Evaluator-optimizer cycles that iterate until target conditions or stop tokens are met.
- **Hierarchical sub-agents**: Delegate specialized tasks to domain-specific worker agents.

### 2. Universal Model Layer (LiteLLM)
Connect to any major model provider (OpenAI, Anthropic, Google Gemini, Mistral, Groq, local Ollama/vLLM) with unified configuration, fallback logic, and zero changes to underlying agent tools.

### 3. RAG as a Service
Incorporate retrieval without external plumbing:
- Automatically parse, chunk, and embed documents, URLs, Amazon S3 objects, and SQL query records.
- Isolated, per-agent knowledge bases searchable via semantic vector indices.

### 4. Text-to-SQL & Database Introspection
Connect Postgres, MySQL, or Snowflake instances. `apowerb` introspects table schemas, generates parameterized queries, and runs validated executions against analytical backends.

### 5. Automation & Event Triggers
- **Webhooks:** Inbound push notifications via Google Cloud Pub/Sub (Gmail) and Microsoft Graph (Outlook) to trigger autonomous email processing agents.
- **Scheduling:** Native cron-style schedules for recurring background audits, report generation, and polling tasks.
- **Real-time SSE:** Stream token-by-token completions, RAG ingestion progress, and agent state transitions in real time.

### 6. Tool & Skill Ecosystem (24+ Modules)
First-class support for enterprise SaaS and developer utilities:
- **Workplaces:** Google Workspace (Docs, Sheets, Drive, Gmail) and Microsoft 365 (Outlook, Teams, OneDrive).
- **Data & Storage:** AWS S3, Cloud Object Storage, PostgreSQL, Vector Stores.
- **Web & Code:** GitHub API, SerpAPI, Tavily, headless browsing, and data visualization generators.

---

## 🏢 Organization Repositories

| Repository | Description | Status |
| :--- | :--- | :--- |
| [**`apowerb`**](https://github.com/apowerb/apowerb) | Core framework, FastAPI backend, Typer CLI, and ADK execution runtime. | Active |
| [**`apowerb-ui`**](https://github.com/apowerb/apowerb-ui) | Next.js frontend companion application for visual agent orchestration. | Active |
| [**`docs`**](https://github.com/apowerb/docs) | Official developer guides, API specs, and tutorials (Mintlify). | Active |
| [**`agent-hub`**](https://github.com/apowerb/agent-hub) | Community & official agent templates, custom skills, and tool definitions. | Active |

---

## ⚡ Quickstart

### Option A: Complete Stack via Docker Compose

Run PostgreSQL, the `apowerb` backend engine, and `apowerb-ui` with a single command:

```bash
git clone https://github.com/apowerb/apowerb.git
cd apowerb
cp .env.example .env
docker compose up -d
```

Visit the dashboard at `http://localhost:3000` or inspect the API OpenAPI documentation at `http://localhost:8000/docs`.

---

### Option B: Local Python Installation

**Prerequisites:**
- Python 3.12 or 3.13
- PostgreSQL instance running locally or remotely
- [`uv`](https://docs.astral.sh/uv/) (recommended) or `pip`

```bash
# Install with uv
uv add apowerb

# Or with pip
pip install apowerb
```

Configure your environment:

```bash
export DATABASE_URL="postgresql+asyncpg://postgres:password@localhost:5432/apowerb"
export OPENAI_API_KEY="your-api-key"
```

Initialize the database schema and start the service:

```bash
# Run migrations
apowerb db upgrade

# Start the server
apowerb server --host 0.0.0.0 --port 8000 --reload
```

---

## 💻 CLI Usage

```bash
# List all active configured agents
apowerb agents list

# Execute an agent directly from terminal
apowerb run --name "support-agent" --prompt "Summarize pending tickets from yesterday"

# Start webhook receiver daemon
apowerb worker --queues default,webhooks
```

---

## 🤝 Contributing

We welcome pull requests, tool contributions, and bug reports from the developer community!

1. Fork the repo and create your branch from `main`.
2. Follow our [Development Guide](https://docs.apowerb.com/contributing/development).
3. Ensure linting and tests pass:
   ```bash
   uv run ruff check .
   uv run pytest
   ```
4. Check out the [Release Process](https://docs.apowerb.com/contributing/releases) to see how PRs are verified and released.

---

## 💬 Community & Support

- 📖 **Documentation:** [docs.apowerb.com](https://docs.apowerb.com/)
- 💬 **Discord Community:** [Join apowerb on Discord](https://discord.com/channels/1470717940075597896)
- 🐛 **Bug Tracker:** [GitHub Issues](https://github.com/apowerb/apowerb/issues)
- 🌐 **Company Website:** [thaink2.com](https://thaink2.com)

---

<div align="center">
  <sub>Released under the Apache 2.0 License • Maintained by <a href="https://thaink2.com">thaink2</a> and the open-source community.</sub>
</div>
