---
title: "Slate"
description: "A terminal-based AI agent for extended collaborative coding sessions with swarm orchestration."
weight: 10
---

# Slate

[Slate](https://docs.randomlabs.ai/en/getting-started/introduction) is a terminal-based AI agent designed for long-running collaborative sessions. Where most AI coding tools lose coherence as conversations grow — requiring you to start fresh sessions, re-explain context, or manually prune history — Slate is built to maintain context over extended periods without degradation.

It orchestrates multiple models under the hood, selecting the right one for planning, search, or execution, and can run tasks in parallel. This makes it especially effective for work that spans hours rather than minutes: deep debugging sessions, large refactors, architectural exploration, and multi-step investigations where losing context midway means starting over.

## When to Use

- You're doing extended work where other tools would require you to repeatedly re-establish context — long debugging sessions, multi-file refactors, or exploratory analysis across a large codebase.
- You want to stay in a single session for hours without worrying about context window management or conversation resets.
- You need parallel task execution — Slate can work on multiple things simultaneously rather than sequentially.
- You prefer a terminal-based workflow over a GUI for AI-assisted development.

## Getting Started

### Prerequisites

- A Unix-based system (macOS or Linux). Windows users should use WSL.
- Node.js installed on your machine.
- Avoid running Slate inside tmux — there are known display issues.

### Install and run

Install Slate globally via npm:

```bash
npm i -g @randomlabs/slate
```

Navigate to your project directory and launch it:

```bash
cd /path/to/your/project
slate
```

Once running, you can start assigning tasks immediately. For example, ask Slate to review your codebase architecture, debug an issue, or generate documentation.

For commands, shortcuts, and detailed usage, see the [Slate documentation](https://docs.randomlabs.ai/en/using-slate).
