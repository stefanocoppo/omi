---
created: 2025-12-30T07:53
updated: 2025-12-30T07:53
---
# LLM CLI Integration

> **Zero-configuration AI assistant access** for any project, vault, or repository.
> Drop this file into a project root - no customization required.

---

## Quick Start

```bash
# Verify LLM CLI is installed
llm --version

# Test with auto-detected project context
llm "Hello from this project"

# Use pre-installed global templates
llm -t summarize < any-file.md
llm -t research "best practices for this domain"
```

If `llm` is not installed, see [Installation](#installation) below.

---

## Global Templates (Pre-Installed)

These templates are available in ALL projects immediately:

| Template | Model | Usage |
|----------|-------|-------|
| `summarize` | gpt-4o-mini | `llm -t summarize < file.md` |
| `code-review` | claude-opus-4.5 | `llm -t code-review < script.py` |
| `research` | sonar-reasoning-pro | `llm -t research "topic"` |
| `suggest-tags` | gpt-4o-mini | `llm -t suggest-tags < note.md` |
| `explain` | gpt-4o | `llm -t explain < code.py` |
| `commit-msg` | gpt-4o-mini | `git diff --staged \| llm -t commit-msg` |
| `second-opinion` | gemini-2.5-pro | `llm -t second-opinion < plan.md` |
| `extract-json` | gpt-4o-mini | `llm -t extract-json < unstructured.txt` |

---

## Core Commands

### Query Any Model

```bash
llm "your prompt"                     # Default model
llm -m gpt-4o "prompt"                # Specific model
llm -m claude-opus-4.5 "prompt"       # Claude
llm -m sonar-reasoning-pro "prompt"   # Web search + citations
llm -m gemini-2.5-pro "prompt"        # Gemini
llm -c "follow-up"                    # Continue conversation
```

### Use Templates

```bash
# Summarize any content
cat README.md | llm -t summarize

# Code review
cat src/main.py | llm -t code-review

# Research with citations
llm -t research "SEO best practices 2025"

# Generate tags for a note
cat article.md | llm -t suggest-tags

# Get a second opinion
cat proposal.md | llm -t second-opinion

# Generate commit message
git diff --staged | llm -t commit-msg
```

### Images and Structured Data

```bash
# Analyze images
llm -m gpt-4o -a screenshot.png "What does this show?"

# Extract structured JSON
llm -m gpt-4o --schema "title, author, date, tags[]" < article.md
```

### Search Query History

```bash
llm logs                    # Recent queries
llm logs -n 20              # Last 20
llm logs -q "keyword"       # Search all logs
llm logs -m claude-opus-4.5 # Filter by model
```

---

## Model Selection Guide

| Task | Model | Why |
|------|-------|-----|
| Quick tasks | `gpt-4o-mini` | Fast, cheap |
| Complex reasoning | `claude-opus-4.5` | Best quality |
| Code generation | `claude-sonnet-4.5` | Code-optimized |
| Web research | `sonar-reasoning-pro` | Citations included |
| Deep research | `sonar-deep-research` | Multi-step |
| Image analysis | `gpt-4o` | Vision capability |
| Bulk processing | `gemini-2.5-flash` | Cost-effective |
| Local/private | `llama3.2` | No cloud (requires Ollama) |

---

## Workflow Patterns

### Multi-Model Verification

```bash
QUERY="Review this approach: [details]"
llm -m gpt-4o "$QUERY"
llm -m claude-opus-4.5 "$QUERY"
llm -m gemini-2.5-pro "$QUERY"
```

### Research-Then-Implement

```bash
# Research first
llm -t research "how to implement feature X" > research.md

# Then implement with context
cat research.md | llm -m claude-opus-4.5 "Generate implementation based on this research"
```

### Batch Processing

```bash
# Summarize all markdown files
for f in *.md; do
  echo "## $f"
  cat "$f" | llm -t summarize
  echo ""
done

# Generate tags for untagged notes
for f in *.md; do
  echo "$f: $(cat "$f" | llm -t suggest-tags)"
done
```

### Git Integration

```bash
# Commit message from staged changes
git diff --staged | llm -t commit-msg

# Summarize recent commits
git log --oneline -20 | llm -m gpt-4o-mini "Summarize these commits"

# Review a PR
gh pr diff 123 | llm -t code-review
```

---

## Semantic Search (Optional)

Build a searchable index of project files:

```bash
# Index markdown files (for vaults/docs)
llm embed-multi myproject --model 3-small --store < files.json

# Search semantically
llm similar myproject -c "productivity systems" -n 10

# List collections
llm collections list
```

**Note**: Embedding requires preparing a JSON file of content. See full documentation at https://llm.datasette.io/en/stable/embeddings/

---

## Installation

### Install LLM CLI

```bash
pip install llm
# or
pipx install llm
```

### Install Plugins

```bash
llm install llm-anthropic      # Claude models
llm install llm-gemini         # Gemini models
llm install llm-openrouter     # 300+ models
llm install llm-perplexity     # Web search
llm install llm-ollama         # Local models
```

### Configure API Keys

```bash
llm keys set openai
llm keys set anthropic
llm keys set gemini
llm keys set perplexity
llm keys set openrouter
```

### Install Global Templates

Run once to install templates available everywhere:

```bash
llm --save summarize -m gpt-4o-mini -s "Summarize in 3 concise bullet points. Focus on actionable insights."
llm --save code-review -m claude-opus-4.5 -s "Review code for: bugs, security, performance. Be concise, suggest fixes."
llm --save research -m sonar-reasoning-pro -s "Provide current information with sources. Focus on 2025 best practices."
llm --save suggest-tags -m gpt-4o-mini -s "Suggest 3-5 tags, comma-separated, lowercase hyphenated format."
llm --save explain -m gpt-4o -s "Explain simply. Assume basic technical knowledge."
llm --save commit-msg -m gpt-4o-mini -s "Generate conventional commit message. Format: type(scope): description. Output only the message."
llm --save second-opinion -m gemini-2.5-pro -s "Provide critical second opinion. Identify blind spots and alternatives."
llm --save extract-json -m gpt-4o-mini -s "Extract structured data. Output valid JSON only."
```

### Verify Setup

```bash
llm --version
llm models
llm templates
llm logs status
```

---

## Integration with Claude Code

| Claude Code | LLM CLI |
|-------------|---------|
| Primary assistant | Second opinions |
| File operations | Batch processing |
| Current session | Searchable history |
| Single model | Multi-model queries |

**Workflow**: Use Claude Code for implementation, LLM CLI for research, verification, and audit trails.

---

## Troubleshooting

```bash
# Model not found
llm models | grep -i "name"

# API key missing
llm keys set PROVIDER

# Plugin missing
llm install llm-PLUGIN

# View config paths
llm keys path
llm templates path
llm logs path
```

---

## Quick Reference

```
QUERY:     llm "prompt" | llm -m MODEL "prompt"
TEMPLATE:  llm -t TEMPLATE < file | llm -t TEMPLATE "input"
CONTINUE:  llm -c "follow-up"
IMAGE:     llm -m gpt-4o -a image.png "describe"
SCHEMA:    llm --schema "field1, field2[]" < file
LOGS:      llm logs | llm logs -q "search" | llm logs -m MODEL
```

---

## Resources

- Documentation: https://llm.datasette.io/
- Plugins: https://llm.datasette.io/en/stable/plugins/directory.html
- Templates: https://llm.datasette.io/en/stable/templates.html

---

*Drop this file into any project. Templates are global - they work everywhere once installed.*
