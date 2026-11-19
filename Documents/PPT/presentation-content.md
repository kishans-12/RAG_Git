# Phase-I, Review-1 Presentation Content

**Student:** Kishan (1BY25SCS07) | **Guide:** Dr. Muneshwar | **Date:** 30-10-2026

Generated into the official Presentation Template (logo/header/format preserved).


## Slide 1 - [Title Slide]

- Name: Kishan
- USN: 1BY25SCS07
- Course: M.Tech(CSE), Semester: III
- Project Title: GraphRAG: A Knowledge-Graph-Enhanced Retrieval-Augmented Generation Framework for Multi-hop Question Answering
- Phase-I, Review-1
- Presented by
- Under the Guidance of Dr. Muneshwar, Associate Professor

## Slide 2 - [Content]

- Content:
- Introduction (2 slides)
- Related Work (6 slides, 20-25 recent papers, 7-field format)
- Problem Statement (1 slide)
- Objectives (1 slide)
- Design Methodology (5 slides: existing vs proposed algorithms + tools)
- Expected Outcomes (1 slide)
- Conclusions (1 slide)
- References

## Slide 3 - Introduction - Background

- Large Language Models (LLMs) are powerful but hallucinate and have a knowledge cutoff.
- Retrieval-Augmented Generation (RAG) grounds answers in retrieved documents, reducing hallucination and adding current knowledge [18], [21].
- Standard RAG: split documents into chunks, embed, store in a vector DB, retrieve top-k by similarity, LLM reads and answers.
- Effective for factoid questions but treats chunks as independent text and ignores relationships among entities.

## Slide 4 - Introduction - Motivation

- Basic vector RAG fails on multi-hop questions that connect information across documents, e.g., 'Who manages the lead engineer of Project Atlas?' [21], [19].
- GraphRAG adds a knowledge graph: entities as nodes, relations as edges, enabling relationship-aware retrieval [18].
- Recent works show KG-enhanced RAG consistently improves reasoning and reduces hallucination across domains [1], [2], [17].
- Motivation: build a GraphRAG system that connects entities across documents and grounds answers with citations.

## Slide 5 - Problem Statement

- Basic RAG retrieves isolated chunks and has no model of entity relationships, limiting multi-hop accuracy.
- Existing GraphRAG works mostly use a pre-existing knowledge graph, not one built from the target documents.
- Few systems attach source citations to answers, limiting trust and verifiability.
- Need: build a cross-document knowledge graph from documents, retrieve via vector + graph, answer multi-hop questions with grounded citations, using free open-source tools.

## Slide 6 - Objectives

- 1. Build a vector RAG baseline over a multi-document corpus.
- 2. Construct a cross-document knowledge graph (entities + relations) from the documents.
- 3. Implement hybrid retrieval (vector similarity + graph traversal) for multi-hop QA.
- 4. Ground each answer with source citations.
- 5. Evaluate multi-hop accuracy and citation correctness vs the baseline on a dataset with known ground truth.

## Slide 7 - Related Work - RAG Foundations & Iterative RAG

- [18] Han et al. (2024) -- Area: GraphRAG survey/framework | Problem: no systematic survey, graph data heterogeneous | Method: holistic framework (query processor, retriever, organizer, generator, data source) | Advantage: foundational reference + public repo | Gap: survey, no method/eval
- [19] Tang & Yang (2024) -- Area: multi-hop RAG benchmark | Problem: RAG weak on multi-hop, no benchmark | Method: news-based dataset + multi-hop queries/evidence; tests embeddings + LLMs | Advantage: exposes RAG weakness; public dataset | Gap: text RAG, no graph
- [4] Wang et al. (2025) -- Area: iterative/chain RAG | Problem: single retrieval fails complex queries | Method: dynamic query reformulation + rejection-sampled retrieval chains | Advantage: +10 EM on multi-hop; SOTA on KILT | Gap: no graph, no citations
- [7] Jiang et al. (2025) -- Area: iterative RAG with summarization | Problem: context overload + repetitive planning | Method: dual-function summarizer for main + sub-question | Advantage: SOTA on HotpotQA / 2WikiMultihopQA | Gap: text only, no graph

