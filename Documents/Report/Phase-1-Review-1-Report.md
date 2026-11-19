# Phase-I, Review-1 Project Report (DRAFT)

> **How to use this draft:** This is the *content* for your official `Phase-1-Review-1 Report format.docx`. Open that DOCX, keep its **Cover page, Declaration, and Signature page** formatting, and paste the section content below into the matching sections. The References are included at the end.
>
> **Placeholders to fill before printing** (clearly marked in the text):
> - Guide's exact academic designation (Professor / Associate Professor / Assistant Professor) — confirm with Dr. Muneshwar.
> - Signature and date fields.
> - Reviewer-1 and Reviewer-2 names (assigned on review day).
>
> **Formatting target (per template):** Times New Roman, 12 pt, 1.5 line spacing, justified, ~20–22 pages, IEEE citations.

---

## COVER PAGE

**BMS INSTITUTE OF TECHNOLOGY AND MANAGEMENT**
Autonomous Institute under VTU, Belagavi, Karnataka – 590 018
Yelahanka, Bengaluru, Karnataka – 560 119

**Phase-I, Review-1 Project Report on**

**GraphRAG: A Knowledge-Graph-Enhanced Retrieval-Augmented Generation Framework for Multi-hop Question Answering**

Submitted in partial fulfilment of the requirements for the conferment of degree of
**MASTER OF TECHNOLOGY**
in
**Computer Science and Engineering**

by
**Kishan – 1BY25SCS07**

Under the Guidance of
**Dr. Muneshwar, [Designation], Dept. of CSE**

**DEPARTMENT OF COMPUTER SCIENCE AND ENGINEERING**
Avalahalli, Yelahanka, Bengaluru, Karnataka – 560119
**October 2026**

---

## DECLARATION

We, hereby declare that the project titled **"GraphRAG: A Knowledge-Graph-Enhanced Retrieval-Augmented Generation Framework for Multi-hop Question Answering"** is a record of original project Phase-I, Review-1 work under the guidance of **Dr. Muneshwar, [Designation]**, Department of Computer Science and Engineering.

We also declare that this project report has not been submitted for the award of any degree, diploma, associateship, fellowship or other title anywhere else.

**Name of the Student:** Kishan
**USN:** 1BY25SCS07
**Signature:** ______________ **Date:** ______________

---

## SIGNATURE PAGE

| Role | Name & Designation | Signature / Date |
|---|---|---|
| Project Guide | Dr. Muneshwar, [Designation], Dept. of CSE | ______________ |
| Associate Head (Cluster-2) | Dr. Shoba M | ______________ |
| HoD, CSE | Dr. Satish Kumar T | ______________ |
| PG Coordinator | Dr. Raguru Jaya Krishna | ______________ |
| Reviewer-1 | ____________________ | ______________ |
| Reviewer-2 | ____________________ | ______________ |

---

## 1. ABSTRACT

Large language models (LLMs) are powerful but tend to hallucinate and rely on training data that can become outdated. Retrieval-Augmented Generation (RAG) reduces these issues by grounding answers in retrieved documents, yet basic vector RAG fetches isolated text chunks and cannot answer questions that require connecting entities across multiple documents. This project proposes a GraphRAG framework that augments vector retrieval with a knowledge graph constructed from the documents themselves. The system extracts entities and relationships, merges them into a cross-document knowledge graph, and retrieves evidence using both vector similarity and graph traversal to support multi-hop question answering, with each answer grounded by source citations for verifiability. The framework is implemented entirely with free, open-source tools (Python, LangChain, Groq, Chroma, NetworkX, and Streamlit) and is evaluated on a synthetic multi-document dataset with known ground truth, comparing multi-hop accuracy and citation correctness against a basic RAG baseline. The expected outcome is an open, reproducible GraphRAG system that answers multi-hop questions more accurately and transparently than plain-text RAG.

---

## 2. INTRODUCTION

### 2.1 Background

