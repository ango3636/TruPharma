# TruPharma: A GenAI-Powered Verification Engine for Real-World Drug Safety

> **Course:** CS 5588 — Data Science Capstone  
> **Team:** **CiteRx Team**  
> **Primary Contact:** **Amy Ngo** (**https://github.com/ango3636**)  
> **Repository:** https://github.com/ango3636/TruPharma  
> **Proposal PDF:** `/proposal/DS_Capstone_Project_Proposal.pdf`

---

## Team

| Name | GitHub |
|------|--------|
| Nithin Songala | https://github.com/reddy-nithin |
| Salman Mirza | https://github.com/SalmanM1 |
| Amy Ngo | https://github.com/ango3636 |

**Team Name:** **CiteRx Team**  
**Primary Contact:** **Amy Ngo**

---

## Problem & Impact

There is a latency gap between **official drug safety profiles** (from controlled clinical trials / regulatory labeling) and **real-world drug safety** (what patients report post-market). The FDA FAERS dataset contains millions of adverse event reports, but the data is noisy, unstructured, and difficult to connect to official drug labeling.

**TruPharma** is a GenAI-driven system that reconciles:
- **Structured regulatory labeling** (NDC / labeling data), and
- **Unstructured post-market adverse event reports** (FAERS)

TruPharma supports two real-world workflows:

1) **Consumer “Check Engine” workflow (Safety Chat)**  
Users enter a drug + symptom in plain language. TruPharma returns a **verified assessment** grounded in both official labels and real-world case counts, with citations.

2) **Pharmacovigilance “Signal Detection” workflow (Signal Heatmap)**  
Analysts view a dashboard showing drugs with the highest disparity between official warnings and recent FAERS reports over a rolling window (e.g., last 90 days).

---

## High-Level GenAI Architecture

### 1) Data Ingestion & Knowledge Layer
- Automated pipeline to fetch updates (OpenFDA APIs)
- Chunking + embeddings for unstructured narratives
- Relational tables for structured labeling + metadata
- Versioning and provenance tracking (timestamps + refresh windows)

### 2) Retrieval (Hybrid)
- **Structured retrieval (SQL):** regulatory “ground truth”
- **Unstructured retrieval (Vector search):** FAERS narratives
- Optional reranking to improve relevance and reduce noise

### 3) Generation + Grounding
- LLM generates responses **only from retrieved evidence**
- Every response includes **citations to label sections and/or FAERS counts**
- “Insufficient evidence” behavior when retrieval is weak

### 4) Agentic Orchestration (Planned)
Multi-agent decomposition + reconciliation pattern:
- Agent A: extracts official label side effects
- Agent B: finds real-world report clusters
- Agent C: verifies disparity and summarizes grounded result

### 5) Interface & Human-in-the-Loop
- Streamlit app (in Snowflake) for Safety Chat
- Signal Heatmap dashboard (Streamlit/Tableau/Power BI)
- User flagging + analyst validation to create feedback loops

---

## Data Sources

- **OpenFDA (Adverse Events + Labeling APIs)**  
  https://open.fda.gov/apis/drug/  
  Use: primary source for labels + FAERS-based evidence, grounding, and ongoing updates.

- **RxNorm (NLM)**  
  https://www.nlm.nih.gov/research/umls/rxnorm/  
  Use: normalization + entity resolution (brand → ingredient → codes) for consistent retrieval.

- **DrugBank (v5.1.14)**  
  https://go.drugbank.com/  
  Use: drug–drug interactions + clinical context to support explanations (license-dependent).

- **BLUE Benchmark (optional evaluation support)**  
  https://github.com/ncbi-nlp/BLUE_Benchmark  
  Use: benchmarking for clinical NLP tasks (mapping / NER / relation signals).

See `/data/` for more.

---

## Methods, Technologies & Tools (Planned)

- **Data Platform:** Snowflake (single source of truth)
- **Vector Search:** Snowflake Cortex Search (or equivalent)
- **Orchestration:** Snowflake Cortex (agentic workflow) + Python
- **Ingestion:** Snowpark Container Services / scheduled pipelines
- **UI:** Streamlit (in Snowflake) + optional BI tool for dashboards
- **Collaboration:** GitHub, issues, updates in `/docs/updates/`

---

## Evaluation Plan

We evaluate **quality, reliability, and trust** (not just “accuracy”).

### Baselines
- **Baseline 1:** vanilla LLM (no retrieval)
- **Baseline 2:** vector-only RAG (no agentic orchestration / no structured joins)
- **Target:** hybrid RAG (structured + vector) + governance + citations (+ optional reranking)

### Metrics (planned)
- **Citation precision / groundedness:** are claims supported by cited evidence?
- **Hallucination rate:** unsupported claims frequency
- **Semantic mapping accuracy:** colloquial → medical term mapping success
- **Latency + cost per query:** real-time feasibility
- **Robustness:** prompt injection / adversarial inputs

Evaluation scripts + protocols live in `/evaluation/`.

---

## Governance & Safety Rules (MVP)

TruPharma is a **decision-support prototype**, not medical advice.
The system will:
- Provide **evidence-grounded summaries with citations**
- Refuse unsafe requests (diagnosis, emergency instructions, personalized dosing)
- Recommend professional consultation for medical decisions
- Detect and block prompt injection attempts and policy violations

Governance rules and prompt templates are maintained in `/docs/governance/`.

---

## Repository Structure

See below for the required directory layout. All deliverables, artifacts, and updates are versioned here throughout the semester.

---

## How to Run (Coming Soon)

Setup and run instructions will be added after Phase 1 ingestion + baseline RAG are implemented.

Planned:
- `pip install -r requirements.txt`
- `python src/ingest/ingest_openfda.py`
- `streamlit run src/app/streamlit_app.py`

---

## Deliverables

By end of semester:
- Working GenAI prototype (Safety Chat + Signal Heatmap)
- Live demo
- Full repo with code, prompts, evaluation scripts, governance docs
- Final technical report (architecture + experiments + lessons learned)