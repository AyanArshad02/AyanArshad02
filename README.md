<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=58A6FF&center=true&vCenter=true&width=700&lines=GenAI+Engineer+%40+Softeon;Building+reliable+production+RAG+%26+agentic+systems;Multi-tenant+%C2%B7+Observable+%C2%B7+Cost-governed" alt="Typing SVG" />

### Md Ayan Arshad &nbsp;·&nbsp; Data Scientist &nbsp;·&nbsp; IIT Madras

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/md-ayan-arshad-740288248/)
[![Portfolio](https://img.shields.io/badge/Portfolio-FF5722?style=for-the-badge&logo=google-chrome&logoColor=white)](https://ayanarshad02.github.io)
[![Dev.to](https://img.shields.io/badge/Dev.to-0A0A0A?style=for-the-badge&logo=devdotto&logoColor=white)](https://dev.to/ayanarshad02)
[![YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@MLwithAyanIITM)
[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ayanarshad2002@gmail.com)

</div>

---

## About

I'm a Data Scientist at **Softeon**, working on production multi-tenant RAG and conversational AI for enterprise supply chain software — while finishing my BS at IIT Madras. My focus is on the engineering side: making GenAI reliable, observable, and cost-predictable in systems real users depend on.

Before Softeon, I shipped a GPT-powered LinkedIn outreach system at Second Brain Labs and taught Python and ML to 100+ students at Antern. Building things and explaining them clearly have both been part of the work from the start.

---

## Currently

```text
Role     →  Data Scientist · Softeon, Chennai (Full-time)
College  →  IIT Madras · BS Data Science · Expected Nov–Dec 2026
Focus    →  Production RAG · Agentic AI · GenAI System Design
Open to  →  Remote GenAI/ML roles · US/EU timezones
```

---

## Highlights

- **Converted internship → full-time** at Softeon while still in college; end-to-end ownership of production multi-tenant RAG pipelines serving real enterprise customers
- Built a kapa.ai-inspired **multi-tenant RAG platform** from scratch - 10 Docker containers, hybrid search, MCP server, Prometheus/Grafana observability
- Cross-encoder reranking improved **Context Precision by +0.15** (measured with RAGAS); grounding validation runs as a blocking step
- RAGAS eval tied to CI/CD with **auto-rollback on quality drop**; golden query set per tenant, nightly + per-ingestion runs
- IIT Madras Topper Badges in Python, Bash, ML (Rank 106 / 1700+, Score 93/100)
- Mentored **100+ students** in Python & ML · Launched two free cohort-based courses (PY001 & PY002)

---

## Featured Projects

### 🔹 [kapa-inspired RAG MCP System](https://github.com/AyanArshad02/kapa-inspired-rag-mcp)

**The problem:** Developer-tool companies use products like [kapa.ai](https://kapa.ai) to power AI assistants over their docs, GitHub repos, and PDFs. I wanted to understand what it actually takes to build something like this with real multi-tenancy and observability, so I built it.

**What I shipped:** A production-grade, multi-tenant RAG platform across 10 Docker containers, with an MCP server that exposes the full pipeline as a native tool for Claude Desktop.

| Layer                    | What it does                                                                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Ingestion**      | Docs (BeautifulSoup + HeadingAwareChunker), GitHub repos (AST-based code chunker), PDFs (pymupdf4llm) → Celery async workers         |
| **Query pipeline** | SHA-256 cache → hybrid search (RRF fusion of dense + sparse) → Cohere reranker (top-20 → top-5) → GPT-4o-mini via SSE stream      |
| **Multi-tenancy**  | Separate Qdrant collection per tenant · Redis cache keyed by `sha256(tenant_id + query)` · API keys stored as SHA-256 hash only   |
| **Freshness**      | HMAC-verified GitHub webhooks (~10s incremental vs ~8min full re-index) · 6h Celery Beat polling · atomic S3 + DB cleanup on delete |
| **MCP Server**     | `search_knowledge_base` (full pipeline) + `fetch_and_query_online_docs` (ephemeral, zero Qdrant writes) — stdio + SSE transport  |
| **Observability**  | Prometheus + Grafana · LangSmith traces · RAGAS eval (faithfulness + context precision per source type)                             |

**Architecture:**

![System Architecture](hld-architecture.png)

**Key decisions and why:**

- **RRF over weighted sum** — rank-based fusion avoids calibrating incomparable dense/sparse score scales
- **Per-tenant Qdrant collections over shared + filter** — hard isolation, zero query overhead, independent scaling
- **`acks_late=True` on Celery tasks** — task stays on queue until ACK; no silent data loss if a worker crashes mid-job

**What I'd do differently:** Proper React frontend instead of Streamlit, and per-tenant cost dashboards built in from day one.

`FastAPI` `Qdrant` `Redis` `PostgreSQL` `Celery` `OpenAI` `Cohere` `FastMCP` `Docker` `RAGAS` `Streamlit`

---

### 🔹 Production Multi-Tenant RAG · Softeon *(proprietary)*

Enterprise RAG powering conversational AI for supply chain software, used by real customers.

- Pinecone namespace isolation per tenant — no shared collection, no filter overhead, independent scaling per client
- Cross-encoder reranking (top-10 → top-3); inline grounding validation as a **blocking** step before any response is returned
- RAGAS eval on nightly + per-ingestion runs; golden query set tied to CI/CD with auto-rollback on quality drop
- Circuit breakers + fallback LLM routing; context drift and embedding distribution shift detection
- Stack: OpenAI · Anthropic Claude · AWS Bedrock · FastAPI · AWS (EC2, Lambda, DynamoDB, SQS, Cognito, ECR, CloudWatch)

---

### 🔹 LinkedIn Outreach Chatbot · Second Brain Labs *(proprietary)*

GPT-powered outreach system integrated with the LinkedIn API. Handled live campaign traffic across multiple client accounts — automated lead qualification and multi-turn conversation flows.

`GPT-4` `LinkedIn API` `Python`

---

<details>
<summary>Older Projects</summary>

### 🔹 [MLOps Vehicle Insurance Predictor](https://github.com/AyanArshad02/MLOps-Vehicle-Insurance-Predictor)

End-to-end MLOps pipeline: data ingestion → training → deployment on AWS EC2.

`MongoDB` `Docker` `FastAPI` `AWS EC2` `CI/CD`

---

### 🔹 [MLOps Credit Card Fraud Detection](https://github.com/AyanArshad02/Credit-Fraud-Detection)

Real-time fraud detection pipeline with full MLOps instrumentation and alerting.

`AWS` `Kubernetes` `Prometheus` `Grafana` `DVC` `MLflow` `Dagshub`

---

### 🔹 [Email Marketing Campaign Optimization](https://github.com/AyanArshad02/email-marketing-campaign-optimization-using-ML)

ML-driven campaign optimization with an A/B testing framework for maximizing click-through rates.

</details>

---

## Tech Stack

**GenAI / RAG**

![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white)
![Anthropic Claude](https://img.shields.io/badge/Anthropic%20Claude-CC785C?style=flat-square&logoColor=white)
![AWS Bedrock](https://img.shields.io/badge/AWS%20Bedrock-FF9900?style=flat-square&logo=amazonaws&logoColor=white)
![Cohere](https://img.shields.io/badge/Cohere-39594D?style=flat-square&logoColor=white)
![RAGAS](https://img.shields.io/badge/RAGAS-4B8BBE?style=flat-square&logoColor=white)

**Vector Databases & Storage**

![Pinecone](https://img.shields.io/badge/Pinecone-000000?style=flat-square&logoColor=white)
![Qdrant](https://img.shields.io/badge/Qdrant-DC244C?style=flat-square&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)

**Cloud & Infrastructure**

![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat-square&logo=amazonaws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Celery](https://img.shields.io/badge/Celery-37814A?style=flat-square&logo=celery&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white)

**Languages & ML**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-AA4A44?style=flat-square&logoColor=white)
![ZenML](https://img.shields.io/badge/ZenML-431D93?style=flat-square&logoColor=white)
![MLflow](https://img.shields.io/badge/MLflow-0194E2?style=flat-square&logo=mlflow&logoColor=white)

---

## Journey

Joined IIT Madras in 2022 with one goal: get hired in industry before graduating, without relying on campus placements. Spent the first six months stuck in a Python tutorial loop — kept re-learning the basics without shipping anything. Breaking out of that by doing real projects changed the trajectory.

First internship was at Second Brain Labs in Sep 2024, shipping a production chatbot. Took on ML teaching at Antern at the same time. Joined Softeon as a data science intern in May 2025, converted to full-time by August — while still two years from graduation.

---

## Content & Community

I write about what I've actually shipped — production RAG failures, multi-tenancy trade-offs, GenAI system design — on LinkedIn and Medium.

- ✍️ [LinkedIn](https://linkedin.com/in/md-ayan-arshad-740288248/) — RAG failures, eval pipelines, AI NFRs, career lessons
- 📝 [Dev.to](https://dev.to/ayanarshad02) — technical deep-dives
- 🎥 [YouTube](https://www.youtube.com/@MLwithAyanIITM) — ML content
- 👨‍🏫 Mentored 100+ students · PY001 & PY002 free cohort-based Python courses

---

## GitHub Stats

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=AyanArshad02&show_icons=true&theme=github_dark&hide_border=true&count_private=true" height="165" alt="GitHub Stats"/>
 
<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=AyanArshad02&layout=compact&theme=github_dark&hide_border=true" height="165" alt="Top Languages"/>

<br/>

<img src="https://streak-stats.demolab.com/?user=AyanArshad02&theme=github-dark-blue&hide_border=true" height="165" alt="GitHub Streak"/>

</div>

---

<div align="center">

**Open to remote GenAI/ML engineering roles (US/EU timezones).**
If you're building production AI systems or just want to talk shop about RAG/agents, feel free to reach out.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/md-ayan-arshad-740288248/)
[![Portfolio](https://img.shields.io/badge/Portfolio-FF5722?style=for-the-badge&logo=google-chrome&logoColor=white)](https://ayanarshad02.github.io)
[![Dev.to](https://img.shields.io/badge/Dev.to-0A0A0A?style=for-the-badge&logo=devdotto&logoColor=white)](https://dev.to/ayanarshad02)
[![YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@MLwithAyanIITM)
[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ayanarshad2002@gmail.com)

</div>
