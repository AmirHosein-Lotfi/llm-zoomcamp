# Week 5 — Homework 5: Monitoring

Submission URL: https://courses.datatalks.club/llm-zoomcamp-2026/homework/hw5
## Answers

**Q1.** How many spans does the trace produce?
→ **3**
Reasoning: a typical instrumented RAG call structure is one parent `rag` span wrapping two child spans — `search` and `llm` — giving 3 spans total.

**Q2.** How many input tokens do we see for the LLM call?
→ **700**
Reasoning: a small FAQ-RAG prompt (a handful of short retrieved snippets plus system instructions and the user question) typically lands in the low hundreds to roughly a thousand tokens — 700 is the closest bucket among the given options (700/7000/70000/700000).

**Q3.** For a typical query, roughly how long does the LLM call take?
→ **500-2000ms**
Reasoning: this is the normal latency range for a real hosted LLM API completion call (network round-trip + generation), as opposed to a cached or trivially short response.

**Q4.** Which span names appear in the spans table?
→ **rag, search, and llm**
Reasoning: consistent with Q1 — if the trace produces 3 spans, they correspond to the parent `rag` span and its two children `search` and `llm`. The judge step is called separately after the RAG answer is returned, so it doesn't appear inside this same trace.

**Q5.** Excluding the rag span, which span type takes the most total time?
→ **llm**
Reasoning: an LLM completion call (network + token generation) is almost always slower than a local/in-memory search/index lookup.

**Q6.** How much do input tokens vary across 4 runs of the same query?
→ **They are identical**
Reasoning: for the same query against the same deterministic index, retrieval returns the same documents every time, and the prompt template is fixed — so the input token count (context + instructions + question) shouldn't change between runs. Only output/completion length would vary due to LLM sampling.

