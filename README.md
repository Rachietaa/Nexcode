# NexCode

NexCode is a command-line AI coding assistant that can read a local codebase, use MCP tools, query documentation with RAG, search the web, and help complete coding tasks.

## Features

- Agentic workflow built with LangGraph
- Support for Groq, Ollama, OpenAI, and Anthropic
- MCP integration for filesystem access
- Tavily-based web search through MCP
- Custom FastMCP RAG server for local documentation search
- Rich CLI interface
- Session persistence
- Confirm mode and auto mode

## Project Structure


nexcode/
├── agent/
│   ├── __init__.py
│   ├── loop.py
│   └── providers.py
├── config/
│   ├── __init__.py
│   └── settings.py
├── docs_source/
├── mcp_client/
│   ├── __init__.py
│   └── client.py
├── rag_server/
│   ├── __init__.py
│   ├── ingest.py
│   ├── retriever.py
│   └── server.py
├── tools/
│   ├── __init__.py
│   └── executor.py
├── planning/
│   └── architecture.md
├── .env
├── .gitignore
├── main.py
├── README.md
└── requirements.txt
Requirements
Before running the project, install:

Python 3.11

Node.js and npm

Git

Conda or venv

Groq API key

Tavily API key

Optional:

Ollama for local models

Setup
1. Create a Python environment
Using conda:

bash
conda create -n nexcode python=3.11 -y
conda activate nexcode
Using venv:

bash
python -m venv venv
venv\Scripts\activate
2. Install Python dependencies
bash
pip install -r requirements.txt
3. Install MCP packages
bash
npm install -g @modelcontextprotocol/server-filesystem
npm install -g tavily-mcp
Environment Variables
Create a .env file in the project root:

text
GROQ_API_KEY=your_groq_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
OPENAI_API_KEY=your_openai_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here
Only the API keys for the providers you use are required.

Add Documentation for RAG
Place your documentation files inside the docs_source/ folder.

Example supported files:

.txt

.md

Then run:

bash
python rag_server/ingest.py
This builds the local Chroma vector database for retrieval.

Run the Project
Start the assistant with:

bash
python main.py
At startup, NexCode lets you choose:

LLM provider

model

execution mode

whether to resume a previous session

Example Prompts
text
Read main.py and summarize what it does
text
Create a Python file called calculator.py with add, subtract, multiply, and divide functions, then run it to verify it works
text
Search the documentation for how LangChain agents work and create a file called notes.md with a summary
text
Search the web for LangChain ReAct best practices and write the result to research.md
MCP Servers
Filesystem MCP server
Used for:

reading files

writing files

editing files

directory listing

Tavily MCP server
Used for:

web search

external information lookup

Custom FastMCP RAG server
Used for:

querying local documentation

retrieving chunks from ChromaDB

HyDE-based retrieval

Execution Modes
Confirm mode
Asks before executing actions.

Auto mode
Runs actions automatically.

Session Persistence
Chat history is saved locally in:

text
.nexcode_session.json
Common Issues
Conda does not activate
Run:

bash
conda init
Then restart the terminal.

npx not found
Install Node.js and restart your terminal.

Missing Python modules
Make sure your environment is activated, then run:

bash
pip install -r requirements.txt
No documents found in docs_source
Add .txt or .md files to docs_source/ and run:

bash
python rag_server/ingest.py
Demo Ideas
text
Read main.py and summarize what it does
text
Search the web for LangChain ReAct agent best practices and also query the local docs, then write everything into research.md
