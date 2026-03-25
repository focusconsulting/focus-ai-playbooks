---
title: "Sandboxed AI Development"
description: "Run AI coding agents with full autonomy inside containers so broad permissions don't risk your host machine."
tags:
  - engineering
weight: 4
---

# Sandboxed AI Development

AI coding agents are most productive when they can read, write, and execute without stopping to ask permission on every action. But unrestricted access to your machine is a bad idea. The agent can read your SSH keys, AWS credentials, browser history, and every other project on your disk. One bad tool call and you're dealing with consequences that are hard to reverse.

The solution is containers. Run the agent inside a [Dev Container](../tools-and-utilities/dev-containers.md) or a plain Docker container and give it full permissions *inside the container*. The container boundary is the safety layer, not the AI's permission system. The agent can do whatever it wants to the project files, run any command, install any package, and none of it touches your host.

## The permission model

AI coding tools like Claude Code have a permission system that prompts before risky actions (file writes, bash execution, etc.). For interactive work this is fine. For autonomous work, where the agent runs unattended for extended periods, the prompts become blockers.

Claude Code's `--dangerously-skip-permissions` flag (or `bypassPermissions` mode in settings) removes all prompts. The name is deliberately alarming because running this on your host machine *is* dangerous. Inside a container, it's the intended workflow. The container is the sandbox; the permission bypass lets the agent work without interruption.

To enable it, either:

**CLI flag:**
```bash
claude --dangerously-skip-permissions
```

**Or in `.claude/settings.local.json` inside the container:**
```json
{
  "permissions": {
    "defaultMode": "bypassPermissions"
  }
}
```

Use the settings file approach if you want the container to always start in bypass mode without remembering to pass the flag.

## What the container isolates

When running inside a container, the AI agent can only access:

- **The project directory**, mounted from your host. This is the one thing the agent *should* be able to modify.
- **Container-local files**: anything installed or created inside the container (node_modules, virtual environments, etc.).

It cannot access:

- Your home directory (`~/.ssh`, `~/.aws`, `~/.config`, `~/.zshrc`)
- Other projects on your machine
- Host system files
- Your browser, email, or any other running applications
- The Docker socket (unless you mount it, which you should never do)

If the agent does something destructive, the damage is limited to the mounted project directory. And since you're working in git, `git checkout .` undoes the filesystem damage.

## Setting up a sandboxed container

### Minimal devcontainer.json

This is a starting point that works for most projects:

```json
{
  "name": "Sandboxed AI Dev",
  "image": "mcr.microsoft.com/devcontainers/base:ubuntu-24.04",
  "features": {
    "ghcr.io/anthropics/devcontainer-features/claude-code:1": {}
  },
  "runArgs": [
    "--cap-drop=ALL",
    "--security-opt=no-new-privileges:true"
  ],
  "remoteUser": "vscode",
  "postCreateCommand": "echo 'Container ready — agent permissions are sandboxed to this container'"
}
```

Add language-specific features (node, python, etc.) based on your project. See [Dev Containers](../tools-and-utilities/dev-containers.md) for details.

### What the runArgs do

- **`--cap-drop=ALL`** removes all Linux capabilities from the container. The agent can't mount filesystems, modify network interfaces, or use any privileged kernel features. Most coding work needs no capabilities.
- **`--security-opt=no-new-privileges:true`** prevents privilege escalation via setuid binaries. Even if the agent finds a setuid binary in the container, it can't gain root.

### Adding resource limits

Prevent a runaway process from starving your host:

```json
{
  "runArgs": [
    "--cap-drop=ALL",
    "--security-opt=no-new-privileges:true",
    "--memory=4g",
    "--cpus=2"
  ]
}
```

Adjust the values based on your machine. 4GB and 2 CPUs is a reasonable default for most development work.

## Network restrictions

By default, the container has full network access. This is usually fine: the agent needs to install packages (npm, pip), interact with git remotes, and call the LLM API. If you want to restrict outbound access to known-good destinations, set up an iptables firewall inside the container.

This requires adding back two capabilities:

```json
{
  "runArgs": [
    "--cap-drop=ALL",
    "--cap-add=NET_ADMIN",
    "--cap-add=NET_RAW",
    "--security-opt=no-new-privileges:true"
  ]
}
```

Then add a `postCreateCommand` or entrypoint script that configures the firewall:

```bash
#!/bin/bash
# Allow loopback
iptables -A OUTPUT -o lo -j ACCEPT

# Allow DNS
iptables -A OUTPUT -p udp --dport 53 -j ACCEPT
iptables -A OUTPUT -p tcp --dport 53 -j ACCEPT

# Allow established connections
iptables -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allowlist: LLM API, package registries, git hosting
iptables -A OUTPUT -p tcp --dport 443 -d api.anthropic.com -j ACCEPT
iptables -A OUTPUT -p tcp --dport 443 -d registry.npmjs.org -j ACCEPT
iptables -A OUTPUT -p tcp --dport 443 -d pypi.org -j ACCEPT
iptables -A OUTPUT -p tcp --dport 443 -d files.pythonhosted.org -j ACCEPT
iptables -A OUTPUT -p tcp --dport 443 -d github.com -j ACCEPT

# Drop everything else
iptables -A OUTPUT -j DROP
```

For most teams this is overkill. Do it if you're running agents against sensitive codebases where data exfiltration is a concern.

Trail of Bits publishes a [reference DevContainer](https://github.com/trailofbits/claude-code-devcontainer) that implements this pattern with a production-tested iptables setup.

## What not to mount

The container should only see the project directory. Never mount:

- **`~/.ssh`**: the agent doesn't need your SSH keys. Use HTTPS for git, or configure a deploy key inside the container.
- **`~/.aws`, `~/.config/gcloud`**: cloud credentials give the agent access to your infrastructure.
- **`/var/run/docker.sock`**: the Docker socket gives the container root-equivalent access to the host. An agent with Docker socket access can spin up a privileged container and escape the sandbox entirely.
- **Your entire home directory**: too broad. Mount only the specific project.

If the agent needs credentials (API keys, database passwords), pass them as environment variables via a `.env` file instead of mounting credential files from the host.

## Without VS Code

The sandboxing pattern works with any container runtime. Plain Docker:

```bash
docker run -it --rm \
  -v "$(pwd):/workspace" \
  -w /workspace \
  --cap-drop=ALL \
  --security-opt=no-new-privileges:true \
  --memory=4g \
  --cpus=2 \
  mcr.microsoft.com/devcontainers/base:ubuntu-24.04 \
  bash
```

Inside the container, install Claude Code (`npm install -g @anthropic-ai/claude-code`) and run it with `--dangerously-skip-permissions`. The isolation is identical to the DevContainer approach.

For the `devcontainer` CLI without VS Code:

```bash
npm install -g @devcontainers/cli
devcontainer up --workspace-folder .
devcontainer exec --workspace-folder . claude --dangerously-skip-permissions
```

## Limitations

Containers share the host kernel. A kernel-level vulnerability could theoretically allow a container escape. For development work this risk is negligible. If you're running agents against untrusted code from unknown sources, look at Docker Desktop's Enhanced Container Isolation mode or a microVM approach for a hypervisor-level boundary.

Container isolation protects the host, not the project files. The agent can still delete files, overwrite code, or introduce bugs inside the mounted project directory. Git is your safety net. Commit before running autonomous agents, and review the diff before accepting changes.
