<div align="center">

# 🧠 MemoryLane AI

**Your AI-powered second brain for the web.**

> Save, summarize, search, and rediscover everything you've ever browsed — intelligently.

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.111+-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![Next.js](https://img.shields.io/badge/Next.js-14+-000000?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org)
[![Chrome Extension](https://img.shields.io/badge/Chrome-Extension-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white)](https://developer.chrome.com/docs/extensions/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](https://opensource.org/licenses/MIT)

<br />

![MemoryLane Banner](./assets/banner.png)

</div>

---

## 📖 What is MemoryLane AI?

Modern users consume **thousands of web pages** every month — articles, tutorials, GitHub repos, research papers, YouTube videos. Most of it is forgotten within days.

**MemoryLane AI** transforms your browser into an intelligent memory system. Save any page with one click, and it automatically:

- ✍️ Generates an AI summary with key insights
- 🏷️ Tags and categorizes the content
- 🔍 Makes it searchable via natural language
- 💬 Lets you *chat* with your saved knowledge
- 🔔 Reminds you to revisit what you've forgotten

---

## ✨ Key Features

| Feature | Description |
|---|---|
| **One-Click Save** | Save any page instantly from the Chrome extension |
| **AI Summarization** | GPT/Gemini-powered 3-5 sentence summaries + key bullet points |
| **Auto Tagging** | Automatically categorizes: Article, Tutorial, GitHub, Video, Docs, Research |
| **Semantic Search** | Find memories using natural language: *"that React hooks article from last month"* |
| **Chat with Knowledge** | RAG-powered chatbot that answers questions from your saved pages |
| **Research Sessions** | Groups tabs you browse together into named research sessions |
| **Forgotten Tab Alerts** | Detects tabs open for days that you've never read |
| **Daily Digest** | Morning briefing of what to review today |
| **Privacy First** | All data stored locally. AI calls are opt-in per page. |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     USER'S BROWSER                          │
│                                                             │
│  ┌─────────────────┐        ┌──────────────────────────┐   │
│  │ Chrome Extension│        │   Next.js Web Dashboard  │   │
│  │  (Manifest V3)  │        │   localhost:3000         │   │
│  │                 │        │                          │   │
│  │  • Popup UI     │        │  • All Memories View     │   │
│  │  • Tab Watcher  │        │  • Semantic Search       │   │
│  │  • Quick Save   │        │  • AI Chat Interface     │   │
│  │  • Notifications│        │  • Research Sessions     │   │
│  └────────┬────────┘        └────────────┬─────────────┘   │
│           │                              │                  │
└───────────┼──────────────────────────────┼──────────────────┘
            │         REST / WebSocket     │
            ▼                             ▼
┌─────────────────────────────────────────────────────────────┐
│              Python FastAPI Backend  :8000                   │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │  AI Engine   │  │  Memory API  │  │  Search Engine   │  │
│  │  (Python)    │  │  (CRUD)      │  │  (Embeddings)    │  │
│  │              │  │              │  │                  │  │
│  │ • Summarize  │  │ • Save Page  │  │ • Vector Search  │  │
│  │ • Tag/Categ. │  │ • Get/Delete │  │ • Keyword Search │  │
│  │ • Embed Text │  │ • Sessions   │  │ • Hybrid Ranking │  │
│  │ • RAG Chat   │  │ • Digest     │  │                  │  │
│  └──────┬───────┘  └──────┬───────┘  └──────────────────┘  │
│         │                 │                                 │
│         ▼                 ▼                                 │
│  ┌──────────────┐  ┌──────────────────────────────────────┐ │
│  │  LLM Provider│  │         SQLite / PostgreSQL           │ │
│  │              │  │                                      │ │
│  │ • Gemini API │  │  memories | sessions | embeddings    │ │
│  │ • OpenAI API │  │  settings | digests  | tags         │ │
│  │ • Ollama     │  │                                      │ │
│  └──────────────┘  └──────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗂️ Project Structure

```
memorylane-ai/
│
├── 📁 extension/                    # Chrome Extension (Manifest V3 + JS)
│   ├── manifest.json
│   ├── background/
│   │   └── service-worker.js        # Tab tracking, alarms, notifications
│   ├── content/
│   │   └── content-script.js        # Page content extractor
│   ├── popup/
│   │   ├── popup.html
│   │   ├── popup.css
│   │   └── popup.js
│   ├── sidepanel/
│   │   ├── sidepanel.html
│   │   ├── sidepanel.css
│   │   └── sidepanel.js
│   └── lib/
│       ├── api-client.js            # Talks to FastAPI backend
│       └── utils.js
│
├── 📁 backend/                      # Python FastAPI AI Backend
│   ├── main.py                      # App entry point
│   ├── requirements.txt
│   │
│   ├── api/
│   │   ├── memories.py              # CRUD endpoints
│   │   ├── search.py                # Semantic + keyword search
│   │   ├── chat.py                  # RAG chat endpoint
│   │   ├── digest.py                # Daily digest generation
│   │   └── sessions.py             # Research session endpoints
│   │
│   ├── core/
│   │   ├── ai.py                    # LLM provider abstraction
│   │   ├── embeddings.py            # Text embedding + vector ops
│   │   ├── summarizer.py            # Page summarization logic
│   │   ├── tagger.py                # Auto-tagging + categorization
│   │   └── rag.py                   # Retrieval-Augmented Generation
│   │
│   ├── db/
│   │   ├── database.py              # SQLAlchemy setup
│   │   ├── models.py                # ORM models
│   │   └── migrations/
│   │
│   └── utils/
│       ├── text_extractor.py        # Clean text from HTML
│       └── config.py                # Settings via pydantic-settings
│
├── 📁 frontend/                     # Next.js 14 Web Dashboard
│   ├── package.json
│   ├── next.config.js
│   │
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx                 # Home / Digest
│   │   ├── memories/
│   │   │   └── page.tsx             # All Memories
│   │   ├── search/
│   │   │   └── page.tsx             # Semantic Search
│   │   ├── chat/
│   │   │   └── page.tsx             # AI Chat Interface
│   │   ├── sessions/
│   │   │   └── page.tsx             # Research Sessions
│   │   └── settings/
│   │       └── page.tsx             # API Keys, Preferences
│   │
│   ├── components/
│   │   ├── ui/                      # Base UI components
│   │   ├── MemoryCard.tsx
│   │   ├── SearchBar.tsx
│   │   ├── ChatWindow.tsx
│   │   ├── SessionCard.tsx
│   │   └── DigestView.tsx
│   │
│   ├── lib/
│   │   ├── api.ts                   # API client (fetch wrapper)
│   │   └── types.ts                 # TypeScript types
│   │
│   └── styles/
│       └── globals.css
│
├── 📁 assets/                       # Shared assets
│   ├── banner.png
│   └── icons/
│
├── docker-compose.yml               # One-command local setup
├── .env.example                     # Environment variable template
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.11+
- Node.js 18+
- Google Chrome / Chromium
- A **Gemini API Key** (free at [aistudio.google.com](https://aistudio.google.com)) or **OpenAI API Key**

---

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/memorylane-ai.git
cd memorylane-ai
```

---

### 2. Set Up Environment Variables

```bash
cp .env.example .env
```

Edit `.env`:

```env
# AI Provider — choose one
GEMINI_API_KEY=your_gemini_api_key_here
OPENAI_API_KEY=your_openai_api_key_here   # optional

# AI Model selection
AI_PROVIDER=gemini                         # gemini | openai | ollama
GEMINI_MODEL=gemini-1.5-flash
EMBEDDING_MODEL=models/text-embedding-004

# Database
DATABASE_URL=sqlite:///./memorylane.db     # or postgresql://...

# Server
BACKEND_PORT=8000
FRONTEND_PORT=3000
CORS_ORIGINS=chrome-extension://*,http://localhost:3000
```

---

### 3. Start the Python Backend

```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate       # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run database migrations
python -m alembic upgrade head

# Start FastAPI server
uvicorn main:app --reload --port 8000
```

Backend docs available at: **http://localhost:8000/docs**

---

### 4. Start the Next.js Frontend

```bash
cd frontend

npm install
npm run dev
```

Open: **http://localhost:3000**

---

### 5. Load the Chrome Extension

1. Open Chrome and go to `chrome://extensions`
2. Enable **Developer Mode** (top right toggle)
3. Click **"Load unpacked"**
4. Select the `extension/` folder
5. Pin the MemoryLane AI icon to your toolbar 📌

---

### Option B: Docker (One Command)

```bash
docker-compose up --build
```

This starts the backend on `:8000` and frontend on `:3000` automatically.

---

## 📡 API Reference

Base URL: `http://localhost:8000/api/v1`

### Memories

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/memories` | Save a new page |
| `GET` | `/memories` | List all memories (paginated) |
| `GET` | `/memories/{id}` | Get a single memory |
| `DELETE` | `/memories/{id}` | Delete a memory |
| `PATCH` | `/memories/{id}` | Update tags / mark reviewed |

### Search

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/search?q=react+hooks` | Hybrid semantic + keyword search |
| `GET` | `/search/semantic?q=...` | Pure vector similarity search |

### AI Chat

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/chat` | RAG chat with your saved knowledge |
| `GET` | `/chat/history` | Past chat conversations |

### Sessions & Digest

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/sessions` | All research sessions |
| `GET` | `/digest/today` | Today's review digest |
| `GET` | `/digest/forgotten` | Forgotten/unread memories |

---

## 🧠 AI Pipeline

When a page is saved, here's what happens:

```
User clicks "Save"
       │
       ▼
Content Script extracts clean text
       │
       ▼
POST /memories  ──►  FastAPI receives {url, title, content}
       │
       ├──► Summarizer  ──► Gemini: "Summarize this in 3-5 sentences..."
       │                         └──► summary, keyInsights[]
       │
       ├──► Tagger      ──► Gemini: "Tag and categorize this page..."
       │                         └──► tags[], category
       │
       └──► Embedder    ──► Gemini Embeddings API
                                 └──► float[] stored in DB
       │
       ▼
Saved to SQLite/PostgreSQL
       │
       ▼
Response: { id, summary, tags, category, savedAt }
       │
       ▼
Popup shows success animation ✓
```

---

## 🔍 Semantic Search

MemoryLane uses **vector embeddings** for natural language search:

```
User query: "find that article about React performance"
       │
       ▼
Embed query ──► [0.12, -0.34, 0.87, ...]
       │
       ▼
Cosine similarity against all stored embeddings
       │
       ▼
Top-K results ranked by relevance score
       │
       ▼
Hybrid re-ranking with keyword boost
       │
       ▼
Results returned with match explanation
```

---

## 💬 RAG Chat

The chat feature uses **Retrieval-Augmented Generation**:

```
User: "What GitHub repos did I save for my startup?"
       │
       ▼
Semantic search over memories (category: GitHub)
       │
       ▼
Top 5 relevant memory summaries retrieved as context
       │
       ▼
Gemini: "Based on your saved memories: [context]
         Answer: [user question]"
       │
       ▼
Cited response with links back to original memories
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Browser Extension** | JavaScript, Chrome APIs (MV3) | Tab tracking, content extraction, popup UI |
| **AI Backend** | Python 3.11, FastAPI | Summarization, embedding, RAG, tagging |
| **AI Models** | Google Gemini / OpenAI GPT | LLM inference + text embeddings |
| **Web Frontend** | Next.js 14, React, TypeScript | Full dashboard & chat interface |
| **Database** | SQLite (dev) / PostgreSQL (prod) | Storing memories, sessions, embeddings |
| **ORM** | SQLAlchemy + Alembic | DB models + migrations |
| **Styling** | CSS Modules / Tailwind CSS | Frontend design system |

---

## 🔒 Privacy & Security

- ✅ **Local-first**: All your memories are stored on **your machine**
- ✅ **Opt-in AI**: Content is only sent to AI APIs when you explicitly save a page
- ✅ **No tracking**: No analytics, no telemetry, no third-party data sharing
- ✅ **API keys**: Stored in local environment variables, never transmitted
- ✅ **CORS**: Backend only accepts requests from the extension and localhost
- ⚙️ **Self-host option**: Use Ollama for 100% offline AI processing

---

## 🗺️ Roadmap

- [x] Core architecture design
- [ ] Python FastAPI backend with AI pipeline
- [ ] Chrome Extension (popup + side panel)
- [ ] Next.js web dashboard
- [ ] Semantic search with vector embeddings
- [ ] RAG chat interface
- [ ] Research session tracking
- [ ] Daily digest & review reminders
- [ ] Ollama (offline) support
- [ ] Firefox extension port
- [ ] Mobile companion app
- [ ] Team / shared knowledge base mode

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](https://github.com/siddhant0610/memorylane-ai/blob/main/CONTRIBUTING.md) before submitting a PR.

```bash
# Fork → Clone → Create branch → Make changes → PR
git checkout -b feature/your-feature-name
```

---

## 📄 License

MIT License — see [LICENSE](https://opensource.org/licenses/MIT) for details.

---
