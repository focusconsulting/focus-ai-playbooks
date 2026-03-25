---
title: "Decision Documentation"
description: "Structure the tradeoffs and reasoning behind a decision so it can be understood and revisited later."
tags:
  - process + operations
related_playbooks:
  - rubber-duck-with-memory
  - sop-process-documentation
  - ai-driven-writing
---

# Decision Documentation

Decisions decay. The context that made a choice obvious disappears: the person who made it leaves, the situation shifts, and six months later someone is relitigating it without access to the reasoning. Or you made a judgment call in the moment and now you need to defend it and can't remember why it felt right.

This playbook is about capturing the reasoning behind decisions, not just the decision itself. The AI helps you think it through, surfacing assumptions you haven't stated, options you might have missed, and objections worth addressing. The output is a document that can be shared, referenced, or revisited.

Not every decision warrants this treatment. The [Bezos decision-making framework](https://productmindset.substack.com/p/bezos-decision-making-framework) draws a useful distinction: **Type 1 decisions** are one-way doors — hard or impossible to reverse, high stakes, worth slowing down for. **Type 2 decisions** are two-way doors — easily reversible, and better served by moving fast and course-correcting. This playbook is for Type 1 decisions, or for Type 2 decisions that are being mistakenly treated as Type 1 and need the analysis to prove it.

The document doesn't need to be formal. An ADR (Architecture Decision Record) for an engineering team looks different from a one-page memo for a leadership discussion. Engineering teams often commit a tech spec or ADR directly to the repo alongside the code it governs. The form adapts. What stays consistent is the structure: here's what we decided, here's what we considered, here's why we landed here.

## When to Use

- You're making a significant decision and want to think through it more carefully before committing.
- A decision needs to be shared with people who weren't in the room when it was made.
- You're making a choice you'll need to defend later and want the reasoning documented now.
- You're reviewing a past decision and need to understand the context it was made in.
- Your team keeps revisiting the same questions because the original reasoning was never written down.

## The Play

### Start with what you already know

Before you bring the AI in, write down what you know: the decision you're trying to make, the options you're aware of, and your initial lean if you have one. Rough notes are fine. The point is to start from your actual thinking rather than letting the AI frame the problem for you.

If you're not sure where to start, describe the situation: what's prompting this decision, what constraints exist, and who it affects.

### Use the AI to challenge your thinking

Give the AI your notes and ask it to help you think through the decision before you document anything. Specifically:

- **What options aren't you considering?** You can easily anchor on the obvious two choices and miss a third that's actually better.
- **What assumptions are you making?** What would have to be true for your preferred option to be the right one?
- **What are the strongest objections?** Not strawmen, but the real reasons someone would push back.
- **What are the reversibility and downside risks?** Use the Type 1 / Type 2 lens here. If the decision is easily reversible, you might not need a full document. Just make the call and move. If it's a one-way door, the analysis is worth the time.
- **Why make this decision now?** What happens if you defer it? Sometimes the right move is to wait for more information. Bezos suggests deciding at roughly 70% of the information you wish you had, but that means acknowledging what you don't know.

Push back on the AI if it surfaces options you've already ruled out or concerns you've already addressed. Keep the conversation focused on what's actually uncertain.

### Structure the document

Once you've thought it through, ask the AI to draft the decision document. A useful structure:

**Context** — What's the situation? What prompted this decision? What's the forcing function or the cost of deferring? What constraints are in play?

**Options considered** — What were the realistic choices? A brief summary of each, without loading the framing in favor of what you picked.

**Decision** — What was decided? State it clearly.

**Reasoning** — Why this option over the others? What criteria mattered most? What tradeoffs did you accept?

**Assumptions** — What has to be true for this to be the right call? If those assumptions turn out to be wrong, what would change?

**Dissenting views** — Were there reasonable objections that didn't carry the vote? Capturing them shows you considered them and makes it easier to revisit if circumstances change.

**Next steps** — What needs to happen as a result of this decision?

Not every section is necessary for every decision. Trim what doesn't apply.

### Review for completeness

Read the draft and ask: would someone who wasn't in the room understand why this decision was made? Would they understand what was ruled out and why? If the assumptions section is empty, you probably have undocumented assumptions. If the dissenting views section is empty, either no one disagreed (unlikely) or the pushback didn't make it into the document.

The document doesn't need to be long, but it needs to be honest. A document that only captures why the winner was great doesn't help you revisit the decision if things go sideways.

### Store it somewhere retrievable

A decision document that nobody can find is useless. Put it where the relevant people will look: a team wiki, a Notion page linked from the relevant project, or for engineering decisions, committed to the repo as an ADR or tech spec alongside the code it applies to. Add a date.

## Related Playbooks

- [Rubber Duck with Memory](rubber-duck-with-memory.md) — If you're genuinely uncertain and need to think before you document, start with a rubber duck session. Clarity often comes from talking through it rather than trying to write it.
- [SOP / Process Documentation](sop-process-documentation.md) — If a decision results in a new or changed process, document that too. The decision doc explains why; the SOP explains how.
- [AI Driven Writing](ai-driven-writing.md) — If the decision document is going to a broader audience (a leadership memo, a public-facing rationale), use the writing pipeline to sharpen the output.

## Prompts

### Decision thinking partner

Use this before drafting the document, when you want to think it through.

```text
I'm trying to make a decision and want to think through it carefully before committing.

Here's the situation: [describe it]
Here are the options I'm considering: [list them]
My initial lean is toward [option] because [rough reasoning].

Help me pressure-test this. What options might I be missing? What assumptions am I
making? What's the strongest case against my preferred option? What would I need to
believe for a different choice to be right?
```

### Decision document draft

Use this once you've thought it through and are ready to write it up.

```text
Help me draft a decision document based on this conversation. Structure it as:

- Context (what's the situation and what prompted the decision)
- Options considered (realistic choices, neutrally described)
- Decision (what was decided, stated clearly)
- Reasoning (why this option, what tradeoffs were accepted)
- Assumptions (what has to be true for this to be right)
- Dissenting views (reasonable objections that didn't carry)
- Next steps

Keep it concise. This should be readable by someone who wasn't in the room.
```

## Examples

*Examples coming soon.*
