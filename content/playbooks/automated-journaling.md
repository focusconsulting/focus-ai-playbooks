---
title: "Automated Journaling"
description: "A lightweight, always-on practice for logging what you're working on using AI and tools like Obsidian."
tags:
  - thinking + reflection
related_playbooks:
  - rubber-duck-with-memory
  - knowledge-digest
---

# Automated Journaling

Most work logs are either too formal to maintain or too informal to be useful. You either try to keep a project tracker that becomes a chore, or you jot things down somewhere and never look at it again.

This playbook is about a lighter practice: keeping an ongoing record of what you're actually doing (decisions made, problems encountered, things learned, context you'll need later) without it feeling like a second job. The goal is to reduce the friction of capture enough that it actually happens, and to use AI to help you structure and reflect on what you've captured.

The tools here are intentionally flexible. The pattern works with Obsidian + MCP, a voice-to-text note, a running chat thread, or any other setup where you can capture quickly and retrieve later.

## When to Use

- You're in a phase of work where context is accumulating fast and you'll need to reconstruct your reasoning later.
- You keep losing the thread between sessions. Each time you pick up a project, you spend ten minutes re-orienting.
- You're working on something complex and want a low-effort way to track the decisions and dead ends.
- You want to be able to write an accurate retrospective, summary, or handoff document without relying on memory.
- You notice you're having the same realization for the third time and want to stop losing it.

## The Play

### Pick one capture point and stick to it

The most common failure mode is spreading captures across too many places. One place where raw notes go. It doesn't have to be fancy — a daily file in Obsidian, a running note in your tool of choice, a dedicated AI session. What matters is that it's always the same place and low enough friction that you'll actually use it.

The note doesn't need to be clean. "Got stuck on the auth flow, realized the token refresh isn't handling 401s from third-party APIs, punted to tomorrow" is a perfect journal entry. Don't edit before you capture.

For a setup that reduces friction even further, see [Obsidian + MCP](../tools-and-utilities/obsidian-mcp.md). When the AI can read and write to your vault directly, capture and retrieval both get easier.

### Log at natural transition points

You don't need to set a timer. Log at the moments that already exist: when you finish a task and start a new one, before you close your laptop, when you shift contexts between projects, or when you just figured something out and want to hold onto it.

If you're using a voice tool, say it out loud on the walk between meetings. If you're in a terminal, a quick note before you close a session. The habit is what matters, not the format.

Some things worth capturing:

- What you decided and why (even rough reasoning)
- What you were stuck on and what unblocked you
- Things you learned that you don't want to lose
- What you were in the middle of when you stopped
- Questions you want to come back to

### Use AI to structure and reflect

Raw logs are useful for retrieval but not much else. Periodically — weekly is a natural cadence — paste your recent logs into an AI session and ask it to help you make sense of them.

Useful prompts:

- "Summarize what I've been working on this week and what's still open"
- "What patterns do you see across these notes? What am I spending most of my time on?"
- "I need to write a weekly update for my manager — pull out the relevant highlights"
- "What decisions did I make this week and what was my reasoning?"

The AI is good at extracting structure from unstructured text. What you're doing is turning informal capture into a usable artifact.

### Close the loop on open threads

A journal isn't just for output. It surfaces what's unresolved. When you synthesize your recent notes, look for questions you asked and never answered, decisions you deferred, things you said you'd come back to. These are the things that fall through the cracks in a busy week.

Decide what to do with each one: follow up now, schedule it, or explicitly close it as "not going to pursue this."

## Related Playbooks

- [Rubber Duck with Memory](rubber-duck-with-memory.md) — The journal captures what happened; the rubber duck session is where you think through what it means.
- [Knowledge Digest](knowledge-digest.md) — If you're consuming external content (articles, talks, reports) and want to fold it into your notes, the knowledge digest playbook handles that intake more systematically.

## Prompts

### Weekly synthesis

```text
Here are my work notes from this week. Help me:
1. Summarize what I worked on and what I accomplished
2. Identify what's still open or unresolved
3. Surface any patterns in where I'm spending time or getting stuck
4. Pull out 2-3 highlights I could use in a weekly update

Notes:
[paste notes]
```

### Context recovery

Use this when you're picking up a project after time away.

```text
Here are my notes from the last time I was working on [project]. Help me reconstruct
where I left off: what was I in the middle of, what decisions had I made, and what
were the open questions?

Notes:
[paste notes]
```
