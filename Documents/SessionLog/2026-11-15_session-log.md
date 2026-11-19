# Session Log — 15 November 2026 (Sunday)

**Student:** Kishan (1BY25SCS07) | **Guide:** Dr. Muneshwar | **Project:** GraphRAG for Multi-hop QA
**Purpose of this log:** a dated record of everything discussed and built today, to be reloaded at the start of the next session so full context is restored.

---

## 1. Context & Goal
Kishan is a final-year M.Tech (CSE), Sem III student who needs an advanced, professional project and its Phase-I Review-1 deliverables. He prefers simple (ELI5) explanations, tables, and bullet points, and wants approval at each step with no surprises. The project is a **GraphRAG** system for multi-hop question answering.

## 2. Academic & Personal Details
- **USN:** 1BY25SCS07
- **Course:** M.Tech (CSE), Semester III
- **Institution:** BMS Institute of Technology and Management, Yelahanka, Bengaluru (Autonomous, VTU)
- **Guide:** Dr. Muneshwar (designation used = "Associate Professor" to match the template — CONFIRM actual rank)
- **PG Coordinator:** Dr. Raguru Jaya Krishna | **HoD CSE:** Dr. Satish Kumar T | **Associate Head (Cluster-2):** Dr. Shoba M
- **Review:** Phase-I, Review-1 — scheduled 30 October 2026 (per mentor mail)
- **Hardware:** Mi NoteBook Horizon Edition 14, i5-10210U, 8 GB RAM (7.83 usable), MX350 2 GB, ~277 GB free
- **Date note:** system date today is 15 Nov 2026; the mail's review date is 30 Oct 2026 — Kishan to reconcile if needed.

## 3. Hard Rules (must follow every session)
- NEVER mention that Kishan is "lazy" or any personal trait in any deliverable.
- NEVER speak negatively about the guide (Dr. Muneshwar); keep all references professional.
- NEVER fabricate research papers or metadata — use only REAL, verifiable papers.
- No paid tools, no credit-card-required services, no surprises. 100% free.

## 4. Topics Discussed Today (chronological)
1. **RAG explained (ELI5)** — a robot that reads YOUR documents before answering: Retrieve → Augmented → Generate.
2. **GraphRAG explained** — RAG + a knowledge graph (entities = nodes, relations = edges) for relationship-aware retrieval; better on multi-hop questions. Compared with a friend's "connected AI graph RAG" framing: real tech plus buzzwords. Agreed professional path = build solid vector RAG first, then extend to GraphRAG so Kishan can defend every layer.
3. **Project plan** — 4 phases: (1) Vector RAG baseline, (2) Knowledge-graph layer, (3) Multi-hop Q&A, (4) Polish (citations, web UI, README). 100% free tools. 6–7 weeks.
4. **LLM path** — Groq free API (primary, fast, no card, works on mobile hotspot) + local Ollama 3B (offline backup for college demo). Demo tip: pre-test on hotspot at home.
5. **Title locked** (see Section 5).
6. **Official templates analysed** (4 files in ProjectMetaDetails): Presentation Template.pptx, Phase-1-Review-1 Report format.docx, PROJECT DIARY, Industry Internship Diary. The internship diary is NOT Kishan's track.
7. **Gap analysis** — official format needs a heavy literature review (20–25 papers in a 7-field format), 25 IEEE references, and existing-vs-proposed methodology algorithms. These were the main gaps beyond the blueprint.
8. **Delay reason + anticipated mentor questions** prepared (in earlier chat; not a file).
9. **Literature review built** — 25 REAL papers gathered via the OpenAlex API (Python urllib), 7-field summaries + paraphrased abstracts + 2-sentence mentor notes + IEEE references. ACL Anthology used to fetch the 3 papers whose OpenAlex abstracts were missing.
10. **Report draft built** — full Phase-I Review-1 report content.
11. **PPT built** — actual .pptx produced by duplicating the template's slides (preserving logo, dept header, date, background) and swapping text; verified every slide keeps logo + header + date.

## 5. Locked Project Decisions
- **Title:** "GraphRAG: A Knowledge-Graph-Enhanced Retrieval-Augmented Generation Framework for Multi-hop Question Answering"
- **Phases:** 1 Vector RAG → 2 KG layer → 3 Multi-hop Q&A → 4 Polish (citations, UI, README)
- **Budget:** ₹0 (100% free, open source only)
- **Timeline:** 6–7 weeks
- **Data:** synthetic "Aether Labs" enterprise corpus (~12 people, 3–4 projects, ~15–20 docs with overlapping entities) for controlled, verifiable ground truth
- **LLM:** Groq free API primary + Ollama 3B backup
- **Tech stack:** Python, LangChain, Groq + Ollama, sentence-transformers (all-MiniLM-L6-v2), Chroma, NetworkX, Streamlit, Kiro IDE

## 6. Files Created Today (with paths)
| Path | What it is |
|---|---|
| `.kiro\memory\user-context.md` | Persistent memory (rules, decisions, progress, status) |
| `Documents\01-Project-Blueprint.md` | Full project blueprint (plan, tech, timeline, diagrams) |
| `Documents\LiteratureReview\00-how-to-use.md` | How to use the lit-review folder |
| `Documents\LiteratureReview\papers-summary.md` | 25 papers, 7-field each + paraphrased abstract + 2-sentence mentor note |
| `Documents\LiteratureReview\references-ieee.md` | 25 references in IEEE format |
| `Documents\Report\Phase-1-Review-1-Report.md` | Full ~20–22 page report draft (paste into official DOCX) |
| `Documents\PPT\Phase-1-Review-1-Presentation.pptx` | 20-slide PPT built from the official template |
| `Documents\PPT\presentation-content.md` | PPT slide text + speaking script |
| `Documents\SessionLog\2026-11-15_session-log.md` | This log |

## 7. PPT Structure (20 slides)
Title → Content (agenda) → Introduction (Background, Motivation) → Problem Statement → Objectives → Related Work (6 slides, 25 papers in 7-field format) → Design Methodology (System Overview, Existing method, Proposed Phase A, Proposed Phase B, Tools) → Expected Outcomes → Conclusion → References. Verified: every slide has logo + "Department of Computer Science and Engineering" header + date.

## 8. Deliverable Status
- ✅ Blueprint
- ✅ Literature Review (25 real papers, 7-field, IEEE refs)
- ✅ Report draft (full content)
- ✅ PPT (20 slides, exact template format)
- ⬜ Project Diary weekly entries (not started)
- ⬜ Actual GraphRAG build (Week 1: Python/Groq/Chroma setup) — not started

## 9. Open Items / Next Steps
- Confirm Dr. Muneshwar's exact designation (used "Associate Professor"); fix on report + PPT slide 1 if wrong.
- Reconcile date if needed (system today = 15 Nov 2026; mail review date = 30 Oct 2026).
- Kishan to skim 3–4 real paper PDFs before submitting (academic integrity — abstracts are paraphrased).
- Paste report content into the official DOCX; open PPT in PowerPoint and check title fit + Related Work density.
- Optional: split dense Related Work slides if they look cramped.
- Next build options when Kishan is ready: Project Diary entries, or start Week 1 coding (Python, Groq, Chroma).

## 10. How to use this log tomorrow
Load this file (and `.kiro\memory\user-context.md`) at session start. Together they restore: who Kishan is, the rules, the locked decisions, the full tech/plan, all files and their locations, and what is done vs pending. No need to re-ask anything already recorded here.

---
*End of session log — 15 Nov 2026.*