Large language models have transformed natural language understanding and generation, but they suffer from two well-known weaknesses: factual hallucination and a knowledge cutoff tied to their training data. *Retrieval-Augmented Generation (RAG)* addresses both by retrieving relevant passages from an external corpus and conditioning the model's answer on them, so the response is grounded in retrievable evidence rather than purely parametric memory [18], [21]. A typical RAG pipeline splits documents into chunks, embeds the chunks into a vector space, stores them in a vector database, and at query time retrieves the top-k chunks most similar to the question, which the LLM then reads to produce an answer.

This vector formulation is effective for factoid look-up but has a structural limitation: it treats each chunk as an independent unit of text and discards the *relationships* among the entities those chunks mention. When a question requires connecting information scattered across several documents—for example, "Who manages the lead engineer of Project Atlas?"—a single similarity search rarely returns all the necessary evidence, and the model must bridge the gap by guessing. This is the *multi-hop* question-answering setting, which asks a system to combine multiple pieces of evidence and perform several reasoning steps [21], [64]. Surveys of multi-hop QA show the field is large and heterogeneous precisely because "multiple hops" can mean many things [21].

*GraphRAG* extends RAG by introducing a knowledge graph: entities become nodes and their relationships become edges, so retrieval can follow the structure of the data rather than only surface similarity [18]. Recent surveys and methods show that adding a knowledge graph to RAG consistently improves reasoning and reduces hallucination across domains [1], [2], [13], [17], [21]. However, the way graphs are built, searched, and used varies widely, and most approaches assume an already-available knowledge graph rather than one constructed from the target documents themselves [18], [22], [25].

### 2.2 Problem Statement

Basic vector RAG cannot reliably answer multi-hop questions that span multiple documents, because it retrieves isolated chunks and has no representation of how entities relate across documents. Existing GraphRAG works largely rely on a pre-existing knowledge graph and seldom attach source citations to their answers, which limits both trust and verifiability. There is therefore a need for a system that (i) builds a knowledge graph directly from the document corpus, (ii) retrieves evidence using a combination of vector similarity and graph traversal, (iii) answers multi-hop questions by reasoning over connected entities, and (iv) grounds each answer with citations to the source passages, all while remaining reproducible with free, open-source tools.

### 2.3 Objectives

1. Build a **vector RAG baseline** over a multi-document corpus to establish a reference for comparison.
2. Construct a **cross-document knowledge graph** (entities and relationships) automatically from the documents and merge entities that appear in multiple documents.
3. Implement **hybrid retrieval** combining vector similarity and graph traversal to support multi-hop question answering.
4. **Ground each answer with source citations** linking claims to the supporting passages.
5. **Evaluate** multi-hop answer accuracy and citation correctness against the baseline on a dataset with known ground truth.

---

## 3. LITERATURE REVIEW

This section reviews 25 recent works (mostly 2025, with foundational 2024 surveys) across RAG, GraphRAG, multi-hop QA, hybrid retrieval, and evaluation, and identifies the gap this project addresses. A structured 7-field summary of each paper is maintained separately in `LiteratureReview/papers-summary.md`; here we synthesize them thematically.

### 3.1 RAG and its limitations

RAG grounds LLM answers in retrieved evidence to reduce hallucination and add current knowledge [18], [21]. However, standard semantic retrieval returns isolated chunks and ignores the relationships among them, which hurts coherence on complex questions [1]. Iterative methods such as CoRAG [4] and ReSP [7] address single-retrieval weakness by retrieving repeatedly and reformulating the query, improving multi-hop performance, but they remain purely text-based and do not model entity structure.

### 3.2 GraphRAG and knowledge-graph-enhanced RAG

GraphRAG augments retrieval with a knowledge graph so that structured, relational information guides the model [18]. KG2RAG [1] uses a knowledge graph to expand and organize chunks into coherent paragraphs; MedRAG [2] builds a domain diagnostic knowledge graph to improve medical reasoning; K-RagRec [3] retrieves structured KG information for recommendation. Frameworks such as FRAG [9] balance flexibility and retrieval quality, SimGRAG [10] aligns queries to subgraphs, SubgraphRAG [22] retrieves right-sized subgraphs, and GraphRAG-FI [13] filters noisy retrieved facts and balances external with intrinsic reasoning. ROGRAG [14] shows that careful multi-stage retrieval with verification markedly improves robustness. These works confirm that a knowledge graph improves RAG reasoning, but most assume the graph already exists and few build it from the target documents or attach citations to answers.

