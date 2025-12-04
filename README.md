# Sanskrit Document Retrieval-Augmented Generation (RAG) System


## Introduction:
This project implements a CPU-only Retrieval-Augmented Generation (RAG) pipeline for answering questions from Sanskrit documents.
The system retrieves relevant Sanskrit text chunks from the uploaded .docx document using semantic search (FAISS + SentenceTransformer) and generates answers through FLAN-T5-Large. Query input may be provided in Devanagari or IAST transliteration, both supported by automatic transliteration.

This repository contains:

Full Python implementation.

Sample Sanskrit document.

Technical report (PDF).

Instructions to reproduce and run the complete system.

## Features:
✔ Sanskrit DOCX ingestion

Reads docx files using python-docx.

✔ Automatic Unicode normalization

Cleans whitespace and irregular formatting.

✔ Intelligent Chunking

Chunk size: 800 characters

Stride: 400 characters

✔ Dual Transliteration Support

Devanagari → IAST

IAST → Devanagari

Uses indic-transliteration.

✔ Semantic Retrieval

Embedding model: paraphrase-multilingual-MiniLM-L12-v2

Vector store: FAISS IndexFlatIP (CPU)

✔ LLM-Based Generation

Model: google/flan-t5-large

Strict, context-only answering

Replies in Sanskrit

✔ CPU-Only Execution

No GPU needed.

## How the System Works:
1. Ingestion

Reads the Sanskrit .docx and extracts full text.

2. Preprocessing

Normalize whitespace

Chunk into overlapping sequences

Convert between Devanagari ↔ IAST

3. Embedding + Indexing

Generate sentence embeddings

Build FAISS vector index

4. Query Handling

Detect script (Devanagari / IAST)

Convert to Devanagari

Retrieve top-k similar chunks

5. Prompt Construction

Context + Query → Final prompt for FLAN-T5

6. Generation

Produces Sanskrit answer with strict grounding:

If context insufficient → returns "न विद्यते"

## Performance:

Embedding: ~5 seconds

Retrieval: ~30 ms

FLAN-T5-Large Generation: ~3–5 seconds

No GPU required
