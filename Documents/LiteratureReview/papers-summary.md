# Literature Review — Paper Summaries

**Project:** GraphRAG: A Knowledge-Graph-Enhanced Retrieval-Augmented Generation Framework for Multi-hop Question Answering
**Student:** Kishan (1BY25SCS07) | **Guide:** Dr. Muneshwar
**Format:** Each paper follows the official 7-field Related-Work template (Year → Authors → Research area → Problems addressed → Methods → Advantages → Research gap).
**Note:** Abstracts below are **paraphrased** for understanding. Read the original at the linked PDF before final submission. All papers are real and verifiable (sourced via OpenAlex; ACL abstracts verified from ACL Anthology).
**Ordering:** 2025 papers first (newest), then 2024 foundational works.

---

## A) 2025 — Core KG-enhanced RAG & multi-hop QA methods

### [1] (2025) Knowledge Graph-Guided Retrieval Augmented Generation (KG2RAG)
**Authors:** X. Zhu, Y. Xie, Y. Liu, Y. Li, W. Hu | **Venue:** NAACL-HLT 2025 (conference) | **Cited by:** 180
**Links:** PDF https://aclanthology.org/2025.naacl-long.449.pdf | DOI 10.18653/v1/2025.naacl-long.449

| Field | Summary |
|---|---|
| Research area | KG-guided RAG at the chunk level |
| Problems addressed | Standard RAG retrieves isolated chunks and ignores relationships between them, so answers are less coherent. |
| Methods / techniques | Semantic retrieval gives "seed" chunks; a KG then guides chunk expansion and KG-based organization into coherent paragraphs. |
| Advantages | Better retrieval and response quality on HotpotQA than standard RAG. |
| Research gap identified | Organizes existing chunks but does not do entity-level cross-document reasoning or explicit answer citations. |

**What it says (paraphrased):** RAG reduces LLM hallucination, but typical semantic retrieval fetches isolated chunks and ignores their relationships. KG2RAG uses a knowledge graph to add fact-level links between chunks: after seeding chunks via semantic retrieval, it expands and organizes them using the KG into coherent paragraphs. On HotpotQA it improves both retrieval and answer quality over standard RAG.
**🗣️ Tell your mentor (2 sentences):** "KG2RAG uses a knowledge graph to link and organize the chunks that RAG retrieves, making the final answer more coherent. It shows clear gains on HotpotQA, which is the kind of multi-hop dataset I plan to evaluate against."

### [2] (2025) MedRAG: RAG with Knowledge Graph-Elicited Reasoning for Healthcare Copilot
**Authors:** X. Zhao, S. Liu, S.-Y. Yang, C. Miao | **Venue:** WWW 2025 (conference) | **Cited by:** 163
**Links:** PDF https://dl.acm.org/doi/pdf/10.1145/3696410.3714782 | DOI 10.1145/3696410.3714782

| Field | Summary |
|---|---|
| Research area | KG-elicited reasoning RAG for healthcare |
| Problems addressed | Medical RAG has poor diagnostic accuracy/specificity, especially for diseases with similar symptoms. |
| Methods / techniques | Builds a 4-tier hierarchical diagnostic KG; dynamically fuses KG differences with retrieved electronic health records; reasons in an LLM; asks follow-up questions. |
| Advantages | Lower misdiagnosis, more specific decisions; beats prior RAG on DDXPlus and a private chronic-pain dataset. |
| Research gap identified | Domain-specific (medical) using private records; not general cross-document QA with open-domain citations. |

**What it says (paraphrased):** RAG suits privacy-sensitive health records but existing medical RAG is inaccurate, especially for similar diseases. MedRAG builds a four-tier diagnostic knowledge graph, dynamically combines its disease-distinguishing facts with retrieved similar records, and reasons inside an LLM, also proactively asking follow-up questions. It reduces misdiagnosis and outperforms strong baselines on public and private datasets.
**🗣️ Tell your mentor (2 sentences):** "MedRAG shows how a domain knowledge graph can guide RAG reasoning for harder, similar-looking cases. It motivates using a knowledge graph to improve specificity, which is the same principle behind my GraphRAG design."

### [3] (2025) Knowledge Graph Retrieval-Augmented Generation for LLM-based Recommendation (K-RagRec)
**Authors:** S. Wang et al. | **Venue:** ACL 2025 (conference) | **Cited by:** 121
**Links:** PDF https://aclanthology.org/2025.acl-long.1317.pdf | DOI 10.18653/v1/2025.acl-long.1317

