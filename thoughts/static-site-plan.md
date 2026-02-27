# Static Site Generator Evaluation & Plan

## Requirements

- Content driven by Markdown
- Ability to link between content pages
- Tagging / categorization of content
- Build and deploy on GitHub Pages
- Custom domain (e.g., `playbooks.focusconsulting.com`)
- Public site, but also deployable via a containerized solution (Docker)
- Top-level sections: Playbooks, Tools & Utilities, Best Practices

---

## Options Evaluated

### 1. Hugo

**What it is:** Go-based static site generator. Single binary, no runtime dependencies. Fastest build times of any SSG (~1ms per page).

**Markdown:** First-class. All content lives in `content/` as `.md` files with YAML front matter. Uses Goldmark (CommonMark-compliant). Supports shortcodes for extending Markdown beyond standard syntax.

**Linking:** Multiple approaches. The `ref`/`relref` shortcodes provide build-time link validation but use Hugo-specific syntax that won't render in GitHub's Markdown preview. A newer embedded render hook approach allows standard Markdown relative links (`[text](../path/to/file.md)`) that also work on GitHub.

**Tagging:** Excellent. Hugo's taxonomy system is one of its strongest features. Ships with `tags` and `categories` by default. Supports custom taxonomies (e.g., `teams`, `roles`, `skill_levels`). Auto-generates listing pages per tag and a tag index — no plugins or manual work needed.

**GitHub Pages:** Official GitHub Actions workflow. Straightforward setup, deploys in under a minute.

**Pros:**
- Fastest builds (sub-second for hundreds of pages)
- Zero runtime dependencies — single binary install
- Best-in-class taxonomy system with auto-generated pages
- Huge community (86k+ GitHub stars), actively maintained
- Built-in syntax highlighting, TOC, image processing, RSS, sitemaps

**Cons:**
- Go template syntax is unintuitive and has a steep learning curve for customization
- No plugin ecosystem — features are built-in or you write Go templates
- Template debugging is difficult with cryptic error messages
- `_index.md` vs `index.md` distinction trips people up
- `ref`/`relref` shortcodes don't work for section pages

**Best theme for this use case:** Hugo Book (clean, minimal, book-style nav from directory structure) or Docsy (heavier, used by Kubernetes docs).

---

### 2. Jekyll

**What it is:** Ruby-based SSG. The original GitHub Pages generator — the only SSG with native, zero-config GH Pages support.

**Markdown:** First-class via Kramdown. Supports fenced code blocks, tables, footnotes, auto TOC via `{:toc}`, attribute lists. Collections system is good for organizing playbooks/guides.

**Linking:** The `{% link _playbooks/file.md %}` Liquid tag provides build-time validation (build fails on broken links). Standard relative Markdown links also work but without validation.

**Tagging:** Built-in `tags` and `categories` in front matter, but **does not auto-generate tag pages**. You either create them manually, use the `jekyll-archives` plugin (which is NOT on the GH Pages whitelist), or build a single `/tags/` index page with Liquid loops and anchor links. This is a significant gap.

**GitHub Pages:** The simplest deployment of any option — push to `main`, GH Pages builds automatically. No CI/CD config needed. However, GH Pages runs Jekyll 3.x (not 4.x) and restricts plugins to a whitelist. Using GitHub Actions bypasses these limits but loses the zero-config advantage.

**Pros:**
- Zero-config GitHub Pages deployment (push and it builds)
- `just-the-docs` theme is excellent (search, nav hierarchy, dark mode, callouts)
- Mature ecosystem, well-understood, extensive Stack Overflow coverage
- Build-time link validation with `{% link %}`
- Liquid templating is accessible to non-developers

**Cons:**
- **Ruby dependency** — biggest friction point. Requires rbenv/rvm, Bundler, gem management. Native extensions sometimes fail on Apple Silicon.
- GH Pages runs Jekyll 3.x, not 4.x
- Plugin whitelist on GH Pages blocks tag page generation and other useful plugins
- Slowest builds of the options (~5-15s for 200 pages vs sub-second for Hugo)
- No incremental builds in practice
- Jekyll is in maintenance mode — stable but not gaining new features

