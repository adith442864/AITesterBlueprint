# 1. LangFlow Quick-Start Guide

## What is LangFlow?

LangFlow is an open-source visual framework for building RAG pipelines and AI applications through a drag-and-drop interface. It's built on top of LangChain and provides a visual way to prototype, test, and deploy RAG systems without writing extensive code.

---

## Installation

```bash
# Install LangFlow
pip install langflow

# Launch LangFlow
langflow run

# Or use Docker
docker run -p 7860:7860 langflowai/langflow:latest

# Access at http://localhost:7860
```

---

## Key LangFlow Components for RAG

| Category | Components | Purpose |
|---|---|---|
| **Data Ingestion** | File Loader, URL Loader, Directory Loader | Load documents from various sources |
| **Processing** | Text Splitter, Semantic Chunker | Split documents into chunks |
| **Embeddings** | OpenAI, HuggingFace, Cohere | Convert text to vectors |
| **Vector Stores** | Chroma, Pinecone, FAISS, Weaviate | Store and retrieve embeddings |
| **Retrieval** | Retriever, Ensemble Retriever, Multi-Query | Fetch relevant documents |
| **LLMs** | ChatOpenAI, Anthropic, Ollama, Groq | Generate responses |
| **Agents** | Tool Calling Agent, ReAct Agent | Orchestrate complex workflows |
| **Output** | Chat Output, Text Output | Display results |

---

## Building Your First RAG Flow

### Step 1: Create a New Flow

- Click **"New Flow"** in the LangFlow dashboard
- Choose **"Blank Flow"** or start from the "Vector Store RAG" template
- Name your flow: **"QA Knowledge Base RAG"**

### Step 2: Add Data Ingestion

- Drag a **"File"** component onto the canvas
- Upload your test documentation (PDF, TXT, or DOCX)
- Drag a **"Recursive Character Text Splitter"** and connect it
- Set `chunk_size=1000` and `chunk_overlap=200`

### Step 3: Add Embedding & Storage

- Drag **"OpenAI Embeddings"** onto the canvas
- Enter your API key in the component settings
- Drag a **"Chroma"** vector store component
- Connect: **Text Splitter → Chroma** (documents input)
- Connect: **OpenAI Embeddings → Chroma** (embeddings input)

### Step 4: Add Retrieval & Generation

- Drag a **"Chat Input"** component
- Drag a **"Retriever"** and connect it to Chroma
- Drag a **"Prompt"** template with RAG instructions
- Drag **"ChatOpenAI"** and connect to the prompt
- Drag **"Chat Output"** and connect to ChatOpenAI

### Step 5: Test & Iterate

- Click the **"Play"** button to start the flow
- Open the chat panel and test with sample queries
- Review the execution trace to debug retrieval and generation
- Adjust parameters (chunk size, k value, temperature) and retest

---

## LangFlow API Deployment

```python
# Export your flow as an API
# LangFlow provides a REST endpoint for each flow

import requests

LANGFLOW_API = "http://localhost:7860/api/v1/run/{flow_id}"

response = requests.post(LANGFLOW_API, json={
    "input_value": "What are the login test cases?",
    "output_type": "chat",
    "input_type": "chat"
})

print(response.json()["outputs"][0]["results"]["message"]["text"])
```

---

## 💡 LangFlow Tips for Educators

1. **Visual learning:** Students can SEE the data flow through each component
2. **Progressive complexity:** Start with Naive RAG, then add reranking, routing, evaluation nodes
3. **Execution trace:** Use it to understand what the retriever actually returns
4. **Export & share:** Export flows as JSON to share with classmates
5. **Side-by-side comparison:** Compare flows to understand the impact of each optimization

---

**Next:** [Naive RAG Flow →](../02_Naive_RAG_Flow/)