## Slide 8 - Related Work - GraphRAG & KG-Enhanced RAG

- [1] Zhu et al. (2025) -- Area: KG-guided chunk RAG | Problem: isolated chunks ignore relationships | Method: semantic seed chunks + KG-guided expansion/organization | Advantage: better retrieval + answers on HotpotQA | Gap: organizes existing chunks, no entity cross-doc reasoning/citations
- [2] Zhao et al. (2025) -- Area: KG-elicited reasoning RAG (medical) | Problem: poor diagnostic accuracy for similar diseases | Method: 4-tier diagnostic KG + fused EHR reasoning + follow-ups | Advantage: lower misdiagnosis vs SOTA | Gap: medical/private, not general QA
- [3] Wang et al. (2025) -- Area: KG-RAG for recommendation | Problem: LLM recommenders hallucinate; plain RAG noisy | Method: retrieve structured KG info for recommendation | Advantage: improves recommendations | Gap: not QA, no citations
- [9] Gao et al. (2025) -- Area: flexible modular KG-RAG | Problem: flexibility vs retrieval-quality trade-off | Method: infer hop range from query; tailored pipelines; no fine-tuning | Advantage: SOTA + efficient + flexible | Gap: uses existing KG

## Slide 9 - Related Work - KG Construction, Subgraph Retrieval & Robustness

- [10] Cai et al. (2025) -- Area: KG-driven subgraph RAG | Problem: aligning query to graph structure | Method: query-to-pattern + pattern-to-subgraph (graph semantic distance) | Advantage: beats SOTA; fast on 10M-node KG | Gap: existing KG
- [22] Li et al. (2024) -- Area: KG-RAG via subgraph retrieval | Problem: retrieval effectiveness vs efficiency | Method: lightweight MLP + parallel triple scoring; adjustable subgraph size | Advantage: small LLMs competitive; GPT-4o SOTA | Gap: existing KG
- [13] Guo et al. (2025) -- Area: GraphRAG filtering + integration | Problem: noisy retrieval + over-reliance on external knowledge | Method: two-stage filtering + logits balance with intrinsic reasoning | Advantage: better reasoning across backbones | Gap: no cross-doc citations
- [14] Wang et al. (2025) -- Area: robust GraphRAG pipeline | Problem: complex pipeline hard to isolate | Method: multi-stage (dual-level + logic-form) retrieval + verification | Advantage: 60% to 75% on SeedBench | Gap: optimization focus

## Slide 10 - Related Work - Multi-hop Reasoning Methods

- [5] Linders & Tomczak (2025) -- Area: training-free KG-extended RAG | Problem: LLM hallucination; KG lacks NL interaction | Method: question decomposition + ICL + chain-of-thought | Advantage: higher multi-hop accuracy on MetaQA | Gap: uses existing KG
- [8] Zhu et al. (2025) -- Area: retrieval-rewriting multi-hop | Problem: 'lost-in-retrieval': key entities dropped | Method: progressive retrieval + rewrite from a sentence graph | Advantage: beats baselines on MuSiQue/2Wiki/HotpotQA | Gap: sentence graph, not full KG
- [11] Cheng et al. (2025) -- Area: dual-process reasoning + retrieval | Problem: dynamic knowledge organization | Method: reasoning-augmented querying + progressive knowledge aggregation | Advantage: better accuracy + coherence | Gap: no graph, no citations
- [23] Shi et al. (2024) -- Area: generate-then-ground multi-hop | Problem: retrieve-then-read limited by retriever + noise | Method: alternate generate single-hop answer + ground into docs | Advantage: SOTA on 4 datasets | Gap: grounds to text, not KG

## Slide 11 - Related Work - Hybrid & Cross-Document Retrieval

