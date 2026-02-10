# Evaluation

This folder will contain evaluation protocols, scripts, and results for **TruPharma**.

Our evaluation will focus on **quality, reliability, and trust** (not just accuracy), including:
- citation precision / groundedness
- hallucination (unsupported claim) rate
- semantic mapping accuracy (colloquial → medical)
- latency and cost per query
- robustness testing (prompt injection / adversarial queries)

## Baselines (planned)
1. Standard LLM (no retrieval)
2. Vector-only RAG (no structured joins / no orchestration)
3. Hybrid RAG + governance + citations (target system)

## What will go here
- query sets (benchmark questions)
- human-in-the-loop rubric and annotation guide
- scripts to compute metrics and compare baselines
- results tables and summary writeups