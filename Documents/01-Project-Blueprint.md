# RAG → GraphRAG Project Blueprint

**For:** Kishan (Final-year Master's student)
**Goal:** Build a professional GraphRAG Q&A system
**Budget:** ₹0 (100% free)
**Timeline:** 6–7 weeks
**Date:** Blueprint v1

---

## 1. What is this project? (one line)

A smart assistant that reads your documents, understands how people and things connect across them, and answers multi-step questions — without guessing.

---

## 2. Two concepts, made simple

### RAG (the foundation)
A robot that answers questions using YOUR documents instead of guessing from memory.

### GraphRAG (the upgrade)
RAG + a knowledge graph. The robot doesn't just search text — it understands how people, projects, and concepts connect across many documents.

**Why GraphRAG beats basic RAG:**
- Basic RAG answers: "What does this document say about X?"
- GraphRAG answers: "Who manages the lead engineer of Project Atlas?" (needs to hop across documents)

---

## 3. How RAG works (simple flow diagram)

```
  ┌──────────────────┐
  │   Documents      │   (your PDFs, notes)
  │  (PDF / notes)   │
  └────────┬─────────┘
           │
           ▼
  ┌──────────────────┐
  │  Cut into chunks  │   (small readable pieces)
  └────────┬─────────┘
           │
           ▼
  ┌──────────────────┐
  │   Embeddings     │   (turn text into numbers)
  └────────┬─────────┘
           │
           ▼
  ┌──────────────────┐
  │  Vector DB       │   (store + search)
  │  (Chroma)        │
  └────────┬─────────┘
           │
           ▼   (when you ask a question)
  ┌──────────────────┐
  │  Find best       │
  │  matching chunks │
  └────────┬─────────┘
           │
           ▼
  ┌──────────────────┐
  │   Send to LLM    │ ───► Answer
  └──────────────────┘
```

---

## 4. How GraphRAG adds a layer

```
                ┌─────────────────────────┐
                │     Knowledge Graph      │
                │  (people, projects,      │
                │   relationships)         │
                └────────────┬────────────┘
                             │
  Your question ────────────►│
                             │
                             ▼
                ┌─────────────────────────┐
                │  Vector search          │
                │   + Graph search        │
                │   (combined)            │
                └────────────┬────────────┘
                             │
                             ▼
                ┌─────────────────────────┐
                │  Multi-hop answer       │
                │  (grounded, cited)       │
                └─────────────────────────┘
```

---

## 5. Tech Stack (100% free)

| Component | Free Tool | Why |
|---|---|---|
| Language | Python | Best for RAG, free |
| Framework | LangChain | Ready-made RAG + GraphRAG pieces |
| LLM (brain) | Groq free API (primary) + Ollama 3B (backup) | ₹0, no card |
| Embeddings | sentence-transformers (all-MiniLM-L6-v2) | Free, offline, fast |
| Vector DB | Chroma (local) | Free, beginner friendly |
| Graph store | NetworkX (simple) → optional Neo4j Community | Free |
| Web UI | Streamlit | Free, makes chat app fast |
| Editor | Kiro IDE / VS Code | Free |

**Total cost = ₹0**

---

## 6. Your Hardware Check

| Component | Your spec | How it affects the project |
|---|---|---|
| CPU | i5-10210U (4C/8T) | Enough for coding + running the app |
| RAM | 8 GB (7.83 usable) | Tight for big local LLMs; fine with cloud path |
| GPU | MX350 2GB | Weak; not useful for LLMs |
| Disk | ~277 GB free | Plenty (we need ~15 GB) |
| **Verdict** | **Good enough** | With the cloud LLM path, you're fine |

---

## 7. LLM Choice — Why Groq (and a local backup)

You have WiFi at home but only a mobile hotspot (Airtel/Jio) at college demos.

**Good news:** API calls send/receive only text (a few KB). So even slow 4G hotspot is more than enough. The real risk is connectivity dropping, not speed.

| Option | Speed | Cost | Internet? | Card? | Role |
|---|---|---|---|---|---|
| **Groq free API** | ⚡ Very fast | ₹0 | Yes (hotspot OK) | No | **Primary** |
| HuggingFace free | Medium | ₹0 | Yes | No | Backup cloud |
| Google Gemini free | Fast | ₹0 | Yes | Account | Backup cloud |
| Local Ollama 3B | Slow on your laptop | ₹0 | No | No | Offline demo backup |

**Plan:**
- Primary: Groq free API (fast, free, no card).
- Backup: local Ollama with a small 3B model — only switch to it if internet dies during your demo.
- **Demo tip:** Pre-test the FULL demo on your hotspot at home before the real college presentation.

---

## 8. Week-by-Week Plan (6–7 weeks)

| Week | Phase | What we build | Approval gate |
|---|---|---|---|
| 1 | Setup + Phase 1 start | Install Python, tools; load docs; first chunking | ⏸️ approve |
| 2 | Phase 1 finish | Embeddings + Chroma + basic Q&A in terminal | ⏸️ approve |
| 3 | Phase 2 | Extract entities + relationships → build graph | ⏸️ approve |
| 4 | Phase 3 | Multi-hop retrieval (vector + graph) | ⏸️ approve |
| 5 | Phase 4 | Streamlit web UI + citations + logging | ⏸️ approve |
| 6 | Polish + test | README, error handling, test multi-hop Qs | ⏸️ approve |
| 7 | Buffer | Fix bugs / improve / demo prep | ✅ done |

---

## 9. What We Build in Each Phase (simple)

- **Phase 1 — Vector RAG**
  - Load documents → cut into chunks → turn into numbers → store in Chroma
  - Ask a question → find relevant chunks → LLM answers
  - *Output:* basic "What does this doc say?" Q&A

- **Phase 2 — Knowledge Graph**
  - LLM reads chunks → pulls out **entities** (people, projects, orgs) and **relationships** (manages, works-on, reviewed-by)
  - Store as a graph (nodes + lines) in NetworkX
  - *Output:* system that "sees" how things connect

- **Phase 3 — Multi-hop Q&A**
  - Question comes in → search BOTH the vector store AND the graph
  - Combine → answer cross-document questions
  - *Output:* this is what beats the buzzword version 😏

- **Phase 4 — Professional polish**
  - Web UI (chat screen, upload docs, ask questions)
  - Show **source citations** (which doc, which line)
  - Logging, error handling, clean README

---

## 10. Synthetic Test Data Plan

Since you have no documents, we create a **fictional company** with overlapping entities — perfect for testing multi-hop:

- **Company:** "Aether Labs" (fictional)
- **~12 people** with roles (CEO, managers, engineers, designers)
- **3–4 projects** with teams
- **~15–20 documents:** meeting minutes, project reports, org chart, email threads, performance reviews
- **The magic:** the same people appear across multiple docs in different relationships
- **Why this is great:** we know the ground truth, so we can **verify** multi-hop answers are correct

**Example test questions we'll answer:**
- "Who manages the lead engineer of Project Atlas?"
- "Which projects share team members?"
- "Who reviewed the people working on Project Atlas?"

---

## 11. Honest Limitations (no surprises)

| Risk | Reality | Mitigation |
|---|---|---|
| Free cloud LLM can hit rate limits | Real | Keep local Ollama backup ready |
| Graph quality depends on model | Smaller models = noisier graphs | Groq's free models are strong enough |
| 6–7 weeks is tight for GraphRAG | It's advanced | We use LangChain patterns (not from scratch) |
| Multi-hop may sometimes hallucinate | Real risk in all GraphRAG | Citations make answers checkable |
| Hotspot may drop during demo | Real | Local backup + pre-test at home |

---

## 12. Cost Summary

- **Money: ₹0**
- No paid APIs, no credit cards, all free tools
- If anything ever needs money, we STOP and ask Kishan first

---

## 13. Next Steps

1. Kishan gives final "go" → we begin Week 1.
2. We install Python, Ollama, LangChain, Chroma, Streamlit.
3. We test Groq API connection works.
4. We build Phase 1 step by step, with approval at each gate.

**Nothing gets built until Kishan says "start."**

---

*End of Blueprint v1*
