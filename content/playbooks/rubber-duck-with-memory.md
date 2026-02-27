---
title: "Rubber Duck with Memory"
description: "Think out loud with an AI that asks good questions and writes everything down."
tags:
  - thinking + reflection
related_playbooks:
  - ai-driven-writing
  - decision-documentation
  - automated-journaling
  - sop-process-documentation
  - research-assistant
  - knowledge-digest
---

## Overview

In software engineering, rubber duck debugging means explaining your problem out loud to a rubber duck on your desk. The act of articulating the problem often reveals the solution. The duck doesn't need to say anything — the value is in forcing yourself to think clearly enough to explain.

This playbook takes that idea and makes it better in two ways. First, the AI isn't silent. It asks clarifying questions, pokes at assumptions, and pushes you to be more specific. Second — and this is the part that actually matters — everything gets written down. The conversation produces a document that captures your thinking as it develops.

Most people have had the experience of talking through a problem, reaching a breakthrough, and then losing the thread a week later because nothing was recorded. Or worse, remembering that you solved something but not how. This playbook treats the document as a first-class output of the thinking process, not an afterthought.

## When to Use

- You're stuck on a problem and can't see it clearly. You need to talk it out, not read more.
- You have a half-formed idea that needs pressure testing before you commit to it.
- You need to arrive at a thesis, position, or recommendation but you're not there yet.
- You're making a decision you'll need to explain or defend later, and you want the reasoning on paper.
- You keep circling the same problem in your head and need to get it out of there to make progress.

## The Play

### Set up the session with context

Start by telling the AI what you're thinking about and where you're stuck. Be honest about what you don't know. Something like "I'm trying to figure out how to structure the rollout of X, and I keep going back and forth between two approaches" gives the AI something real to work with.

If there's relevant background — prior decisions, constraints, stakeholder concerns, earlier attempts — provide it. If you need to gather context before the session, a [research assistant](research-assistant.md) session can help you pull together what you need. If you've been building a [knowledge digest](knowledge-digest.md), this is where that investment pays off: feed in the relevant notes so the AI has real context, not just your recollection of it.

Tell the AI explicitly that you want it to ask questions and challenge your reasoning, not jump to solutions. Left to its defaults, AI will try to be helpful by giving you answers. That's not what you want here.

### Think out loud

Talk through your problem. Don't worry about being organized. Say what you're considering, what worries you, what you've tried, what the tradeoffs seem to be. Let it be messy.

The AI's job is to listen and ask the kind of questions that move your thinking forward. "What happens if that assumption is wrong?" or "You mentioned X as a constraint but haven't said why — is it actually fixed?" The questions a good colleague would ask, except you can do this at 11pm on a Tuesday without bothering anyone.

Follow the thread wherever it goes. Some of the best rubber duck sessions start with one problem and end up clarifying something adjacent that turns out to matter more.

### Write it down as you go

This is what separates a useful session from a chat that vanishes. As your thinking takes shape, periodically ask the AI to capture the current state of your reasoning in a document — not a transcript, but a distilled summary: what you've concluded, what's still open, what the key tensions are.

Some people do this at natural breaks in the conversation. Others ask the AI to maintain a running document that gets updated as the discussion goes. Either works. What matters is that the output isn't the conversation history — it's a clean artifact that future-you can pick up without re-reading the whole thread.

If you're using a tool that supports persistent documents (like Claude's artifacts or a connected notes app), keep the document open alongside the conversation so you can watch your thinking accumulate.

### Come back to it

You don't have to resolve everything in one sitting. Close the session, go do something else, come back when you've had time to sit with it.

When you return, start by reviewing the document, not the conversation. The document is the state of your thinking. Pick up from there. "Last time I landed on X but I've been mulling it over and I'm not sure about Y" is a much better starting point than scrolling through a long chat trying to remember where you left off.

Over time, the document becomes a record of how your thinking evolved — useful well beyond the immediate problem. When someone asks "why did you decide to do it this way?" you have something better than "it felt right."

### Distill into next steps

A document that captures your reasoning is valuable. One that ends with concrete next steps is more so. Once your thinking has converged enough, ask the AI to help you turn the conclusions into actions. What specifically are you going to do? In what order? What depends on what?

This doesn't need to be a full project plan. It might be three bullet points. But the session should end with "here's what I'm doing about it" rather than just "I understand the problem better now." If the thinking isn't far enough along for next steps, name that in the document so you know where to pick up.

If you're keeping an [automated journal](automated-journaling.md), the next steps are worth capturing there too — it connects the thinking session to the work that follows.

### Know when to stop talking and start doing

Rubber ducking is generative but it can become a way to avoid committing. If you've gone back and forth across multiple sessions and the document keeps changing rather than converging, that's a signal. You probably have enough clarity to act and are holding out for certainty that isn't coming.

Read the document one more time, make a call, and move on. It'll still be there if you need to revisit the reasoning.

## Related Playbooks

- [AI Driven Writing](ai-driven-writing.md) — If your rubber duck session is about figuring out what you want to say, the document you produce can become the thesis and raw material for the writing pipeline.
- [Decision Documentation](decision-documentation.md) — If the session is about making a decision, the document can feed directly into a structured decision record.
- [Automated Journaling](automated-journaling.md) — Capture next steps and reasoning in your journal to connect thinking sessions to the work that follows.
- [SOP / Process Documentation](sop-process-documentation.md) — Sometimes you rubber duck your way through explaining how something works and realize you've written most of an SOP.
- [Research Assistant](research-assistant.md) — Gather context before a rubber duck session so you're working from evidence, not memory.
- [Knowledge Digest](knowledge-digest.md) — If you've been digesting content over time, your accumulated notes become high-quality input for rubber duck sessions.

## Examples

*Examples coming soon.*