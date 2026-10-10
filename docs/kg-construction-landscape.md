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
| Graphusion | 2024 | arXiv | Global fusion of locally extracted subgraphs | Targets scientific concept maps |
| TriX | 2024 | arXiv | Multi-pass self-consistent triple extraction | Reduces hallucinated relations |
| KGGen | 2025 | arXiv (Feb) | LLM extraction + clustering-based canonicalization | Ships with the MINE benchmark |

**Frontier LLMs commonly used as the extraction backbone** (structured output / JSON schema
mode is essential): GPT-4.1 and o-series (OpenAI), Claude Opus / Sonnet (Anthropic),
Gemini 2.5 (Google), Qwen3 and Llama 4 for self-hosted setups.

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

### 2.1 Sentence-level relation / joint extraction

| Dataset | Year | Size | Relations | Notes |
|---|---|---|---|---|
| ACE04 / ACE05 | 2004 / 2005 | ~450 docs | 6–7 types | Licensed (LDC); newswire + broadcast |
| CoNLL04 | 2004 | 1.4k sents | 5 | Small, clean, human-annotated |
| NYT / NYT-10 | 2010 | 1.1M sents | 24 | Distant supervision; noisy but standard |
| ADE | 2012 | 4.3k sents | 1 (adverse drug event) | Biomedical binary relation |
| TACRED | 2017 | 106k sents | 41 | Crowd-annotated; label noise issues |
| WebNLG | 2017 | 25k triple-sets | 246 (WebNLG+) | DBpedia triples ↔ text; WebNLG+ released 2020 |
| SciERC | 2018 | 500 abstracts | 7 | AI/NLP paper abstracts; entities + relations + coref |
| FewRel | 2018 | 70k instances | 100 | Few-shot RE; FewRel 2.0 (domain adaptation) in 2019 |
| REBEL dataset | 2021 | ~6M sents | 220+ | Wikipedia ↔ Wikidata; pretraining scale |
| Re-TACRED | 2021 | 91k sents | 40 | Relabeled TACRED, ~8% of original labels were wrong |
| CrossRE | 2022 | 5.3k sents | 17 | Six domains; cross-domain generalization |

### 2.2 Document-level extraction

| Dataset | Year | Size | Notes |
|---|---|---|---|
| DocRED | 2019 | 5k docs | Cross-sentence, multi-hop; **high false-negative rate** |
| BioRED | 2022 | 600 abstracts | Biomedical, multi-entity-type, document-level |
| Re-DocRED | 2022 | 4k docs | Revised DocRED; **use this instead of DocRED** |
| SciER | 2024 | 106 full papers | Scientific entity + relation, document-level, fine-grained |

### 2.3 Entity linking & canonicalization

| Dataset | Year | Notes |
|---|---|---|
| AIDA-CoNLL | 2011 | The canonical EL benchmark; part of the GERBIL suite |
| MSNBC / AQUAINT / ACE2004 | 2007–2011 | Small out-of-domain EL test sets |
| WNED-WIKI / WNED-CWEB | 2016 | Automatically built, harder EL sets |
| CESI (ReVerb45K, Base, Ambiguous) | 2018 | Open-KG noun-phrase canonicalization |
| OPIEC | 2019 | 341M open IE triples from Wikipedia |
| ZESHEL | 2019 | Zero-shot EL across unseen domains (Wikia) |

### 2.4 End-to-end KG construction (LLM era)

| Benchmark | Year | What it measures |
|---|---|---|
| Text2KGBench | 2023 | Ontology-driven KG generation from text; Wikidata-TekGen (10 ontologies) + DBpedia-WebNLG (19 ontologies) splits. Metrics: triple F1, ontology conformance, hallucination rate |
| LLMs4OL | 2023 | LLM ability on ontology learning subtasks (term typing, taxonomy, relation extraction) |
| LLM-KG-Bench | 2023 | Automated eval of LLMs on RDF/SPARQL/Turtle manipulation tasks |
| KGQuiz | 2023 | Probes depth and breadth of factual knowledge encoded in LLMs |
| MINE (ships with KGGen) | 2025 | Measures information recovery from a constructed graph |

### 2.5 Domain-specific

| Dataset | Year | Domain |
|---|---|---|
| DDI Extraction | 2013 | Drug–drug interaction |
| ChemProt (BioCreative VI) | 2017 | Chemical–protein interaction |
| CUAD | 2021 | Legal contracts, 41 clause types |

### 2.6 KG completion / link prediction

| Dataset | Year | Entities | Relations | Notes |
|---|---|---|---|---|
| FB15k-237 | 2015 | 14.5k | 237 | Freebase, inverse relations removed |
| YAGO3-10 | 2015 | 123k | 37 | — |
| WN18RR | 2018 | 41k | 11 | WordNet, leakage-free version of WN18 |
| CoDEx | 2020 | 2k–78k | 42–69 | Three sizes; includes hard negatives |
| ogbl-wikikg2 | 2020 | 2.5M | 535 | Large-scale, OGB leaderboard |
| ILPC | 2022 | varies | varies | Inductive link prediction challenge |

### 2.7 Downstream RAG-over-KG evaluation

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

1. **Re-DocRED** — document-level triple precision / recall / F1. Primary number.
2. **Text2KGBench** — ontology conformance and hallucination rate, since the pipeline is
   schema-driven.
3. **SciER** — if the target corpus is scientific papers.

**Extrinsic (does the graph help?)**

4. **MuSiQue** and **2WikiMultiHopQA** — multi-hop QA accuracy / EM / F1 with and without
   the KG in the retrieval loop.

**Baselines to compare against**

- Vanilla vector RAG (no graph) — the ablation reviewers always ask for.
- GLiNER + GLiREL local extraction.
- GraphRAG and/or LightRAG as the LLM-pipeline reference.
- REBEL or ReLiK as a supervised extraction reference.

Report cost (tokens or GPU-hours) per document alongside quality. Indexing cost is the main
practical differentiator between these systems and is frequently omitted.

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
- Re-DocRED: <https://github.com/tonytan48/Re-DocRED>
- MuSiQue: <https://github.com/StonyBrookNLP/musique>
- OGB (ogbl-wikikg2): <https://ogb.stanford.edu/docs/linkprop/>
