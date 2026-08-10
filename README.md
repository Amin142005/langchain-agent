
# LangChain Multi-Agent Research Assistant

A Python open-source research automation project built around the LangChain ecosystem and LLM-powered agents. This repository demonstrates a small research workflow that can search the web, scrape selected sources, synthesize findings into a research report, and critique the resulting output.

## Why This Project Exists

This project is a practical starting point for building agentic research assistants that combine information retrieval, web extraction, content synthesis, and evaluation workflows. It is intentionally small and modular, making it a useful foundation for experiments, internal tools, or spin-off products.

## Features

- Agentic web search through Tavily.
- URL scraping and content extraction with `requests`, `BeautifulSoup`, `readability`, and `trafilatura`.
- A LangChain search agent for query planning and retrieval.
- A reader agent that selects and extracts deeper source content.
- A writer chain that produces a structured research report.
- A critic chain that scores and reviews the generated report.
- A Streamlit interface for interactive usage.

## Tech Stack

- Python 3.11+
- LangChain
- LangChain Core
- LangChain OpenAI
- OpenAI models through `ChatOpenAI`
- Tavily search API
- Streamlit
- BeautifulSoup, Readability, Trafilatura, requests
- Python dotenv
- Rich logging

## Architecture

The project follows a simple multi-agent research pipeline:

1. Search Agent
   - The `web_search` tool calls Tavily and collects recent, relevant source metadata.

2. Reader Agent
   - The `scrape_url` tool fetches a selected page and extracts readable content.

3. Writer Chain
   - The writer prompt formats the gathered research into a structured report.

4. Critic Chain
   - The critic prompt assesses the report and returns feedback.

The orchestration layer is implemented in [src/pipelines/pipeline.py](src/pipelines/pipeline.py) and is consumed by the Streamlit application in [app.py](app.py) and the example runner in [main.py](main.py).

## Project Structure

```text
langchain-agent/
├── app.py                 # Streamlit web UI
├── main.py                # Example entry point
├── requirements.txt       # Dependency list
├── src/
│   ├── agents/
│   │   └── agents.py      # LLM agents and prompt chains
│   ├── pipelines/
│   │   └── pipeline.py    # Research execution flow
│   └── tools/
│       └── tools.py       # Search and scrape tool definitions
└── README.md
```

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/langchain-agent.git
cd langchain-agent
```

Create a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Create a `.env` file in the project root with your API keys:

```env
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
```

## Running

Run the example research pipeline:

```bash
python main.py
```

Launch the Streamlit UI:

```bash
streamlit run app.py
```

## Example Usage

The default workflow is configured in [main.py](main.py):

```python
from src.pipelines.pipeline import run_research_pipeline

topic = "the impact of AI on the job market in 2026"
run_research_pipeline(topic)
```

## Contributing

Contributions are welcome. If you want to improve the workflow, add new agents, improve scraping quality, or improve the UI, please open an issue or submit a pull request.

## License

This project is licensed under the MIT License.