### 3.3 Multi-hop question answering

Multi-hop QA requires combining several pieces of evidence and reasoning over multiple steps [21]. MultiHop-RAG [6] benchmarks show existing RAG struggles on multi-hop queries. Methods tackle this via question decomposition [5], [8], progressive retrieval-rewriting to avoid "lost-in-retrieval" [8], dual-process reasoning-retrieval coupling [11], and generate-then-ground grounding of each step into retrieved documents [23]. A comparative study [16] directly shows structured knowledge (GraphRAG) lifts multi-hop semantic scores by 20–30% and lets the system answer about 80% of questions where plain RAG refused. These results motivate combining graph structure with a multi-hop reasoning loop, but the works above either use text alone or an existing graph, and none emphasizes source citations.

### 3.4 Hybrid vector–graph retrieval

The closest strand to this project is hybrid retrieval combining vector and graph signals. HybridRAG [20] retrieves context from both a vector database and a knowledge graph and outperforms either alone for financial information extraction. The cross-document GraphRAG method of [25] builds per-document knowledge graphs, merges them into one cross-document graph, and uses vector embeddings of graph relations for retrieval, reporting gains in factual accuracy and answer quality. Document Knowledge Graph [24] builds a graph from document structure (rather than entities) to extend QA beyond text. These works validate the hybrid vector–graph design the project adopts, but [24] uses structure not entities, [20] is domain-specific, and [25]—the nearest to this work—does not attach explicit citations and uses a small dataset.

### 3.5 Evaluation, benchmarks, and robustness

Reliable evaluation is itself a research problem. GraphRAG-Bench [6] argues for hard, domain-specific, multi-hop questions and whole-pipeline assessment; an unbiased evaluation framework [15] shows reported GraphRAG gains are often inflated by biased question generation and answer scoring. Multi-hop QA best practices for dataset construction are surveyed in [21]. These guide the project's evaluation design: multi-hop questions with known ground truth and an unbiased comparison against a vector-RAG baseline, without overstating gains.

### 3.6 Surveys

The GraphRAG survey [18] defines a holistic framework (query processor, retriever, organizer, generator, data source) used here to describe the system. Surveys [17] and [12] consolidate KG-enhanced RAG across domains and report consistent gains over standard RAG, supporting the core premise.

### 3.7 Research Gap

Across these works, three gaps recur: (i) most GraphRAG methods use a **pre-existing** knowledge graph rather than constructing one from the target documents; (ii) few perform **cross-document** entity linking to answer multi-hop questions that span documents; and (iii) almost none attach **source citations** to answers, which limits verifiability. This project addresses all three by building a cross-document knowledge graph from the corpus, retrieving with hybrid vector–graph traversal, and grounding each answer with citations, evaluated on multi-hop questions with known ground truth.

---

## 4. METHODOLOGY

### 4.1 Approach: existing method vs proposed method

**Existing method — Basic Vector RAG (baseline).**
1. Given a document corpus *D* and query *q*, split *D* into chunks {c₁ … cₙ}.
2. Embed each chunk: eᵢ = Embed(cᵢ); store in a vector database.
3. Embed the query: e_q = Embed(q).
4. Retrieve the top-k chunks by cosine similarity; concatenate as context *C*.
5. Answer = LLM(C, q); return the answer (no graph, no citations).

This retrieves isolated chunks and cannot follow entity relationships across documents, which limits multi-hop accuracy [1], [21].

**Proposed method — GraphRAG with cross-document graph and citations.**

*Phase A – Indexing (offline):*
1. Split *D* into chunks; embed and store in the vector database (Chroma).
2. For each chunk, use the LLM to extract entities *E* and relations *R* with types.
3. Build a knowledge graph *G = (E, R)* in NetworkX; merge (coreference-link) entities that refer to the same real-world object across documents, producing **cross-document edges**.
4. Index *G* for subgraph/traversal retrieval alongside the vector index.