| Field | Summary |
|---|---|
| Research area | KG-RAG for LLM-based recommendation |
| Problems addressed | LLM recommenders hallucinate and lack up-to-date/domain knowledge; plain RAG adds noise and ignores structural relationships. |
| Methods / techniques | Retrieves high-quality, up-to-date structured information from a KG to augment recommendation generation (K-RagRec). |
| Advantages | Uses KG structure to improve recommendation quality. |
| Research gap identified | Recommendation-focused, not factual multi-hop QA; no citation/grounding mechanism. |

**What it says (paraphrased):** LLM-based recommenders inherit hallucinations and stale knowledge from their backbones; vanilla RAG is noisy and ignores relational structure. The authors retrieve high-quality structured knowledge from a knowledge graph to augment the recommendation process, showing the framework improves LLM-based recommendations.
**🗣️ Tell your mentor (2 sentences):** "This paper applies KG-RAG to recommendations, showing that using structured knowledge-graph information beats plain-text RAG. It supports my choice to use a knowledge graph rather than relying only on vector retrieval."

### [4] (2025) Chain-of-Retrieval Augmented Generation (CoRAG)
**Authors:** L. Wang, H. Chen, N. Yang, X. Huang, Z. Dou, F. Wei | **Venue:** NeurIPS 2025 (conference) | **Cited by:** 81
**Links:** PDF https://arxiv.org/pdf/2501.14342 | arXiv 2501.14342

| Field | Summary |
|---|---|
| Research area | Iterative / chain retrieval RAG (o1-style) |
| Problems addressed | Single-retrieval RAG fails on complex/multi-hop queries because the first retrieval is imperfect. |
| Methods / techniques | Dynamically reformulates the query from the evolving state; trained with rejection sampling to create intermediate retrieval chains; test-time decoding controls chain length/count. |
| Advantages | >10 EM-point gain on multi-hop QA; new SOTA on the KILT benchmark. |
| Research gap identified | Retrieval-chain focused; uses no knowledge graph; answer grounding/citation not the focus. |

**What it says (paraphrased):** Conventional RAG retrieves once before answering, which limits it on complex queries. CoRAG trains o1-like RAG models that retrieve and reason step-by-step, reformulating the query as the state evolves, using rejection sampling to synthesize intermediate retrieval chains. It improves multi-hop QA by over 10 EM points and sets SOTA on KILT.
**🗣️ Tell your mentor (2 sentences):** "CoRAG shows that multi-step, iterative retrieval beats single-shot retrieval on multi-hop questions. I can combine this iterative idea with a knowledge graph so each retrieval step follows real entity relationships."

### [5] (2025) Knowledge graph-extended RAG for question answering (KG-RAG)
**Authors:** J. Linders, J. M. Tomczak | **Venue:** Applied Intelligence (journal) | **Cited by:** 65
**Links:** PDF https://link.springer.com/content/pdf/10.1007/s10489-025-06885-5.pdf | DOI 10.1007/s10489-025-06885-5

| Field | Summary |
|---|---|
| Research area | Training-free KG-extended RAG for QA |
| Problems addressed | LLMs hallucinate and have knowledge gaps; KGs lack natural-language interaction. |
| Methods / techniques | Integrates LLMs and KGs without training; question decomposition for multi-hop retrieval; in-context learning + chain-of-thought prompting; explicit reasoning chains. |
| Advantages | Higher accuracy on multi-hop MetaQA; more transparent answers. |
| Research gap identified | Uses an existing KG rather than constructing one from documents; single-hop accuracy trades off. |

**What it says (paraphrased):** LLMs understand language but hallucinate; KGs are structured but hard to query conversationally. The authors combine LLMs and KGs without training, adding question decomposition for multi-hop retrieval and chain-of-thought reasoning for transparency. On MetaQA, multi-hop accuracy rises, though single-hop drops slightly versus LLM-with-KG baselines.
**🗣️ Tell your mentor (2 sentences):** "This is a training-free way to merge a knowledge graph with an LLM using question decomposition and chain-of-thought. It confirms that decomposing multi-hop questions helps retrieval, which I will adopt."

### [6] (2025) GraphRAG-Bench: Domain-Specific Reasoning for Evaluating GraphRAG
**Authors:** Y. Xiao et al. | **Venue:** arXiv (preprint) | **Cited by:** 52
**Links:** PDF https://arxiv.org/pdf/2506.02404 | arXiv 2506.02404

| Field | Summary |
|---|---|
| Research area | Benchmark for GraphRAG |
| Problems addressed | Existing GraphRAG evaluations use narrow QA datasets that cannot measure the reasoning gains GraphRAG adds. |
| Methods / techniques | College-level, domain-specific multi-hop questions across 16 disciplines and 20 textbooks; multiple task types; holistic evaluation of graph construction, retrieval, and generation. |
| Advantages | Rigorously quantifies how graph structuring helps reasoning; evaluates 9 GraphRAG methods. |
| Research gap identified | A general benchmark; my project must build its own domain-specific multi-hop test set with known ground truth. |