- [20] Sarmah et al. (2024) -- Area: hybrid KG + vector RAG | Problem: vector RAG weak on financial docs | Method: retrieve from vector DB + knowledge graph | Advantage: beats VectorRAG and GraphRAG individually | Gap: financial domain; no multi-hop QA/citations
- [24] Knollmeyer et al. (2024) -- Area: document-structure KG RAG | Problem: vector RAG cannot answer beyond text content | Method: build KG from document structure (not entities) | Advantage: extends QA beyond text | Gap: structure not entities; no cross-doc reasoning
- [25] Shavaki et al. (2024) -- Area: GraphRAG for cross-doc multi-hop | Problem: multi-hop across documents is hard | Method: per-doc KGs merged into cross-document graph + vector embeddings of relations | Advantage: better accuracy + answer quality | Gap: no explicit citations; small dataset (closest to our work)
- [16] Aksoy & Unalir (2025) -- Area: RAG vs GraphRAG comparison | Problem: does structured knowledge beat unstructured RAG | Method: extract triples + LLM question analysis + filtered triples | Advantage: +20-30% semantic scores; answers ~80% RAG refused | Gap: preprint, small, no citations

## Slide 12 - Related Work - Surveys, Benchmarks & Evaluation

- [6] Xiao et al. (2025) -- Area: GraphRAG benchmark | Problem: evaluation datasets too narrow | Method: college-level multi-hop Qs across 16 disciplines + whole-pipeline assessment | Advantage: quantifies graph-structuring benefits | Gap: general benchmark
- [15] Zeng et al. (2025) -- Area: GraphRAG evaluation | Problem: biased evaluation inflates gains | Method: graph-text-grounded question generation + unbiased assessment | Advantage: shows real gains are more modest | Gap: evaluation method only
- [21] Mavi et al. (2024) -- Area: multi-hop QA survey | Problem: field hard to generalize | Method: formal definition + datasets/models/eval + best practices | Advantage: thorough structuring of the field | Gap: survey
- [17] Chinchakandi et al. (2025) -- Area: KG-enhanced RAG survey | Problem: plain RAG lacks context for complex problems | Method: review KG-RAG by architecture across domains | Advantage: KG-RAG beats RAG (+35.2%, +18.7%) | Gap: survey
- [12] Wang & Shi (2025) -- Area: KG + RAG reasoning survey | Problem: specialized domains need multi-hop reasoning | Method: review KG+RAG concepts, techniques, challenges | Advantage: consolidates the field | Gap: survey

## Slide 13 - Design Methodology - System Overview

- Proposed GraphRAG system has two pipelines (existing baseline = vector RAG only):
- Indexing (offline): documents -> chunks -> embeddings -> vector DB (Chroma); and chunks -> entity/relation extraction -> cross-document knowledge graph (NetworkX).
- Query (online): decompose multi-hop question -> vector retrieval + graph traversal -> fuse evidence -> LLM generates answer with citations.
- Existing method = vector retrieval only (no graph, no citations). Proposed method adds the graph layer + grounding.

## Slide 14 - Design Methodology - Existing Method (Basic Vector RAG)

- Input: document corpus D, query q.
- 1. Split D into chunks {c1..cn}.
- 2. Embed each chunk ei = Embed(ci); store in vector DB.
- 3. Embed query eq = Embed(q).
- 4. Retrieve top-k chunks by cosine similarity; concatenate as context C.
- 5. Answer = LLM(C, q); return answer (no graph, no citations).
- Limitation: isolated chunks, no entity relationships -> weak on multi-hop.

## Slide 15 - Design Methodology - Proposed Method (Phase A: Indexing)

- 1. Split D into chunks; embed and store in Chroma.
- 2. For each chunk, LLM extracts entities E and relations R (with types).
- 3. Build knowledge graph G = (E, R) in NetworkX.
- 4. Merge (coreference-link) entities referring to the same real-world object across documents -> cross-document edges.
- 5. Index G for subgraph/traversal retrieval alongside the vector index.

## Slide 16 - Design Methodology - Proposed Method (Phase B: Query)

- 1. Decompose multi-hop query q into sub-questions.
- 2. Vector retrieval: top-k chunks for q.
- 3. Graph retrieval: find seed entities in those chunks; traverse G over required hops.
- 4. Fuse vector chunks + graph subgraph into context C.
- 5. Generate answer with LLM, grounded in C.
- 6. Attach source citations (source chunk/document) to each claim.
- 7. Return answer + citations.

## Slide 17 - Design Methodology - Tools & Technologies

