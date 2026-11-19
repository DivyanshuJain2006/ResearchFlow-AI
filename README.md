# 🔬 LangGraph Research Assistant

A multi-agent AI research assistant built with **LangGraph, LangChain, Groq, and Tavily**. It generates AI analyst personas, conducts parallel research interviews, retrieves information from the web, and synthesizes findings into a structured research report.

![Python](https://img.shields.io/badge/Python-3.12+-3776AB?logo=python&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-Orchestration-1C3C3C)
![LangChain](https://img.shields.io/badge/LangChain-Framework-1C3C3C)
![Groq](https://img.shields.io/badge/Groq-LLM%20Inference-F55036)
![Tavily](https://img.shields.io/badge/Tavily-Web%20Search-0EA5E9)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📌 Overview

The LangGraph Research Assistant automates a structured research process using multiple AI-generated analyst personas.

Instead of relying on a single AI response, the system creates different analysts with distinct perspectives. Each analyst explores the research topic through an interview workflow, retrieves relevant information using Tavily, and contributes findings to a consolidated report.

The project demonstrates how multi-agent workflows, state management, human-in-the-loop interactions, and parallel execution can be implemented using LangGraph.

## ✨ Features

- **AI Analyst Generation:** Generates multiple analyst personas with different roles, expertise, and perspectives.
- **Human-in-the-Loop:** Allows users to review, approve, or provide feedback on generated analysts.
- **Multi-Agent Research:** Conducts independent research interviews through analyst-specific workflows.
- **Web Search Integration:** Uses Tavily to retrieve relevant information from the web.
- **Structured Outputs:** Uses Pydantic models to structure analyst generation and search queries.
- **Parallel Execution:** Uses LangGraph's `Send` API to initiate multiple analyst interviews.
- **Automated Report Generation:** Combines research findings into a structured Markdown report.
- **LangGraph Studio Support:** Provides graph configurations for local development and workflow inspection.

## 🏗️ Architecture

The system follows a multi-stage research workflow:

```text
                Research Topic
                      |
                      v
              Create Analysts
                      |
                      v
              Generate Personas
                      |
                      v
              Human Feedback
                      |
             +--------+--------+
             |                 |
          Revise             Approve
             |                 |
             v                 v
       Regenerate       Parallel Interviews
                              |
                    +---------+---------+
                    |         |         |
                 Analyst 1 Analyst 2 Analyst 3
                    |         |         |
                    v         v         v
                 Generate Research Questions
                              |
                              v
                       Tavily Web Search
                              |
                              v
                       Generate Answers
                              |
                              v
                       Write Sections
                              |
                              v
                       Combine Findings
                              |
                              v
                       Final Research Report
```

## 🔄 How It Works

1. **Research Topic:** The user provides a topic to investigate.
2. **Analyst Generation:** The LLM generates multiple analyst personas using structured output.
3. **Human Feedback:** The workflow pauses to allow the user to approve or revise the generated analysts.
4. **Parallel Interviews:** LangGraph initiates an interview workflow for each approved analyst.
5. **Web Research:** Tavily retrieves relevant information based on dynamically generated search queries.
6. **Answer Generation:** Groq generates research answers using the retrieved context.
7. **Section Writing:** Each analyst's interview is converted into a research section.
8. **Report Synthesis:** The findings are combined into an introduction, body, conclusion, and final report.

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| LangGraph | Multi-agent orchestration and state management |
| LangChain | LLM integration and structured outputs |
| Groq | LLM inference using `openai/gpt-oss-120b` hosted on Groq |
| Tavily | Web search and information retrieval |
| Pydantic | Structured data models and validation |
| LangSmith | LLM tracing and workflow monitoring |
| uv | Dependency and environment management |

## 📂 Project Structure

```text
LangGraph-Research-Assistant/
│
├── src/
│   ├── __init__.py
│   ├── agent.py
│   ├── answering_questions.py
│   ├── deep_agent.py
│   │
│   └── utils/
│       ├── __init__.py
│       ├── edges.py
│       ├── models.py
│       ├── nodes.py
│       ├── objects.py
│       ├── prompts.py
│       ├── states.py
│       └── tools.py
│
├── screenshots/
│   └── Screenshot 2026-09-08 101749.png
│
├── .env.example
├── .gitignore
├── langgraph.json
├── main.py
├── pyproject.toml
├── uv.lock
└── README.md
```

### Important Files

| File | Responsibility |
|---|---|
| `agent.py` | Analyst generation and human feedback workflow |
| `answering_questions.py` | Interview question-answering graph |
| `deep_agent.py` | Complete research workflow |
| `utils/nodes.py` | Graph node implementations |
| `utils/edges.py` | Conditional routing and parallel execution |
| `utils/states.py` | Graph state definitions |
| `utils/objects.py` | Pydantic models |
| `utils/prompts.py` | LLM prompt templates |
| `utils/models.py` | Groq model initialization |
| `utils/tools.py` | Tavily web search integration |
| `langgraph.json` | LangGraph graph registration |

## 🚀 Getting Started

### Prerequisites

Make sure you have:

- Python 3.12 or higher
- uv package manager
- Groq API key
- Tavily API key

Optional:
- LangSmith API key for tracing and monitoring.

### 1. Clone the Repository

```bash
git clone https://github.com/DivyanshuJain2006/LangGraph-Research-Assistant.git

cd LangGraph-Research-Assistant
```

### 2. Install Dependencies

```bash
uv sync
```

This installs the project dependencies and creates the virtual environment.

### 3. Configure Environment Variables

Create a `.env` file in the root directory.

You can use `.env.example` as a reference.

```env
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key

LANGSMITH_API_KEY=your_langsmith_api_key
LANGSMITH_TRACING_V2=true
LANGSMITH_PROJECT=LangGraph-Research-Assistant
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
```

LangSmith configuration is optional. Keep all actual API keys private and never commit your `.env` file.

### 4. Run the Application

Start the LangGraph development server:

```bash
uv run langgraph dev
```

Open the local development URL displayed in your terminal to access the LangGraph development interface.

## 📥 Example Research Input

**Topic:**

```text
How autonomous AI agents are transforming software engineering.
```

**Example graph input:**

```json
{
  "topic": "How autonomous AI agents are transforming software engineering",
  "max_analysts": 3
}
```

The research workflow generates analyst personas, conducts interviews, retrieves web information, and produces a consolidated Markdown report.

## 🧠 Key Concepts Demonstrated

- Multi-agent system design
- LangGraph StateGraph
- Typed state management
- Conditional graph routing
- Human-in-the-loop interrupts
- Parallel execution using `Send`
- LLM structured output
- Web search and retrieval
- Map-reduce style report synthesis

## 🔐 Security

- Never upload API keys or `.env` files.
- Use `.env.example` to document required environment variables.
- Rotate credentials if they are accidentally exposed.

## 📄 License

This project is licensed under the MIT License.
