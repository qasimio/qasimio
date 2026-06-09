<div align="center">

<h1 align="center">Qasim Sethar</h1>

<p align="center">
<img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=700&size=28&pause=1000&color=2E6DA4&center=true&vCenter=true&width=800&lines=AI+Systems+Engineer;Autonomous+Agents+·+RAG+·+Retrieval+Infrastructure" />
</p>

</div>

[![Portfolio](https://img.shields.io/badge/Portfolio-qasimio.me-2E6DA4?style=for-the-badge&logo=firefox&logoColor=white)](https://qasimio.me)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-qasimio-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/qasimio)
[![Email](https://img.shields.io/badge/Email-amkassim444%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:amkassim444@gmail.com)
[![Patreon](https://img.shields.io/badge/Patreon-qasimio-F96854?style=for-the-badge&logo=patreon&logoColor=white)](https://patreon.com/qasimio)

</div>

---

## What I Build

I design and implement systems at the boundary between classical software engineering and applied AI — specifically:

- **Autonomous agent loops** that plan, execute, and self-correct over multi-step coding tasks
- **Retrieval pipelines** that ingest messy real-world documents and serve precise, ranked context to LLMs
- **CLI/TUI tooling** that runs locally, requires no cloud dependency, and treats safety as a design constraint

My engineering approach is shaped by one conviction: language models are only as useful as the infrastructure surrounding them. I focus on that infrastructure.

---

## Systems

### Operon — Autonomous Code Intelligence Agent

[![Stars](https://img.shields.io/github/stars/qasimio/Operon?style=flat-square&color=2E6DA4)](https://github.com/qasimio/Operon/stargazers)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://github.com/qasimio/Operon)
[![Textual](https://img.shields.io/badge/TUI-Textual-FF69B4?style=flat-square)](https://github.com/qasimio/Operon)
[![License](https://img.shields.io/github/license/qasimio/Operon?style=flat-square)](https://github.com/qasimio/Operon/blob/main/LICENSE)

A terminal-native agent that operates on a full repository — not just individual files. Operon builds a persistent, hash-gated symbol graph across the entire codebase, then uses it to execute multi-file refactors, generate structured documentation, and answer questions about execution flow.

Key engineering decisions:
- **Deterministic-first REVIEWER**: verifies changes by comparing disk hash to diff memory snapshot before any LLM call — eliminates hallucinated confirmation
- **CRUD fast-path**: structured operations (import insertion, variable renaming, comment placement) handled via `tokenize` and `ast` without LLM — removes the most common failure mode of small local models
- **5-tier surgical diff engine**: SEARCH/REPLACE patching with cascading fallbacks from exact string match through fuzzy multi-line tolerance
- **Mandatory approval gate**: no filesystem write occurs without explicit human confirmation; timeout auto-rejects to prevent hang
- **9-provider LLM router** with hot-reload config — model switching takes effect on the next call, no restart

**→ [github.com/qasimio/Operon](https://github.com/qasimio/Operon)**

---

### MQNotebook — Enterprise RAG System

[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](https://github.com/qasimio/MQNotebook)
[![LlamaIndex](https://img.shields.io/badge/LlamaIndex-8A2BE2?style=flat-square)](https://github.com/qasimio/MQNotebook)
[![Streamlit](https://img.shields.io/badge/Live_Demo-Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](https://mqnotebook.streamlit.app)

A retrieval system designed for the documents that most RAG demos ignore: scanned PDFs, PPTX speaker notes, multi-sheet Excel files. The engineering focus is retrieval correctness under real document conditions.

Key engineering decisions:
- Custom OCR pipeline (Tesseract + Poppler) handles flattened text and image-only pages
- Hybrid search: dense vector retrieval re-ranked by a Cross-Encoder, yielding **~40% precision improvement** over cosine similarity alone
- Session-isolated storage handler resolves Windows file-locking failures (WinError 32) in persistent vector stores
- Context injection optimized to **reduce token usage by ~60%** without precision loss

**→ [github.com/qasimio/MQNotebook](https://github.com/qasimio/MQNotebook) · [Live Demo](https://mqnotebook.streamlit.app)**

---

### DevShelf — Vertical Search Engine (from First Principles)

[![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)](https://github.com/qasimio/DevShelf)
[![IR](https://img.shields.io/badge/Information_Retrieval-555555?style=flat-square)](https://github.com/qasimio/DevShelf)

A search engine for Computer Science literature built without Lucene or ElasticSearch. The goal was to understand retrieval at the data-structure level before building RAG systems on top of it.

Key engineering decisions:
- Positional inverted index with **O(1)** keyword lookup via custom hashing
- Offline Indexer pre-processes corpora at build time, pushing query latency to **sub-millisecond**
- O(L) Trie for prefix-completion; Levenshtein distance for fuzzy matching
- TF-IDF scoring with behavioral re-ranking

The classical IR knowledge from DevShelf directly informs the hybrid search design in MQNotebook.

**→ [github.com/qasimio/DevShelf](https://github.com/qasimio/DevShelf)**

---

### FOLDR — Intelligent File Automation CLI

[![PyPI](https://img.shields.io/pypi/v/foldr?style=flat-square&color=2E6DA4)](https://pypi.org/project/foldr/)
[![PyPI Downloads](https://static.pepy.tech/personalized-badge/foldr?period=total&units=NONE&left_color=BLACK&right_color=GREEN&left_text=downloads)](https://pepy.tech/projects/foldr)
[![Python](https://img.shields.io/badge/python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://pypi.org/project/foldr/)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-blue?style=flat-square)](https://github.com/qasimio/foldr)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](https://github.com/qasimio/foldr/blob/main/LICENSE)

A published CLI tool that keeps directories clean automatically — organizing **240+ file extensions** across **30+ categories** with background watch mode, full undo, deduplication, and custom category configuration. Designed for data pipeline preparation, ML dataset cleaning, and anyone who wants their Downloads folder to organize itself.

```bash
pip install foldr                          # one install, everything included

foldr ~/Downloads --preview               # see the full plan before anything moves
foldr ~/Downloads                         # organize (preview → confirm → move)
foldr ~/Downloads --recursive --depth 2   # include subdirectories
foldr watch ~/Downloads                   # organize now + keep watching forever
foldr undo                                # restore the last operation instantly
```

Key engineering decisions:
- **Background daemon architecture**: `foldr watch` spawns a detached OS-native subprocess that runs indefinitely — using inotify (Linux), kqueue (macOS), or ReadDirectoryChangesW (Windows) — 0% CPU when idle; terminal returns immediately
- **Two-phase watch pipeline**: initial full-directory scan on daemon start organizes existing files, then event-driven processing handles every subsequent arrival — files moved back to root are re-organized; no one-time-only moves
- **JSON undo system**: every organize operation writes an immutable history entry; `foldr undo` reverses any operation independently — git-revert semantics applied to filesystem state
- **240+ extensions, 30+ categories**: Documents, Images, Videos, Audio, Code, Archives, Executables, Databases, Machine Learning models, and more — all configurable via TOML
- **Zero external dependency for output**: ANSI rendering via ctypes (Win10+) with colorama fallback — no rich, no pyfiglet, no curses
- **Conflict-safe moves**: resolves filename collisions by appending `_(1)`, `_(2)` — never overwrites existing files

```bash
foldr ~/Downloads --dedup keep-newest     # remove duplicate files (preview first — irreversible)
foldr history                             # browse all past operations with IDs
foldr config --edit                       # open category config in your editor
foldr watch ~/Downloads --recursive       # watch and organize subdirectories too
```

**→ [github.com/qasimio/foldr](https://github.com/qasimio/foldr) · [pypi.org/project/foldr](https://pypi.org/project/foldr/)**

---

## Tech Stack

<div align="center">

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)

**AI · Agents · Retrieval**

![LlamaIndex](https://img.shields.io/badge/LlamaIndex-8A2BE2?style=for-the-badge)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge)
![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)

**Vector & Search**

![LanceDB](https://img.shields.io/badge/LanceDB-2E6DA4?style=for-the-badge)
![ChromaDB](https://img.shields.io/badge/ChromaDB-FF6F00?style=for-the-badge)
![Tesseract](https://img.shields.io/badge/Tesseract_OCR-333333?style=for-the-badge)

**Systems & Tooling**

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)
![Textual](https://img.shields.io/badge/Textual_TUI-FF69B4?style=for-the-badge)
![Watchdog](https://img.shields.io/badge/Watchdog-4EAA25?style=for-the-badge)
![PyPI](https://img.shields.io/badge/PyPI-3775A9?style=for-the-badge&logo=pypi&logoColor=white)

</div>

---

## Other Work

| Project | What it demonstrates |
|---------|---------------------|
| BabyGPT | Character-level LSTM language model from scratch in TensorFlow |
| Sentiment Filter | NLP edge cases — negation paradox, context-sensitivity |
| MQ Banking Core | Low-level transactional system in C++ with file-level I/O |
| Digital Eye | CNN-based image classification pipeline in Keras |

---

## Currently Working On

- Extending Operon's symbol graph to JS/TS via Babel AST integration
- LSP server mode for editor integration
- Structured output evaluation framework for RAG retrieval quality

---

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=qasimio&label=Profile%20Views&color=2E6DA4&style=flat" alt="profile views" />
</p>

<div align="center">

[![GitHub Streak](https://streak-stats.demolab.com/?user=qasimio&theme=default&hide_border=true)](https://git.io/streak-stats)

*Building systems that make LLMs reliable, not just capable.*

</div>
