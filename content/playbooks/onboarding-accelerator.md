---
title: "Onboarding Accelerator"
description: "Use AI to rapidly build a mental model of a new domain, team, or role by processing the documents and decisions that already exist."
tags:
  - intake + learning
related_playbooks:
  - research-assistant
  - rubber-duck-with-memory
  - active-learning-partner
  - knowledge-digest
---

## Overview

When someone joins an existing team, there's usually a mountain of context that already exists somewhere. Product briefs in Google Drive. Architecture decisions in Confluence. Strategy decks from last quarter. Roadmap documents. Meeting notes. Slack threads that settled important debates. The problem isn't that the knowledge doesn't exist — it's that nobody has time to walk the new person through all of it, and reading everything unguided takes weeks.

This playbook uses AI to compress that ramp-up. Instead of reading fifty documents and trying to piece together how they relate, you feed them to the AI and have a structured conversation about what's in them. The AI becomes a guide through the existing body of knowledge, helping you build a mental model of the team's context, decisions, and current state.

Not a replacement for talking to people. There's context that lives in heads and nowhere else. But a huge amount of ramp-up is just processing existing documents, and that's time you can get back.

## When to Use

- You're stepping into a role where someone else has been doing the work and there's a body of documents, decisions, and history to absorb.
- You're joining a team mid-stream on a project and need to understand what's been decided, what's in flight, and what's still open.
- You're a manager or lead taking over a team and need to understand the product, the roadmap, and the key relationships.
- You're moving into a new domain within the company and the institutional knowledge is scattered across tools and locations.

## The Play

### Map out where the knowledge lives

Before you start feeding documents to the AI, figure out what exists and where. Ask the outgoing person or your new teammates: where do things live?

Google Drive might have product briefs, strategy decks, research findings, and one-pagers. Confluence might have architecture decisions, process documentation, and project histories. There might be important Slack threads, recorded presentations, or shared spreadsheets.

You don't need to find everything. You need the high-signal documents — the ones that capture decisions, strategy, and context rather than day-to-day noise. A product strategy doc from three months ago is more useful than last Tuesday's standup notes.

Ask the outgoing person: "If I could only read ten documents to understand this team, which ten?" That question alone is worth asking even if you end up reading more.

### Set up a project with the core documents

Create a [Claude Project](../tooling/claude-projects.md) and load it with the key documents you've identified. If the content lives in [Google Drive](../tooling/claude-google-drive.md), you can connect it directly rather than downloading and uploading.

For content in Confluence or other tools, you'll need to export or copy it in. Markdown or plain text works fine — the AI cares about content, not layout.

Organize what you load roughly by type: strategy and vision, product briefs and requirements, architecture and technical decisions, process docs. Not strictly necessary, but it helps when you're later asking questions about specific areas.

### Start with the big picture

Don't dive into details. Ask the AI for a high-level summary of the team's current state based on everything you've loaded. What is this team working on? What are the major products or workstreams? What are the priorities?

This first pass will be rough, but it gives you a map. You'll see the shape of things — what the team considers important, how they talk about their work, where the emphasis sits. It also surfaces gaps right away. If the summary doesn't mention something you expected, either the documents don't cover it or you haven't loaded the right ones.

### Go deeper by area

Once you have the big picture, drill into specifics. The questions depend on your role, but some patterns tend to be useful:

For product context — the current roadmap, what shipped recently, what's in progress, what decisions are still open. What were the key tradeoffs? What alternatives got considered and rejected?

For team context — how the team is structured, key relationships with other teams, where the dependencies are. How does work get prioritized? How are decisions made? Who are the stakeholders?

For historical context — the biggest decisions in the last six months and what drove them. What changed direction and why. This is often where the most useful stuff hides, because the reasoning behind pivots rarely makes it into current docs.

### Build a running onboarding document

As you work through these questions, have the AI maintain a running document that captures your emerging understanding.

First, it forces the learning into a concrete artifact. Writing things down — even if the AI is doing the writing — makes the understanding stick better than just reading summaries.

Second, it gives you something to validate. Take the document to the outgoing person or your new team and say "here's my understanding so far — what am I getting wrong?" Far more productive than showing up cold and asking them to explain everything from scratch. It also draws out the things that aren't in any document, the unwritten context that only surfaces in conversation.

### Use it as a launchpad, not a crutch

The onboarding document and the Claude Project get you up to speed faster. They're not a permanent substitute for actually knowing your domain. Once you've built your initial mental model, start doing the work — sit in meetings, make decisions, write documents. The understanding that sticks comes from doing, not reading.

The project stays useful as a reference when you need to remember why something was decided or what the original reasoning was. But the goal is to get to the point where you don't need it for most things.

## Related Playbooks

- [Research Assistant](research-assistant.md) — If onboarding requires targeted research on specific topics (an industry, a competitor, a technology), use this for those focused investigations.
- [Rubber Duck with Memory](rubber-duck-with-memory.md) — As you form opinions about what should change or what needs attention, talk it through. The onboarding document gives you context; the rubber duck session helps you figure out what to do with it.
- [Active Learning Partner](active-learning-partner.md) — If there are domains you need to learn deeply, not just understand the team's context around, use this to build that knowledge through dialogue.
- [Knowledge Digest](knowledge-digest.md) — Once you're onboarded, transition to a digest workflow to keep processing new information as it comes in rather than doing another big ramp-up later.

## Examples

*Examples coming soon.*