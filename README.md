# ProofStack AI
### Production-Quality AI Research and Evidence Intelligence Platform
**Built for the Nebius x NVIDIA Global AI Hackathon**

> *"Intelligence is easy. Evidence is everything."*

ProofStack AI investigates complex questions, retrieves real-world web evidence, extracts factual claims, rigorously evaluates evidence support and contradictions, identifies boundaries of uncertainty, and generates transparent, source-backed research reports.

---

## 1. System Architecture

```text
User Interface (React + TypeScript + Tailwind CSS)
    ↓
Research Orchestrator (FastAPI / Express Backend)
    ├── 1. Research Decomposition (Breaks down query into empirical targets)
    ├── 2. Evidence Retrieval (Tavily Search API)
    ├── 3. Claim Extraction (NVIDIA Nemotron via Nebius Token Factory)
    ├── 4. Evidence Assessment (SUPPORTED | CONTRADICTED | MIXED | INSUFFICIENT EVIDENCE)
    ├── 5. Contradiction Analysis (Exposes conflicting cross-source claims)
    └── 6. Uncertainty & Epistemic Boundaries Report
    ↓
Validated Research Report & Source Explorer
    ↓
Interactive Research Dashboard
```

---

## 2. Evidence Assessment Philosophy

A citation is **never** treated as proof merely because a document was retrieved. ProofStack AI enforces strict separation between:
1. **Finding a source** (Relevance).
2. **Extracting an atomic factual claim** (Passage attribution).
3. **Evaluating whether the passage genuinely supports, refutes, or is ambiguous toward the claim**.
4. **Distinguishing empirical retrieved facts from model synthesis and recommendations**.

### Four Formal Evidence Labels:
- **`SUPPORTED`**: The available source passages directly and unequivocally substantiate the claim.
- **`CONTRADICTED`**: The available evidence directly refutes the claim with verifiable opposing findings.
- **`MIXED`**: Materially conflicting evidence exists across peer sources or testing methodologies.
- **`INSUFFICIENT EVIDENCE`**: The retrieved material does not establish the claim either way. *Lack of evidence is never presented as proof that a claim is false.*

---

## 3. Technology Stack

- **Frontend**: React 19, TypeScript, Tailwind CSS v4, Lucide Icons, Motion.
- **AI Model**: NVIDIA Nemotron (`nvidia/llama-3.1-nemotron-70b-instruct`) via **Nebius Token Factory**.
- **Web Search & Evidence Retrieval**: **Tavily Search API**.
- **Backend**:
  - Full-stack runtime via **Express + Vite middleware** (runs on port 3000 in unified container).
  - Standalone **Python FastAPI** service located in `/backend` with Pydantic validation schemas.
- **Database**: In-memory session store with PostgreSQL adapter configuration (`DATABASE_URL`).

---

## 4. Setup & Configuration

### A. Environment Variables (`.env`)
Copy `.env.example` to `.env` and configure your credentials:

```bash
# NEBIUS TOKEN FACTORY (NVIDIA NEMOTRON)
NEBIUS_API_KEY="your_nebius_api_key_here"
NEBIUS_BASE_URL="https://api.tokenfactory.nebius.ai/v1"
NEBIUS_MODEL="nvidia/llama-3.1-nemotron-70b-instruct"

# TAVILY WEB RESEARCH API
TAVILY_API_KEY="tvly-your_tavily_api_key_here"

# PERSISTENT DATABASE (Optional PostgreSQL)
DATABASE_URL="postgresql://user:password@localhost:5432/proofstack"
```

### B. Running the Web Application
```bash
npm install
npm run dev
# The full application is accessible at http://localhost:3000
```

### C. Running Standalone FastAPI Backend (Optional)
```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

---

## 5. Pre-Indexed Benchmark Mode (Zero-Failure Guarantee)

If API keys are not supplied during evaluation or network constraints arise:
- ProofStack AI provides an explicit, transparent **Pre-Indexed Benchmark Mode** using deterministic empirical research cases (such as SWE-bench open model comparisons and speculative decoding mathematical evaluations).
- All benchmark data is visibly labeled as `DEMO MODE (PRE-INDEXED BENCHMARK)` with genuine paper citations and verified benchmark scores.
- Live investigations run automatically as soon as Nebius and Tavily keys are configured.

---

## 6. License & Disclaimer
ProofStack AI is an open research tool. Retrieved quotes and summaries represent the content of external third-party sources.
