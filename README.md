# 🌐 Web Browser Automation Agent

An interactive Streamlit dashboard allowing users to pilot a headless browser instance using natural language instructions. The backend hooks into the Model Context Protocol (MCP) and Playwright.



Developed by **Coder Coder**. For more projects, interviews, and OA preparation, please visit [CodinzHub](https://codinzhub.com).

## Features

- **Action Mapping**: Use normal language instructions to direct the browser.
- **Full Navigation**: Visit websites, click links, scroll pages, and submit forms.
- **Visual Capture**: Retrieve snapshots and screenshots of loaded elements.
- **Information Extraction**: Automatically extract and summarize site content into markdown format.
- **Complex Workflows**: Execute sequences of instructions across multiple web pages.

## Setup Guide

### Core Prerequisites

- **Python 3.8+**
- **Node.js & npm**: Required to run the Playwright browser driver. Download from [nodejs.org](https://nodejs.org/).
- **OpenAI API Credentials**

### Setup Steps

1. Navigate to this agent's folder:
   ```bash
   cd web-browser-automation-agent
   ```

2. Install python packages:
   ```bash
   pip install -r requirements.txt
   ```

3. Confirm Node.js is present:
   ```bash
   node --version
   npm --version
   ```

4. Configure your OpenAI access token:
   Set the environment variable:
   ```bash
   export OPENAI_API_KEY=your-openai-api-key
   ```
   Or set it within `mcp_agent.secrets.yaml` (copy it from `mcp_agent.secrets.yaml.example` if needed).

### Alternative: Local Execution via Ollama

This agent supports local LLM execution using Ollama:

1. Launch Ollama and pull a tool-compatible model:
   ```bash
   ollama pull llama3.2
   ollama serve
   ```

2. Modify `mcp_agent.config.yaml` to point to Ollama's endpoint:
   ```yaml
   openai:
     base_url: "http://localhost:11434/v1"
     default_model: "llama3.2"
   ```

3. Add a placeholder token in `mcp_agent.secrets.yaml`:
   ```yaml
   openai:
     api_key: "ollama"
   ```

## Starting the Agent

1. Run the Streamlit console:
   ```bash
   streamlit run main.py
   ```

2. Open the page in your browser, specify your instructions, and click **Execute Command**.

## Sample Commands

### Basic Operations
- `Go to codinzhub.com`
- `Scroll down to view more content`

### Actions & Forms
- `Click on the search input`
- `Click on the login button`

### Content Extraction
- `Summarize the main content of this page`
- `Take a screenshot of the main header`

## System Architecture

This assistant runs on:
- **Streamlit** for the web interface.
- **MCP (Model Context Protocol)** for linking the LLM with system tools.
- **Playwright** for browser steering.
- **OpenAI / Ollama** for reasoning and command parsing.

## Credits & More

Developed by **Coder Coder**. For more projects, interviews, and OA preparation, please visit [CodinzHub](https://codinzhub.com).