*Phase B – Query (online):*
1. Decompose a multi-hop query *q* into sub-questions.
2. **Vector retrieval**: top-k chunks for *q*.
3. **Graph retrieval**: identify seed entities mentioned in those chunks; traverse *G* over the required hops to fetch the related subgraph.
4. **Fuse** vector chunks and graph subgraph into context *C*.
5. Generate the answer with the LLM, instructed to ground each claim in *C*.
6. Attach **source citations** (source chunk / document) to each claim.
7. Return the answer with citations.

The proposed method differs from the baseline in three ways: it constructs a cross-document graph, retrieves using both vector and graph signals, and emits citations—directly targeting the gaps in Section 3.7.

### 4.2 Tools and Technologies

| Layer | Tool | Role | Cost |
|---|---|---|---|
| Language | Python | Implementation | Free |
| Framework | LangChain | RAG + graph orchestration | Free, open source |
| LLM | Groq API (primary) + Ollama 3B (offline backup) | Reasoning / entity extraction / answering | Free, no card |
| Embeddings | sentence-transformers (all-MiniLM-L6-v2) | Vector embeddings | Free, local |
| Vector DB | Chroma | Store/search chunks | Free, local |
| Graph store | NetworkX | Knowledge graph | Free |
| UI | Streamlit | Chat web app | Free |
| Editor | Kiro IDE / VS Code | Development | Free |

All components are free and open source, so the system is fully reproducible without licensing cost.

### 4.3 System Architecture and Processes

The pipeline has four stages, matching the GraphRAG framework of [18]:

1. **Query processing** – receive the user question; decompose multi-hop questions into sub-questions.
2. **Retrieval** – dual channel: vector retrieval over Chroma and graph traversal over NetworkX; results are fused.
3. **Organization** – filter and rank fused evidence (inspired by [13], [14]) and assemble grounded context.
4. **Generation** – the LLM produces an answer with inline citations to source passages.

The system is built in four implementation phases (Section 5): a vector RAG baseline first, then the graph layer, then multi-hop retrieval, then citations and a Streamlit UI. A free local model (Ollama) is kept as a fallback so the demo works even without internet.

### 4.4 Data Collection

Because no suitable public corpus with controlled, overlapping entities was available, a **synthetic enterprise corpus** is constructed for verifiable evaluation: a fictional company ("Aether Labs") with ~12 people, 3–4 projects, and ~15–20 documents (meeting minutes, project reports, an org chart, email threads, and performance reviews). The same people appear across multiple documents in different relationships, creating genuine cross-document multi-hop links. Ground-truth answers are known by construction, enabling exact evaluation of multi-hop accuracy and citation correctness—an unbiased setup informed by [6], [15], [21]. Multi-hop questions of varying hop length (1–3) are authored, and the proposed system is compared against the vector RAG baseline on answer accuracy and citation correctness.

---

## 5. PROJECT PLAN

**Timeline (6–7 weeks):**

| Week | Phase | Deliverable | Milestone |
|---|---|---|---|
| 1 | Setup + Phase 1 start | Python, LangChain, Chroma, Groq configured; ingestion + chunking | Baseline running |
| 2 | Phase 1 finish | Embeddings + Chroma + basic vector RAG Q&A (terminal) | Baseline evaluated |
| 3 | Phase 2 | Entity/relation extraction → cross-document knowledge graph in NetworkX | Graph built |
| 4 | Phase 3 | Hybrid vector + graph retrieval for multi-hop QA | Multi-hop working |
| 5 | Phase 4 | Citations + Streamlit UI + logging | UI delivered |
| 6 | Polish + test | README, error handling, multi-hop evaluation vs baseline | Eval complete |
| 7 | Buffer | Bug fixing, demo prep, demo on mobile hotspot | Demo ready |

**Resource allocation:** one student (Kishan); a personal laptop (i5, 8 GB RAM); free APIs and libraries; guide supervision (Dr. Muneshwar) for weekly review and feedback.

