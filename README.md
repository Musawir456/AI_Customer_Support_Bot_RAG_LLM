# 🤖 Customer Support RAG Chatbot

![Python](https://img.shields.io/badge/Python-3.10+-blue) ![LangChain](https://img.shields.io/badge/LangChain-Enabled-green) ![Groq](https://img.shields.io/badge/Groq-LLaMA3.3--70B-orange) ![ChromaDB](https://img.shields.io/badge/ChromaDB-VectorStore-purple) ![License](https://img.shields.io/badge/License-MIT-yellow)

### RAG-Powered | Ticket-Aware | Real-Time Support Automation

An AI-powered customer support chatbot built with Retrieval-Augmented Generation (RAG). Trained on real support ticket data, it retrieves relevant resolutions and generates accurate, context-grounded answers — eliminating hallucinations and reducing support workload.

---

## 🎬 Demo

[![Watch Demo](https://img.youtube.com/vi/PtP3vy3SSS4/maxresdefault.jpg)](https://youtu.be/PtP3vy3SSS4)

> Click the thumbnail to watch the full demo on YouTube.

---

## ✨ Key Features

- **RAG Pipeline:** Retrieves top-3 relevant support tickets before generating any response — answers are always grounded in real data.
- **Zero Hallucination:** LLM only responds based on retrieved context, never fabricates resolutions.
- **Ticket-Aware Responses:** Understands ticket type, priority, subject, description, resolution, and customer satisfaction ratings.
- **Persistent Vector Store:** ChromaDB persists embeddings locally — no re-indexing on every restart.
- **Auto Rebuild:** Detects new data and automatically rebuilds the vector store when needed.
- **Chat History:** Full conversation memory within session via Streamlit state management.

---

## 🛠️ Tech Stack & Design Decisions

| Component | Tool | Why |
|---|---|---|
| Orchestration | LangChain | Modular RAG chain with RetrievalQA |
| LLM | Groq (LLaMA 3.3-70B) | Ultra-fast inference, enterprise-grade reasoning |
| Embeddings | all-MiniLM-L6-v2 | Lightweight, high semantic accuracy |
| Vector Store | ChromaDB | Persistent local indexing, no cloud dependency |
| Backend | FastAPI | Async query handling via `/ask` endpoint |
| UI | Streamlit | Lightweight chat interface with session state |

---

## 🏗️ Architecture Flow
```
Support Ticket CSV
      ↓
Document Loader (Ticket Type, Subject, Description, Resolution, Priority, Satisfaction)
      ↓
HuggingFace Embeddings (all-MiniLM-L6-v2)
      ↓
ChromaDB Vector Store (Persistent)
      ↓
User Query → Top-3 Retrieval
      ↓
LLaMA 3.3-70B via Groq → Grounded Answer
      ↓
FastAPI → Streamlit Chat UI
```

---

## 🚀 Quick Start

**1. Clone the repo:**
```bash
git clone https://github.com/YasraNafees/Customer-Support-RAG-Chatbot.git
cd Customer-Support-RAG-Chatbot
```

**2. Install dependencies:**
```bash
pip install -r requirements.txt
```

**3. Set environment variables:**

Create a `.env` file:
```
GROQ_API_KEY=your_groq_key_here
```

**4. Add your data:**

Place your support ticket CSV as `my_data.csv` in the root directory.

**5. Run the application:**
```bash
# Start FastAPI backend
uvicorn main:app --reload

# Start Streamlit UI (new terminal)
streamlit run app.py
```

---

## 📁 Data Format

Your CSV should include these columns:

| Column | Description |
|---|---|
| Ticket Type | Category of support issue |
| Ticket Subject | Brief issue title |
| Ticket Description | Full issue description |
| Resolution | How the issue was resolved |
| Ticket Priority | Low / Medium / High |
| Customer Satisfaction Rating | Post-resolution rating |

---

# 🤖 AI Customer Support Bot — RAG + LLM

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![LangChain](https://img.shields.io/badge/LangChain-Enabled-green?style=flat-square)
![Groq](https://img.shields.io/badge/Groq-LLaMA3.3--70B-orange?style=flat-square)
![ChromaDB](https://img.shields.io/badge/ChromaDB-VectorStore-purple?style=flat-square)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-teal?style=flat-square&logo=fastapi)
![Streamlit](https://img.shields.io/badge/Streamlit-UI-red?style=flat-square&logo=streamlit)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

> **An advanced customer support system leveraging RAG architecture and Large Language Models to deliver precise, context-driven responses by combining information retrieval with generative AI.**

---

## 📋 Table of Contents

- [Overview](#overview)
- [Live Demo](#live-demo)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [API Reference](#api-reference)
- [Data Format](#data-format)
- [Screenshots](#screenshots)
- [Contributing](#contributing)

---

## 🧠 Overview

The **AI Customer Support Bot** is a production-grade RAG (Retrieval-Augmented Generation) system that ingests real customer support ticket data, embeds it into a persistent ChromaDB vector store, and answers natural language queries using **LLaMA 3.3-70B** via Groq's ultra-fast inference API.

The system exposes a REST API via **FastAPI** and a conversational chat interface via **Streamlit** — giving both developers and end-users a seamless experience.

**Why RAG?** Unlike vanilla LLMs, this bot retrieves the top-3 most semantically relevant tickets *before* generating a response, ensuring answers are always grounded in real data with zero hallucination.

---

## 🎬 Live Demo

[![Watch Demo](https://img.youtube.com/vi/PtP3vy3SSS4/maxresdefault.jpg)](https://youtu.be/PtP3vy3SSS4)

> 📺 Click the thumbnail to watch the full walkthrough on YouTube.

---

## ✨ Key Features

- **🔍 RAG Pipeline** — Retrieves top-3 semantically relevant tickets before every response; answers are always grounded in real data
- **🧠 Zero Hallucination** — LLM only responds based on retrieved context, never fabricates resolutions
- **🎫 Ticket-Aware Responses** — Understands ticket type, priority, subject, description, resolution, and satisfaction ratings
- **💾 Persistent Vector Store** — ChromaDB persists embeddings locally — no re-indexing on every server restart
- **🔄 Auto Rebuild Detection** — Detects new CSV data and automatically rebuilds the vector store when needed
- **💬 Chat History** — Full conversation memory within session via Streamlit state management
- **⚡ Blazing Fast Inference** — Groq's LPU hardware delivers sub-second LLM responses
- **📡 REST API** — Clean `/ask` GET endpoint for programmatic access and integrations
- **⏱️ Request Timing Middleware** — Built-in logging of response times per endpoint

---

## 🏗️ Architecture

```
📄 Support Ticket CSV (my_data.csv)
          │
          ▼
  ┌───────────────────┐
  │  Document Loader  │  ← Ticket Type, Subject, Description,
  │  (rag_pipeline.py)│    Resolution, Priority, Satisfaction
  └────────┬──────────┘
           │
           ▼
  ┌─────────────────────────────┐
  │  HuggingFace Embeddings     │  ← all-MiniLM-L6-v2
  │  (sentence-transformers)    │    Lightweight, high semantic accuracy
  └────────┬────────────────────┘
           │
           ▼
  ┌───────────────────┐
  │  ChromaDB         │  ← Persistent local vector store
  │  (vectorstore/)   │    No cloud dependency
  └────────┬──────────┘
           │
           ▼
  ┌────────────────────────────┐
  │  User Query                │
  │  → Top-3 Similarity Search │
  └────────┬───────────────────┘
           │
           ▼
  ┌────────────────────────────────┐
  │  LLaMA 3.3-70B via Groq        │  ← Context-grounded answer generation
  │  RetrievalQA (chain="stuff")   │
  └────────┬───────────────────────┘
           │
     ┌─────┴──────┐
     ▼            ▼
┌─────────┐  ┌──────────────┐
│ FastAPI │  │  Streamlit   │
│  /ask   │  │  Chat UI     │
└─────────┘  └──────────────┘
```

---

## 📁 Project Structure

```
AI_Customer_Support_Bot_RAG_LLM/
│
├── my_data.csv                  # Customer support ticket dataset
│
├── vectorstore/                 # Persisted ChromaDB embeddings
│   └── chroma.sqlite3
│
├── rag_pipeline.py              # Core RAG logic: load → embed → retrieve → answer
├── app.py                       # FastAPI backend with /ask endpoint + middleware
├── streamlit_app.py             # Streamlit chat UI frontend
│
├── requirements.txt             # Python dependencies
└── README.md
```

---

## 🛠️ Tech Stack

| Layer | Tool | Reason |
|---|---|---|
| **Orchestration** | LangChain | Modular RAG chain with `RetrievalQA` |
| **LLM** | Groq — LLaMA 3.3-70B | Ultra-fast inference via LPU hardware |
| **Embeddings** | `all-MiniLM-L6-v2` | Lightweight, high semantic accuracy |
| **Vector Store** | ChromaDB | Persistent local indexing, no cloud dependency |
| **Backend API** | FastAPI | Async `/ask` GET endpoint with timing middleware |
| **Chat UI** | Streamlit | Stateful chat interface with session memory |
| **Data** | Pandas | CSV ingestion and row-to-document conversion |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- A free [Groq](https://console.groq.com/) API key

### 1. Clone the Repository

```bash
git clone https://github.com/Musawir456/AI_Customer_Support_Bot_RAG_LLM.git
cd AI_Customer_Support_Bot_RAG_LLM
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

> ⚠️ **Never commit your `.env` file.** Add it to `.gitignore`.

### 4. Add Your Data

Place your support ticket CSV as `my_data.csv` in the root directory. See [Data Format](#data-format) for required columns.

### 5. Run the Application

**Terminal 1 — Start the FastAPI backend:**
```bash
uvicorn app:app --reload
```

**Terminal 2 — Start the Streamlit chat UI:**
```bash
streamlit run streamlit_app.py
```

| Interface | URL |
|---|---|
| Streamlit Chat | http://localhost:8501 |
| FastAPI REST | http://localhost:8000 |
| Swagger Docs | http://localhost:8000/docs |

---

## 📡 API Reference

### `GET /ask`

Submit a natural language question and receive a grounded answer from the RAG pipeline.

**Query Parameter:**

| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | `string` | ✅ Yes | Your natural language question |

**Example Request:**
```bash
curl "http://localhost:8000/ask?query=show%20me%20tickets%20with%20satisfaction%20rating%3D5"
```

**Example Response (`200 OK`):**
```json
{
  "query": "show me tickets with satisfaction rating=5",
  "answer": "There is one ticket with a satisfaction rating of 5.0:\n\nTicket Type: Technical issue\nSubject: Product compatibility\nResolution: East degree with.\nPriority: High\nSatisfaction: 5.0"
}
```

**Error Response:**
```json
{
  "error": "Description of what went wrong"
}
```

---

## 📊 Data Format

Your `my_data.csv` must include these columns:

| Column | Description | Example |
|---|---|---|
| `Ticket Type` | Category of support issue | `Technical issue`, `Billing inquiry` |
| `Ticket Subject` | Brief issue title | `Product compatibility` |
| `Ticket Description` | Full issue description | `I'm having trouble with...` |
| `Resolution` | How the issue was resolved | `Issue escalated to tier-2 support` |
| `Ticket Priority` | Severity level | `Low`, `Medium`, `High` |
| `Customer Satisfaction Rating` | Post-resolution score (1–5) | `4.5` |

---

## 📸 Screenshots

### 💬 Streamlit Chat UI

**Billing Inquiry Query**

The bot returns a precise, data-grounded answer about billing ticket counts.

![Streamlit Chat - Billing](screenshots/pro2.PNG)

**Technical Issues Query**

The bot lists common subjects under Technical issues, retrieved directly from the vector store.

![Streamlit Chat - Technical](screenshots/pro.PNG)

---

### ⚡ FastAPI Swagger UI

**Query Input — `/ask` endpoint**

Natural language queries are submitted as a `query` parameter via Swagger UI.

![FastAPI Query](screenshots/pr2.PNG)

**Server Response — `200 OK`**

Structured JSON response with the grounded answer returned in milliseconds.

![FastAPI Response](screenshots/pr3.PNG)

---

## 🔧 How Vector Store Rebuild Works

The system is intelligent about when to rebuild embeddings:

```python
# On startup (app.py):
if os.path.exists("vectorstore"):
    vectordb = create_vectorstore(docs=None)   # ✅ Load existing — instant!
else:
    docs = load_data("my_data.csv")
    vectordb = create_vectorstore(docs)        # 🔨 Build fresh — one-time cost
```

To force a full rebuild with new data, delete the `vectorstore/` directory and restart:

```bash
rm -rf vectorstore/
uvicorn app:app --reload
```

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to your fork: `git push origin feature/your-feature-name`
5. Open a Pull Request

For major changes, please open an issue first to discuss your proposal.

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify, and distribute.

---

<div align="center">

Built with ❤️ by <a href="https://github.com/Musawir456">Musawir456</a>

⭐ **Star this repo if you found it helpful!**

</div>
