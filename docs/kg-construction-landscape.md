# Knowledge Graph Construction — Models & Benchmarks

Reference notes for KGCR-RAG-2026. Years are the first public release (arXiv preprint or
conference publication, whichever came first).

---

## 1. Models & Systems

### 1.1 LLM-based extraction pipelines

These are not single models but orchestration frameworks that wrap a general-purpose LLM
with prompting, chunking, entity resolution and summarization stages.

| System | Year | Venue / Source | What it does | Notes |
|---|---|---|---|---|
| AutoKG | 2023 | arXiv | Multi-agent LLM loop for schema induction + triple extraction | Early proof that LLMs can replace supervised IE |
| GraphRAG | 2024 | Microsoft Research | LLM extraction → Leiden community detection → hierarchical community summaries | Reference architecture for RAG-oriented KGs; expensive to index |
| LightRAG | 2024 | arXiv (Oct) | Dual-level (local + global) retrieval over an LLM-built graph | ~10x cheaper indexing than GraphRAG |
| nano-graphrag | 2024 | Open source | Minimal reimplementation of GraphRAG | Good baseline to fork |
| iText2KG | 2024 | WISE 2024 | Incremental, ontology-free KG building with built-in entity resolution | Handles streaming documents |
| Docs2KG | 2024 | arXiv | Heterogeneous document (PDF, HTML, email) → unified KG | Strong on layout-heavy sources |
| SAC-KG | 2024 | ACL 2024 | LLM as a domain-KG "generator + verifier" at million-triple scale | Self-correcting |
| TriX | 2024 | arXiv | Multi-pass self-consistent triple extraction | Reduces hallucinated relations |
| KGGen | 2025 | arXiv (Feb) | LLM extraction + clustering-based canonicalization | Ships with the MINE benchmark |

### 1.2 Fine-tuned / specialized extraction models

Cheap, self-hostable, deterministic. Usually BERT- or BART-sized.

| Model | Year | Venue | Task | Notes |
|---|---|---|---|---|
| REBEL | 2021 | EMNLP Findings | Seq2seq end-to-end relation extraction | BART-based; still a solid baseline |
| HittER | 2021 | EMNLP | Hierarchical transformer for KG embedding | — |
| OneRel | 2022 | AAAI | Joint extraction as a single one-module classification | SOTA-class on NYT / WebNLG |
| UniRel | 2022 | EMNLP | Unified entity–relation interaction representation | SOTA-class on NYT / WebNLG |
| mREBEL | 2023 | ACL | Multilingual REBEL, 18 languages | — |
| InstructUIE | 2023 | arXiv | Instruction-tuned universal information extraction | Flan-T5 backbone |
| UniversalNER | 2023 | ICLR 2024 | Targeted distillation from GPT for open NER | Outperforms its teacher on NER |
| YAYI-UIE | 2023 | arXiv | Chat-model UIE, strong Chinese support | — |
| GLiNER | 2024 | NAACL 2024 | Zero-shot NER with a bidirectional encoder | Runs on CPU; arbitrary entity types at inference |
| GLiREL | 2024 | NAACL 2025 | Zero-shot relation extraction, GLiNER-style | Natural pairing with GLiNER |
| ReLiK | 2024 | ACL 2024 | Joint entity linking + relation extraction, retriever–reader | Very fast; strong academic + practical tradeoff |

### 1.3 KG completion / link prediction

Different task: these take an existing (incomplete) graph and predict missing edges. Relevant
if your pipeline needs to densify a constructed KG.

| Model | Year | Venue | Notes |
|---|---|---|---|
| CompGCN | 2020 | ICLR | Composition-based multi-relational GCN |
| NBFNet | 2021 | NeurIPS | Neural Bellman-Ford; path-based, inductive |
| NodePiece | 2022 | ICLR | Anchor-based, parameter-efficient node vocabulary |
| ULTRA | 2023 | ICLR 2024 | Foundation model for KG reasoning; zero-shot transfer to unseen graphs |

---

## 2. Benchmark Datasets

### 2.1 End-to-end KG construction (LLM era)

| Benchmark | Year | What it measures |
|---|---|---|
| Text2KGBench | 2023 | Ontology-driven KG generation from text; Wikidata-TekGen (10 ontologies) + DBpedia-WebNLG (19 ontologies) splits. Metrics: triple F1, ontology conformance, hallucination rate |
| LLMs4OL | 2023 | LLM ability on ontology learning subtasks (term typing, taxonomy, relation extraction) |
| LLM-KG-Bench | 2023 | Automated eval of LLMs on RDF/SPARQL/Turtle manipulation tasks |
| KGQuiz | 2023 | Probes depth and breadth of factual knowledge encoded in LLMs |
| MINE (ships with KGGen) | 2025 | Measures information recovery from a constructed graph |


### 2.2 Downstream RAG-over-KG evaluation

Extrinsic evaluation — does the constructed KG actually improve answers?

| Dataset | Year | Notes |
|---|---|---|
| HotpotQA | 2018 | 2-hop multi-hop QA with supporting facts |
| 2WikiMultiHopQA | 2020 | Wikipedia + Wikidata, explicit reasoning paths |
| MuSiQue | 2022 | 2–4 hop, composed to resist shortcut reasoning; hardest of the three |
| CRAG | 2024 | Meta KDD Cup 2024; web + mock-KG retrieval, 5 domains |
| STaRK | 2024 | Retrieval over semi-structured KGs (product, academic, biomedical) |
| UltraDomain | 2024 | Long-context domain corpora; used by LightRAG / GraphRAG papers |

---

## 3. Recommended Evaluation Plan for KGCR-RAG-2026

**Intrinsic (is the graph correct?)**

1. **Text2KGBench** — ontology conformance and hallucination rate, since the pipeline is
   schema-driven.
2. **SciER** — if the target corpus is scientific papers.

**Extrinsic (does the graph help?)**

3. **MuSiQue** and **2WikiMultiHopQA** — multi-hop QA accuracy / EM / F1 with and without
   the KG in the retrieval loop.
---

## 4. Quick Reference — Links

- GraphRAG: <https://github.com/microsoft/graphrag>
- LightRAG: <https://github.com/HKUDS/LightRAG>
- GLiNER: <https://github.com/urchade/GLiNER>
- GLiREL: <https://github.com/jackboyla/GLiREL>
- ReLiK: <https://github.com/SapienzaNLP/relik>
- REBEL: <https://github.com/Babelscape/rebel>
- ULTRA: <https://github.com/DeepGraphLearning/ULTRA>
- Text2KGBench: <https://github.com/cenguix/Text2KGBench>
- MuSiQue: <https://github.com/StonyBrookNLP/musique>
