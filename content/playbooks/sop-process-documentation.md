---
title: "SOP / Process Documentation"
description: "Walk through a process conversationally and let the AI turn it into structured documentation."
tags:
  - process + operations
related_playbooks:
  - rubber-duck-with-memory
  - ai-driven-writing
  - decision-documentation
---

# SOP / Process Documentation

Every team has tribal knowledge: the stuff that lives in one person's head and gets passed along through hallway conversations, pairing sessions, and "just ask Sarah." It works until Sarah is on vacation, or leaves, or the team grows faster than the oral tradition can keep up. Then things break, get done inconsistently, or take three times as long because someone is reverse-engineering a process from scratch.

This playbook uses AI to extract that tribal knowledge into structured documentation. You describe the process conversationally (how you actually do it, what to watch out for, where things can go wrong) and the AI structures it into documentation you can share. The output is the point. Your knowledge gets out of your head and into a format that lives without you.

This is also one of the best uses of [voice input](../tools-and-utilities/voice-input.md) with AI. Instead of typing out a process you've done a hundred times, just talk through it. Speak the way you'd explain it to a colleague sitting next to you. Most people can describe a process out loud far faster and more naturally than they can write it down, and the AI handles the translation from spoken explanation to structured document.

## When to Use

- A process exists only in your head and needs to be written down for someone else.
- You're onboarding someone and realizing how much implicit knowledge you have that isn't documented.
- A recurring task keeps getting done inconsistently across the team.
- You're about to hand something off and need to document it first.
- You've just learned how to do something new and want to capture it while it's fresh.

## The Play

### Talk through it before you write anything

Don't open a doc and start typing. Describe the process out loud to the AI, literally out loud, using [voice input](../tools-and-utilities/voice-input.md) if you can. Talk as if you're explaining it to a smart colleague who's never done it. Include the details you'd mention in a real handoff: what tools you use, what order things happen in, what you check before moving to the next step, and where things break if you get it wrong. Speaking it produces better raw material than typing. You're more natural, less self-editing, and faster.

If you have trouble getting started, try the walk-through prompt: "I'm going to describe a process I do regularly. Ask me clarifying questions as I go to help me surface the things I might take for granted."

This is where the value is. The AI will ask about things you skipped over because they felt obvious. Those are usually the things that trip people up when they try to follow the documentation.

### Let the AI draft the structure

Once you've talked through it, ask the AI to draft a structured SOP from the conversation. A good SOP typically includes:

- **Purpose** — what this process accomplishes and when it applies
- **Prerequisites** — what needs to be in place before you start (access, tools, prior steps)
- **Steps** — numbered, in order, specific enough that someone could follow them without asking you
- **Decision points** — where the path forks based on what you find
- **Common issues** — what goes wrong and what to do when it does
- **Outputs / Verification** — how you know you did it right
- **Owner** — who maintains this document and who to ask with questions
- **Last updated** — when the document was last verified as accurate

### Read it as if you've never done the task

Read the draft as if you're the person who needs to follow it, not the person who wrote it. Where does it assume knowledge? Where would you stop and ask a question? Where does a step skip over something you actually do?

Mark up the gaps and feed them back. "Step 4 assumes you already have X configured — add a step before it" or "There's a whole decision point missing between step 6 and step 7." Work through a round or two of this until the document holds up on its own.

### Test it with someone who doesn't know the process

If possible, hand it to someone who hasn't done the task before and watch them work through it. The places they get stuck are the places the documentation is incomplete. This is faster feedback than trying to anticipate everything yourself.

### Keep it alive

Documentation that isn't updated becomes a liability. When the process changes, update the doc. Add a "last verified" date at the top so readers know how current it is.

If your team has a standard place for this kind of documentation, move it there. An SOP in a Google Doc that nobody can find isn't useful.

## Related Playbooks

- [Rubber Duck with Memory](rubber-duck-with-memory.md) — If the process is complex or you're struggling to articulate it, talk through it in a rubber duck session first to get the implicit knowledge out before trying to document it.
- [AI Driven Writing](ai-driven-writing.md) — If the process documentation is meant for a broader audience (a published guide, a training document), use the writing pipeline to polish the output.
- [Decision Documentation](decision-documentation.md) — If the process involves a lot of judgment calls, pair it with decision documentation to capture the reasoning behind the choices, not just the steps.

## Prompts

### Walk-through starter

Use this to get the conversation going without worrying about structure.

```text
I'm going to describe a process I do regularly. As I explain it, ask me clarifying
questions to help me surface things I might take for granted or skip over. Don't try
to structure it yet — just help me get it all out.

Here's the process: [describe it]
```

### SOP draft request

Use this after talking through the process to get a first structured draft.

```text
Based on what I've described, draft a structured SOP that someone unfamiliar with
this process could follow without asking me questions. Include:

- Purpose
- Prerequisites (tools, access, prior steps)
- Step-by-step instructions, numbered and in order
- Decision points where the path branches
- Common issues and how to handle them
- How to verify the process completed correctly

Flag anywhere you're uncertain about the details or where my description had gaps.
```
