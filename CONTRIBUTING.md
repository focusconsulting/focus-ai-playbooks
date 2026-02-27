# Contributing

## Prerequisites

- [Hugo](https://gohugo.io/installation/) (extended edition)
- Git

Install Hugo on macOS:

```bash
brew install hugo
```

## Local Development

Clone the repo with submodules:

```bash
git clone --recurse-submodules git@github.com:focusconsulting/focus-ai-playbooks.git
cd focus-ai-playbooks
```

Start the dev server:

```bash
hugo server
```

The site will be available at `http://localhost:1313/`. Changes to content files reload automatically.

## Docker Preview

If you prefer not to install Hugo locally:

```bash
docker compose up
```

The site will be available at `http://localhost:8080/`.

## Creating New Content

### File Location

Content goes in one of three top-level sections:

| Section | Directory | Purpose |
|---|---|---|
| Playbooks | `content/playbooks/` | Step-by-step workflow guides |
| Tools & Utilities | `content/tools-and-utilities/` | Tool reference guides |
| Best Practices | `content/best-practices/` | Standards and conventions |

### Front Matter Template

Every Markdown file needs YAML front matter at the top:

```yaml
---
title: "Your Page Title"
weight: 1
tags: ["tag1", "tag2"]
categories: ["Category Name"]
---
```

- `title` — displayed in navigation and page header
- `weight` — controls sort order in the sidebar (lower = higher)
- `tags` — used for cross-cutting categorization (see existing tags before creating new ones)
- `categories` — the broad category this content belongs to

### Creating a New Page

```bash
# Create a new playbook
hugo new content playbooks/my-new-playbook.md

# Create a new sub-section (directory with its own index)
mkdir -p content/playbooks/my-section
cat > content/playbooks/my-section/_index.md << 'EOF'
---
title: "My Section"
weight: 1
bookCollapseSection: true
---

# My Section

Description of this section.
EOF
```

### Linking Between Pages

Use standard Markdown relative links:

```markdown
See the [Prompt Engineering guide](../ai-engineering/prompt-engineering.md) for details.
```

Or absolute paths from the content root:

```markdown
Check the [Code Review best practices](/best-practices/code-review/).
```

### Tags

Use lowercase, hyphenated tags. Check existing tags at `/tags/` before creating new ones to avoid duplicates.

Common tags: `ai`, `llm`, `tools`, `engineering`, `delivery`, `quality`

## Deployment

Pushing to `main` automatically triggers a GitHub Actions build and deploys to GitHub Pages. No manual deployment steps needed.
