# Literature Review Folder — How to Use This

**Project:** GraphRAG: A Knowledge-Graph-Enhanced Retrieval-Augmented Generation Framework for Multi-hop Question Answering
**Student:** Kishan (1BY25SCS07) | **Guide:** Dr. Muneshwar

---

## What's in this folder

| File | What it is | How to use it |
|---|---|---|
| `00-how-to-use.md` | This guide | Read first |
| `papers-summary.md` | All 25 papers in the official 7-field format, each with a paraphrased abstract and a 2-sentence "tell your mentor" note | Main content for your Literature Review section and PPT Related-Work slides |
| `references-ieee.md` | The 25 references in IEEE format | Copy into the References section of your report |

---

## How this maps to your official templates

### For the PPT (Presentation Template.pptx)
The template wants **Related Work on 5–6 slides**, each paper in this exact 7-field format:
- Year of publication (decreasing order)
- Authors
- Research area
- Problems addressed
- Methods or techniques applied
- Advantages
- Research gap identified

`papers-summary.md` already has every paper in exactly those 7 fields. To make slides:
1. Group ~4–5 papers per slide (25 papers ÷ 5–6 slides ≈ 4–5 each).
2. Put each paper's 7-field table (or condensed bullets) on the slide.
3. Order newest-first (the file is already ordered that way).

### For the Report (Phase-1-Review-1 Report format.docx)
The report needs a **Literature Review of 6–8 pages** summarizing 20–25 papers, plus **References (25, IEEE)**.
1. Use `papers-summary.md` as the content for the Literature Review section — narrate it in paragraphs (don't just paste tables; rewrite each paper's 7 fields into 3–5 flowing sentences per paper, grouped by theme).
2. Copy `references-ieee.md` into the References section at the end of the report.
3. Add a short "research gap" paragraph at the end of the Literature Review: most works use an *existing* knowledge graph; few construct a *cross-document entity graph* and even fewer attach *source citations* to answers — that gap is what this project addresses.

---

## ⚠️ Before you submit (academic integrity)

- The abstracts in `papers-summary.md` are **paraphrased**, not copied. Open 3–4 of the linked PDFs and skim the real abstracts so you genuinely understand what each paper did.
- If your mentor asks about any paper, use the **"🗣️ Tell your mentor"** line — it's a ready 2-sentence explanation.
- These are **real, verifiable papers**. Every entry has a working PDF/DOI link. Don't change the titles or authors.

---

## 🗣️ What to tell your mentor about this literature review (in general)

> "I reviewed 25 recent papers on GraphRAG and knowledge-graph-enhanced RAG, mostly from 2025 with a few foundational 2024 works. They show three clear things: first, adding a knowledge graph to RAG consistently improves answer accuracy over plain-text RAG; second, the biggest open problem is multi-hop reasoning across multiple documents; and third, most systems use an existing knowledge graph and very few attach source citations to their answers. My project sits exactly in that gap — it builds a cross-document knowledge graph from the documents themselves and grounds each answer with a citation, which I'll evaluate on multi-hop questions with known ground truth."

---

## How the papers connect to my project (the story)

| Theme | Papers | Why it matters |
|---|---|---|
| Foundational GraphRAG framework | [18], [21] | Define the components and the multi-hop QA task I'm solving |
| Hybrid vector + graph retrieval (my approach) | [20] HybridRAG | Directly supports combining vector DB + KG |
| Cross-document graph for multi-hop | [25] | Closest to my work; I extend it with citations |
| Direct RAG-vs-GraphRAG comparison | [16] | Empirical evidence for my premise |
| Evaluation & benchmarks | [6], [15], [19] | How I'll evaluate honestly |
| Retrieval quality / robustness | [9], [10], [12], [14] | Techniques I can adopt |
| Multi-hop reasoning methods | [4], [7], [8], [11], [23] | Reasoning-loop ideas |
| KG construction / subgraph retrieval | [1], [9], [10], [22] | How I build and search my graph |

---

*If anything looks wrong or you want to swap a paper, tell me and I'll adjust before you submit.*
