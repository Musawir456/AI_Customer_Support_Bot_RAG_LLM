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

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first.
