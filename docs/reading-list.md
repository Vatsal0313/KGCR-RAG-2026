# Reading List & Datasets per Pod

Materials for the three pods (P1 Construction, P2 Graph & Reasoning, P3 RAG & Evaluation).
Each pod has a **Must-read** set (finish in weeks 1–2), an **Extended** set (reference during
implementation), and the **datasets** that pod is responsible for loading.

---

## 0. Everyone reads these first (week 1)

| # | Paper | Year | Why |
|---|---|---|---|
| 0.1 | Pan et al., *Unifying Large Language Models and Knowledge Graphs: A Roadmap* (IEEE TKDE) | 2024 | Single best framing of the whole LLM↔KG space. Defines the vocabulary the team will use. |
| 0.2 | Peng et al., *Graph Retrieval-Augmented Generation: A Survey* | 2024 | Covers the P3 half and how it depends on P1/P2 output quality. |
| 0.3 | Mihindukulasooriya et al., *Text2KGBench* (ISWC) | 2023 | Our primary intrinsic benchmark — everyone must understand its metrics. |

---

## P1 — Construction (S1, S2)

### Must-read

| # | Paper | Year | Source |
|---|---|---|---|
| 1.1 | Zhong et al., *A Comprehensive Survey on Automatic Knowledge Graph Construction* (ACM CSUR) | 2023 | <https://dl.acm.org/doi/pdf/10.1145/3618295> |
| 1.1 | Huguet Cabot & Navigli, *REBEL: Relation Extraction By End-to-end Language generation* | 2021 | |
| 1.2 | Zaratiana et al., *GLiNER: Generalist Model for NER using Bidirectional Transformer* | 2024 | |
| 1.3 | Boylan et al., *GLiREL: Generalist Model for Zero-Shot Relation Extraction* | 2024 | |
| 1.4 | Orlando et al., *Retrieve, Read and LinK (ReLiK)* | 2024 | |
| 1.5 | Edge et al., *From Local to Global: A Graph RAG Approach* | 2024 | |

### Extended

| # | Paper | Year | Note |
|---|---|---|---|
| 1.1 | Lairgi et al., *iText2KG* (WISE) | 2024 | Incremental construction + built-in entity resolution |
| 1.2 | Mo et al., *KGGen* | 2025 | Clustering-based canonicalization; ships MINE benchmark |
| 1.3 | Zhou et al., *UniversalNER / Targeted Distillation* (ICLR) | 2024 | How to distill GPT-quality NER into a small local model |
| 1.4 | Wadhwa et al., *Revisiting Relation Extraction in the era of LLMs* (ACL) | 2023 | Sobering: LLMs underperform fine-tuned models on standard RE |

### P1 datasets

| Dataset | Year | Use in our project | Source |
|---|---|---|---|
| **SciER** | 2024 | Primary — document-level scientific entity+relation | <https://github.com/edzq/SciER> |
| **Re-DocRED** | 2022 | Document-level triple F1; use instead of DocRED | <https://github.com/tonytan48/Re-DocRED> |
| **Text2KGBench** | 2023 | Ontology conformance + hallucination rate | <https://github.com/cenguix/Text2KGBench> |
| SciERC | 2018 | Smaller sanity-check set, same domain | <http://nlp.cs.washington.edu/sciIE/> |
| WebNLG+ | 2020 | Standard comparison point vs. REBEL/UniRel | <https://gitlab.com/shimorina/webnlg-dataset> |
| CoNLL04 | 2004 | Tiny, clean; good for unit tests | bundled in most RE toolkits |
| CrossRE | 2022 | Domain-transfer stress test | <https://github.com/mainlp/CrossRE> |

**P1 week-1 concrete task:** load SciER, run the existing spaCy extractor on it, and record
precision/recall/F1. That number is the floor for the entire project.

---

## P2 — Graph & Reasoning (S3, S4)

### Must-read — S3 (canonicalization + persistence)

| # | Paper | Year | Venue | Relevance |
|---|---|---|---|---|
| 2.1 | Vashishth et al., *CESI: Canonicalizing Open Knowledge Bases using Embeddings and Side Information* | 2018 | WWW | The canonical (pun intended) open-KB canonicalization method |
| 2.2 | Wu et al., *Scalable Zero-shot Entity Linking with Dense Entity Retrieval* (BLINK) | 2020 | EMNLP | Bi-encoder + cross-encoder EL; the practical default |
| 2.3 | De Cao et al., *Autoregressive Entity Retrieval* (GENRE) | 2021 | ICLR | Generative EL; constrained decoding over entity names |
| 2.4 | Li et al., *Deep Entity Matching with Pre-Trained Language Models* (Ditto) | 2020 | VLDB | Entity resolution from the DB community — more practical than the NLP framing |

### Must-read — S4 (reasoning)

| # | Paper | Year | Venue | Relevance |
|---|---|---|---|---|
| 2.5 | Vashishth et al., *CompGCN* | 2020 | ICLR | Baseline multi-relational GNN |
| 2.6 | Zhu et al., *Neural Bellman-Ford Networks* | 2021 | NeurIPS | Path-based, inductive, interpretable |
| 2.7 | Galkin et al., *Towards Foundation Models for KG Reasoning* (ULTRA) | 2023 | ICLR 2024 | Zero-shot transfer — works on **our** graph with no training |
| 2.8 | Luo et al., *Reasoning on Graphs (RoG): Faithful and Interpretable LLM Reasoning* | 2023 | ICLR 2024 | Plan-then-retrieve over KG paths; direct input to P3 |
| 2.9 | Sun et al., *Think-on-Graph* | 2023 | ICLR 2024 | LLM agent walking the KG; the main alternative to 2.8 |

