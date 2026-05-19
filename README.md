# GAIA Agent - Hugging Face Agents Course

## Description

This project was developed as the final assignment for the Hugging Face Agents Course.

The goal of the project is to create an AI agent capable of solving simplified GAIA benchmark tasks using:
- LangGraph
- LangChain
- Retrieval Augmented Generation (RAG)
- external tools
- web search
- routing logic

---

# Features

The agent can:
- answer basic knowledge questions,
- perform mathematical calculations,
- retrieve weather information,
- search the web using DuckDuckGo,
- route questions dynamically using LangGraph.

---

# Technologies Used

- Python
- LangGraph
- LangChain
- Hugging Face Transformers
- DuckDuckGo Search
- GPT2
- BM25 Retrieval

---

# Project Structure

```text
unit4/
│
├── app.py
├── requirements.txt
├── gaia_agent.ipynb
├── unit4_notes.md
└── README.md
```

---

# Agent Architecture

The project uses:
- StateGraph
- tools
- conditional routing
- simple multi-tool orchestration

The workflow:
1. receives a question,
2. decides which tool to use,
3. executes the tool,
4. returns the final answer.

---

# Notes

Some official course examples relied on:
- GPT-4o,
- OpenAI APIs,
- advanced tool-calling,
- async workflows.

This implementation was adapted to run locally with compatible Hugging Face and LangGraph components.