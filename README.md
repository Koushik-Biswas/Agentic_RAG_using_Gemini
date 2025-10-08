# Agentic RAG with Gemini Flash Thinking

This Streamlit application showcases an agentic Retrieval-Augmented Generation (RAG) pipeline built around Google96s Gemini 2.0 Flash Thinking and Gemini exp models, Qdrant for vector storage, and the Agno agent framework (formerly PhiData). It combines document understanding, intelligent query rewriting, and optional web search to deliver comprehensive, source-grounded responses.

## ✨ Features

- **Document Processing**
  - PDF uploads with automatic chunking and embedding
  - Web page ingestion using BeautifulSoup filtering
  - Persistent vector storage in Qdrant Cloud
- **Intelligent Querying**
  - Gemini-powered query reformulation for better recall
  - Similarity threshold filtering to control relevance
  - Dynamic fallback to web search when database answers are insufficient
  - Source attribution with snippet previews
- **Advanced Capabilities**
  - Exa AI integration with optional domain whitelisting
  - Context-aware response generation from Gemini 2.0 Flash Thinking
  - Chat history persistence and manual reset controls

## 🧰 Tech Stack

- [Streamlit](https://streamlit.io/) for the interactive UI
- [Agno](https://github.com/agno-ai/agno) agent framework
- Google [Gemini API](https://ai.google.dev/) (chat + embeddings)
- [Qdrant Cloud](https://qdrant.tech/) vector database
- [Exa](https://exa.ai/) web search API (optional)

## 🚀 Getting Started

### 1. Prerequisites

- Python 3.10+
- Accounts and API keys for Google Gemini, Qdrant, and optionally Exa

### 2. Install dependencies

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 3. Launch the app

```powershell
streamlit run .\agentic_rag_gemini.py
```

## 🔑 Configuration

All runtime credentials are managed from the Streamlit sidebar:

1. Enter your **Google API key** (required)
2. Provide **Qdrant Cloud URL** and **API key** (required for vector storage)
3. Optionally toggle web search and supply your **Exa API key**
4. Adjust the similarity threshold or custom domain list to fine-tune retrieval behavior

## 📚 Usage Flow

1. **Upload Data**
   - Drop PDFs into the uploader or paste URLs to ingest external content
   - Processed sources appear in the sidebar for quick reference
2. **Ask Questions**
   - Type queries into the chat input; the system rewrites them for optimal retrieval
   - Relevant documents are surfaced first; the app falls back to Exa search if needed
3. **Review Answers & Sources**
   - Responses cite whether they used internal documents or web results
   - Expand the source list to preview supporting text snippets

## 🧪 Development Notes

- Environment variables: the script mirrors sidebar values into `os.environ` for Gemini SDK compatibility.
- The `GeminiEmbedder` class centralizes embedding generation to keep Qdrant ingest consistent.
- Query rewriting, web search, and RAG responses each operate via dedicated Agno agents for clarity and composability.

## ☁️ Deploying to Streamlit Cloud

1. Push this project to GitHub (or another Git provider supported by Streamlit).
2. In [Streamlit Community Cloud](https://streamlit.io/cloud), create a new app and point it at the repository and branch containing this project.
3. Add a `requirements.txt` reference when prompted (already included in the repo).
4. Configure secrets:
   - In the Streamlit Cloud dashboard, open **App → Settings → Secrets**.
   - Paste a TOML block such as:

     ```toml
     google_api_key = "your-google-api-key"
     qdrant_api_key = "your-qdrant-api-key"
     qdrant_url = "https://your-cluster.cloud.qdrant.io:6333"
     exa_api_key = "your-exa-api-key"
     ```

   - These values load automatically into the sidebar when the app starts.
5. Deploy. The app will spin up with the latest commits; you can redeploy anytime by pushing to the tracked branch.

<img width="1830" height="920" alt="image" src="https://github.com/user-attachments/assets/00b542dd-625d-4d03-9d01-2dad7d3953c5" />

### Local secrets during development

Create a `.streamlit/secrets.toml` file (ignored by git) with the same TOML structure above to prefill keys when running `streamlit run` locally.

If you prefer not to maintain a secrets file during local development, set environment variables (`GOOGLE_API_KEY`, `QDRANT_API_KEY`, `QDRANT_URL`, `EXA_API_KEY`). The app now falls back to these values when a secrets file is absent.

## ✅ Quality Checklist

- `agentic_rag_gemini.py` free of unsupported Agno arguments (`show_tool_calls` removed)
- `requirements.txt` includes `google-genai` and `exa_py`
- README captures setup, configuration, and feature overview

## 📄 License
All Rights Reserved to Koushik Biswas@2025.
