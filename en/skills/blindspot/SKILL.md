---
name: blindspot
description: Pre-work blindspot scan and domain teaching. Trigger at the start of a new project or phase, when entering an unfamiliar domain or unfamiliar material, or when the user says "blindspot pass", "scan for blindspots", "find my unknowns", "teach me this domain", or "teach me how to give better instructions".
---

# Blindspot Pass

The purpose has two layers: (1) surface the user's "unknown unknowns"; (2) **teach the user the domain so they can give better instructions**. The scan is the means; raising their ability to ask is the end — next time they'll be able to ask the right questions themselves.

## Steps

1. **Locate the starting point**: Read `SPEC.md` and existing project material, and confirm the user's experience level in this domain — "I know nothing about X" and "I've done something similar" lead to different teaching depths. When unsure, just ask.
2. **Scan for unknown unknowns**: List the aspects they may not have considered at all — domain conventions, common pitfalls, default audience expectations, material constraints. Search the web to fill gaps when needed.
3. **Domain crash course** (the core of this skill — the "teach me color grading" mode):
   - **Mental model**: how this domain's logic reads in one sentence; what an expert looks at when judging a piece of work.
   - **Jargon glossary**: what each key term they need actually means — only with the right words can they give the right instructions.
   - **What counts as "good"**: where the difference between good and bad lies, ideally with contrasting examples (find two examples and point out the differences), so they go from "can't see the difference" to "can tell good from bad".
   - **Common failure patterns**: the holes beginners fall into most, and the symptoms that signal the direction is wrong.
4. **Produce "better instruction" examples**: Rewrite their original request into two or three concrete instruction examples, explaining what changed and why — e.g. "make my video look nice" becomes "grade toward teal-orange, keep skin tones natural, raise contrast one notch". These are ready to copy and use directly, and also models to learn from.
5. **Presenting the teaching**: Combine the crash course (step 3) and the instruction examples (step 4) into a **single-page HTML handout** (saved to `notes/`) — an SVG diagram of the mental model, the jargon table, good/bad examples side by side, and a copy button on every instruction example. Long-form content meant for humans to read goes in HTML, not long markdown.
6. **Fill back and hand off**: Write new facts and judgment criteria into `SPEC.md` (judgment criteria usually belong under acceptance criteria or reference examples); ambiguities that are "known unknowns" go into the unknowns list; if the list still has open items, go back and run `/interview`; only start work once everything has converged.

## Principles

- Teach before doing the work for them: in a domain where they "can't even tell good from bad", teach until they can judge before producing anything — otherwise no number of versions will let them choose.
- Match teaching depth to the purpose: they need to "give instructions and verify results", not become an expert; crash-course to sufficiency, don't dump the whole domain on them.
- End every teaching session with one question: "How would you now re-describe what you want?" — their restatement is the test of what they learned.
- All HTML output follows WORKFLOW.md "HTML output and interactive interfaces": embedded comment layer + "copy results" exit (ready-made snippet: `notes/html-comment-layer.html`).
- "No major blindspots here" is a valid and valuable result: don't force a list of blindspots just to show your work — invented blindspots waste the interviews and attention that follow.
- This skill ends at "fill back the spec, hand off": no implementation without the user's request.