**Best theme for this use case:** `just-the-docs` — de facto standard for Jekyll documentation sites.

---

### 3. GitBook

**What it is:** Two things that share a name:
- **`gitbook-cli` (open-source):** Dead. Last npm publish was July 2017. Broken on Node 12+. Known security vulnerabilities. Do not use.
- **GitBook.com (SaaS):** Active commercial platform. Cannot deploy to GitHub Pages. Free plan is single-user only; team plan starts at $65/month.

**Tagging:** Neither version supports tags.

**Verdict:** **Not viable.** The open-source tool is dead, and the SaaS product doesn't meet our requirements (no GH Pages, no tags, vendor lock-in, cost).

---

### 4. MkDocs + Material Theme (bonus evaluation)

**What it is:** Python-based SSG purpose-built for documentation. The Material for MkDocs theme (18k+ GitHub stars) is the de facto standard.

**Markdown:** Excellent. Full Markdown plus admonitions, content tabs, code highlighting with line numbers, Mermaid diagrams, math, task lists, footnotes via Python-Markdown extensions.

**Linking:** Standard Markdown relative links. No built-in broken-link detection but available via `mkdocs-linkcheck` plugin.

**Tagging:** **Best-in-class.** Native, built-in tags plugin. Tag hierarchies, tag icons, shadow tags (internal/draft tags hidden from published output), folder-level tags via `.meta.yml` files. Tags render above page titles and are searchable. Configuration is trivial:
```yaml
plugins:
  - tags
```

**GitHub Pages:** First-class. Single command `mkdocs gh-deploy` or a ~10-line GitHub Actions workflow.

**Pros:**
- Best tagging/taxonomy support of any option
- Beautiful default theme with dark mode, excellent search, nav tabs
- Simplest setup: `pip install mkdocs-material`, write `mkdocs.yml`, add Markdown
- 800+ plugins in the MkDocs catalog
- Pure Markdown workflow — no JSX, no Go templates, no Liquid
- Actively maintained with frequent releases

**Cons:**
- Requires Python (not an issue for CI, minor issue for local dev on JS-centric teams)
- Some advanced features (blog, privacy plugin) require paid Insiders tier ($15/month)
- Less customizable than Docusaurus for bespoke components
- No MDX support

---

## Comparison Matrix

| Criteria | Hugo | Jekyll | GitBook | MkDocs Material |
|---|---|---|---|---|
| Markdown support | Excellent | Excellent | N/A (dead) | Excellent |
| Internal linking | Good (with caveats) | Good (with `{% link %}`) | N/A | Good |
| **Tagging** | **Excellent** (auto pages) | **Weak** (no auto pages) | **None** | **Best** (hierarchies, icons, shadow) |
| GH Pages deploy | Actions workflow | Zero-config or Actions | N/A | `gh-deploy` command or Actions |
| Build speed | ~1ms/page | ~50ms/page | N/A | Fast |
| Local dev setup | `brew install hugo` | Ruby + Bundler + gems | N/A | `pip install mkdocs-material` |
| Template learning curve | Steep (Go templates) | Moderate (Liquid) | N/A | Low (Jinja2) |
| Maintenance status | Very active | Maintenance mode | Dead | Very active |
| Best doc theme | Hugo Book / Docsy | just-the-docs | N/A | Material (built-in) |

---

## Recommendation: Hugo

**Hugo is the best fit for this project.** Here's why:

1. **Tagging without compromise.** Hugo's taxonomy system auto-generates tag listing pages and tag index pages from front matter alone — no plugins, no manual page creation, no workarounds. This directly satisfies the tagging requirement.

2. **Zero runtime dependencies.** A single `brew install hugo` and you're running. No Ruby version management, no Python virtualenvs. This minimizes contributor friction.

3. **Build speed.** Sub-second builds mean instant feedback during local development. As the playbook grows, this advantage compounds.

4. **GitHub Pages deployment is solved.** Official, well-tested GitHub Actions workflow. Copy-paste setup.

5. **Content portability.** Plain Markdown files with YAML front matter. Content is readable on GitHub directly and portable to any other SSG if we ever migrate.

