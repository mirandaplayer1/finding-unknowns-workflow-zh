---
name: reflect
description: Post-completion reflection and memory promotion. Trigger in a NEW conversation after a round of work ends, or when the user says "reflect", "retrospective", or "distill the lessons". Never run it casually inside the working conversation.
---

# Reflect

Purpose: Distill the working-level play-by-play into rules and lessons that last. Must run in a separate conversation with completely fresh context — a producer grading its own work suffers confirmation bias.

## Steps

1. Read `notes/implementation-notes.md`, the recent entries in `DECISIONS.md`, the spec change log in `SPEC.md`, and the change report and quiz results from `/quiz` (the user's wrong answers are a signal that "the decision log wasn't written clearly enough").
2. **Compare plan against reality**: which deviation log entries reflect spec defects (should be folded back into SPEC.md), which are process problems (candidates for rules in the working rules file), and which were one-off accidents (fine to leave in the notes).
3. **Promotion decision (gated)**: The rules file is `WORKFLOW.md`; do not write into CLAUDE.md — that's just an import shell (only keep using CLAUDE.md in older projects where the rules already live there).
   - The same kind of lesson appeared twice or more → condense it into one rule in the rules file's self-improvement section, with a one-line source.
   - Appeared only once → it stays at the notes layer; no promotion this time.
   - Check the existing rules in the rules file: any that were never violated again and are now internalized? Propose deleting them to keep the rules file lean.
4. **Decision log quality check**: Spot-check recent DECISIONS.md entries — is the "how to judge this myself next time" actually portable? Rewrite the vague ones.
5. **Wrap up**: Archive implementation-notes.md to `notes/archive/YYYY-MM-DD.md` and start a clean new notes file.
6. Report to the user: what was promoted, what was deleted, and why, so they can veto. More than five proposals → build an HTML review page (each item with an "approve / veto" checkbox plus a comment field, and a "copy decisions" button at the bottom); execute the writes only after the user pastes their decisions back.

## Principles

- Prefer promoting too little: every line in the rules file is a fixed cost paid in every conversation, and a stale rule misleads more than no rule at all.
- Every write action: list it first and get consent, then execute.
- All HTML output follows WORKFLOW.md "HTML output and interactive interfaces": embedded comment layer + "copy results" exit (ready-made snippet: `notes/html-comment-layer.html`).
