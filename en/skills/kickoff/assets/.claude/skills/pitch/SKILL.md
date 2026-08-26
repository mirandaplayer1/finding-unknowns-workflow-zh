---
name: pitch
description: Pitch / explainer page — packages the spec, prototype, decisions, and implementation notes into one shareable HTML that lets others quickly understand and nod along. Trigger when the work needs to be shown to a manager, colleague, or stakeholder, when buy-in or approval is needed, or when the user says "pitch", "make an explainer", "package this up for someone", or "help me get buy-in".
---

# Pitch & Explainer

Purpose: Delivery doesn't end when the work is done. The reader arrives carrying "exactly the same unknowns you started with"; the pitch's job is to eliminate those unknowns for them — and to let experts see at a glance that you've already considered the failure points they would ask about.

## Steps

1. **Ask two things first** (one AskUserQuestion call for both):
   - Who is this for? — determines depth and vocabulary (managers want conclusions and risks; colleagues want context and approach).
   - What do you need them to do? — approve, give feedback, or follow along. The entire pitch is written around that action.
2. Read `SPEC.md`, `DECISIONS.md`, `notes/implementation-notes.md`, and this round's deliverable. If a /quiz change report exists, use it directly as material.
3. **Produce a single HTML** (saved to `notes/`), with a fixed five-block structure:
   - **The conclusion on the first screen**: what was done, why, and what you need from them; if a demo screenshot or GIF exists, put it right at the top.
   - **One picture beats three paragraphs**: an SVG flow diagram or a before/after comparison that makes the change clear.
   - **Risks and failure points already considered**: this is the section expert reviewers most want to check; writing it proactively speeds up approval. It's allowed to say honestly "not handled + why that's acceptable for now" — if this section is easy to write, the problem wasn't thought about hard enough.
   - **What this explicitly does not include**: draw the scope lines clearly so reviewers don't come in with wrong expectations — scope misunderstandings are the most expensive kind of back-and-forth.
   - **Decision summary**: one line per key trade-off, tagged with D-numbers; details always collapsed, closed by default.
4. Embed the comment layer per WORKFLOW.md "HTML output and interactive interfaces". When their feedback is pasted back into the conversation, fill it into `SPEC.md` or `DECISIONS.md`.

## Principles

- Write for their unknowns, not for your own memory: they haven't read a single file in this project — explain jargon and D-numbers on the spot.
- Cut anything past three screens: details that don't fit within three screens move into the collapsed sections. If one page can't tell the story, the conclusion usually isn't clear yet.
- This comes after /quiz: score perfect yourself first — only then are you qualified to explain it to someone else.
