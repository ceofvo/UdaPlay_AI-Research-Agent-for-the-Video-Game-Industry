# UdaPlay: AI Game Research Agent

UdaPlay answers video-game questions using a local ChromaDB collection and a web-search tool. The project is run through two notebooks, in order.

## Run

Run these commands from the project root with Python 3.11 or newer:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install "chromadb==0.6.3" "openai==1.68.2" "pydantic==2.10.6" "tavily-python==0.5.1" "python-dotenv==1.0.1" "pdfplumber==0.11.5" "typing-extensions==4.12.2" ipykernel
```

Select the `.venv` kernel in Jupyter or VS Code.

Create a `.env` file in the project root:

```dotenv
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
OPENAI_BASE_URL=your_vocareum_openai_base_url
TAVILY_API_KEY=your_tavily_api_key
```

The embedding cells read `OPENAI_BASE_URL`; without it, they default to the Vocareum endpoint. 

Execute every cell from top to bottom in this order:

1. [Udaplay_01_data_ingestion_and_vector_store.ipynb](Udaplay_01_data_ingestion_and_vector_store.ipynb) reads the JSON records in `games/` and creates/updates the persistent `chromadb/` collection named `udaplay`.
2. [Udaplay_02_agent_retrieve_evaluate_and_web_search.ipynb](Udaplay_02_agent_retrieve_evaluate_and_web_search.ipynb) loads that collection and runs the agent, retrieval evaluation, and web-search workflow.

Start Jupyter from this directory so notebook-relative paths (`games/`, `chromadb/`, and `lib/`) resolve correctly. The second notebook depends on the vector store produced by the first.

## Repository Layout

```text
games/       Game records in JSON format
lib/         Agent, LLM, tools, memory, and vector-store implementation
chromadb/    Persistent local vector store
Udaplay_01...  Ingestion and vector-store notebook
Udaplay_02...  Retrieval, evaluation, and web-search notebook
```
