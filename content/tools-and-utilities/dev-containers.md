---
title: "Dev Containers"
description: "Run your development environment inside a container for isolation, reproducibility, and safe autonomous AI agent usage."
tags:
  - engineering
---

# Dev Containers

Dev Containers run your entire development environment inside a Docker container. Your editor connects to the container, and everything (the shell, the filesystem, installed tools, running processes) lives inside it. The host machine is untouched unless you explicitly mount a directory.

For AI-assisted development, this means you can give an agent broad permissions (file writes, bash execution, full autonomy) without risking your host machine, your home directory, your SSH keys, or anything outside the project.

## Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running
- VS Code with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) installed

## Quick start with VS Code

Add a `.devcontainer/devcontainer.json` to your repo:

```json
{
  "name": "Dev Environment",
  "image": "mcr.microsoft.com/devcontainers/base:ubuntu-24.04",
  "features": {
    "ghcr.io/devcontainers/features/node:1": { "version": "20" },
    "ghcr.io/devcontainers/features/python:1": { "version": "3.12" },
    "ghcr.io/devcontainers/features/git:1": {},
    "ghcr.io/anthropics/devcontainer-features/claude-code:1": {}
  },
  "remoteUser": "vscode",
  "postCreateCommand": "echo 'Container ready'"
}
```

Open the repo in VS Code and run **Dev Containers: Reopen in Container** from the command palette (Cmd+Shift+P). VS Code will build the container, install the features, and reconnect. Your terminal now runs inside the container.

The `features` block installs tools without a custom Dockerfile. Anthropic publishes an [official feature](https://github.com/anthropics/devcontainer-features) that installs the `claude` CLI. Add or remove features based on your stack.

## Language-specific images

Microsoft provides pre-built images for common stacks. Use these instead of the `base` image when your project is primarily one language.

| Stack | Image |
| ----- | ----- |
| Node.js | `mcr.microsoft.com/devcontainers/javascript-node:20` |
| Python | `mcr.microsoft.com/devcontainers/python:3.12` |
| Go | `mcr.microsoft.com/devcontainers/go:1.22` |
| Rust | `mcr.microsoft.com/devcontainers/rust:latest` |
| Java | `mcr.microsoft.com/devcontainers/java:21` |

Full list at [mcr.microsoft.com/devcontainers](https://mcr.microsoft.com/en-us/catalog?search=devcontainers).

## Customizing the container

### Installing VS Code extensions automatically

```json
{
  "customizations": {
    "vscode": {
      "extensions": [
        "dbaeumer.vscode-eslint",
        "esbenp.prettier-vscode",
        "ms-python.python"
      ],
      "settings": {
        "editor.formatOnSave": true
      }
    }
  }
}
```

### Forwarding ports

```json
{
  "forwardPorts": [3000, 8000]
}
```

### Running setup commands

```json
{
  "postCreateCommand": "npm install",
  "postStartCommand": "npm run dev"
}
```

`postCreateCommand` runs once when the container is first created. `postStartCommand` runs every time the container starts.

### Using a Dockerfile

For more control, point at a Dockerfile instead of using `image`:

```json
{
  "name": "Custom Dev Environment",
  "build": {
    "dockerfile": "Dockerfile"
  },
  "remoteUser": "vscode"
}
```

Place the `Dockerfile` in `.devcontainer/` alongside the JSON config.

## Without VS Code

You don't need VS Code. The `devcontainer` CLI and plain Docker both work.

### Using the devcontainer CLI

Install it globally:

```bash
npm install -g @devcontainers/cli
```

Then build and start the container from your repo root:

```bash
devcontainer up --workspace-folder .
devcontainer exec --workspace-folder . bash
```

This reads the same `.devcontainer/devcontainer.json` and gives you a shell inside the container.

### Using plain Docker

No DevContainer tooling needed. Mount your repo into a container directly:

```bash
docker run -it --rm \
  -v "$(pwd):/workspace" \
  -w /workspace \
  --cap-drop=ALL \
  --security-opt=no-new-privileges:true \
  mcr.microsoft.com/devcontainers/base:ubuntu-24.04 \
  bash
```

Inside the container, install whatever tools you need (`npm`, `python`, `claude`, etc.) and work from there. Same filesystem isolation, no VS Code or DevContainer machinery.

For a reusable setup, write a `docker-compose.yml`:

```yaml
services:
  dev:
    image: mcr.microsoft.com/devcontainers/base:ubuntu-24.04
    volumes:
      - .:/workspace
    working_dir: /workspace
    cap_drop:
      - ALL
    security_opt:
      - no-new-privileges:true
    stdin_open: true
    tty: true
```

Then: `docker compose run dev bash`

## Security hardening

See [Sandboxed AI Development](../best-practices/sandboxed-ai-development.md) for detailed guidance on locking down the container for autonomous AI agent usage, including permission configuration, capability dropping, network restrictions, and resource limits.

## Further reading

- [VS Code Dev Containers docs](https://code.visualstudio.com/docs/devcontainers/containers)
- [Dev Container JSON reference](https://containers.dev/implementors/json_reference/)
- [Available Dev Container features](https://containers.dev/features)
- [Anthropic devcontainer-features](https://github.com/anthropics/devcontainer-features)
- [Trail of Bits claude-code-devcontainer](https://github.com/trailofbits/claude-code-devcontainer)