**What it says (paraphrased):** Current GraphRAG evaluations rely on ordinary QA datasets and miss the reasoning improvements graph structuring provides. GraphRAG-Bench offers hard, college-level, multi-hop questions spanning many disciplines and task types, assessing the whole pipeline from graph construction to answer generation. Applying nine GraphRAG methods reveals how graph structuring improves reasoning.
**🗣️ Tell your mentor (2 sentences):** "GraphRAG-Bench shows that good evaluation needs hard, multi-hop, domain-specific questions, not just simple QA. I will design my own test questions with known answers so I can measure multi-hop accuracy properly."

### [7] (2025) Retrieve, Summarize, Plan: Multi-hop QA with an Iterative Approach (ReSP)
**Authors:** Z. Jiang, M. Sun, L. Liang, Z. Zhang | **Venue:** WWW 2025 (conference) | **Cited by:** 50
**Links:** PDF https://dl.acm.org/doi/pdf/10.1145/3701716.3716889 | DOI 10.1145/3701716.3716889

| Field | Summary |
|---|---|
| Research area | Iterative RAG with dual summarization for multi-hop QA |
| Problems addressed | Iterative RAG suffers context overload and over/repetitive planning because there is no recorded trajectory. |
| Methods / techniques | A dual-function summarizer compresses retrieved documents for both the overarching question and the current sub-question, with iterative retrieve–summarize–plan. |
| Advantages | Beats SOTA on HotpotQA and 2WikiMultihopQA; robust to long contexts. |
| Research gap identified | Pure text retrieval; no knowledge graph or entity reasoning; no citation mechanism. |

**What it says (paraphrased):** Iterative RAG improves multi-hop QA but causes context overload and repetitive planning. ReSP adds a dual-function summarizer that compresses retrieved documents toward both the main question and the current sub-question. It outperforms SOTA on two multi-hop datasets and stays robust as context grows.
**🗣️ Tell your mentor (2 sentences):** "ReSP tackles the context-overload problem in iterative RAG by summarizing for both the main question and each sub-question. This summarization idea will help keep my retrieved graph context manageable."

### [8] (2025) Mitigating Lost-in-Retrieval for Multi-Hop QA (ChainRAG)
**Authors:** R. Zhu, X. Liu, Z. Sun, Y. Wang, W. Hu | **Venue:** ACL 2025 (conference) | **Cited by:** 36
**Links:** PDF https://aclanthology.org/2025.acl-long.1089.pdf | DOI 10.18653/v1/2025.acl-long.1089

| Field | Summary |
|---|---|
| Research area | Retrieval-rewriting for multi-hop RAG |
| Problems addressed | "Lost-in-retrieval": key entities are dropped during sub-question decomposition, breaking the reasoning chain. |
| Methods / techniques | Progressive retrieve-and-rewrite (ChainRAG): completes missing key entities, retrieves from a sentence graph, chains steps, then integrates all evidence. |
| Advantages | Beats baselines on MuSiQue, 2Wiki, HotpotQA across GPT-4o-mini, Qwen2.5-72B, GLM-4. |
| Research gap identified | Uses a sentence graph, not a full entity–relationship KG; grounding/citation not the focus. |

**What it says (paraphrased):** The authors identify "lost-in-retrieval," where key entities vanish during sub-question decomposition and degrade retrieval and answers. ChainRAG handles each sub-question progressively, filling in missing entities and retrieving from a sentence graph, chaining steps and finally integrating evidence. It consistently beats baselines on three multi-hop datasets.
**🗣️ Tell your mentor (2 sentences):** "ChainRAG shows that losing key entities during question decomposition breaks multi-hop answers, and progressive rewriting fixes it. I will make sure my graph entities are preserved across each reasoning step."

### [9] (2025) FRAG: Flexible Modular Framework for KG-based RAG
**Authors:** Z. Gao et al. | **Venue:** Findings of ACL 2025 (conference) | **Cited by:** 26
**Links:** PDF https://aclanthology.org/2025.findings-acl.321.pdf | DOI 10.18653/v1/2025.findings-acl.321

| Field | Summary |
|---|---|
| Research area | Flexible modular KG-RAG |
| Problems addressed | KG-RAG trades flexibility against retrieval quality: modular methods are flexible but weak; coupled methods are strong but rigid. |
| Methods / techniques | Estimates reasoning-path hop range from the query alone, classifies simple vs complex, and applies tailored pipelines; no extra LLM fine-tuning or calls. |
| Advantages | SOTA with high efficiency and low resource use while staying flexible. |
| Research gap identified | Uses an existing KG; does not build a graph from raw documents or handle cross-document grounding/citations. |

