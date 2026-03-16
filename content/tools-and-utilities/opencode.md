---
title: "OpenCode"
description: "An open-source terminal-based AI coding assistant with broad model support and IDE integration."
weight: 9
---

# OpenCode

[OpenCode](https://opencode.ai/) is an open-source AI coding agent that runs in your terminal, IDE, or as a desktop app. It supports 75+ model providers through [Models.dev](https://models.dev/) — including local models via Ollama — and can authenticate with existing accounts like GitHub Copilot or ChatGPT Plus. It doesn't store your code or context, making it a reasonable option for privacy-sensitive work.

OpenCode includes LSP integration (it automatically loads the right language server for whatever you're working in), concurrent sessions on the same project, and session sharing for debugging or handoffs.

## When to Use

- You want an AI coding assistant that isn't locked to a single model provider — OpenCode lets you switch between models or use local ones.
- You're working in a privacy-sensitive environment and need a tool that doesn't store your code or context.
- You want terminal, desktop, and IDE options from the same tool.
- You need to run multiple agent sessions concurrently on the same project.

## Getting Started

Install via the one-liner:

```bash
curl -fsSL https://opencode.ai/install | bash
```

Navigate to your project directory and launch it:

```bash
cd /path/to/your/project
opencode
```

A desktop app beta is also available for macOS, Windows, and Linux at [opencode.ai](https://opencode.ai/).

For detailed usage and configuration, see the [OpenCode documentation](https://opencode.ai/).

## Oh-My-OpenAgent

[Oh-My-OpenAgent](https://github.com/code-yeongyu/oh-my-openagent) (OmO) is a plugin harness that sits on top of OpenCode and orchestrates multiple specialized AI agents to work collaboratively. Rather than a single agent handling everything, OmO delegates to purpose-built specialists:

- **Sisyphus** — the main orchestrator that plans work and delegates to specialists.
- **Hephaestus** — a deep autonomous worker that explores codebases and executes end-to-end tasks independently.
- **Prometheus** — a strategic planner that interviews you, identifies scope, and builds detailed plans before execution begins.

OmO's standout features include hash-anchored edits (which eliminate stale-line errors common in AI code editing), on-demand MCP servers scoped to specific tasks, an `/init-deep` command that auto-generates context files throughout your project, and background agents that execute in parallel. It also includes LSP and AST-grep integration for IDE-precision refactoring across 25 languages.

### Installing Oh-My-OpenAgent

Copy the [installation prompt](https://github.com/code-yeongyu/oh-my-openagent) to your LLM agent, or follow the installation guide in the repository. OmO requires subscriptions to the model providers it orchestrates — see the repo for current provider requirements and costs.
