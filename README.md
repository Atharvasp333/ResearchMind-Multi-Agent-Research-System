# ResearchMind — Multi-Agent AI Research System

An autonomous, multi-agent AI research platform designed to investigate complex topics, synthesize deep insights, and generate rigorous, peer-reviewed research reports.

Rather than relying on a single prompt or generic search query, ResearchMind distributes the research lifecycle across specialized AI agents and reasoning chains. These components discover current web information, extract in-depth source material, write structured academic/industry-grade reports, and subject the findings to strict critical evaluation.

---

## Architecture Overview

```
                      [ User Input: Research Topic ]
                                     │
                                     ▼
                           ┌───────────────────┐
                           │ 01. Search Agent  │
                           └───────────────────┘
                                     │ (Web results & candidate URLs)
                                     ▼
                           ┌───────────────────┐
                           │ 02. Reader Agent  │
                           └───────────────────┘
                                     │ (Deep scraped textual content)
                                     ▼
                           ┌───────────────────┐
                           │ 03. Writer Chain  │
                           └───────────────────┘
                                     │ (Structured draft report)
                                     ▼
                           ┌───────────────────┐
                           │ 04. Critic Chain  │
                           └───────────────────┘
                                     │ (Objective review & score)
                                     ▼
              [ Formatted Report + Critic Review + Markdown Export ]
```

---

## Core Features & Capabilities

* **Autonomous Multi-Stage Pipeline**: Conducts end-to-end research without manual intervention, passing contextual state smoothly from discovery to final critique.
* **Live Web Grounding**: Gathers real-time, verified information from the live web instead of relying solely on frozen model training data.
* **Deep Page Extraction**: Cleans and extracts the core textual body from the most relevant source page, removing scripts, navigation bars, and footers for high-density analysis.
* **Structured Report Generation**: Formats research into clear sections (Introduction, Key Findings, Conclusion, and Cited Sources).
* **Automated Peer Review & Scoring**: A dedicated critic agent evaluates the report on a 1-to-10 scale, detailing strengths, weaknesses, and a concluding verdict.
* **Interactive Web Dashboard**: Built with a dark-themed user interface featuring custom typography, responsive step cards, and progress spinners.
* **Transparent Pipeline Inspection**: Expandable raw-data panels allow users to audit the exact search snippets and scraped page content used by the agents.
* **One-Click Export**: Allows downloading the finalized research report directly as a formatted Markdown (`.md`) file.
* **Dual Execution Modes**: Can run as an interactive Streamlit web application or as a standalone CLI script for headless environments.

---

## Specialized Agents & Chains

The system splits the research cognitive load into four specialized stages:

### 1. Agent 01 — Search Agent
* **Role**: Primary discovery and information gathering.
* **Behavior**: Receives the user’s topic and formulates targeted web queries. It analyzes the search space and gathers top relevant results with titles, URLs, and concise snippets.
* **Tool Used**: Web search interface powered by the **Tavily Search API**.

### 2. Agent 02 — Reader Agent
* **Role**: Deep-content reading and extraction.
* **Behavior**: Evaluates the discoveries supplied by the Search Agent, selects the most authoritative URL, and reads the full web page content to extract detailed facts, data points, and technical nuance.
* **Tool Used**: HTML scraper that parses DOM structures and strips boilerplate using **BeautifulSoup4**.

### 3. Stage 03 — Writer Chain
* **Role**: Research synthesis and structured writing.
* **Behavior**: Takes the combined outputs from both the Search Agent and Reader Agent. It synthesizes these disparate pieces into a cohesive, publication-ready research report with point-by-point explanations and transparent source citations.

### 4. Stage 04 — Critic Chain
* **Role**: Quality assurance and rigorous peer review.
* **Behavior**: Inspects the generated draft under strict objective criteria. It checks factual clarity, depth, source attribution, and logical structure, returning a standardized review with an overall score out of 10, key strengths, areas to improve, and a final verdict.

---

## Technologies & Ecosystem

| Component | Technology / Library | Purpose |
| :--- | :--- | :--- |
| **LLM Inference** | **Groq Cloud (LPU)** (`openai/gpt-oss-120b`) | Ultra-fast inference with deterministic settings (`temperature=0`) |
| **Agent Orchestration** | **LangChain** (`langchain`, `langchain-core`) | Agent runtime, tool binding, prompts, and LCEL chains |
| **Provider Adapter** | **`langchain-groq`** | Groq chat model integration for LangChain |
| **Search Engine** | **Tavily Search API** (`tavily-python`) | Agent-optimized search engine returning high-relevance results |
| **Scraping & Parsing** | **BeautifulSoup4**, **Requests**, **lxml** | HTML DOM parsing, noise removal, and clean text extraction |
| **Frontend UI** | **Streamlit** | Interactive UI with custom CSS, reactive step cards, and session management |
| **Environment Config** | **python-dotenv** | Secure management of API keys and environment variables |
| **Terminal & Utilities** | **Rich**, **Pydantic**, **Tenacity** | Terminal formatting, data validation, and retry handling |

---

## Project Structure

```text
Multi Agent Research System/
│
├── .env                  # Environment file for API keys (Ignored by Git)
├── .env.example          # Environment template with placeholders
├── .gitignore            # Git exclusion rules
├── README.md             # Project documentation
├── requirements.txt      # Python dependencies
│
├── agents.py             # Agent definitions, prompts, and LCEL chain setup
├── tools.py              # Web search and scraping tools
├── pipeline.py           # CLI runner for the multi-stage research pipeline
└── app.py                # Streamlit web application dashboard
```

---

## Getting Started

### 1. Prerequisites
* Python 3.10 or higher
* Groq API Key ([console.groq.com](https://console.groq.com/keys))
* Tavily Search API Key ([tavily.com](https://tavily.com))

### 2. Installation
Clone the repository and install dependencies:
```bash
pip install -r requirements.txt
```

### 3. Environment Configuration
Duplicate `.env.example` as `.env` and fill in your API keys:
```bash
# On Linux/macOS
cp .env.example .env

# On Windows PowerShell
Copy-Item .env.example .env
```
Inside `.env`:
```env
GROQ_API_KEY=your_actual_groq_api_key
TAVILY_API_KEY=your_actual_tavily_api_key
```

### 4. Running the Application

* **Interactive Web App (Streamlit)**:
  ```bash
  streamlit run app.py
  ```

* **Command-Line Interface (CLI)**:
  ```bash
  python pipeline.py
  ```