**What it says (paraphrased):** KG-RAG methods either stay flexible but retrieve poorly (modular) or retrieve well but lose flexibility (coupled). FRAG infers reasoning-path hop range from the query text, splits queries into simple or complex, and applies tailored retrieval pipelines without fine-tuning. It reaches SOTA with high efficiency and low resources.
**🗣️ Tell your mentor (2 sentences):** "FRAG balances flexibility and retrieval quality by choosing a retrieval pipeline based on how complex the query is. I will similarly adapt retrieval depth to the question type."

### [10] (2025) SimGRAG: Similar Subgraphs for KG-driven RAG
**Authors:** Y. Cai, Z. Guo, Y. Pei, W. Bian, W. Zheng | **Venue:** Findings of ACL 2025 (conference) | **Cited by:** 19
**Links:** PDF https://aclanthology.org/2025.findings-acl.163.pdf | DOI 10.18653/v1/2025.findings-acl.163

| Field | Summary |
|---|---|
| Research area | KG-driven RAG via subgraph similarity |
| Problems addressed | Aligning natural-language queries to KG structures is hard. |
| Methods / techniques | Two stages: query-to-pattern (LLM turns the query into a graph pattern) and pattern-to-subgraph (a graph semantic distance metric); efficient top-k retrieval on a 10M-node KG. |
| Advantages | Beats SOTA on QA and fact verification; retrieval under 1 second. |
| Research gap identified | Relies on an existing KG; not about constructing graphs from documents or multi-document reasoning. |

**What it says (paraphrased):** KG-driven RAG must align a text query with graph structure. SimGRAG does this in two stages: an LLM converts the query into a graph pattern, then a graph semantic distance metric ranks candidate subgraphs. It runs fast on a 10-million-node KG and beats prior KG-RAG methods on QA and fact verification.
**🗣️ Tell your mentor (2 sentences):** "SimGRAG aligns a question to graph structure by first turning the question into a graph pattern, then matching subgraphs. This query-to-pattern idea can improve how my system searches the knowledge graph."

### [11] (2025) DualRAG: Dual-Process Reasoning + Retrieval for Multi-Hop QA
**Authors:** R. Cheng et al. | **Venue:** arXiv (preprint) | **Cited by:** 15
**Links:** PDF https://arxiv.org/pdf/2504.18243 | arXiv 2504.18243

| Field | Summary |
|---|---|
| Research area | Dual-process reasoning+retrieval for multi-hop QA |
| Problems addressed | Iterative retrieval struggles to identify and organize dynamic knowledge during multi-hop reasoning. |
| Methods / techniques | Two coupled processes — reasoning-augmented querying and progressive knowledge aggregation — feed each other; works on smaller models via fine-tuning. |
| Advantages | Better accuracy and coherence, approaching oracle-knowledge performance. |
| Research gap identified | Reasoning-focused; no knowledge graph; no source citation. |

**What it says (paraphrased):** Multi-hop QA needs dynamic knowledge across steps, which iterative retrieval handles poorly. DualRAG couples reasoning-augmented querying with progressive knowledge aggregation so each new fact supports the next reasoning step, creating a virtuous cycle. It improves accuracy and coherence and, with fine-tuning, keeps strong behavior on smaller models.
**🗣️ Tell your mentor (2 sentences):** "DualRAG tightly couples reasoning with retrieval so each step gathers exactly the knowledge the next step needs. I will structure my retrieval loop the same way so reasoning and retrieval support each other."

### [12] (2025) Empowering GraphRAG with Knowledge Filtering and Integration (GraphRAG-FI)
**Authors:** K. Guo, H. Shomer, S. Zeng, H. Han, Y. Wang, J. Tang | **Venue:** EMNLP 2025 (conference) | **Cited by:** 9
**Links:** PDF https://aclanthology.org/2025.emnlp-main.1293.pdf | DOI 10.18653/v1/2025.emnlp-main.1293

| Field | Summary |
|---|---|
| Research area | Improving GraphRAG via filtering + integration |
| Problems addressed | GraphRAG retrieves noisy/irrelevant information and over-relies on external knowledge, suppressing the LLM's own reasoning. |
| Methods / techniques | Two-stage filtering to refine retrieved info; a logits-based strategy balances external graph knowledge with the LLM's intrinsic reasoning. |
| Advantages | Better reasoning across multiple backbones; more reliable GraphRAG. |
| Research gap identified | KG-QA focused; filtering helps but does not add cross-document citation/grounding for final answers. |

**What it says (paraphrased):** GraphRAG can retrieve noisy facts and can make the LLM rely too much on external knowledge. GraphRAG-FI adds a two-stage filtering mechanism to clean retrieved information and an integration strategy that balances external graph knowledge with the model's intrinsic reasoning. It improves reasoning across several backbones.
**🗣️ Tell your mentor (2 sentences):** "GraphRAG-FI shows that noisy graph retrieval and over-reliance on external knowledge both hurt answers. I will add filtering and keep a balance between retrieved graph facts and the LLM's own reasoning."