6. **Active development.** Frequent releases, 86k+ stars, large community. Not going anywhere.

**Why not the others:**
- **Jekyll:** Tag page generation requires workarounds or plugins blocked by GH Pages. Ruby dependency is real friction. In maintenance mode.
- **GitBook:** Dead (CLI) or wrong model (SaaS).
- **MkDocs Material:** A very close second. Its tagging is actually superior to Hugo's. The reason Hugo edges it out is the zero-dependency install (single Go binary vs. Python + pip) and the broader theme/community ecosystem. MkDocs Material would also be a great choice — if the team is more comfortable with Python, it's worth reconsidering.

---

## Implementation Plan

### Phase 1: Project Scaffolding

1. Install Hugo: `brew install hugo`
2. Initialize site: `hugo new site . --force` (in existing repo)
3. Add Hugo Book theme as a git submodule
4. Configure `hugo.yaml` with:
   - Site metadata (title, baseURL)
   - Taxonomies: `tags`, `categories`
   - Markdown render hook for standard relative links
   - Menu and navigation structure

### Phase 2: Content Structure

```
content/
  _index.md                          # Homepage / landing
  playbooks/
    _index.md                        # Playbooks section index
    ai-engineering/
      _index.md
      prompt-engineering.md
      model-evaluation.md
    delivery/
      _index.md
      project-kickoff.md
      stakeholder-management.md
  tools-and-utilities/
    _index.md                        # Tools & Utilities section index
    claude-code.md
    cursor.md
    github-copilot.md
  best-practices/
    _index.md                        # Best Practices section index
    code-review.md
    documentation.md
    testing-strategy.md
```

Each file gets front matter:
```yaml
---
title: "Prompt Engineering"
tags: ["ai", "llm", "engineering"]
categories: ["AI Engineering"]
weight: 10
---
```

### Phase 3: GitHub Pages Deployment

1. Add `.github/workflows/hugo.yaml` with the official Hugo deploy workflow
2. Configure repo Settings > Pages > Source to "GitHub Actions"
3. Push to `main` → site auto-deploys

### Phase 4: Custom Domain

1. Configure a custom domain in GitHub Pages settings (e.g., `playbooks.focusconsulting.com`)
2. Add a `CNAME` file to the `static/` directory so Hugo includes it in the build output
3. Set `baseURL` in `hugo.yaml` to the custom domain
4. Configure DNS: add a CNAME record pointing the subdomain to `focusconsulting.github.io`
5. Enable "Enforce HTTPS" in GitHub Pages settings once DNS propagates

### Phase 5: Containerized Deployment

Add a `Dockerfile` for building and serving the site independently of GitHub Pages:

```dockerfile
# Build stage
FROM hugomods/hugo:latest AS build
WORKDIR /src
COPY . .
RUN hugo --minify

# Serve stage
FROM nginx:alpine
COPY --from=build /src/public /usr/share/nginx/html
EXPOSE 80
```

Add a `docker-compose.yml` for local/self-hosted use:

```yaml
services:
  site:
    build: .
    ports:
      - "8080:80"
```

This gives two deployment paths:
- **GitHub Pages** (primary): push to `main`, auto-deploys via Actions
- **Container** (alternative): `docker compose up` for local preview or deployment to any container host (ECS, Cloud Run, k8s, etc.)

### Phase 6: Content Authoring Guide

- Add `CONTRIBUTING.md` with instructions for:
  - Creating new content (front matter template, file naming)
  - Using tags consistently
  - Linking between pages
  - Local preview with `hugo server`
  - Container-based preview with `docker compose up`

---

## Decisions (Resolved)

- **Custom domain:** Yes — will configure (e.g., `playbooks.focusconsulting.com`)
- **Access control:** Public site. No GH Enterprise needed.
- **Containerized deployment:** Required. Dockerfile included in Phase 5 for alternative deployment to any container host.
- **Content sections:** Playbooks, Tools & Utilities, Best Practices
- **SSG choice confirmed:** Hugo. Superior tagging not needed — Hugo's built-in taxonomy is sufficient.
