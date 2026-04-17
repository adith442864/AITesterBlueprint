# Project 21: DeepEval for SDET - Practical LLM Testing

## Overview

This project takes the evaluation concepts from Project 20 and puts them into production-grade SDET practice. You will build real test suites using DeepEval, write custom metrics, test actual LLM-powered features (chatbots, summarizers, classifiers), and integrate everything into a CI/CD pipeline with quality gates. This is the hands-on, code-heavy counterpart to the theory in Project 20.

## Objective

Build production-ready LLM test suites using DeepEval with real SDET patterns: custom metrics, parameterized test cases, threshold-based quality gates, regression tracking, and automated CI/CD evaluation.

## Tech Stack

| Technology | Purpose |
|-----------|---------|
| Python 3.11+ | Core language |
| DeepEval | LLM evaluation framework |
| Pytest | Test runner and assertions |
| Pydantic | Input/output schema validation |
| FastAPI | Sample LLM app to test against |
| ChromaDB | Vector store for RAG test target |
| GitHub Actions | CI/CD evaluation pipeline |
| Ollama / OpenAI | LLM providers |

## What You Will Learn

- Set up DeepEval in an existing SDET project structure
- Write parameterized LLM test cases with multiple metrics per test
- Build custom DeepEval metrics for domain-specific evaluation
- Test a chatbot for answer relevancy, faithfulness, and tone
- Test a summarizer for completeness, conciseness, and factual accuracy
- Test a classifier for precision, recall, and edge case handling
- Build golden datasets from production logs
- Set up quality gates (fail CI if faithfulness drops below 0.85)
- Track metric drift across releases with DeepEval dashboard
- Run evaluation suites against both OpenAI and local Ollama models

## Key Deliverables

1. **Chatbot Test Suite** - 20+ test cases evaluating a QA chatbot for relevancy, hallucination, and helpfulness
2. **Summarizer Test Suite** - Tests for document summarization accuracy and completeness
3. **Classifier Test Suite** - Tests for bug severity classification with confusion matrix analysis
4. **Custom Metrics** - Domain-specific metrics (e.g., "QA terminology accuracy", "test step completeness")
5. **Golden Dataset Builder** - Script to generate golden datasets from production examples
6. **Quality Gate Pipeline** - GitHub Actions workflow with threshold-based pass/fail gates
7. **Drift Detection Dashboard** - Track how evaluation scores change across model versions or prompt changes
8. **Sample LLM App** - FastAPI app with chatbot, summarizer, and classifier endpoints to test against

## Project Structure

```
Project_21_DeepEval_SDET/
├── README.md
├── requirements.txt
├── app/
│   ├── main.py                    # FastAPI sample LLM app
│   ├── chatbot.py                 # QA chatbot endpoint
│   ├── summarizer.py              # Document summarizer endpoint
│   └── classifier.py              # Bug severity classifier endpoint
├── tests/
│   ├── conftest.py                # Shared fixtures, model config
│   ├── test_chatbot/
│   │   ├── test_relevancy.py
│   │   ├── test_hallucination.py
│   │   └── test_helpfulness.py
│   ├── test_summarizer/
│   │   ├── test_completeness.py
│   │   ├── test_conciseness.py
│   │   └── test_factual.py
│   ├── test_classifier/
│   │   ├── test_severity.py
│   │   └── test_edge_cases.py
│   └── test_regression/
│       └── test_golden_dataset.py
├── metrics/
│   ├── qa_terminology_metric.py   # Custom: checks QA-specific language
│   ├── test_step_metric.py        # Custom: validates test step structure
│   └── tone_metric.py             # Custom: professional tone checker
├── datasets/
│   ├── chatbot_golden.json
│   ├── summarizer_golden.json
│   ├── classifier_golden.json
│   └── build_dataset.py
├── reports/
│   ├── generate_report.py
│   └── drift_tracker.py
└── .github/
    └── workflows/
        └── deepeval_ci.yml
```

## Getting Started

### Prerequisites
- Python 3.11+
- OpenAI API key or Ollama running locally
- DeepEval account (free tier) for dashboard tracking

### Installation
```bash
cd Project_21_DeepEval_SDET
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Start the Sample App
```bash
uvicorn app.main:app --reload --port 8000
```

### Run All Evaluation Tests
```bash
deepeval test run tests/
```

### Run Specific Test Suite
```bash
deepeval test run tests/test_chatbot/ -v
```

### Generate Evaluation Report
```bash
python reports/generate_report.py
```

### Track Drift
```bash
python reports/drift_tracker.py --compare latest
```

## Starter Projects

This project includes two complete starter projects in the `projects/` folder:

### Project 21.1: QA Chatbot Evaluator (`projects/01_QA_Chatbot_Evaluator/`)
- **What you build:** A FastAPI QA chatbot + complete DeepEval test suite
- **What you evaluate:** Answer relevancy, faithfulness, hallucination detection
- **Includes:** Chatbot server, knowledge base documents, golden dataset, HTML report generator
- **Goal:** Set up your first real LLM evaluation workflow end-to-end

### Project 21.2: RAG Pipeline Quality Gate (`projects/02_RAG_Pipeline_Quality_Gate/`)
- **What you build:** An automated CI/CD quality gate for a RAG pipeline
- **What you evaluate:** 6 metrics with threshold-based pass/fail, A/B model comparison
- **Includes:** Full RAG pipeline, quality gate runner, GitHub Actions workflow, drift tracker
- **Goal:** Block bad LLM changes from merging, just like you block failing E2E tests

## QA Angle

This is where SDET meets AI evaluation. As an SDET, you already write automated test suites, set up CI/CD gates, and track quality metrics. This project teaches you to apply those exact same patterns to LLM-powered features. Instead of asserting `response.status == 200`, you assert `faithfulness_score >= 0.85`. Instead of checking UI elements, you check if the AI hallucinates. The testing mindset is the same - the metrics are different. Every SDET working on AI-powered products needs this in their toolkit.
