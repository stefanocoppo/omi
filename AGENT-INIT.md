---
created: 2025-12-30
updated: 2025-12-30
---
# Global Agent Orchestration

> **Multi-agent AI workflows** accessible from any project, vault, or repository.
> Drop this file anywhere - the agent system is globally installed.

---

## Quick Start

```bash
# Run an agent task (routes to best model automatically)
ai-agent run "Summarize this codebase"

# Interactive chat mode
ai-agent chat

# Test setup
ai-agent test

# Direct LLM queries (23 templates available)
llm "Your question"
llm -t architect "Design a REST API"
llm -t deep-research "Latest AI frameworks 2025"
```

---

## Global Agent Commands

| Command | Description |
|---------|-------------|
| `ai-agent run "task"` | Execute task with multi-model routing |
| `ai-agent chat` | Interactive agent mode |
| `ai-agent test` | Verify agent setup |
| `ai-agent list` | Show available models and templates |

---

## LLM CLI Commands

| Command | Description |
|---------|-------------|
| `llm "prompt"` | Query default model (gpt-5.2) |
| `llm -m MODEL "prompt"` | Query specific model |
| `llm -t TEMPLATE "prompt"` | Use a template |
| `llm -c "follow-up"` | Continue conversation |
| `llm logs -q "search"` | Search query history |

---

## Available Templates (23)

### Core Templates
| Template | Model | Usage |
|----------|-------|-------|
| `summarize` | gpt-4o-mini | `llm -t summarize < file.md` |
| `code-review` | claude-opus-4.5 | `llm -t code-review < script.py` |
| `research` | sonar-reasoning-pro | `llm -t research "topic"` |
| `explain` | gpt-4o | `llm -t explain < code.py` |
| `commit-msg` | gpt-4o-mini | `git diff --staged \| llm -t commit-msg` |

### Advanced Templates
| Template | Model | Best For |
|----------|-------|----------|
| `debate` | gpt-5.2 | Multi-perspective analysis |
| `architect` | claude-opus-4.5 | System design |
| `deep-research` | sonar-deep-research | Comprehensive research |
| `refactor` | claude-sonnet-4.5 | Code cleanup |
| `security-audit` | claude-opus-4.5 | Vulnerability analysis |
| `debug` | gpt-5.2 | Error analysis |
| `test-gen` | claude-sonnet-4.5 | Generate tests |
| `pr-review` | claude-opus-4.5 | PR analysis |

---

## Model Routing

The agent automatically routes tasks to the best model:

| Task Type | Model | Why |
|-----------|-------|-----|
| General | gpt-5.2 | Best overall reasoning |
| Code | claude-sonnet-4.5 | Code-optimized |
| Research | sonar-reasoning-pro | Web search with citations |
| Review/Quality | claude-opus-4.5 | Highest quality analysis |
| Quick/Simple | gpt-4o-mini | Fast and cheap |

---

## Example Workflows

### Research → Implement
```bash
# Deep research first
llm -t deep-research "best practices for X" > research.md

# Then implement
cat research.md | llm -m claude-sonnet-4.5 "Implement based on this"
```

### Multi-Model Verification
```bash
QUERY="Should we use microservices?"
llm -m gpt-5.2 "$QUERY"
llm -m claude-opus-4.5 "$QUERY"
llm -m gemini-2.5-pro "$QUERY"
```

### Code Review Pipeline
```bash
cat code.py | llm -t security-audit > security.md
cat code.py | llm -t code-review > review.md
cat code.py | llm -t test-gen > tests.py
```

---

## Installation Location

```
%APPDATA%\claude-agents\
├── agents\
│   ├── graph.py          # Main orchestration
│   ├── config\
│   │   ├── routing.yaml  # Model routing
│   │   └── agents.yaml   # Agent definitions
│   └── tools\
│       ├── llm_client.py # LLM wrapper
│       └── mcp_client.py # MCP wrapper
├── scripts\
│   └── ai-agent.bat      # CLI wrapper
└── data\
    └── agent_state.db    # State persistence

%APPDATA%\io.datasette.llm\
├── templates\            # 23 LLM templates
├── logs.db               # Query history
└── keys.json             # API keys
```

---

## Setup (One-Time)

If `ai-agent` command not found, add to PATH:

```batch
setx PATH "%PATH%;%APPDATA%\claude-agents\scripts"
```

Or run directly:
```batch
%APPDATA%\claude-agents\scripts\ai-agent.bat test
```

---

## Resources

- LLM CLI: https://llm.datasette.io/
- Templates: `llm templates`
- Models: `llm models`
- Logs: `llm logs`

---

*This file can be dropped into any project. The agent system is globally installed and works everywhere.*
