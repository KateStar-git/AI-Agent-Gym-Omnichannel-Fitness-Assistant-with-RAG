
# 🍍 Papaya Gym: Automated Ingestion Pipeline & AI Customer Agent

A production-grade, data-driven AI Agent ecosystem built in **n8n**. This project automates the entire lifecycle of enterprise knowledge management: from dynamically fetching, chunking, and indexing new company assets from **Google Drive** into **Pinecone**, to serving that knowledge in real time via an intelligent **AI Support Agent Webhook**.

## 🏗️ System Architecture Overview

The project is split into two modular, highly scalable workflows:

[ Google Drive Folder ] ──(Scheduled Sync)──► [ Chunking & Embeddings ] ──► [ Pinecone DB ]
▲
│ (RAG Search)
[ Customer Webhook ] ────────────────────────► [ AI Agent Papaya ] ──────────────┘

## 🛠️ Project Components

### 1. The Knowledge Ingestion Pipeline (`Papaya Gym Vectore Store`)
This workflow eliminates manual data management by establishing an automated ETL (Extract, Transform, Load) pipeline for the AI's knowledge base.

* **Trigger:** Automated `Schedule Trigger` (Cron-based execution).
* **Data Ingestion:** Monitors and pulls the latest assets, documents, and gym rules from a designated Google Drive repository.
* **Text Processing:** Utilizes a `Recursive Character Text Splitter` to handle document chunking gracefully, preserving semantic context.
* **Vector Vectorization & Storage:** Streams chunks through OpenAI's embedding model and saves them directly into a **Pinecone Vector Store**.
* **Flow Control:** Implements a strict `Loop Over Items` mechanism to safely handle large batches of file uploads without hitting API rate limits.

### 2. The Customer Assistant (`Agent Papaya`)
An AI agent optimized to handle real-world user queries regarding gym offers, memberships, and facility regulations.

* **Interface:** Driven by a robust, non-blocking `Webhook` node to process incoming requests from any front-end app or messaging tool.
* **RAG Grounding:** Before formulating an answer, the `LangChain Agent` queries the Pinecone vector index to fetch exact, contextual information about "Papaya Gym".
* **Core Model:** Powered by `gpt-4.1-mini` to ensure rapid execution and highly precise tool orchestration.
## 🚀 Key Features

- **Automated Knowledge Sync**: No manual script execution needed to update the AI's brain. Simply drop a new PDF into Google Drive, and the schedule syncs it.
- **Enterprise Splitting**: Documents are recursively chunked to ensure that small, specific answers (like pricing lists) are not lost inside large documents.
- **Production-Ready Endpoints**: The agent is encapsulated behind a clean Webhook infrastructure, ready to be linked with website chat widgets, custom applications, or messaging channels.

## 🧰 Tech Stack

* **Automation Engine:** n8n
* **Vector Database:** Pinecone
* **LLM Engine:** OpenAI Core (`gpt-4.1-mini`) & OpenAI Embeddings
* **Cloud Storage Integration:** Google Drive API
* **Architecture Style:** Retrieval-Augmented Generation (RAG) & Event-Driven Microservices
