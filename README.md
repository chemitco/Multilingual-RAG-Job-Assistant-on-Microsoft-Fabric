# 🇮🇳 Multilingual RAG-Powered Virtual Assistant for Government Examination Preparation using Azure OpenAI, LangChain, and Microsoft Fabric Eventhouse

---

## 🧭 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [OpenAI Models Used](#openai-models-used)
- [Architecture](#architecture)
- [How It Works](#how-it-works)
- [Setup](#setup)
- [Dashboard](#dashboard)
- [Output](#output)
- [Conclusion](#conclusion)
- [License](#license)
- [Contributing](#contributing)

---

## 🌍 Overview

The **Multilingual RAG-Powered Virtual Assistant** is an AI-driven solution built using **Azure OpenAI**, **LangChain**, and **Microsoft Fabric Eventhouse**.  
It automates the ingestion of **PDF documents** from **official government websites** (via web scraping) and **manual uploads**, assisting students preparing for **government and competitive exams in India**.

This assistant provides **accurate, multilingual, and real-time** information such as notifications, eligibility, and exam schedules — directly from verified PDFs.

### 🎯 Advantages
- Fetches official, verified updates (UPSC, IBPS, SSC, etc.)
- Provides multilingual answers (English, Hindi, and others)
- Extracts both text and tables
- Reduces manual searching across sites
- Uses **Eventhouse** for scalable, vector-based search
- Avoids duplicates using stable `chunk_id`
- Combines **RAG + GPT** for context-based answers

---

## 🚀 Features

| Feature | Description |
|----------|--------------|
| 📄 PDF Ingestion | Extracts both text and tables from multiple PDFs |
| 🌐 Multilingual Support | Answers queries in several Indian languages |
| 🧠 RAG Architecture | Uses embeddings + GPT for contextual answers |
| 💾 Eventhouse Integration | Stores text, embeddings, and metadata |
| 🧾 Deduplication | Stable hash-based chunk identification |
| 📊 Dashboard | KQL-based ingestion and language insights |
| ⚡ Modular Design | Clear, reusable Fabric notebooks |

---

## 🧩 Prerequisites

You need access to:

- ✅ **Microsoft Fabric Account** (Lakehouse + Eventhouse)
- ✅ **Azure OpenAI Studio** (model deployment rights)
- ✅ **Deployed Azure OpenAI Resource** (GPT + embeddings)
- ✅ **Fabric Workspace Setup** (edit + contributor access)
- ✅ **Python Runtime** (Fabric or local conda environment)

---

## 🧠 OpenAI Models Used

| Model | Purpose | Description |
|--------|----------|-------------|
| **`text-embedding-ada-002`** | Embedding | Converts text and tables into dense numerical vectors for similarity-based search |
| **`gpt-4o` / `gpt-35-turbo`** | Language Model | Answers queries contextually using retrieved chunks from Eventhouse |

These models combine to create a **Retrieval-Augmented Generation (RAG)** pipeline that supports multilingual Q&A.

---

## 🏗️ Architecture

This system integrates **Azure OpenAI**, **LangChain**, and **Microsoft Fabric** components for an end-to-end RAG workflow.

![Architecture Diagram](images/architecture.png)

### Components
1. **Fabric Lakehouse** → stores PDFs and text extractions  
2. **Fabric Notebooks** → extract, chunk, embed, and upload data  
3. **Azure OpenAI** → generates embeddings and answers  
4. **Eventhouse DB** → stores embeddings and metadata  
5. **KQL Dashboard** → monitors ingestion and data metrics
---

## 💡 How It Works

The RAG pipeline consists of two main phases — **indexing** and **retrieval**.

### 🧱 Step 1: Processing the Files and Indexing the Embeddings

This step prepares and stores vector embeddings into **Fabric Eventhouse**.

1. **Read PDF documents** from Fabric Lakehouse  
2. **Extract both text and tables** using `PyPDFLoader` and `pdfplumber`  
3. **Generate embeddings** using the `text-embedding-ada-002` model  
4. **Store both text and embeddings** into Eventhouse (`embeddingtables`)

📸 *Add diagram:*  
![Processing and Indexing Flow](images/ingestion_flow.png)

---

### 💬 Step 2: RAG – Getting Answers

1. Convert the question into an embedding  
2. Search that embedding against Eventhouse vectors  
3. Retrieve top-matching chunks  
4. Combine them with the query and pass to **GPT-4o**  
5. GPT returns a fluent, multilingual answer  

📸 *Add diagram:*  
![RAG Retrieval Flow](images/query_flow.png)

---

## ⚙️ Setup

### 🧩 Step 1 – Create a Fabric Workspace  
Create a workspace named **GovExamAssistant** in Microsoft Fabric.

### 🧩 Step 2 – Create a Lakehouse  
Create a Lakehouse named `govexam-lakehouse` for storing PDFs and extracted data.

### 🧩 Step 3 – Upload PDFs  
Upload exam PDFs (IBPS, UPSC, DDA, SSC etc.) manually or from a scraping script to:

### 🧩 Step 4 – Create an Eventhouse  
Create an **Eventhouse** database named `govexam_eventhouse`.

### 🧩 Step 5 – Create the Embeddings Table  
Create a table named `embeddingtables` with columns:  
`doc_id, document_name, source_url, page_no, chunk_no, content, embedding, chunk_id, content_type, lang, ingest_time`

### 🧩 Step 6 – Import and Configure Notebooks  
Upload:
- `01_ingest_pdfs.ipynb` – extracts & splits data  
- `02_generate_embeddings.ipynb` – creates embeddings  
- `03_query_rag_engine.ipynb` – performs Q&A  

### 🧩 Step 7 – Connect to Eventhouse  
Set the following inside your notebook:

```python
KUSTO_URL = "<your-eventhouse-cluster-url>"
KUSTO_DATABASES = "govexam_eventhouse"
KUSTO_TABLES = "embeddingtables"



