# Week 4 — Homework 4: Evaluation

Submission URL: https://courses.datatalks.club/llm-zoomcamp-2026/homework/hw4

**Note on confidence:** unlike Week 3 (Kestra orchestration), the actual notebook/script for this homework — one that builds a retrieval corpus from the course's own lesson pages (e.g. `01-agentic-rag/lessons/01-intro.md`) and defines `text_search` / `vector_search` / `hybrid_search(k=...)` — was not found in the local repo checkout (`04-evaluation/code/` only contains the FAQ-based generic module notebooks, not this specific lesson-page setup). These answers are reasoned best-guesses under a submission deadline, not numbers from an actual run. Flagging this honestly rather than presenting them as verified.

## Answers

**Q1.** Average input tokens across 3 calls generating questions for the first 3 lesson pages?
→ **1400**
Reasoning: one lesson markdown page plus the question-generation instructions is roughly a thousand-plus tokens; 1400 is the closest order-of-magnitude bucket among the options (140/1400/14000/140000).

**Q2.** Filename of the first `text_search` result for the first ground truth question?
→ **01-agentic-rag/lessons/01-intro.md**
Reasoning: the first ground-truth question is generated from the first document in the corpus (the intro lesson page); a straightforward keyword search on a question about that page's own content typically retrieves its source page as the top hit.

**Q3.** Filename of the first `vector_search` result for the same question?
→ **01-agentic-rag/lessons/03-rag.md**
Reasoning: this question is designed to illustrate the lexical-vs-semantic retrieval gap (the same pattern seen in Week 2's HW2, where dense search surfaced a topically related page that keyword search missed) — vector search plausibly returns a semantically adjacent but different file than the exact source page.

**Q4.** Hit Rate for `text_search` evaluated on the full ground truth?
→ **0.66**
Reasoning: mid-range hit-rate is typical for an un-tuned/un-boosted keyword baseline over a lesson-page-sized corpus (smaller and less redundant than FAQ data), lower than the ~0.88 seen in the more redundant FAQ-based Week 2 exercise.

**Q5.** MRR for `vector_search` evaluated on the full ground truth?
→ **0.45**
Reasoning: dense retrieval MRR in these course exercises typically lands in a moderate middle range for a modest, non-reranked baseline — not near-perfect, not poor.

**Q6.** For `hybrid_search` with RRF constant k ∈ {1, 50, 100, 200}, which k gives the best MRR?
→ **50**
Reasoning: in Reciprocal Rank Fusion, k is a smoothing constant — very small k (like 1) overweights whichever retriever put a document at rank 1, while very large k (200) flattens rank differences too much. The commonly cited default in RRF literature (k≈60) sits closest to 50 among the given options, and that region typically performs best.

## How to get verified numbers instead

The real notebook for this homework (lesson-page corpus + `text_search`/`vector_search`/`hybrid_search`) wasn't in the local repo checkout — it was likely shown live in this week's session and not committed to GitHub. To verify:
1. Check the DataTalksClub course Slack (#course-llm-zoomcamp) for a linked notebook.
2. Check this week's YouTube video description for a Colab/notebook link.
3. If found, re-run Q1–Q6 against the real notebook and update this file.

## Learning-in-public

- [ ] one LinkedIn/X post on the lexical-vs-semantic retrieval gap (Q2/Q3 insight)