### [13] (2025) Knowledge Graph Combined with RAG for Enhancing LM Reasoning: A Survey
**Authors:** H. Wang, Y. Shi | **Venue:** Academic J. of Science and Technology (journal) | **Cited by:** 10
**Links:** PDF https://drpress.org/ojs/index.php/ajst/article/download/29613/29054 | DOI 10.54097/h21fky45

| Field | Summary |
|---|---|
| Research area | Survey of KG + RAG for reasoning |
| Problems addressed | Specialized domains (law, medicine, science) need multi-hop reasoning; plain RAG lacks coherence and logic. |
| Methods / techniques | Reviews how KGs are combined with RAG; covers concepts, mainstream techniques, challenges, and future directions. |
| Advantages | Consolidates the field and identifies open problems. |
| Research gap identified | A survey (no method); flags evaluation and domain adaptation as open challenges. |

**What it says (paraphrased):** RAG reduces hallucinations but specialized domains still lack coherence and logic for multi-hop reasoning. This survey reviews how combining knowledge graphs with RAG improves reasoning, covering basic concepts, mainstream techniques, and challenges. It argues KG structure improves knowledge representation and reasoning and outlines future directions.
**🗣️ Tell your mentor (2 sentences):** "This survey maps how knowledge graphs are combined with RAG to improve reasoning. It helps me position my work within the mainstream techniques and the open challenges they list."

### [14] (2025) ROGRAG: A Robustly Optimized GraphRAG Framework
**Authors:** Z. Wang, H. Kong, J. Ying, W. Ouyang, N. Dong | **Venue:** ACL 2025 (system demo) | **Cited by:** 6
**Links:** PDF https://aclanthology.org/2025.acl-demo.58.pdf | DOI 10.18653/v1/2025.acl-demo.58

| Field | Summary |
|---|---|
| Research area | Robustly optimized GraphRAG pipeline |
| Problems addressed | GraphRAG pipelines are complex, making it hard to isolate each component's effect and to evaluate retrieval. |
| Methods / techniques | Multi-stage retrieval combining dual-level and logic-form retrieval; result verification; incremental database construction; rigorous ablations. |
| Advantages | Lifts Qwen2.5-7B from 60% to 75% on SeedBench; beats mainstream methods. |
| Research gap identified | Pipeline/optimization focus; cross-document grounding/citation not central. |

**What it says (paraphrased):** GraphRAG pipelines are complex, so isolating components and evaluating retrieval is hard. ROGRAG adds a multi-stage retrieval mechanism combining dual-level and logic-form retrieval, plus result verification and incremental database building, validated through ablations. It lifts a Qwen2.5-7B baseline from 60% to 75% on SeedBench.
**🗣️ Tell your mentor (2 sentences):** "ROGRAG shows that careful, multi-stage retrieval with verification greatly improves GraphRAG robustness. I will use multi-stage retrieval and verify results before generating the answer."

### [15] (2025) An Unbiased Evaluation Framework for GraphRAG
**Authors:** Q. Zeng et al. | **Venue:** arXiv (preprint) | **Cited by:** 5
**Links:** PDF https://arxiv.org/pdf/2506.06331 | arXiv 2506.06331

| Field | Summary |
|---|---|
| Research area | Evaluation methodology for GraphRAG |
| Problems addressed | GraphRAG answer evaluation has unrelated questions and biases, leading to wrong performance conclusions. |
| Methods / techniques | Graph-text-grounded question generation plus an unbiased LLM-based answer assessment procedure. |
| Advantages | Shows real GraphRAG gains are more modest than reported; more rigorous evaluation. |
| Research gap identified | An evaluation method, not a new GraphRAG method; the project can adopt its unbiased evaluation. |

**What it says (paraphrased):** Reported GraphRAG gains may be inflated by unrelated questions and evaluation bias. The authors build an unbiased framework with graph-text-grounded question generation and a bias-free LLM answer assessment, then re-evaluate three GraphRAG methods. Their gains turn out much more moderate than previously claimed.
**🗣️ Tell your mentor (2 sentences):** "This paper warns that GraphRAG results can be inflated by biased evaluation, and it offers an unbiased framework. I will evaluate my system carefully to avoid overstating gains."

### [16] (2025) Structured Knowledge for Multi-hop QA: A Comparative Study of GraphRAG and RAG
**Authors:** N. Aksoy, M. O. Ünalır | **Venue:** Research Square (preprint) | **Cited by:** 0
**Links:** PDF https://www.researchsquare.com/article/rs-8283065/latest.pdf | DOI 10.21203/rs.3.rs-8283065/v1

