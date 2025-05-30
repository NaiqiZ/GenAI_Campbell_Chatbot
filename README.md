# ALAB_Campbell_MarketingChatbot

This repository documents our project developed as part of the MIT GenAI Lab (15.S04), designed for Campbell’s marketing team to analyze Amazon advertising data via a chat interface powered by LangGraph and Databricks MLflow.

---

## Project Overview

We built a custom multi-agent system that enables business users to ask marketing questions in plain English and receive data-backed insights in real-time.

The system connects:
- Structured advertising data in Databricks
- SQL querying through Genie Agent
- Interpretation via LLMs and LangGraph agents

The goal: to empower marketing teams with actionable answers through a secure, easy-to-use chat interface.

---

## Technical Approach

- **Language**: Python, SQL 
- **Model**: LangGraph with Supervisor, Genie, LLM, and Final Answer agents  
- **LLM Orchestration**: LangGraph  
- **SQL Agent**: Genie Agent (Databricks SQL)  
- **Deployment**: MLflow + Unity Catalog  
- **Interface**: Auto-generated Databricks review app

---

## What This Tool Does

**Ask a marketing question in English, and get back a business-ready, data-grounded answer.**

Example questions:
- “Which keywords had the highest ROAS last month?”
- “What is our ad spend trend over time?”
- “What campaigns should we reinvest in?”

System flow:
1. Interprets user’s question
2. Queries structured data (Genie Agent)
3. Applies LLM interpretation
4. Summarizes into business insight (Final Answer Agent)

---

## Environment & Reproducibility

This tool runs entirely **inside the Databricks environment** and depends on:
- Databricks MLflow model registry and endpoints
- Native LangGraph integration
- Genie SQL Agent with Campbell’s Amazon Ads data access
- Unity Catalog for model governance

**Note**:
- Data is internal to Campbell’s and not included in this repo.
- Tokens and credentials are managed via Databricks secrets and excluded from this repo.

---

## How to Run (Inside Databricks)

### 1. Set up dependencies
```bash
pip install -r requirements.txt
```

### 2. Explore via notebook
Open `interactive_chat` to:
- Test agent response chains
- Trace Genie → LLM → Final output
- Debug full LangGraph step traces

### 3. Log & Deploy with MLflow
```python
mlflow.pyfunc.log_model(...)
mlflow.register_model(...)
agents.deploy(...)
```

---

## Repository Structure

| File | Description |
|------|-------------|
| `agent.py`           | LangGraph agent flow (Supervisor, Genie, LLM, Final Answer) |
| `chat_model.py`      | MLflow wrapper for LangGraph ChatAgent |
| `config.yaml`        | Deployment & runtime configuration |
| `config_utils.py`    | Utility functions for config loading |
| `input_examples.py`  | Sample input cases |
| `interactive_chat`   | Notebook to test and debug flows |
| `requirements.txt`   | Environment dependencies |

---

## Agent Architecture

- **Supervisor Agent** routes queries to the right agent.
- Genie Agent fetches structured data.
- LLM Agent interprets results.
- Final Answer Agent composes the final response.

---


## Deployment Summary

- Model logged using `mlflow.pyfunc.log_model`
- Registered to Unity Catalog under `main.retail_media.campbells_genai_versionFinal`
- Deployed with `agents.deploy()` to expose secure endpoint
- Interface launched via Databricks review app

---

## Team

Members: Ellie Yang, Naiqi Zhang, Brenda Silva, Yu He  
Developed under the MIT GenAI Lab • 2025
