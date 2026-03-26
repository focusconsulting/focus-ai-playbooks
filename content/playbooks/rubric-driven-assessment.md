---
title: "Rubric Driven Assessment"
description: "Codify your thinking into a concrete rubric, then let AI apply it consistently as your work evolves."
tags:
  - production + review
related_playbooks:
  - ai-driven-writing
  - generating-speaker-notes
  - audience-translation
  - generating-variations
---

# Rubric Driven Assessment

You already know what good looks like. The problem is applying that judgment consistently — especially when you're deep in the work and can't see it clearly anymore.

This playbook is about getting your standards out of your head and into a rubric that an AI can apply on your behalf. It might be five bullet points. It might be a detailed scoring table. What matters is that it's specific enough to produce useful feedback when someone other than you evaluates against it.

These rubrics should be extremely specific to your situation. A rubric for a government white paper might incorporate research on how agencies evaluate proposals, or details about the specific reviewers who will read it. "Clear and concise" doesn't tell you much. "Addresses the reviewer's known concern about implementation timelines" does.

You drive the rubric. The AI applies it. You keep control of what matters; the AI handles the repetitive checking.

This pairs naturally with almost any content production workflow, which makes it one of the more useful playbooks in the collection.

## When to Use

- You're producing multiple pieces of content that need to meet the same standard.
- You keep giving the same feedback on your own drafts or on AI output.
- You want to evaluate AI-generated content but don't have a clear framework for what "good enough" means here.
- You're iterating across drafts and want a concrete signal on whether things are improving.
- You need to hand off quality standards to someone else — or to yourself six months from now.

## The Play

### Start with your gut reaction

Before building anything, pull up a piece of content you think is strong and one you think is weak. What separates them? Write down whatever comes to mind, unorganized.

The rubric should capture *your* judgment, not a generic standard. If you skip this and ask the AI to generate a rubric from scratch, you've outsourced the thinking.

### Draft the rubric collaboratively

Bring your rough notes to the AI and ask it to help organize them into a structured rubric. A useful rubric typically has:

**Dimensions** — the aspects you're evaluating. Clarity, structure, tone, accuracy, completeness — whatever actually matters for this piece of work.

**Levels** — what each dimension looks like at different quality tiers, with a score attached. A dimension might score 1 through 5, where 1 means the content misses entirely and 5 means it nails it. Each dimension gets its own score, and those scores sum to a total you can track across drafts. The scoring also forces the AI to commit to a judgment instead of giving you "this is mostly good" non-feedback.

**Specific indicators** — these make or break the rubric. "Uses concrete examples to support each claim" is evaluable. "Is well-written" is not. If you're writing for a particular audience, the indicators should reflect what that audience cares about.

Push back during this step. If the AI suggests a dimension that doesn't match what you care about, cut it. If the indicators are too generic, ask it to ground them: who is reading this, and what do they need to walk away with?

The rubric might end up being five focused bullet points or a detailed table. Either is fine as long as the criteria are specific.

### Test the rubric if you can

If you have content you've already formed an opinion on, use it to validate the rubric. Give the AI a piece and ask it to score against the rubric. Compare its scores to your gut.

Where the scores diverge, the rubric has a gap — a missing dimension, poorly calibrated levels, an ambiguous indicator. Refine and test again. This calibration is what makes the rubric trustworthy going forward.

Not always possible, especially for something new. The rubric will still sharpen through use.

### Apply the rubric in a separate session

Evaluate your content in a different AI session from the one you used to create or iterate on it. The working session has context that biases evaluation — it "knows" what you were trying to do. A fresh session sees only the content and the rubric, which is closer to how your actual audience will experience it.

Provide the rubric in full and ask for a dimension-by-dimension assessment with scores and reasoning. "How does this look?" gets you nothing. A scored rubric gives you something concrete: a total that went from 18 to 23 between drafts tells you more than "it's getting better."

Use the rubric as a checkpoint throughout your workflow — after a draft, after a revision, after a major restructure. It gives you a signal on whether your edits are actually moving things in the right direction.

### Add-on: Calibrate with human raters

This step is optional but dramatically increases rubric reliability. It's especially worth doing when the rubric will be used repeatedly or when the stakes are high enough that "close enough" isn't good enough.

**Select your raters and samples.** Choose two other people — ideally people who understand the domain or the audience. Then pick three pieces of content to evaluate. Choose items that span a range of quality: one you think is strong, one middling, one weak. This spread forces the rubric to differentiate rather than clustering everything in the same score range.

**Have each person score independently.** Give all three raters (including you) the rubric and the three items. Everyone scores each item against each dimension without discussing it first. Independent scoring is important — you're trying to find where the rubric is ambiguous, and discussion before scoring masks exactly the disagreements you need to surface.

**Level-set together.** Compare scores across all three raters. Where scores align, the rubric is clear. Where they diverge, dig in: was the indicator ambiguous? Did people interpret a dimension differently? Were the level descriptions too vague to distinguish a 3 from a 4? Work through the disagreements and agree on an expected score for each item across each dimension. These consensus scores become your benchmark.

**Run the AI against the same items.** In a fresh session, give the AI the rubric and each of the three items. Compare its scores to the consensus scores from your human raters.

**Iterate until scores converge.** Where the AI scores diverge from the human consensus, the rubric still has gaps — language that humans can interpret from context but that the AI reads differently, or indicators that aren't specific enough to produce consistent results across any evaluator. Revise the rubric and re-run until the AI's scores track closely with the human benchmark. You don't need perfect alignment, but the pattern of scores should match: the strong piece should score highest, the weak piece lowest, and the gaps between dimensions should be directionally consistent.

The investment here pays off every time the rubric gets used afterward. A rubric that produces consistent scores across humans and AI is one you can trust to run without babysitting.

### Evolve the rubric over time

Your standards will shift as you learn what works. When you notice the rubric missing something or over-weighting a dimension that stopped mattering, update it. Treat it as a living document.

## Related Playbooks

- [AI Driven Writing](ai-driven-writing.md) — Use the rubric at each stage of the writing pipeline (thesis, outline, draft) to catch issues early rather than only at the end.
- [Generating Speaker Notes](generating-speaker-notes.md) — Apply a rubric tuned for spoken delivery: pacing, audience awareness, transitions.
- [Audience Translation](audience-translation.md) — Build audience-specific rubrics so the same content can be evaluated differently for different readers.
- [Generating Variations](generating-variations.md) — Use a rubric to evaluate and rank variations of taglines, pitches, or messaging rather than relying on gut feel alone.