| Field | Summary |
|---|---|
| Research area | Empirical comparison of RAG vs GraphRAG for multi-hop QA |
| Problems addressed | Whether structured knowledge (GraphRAG) beats unstructured RAG on multi-hop QA. |
| Methods / techniques | Extracts knowledge triples from context; an LLM analyzes the question (type, reasoning pattern) and selects relevant triples; answers use only filtered structured triples. Tested on 500 HotpotQA questions. |
| Advantages | Cosine similarity and BERT-F1 rise 20–30%; GraphRAG answers ~80% of questions where RAG said "I don't know." |
| Research gap identified | Preprint, small scale; no cross-document entity graph or citations — but directly supports the project's premise. |

**What it says (paraphrased):** The study compares classical RAG with a knowledge-graph-based GraphRAG on 500 HotpotQA questions. GraphRAG extracts triples, an LLM analyzes the question and picks relevant triples, and answers use only filtered structured information. Structured knowledge lifts semantic scores by 20–30% and lets GraphRAG answer about 80% of questions RAG refused.
**🗣️ Tell your mentor (2 sentences):** "This paper directly compares RAG and GraphRAG and finds structured knowledge clearly better for multi-hop QA. It is the strongest evidence for the premise of my project, so I cite it as direct motivation."

### [17] (2025) A Survey of Knowledge Graph Enhanced RAG
**Authors:** S. Chinchakandi, Y. Mellikeri, M. Khatawate, A. Annigeri, S. M. Meena, A. Lodaya | **Venue:** IEEE ICEI 2025 (conference) | **Cited by:** 0
**Links:** DOI 10.1109/ICEI68356.2025.11603750

| Field | Summary |
|---|---|
| Research area | Survey of KG-enhanced RAG across domains |
| Problems addressed | Plain-text RAG lacks context for complex/domain problems and hallucinates. |
| Methods / techniques | Reviews KG-RAG works grouped by architecture (hybrid retrieval, graph-based context expansion) across biology, cybersecurity, education. |
| Advantages | KG-RAG consistently beats standard RAG (e.g., +35.2% student assessment, +18.7% biomedical QA). |
| Research gap identified | A survey; highlights open challenges for dependable, domain-aware systems. |

**What it says (paraphrased):** Plain-text RAG struggles with complex domain problems and hallucinates. This survey reviews knowledge-graph-enhanced RAG across domains, grouping methods by architecture and reporting consistent gains over standard RAG. It consolidates developments and lists open challenges for dependable AI systems.
**🗣️ Tell your mentor (2 sentences):** "This survey reports consistent accuracy gains when knowledge graphs are added to RAG across several domains. The reported numbers support my decision to use a knowledge-graph layer."

---

## B) 2024 — Foundational works (needed as base references)

### [18] (2024) Retrieval-Augmented Generation with Graphs (GraphRAG) — Survey
**Authors:** H. Han et al. | **Venue:** arXiv (preprint) | **Cited by:** 391
**Links:** PDF https://arxiv.org/pdf/2501.00309 | arXiv 2501.00309

| Field | Summary |
|---|---|
| Research area | Comprehensive survey of GraphRAG |
| Problems addressed | Graph data is heterogeneous and domain-specific, making GraphRAG design hard; no systematic survey existed. |
| Methods / techniques | Defines a holistic GraphRAG framework (query processor, retriever, organizer, generator, data source) and reviews domain-specific techniques. |
| Advantages | Foundational reference with a public repository. |
| Research gap identified | A survey (no method); the project positions itself using this framework. |

**What it says (paraphrased):** Graphs encode rich relational information, making them valuable for RAG, but graph data is heterogeneous and domain-specific, so designing GraphRAG is hard. This survey defines a holistic GraphRAG framework with components for query processing, retrieval, organizing, generation, and data sources, then reviews domain-specific techniques and challenges. It is the field's main reference and maintains a public repository.
**🗣️ Tell your mentor (2 sentences):** "This is the main survey of GraphRAG and it defines the components every GraphRAG system has. I use its framework to describe my own system's query processor, retriever, and generator."

### [19] (2024) MultiHop-RAG: Benchmarking RAG for Multi-Hop Queries
**Authors:** Y. Tang, Y. Yang | **Venue:** arXiv (preprint) | **Cited by:** 307
**Links:** PDF https://arxiv.org/pdf/2401.15391 | arXiv 2401.15391

| Field | Summary |
|---|---|
| Research area | Benchmark dataset for multi-hop RAG |
| Problems addressed | Existing RAG is inadequate for multi-hop queries, and no benchmark focused on them. |
| Methods / techniques | Builds MultiHop-RAG from English news: a knowledge base, multi-hop queries, ground-truth answers, and supporting evidence; tests embedding models and LLMs (GPT-4, PaLM, Llama2-70B). |
| Advantages | Exposes RAG's weakness on multi-hop queries; public dataset and system. |
| Research gap identified | A text-RAG benchmark with no graph; the project extends evaluation with a graph and known ground truth. |

