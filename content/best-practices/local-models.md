---
title: "[UNDER CONSTRUCTION] Running Models Locally"
description: "Best practices for running local LLMs and using them with coding tools like OpenCode."
weight: 1
---

# Running Models Locally

Tools like Ollama and LM Studio let you run open-source language models on your own machine. Combined with coding assistants like OpenCode, local models give you a fast, private, offline-capable option for certain development tasks.

## When Local Models Make Sense

Local models are a good fit when:

- **Privacy is non-negotiable.** Nothing leaves your machine. If you're working with sensitive code or data that shouldn't touch an external API, local is the safe default.
- **You need offline access.** Traveling, on a flight, unreliable internet. Local models don't need a connection.
- **You want fast iteration on small tasks.** Quick completions, boilerplate generation, simple refactors. On good hardware, a local model responds faster than a round-trip to an API.
- **You're experimenting with different models.** Try different models and compare outputs without managing API keys or billing.

Local models are a poor fit when:

- **You need the best possible output quality.** Cloud models are far more capable, especially for complex reasoning, large codebases, or nuanced tasks.
- **Context window matters.** Local models have smaller effective context windows, and quality degrades faster as you approach the limit.
- **Your hardware can't keep up.** A model that doesn't fit in your machine's memory will be painfully slow.

## Using Local Models with OpenCode

OpenCode supports connecting to local model providers out of the box. Point it at a local Ollama or LM Studio instance and it will use that model for code completions and chat.

Refer to the [OpenCode]({{< relref "opencode" >}}) tool page for setup details as they become available.

## Choosing the Right Model

Not all local models are equal. The right choice depends on your hardware and use case.

**For coding tasks**, look for models trained or fine-tuned on code. Models in the 7B–14B parameter range balance quality and speed well on most modern laptops. Larger models (30B+) produce better output but need significant RAM and a capable GPU.

**Check your hardware first.** Rough rule of thumb: you need about 1 GB of RAM per billion parameters for a quantized model. A 13B model needs ~13 GB of free memory. On a MacBook with Apple Silicon, unified memory helps, but you're still sharing it with everything else on the system.

**Start small, then scale up.** Try a smaller model first. If the output isn't good enough, move up a size. A model that's too large for your hardware will give you worse results than a smaller model that fits comfortably.

### Recommended Models:

- qwen3.5 (9 billion parameters): MoE model that fits neatly in about 10GB of VRAM

## Tips

- **Keep models updated.** Model releases move fast. Check for new versions periodically. A newer, smaller model often outperforms an older, larger one.
- **Use quantized models.** Quantized versions (Q4, Q5, Q8) use less memory with minimal quality loss. Q4 or Q5 is fine for most coding tasks.
- **Don't mix up your workflows.** Know when you're using a local model vs. a cloud model. The quality difference is real, and it's easy to assume you're getting cloud-level output from a 7B model. Use local for speed and privacy; switch to cloud for quality-critical work.
- **Set expectations with your team.** If you're sharing prompts or playbooks that assume a cloud model, note where a local model won't produce comparable results.
