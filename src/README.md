# Source Code

This folder will contain the implementation for **TruPharma**.

TruPharma is designed as a Hybrid RAG system (structured + unstructured retrieval) with
grounded generation and governance rules to reduce hallucinations.

## What will go here
- ingestion pipeline (OpenFDA updates, labeling ingestion, refresh windows)
- retrieval layer (SQL + vector search, optional reranking)
- generation layer (grounded answers with citations)
- governance layer (refusal rules, prompt-injection defenses)
- prototype interface code (e.g., Streamlit app)