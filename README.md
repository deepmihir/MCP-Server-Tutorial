# MCP Server for Documentation Search

This project implements a custom MCP (Model Control Protocol) server that enables Claude to search through documentation for popular Python libraries including LangChain, LlamaIndex, and OpenAI.

## Features

- Search documentation for specific queries across supported libraries
- Integration with Google Search API via Serper for finding relevant documentation pages
- Web scraping capabilities to extract content from documentation pages
- Designed to work with Claude Desktop through MCP

## System Requirements

* Python 3.10 or higher
* MCP SDK 1.2.0 or higher
* `uv` package manager

## Getting Started

### Installing uv Package Manager

On MacOS/Linux:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

On Windows:
```bash
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Make sure to restart your terminal afterwards to ensure that the `uv` command gets picked up. For more information about uv package manager visit : [https://docs.astral.sh](https://docs.astral.sh/uv/getting-started/installation/)

### Project Setup

1. Create and initialize the project:
```bash
# Create a new directory for our project
uv init mcp-server
cd mcp-server

# Create virtual environment and activate it
uv venv
source .venv/bin/activate  # On Windows use: .venv\Scripts\activate

# Install dependencies
uv add "mcp[cli]" httpx
```

2. Create the server implementation file:
```bash
touch main.py
```

### Running the Server

1. Start the MCP server:
```bash
uv run main.py
```

2. The server will start and be ready to accept connections

## Connecting to Claude Desktop

1. Install Claude Desktop from the official website
2. Configure Claude Desktop to use your MCP server:

Edit `~/Library/Application Support/Claude/claude_desktop_config.json`:
```json
{
    "mcpServers": {
        "mcp-server": {
            "command": "uv",  # It's better to use the absolute path to the uv command
            "args": [
                "--directory",
                "/ABSOLUTE/PATH/TO/YOUR/mcp-server",
                "run",
                "main.py"
            ]
        }
    }
}
```

3. Restart Claude Desktop

## Troubleshooting

If your server isn't being picked up by Claude Desktop:

1. Check the configuration file path and permissions
2. Verify the absolute path in the configuration is correct
3. Ensure uv is properly installed and accessible
4. Check Claude Desktop logs for any error messages