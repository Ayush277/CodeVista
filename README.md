<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/FastAPI-0.109-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI"/>
  <img src="https://img.shields.io/badge/Gemini_AI-Powered-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Gemini"/>
  <img src="https://img.shields.io/badge/SQLite-Database-003B57?style=for-the-badge&logo=sqlite&logoColor=white" alt="SQLite"/>
  <img src="https://img.shields.io/badge/License-Educational-green?style=for-the-badge" alt="License"/>
</p>

# 🔍 CodeVista — AI-Powered GitHub Repository Analyzer

> **Understand any GitHub codebase in seconds.** CodeVista uses Google's Gemini AI to analyze repository structure, architecture, tech stack, and more — then lets you ask questions about the codebase in plain English.

---

## 📋 Table of Contents

- [What is CodeVista?](#-what-is-codevista)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Setup & Installation](#-setup--installation)
- [Environment Variables](#-environment-variables)
- [Running the App](#-running-the-app)
- [API Endpoints](#-api-endpoints)
- [How It Works](#-how-it-works)
- [Database Schema](#-database-schema)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [Troubleshooting](#-troubleshooting)

---

## 🧠 What is CodeVista?

CodeVista is a **full-stack web application** that takes any public GitHub repository URL and performs a deep AI-powered analysis on it. It generates:

- A comprehensive **project overview**
- Full **tech stack** breakdown with versions
- **Architecture pattern** identification (MVC, Monolith, Microservices, etc.)
- **Architecture diagrams** rendered via Mermaid.js
- **Key file** identification with roles and purposes
- **Issues & risks** assessment from GitHub issues
- A **contributor guide** for new developers
- **Natural language Q&A** — ask any question about the codebase

The backend is built with **FastAPI** (Python) and the frontend is a **single-page React app** served from a single `index.html` file.

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 🤖 **AI Analysis** | Single Gemini API call per repo — generates structured, validated JSON |
| 💬 **Q&A Chat** | Ask questions in plain English about any analyzed repository |
| 📊 **Architecture Diagrams** | Auto-generated Mermaid.js diagrams rendered client-side |
| ⚡ **Async Processing** | Background task processing — UI stays responsive during analysis |
| 🔄 **Real-time Updates** | WebSocket support for live analysis progress |
| 📈 **Code Quality Metrics** | Automated scoring for docs, tests, organization, dependencies |
| 🔀 **Repo Comparison** | Compare multiple repos across tech stack, architecture, complexity |
| 🗄️ **Persistent Storage** | SQLite database stores all analysis results |
| 🛡️ **Rate Limiting** | Built-in rate limiting via SlowAPI |
| 🧪 **Test Suite** | pytest-based tests with async support |

---

## 🛠️ Tech Stack

### Backend
| Technology | Purpose |
|---|---|
| **Python 3.9+** | Core language |
| **FastAPI** | Web framework (async) |
| **Uvicorn** | ASGI server |
| **SQLAlchemy 2.0** | ORM (async mode) |
| **aiosqlite** | Async SQLite driver |
| **Pydantic** | Data validation & serialization |
| **httpx** | Async HTTP client (GitHub API calls) |
| **google-genai** | Google Gemini AI SDK |
| **SlowAPI** | Rate limiting |
| **python-dotenv** | Environment variable management |
| **websockets** | Real-time progress updates |

### Frontend
| Technology | Purpose |
|---|---|
| **React 18** | UI library (loaded via CDN) |
| **Tailwind CSS** | Utility-first styling (loaded via CDN) |
| **Mermaid.js** | Architecture diagram rendering |
| **Babel** | JSX transpilation in-browser |

---

## 📁 Project Structure

```
CodeVista-main/
├── main.py                  # FastAPI app entry point & configuration
├── index.html               # Single-page React frontend
├── requirements.txt         # Production Python dependencies
├── requirements-dev.txt     # Development dependencies (testing, linting)
├── .env                     # Environment variables (YOU CREATE THIS)
├── .gitignore               # Git ignore rules
├── Procfile                 # Heroku deployment command
├── railway.json             # Railway deployment config
├── runtime.txt              # Python version specification
├── pytest.ini               # Test configuration
│
├── routes/                  # API route handlers
│   ├── api.py               # All REST endpoints (/analyze-repo, /ask, /status, etc.)
│   └── websocket.py         # WebSocket endpoint for real-time updates
│
├── services/                # Core business logic
│   ├── analysis_service.py  # Main analysis orchestration
│   ├── gemini_service.py    # Gemini AI integration & prompt engineering
│   ├── github_service.py    # GitHub API interactions
│   ├── cache_service.py     # Smart caching layer
│   ├── code_quality_service.py  # Code quality scoring
│   ├── comparative_service.py   # Multi-repo comparison
│   ├── dependency_analyzer.py   # Dependency detection
│   └── diagram_generator.py     # Mermaid diagram generation
│
├── models/                  # Data models
│   ├── schemas.py           # SQLAlchemy database models (12 tables)
│   └── pydantic_models.py   # Request/response validation models
│
├── db/                      # Database layer
│   ├── database.py          # Async engine & session configuration
│   └── migration.py         # Schema migration helpers
│
├── utils/                   # Utility modules
│   ├── file_filter.py       # Smart file filtering & prioritization
│   ├── logger.py            # Structured JSON logging
│   └── rate_limiter.py      # Rate limiter configuration
│
└── tests/                   # Test suite
    ├── conftest.py           # Shared test fixtures
    ├── test_api_endpoints.py # API endpoint tests
    ├── test_diagram_generator.py # Diagram generation tests
    └── test_github_service.py    # GitHub service tests
```

---

## ⚙️ Prerequisites

Before running CodeVista, make sure you have:

| Requirement | Details |
|---|---|
| **Python** | Version **3.9 or higher** ([Download](https://www.python.org/downloads/)) |
| **pip** | Comes with Python (package installer) |
| **Git** | To clone the repository ([Download](https://git-scm.com/)) |
| **Gemini API Key** | **Required** for AI analysis ([Get one free](https://aistudio.google.com/app/apikey)) |
| **GitHub Token** | **Optional** — increases GitHub API rate limit from 60 to 5,000 requests/hour |

---

## 🚀 Setup & Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/<your-username>/CodeVista.git
cd CodeVista
```

### Step 2: Create a Virtual Environment

```bash
# Create virtual environment
python -m venv venv

# Activate it
# macOS / Linux:
source venv/bin/activate

# Windows:
venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Create Your `.env` File

Create a file named `.env` in the project root:

```env
# ─── REQUIRED ─────────────────────────────────────────────
GEMINI_API_KEY=your_gemini_api_key_here

# ─── OPTIONAL ─────────────────────────────────────────────
# Gemini model: "flash" (faster, cheaper) or "pro" (higher quality)
GEMINI_MODEL=flash

# GitHub personal access token (raises rate limit from 60 to 5000 req/hr)
GITHUB_TOKEN=your_github_token_here
```

> **⚠️ Important:** Without `GEMINI_API_KEY`, the app will run in **mock mode** — it will return placeholder analysis instead of real AI insights.

---

## 🔑 Environment Variables

| Variable | Required | Default | Description |
|---|---|---|---|
| `GEMINI_API_KEY` | ✅ Yes | — | Your Google Gemini API key |
| `GEMINI_MODEL` | ❌ No | `flash` | `flash` (fast & cheap) or `pro` (higher quality) |
| `GITHUB_TOKEN` | ❌ No | — | GitHub PAT for higher API rate limits |
| `PORT` | ❌ No | `8000` | Server port (auto-set on Railway/Heroku) |

### How to Get Your API Keys

#### Gemini API Key (Required)
1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Sign in with your Google account
3. Click **"Create API Key"**
4. Copy the key and paste it in your `.env` file

#### GitHub Token (Optional but Recommended)
1. Go to [GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)](https://github.com/settings/tokens)
2. Click **"Generate new token (classic)"**
3. No special scopes needed for public repos — just click **"Generate token"**
4. Copy the token and paste it in your `.env` file

---

## ▶️ Running the App

```bash
# Option 1: Run directly
python main.py

# Option 2: Run with uvicorn (with hot-reload)
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Once running, open your browser to:

| URL | What it is |
|---|---|
| `http://localhost:8000` | 🖥️ CodeVista Web UI |
| `http://localhost:8000/docs` | 📝 Swagger API Documentation |
| `http://localhost:8000/redoc` | 📖 ReDoc API Documentation |

---

## 🌐 API Endpoints

### Core Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/analyze-repo` | Start analyzing a GitHub repository |
| `GET` | `/api/status/{repo_id}` | Check analysis progress |
| `GET` | `/api/analysis/{repo_id}` | Get completed analysis results |
| `POST` | `/api/ask` | Ask a question about an analyzed repo |
| `GET` | `/api/health` | Health check |

### Advanced Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/compare` | Compare multiple repositories |
| `GET` | `/api/code-quality/{repo_id}` | Get code quality metrics |
| `WS` | `/ws/analysis/{repo_id}` | WebSocket for real-time progress |

### Quick Test with cURL

```bash
# 1. Start analysis
curl -X POST http://localhost:8000/api/analyze-repo \
  -H "Content-Type: application/json" \
  -d '{"repo_url": "https://github.com/fastapi/fastapi"}'

# Response: {"repo_id": "some-uuid", "status": "processing", ...}

# 2. Check status (replace YOUR_REPO_ID)
curl http://localhost:8000/api/status/YOUR_REPO_ID

# 3. Get results (after status shows "completed")
curl http://localhost:8000/api/analysis/YOUR_REPO_ID

# 4. Ask a question
curl -X POST http://localhost:8000/api/ask \
  -H "Content-Type: application/json" \
  -d '{"repo_id": "YOUR_REPO_ID", "question": "What is this project about?"}'
```

---

## 🔄 How It Works

```
┌──────────────┐     ┌───────────────┐     ┌──────────────┐
│  User pastes │────▶│  FastAPI       │────▶│  GitHub API  │
│  GitHub URL  │     │  Backend       │     │  (fetch repo)│
└──────────────┘     └───────┬───────┘     └──────────────┘
                             │
                     ┌───────▼───────┐
                     │  Analysis     │
                     │  Service      │
                     │  (orchestrate)│
                     └───────┬───────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
      ┌───────▼──────┐ ┌────▼─────┐ ┌──────▼───────┐
      │  File Filter  │ │ Dep      │ │  Gemini AI   │
      │  & Prioritize │ │ Analyzer │ │  (1 API call)│
      └──────────────┘ └──────────┘ └──────┬───────┘
                                           │
                                   ┌───────▼───────┐
                                   │  SQLite DB    │
                                   │  (12 tables)  │
                                   └───────┬───────┘
                                           │
                                   ┌───────▼───────┐
                                   │  React UI     │
                                   │  (dashboard)  │
                                   └───────────────┘
```

### Analysis Pipeline (Step-by-Step)

1. **URL Validation** — Validates the GitHub repo URL format
2. **Metadata Fetch** — Gets repo info (owner, name, language) via GitHub API
3. **File Discovery** — Fetches repo tree, filters & prioritizes important files
4. **Content Extraction** — Downloads README, config files, key source files
5. **Dependency Analysis** — Detects frameworks, libraries, languages from config files
6. **Issue Fetching** — Gets open and recently closed GitHub issues
7. **AI Analysis** — **Single** Gemini API call generates all insights as structured JSON
8. **Database Storage** — Results stored across 12 normalized SQLite tables
9. **Diagram Generation** — Mermaid.js syntax generated for architecture visualization
10. **Results Ready** — Frontend polls status, then displays all analysis tabs

### File Filtering Logic

The system intelligently selects which files to analyze:

- **Priority 100:** Entry points (`main.py`, `index.js`, `app.py`)
- **Priority 80:** Config files (`package.json`, `requirements.txt`, `Dockerfile`)
- **Priority 60:** Root/src directory files
- **Priority 40:** Other source files
- **Ignored:** `node_modules/`, `venv/`, `.git/`, `build/`, `dist/`
- **Size Limit:** Files truncated to 10KB, max 30 files total

---

## 🗄️ Database Schema

CodeVista uses **12 normalized SQLite tables**:

| Table | Purpose |
|---|---|
| `repositories` | Repository metadata (URL, owner, name, language) |
| `analysis_sessions` | Tracks analysis status & progress |
| `analysis_summary` | Core summary, purpose, architecture pattern, diagrams |
| `tech_stack` | Individual technologies detected |
| `architecture_components` | Architectural modules/components |
| `key_files` | Important files with roles and purposes |
| `setup_steps` | Ordered setup instructions |
| `contribution_areas` | Safe areas for new contributors |
| `risky_areas` | Areas requiring caution |
| `known_issues` | Issues identified from GitHub |
| `qa_logs` | Question-answer history |
| `raw_analysis_responses` | Raw Gemini responses (for debugging) |

---

## 🧪 Testing

```bash
# Install dev dependencies
pip install -r requirements-dev.txt

# Run all tests
pytest

# Run with coverage
pytest --cov=. --cov-report=html

# Run specific test file
pytest tests/test_api_endpoints.py -v
```

---

## 🚢 Deployment

CodeVista is pre-configured for deployment on:

### Railway
- Config is in `railway.json`
- Set environment variables in Railway dashboard
- Deploys automatically with Nixpacks

### Heroku
- Config is in `Procfile` and `runtime.txt`
- Set environment variables via `heroku config:set`

### Docker (Manual)
```bash
# Example Dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## 🔧 Troubleshooting

| Problem | Solution |
|---|---|
| **`ModuleNotFoundError`** | Activate virtual env: `source venv/bin/activate`, then `pip install -r requirements.txt` |
| **Database errors** | Delete `app.db` and restart — it auto-recreates |
| **GitHub rate limit (403)** | Add `GITHUB_TOKEN` to your `.env` file |
| **Gemini API errors** | Verify your `GEMINI_API_KEY` in `.env`. Check quota at [AI Studio](https://aistudio.google.com/) |
| **Mock mode warning** | Set `GEMINI_API_KEY` in `.env` — without it, you get placeholder data |
| **Port already in use** | Kill existing process: `lsof -i :8000` then `kill -9 <PID>`, or use a different port |
| **Analysis stuck** | Check terminal logs for errors. Try deleting `app.db` and re-analyzing |

---

## 📄 License

This is a demonstration project for educational purposes.

---

<p align="center">
  Made with ❤️ using FastAPI + Gemini AI
</p>
