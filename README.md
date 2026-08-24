# RAG Using LangChain

A comprehensive collection of Retrieval-Augmented Generation (RAG) implementations using LangChain with various LLMs, vector stores, and deployment options.

## Project Overview

This project demonstrates multiple RAG architectures and implementations including:
- **Simple RAG** with various document loaders (Text, PDF, Web)
- **API Server** using FastAPI + LangServe
- **Streamlit Chatbots** with OpenAI, Ollama, Groq, and HuggingFace
- **Vector Stores**: FAISS, ObjectBox, Cassandra/AstraDB
- **Embeddings**: OpenAI, Ollama, HuggingFace (BGE)
- **Agents** with Wikipedia, Arxiv, and custom retriever tools

---

## Project Structure

```
rag_using_langchain/
├── requirements.txt              # Python dependencies
├── README.md                     # This file
├── LICENSE
├── .gitignore
│
├── api/                          # FastAPI + LangServe REST API
│   ├── app.py                    # API server with OpenAI & Ollama endpoints
│   └── client.py                 # Streamlit client for API
│
├── chatbot/                      # Streamlit chatbot implementations
│   ├── app.py                    # OpenAI GPT-3.5-turbo chatbot
│   └── localama.py               # Ollama Llama2 chatbot
│
├── rag/                          # Simple RAG notebooks
│   ├── simplerag.ipynb           # Basic RAG with Text, Web, PDF loaders
│   ├── attention.pdf             # "Attention Is All You Need" paper
│   └── speech.txt                # Sample text document
│
├── openai/                       # OpenAI GPT-4o RAG
│   └── GPT4o_Lanchain_RAG.ipynb  # RAG with ObjectBox vector store
│
├── groq/                         # Groq + Llama3/Mixtral RAG
│   ├── app.py                    # Streamlit app with FAISS + Web loader
│   ├── llama3.py                 # Streamlit app with FAISS + PDF loader
│   └── groq.ipynb                # Notebook with AstraDB/Cassandra
│
├── objectbox/                    # ObjectBox vector store demo
│   ├── app.py                    # Streamlit app with PDF documents
│   ├── .env                      # Environment variables
│   └── us_census/                # PDF documents (US Census data)
│
├── huggingface/                  # HuggingFace embeddings + local LLMs
│   ├── huggingface.ipynb         # FAISS + BGE embeddings + Mistral
│   └── us_census/                # PDF documents (US Census data)
│
├── agents/                       # LangChain Agents
│   └── agents.ipynb              # OpenAI Functions Agent with tools
│
└── chain/                        # Retriever & Chain examples
    ├── retriever.ipynb           # PDF loading, splitting, retrieval
    └── attention.pdf             # "Attention Is All You Need" paper
```

---

## Prerequisites

- Python 3.10+
- pip or conda
- API Keys (as needed):
  - **OpenAI API Key** - for OpenAI models/embeddings
  - **Groq API Key** - for Groq models (Llama3, Mixtral)
  - **LangChain API Key** - for LangSmith tracing (optional)
  - **HuggingFace Token** - for HuggingFace Hub models (optional)
  - **AstraDB Token** - for Cassandra vector store (optional)

---

## Installation

### Bash (Linux/macOS/Git Bash)

```bash
# Clone the repository
git clone <repository-url>
cd rag_using_langchain

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# For Jupyter notebooks
pip install jupyter ipykernel
python -m ipykernel install --user --name=rag-langchain --display-name "RAG LangChain"
```

### PowerShell (Windows)

```powershell
# Clone the repository
git clone <repository-url>
cd rag_using_langchain

# Create virtual environment
python -m venv venv
.\venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt

# For Jupyter notebooks
pip install jupyter ipykernel
python -m ipykernel install --user --name=rag-langchain --display-name "RAG LangChain"
```

---

## Environment Configuration

Create a `.env` file in the project root (or in specific subdirectories as needed):

```bash
# Required for OpenAI models
OPENAI_API_KEY=your_openai_api_key_here

# Required for Groq models
GROQ_API_KEY=your_groq_api_key_here

# Optional: LangSmith tracing
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=your_langchain_api_key_here

# Optional: HuggingFace
HUGGINGFACEHUB_API_TOKEN=your_hf_token_here
```

### PowerShell (create .env)

```powershell
@"
OPENAI_API_KEY=your_openai_api_key_here
GROQ_API_KEY=your_groq_api_key_here
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=your_langchain_api_key_here
"@ | Set-Content -Path .env -Encoding UTF8
```

---

## Running the Applications

### 1. API Server (FastAPI + LangServe)

**Terminal 1 - Start Server:**
```bash
# Bash
cd api
python app.py

# PowerShell
cd api
python app.py
```
Server runs at `http://localhost:8000`
- `/openai` - Direct OpenAI chat
- `/essay` - Essay generation (OpenAI)
- `/poem` - Poem generation (Ollama Llama2)

