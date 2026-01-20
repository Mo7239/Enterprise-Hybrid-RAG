# 🧠 Enterprise Hybrid RAG System

A production-oriented **Retrieval-Augmented Generation (RAG)** system designed to answer user questions accurately using external PDF documents, while minimizing hallucinations and maintaining strong observability and evaluation practices.

This project focuses on **clean architecture, modular design, and real-world engineering decisions**
---

## 🔍 Problem Statement

Large Language Models (LLMs) are powerful, but they often generate answers based on general knowledge rather than a specific source.  
This can lead to hallucinations, incorrect answers, or responses that are not grounded in the actual document provided by the user.

The challenge becomes even harder in **multi-turn conversations**, where follow-up questions depend on previous context and references.

---

## 💡 Solution Overview

This project implements a **hybrid RAG pipeline** that combines document retrieval, conversational memory, and systematic evaluation to produce accurate and grounded answers.

Key design principles:
- Strict separation between retrieval and generation
- Hybrid retrieval for better recall and precision
- Memory-aware conversations without polluting retrieval
- Full observability and evaluation using LangSmith

---

## 🏗️ System Architecture

```
User
 ↓
Conversation Memory (Window-based)
 ↓
Query Rewriting
 ↓
Hybrid Retriever (Dense + Sparse)
 ↓
Context Assembly
 ↓
LLM Generation (LLaMA 3.2 via Ollama)
 ↓
Evaluation & Observability (LangSmith)
```

---

## ⚙️ Core Components

### 🔹 Configuration Management
Centralized and immutable settings using data classes to control:
- LLM behavior
- Chunking strategy
- Embeddings
- Retrieval weights
- Memory window
- Observability

---

### 🔹 LLM Engine Abstraction
An abstraction layer that decouples model serving from the pipeline logic, allowing easy switching between LLM providers without changing the core system.

---

### 🔹 PDF Ingestion & Metadata Enrichment
Responsible for loading raw PDF documents and attaching consistent metadata such as:
- Source
- Page number
- Document type

No chunking or embedding logic is applied at this stage to keep the pipeline modular.

---

### 🔹 Semantic Chunking
Documents are split into semantically meaningful chunks using a recursive strategy, with configurable chunk size and overlap.  
Each chunk is enriched with metadata for traceability and debugging.

---

### 🔹 Hybrid Retrieval
A combination of:
- **Dense retrieval** (semantic similarity)
- **Sparse retrieval** (keyword-based)

Weighted fusion is used to balance recall and precision, producing high-quality context for the LLM.

---

### 🔹 Conversational Memory
A window-based memory mechanism is used to maintain conversational context across turns, while ensuring retrieval remains query-focused and unaffected by chat history.

---

## 📊 Evaluation & Observability

The system integrates **LangSmith** for full observability and evaluation.

Implemented evaluators:
- **Answer Relevance** – checks whether the answer addresses the user’s question
- **Context Groundedness** – ensures the answer is fully supported by the retrieved context

---



## 🛠️ Tech Stack

- Python
- LangChain
- LangSmith
- Ollama
- LLaMA 3.2
- Qwen 2.5

---

## 👨‍💻 Author

**Mohamed Wasef** [Linekd-in](https://www.linkedin.com/in/mohamed-wasef-789743233/) 