- Language: Python (free, open source).
- Framework: LangChain (RAG + graph orchestration).
- LLM: Groq free API (primary) + Ollama 3B (offline backup) - free, no card.
- Embeddings: sentence-transformers (all-MiniLM-L6-v2) - local, free.
- Vector DB: Chroma (local, free).  Graph store: NetworkX (free).  UI: Streamlit (free).
- All components free and open source -> fully reproducible at zero cost.

## Slide 18 - Expected Outcomes

- A working GraphRAG system that answers multi-hop questions over a multi-document corpus, outperforming a vector-RAG baseline.
- Cross-document knowledge graph built from documents with merged entities and explicit cross-document relationships.
- Hybrid vector-graph retrieval combining similarity search and graph traversal.
- Cited answers linking each claim to its source passage (verifiable, less hallucination).
- A reproducible, free implementation with a Streamlit web UI for demonstration.
- An evaluation report on answer accuracy and citation correctness (unbiased evaluation [6], [15]).

## Slide 19 - Conclusion

- Proposed a GraphRAG framework that augments RAG with a cross-document knowledge graph for multi-hop QA.
- Literature shows KGs consistently improve RAG; cross-document multi-hop QA and answer citations remain open.
- Methodology builds the graph from documents, retrieves via hybrid vector-graph traversal, grounds answers with citations, and evaluates on a synthetic corpus with known ground truth.
- Scoped to 6-7 weeks with free, open-source tools; expected to deliver more accurate and verifiable multi-hop answers than plain-text RAG.

## Slide 20 - References

- [1] X. Zhu et al., 'Knowledge Graph-Guided RAG,' NAACL-HLT, 2025.
- [2] X. Zhao et al., 'MedRAG: RAG with KG-Elicited Reasoning,' WWW, 2025.
- [3] S. Wang et al., 'KG RAG for LLM-based Recommendation,' ACL, 2025.
- [4] L. Wang et al., 'Chain-of-Retrieval Augmented Generation,' NeurIPS, 2025.
- [5] J. Linders and J. M. Tomczak, 'KG-extended RAG for QA,' Appl. Intell., 2025.
- [6] Y. Xiao et al., 'GraphRAG-Bench,' arXiv:2506.02404, 2025.
- [7] Z. Jiang et al., 'Retrieve, Summarize, Plan,' WWW, 2025.
- [8] R. Zhu et al., 'Mitigating Lost-in-Retrieval,' ACL, 2025.
- [9] Z. Gao et al., 'FRAG,' Findings ACL, 2025.
- [10] Y. Cai et al., 'SimGRAG,' Findings ACL, 2025.
- [11] R. Cheng et al., 'DualRAG,' arXiv:2504.18243, 2025.
- [12] H. Wang and Y. Shi, 'KG + RAG Survey,' Acad. J. Sci. Technol., 2025.
- [13] K. Guo et al., 'Empowering GraphRAG with Filtering & Integration,' EMNLP, 2025.
- [14] Z. Wang et al., 'ROGRAG,' ACL Demo, 2025.
- [15] Q. Zeng et al., 'Unbiased Eval Framework for GraphRAG,' arXiv:2506.06331, 2025.
- [16] N. Aksoy and M. O. Unalir, 'GraphRAG vs RAG, Comparative Study,' Research Square, 2025.
- [17] S. Chinchakandi et al., 'Survey of KG-Enhanced RAG,' IEEE ICEI, 2025.
- [18] H. Han et al., 'Retrieval-Augmented Generation with Graphs (GraphRAG),' arXiv:2501.00309, 2024.
- [19] Y. Tang and Y. Yang, 'MultiHop-RAG,' arXiv:2401.15391, 2024.
- [20] B. Sarmah et al., 'HybridRAG,' ACM ICAIF, 2024.
- [21] V. Mavi et al., 'Multi-hop Question Answering,' Found. Trends Inf. Retrieval, 2024.
- [22] M. Li et al., 'Simple Is Effective (SubgraphRAG),' arXiv:2410.20724, 2024.
- [23] Z. Shi et al., 'Generate-then-Ground,' ACL, 2024.
- [24] S. Knollmeyer et al., 'Document Knowledge Graph,' IEEE ETFA, 2024.
- [25] M. A. Shavaki et al., 'KG-Based RAG for Multi-Hop QA,' IKT, 2024.