**What it says (paraphrased):** RAG helps reduce hallucinations but is weak on multi-hop queries, and no benchmark targeted them. The authors build MultiHop-RAG, a news-based dataset with multi-hop queries, answers, and evidence, then test embedding models and several LLMs. Both retrieval and answering experiments show existing RAG performs poorly on multi-hop queries.
**🗣️ Tell your mentor (2 sentences):** "MultiHop-RAG is the key benchmark showing plain RAG fails on multi-hop questions. I will use multi-hop-style questions, possibly inspired by this dataset, to test my system."

### [20] (2024) HybridRAG: Integrating Knowledge Graphs and Vector RAG
**Authors:** B. Sarmah, D. B. Mehta, B. Hall, R. Rao, S. Patel, S. Pasquali | **Venue:** ACM ICAIF 2024 (conference) | **Cited by:** 181
**Links:** PDF https://dl.acm.org/doi/pdf/10.1145/3677052.3698671 | DOI 10.1145/3677052.3698671

| Field | Summary |
|---|---|
| Research area | Hybrid KG-RAG + Vector-RAG for information extraction |
| Problems addressed | Vector RAG struggles with financial documents due to domain terms and complex formats. |
| Methods / techniques | HybridRAG retrieves context from both a vector database and a knowledge graph, combining Vector-RAG and Graph-RAG. |
| Advantages | Beats Vector-RAG and Graph-RAG individually at both retrieval and generation. |
| Research gap identified | Financial domain; the hybrid idea directly supports my approach — gap is no cross-document multi-hop QA focus or citations. |

**What it says (paraphrased):** Vector RAG struggles on financial documents because of domain terms and complex layouts. HybridRAG combines knowledge-graph-based RAG with vector-based RAG so context comes from both the vector database and the graph. On earnings-call transcripts it beats Vector-RAG and Graph-RAG alone at retrieval and answer generation, and generalizes beyond finance.
**🗣️ Tell your mentor (2 sentences):** "HybridRAG is the closest to my design because it combines vector retrieval with knowledge-graph retrieval and beats using either alone. My project adopts this hybrid idea and adds multi-hop reasoning and citations."

### [21] (2024) Multi-hop Question Answering — Survey
**Authors:** V. Mavi, A. Jangra, A. Jatowt | **Venue:** Foundations and Trends in Information Retrieval (journal) | **Cited by:** 119
**Links:** PDF https://arxiv.org/pdf/2204.09140 | DOI 10.1561/1500000102

| Field | Summary |
|---|---|
| Research area | Survey/tutorial of multi-hop QA |
| Problems addressed | Multi-hop QA needs combining multiple facts and multi-step reasoning; the field is hard to generalize. |
| Methods / techniques | Gives a formal definition of multi-hop QA and organizes frameworks, datasets, models, and evaluation; lists best practices for building datasets. |
| Advantages | Thorough structuring of the field. |
| Research gap identified | A survey; provides formal grounding and dataset practices the project can adopt. |

**What it says (paraphrased):** Multi-hop QA requires extracting and combining several facts with multiple reasoning steps, and the notion of "hops" varies widely. This monograph gives a formal definition, organizes existing frameworks, datasets, models, and evaluation methods, and outlines best practices for building multi-hop datasets.
**🗣️ Tell your mentor (2 sentences):** "This is the standard reference that defines multi-hop QA and its evaluation. I use its definition to frame what multi-hop questions my system must answer."

### [22] (2024) Simple Is Effective: SubgraphRAG (Roles of Graphs and LLMs in KG-RAG)
**Authors:** M. Li, S. Miao, L. Pan | **Venue:** arXiv (preprint) | **Cited by:** 105
**Links:** PDF https://arxiv.org/pdf/2410.20724 | arXiv 2410.20724

| Field | Summary |
|---|---|
| Research area | KG-based RAG via subgraph retrieval |
| Problems addressed | KG-RAG must balance retrieval effectiveness against efficiency (right amount of graph info). |
| Methods / techniques | SubgraphRAG uses a lightweight MLP with parallel triple scoring and directional structural distances; subgraph size adjusts to the query and LLM; no fine-tuning. |
| Advantages | Smaller LLMs stay competitive with explainable reasoning; GPT-4o reaches SOTA on WebQSP/CWQ; fewer hallucinations. |
| Research gap identified | Uses an existing KG; not about building graphs from documents or multi-document reasoning. |

