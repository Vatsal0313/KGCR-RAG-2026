# Reading List & Datasets per Pod

Materials for the three pods (P1 Construction, P2 Graph & Reasoning, P3 RAG & Evaluation).
Each pod has a **Must-read** set (finish in weeks 1–2), an **Extended** set (reference during
implementation), and the **datasets** that pod is responsible for loading.

---

## 0. Everyone reads these first

| # | Paper | Year | Source |
|---|---|---|---|
| 0.1 | Pan et al., *Unifying Large Language Models and Knowledge Graphs: A Roadmap* (IEEE TKDE) | 2024 | |
| 0.2 | Peng et al., *Graph Retrieval-Augmented Generation: A Survey* | 2024 | |
| 0.3 | Lewis et al., *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks* | 2020 | <https://dl.acm.org/doi/pdf/10.5555/3495724.3496517> |

---

## P1 — KG Construction from Text

### Must-read

| # | Paper | Year | Source |
|---|---|---|---|
| 1.1 | Zhong et al., *A Comprehensive Survey on Automatic Knowledge Graph Construction* (ACM CSUR) | 2023 | <https://dl.acm.org/doi/pdf/10.1145/3618295> |
| 1.1 | Mihindukulasooriya et al., *Text2KGBench: A Benchmark for Ontology-Driven Knowledge Graph Generation from Text* | 2023 | <https://dl.acm.org/doi/abs/10.1007/978-3-031-47243-5_14> |
| 1.2 | Tiwari et al., *Ontology-Aware Prompting for Knowledge Graph Construction from Text* | 2026 | <https://ebooks.iospress.nl/volumearticle/80576> |
| 1.3 | Lermanda et al., *Evaluating Knowledge Graph Construction from Text Without Supervision* | 2026 | <https://dl.acm.org/doi/10.1007/978-3-032-25156-5_2> <https://drive.google.com/file/d/1O139AZ9FUdVBlvRUErFIo8k1OtQ6neV4/view?pli=1> |

### P1 datasets

| Dataset | Year | Source |
|---|---|---|
| **Text2KGBench** | 2023  | <https://github.com/cenguix/Text2KGBench> |
| **bigs-unsupervised** | 2026 |  <https://github.com/MaxOjeda/bigs-unsupervised/> |

---

## P2 — KG Reasoning and RAG 

### Must-read — S5 (retrieval + generation)

| # | Paper | Year | Source |
|---|---|---|---|
| 3.1 | Lewis et al., *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks* | 2020 | NeurIPS | The origin paper. Non-negotiable. |
| 3.3 | Edge et al., *GraphRAG* | 2024 | MSR | Shared with P1 — read the query-time half |
| 3.4 | He et al., *G-Retriever: RAG for Textual Graph Understanding and QA* | 2024 | NeurIPS | Subgraph retrieval as a Steiner-tree problem. Most directly reusable. |

### Must-read — S6 (evaluation)

| # | Paper | Year | Venue | Relevance |
|---|---|---|---|---|
| 3.7 | Trivedi et al., *MuSiQue: Multihop Questions via Single-hop Question Composition* | 2022 | TACL | Our hardest extrinsic benchmark; read how shortcuts are blocked |
| 3.8 | Ho et al., *2WikiMultiHopQA* | 2020 | COLING | Has explicit reasoning paths — lets us evaluate the KG, not just the answer |
| 3.9 | Es et al., *RAGAS: Automated Evaluation of RAG* | 2024 | EACL | Faithfulness / answer-relevance / context-precision metrics |
| 3.10 | Saad-Falcon et al., *ARES: Automated Evaluation Framework for RAG* | 2024 | NAACL | Adds confidence intervals; use for the final table |
| 3.11 | Liu et al., *Lost in the Middle* | 2024 | TACL | Why context ordering changes results — affects every number S6 reports |

### P2 datasets

| Dataset | Year | Use | Source |
|---|---|---|---|
| **MuSiQue** | 2022 | Primary extrinsic benchmark (2–4 hop) | <https://github.com/StonyBrookNLP/musique> |
| **2WikiMultiHopQA** | 2020 | Secondary; reasoning-path supervision | <https://github.com/Alab-NII/2wikimultihop> |
| HotpotQA | 2018 | Warm-up / debugging | <https://hotpotqa.github.io/> |
| CRAG | 2024 | Robustness to noisy retrieval | <https://github.com/facebookresearch/CRAG> |
| STaRK | 2024 | If we add a product/biomed domain | <https://github.com/snap-stanford/stark> |
| UltraDomain | 2024 | Used by LightRAG/GraphRAG — needed for fair comparison | released with LightRAG |

**P3 week-1 concrete task:** build the eval harness against **stub** graph data from S7. Report
vanilla DPR-RAG numbers on MuSiQue before any KG exists. That is the ablation baseline.

---

## Shared infrastructure the pods should not rebuild

| Need | Use | Not |
|---|---|---|
| Link prediction baselines | **PyKEEN** | custom TransE |
| Entity/relation models | **HuggingFace** + GLiNER/GLiREL/ReLiK repos | from scratch |
| Vector store | **FAISS** or **Qdrant** | custom index |
| Graph store | **Neo4j** (Docker) or **Apache Jena Fuseki** | pickled networkx |
| RAG eval | **RAGAS** | hand-rolled LLM-judge prompts |
| Experiment tracking | **Weights & Biases** or a CSV + git | screenshots in a chat group |

---

## Suggested reading schedule

| Week | P1 | P2 | P3 |
|---|---|---|---|
| 1 | 0.1–0.4, 1.1–1.3 | 0.1–0.4, 2.1–2.2 | 0.1–0.4, 3.1–3.2 |
| 2 | 1.4–1.5, 1.12 | 2.5, 2.7, SHACL | 3.3–3.5, 3.7–3.8 |
| 3 | 1.6–1.8 | 2.3–2.4, 2.8–2.9 | 3.9–3.11 |
| 4+ | as needed | as needed | as needed |

One paper per pod per week after week 3, presented in the Thursday sync in 10 minutes.