**Terminal 2 - Run Streamlit Client:**
```bash
# Bash
cd api
streamlit run client.py

# PowerShell
cd api
streamlit run client.py
```
Client runs at `http://localhost:8501`

**Prerequisites:** Ollama must be installed and running for `/poem` endpoint:
```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh  # Linux
# Or download from https://ollama.com/download

# Pull Llama2 model
ollama pull llama2

# Start Ollama server
ollama serve
```

### 2. Chatbot - OpenAI (chatbot/app.py)

```bash
# Bash
cd chatbot
streamlit run app.py

# PowerShell
cd chatbot
streamlit run app.py
```
Runs at `http://localhost:8501` - Simple chat with GPT-3.5-turbo

### 3. Chatbot - Ollama Llama2 (chatbot/localama.py)

```bash
# Bash
cd chatbot
streamlit run localama.py

# PowerShell
cd chatbot
streamlit run localama.py
```
Runs at `http://localhost:8501` - Chat with local Llama2 via Ollama

**Prerequisites:** Ollama running with `llama2` model pulled.

### 4. Groq + Llama3 RAG (groq/llama3.py)

```bash
# Bash
cd groq
streamlit run llama3.py

# PowerShell
cd groq
streamlit run llama3.py
```
Runs at `http://localhost:8501` - RAG with PDF documents (US Census data), FAISS vector store, Llama3-8b-8192

**Features:**
- Click "Documents Embedding" to build vector store
- Query PDF documents with citations

### 5. Groq + Mixtral RAG (groq/app.py)

```bash
# Bash
cd groq
streamlit run app.py

# PowerShell
cd groq
streamlit run app.py
```
Runs at `http://localhost:8501` - RAG with web content (LangSmith docs), FAISS + Ollama embeddings, Mixtral-8x7b

### 6. ObjectBox Vector Store (objectbox/app.py)

```bash
# Bash
cd objectbox
streamlit run app.py

# PowerShell
cd objectbox
streamlit run app.py
```
Runs at `http://localhost:8501` - RAG with PDF documents, ObjectBox vector store, OpenAI embeddings, Llama3-8b-8192

**Features:**
- Click "Documents Embedding" to build ObjectBox database
- Query with document similarity search expander

### 7. HuggingFace Embeddings + Local LLM (huggingface/huggingface.ipynb)

Open in Jupyter:
```bash
# Bash
cd huggingface
jupyter notebook huggingface.ipynb

# PowerShell
cd huggingface
jupyter notebook huggingface.ipynb
```

**Features:**
- Loads PDF documents from `us_census/`
- Uses `BAAI/bge-small-en-v1.5` embeddings (384-dim)
- FAISS vector store
- Mistral-7B via HuggingFace Hub
- RetrievalQA chain with custom prompt

### 8. OpenAI GPT-4o RAG (openai/GPT4o_Lanchain_RAG.ipynb)

Open in Jupyter:
```bash
# Bash
cd openai
jupyter notebook GPT4o_Lanchain_RAG.ipynb

# PowerShell
cd openai
jupyter notebook GPT4o_Lanchain_RAG.ipynb
```

**Features:**
- WebBaseLoader for LangSmith documentation
- ObjectBox vector store with OpenAI embeddings
- GPT-4o model
- RetrievalQA with LangChain Hub prompt

### 9. Simple RAG Examples (rag/simplerag.ipynb)

Open in Jupyter:
```bash
# Bash
cd rag
jupyter notebook simplerag.ipynb

# PowerShell
cd rag
jupyter notebook simplerag.ipynb
```