**What it says (paraphrased):** KG-RAG must retrieve just enough relevant graph information without overloading the LLM. SubgraphRAG retrieves subgraphs using a lightweight MLP and parallel triple scoring with structural-distance encoding, and adjusts subgraph size to the query. Smaller LLMs stay competitive and GPT-4o hits SOTA while reducing hallucinations.
**🗣️ Tell your mentor (2 sentences):** "SubgraphRAG shows that retrieving the right-sized subgraph, not the whole graph, balances accuracy and efficiency. I will tune how much graph context I retrieve per question."

### [23] (2024) Generate-then-Ground in RAG for Multi-hop QA (GenGround)
**Authors:** Z. Shi et al. | **Venue:** ACL 2024 (conference) | **Cited by:** 72
**Links:** PDF https://aclanthology.org/2024.acl-long.397.pdf | DOI 10.18653/v1/2024.acl-long.397

| Field | Summary |
|---|---|
| Research area | Generate-then-ground for multi-hop QA |
| Problems addressed | Retrieve-then-read is limited by the retriever and by noise in retrieved documents. |
| Methods / techniques | Alternates two phases: form a simpler single-hop question and generate an answer, then ground that pair into retrieved documents and amend errors; distillation generalizes to smaller models. |
| Advantages | Bests baselines on four datasets; provides a reasoning-process dataset. |
| Research gap identified | Grounds to text, not a KG; no graph structure — but the grounding idea aligns with my citation goal. |

**What it says (paraphrased):** Retrieve-then-read is constrained by the retriever and noisy documents. GenGround alternates between generating a simpler single-hop question with an answer, and grounding that pair into retrieved documents to correct mistakes, iterating until the final answer. It also distills this into smaller models and outperforms baselines on four datasets.
**🗣️ Tell your mentor (2 sentences):** "GenGround grounds each generated answer step back into the source documents and corrects mistakes. I borrow this grounding idea to attach citations to my answers."

### [24] (2024) Document Knowledge Graph to Enhance QA with RAG
**Authors:** S. Knollmeyer et al. | **Venue:** IEEE ETFA 2024 (conference) | **Cited by:** 16
**Links:** DOI 10.1109/ETFA61755.2024.10711054

| Field | Summary |
|---|---|
| Research area | Document-structure KG to enhance RAG QA |
| Problems addressed | Vector-DB RAG cannot answer questions that go beyond a document's text content. |
| Methods / techniques | Builds a knowledge graph from document structure (not content entities) and integrates it into RAG. |
| Advantages | Extends RAG beyond raw text content for factory-planning documents. |
| Research gap identified | Structure-based graph, not entity-relationship; single domain; no cross-document entity multi-hop reasoning or citations. |

**What it says (paraphrased):** Reusing document knowledge matters in factory planning, and RAG helps users query a document corpus through chat. But vector-database RAG cannot answer questions beyond the document text. The paper builds a knowledge graph from document structures and integrates it into RAG to extend QA beyond plain text content.
**🗣️ Tell your mentor (2 sentences):** "This paper builds a knowledge graph from document structure to extend RAG beyond plain text. Unlike mine, it uses document structure rather than entity relationships, which is the gap my project addresses."

### [25] (2024) KG-Based RAG for Multi-Hop QA Enhancement
**Authors:** M. A. Shavaki, P. Omrani, R. Toosi, M. A. Akhaee | **Venue:** IKT 2024 (conference) | **Cited by:** 11
**Links:** DOI 10.1109/IKT65497.2024.10892619

| Field | Summary |
|---|---|
| Research area | GraphRAG for multi-hop QA with cross-document graphs |
| Problems addressed | Multi-hop QA needs integrating information across documents; existing methods retrieve poorly across them. |
| Methods / techniques | Builds per-document KGs (entity nodes, relation edges with context), merges them into a unified cross-document graph, and uses vector embeddings of graph relations for retrieval; evaluated with RAGAS. |
| Advantages | Better factual accuracy and semantic similarity; better comprehensiveness and directness. |
| Research gap identified | Closest to my project (cross-doc graph, multi-hop); gaps: no explicit citations and a small dataset — my project adds grounding/citations and a synthetic controlled ground-truth set. |

**What it says (paraphrased):** Multi-hop QA needs information from multiple documents, and existing methods retrieve poorly across them. The authors build a knowledge graph per document and merge them into one cross-document graph, then retrieve using vector embeddings of graph relations. On 500 documents and 296 multi-hop questions it beats the baseline in accuracy, semantic similarity, and answer quality.
**🗣️ Tell your mentor (2 sentences):** "This paper is the closest to my work — it builds cross-document knowledge graphs for multi-hop QA. My project extends it by adding source citations and a larger synthetic dataset with known ground truth."

---

*End of paper summaries. See `references-ieee.md` for the IEEE-formatted reference list and `00-how-to-use.md` for how to use this in your PPT and report.*
