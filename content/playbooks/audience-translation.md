---
title: "Audience Translation"
description: "Adapt a single document for different audiences without rewriting from scratch each time."
tags:
  - production + review
related_playbooks:
  - rubric-driven-assessment
  - ai-driven-writing
  - generating-variations
  - secondary-ai-review
  - research-assistant
  - rubber-duck-with-memory
---

## Overview

You wrote a solid document for one audience and now you need a version for a different one. The technical brief needs an executive summary. The internal strategy doc needs a client-facing version. The detailed proposal needs a two-pager for a stakeholder who won't read ten pages.

Most people handle this by opening a new document and rewriting from scratch, or worse, by sending the original and hoping the reader will pull out what's relevant to them. Both waste time — yours in the first case, theirs in the second.

This playbook uses AI to do the translation. You start with a strong base document and adapt it for each audience by changing what gets emphasized, how much detail to include, what language to use, and what to cut. The thinking stays the same; the packaging changes.

The rewriting isn't the hard part — AI handles that fine. Being precise about what each audience needs is. An executive and a practitioner reading about the same initiative care about different things, and "make it shorter" doesn't capture the difference.

## When to Use

- You have a document that works for one audience and need a version for a different one.
- You're preparing for a meeting or presentation where different stakeholders need different levels of detail from the same underlying material.
- You've written something technical that needs a non-technical version, or the reverse.
- You keep rewriting the same content from scratch for different readers and want to stop doing that.
- You need to send the same update to multiple groups (leadership, partners, the team) and each group cares about different aspects.

## The Play

### Start with a strong base document

The base document is your source of truth — the version with all the thinking, detail, and nuance. Everything else gets derived from it. If the base is weak, the translations will be too, just in a way that's harder to spot because the prose will sound fine.

If you don't have a strong base yet, write one first. The [AI-driven writing](ai-driven-writing.md) pipeline works well for this. Get the full version right before you start adapting.

### Define each audience concretely

For each audience you're translating to, write down three things:

**Who they are and what they already know.** A client who sat through your initial pitch needs a different follow-up than one seeing the material for the first time. A technical evaluator needs different framing than a procurement officer. The more specific you are about the person, the better the translation. If you don't know much about the audience, a [research assistant](research-assistant.md) session can help you build a profile from their LinkedIn, recent talks, or company news before you start.

**What they care about.** Not what you want to tell them — what they actually want to know. A client's CTO evaluating your proposal cares about integration risk and technical approach. Their CFO cares about cost structure and ROI timeline. Their program manager cares about milestones and what they need to provide on their end. Your specific audience might not fit these patterns, which is the whole reason to write it down rather than assume. If you're struggling to pin down what a particular audience cares about, a [rubber duck session](rubber-duck-with-memory.md) can help you talk through it.

**What they should do after reading.** Every document is trying to get the reader somewhere. Maybe it's "approve this budget." Maybe it's "feel confident enough in our technical approach to advocate for us internally." Maybe it's "understand what they need to have ready before the kickoff." If you can't name what the reader should walk away with, the translation won't have a clear shape.

### Give the AI the base document and the audience profile

Feed in the full base document along with your audience description. Be explicit about what should change. "Rewrite this for the client" is too vague. "Adapt this for the client's Director of IT — he attended our initial demo but wasn't in the technical deep-dive. He needs to understand what we're proposing, how it integrates with their existing systems, and what his team will need to do during implementation. Keep it under two pages and lead with the business outcomes." That gives the AI enough to make real choices about what to keep, cut, and reframe.

Tell the AI what format you want and ask for markdown. A one-page summary, talking points for a slide deck, and a three-paragraph email are all different shapes, and the shape forces different decisions about what makes the cut.

### Review for audience fit, not just accuracy

When you read the translated version, the question isn't just "is this correct?" — it's "would this land with the person I'm sending it to?" A version that's technically accurate but misses what the reader cares about hasn't done its job.

Check that the emphasis matches the audience. If you said the client's Director of IT cares about integration risk, does the translated version lead with that or bury it? Check that the detail level is right — enough that the reader can act, not so much that they're wading through material that isn't for them.

If you've built audience-specific rubrics through [rubric-driven assessment](rubric-driven-assessment.md), this is where they pay off. Score the translation against the rubric for that audience. If you haven't built rubrics and you're going to do this kind of translation regularly, it's worth the investment.

### Maintain a link back to the base

Translated versions drift from the source. The base document gets updated, someone edits the client summary directly, and now the two versions contradict each other. This gets worse the longer a document stays alive.

Keep a note in each translated version pointing back to the base and the date it was derived from. When the base changes, re-run the translation rather than trying to manually sync edits across versions. Re-translating from an updated base takes minutes; reconciling documents that have diverged over weeks is a nightmare.

## Related Playbooks

- [Rubric Driven Assessment](rubric-driven-assessment.md) — Build audience-specific rubrics so you can evaluate whether each translation actually works for its intended reader.
- [AI Driven Writing](ai-driven-writing.md) — Get the base document right first. A strong base makes every translation easier.
- [Generating Variations](generating-variations.md) — If you're not sure which framing will land for a given audience, generate variations of key sections and evaluate them before committing.
- [Secondary AI Review](secondary-ai-review.md) — After translation, review for AI patterns that crept in, especially if you're translating into a voice or tone that's different from the base.
- [Research Assistant](research-assistant.md) — If you're translating for an audience you don't know well, build a profile first from their LinkedIn, published work, or company context.
- [Rubber Duck with Memory](rubber-duck-with-memory.md) — If you're having trouble defining what an audience cares about or how they differ from another, talk it through before translating.

## Prompts

### Audience translation

Use this prompt in a session with the base document pasted in below it.

```
Translate the following content for a specific audience. Do not change the 
underlying facts, arguments, or conclusions. Your job is to adapt the emphasis, 
detail level, language, and structure so that it lands for the target reader.

Original content context:
[Describe what the base document is — e.g., "This is a technical proposal for 
a data platform modernization project. It was written for an internal engineering 
audience and covers architecture, implementation approach, timeline, and risks."]

Profile:
[Describe the target reader — e.g., "The reader is the client's Director of IT. 
He attended our initial demo but was not in the technical deep-dive sessions. He 
cares about how this integrates with their existing systems, what his team will 
need to do during implementation, and the business outcomes. He is not evaluating 
the technical approach in detail — he needs to feel confident it's sound and 
understand what it means for his organization."]

Adapt the content for this reader. Lead with what they care about most. Cut detail 
that doesn't serve them. Adjust language to match their context — avoid jargon they 
wouldn't use and explain concepts they might not be familiar with.

Output in markdown. Keep it under [LENGTH].

---

[PASTE BASE DOCUMENT HERE]
```

## Examples

*Examples coming soon.*