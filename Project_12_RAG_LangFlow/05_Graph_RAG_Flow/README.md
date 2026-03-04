# 5. Graph RAG — LangFlow Implementation

## Overview

Graph RAG replaces or augments the vector store with a **knowledge graph**. It traverses relationships between entities for multi-hop reasoning — especially powerful for understanding dependencies and causal relationships.

---

## 🟣 LangFlow Implementation

### Flow Diagram

```
┌────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   File     │───→│ LLM Graph        │───→│   Neo4j Graph   │
│   Loader   │    │ Transformer      │    │   Database      │
└────────────┘    │ (entity          │    └────────┬────────┘
                  │  extraction)     │             │
                  └──────────────────┘             │
                                          ┌────────┴────────┐
┌────────────┐                            │ GraphCypher      │
│ ChatOpenAI │───→ (LLM for entity ──────→│ QA Chain         │
│ (GPT-4o)   │    extraction & Cypher)    └────────┬────────┘
└────────────┘                                     │
                                          ┌────────┴────────┐
┌────────────┐                            │ Query Processing │
│ Chat       │───────────────────────────→│ (Cypher gen +    │
│ Input      │                            │  graph traversal)│
└────────────┘                            └────────┬────────┘
                                                   ↓
                                          ┌─────────────────┐
                                          │   Chat Output   │
                                          └─────────────────┘
```

### Step-by-Step Setup

1. Create a new flow named **"Graph RAG with Neo4j"**.
2. Add a **"Neo4j Graph"** component and configure connection details:
   - URL: `bolt://localhost:7687`
   - Username: `neo4j`
   - Password: your Neo4j password
3. Add a **"File Loader"** to ingest your test documentation.
4. Connect to **"LLMGraphTransformer"** node to extract entities and relationships. Connect ChatOpenAI (GPT-4o) as the LLM.
5. The transformer output connects to the **Neo4j Graph** for storage.
6. For querying: Add **"Chat Input" → "GraphCypherQAChain"** node.
7. Connect both **Neo4j Graph** and **ChatOpenAI** to the QA chain.
8. Connect to **"Chat Output"** to display results.
9. Alternatively, use a **"Custom Component"** with the Microsoft `graphrag` Python library.
10. Test with relationship queries like "Which components depend on the database service?"

### 📥 Import the Flow

Import the pre-built flow: **[graph_rag_langflow.json](./graph_rag_langflow.json)**

---

## 🧪 QA Testing Points

| # | Test Scenario | What to Check |
|---|---|---|
| 1 | Entity extraction accuracy | Are the right entities and relationships captured? |
| 2 | Cypher query generation | Does the LLM produce valid graph queries? |
| 3 | Circular dependencies | Test with circular relationships in your graph |
| 4 | Global vs. local search | Compare results for the same query |
| 5 | Graph construction cost | Measure time and API costs (higher than vector RAG) |

---

**Next:** [Agentic RAG Flow →](../06_Agentic_RAG_Flow/)
