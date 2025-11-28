# Sistema RAG - Regulamento FACOM/UFMS

Sistema de Retrieval-Augmented Generation (RAG) para responder perguntas sobre o regulamento da pós-graduação da FACOM/UFMS, com avaliação de factualidade usando Fact Score.

## 📋 Pré-requisitos

- Conta Groq (API gratuita)
- PDF do regulamento FACOM/UFMS

## 🚀 Como Executar

Execute os notebooks na seguinte ordem:

### 1️⃣ Extração do PDF
**Notebook:** `pdf_facom_resolucao_pos_ufms.ipynb`

**Output:** `/content/texto.txt` (texto limpo do PDF)

---

### 2️⃣ Geração de Embeddings
**Notebook:** `embedding_facom_resolucao_pos_ufms.ipynb`

**Output:** 
- `/content/chunks.json` (trechos do texto)
- `/content/embeddings.npy` (vetores de embedding)
- `/content/meta.json` (metadados)

---

### 3️⃣ Indexação no ChromaDB
**Notebook:** `chromadb_facom_resolucao_pos_ufms.ipynb`

**Output:** `/content/chroma_db/` (banco vetorial)

---

### 4️⃣ Reranking
**Notebook:** `rerank_facom_resolucao_pos_ufms.ipynb`
---

### 5️⃣ Sistema RAG Completo com Fact Score
**Notebook:** `rag_full.ipynb`
---
---

## 🛠️ Tecnologias Utilizadas

- **Extração**: PyMuPDF, pdfplumber
- **Chunking**: LangChain RecursiveCharacterTextSplitter
- **Embeddings**: sentence-transformers (paraphrase-multilingual-MiniLM-L12-v2)
- **Vector DB**: ChromaDB
- **Reranking**: Cross-Encoder (ms-marco-MiniLM-L-6-v2)
- **LLM**: Llama 3.3 70B (via Groq)
- **Fact Score**: Decomposição + Verificação com LLM

---

## ⚙️ Configurações Recomendadas

- **chunk_size**: 1000 caracteres
- **chunk_overlap**: 200 caracteres
- **retrieve_k**: 20 documentos
- **final_k**: 3 documentos (após reranking)
- **temperature**: 0.3 (RAG) / 0.5 (chat livre)
- **device**: "cuda" (com GPU) / "cpu" (sem GPU)

---

## 📈 Métricas

O sistema rastreia:
- Total de mensagens
- Tokens consumidos
- Fact Score por resposta
- Fact Score médio da sessão
- Afirmações suportadas vs não suportadas

---
