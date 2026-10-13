# Web Browser Automation Agent

An interactive Streamlit application that accepts natural-language instructions and uses an MCP-connected Playwright browser agent to navigate pages, interact with elements, and summarize information.

**Maintained and customized by Dhruv Mittal.** This repository adapts an existing browser-automation example; see [Acknowledgements](#acknowledgements) for source attribution.

## Features

- Natural-language instructions for browser tasks
- Page navigation, scrolling, clicking, and form interaction through Playwright MCP
- Web-page content extraction and Markdown summaries
- Multi-step browsing workflows
- Streamlit interface for submitting tasks and viewing results
- OpenAI model configuration, with an optional OpenAI-compatible local endpoint such as Ollama

## Requirements

- Python **3.10 or newer**
- Node.js and npm (used to launch `@playwright/mcp` through `npx`)
- An OpenAI API key, unless you configure a compatible local model endpoint

## Setup

### 1. Clone the repository and enter its directory

```bash
git clone https://github.com/Dhruv-ux-dev/web-browser-automation-agent.git
cd web-browser-automation-agent
```

### 2. Create a virtual environment and install dependencies

```bash
python3 -m venv .venv
source .venv/bin/activate        # macOS/Linux
# On Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Configure credentials

The simplest option is to set your key in the shell before starting the app:

```bash
export OPENAI_API_KEY="your-openai-api-key"  # macOS/Linux
# On Windows PowerShell: $env:OPENAI_API_KEY="your-openai-api-key"
```

Alternatively, copy the safe example file and edit the local copy:

```bash
cp mcp_agent.secrets.yaml.example mcp_agent.secrets.yaml
```

Replace `YOUR_OPENAI_API_KEY` with your own key. **Never commit `mcp_agent.secrets.yaml` or share your API key.** The `.gitignore` file excludes the local secrets file.

### 4. Run the app

Make sure Node.js and npm are available, then run:

```bash
node --version
npm --version
streamlit run main.py
```

Streamlit will print a local URL (usually `http://localhost:8501`). Open it, enter a task in **Specify Actions**, and click **Execute Command**. The first agent run may take longer while `npx` obtains the Playwright MCP package.

## Example tasks

- `Open example.com and summarize the main page.`
- `Search a public documentation site for installation instructions and summarize the steps.`
- `Navigate to a public article, extract its main points, and return a concise summary.`

Use browser automation only on sites and accounts you are authorized to access. Review actions carefully before automating forms or other changes that affect real accounts or data.

## Configuration

The MCP server and model are configured in `mcp_agent.config.yaml`. The default model is `gpt-4o-mini`; update it there if you use a different supported model. The Playwright MCP server is launched using `npx @playwright/mcp@latest`.

For an OpenAI-compatible local endpoint such as Ollama, edit the `openai` section in `mcp_agent.config.yaml` to set the appropriate `base_url` and model name, and configure a local placeholder key in `mcp_agent.secrets.yaml` as required by your backend. Local model tool-calling compatibility depends on the model and server configuration.

## Project structure

```text
web-browser-automation-agent/
├── main.py                         # Streamlit UI and agent workflow
├── mcp_agent.config.yaml            # MCP server and model configuration
├── mcp_agent.secrets.yaml.example   # Safe credentials template
├── requirements.txt                 # Python dependencies
├── .gitignore                       # Excludes secrets, logs, and local files
└── README.md
```

## Troubleshooting

- **Authentication error:** set `OPENAI_API_KEY` or configure your local `mcp_agent.secrets.yaml`.
- **`npx`/Playwright MCP does not start:** confirm Node.js and npm are installed and available on `PATH`; check your network access for the first package download.
- **Python dependency conflicts:** use Python 3.10+ and install from `requirements.txt` in a fresh virtual environment. The requirements file caps the Python MCP SDK below version 2 because this app has not been migrated to the MCP SDK v2 API.

## Acknowledgements

The starting implementation contains source attribution to **Coder Coder / CodinzHub**. This repository retains that acknowledgement because the project is adapted from an existing browser-agent example. The current maintenance and customizations are by **Dhruv Mittal**.
