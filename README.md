# 📄 Legal Document Question Answering using RAG

This project demonstrates how to build a **Retrieval-Augmented Generation (RAG)** pipeline using LangChain and OpenAI to answer questions from legal documents such as NDAs, acquisition agreements, and privacy policies.

---

## 🎯 Objective

- To process and analyse legal text documents from various subdomains.
- To build a RAG-based question-answering pipeline using LangChain.
- To evaluate the model’s performance on a benchmark dataset using ROUGE, BLEU, and optionally RAGAS scores.

---

## 🗂️ Dataset

- **Corpus**: 4 types of legal contracts in `.txt` format:
  - `contractnli/`
  - `cuad/`
  - `maud/`
  - `privacy_qa/`
- **Benchmarks**: JSON files with legal questions under the `"tests"` key, each containing a `"query"` field.

---

## 🧪 Workflow

### 1. Data Loading & Cleaning
- Extracted `.txt` files from a zip.
- Loaded all text files recursively using `DirectoryLoader`.
- Preprocessed the text by:
  - Removing emails, phone numbers, and special characters.
  - Lowercasing, removing stopwords, and trimming extra spaces.

### 2. Exploratory Data Analysis (EDA)
- Calculated document length stats.
- Found most/least frequent words using `nltk`.
- Used TF-IDF and cosine similarity to identify redundant contracts.

### 3. Document Chunking
- Used `RecursiveCharacterTextSplitter` with chunk size = 500, overlap = 100.

### 4. Embedding and Vector Database
- Used `OpenAIEmbeddings` to embed chunks.
- Stored vectors in **Chroma** or **FAISS** vector DB.
- Persisted vector DB locally for reuse.

### 5. RAG Chain Construction
- Combined retriever and `ChatOpenAI` into a `RetrievalQA` chain.
- Supported question-answering with source document tracing.

### 6. Benchmark Evaluation
- Extracted 6,889 benchmark questions from JSON.
- Created a function to evaluate RAG answers against ground truths.
- Metrics: **ROUGE-L**, **BLEU**.
- Ran evaluation on top 100 questions due to compute constraints.

---

## 📊 Evaluation Results

| Metric     | Score     |
|------------|-----------|
| ROUGE-L    | 0.0000    |
| BLEU       | 0.0000    |

> ⚠️ Most benchmark questions had no ground truth answers, hence evaluation scores are limited.

---

## 💡 Conclusions

- RAG pipeline successfully retrieved relevant legal context and generated informative responses.
- Chunking, embedding, and retrieval worked well on legal text.
- Evaluation was constrained by lack of answers in the benchmark set.
- With better-annotated data, this pipeline can scale to contract review, compliance monitoring, and legal chatbots.

---

## 🚀 Future Improvements

- Use domain-specific LLMs or fine-tuned models for legal text.
- Expand benchmark set with high-quality human-annotated answers.
- Integrate semantic metrics (BERTScore, RAGAS) where applicable.

---

## 🛠️ Technologies Used

- Python, Colab, LangChain, OpenAI API
- FAISS / Chroma for vector DB
- ROUGE & BLEU for evaluation
- NLTK, sklearn, tqdm, dotenv

---