---

## 6. EXPECTED OUTCOMES

1. A working **GraphRAG system** that answers multi-hop questions over a multi-document corpus, outperforming a vector-RAG baseline on multi-hop accuracy.
2. **Cross-document knowledge graph** construction from documents, with merged entities and explicit cross-document relationships.
3. **Hybrid vector–graph retrieval** combining similarity search and graph traversal.
4. **Cited answers** linking each claim to its source passage, enabling verification and reducing ungrounded hallucination.
5. A **reproducible, free** implementation and a **Streamlit web UI** for interactive demonstration.
6. An **evaluation report** comparing the proposed system with the baseline on answer accuracy and citation correctness, following unbiased evaluation practices [6], [15].

These outcomes directly address the problem statement by enabling accurate, transparent multi-hop answers grounded in the user's own documents.

---

## 7. CONCLUSION

This report presented the Phase-I plan for a GraphRAG framework that enhances retrieval-augmented generation with a cross-document knowledge graph for multi-hop question answering. The literature review established that knowledge graphs consistently improve RAG, that multi-hop cross-document QA remains an open challenge, and that few works both build the graph from the target documents and attach source citations. The proposed methodology constructs such a graph, retrieves using hybrid vector–graph traversal, grounds answers with citations, and evaluates on a synthetic corpus with known ground truth using free, open-source tools. The project is scoped to 6–7 weeks and, on completion, is expected to demonstrate more accurate and verifiable multi-hop answering than plain-text RAG.

---

## 8. REFERENCES

[1] X. Zhu, Y. Xie, Y. Liu, Y. Li, and W. Hu, "Knowledge Graph-Guided Retrieval Augmented Generation," in *Proc. Conf. North Amer. Chapter Assoc. Comput. Linguistics: Hum. Lang. Technol. (NAACL-HLT)*, Albuquerque, NM, USA, 2025, pp. 8912–8924.

[2] X. Zhao, S. Liu, S.-Y. Yang, and C. Miao, "MedRAG: Enhancing Retrieval-Augmented Generation with Knowledge Graph-Elicited Reasoning for Healthcare Copilot," in *Proc. ACM Int. World Wide Web Conf. (WWW)*, 2025.

[3] S. Wang *et al.*, "Knowledge Graph Retrieval-Augmented Generation for LLM-based Recommendation," in *Proc. 63rd Annu. Meeting Assoc. Comput. Linguistics (ACL)*, Vienna, Austria, 2025, pp. 27152–27168.

[4] L. Wang, H. Chen, N. Yang, X. Huang, Z. Dou, and F. Wei, "Chain-of-Retrieval Augmented Generation," in *Adv. Neural Inf. Process. Syst. (NeurIPS)*, 2025.

[5] J. Linders and J. M. Tomczak, "Knowledge graph-extended retrieval augmented generation for question answering," *Appl. Intell.*, 2025, doi: 10.1007/s10489-025-06885-5.

[6] Y. Xiao *et al.*, "GraphRAG-Bench: Challenging Domain-Specific Reasoning for Evaluating Graph Retrieval-Augmented Generation," arXiv:2506.02404, 2025.

[7] Z. Jiang, M. Sun, L. Liang, and Z. Zhang, "Retrieve, Summarize, Plan: Advancing Multi-hop Question Answering with an Iterative Approach," in *Proc. ACM Int. World Wide Web Conf. (WWW)*, 2025.

[8] R. Zhu, X. Liu, Z. Sun, Y. Wang, and W. Hu, "Mitigating Lost-in-Retrieval Problems in Retrieval Augmented Multi-Hop Question Answering," in *Proc. 63rd Annu. Meeting Assoc. Comput. Linguistics (ACL)*, 2025.

[9] Z. Gao *et al.*, "FRAG: A Flexible Modular Framework for Retrieval-Augmented Generation based on Knowledge Graphs," in *Findings Assoc. Comput. Linguistics (Findings ACL)*, 2025.

