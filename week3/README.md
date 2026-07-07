# Week 3 — Homework 3: AI Orchestration with Kestra

Source: https://courses.datatalks.club/llm-zoomcamp-2026/homework/hw3
Module: `03-orchestration`, flow: `flows/4_simple_agent.yaml` (task `multilingual_agent` → `english_brevity` → `log_token_usage`)

## Answers

**Q1.** After trying the same prompt in ChatGPT vs Kestra AI Copilot, what is the primary reason AI Copilot generates better Kestra flows?
→ **AI Copilot has access to current Kestra plugin documentation**
Reasoning: this is a context-engineering/RAG point (see `lessons/02-context-engineering.md`) — ChatGPT only has training-data knowledge of Kestra's YAML syntax and plugins, which drifts out of date; AI Copilot is grounded in Kestra's actual current plugin docs.

**Q2.** The non-RAG response about Kestra 1.1 features is best described as:
→ **Vague, generic, or fabricated — the model guesses from training data**
Reasoning: without retrieval grounding, the model has no real source for a specific version's release notes and hallucinates plausible-sounding but unverifiable claims.

**Q3.** Approximate output token count for `multilingual_agent` with `summary_length = short`?
→ **60–100 tokens**
Reasoning: the flow's system prompt (`4_simple_agent.yaml` line 55) defines "short" as strictly 1–2 sentences of factual, fluff-free text — that's roughly 40–70 words ≈ 60–90 tokens.

**Q4.** With `summary_length = long`, roughly how many times more output tokens vs short?
→ **2–5x more**
Reasoning: "long" is defined as 1–3 paragraphs (line 57) vs "short"'s 1–2 sentences. Paragraphs run ~50–100 words each, so 1–3 paragraphs ≈ 150–300 words — about 2–4x the short summary's word count, not an order of magnitude.

**Q5.** After changing `english_brevity` to ask for 3 sentences instead of 1, output token count vs original?
→ **2–4x more**
Reasoning: `english_brevity`'s prompt (line 63) hard-codes "exactly 1 sentence." Tripling the sentence count roughly triples token count (~20–30 tokens → ~60–90 tokens) — a real multiple, not "about the same."

**Q6.** For production workflows requiring deterministic, repeatable results with strict compliance requirements, which approach is most appropriate?
→ **Use traditional task-based workflows for predictability and auditability**
Reasoning: covered in `lessons/08-best-practices.md` — agentic/autonomous flows trade determinism for flexibility; regulated/compliance-heavy production paths need fixed, auditable task sequences instead.

## How to verify these yourself (optional, if time allows)

1. `cd llm-zoomcamp-main/llm-zoomcamp-main/03-orchestration`
2. `docker compose up -d` (starts local Kestra — see this folder's own `docker-compose.yml`)
3. Open `http://localhost:8080`, import `flows/4_simple_agent.yaml`, add your `GEMINI_API_KEY` secret.
4. Execute with `summary_length=short`, then `long` — check the **Outputs** tab / `log_token_usage` task output for real `tokenUsage.outputTokenCount` values.
5. Edit `english_brevity`'s prompt to "exactly 3 sentences", re-run, compare.

## Learning-in-public

- [ ] one LinkedIn/X post on the RAG vs non-RAG Kestra Copilot comparison (Q1/Q2 insight)