### Extended / specs

| # | Resource | Note |
|---|---|---|
| 2.10 | W3C **SHACL** spec | Constraint validation — this is how S4 proves the graph is consistent |
| 2.11 | W3C **OWL 2 RL** profile | Rule-based entailment that is actually tractable |
| 2.12 | Ren et al., *Query2Box* (ICLR 2020) | Complex logical queries in embedding space |
| 2.13 | Ji et al., *A Survey on Knowledge Graphs: Representation, Acquisition, Applications* (TNNLS 2022) | Broad reference |
| 2.14 | Neo4j Graph Data Science docs / Apache Jena docs | Pick one and read the modelling guide before designing the schema |

### P2 datasets

| Dataset | Year | Use | Source |
|---|---|---|---|
| **CESI ReVerb45K / Base / Ambiguous** | 2018 | Canonicalization eval — directly measures S3's module | <https://github.com/malllabiisc/cesi> |
| **AIDA-CoNLL** | 2011 | Entity linking accuracy | via GERBIL <http://gerbil.aksw.org/> |
| ZESHEL | 2019 | Zero-shot EL, unseen domains | <https://github.com/lajanugen/zeshel> |
| OPIEC | 2019 | Large open-IE triple corpus for canonicalization at scale | <https://www.uni-mannheim.de/dws/research/resources/opiec/> |
| **FB15k-237** | 2015 | Link prediction sanity check | standard, bundled with PyKEEN |
| **WN18RR** | 2018 | Link prediction, leakage-free | standard, bundled with PyKEEN |
| CoDEx (s/m/l) | 2020 | Harder LP with real negatives | <https://github.com/tsafavi/codex> |
| ILPC 2022 | 2022 | Inductive LP — matches our "new documents arrive" setting | <https://github.com/pykeen/ilpc2022> |

**Tooling:** use **PyKEEN** for link prediction baselines rather than reimplementing. ULTRA
ships pretrained checkpoints — run those before training anything.

**P2 week-1 concrete task:** stand up Neo4j in Docker, define the `GraphStore` ABC with S7,
and load the toy graph from [output.json](output.json) into it.

---

## P3 — RAG & Evaluation (S5, S6)

### Must-read — S5 (retrieval + generation)

| # | Paper | Year | Venue | Relevance |
|---|---|---|---|---|
| 3.1 | Lewis et al., *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks* | 2020 | NeurIPS | The origin paper. Non-negotiable. |
| 3.2 | Karpukhin et al., *Dense Passage Retrieval* (DPR) | 2020 | EMNLP | The vector-RAG baseline we must beat |
| 3.3 | Edge et al., *GraphRAG* | 2024 | MSR | Shared with P1 — read the query-time half |
| 3.4 | He et al., *G-Retriever: RAG for Textual Graph Understanding and QA* | 2024 | NeurIPS | Subgraph retrieval as a Steiner-tree problem. Most directly reusable. |
| 3.5 | Gutiérrez et al., *HippoRAG* | 2024 | NeurIPS | Personalized PageRank over a KG for multi-hop. Strong, cheap. |
| 3.6 | Asai et al., *Self-RAG* | 2023 | ICLR 2024 | Retrieval with self-critique — the quality ceiling trick |

### Must-read — S6 (evaluation)

| # | Paper | Year | Venue | Relevance |
|---|---|---|---|---|
| 3.7 | Trivedi et al., *MuSiQue: Multihop Questions via Single-hop Question Composition* | 2022 | TACL | Our hardest extrinsic benchmark; read how shortcuts are blocked |
| 3.8 | Ho et al., *2WikiMultiHopQA* | 2020 | COLING | Has explicit reasoning paths — lets us evaluate the KG, not just the answer |
| 3.9 | Es et al., *RAGAS: Automated Evaluation of RAG* | 2024 | EACL | Faithfulness / answer-relevance / context-precision metrics |
| 3.10 | Saad-Falcon et al., *ARES: Automated Evaluation Framework for RAG* | 2024 | NAACL | Adds confidence intervals; use for the final table |
| 3.11 | Liu et al., *Lost in the Middle* | 2024 | TACL | Why context ordering changes results — affects every number S6 reports |

### Extended

| # | Paper | Year | Note |
|---|---|---|---|
| 3.12 | Gao et al., *RAG for LLMs: A Survey* | 2023 | Navigational map of the design space |
| 3.13 | Yang et al., *HotpotQA* (EMNLP) | 2018 | Easier warm-up multi-hop set |
| 3.14 | Yang et al., *CRAG: Comprehensive RAG Benchmark* | 2024 | KDD Cup 2024; realistic noisy retrieval |
| 3.15 | Wu et al., *STaRK* | 2024 | Retrieval over semi-structured KGs |
| 3.16 | Jin et al., *Long-context LLMs Meet RAG* | 2024 | Needed to answer "why not just use a 1M-token context?" |

### P3 datasets

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
