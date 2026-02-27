---
title: "Research Assistant"
description: "Targeted research synthesis for a specific purpose, turning raw sources into actionable preparation."
tags:
  - intake + learning
related_playbooks:
  - rubric-driven-assessment
  - meeting-prep
  - onboarding-accelerator
  - rubber-duck-with-memory
  - knowledge-digest
---

## Overview

This playbook is about using AI to do focused research for a specific, time-bound purpose. You have a meeting on Thursday, an interview on Monday, a proposal due next week. You need to understand something well enough to be effective, and you don't have four hours to read everything yourself.

The word that matters here is targeted. This isn't general learning or ongoing curation. You have a concrete goal, specific sources to work from, and a clear picture of what you need to walk away knowing. The AI processes the raw material and produces a synthesis you can act on.

A common example: you've submitted a proposal and been invited to interview before a procurement panel. You have LinkedIn URLs for the four panelists. You need to understand their backgrounds, what they've worked on, what they probably care about, and where your proposal lines up with their priorities. Doing that manually for four people takes an hour or more. With this playbook, you can have a usable briefing in minutes.

## When to Use

- You have a meeting, interview, or presentation and need to get up to speed on the people or topics involved.
- You're preparing a proposal and need to understand the audience, their organization, or their industry well enough to tailor your approach.
- You've collected a pile of sources (articles, reports, profiles, internal docs) and need to extract what's relevant to a specific question.
- You need to compare or contrast multiple sources and pull out themes, disagreements, or patterns.
- Someone asked you to "get smart on" something by tomorrow.

## The Play

### Define what you need to know and why

Before you hand the AI anything, get clear on the purpose. "Research this company" is too vague. "I'm pitching this company on our analytics platform next Tuesday and I need to understand their current tech stack, recent strategic priorities, and the background of the three people in the room" — that's something the AI can work with.

Write down the specific questions you need answered. These become the structure of your output. If you can't articulate what you need to know, you're not ready to research yet — you'll just accumulate information without a frame for what matters.

### Gather your sources

Pull together whatever raw material you have: LinkedIn profiles, company websites, annual reports, news articles, internal docs, prior meeting notes, Slack threads. The AI can process a lot at once, so err on the side of giving it more.

Be deliberate about what you include, though. If you're preparing for a meeting with a specific person, their LinkedIn, recent talks or posts, and their company's latest news are high-signal. A random industry report from two years ago probably isn't.

If you don't have sources yet, the AI can help find them — search for recent news about the company, find published work by a particular person, identify key reports in a domain. [Claude for Chrome](../tooling/claude-for-chrome.md) is especially useful here: you can browse LinkedIn profiles, company pages, and articles and have Claude process what's on the page without copying and pasting content back and forth. But treat this step as gathering, not analysis. Collect first, synthesize second.

### Give the AI your sources and your questions

Feed everything in along with your questions. Be explicit about the output format. A briefing organized by person is different from one organized by theme, and both are different from a comparison table. Ask for markdown — easy to read, easy to edit, easy to move elsewhere.

Tell the AI what the research is for. "I need to prepare for a sales call" produces different emphasis than "I need to evaluate whether to partner with this company," even with the same underlying sources. Purpose shapes what gets highlighted and what gets buried.

If the source material is long, consider processing it in batches and then asking the AI to synthesize across them. One pass through everything is simpler but can dilute the output when you're working with a lot of material.

### Check the output against your questions

Go back to the questions you wrote down at the start. Does the synthesis actually answer them? Are there gaps where the sources didn't cover something you expected? Are there claims that feel like the AI filled in rather than pulled from the material?

Your judgment matters here. The AI is good at extracting and organizing. It's less good at knowing what you don't know. If the briefing says nothing about a topic you expected to find, that might mean the sources didn't cover it, or it might mean the AI didn't flag it. Ask directly.

If you have a [rubric](rubric-driven-assessment.md) for what a good briefing looks like, apply it here. Over time you'll develop a feel for what level of preparation actually makes a difference and can calibrate accordingly.

### Update as you learn more

Research isn't always one-shot. After the first meeting, you'll know more about what matters. After the initial briefing, you might realize you need depth on a topic you originally skipped over. Go back, add new sources or questions, and have the AI update the synthesis.

If the research feeds into something ongoing rather than a single event, consider moving to a [knowledge digest](knowledge-digest.md) workflow where you're continuously processing new material instead of doing one-off sprints.

## Related Playbooks

- [Rubric Driven Assessment](rubric-driven-assessment.md) — Build a rubric for what a good briefing looks like so you can evaluate research quality consistently, especially if you do this kind of prep regularly.
- [Meeting Prep / Pre-read Generator](meeting-prep.md) — Meeting prep is a specific application of research. If your research is for a meeting, this playbook adds structure around agendas and attendee context.
- [Onboarding Accelerator](onboarding-accelerator.md) — If you need to understand a whole domain, team, or role rather than prepare for a single event, the onboarding playbook is a better fit.
- [Rubber Duck with Memory](rubber-duck-with-memory.md) — Once you have your research, talk through what it means and how to act on it.
- [Knowledge Digest](knowledge-digest.md) — If a one-off research task turns into an ongoing need, transition to a digest workflow for continuous processing.

## Examples

*Examples coming soon.*