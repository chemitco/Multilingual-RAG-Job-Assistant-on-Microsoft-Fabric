# 🌐 Multilingual RAG-Powered Virtual Assistant using Azure OpenAI and Microsoft Fabric Eventhouse

---

## 📚 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Data Flow](#data-flow)
- [Setup and Configuration](#setup-and-configuration)
  - [1️⃣ Prerequisites](#1️⃣-prerequisites)
  - [2️⃣ Environment Setup](#2️⃣-environment-setup)
  - [3️⃣ Ingest PDFs into Fabric Lakehouse](#3️⃣-ingest-pdfs-into-fabric-lakehouse)
  - [4️⃣ Generate and Store Embeddings](#4️⃣-generate-and-store-embeddings)
  - [5️⃣ Create KQL Dashboards](#5️⃣-create-kql-dashboards)
- [KQL Dashboard Examples](#kql-dashboard-examples)
- [Sample Outputs](#sample-outputs)
- [Conclusion](#conclusion)
- [License](#license)
- [Contributing](#contributing)

---

## 🌍 Overview

The **Multilingual RAG-Powered Virtual Assistant** is an AI-driven solution built using **Azure OpenAI**, **LangChain**, and **Microsoft Fabric Eventhouse**.  
It enables users to upload and query multilingual documents — PDFs containing both **text and tables** — while storing embeddings and metadata in **Fabric Eventhouse** for scalable retrieval and visualization.

This assistant can:
- Process PDFs (official circulars, recruitment notices, or reports)
- Extract both **text** and **tables**
- Generate **multilingual embeddings**
- Store them in **Fabric Eventhouse**
- Provide interactive analytics via **KQL dashboards**

---

## 🚀 Features

- 🗂️ **PDF Text & Table Extraction** using `PyPDFLoader` and `pdfplumber`
- 💬 **Multilingual Embedding Support** (`sentence-transformers`, `Azure OpenAI`)
- 🧠 **Semantic Search / RAG** using stored embeddings
- 📊 **KQL + Power BI Dashboards** for monitoring document ingestion and embedding stats
- 🧾 **Deduplication & Incremental Uploads** (no duplicate embeddings)
- ☁️ **Fabric Integration**: Eventhouse, Lakehouse, OneLake
- 🔒 **Secure**: Uses Fabric tokens for access control
- 🧩 **Extensible**: Ready for integration with chatbots or QnA apps

---

## 🏗️ Architecture

> 📸 **Place your architecture screenshot here**  
> Save it in your repo at: `images/architecture.png`

Example:
```markdown
![System Architecture](images/architecture.png)
