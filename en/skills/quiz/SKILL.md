---
name: quiz
description: Produces a comprehension quiz. Trigger when a round of work is complete, before delivery or final sign-off, or when the user says "quiz me", "test me", or "make sure I actually understand this".
---

# Quiz

Purpose: Merely browsing the deliverable yields only shallow understanding — much of what matters hides in "why it's arranged this way" and "what else is affected if you touch this". Before delivery, use a quiz to confirm the user truly understands this round's output.

## Steps

1. Read this round's changes, the new entries in `DECISIONS.md`, and `notes/implementation-notes.md`.
2. Produce a **single interactive HTML file** (saved to `notes/`): the top half is a change report, containing in order:
   - Mental model: after this change, how the whole deliverable's logic reads in one sentence
   - What was done and why (linked to the relevant decision numbers)
   - Ripple map: which parts of the existing content this change affected (use an SVG diagram of the ripple relationships where it fits)
   - Deviations from the plan
3. The bottom half is an interactive quiz, five to eight questions, with clickable options and instant right/wrong plus a short explanation on submit; at the bottom, a "copy my results" button that outputs each answer and whether it was right as structured text. Questions must cover:
   - At least one "why A and not B" question (mapping to DECISIONS.md)
   - At least one edge case ("if the audience were X / the context became Y, does this arrangement still hold?")
   - At least one blast-radius question ("if you changed this part, what else has to move with it?")
4. When the user pastes their results back into the conversation, go deep on the wrong answers, pointing back to the exact spot in the deliverable. For each wrong answer, first diagnose which kind it is — and say which: (a) a gap in the user's understanding → explain further; (b) the deliverable is too convoluted → that's a "this should be simplified" signal, not the user's fault. The results also feed /reflect (a wrong answer = a signal that the decision log wasn't clear enough).
5. Recommend delivery only on a perfect score; otherwise re-explain the weak spots and issue new questions. Two misses in a row on the same topic → recommend simplifying or splitting that part of the deliverable instead of writing more questions.
6. After a perfect score, hand off: if the work needs to be shown to others or needs buy-in → `/pitch`; if not, deliver directly, then run `/reflect` in a new conversation.

## Principles

- Test understanding, not recall: ask about judgment and causality, not "what did page N say".
- When explaining, give the mental model first, then the details.
- All HTML output follows WORKFLOW.md "HTML output and interactive interfaces": embedded comment layer + "copy results" exit (ready-made snippet: `notes/html-comment-layer.html`).
