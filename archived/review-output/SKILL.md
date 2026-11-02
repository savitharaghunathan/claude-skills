---
name: review-output
description: Critically reviews AI-generated output by asking three probing questions to surface hidden risks, rejected alternatives, and areas of low confidence. Use after generating code, plans, or any non-trivial output.
---

After generating output, perform a structured self-review by answering these three questions honestly and specifically. Do not give vague or generic answers — ground every point in the actual work you just produced.

## 1. What was the hardest decision you made here?

Identify the trickiest judgment call in the output. Explain:
- What made it difficult (competing constraints, ambiguity, trade-offs)
- What you chose and why
- What could go wrong with that choice

## 2. What alternatives did you reject, and why?

List at least two concrete alternatives you considered but did not use. For each:
- Describe the alternative approach
- Explain why you rejected it (performance, complexity, correctness, style, etc.)
- Note if any rejected alternative might actually be better in a different context

## 3. What are you least confident about?

Be direct about weak spots. Call out:
- Any assumptions you made that you couldn't verify
- Parts of the output that feel brittle or under-tested
- Areas where a domain expert might disagree with your approach

---

Format the review clearly with these three numbered headings. Be concise but specific — each answer should reference actual lines, functions, or decisions from the output, not abstract generalities.