[10] Y. Cai, Z. Guo, Y. Pei, W. Bian, and W. Zheng, "SimGRAG: Leveraging Similar Subgraphs for Knowledge Graphs Driven Retrieval-Augmented Generation," in *Findings Assoc. Comput. Linguistics (Findings ACL)*, 2025.

[11] R. Cheng *et al.*, "DualRAG: A Dual-Process Approach to Integrate Reasoning and Retrieval for Multi-Hop Question Answering," arXiv:2504.18243, 2025.

[12] H. Wang and Y. Shi, "Knowledge Graph Combined with Retrieval-Augmented Generation for Enhancing LMs Reasoning: A Survey," *Academic J. Sci. Technol.*, 2025, doi: 10.54097/h21fky45.

[13] K. Guo, H. Shomer, S. Zeng, H. Han, Y. Wang, and J. Tang, "Empowering GraphRAG with Knowledge Filtering and Integration," in *Proc. Conf. Empirical Methods Natural Lang. Process. (EMNLP)*, 2025.

[14] Z. Wang, H. Kong, J. Ying, W. Ouyang, and N. Dong, "ROGRAG: A Robustly Optimized GraphRAG Framework," in *Proc. 63rd Annu. Meeting Assoc. Comput. Linguistics: Syst. Demonstrations (ACL)*, 2025.

[15] Q. Zeng *et al.*, "How Significant Are the Real Performance Gains? An Unbiased Evaluation Framework for GraphRAG," arXiv:2506.06331, 2025.

[16] N. Aksoy and M. O. Ünalır, "Structured Knowledge for Multi-hop QA: A Comparative Study of GraphRAG and RAG," Research Square preprint, 2025, doi: 10.21203/rs.3.rs-8283065/v1.

[17] S. Chinchakandi, Y. Mellikeri, M. Khatawate, A. Annigeri, S. M. Meena, and A. Lodaya, "A Survey of Knowledge Graph Enhanced Retrieval-Augmented Generation," in *Proc. IEEE Conf. Eng. Informatics (ICEI)*, 2025, doi: 10.1109/ICEI68356.2025.11603750.

[18] H. Han *et al.*, "Retrieval-Augmented Generation with Graphs (GraphRAG)," arXiv:2501.00309, 2024.

[19] Y. Tang and Y. Yang, "MultiHop-RAG: Benchmarking Retrieval-Augmented Generation for Multi-Hop Queries," arXiv:2401.15391, 2024.

[20] B. Sarmah, D. B. Mehta, B. Hall, R. Rao, S. Patel, and S. Pasquali, "HybridRAG: Integrating Knowledge Graphs and Vector Retrieval Augmented Generation for Efficient Information Extraction," in *Proc. ACM Int. Conf. AI Finance (ICAIF)*, 2024.

[21] V. Mavi, A. Jangra, and A. Jatowt, "Multi-hop Question Answering," *Found. Trends Inf. Retrieval*, 2024, doi: 10.1561/1500000102.

[22] M. Li, S. Miao, and L. Pan, "Simple Is Effective: The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation," arXiv:2410.20724, 2024.

[23] Z. Shi *et al.*, "Generate-then-Ground in Retrieval-Augmented Generation for Multi-hop Question Answering," in *Proc. 62nd Annu. Meeting Assoc. Comput. Linguistics (ACL)*, Bangkok, Thailand, 2024, pp. 7339–7353.

[24] S. Knollmeyer, M. U. Akmal, L. Koval, S. Asif, S. G. Mathias, and D. Großmann, "Document Knowledge Graph to Enhance Question Answering with Retrieval Augmented Generation," in *Proc. IEEE Int. Conf. Emerging Technol. Factory Automat. (ETFA)*, 2024, doi: 10.1109/ETFA61755.2024.10711054.

[25] M. A. Shavaki, P. Omrani, R. Toosi, and M. A. Akhaee, "Knowledge Graph Based Retrieval-Augmented Generation for Multi-Hop Question Answering Enhancement," in *Proc. Int. Conf. Inf. Knowl. Technol. (IKT)*, 2024, doi: 10.1109/IKT65497.2024.10892619.

---

*End of Phase-I, Review-1 Report draft.*
