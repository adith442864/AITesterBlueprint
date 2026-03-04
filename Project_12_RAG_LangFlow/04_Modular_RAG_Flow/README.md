# 4. Modular RAG — LangFlow Implementation

## Overview

Modular RAG treats the RAG pipeline as a set of interchangeable, plug-and-play components with a **query router** that directs queries to the appropriate domain-specific retriever.

---

## 🟣 LangFlow Implementation: Modular RAG with Query Router

### Flow Diagram

```
                         ┌──────────────────┐
                         │   Chat Input     │
                         └────────┬─────────┘
                                  │
                         ┌────────┴─────────┐
                         │ Router Prompt     │
                         │ "Classify query   │
                         │  as api_testing,  │
                         │  ui_testing, or   │
                         │  perf_testing"    │
                         └────────┬─────────┘
                                  │
                         ┌────────┴─────────┐
                         │ ChatOpenAI        │
                         │ (classifier)      │
                         └────────┬─────────┘
                                  │
              ┌───────────────────┼───────────────────┐
              ↓                   ↓                   ↓
     ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
     │ API Docs         │ │ UI Docs          │ │ Perf Docs        │
     │ Vector Store     │ │ Vector Store     │ │ Vector Store     │
     │ + Retriever      │ │ + Retriever      │ │ + Retriever      │
     └────────┬────────┘ └────────┬────────┘ └────────┬────────┘
              └───────────────────┼───────────────────┘
                                  ↓
                         ┌─────────────────┐
                         │ Prompt Template  │
                         │ (final answer)   │
                         └────────┬────────┘
                                  ↓
                         ┌─────────────────┐
                         │ ChatOpenAI       │
                         │ (generator)      │
                         └────────┬────────┘
                                  ↓
                         ┌─────────────────┐
                         │ Chat Output      │
                         └─────────────────┘
```

### Step-by-Step Setup

1. Create a new flow named **"Modular RAG with Query Router"**.
2. Add a **"Chat Input"** node for user queries.
3. Add a **"Prompt"** node configured as a router:
   ```
   Classify this query as api_testing, ui_testing, or performance_testing: {input}
   ```
4. Connect **ChatOpenAI** to the router prompt to get the classification.
5. Create **three separate retriever branches**, each with its own vector store (API docs, UI docs, Performance docs).
6. Use a **"Conditional Router"** or **"Python Function"** node to direct the query to the correct retriever based on the LLM classification.
7. Each branch connects to the same **"Prompt Template"** for final answer generation.
8. Connect to **ChatOpenAI → Chat Output**.
9. Test by sending queries from each domain and verify they route correctly.

### 📥 Import the Flow

Import the pre-built flow: **[modular_rag_langflow.json](./modular_rag_langflow.json)**

---

## 🧪 QA Testing Points

| # | Test Scenario | What to Check |
|---|---|---|
| 1 | Routing accuracy | Does the router classify edge-case queries correctly? |
| 2 | Fallback behavior | What happens when the router is uncertain? |
| 3 | A/B testing generators | Compare different generator models with the same retriever |
| 4 | Module hot-swapping | Verify swapping doesn't break the pipeline |
| 5 | Cross-domain queries | Test queries that span multiple domains |

---

**Next:** [Graph RAG Flow →](../05_Graph_RAG_Flow/)
