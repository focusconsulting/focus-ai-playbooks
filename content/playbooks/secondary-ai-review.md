---
title: "Secondary AI Review"
description: "Use a fresh AI session to catch the patterns and tics that accumulate when AI helps you write."
tags:
  - production + review
related_playbooks:
  - ai-driven-writing
  - rubric-driven-assessment
  - audience-translation
  - generating-speaker-notes
---

## Overview

When you work with AI on a piece of writing, the output picks up patterns. You've seen them even if you haven't named them. Filler phrases that sound confident but say nothing. Em-dashes used three times per paragraph. Lists where every item has exactly three sub-points. Hedging language that softens every claim. Transitions that all follow the same structure.

The problem is that the AI session you've been working in won't catch these. It produced them. It thinks they're fine. If you ask it to review its own work, it will mostly tell you it looks good, because within the context of that session, it does.

This playbook uses a separate AI session or a different model entirely to review the output with fresh eyes. The second session has no memory of what you were trying to do, no context about your drafts and revisions, and no attachment to the choices that were made. It sees only what your reader will see. That distance is what makes it useful.

## When to Use

- You've been iterating on a document with AI assistance and it's gone through several rounds of revision. The more rounds, the more AI patterns accumulate.
- Something feels "off" about the writing but you can't pinpoint what. It reads fine sentence by sentence but doesn't sound like a person wrote it.
- You're about to publish or share something externally and want to make sure it doesn't read like AI output.
- You used AI to fill in content from an outline and want to clean up the result before treating it as a real draft.
- A colleague or client has mentioned that something "sounds like AI" and you want to prevent that feedback.

## The Play

### Open a completely separate session

This is the core of the playbook. Do not review the document in the same session you wrote it in. Start a new conversation with no prior context. If you have access to a different model, even better. The point is that the reviewer has zero knowledge of your intent, your outline, your earlier drafts, or the conversation that produced the document.

Paste in the document and nothing else. Don't explain what it's about. Don't give background. The reviewer should encounter this the way a reader would: cold.

### Ask for specific AI writing patterns

Don't ask "does this look good?" or "can you improve this?" Those prompts invite the AI to make the writing more like its own preferences, which is the opposite of what you want.

Instead, ask it to identify specific patterns. Some things worth flagging:

**Filler phrases** that add words without adding meaning. "It's worth noting that," "it's important to understand," "at the end of the day," "this is particularly significant because." These phrases pad the writing and slow the reader down.

**Em-dash overuse.** AI loves em-dashes. One or two in a document is fine. Six per page is a tell.

**Symmetric structures** where every section has the same number of points, every paragraph follows the same shape, or every list has exactly three items. Real writing is uneven. AI writing tends toward artificial balance.

**Hedging and softening.** "It may be helpful to consider," "this could potentially," "it's generally advisable." If the document is making a recommendation, it should make it. Hedging undercuts the point.

**Transition sameness.** If every paragraph starts with "This," "However," "Additionally," or "Moreover," the transitions have become mechanical.

**Inflated language.** Simple ideas dressed up in complex phrasing. "Leverage" instead of "use." "Facilitate" instead of "help." "Utilize" instead of... also "use."

Ask the AI to flag instances of each, with line references or quotes so you can find them in the document.

### Fix selectively, not wholesale

The review will probably surface a lot of instances. Don't hand the document back and say "fix all of these." That just replaces one set of AI patterns with another.

Instead, go through the flagged items yourself and decide which ones to change. Some filler phrases might actually serve a purpose in context. Some hedging might be appropriate for the audience. Your judgment on what to keep and what to cut is the whole point.

For the ones you do want to fix, rewrite them yourself or give the AI specific, targeted instructions. "Replace this sentence with something more direct" is better than "make this section sound less like AI."

### Build a personal hit list

After a few rounds of secondary review, you'll start noticing which patterns show up in your AI-assisted writing consistently. Maybe your sessions always produce em-dash heavy prose. Maybe the filler phrases cluster in introductions. Maybe the hedging gets worse in later sections where you gave the AI less direction.

Write these down. The next time you do a secondary review, you can give the reviewer your personal hit list upfront: "check specifically for these patterns." This makes the review faster and more targeted over time. It can also feed back into how you prompt during the writing process. If you know your output always hedges, you can tell the AI to be more direct from the start.

## Related Playbooks

- [AI Driven Writing](ai-driven-writing.md) — Secondary review is the natural final step after the writing pipeline. The more AI-assisted iteration a document has been through, the more it needs this.
- [Rubric Driven Assessment](rubric-driven-assessment.md) — If "doesn't sound like AI" is an important quality bar, build it into your rubric as a scored dimension.
- [Audience Translation](audience-translation.md) — When adapting content for a new audience, run a secondary review on the adapted version. Translation passes tend to introduce new AI patterns on top of whatever was already there.
- [Generating Speaker Notes](generating-speaker-notes.md) — Speaker notes that sound like AI are especially noticeable because spoken language has a different rhythm than written language. Worth a secondary review pass.

## Prompts

### Style-only editing pass

Use this prompt in a fresh session with the document pasted in below it.

```
You are editing the following content for style only. Do not change the meaning, 
argument, or structure. Do not add new ideas or remove existing ones. Your job is 
to make targeted edits that remove patterns commonly introduced by AI-assisted writing.

Specifically, look for and fix:

- Symmetric sentence structures where consecutive sentences or paragraphs follow 
  the same shape. Vary the rhythm.
- Em-dash overuse. Replace most em-dashes with simpler punctuation or restructure 
  the sentence. One or two in an entire document is fine.
- Filler phrases that add words without meaning: "it's worth noting that," 
  "it's important to understand," "at the end of the day," "this is particularly 
  significant." Cut them.
- Identical or formulaic transitions: "Additionally," "Moreover," "Furthermore," 
  "However" used mechanically. Rewrite for natural flow.
- Inflated language: "leverage" instead of "use," "facilitate" instead of "help," 
  "utilize" instead of "use," "implement" instead of "do." Use the simpler word.
- Hedging that weakens claims: "it may be helpful to consider," "this could 
  potentially," "it's generally advisable." If the content is making a point, 
  let it make the point.

This content will be read by busy, tired humans. Edit for concision. If a sentence 
can lose a word without losing meaning, lose the word.

Return the full edited document. Do not explain your changes.

---

[PASTE CONTENT HERE]
```

## Examples

*Examples coming soon.*