**Covers:**
- TextLoader (speech.txt)
- WebBaseLoader (Lilian Weng's blog)
- PyPDFLoader (attention.pdf)
- Text splitting with RecursiveCharacterTextSplitter

### 10. Retriever & Chain (chain/retriever.ipynb)

Open in Jupyter:
```bash
# Bash
cd chain
jupyter notebook retriever.ipynb

# PowerShell
cd chain
jupyter notebook retriever.ipynb
```

**Covers:**
- PDF loading and chunking
- Document splitting with overlap
- Basic retrieval pipeline

### 11. Agents (agents/agents.ipynb)

Open in Jupyter:
```bash
# Bash
cd agents
jupyter notebook agents.ipynb

# PowerShell
cd agents
jupyter notebook agents.ipynb
```

**Features:**
- OpenAI Functions Agent
- Tools: Wikipedia, Arxiv, Custom Retriever (LangSmith docs)
- FAISS vector store with OpenAI embeddings
- Verbose agent execution tracing

### 12. Groq + AstraDB (groq/groq.ipynb)

Open in Jupyter:
```bash
# Bash
cd groq
jupyter notebook groq.ipynb

# PowerShell
cd groq
jupyter notebook groq.ipynb
```

**Features:**
- WebBaseLoader for Lilian Weng's blog
- Cassandra/AstraDB vector store
- OpenAI embeddings
- Mixtral-8x7b-32768 via Groq
- Retrieval chain with custom prompt

---

## Key Components Explained

### Document Loaders
| Loader | Use Case | Example |
|--------|----------|---------|
| `TextLoader` | Plain text files | `speech.txt` |
| `PyPDFLoader` | Single PDF | `attention.pdf` |
| `PyPDFDirectoryLoader` | Multiple PDFs | `us_census/` folder |
| `WebBaseLoader` | Web pages | LangSmith docs, Lilian Weng blog |

### Text Splitters
- **RecursiveCharacterTextSplitter** - Default, chunk_size=1000, chunk_overlap=200
- Preserves semantic boundaries (paragraphs, sentences)

### Vector Stores
| Store | Type | Embeddings | Use Case |
|-------|------|------------|----------|
| FAISS | In-memory | OpenAI, Ollama, HuggingFace | Quick prototyping |
| ObjectBox | Embedded DB | OpenAI | Local persistence |
| Cassandra/AstraDB | Cloud DB | OpenAI | Production scale |

### Embedding Models
| Model | Dimensions | Provider | Notes |
|-------|------------|----------|-------|
| `text-embedding-3-small` | 1536 | OpenAI | Default OpenAI |
| `nomic-embed-text` | 768 | Ollama | Local, requires Ollama |
| `BAAI/bge-small-en-v1.5` | 384 | HuggingFace | Local, fast, good quality |

### LLMs
| Model | Provider | API Key | Notes |
|-------|----------|---------|-------|
| GPT-3.5-turbo | OpenAI | Required | Fast, cheap |
| GPT-4o | OpenAI | Required | Best quality |
| Llama2 | Ollama | None | Local, 7B params |
| Llama3-8b-8192 | Groq | Required | Very fast inference |
| Mixtral-8x7b-32768 | Groq | Required | MoE, high quality |
| Mistral-7B | HuggingFace | Optional | Local or Hub |

---

## API Endpoints (api/app.py)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/openai/invoke` | POST | Direct OpenAI chat |
| `/essay/invoke` | POST | Generate 100-word essay |
| `/poem/invoke` | POST | Generate 100-word poem (Llama2) |

**Request Format:**
```json
{
  "input": {
    "topic": "your topic here"
  }
}
```

**Response Format:**
```json
{
  "output": {
    "content": "generated text"
  }
}
```

---

## Troubleshooting

### Common Issues

**1. ModuleNotFoundError**
```bash
# Ensure virtual environment is activated
# Bash
source venv/bin/activate
# PowerShell
.\venv\Scripts\Activate.ps1

# Reinstall requirements
pip install -r requirements.txt
```

**2. API Key Errors**
- Verify `.env` file exists in correct directory
- Check API key validity at respective provider dashboards
- Ensure no extra spaces/quotes in `.env`

**3. Ollama Connection Refused**
```bash
# Start Ollama server
ollama serve

# Verify model is pulled
ollama list
# Should show llama2

# Pull if missing
ollama pull llama2
```

**4. Port Already in Use**
```bash
# Kill process on port 8000
# Bash
lsof -ti:8000 | xargs kill -9
# PowerShell
Get-Process -Id (Get-NetTCPConnection -LocalPort 8000).OwningProcess | Stop-Process -Force

# Or use different port in app.py
uvicorn.run(app, host="localhost", port=8001)
```

**5. FAISS/ObjectBox Import Errors**
```bash
# Reinstall with specific versions
pip install faiss-cpu==1.7.4
pip install langchain-objectbox==0.1.0
```

**6. HuggingFace Model Download Issues**
```bash
# Set cache directory
export HF_HOME=/path/to/cache  # Bash
$env:HF_HOME = "C:\path\to\cache"  # PowerShell

# Or login
huggingface-cli login
```

---

## Dependencies (requirements.txt)

```
langchain_openai 
langchain_core
python-dotenv
streamlit
langchain_community
langserve
fastapi
uvicorn
sse_starlette
bs4
pypdf
chromadb
faiss-cpu
groq
cassio
beautifulsoup4
langchain-groq
wikipedia
arxiv
langchainhub
sentence_transformers
PyPDF2
langchain-objectbox
```


## Resources

- [LangChain Documentation](https://python.langchain.com/)
- [LangServe Documentation](https://github.com/langchain-ai/langserve)
- [Streamlit Documentation](https://docs.streamlit.io/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Ollama](https://ollama.com/)
- [Groq](https://groq.com/)
- [ObjectBox](https://objectbox.io/)
- [AstraDB](https://www.datastax.com/astra)
- [HuggingFace](https://huggingface.co/)