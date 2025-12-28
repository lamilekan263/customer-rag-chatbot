# AI Customer Support Chatbot

An end-to-end **Retrieval-Augmented Generation (RAG)** powered customer support chatbot built with **LangChain**, **FAISS**, and **Ollama**. The application ingests company documentation (PDFs), indexes them into a vector database, and provides accurate, context-grounded answers to customer queries using a local LLM.

---

## ✨ Features

- 📄 **Document Ingestion**: Load and parse PDF documents from a directory
- ✂️ **Smart Text Chunking**: Recursive text splitting with configurable chunk size and overlap
- 🔎 **Semantic Search**: FAISS-based vector similarity search
- 🧠 **Local LLM Inference**: Powered by Ollama (Gemma model)
- 💬 **Conversational Memory**: Context-aware, multi-turn question answering
- 📚 **Source-Aware Responses**: Optionally return source documents with answers
- 🔒 **Offline-Friendly**: No external API calls required when using local embeddings and LLMs

---

## 🏗️ Architecture Overview

The application follows a modular RAG pipeline:

1. **Document Loading**  
   PDFs are loaded from a directory using `PyPDFLoader`.

2. **Text Splitting**  
   Documents are split into semantically meaningful chunks using a `RecursiveCharacterTextSplitter`.

3. **Embedding Generation**  
   Chunks are embedded using SentenceTransformer embeddings.

4. **Vector Storage**  
   Embeddings are stored and queried using FAISS.

5. **Retrieval + Generation**  
   Relevant chunks are retrieved and passed to an LLM via a structured prompt.

6. **Conversational Chain**  
   A `ConversationalRetrievalChain` maintains chat history and context across turns.

---

## 🧩 Project Structure

```text
.
├── data/                          # PDF documents used as knowledge base
├── DocumentLoader.py              # Handles loading PDFs and directories
├── DocumentTextSplitterManager.py # Manages recursive text splitting
├── EmbeddingManager.py            # Initializes embedding providers
├── main.py / notebook.ipynb       # RAG pipeline execution
├── requirements.txt
└── README.md
```

---

## 🚀 Getting Started

### 1. Prerequisites

- Python 3.9+
- Ollama installed locally
- A supported Ollama model (e.g. `gemma3:1b`)

Install Ollama and pull the model:

```bash
ollama pull gemma3:1b
```

---

### 2. Installation

Clone the repository and install dependencies:

```bash

git clone https://github.com/lamilekan263/customer-rag-chatbot.git
cd customer-rag-chatbot
pip install -r requirements.txt
```

---

### 3. Add Your Documents

Place your customer support PDFs inside the `data/` directory:

```text
data/
 ├── faq.pdf
 ├── return_policy.pdf
 └── shipping_info.pdf
```

---

### 4. Run the Application

Execute the ragchat notebook:



The chatbot will:

- Load and chunk documents
- Build a FAISS vector index
- Answer customer support questions using retrieved context

---

## 🧪 Example Questions

```text
- What is your refund policy?
- How long does standard delivery take?
- How can I contact customer support?
```

---

## 🧠 Prompting Strategy

The chatbot uses a **strict context-grounded system prompt**:

- Answers are generated **only** from retrieved documents
- If the answer is missing, the bot responds with:
  > "I don't know based on the retrieved documents."

This ensures reliability and prevents hallucinations.

---

## ⚙️ Configuration

### Text Splitting

```python
DocumentTextSplitterManager(
    chunk_size=100,
    chunk_overlap=20
)
```

### Embeddings

Default embedding model:

```text
thenlper/gte-small
```

### Retriever

```python
retriever = vectorDb.as_retriever(search_kwargs={"k": 8})
```

---

## 🔮 Future Improvements

- Support for additional document types (DOCX, TXT, HTML)
- Streaming responses
- Web UI (Streamlit / Next.js)
- Hybrid search (BM25 + Vector)
- Evaluation metrics for retrieval quality

---

## 🛡️ Limitations

- Answer quality depends on document quality
- Large PDFs may require tuning chunk sizes
- Local LLM performance depends on hardware

---

## 📄 License

This project is licensed under the MIT License.

---

## 👤 Author

**Ibrahim**  
AI / Machine Learning Engineer

---