---
title: "Ollama"
description: "Run open-source large language models locally on your machine."
---

# Ollama

[Ollama](https://ollama.com) lets you download and run open-source large language models locally. It handles model management, quantization, and exposes a local API that other tools (like OpenCode) can connect to.

## Getting Started

Download Ollama from [ollama.com](https://ollama.com), install it, and pull a model:

```bash
ollama pull qwen3.5
ollama run qwen3.5
```

See the [Ollama documentation](https://github.com/ollama/ollama) for the full list of available models and configuration options.

## When to Use It

Ollama is the simplest way to run models locally. Use it when you need offline access, want to keep data off external APIs, or want to experiment with different open-source models. See [Running Models Locally]({{< relref "local-models" >}}) for guidance on choosing models and hardware requirements.
