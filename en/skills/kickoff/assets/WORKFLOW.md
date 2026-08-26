# Standing Project Instructions

## File map (read this first)

All of this project's memory lives in files, divided as follows:

- `SPEC.md` — the spec, single source of truth. Read it every time you start work; if it's still the blank template, run `/kickoff` first.
- `DECISIONS.md` — decision log, teaching-oriented. Any decision with a real trade-off goes here.
- `notes/implementation-notes.md` — this round's plan, progress, and deviation log. Working journal; archived after retrospective.
- `notes/*.html` — interactive interfaces for me to read and operate (questionnaires, handouts, reports). Disposable.
- This file (WORKFLOW.md) — working rules, auto-loaded via the `@WORKFLOW.md` import in the root `CLAUDE.md`. Only the `/reflect` promotion process may modify it.

Process order: `/kickoff` drafts the spec (run `/scout` in between when the approach is undecided, to see how the industry solves it) → `/interview` and `/blindspot` converge the unknowns → implementation plan → implementation → `/quiz` to confirm you understand it → (`/pitch` for buy-in when others need to see it) → `/reflect` retrospective in a new conversation.

## The spec is the single source of truth

- Read `SPEC.md` before starting any work. All output follows the spec, not memory.
- **Gate: while SPEC.md has not been approved by me (still the blank template, or littered with "to be confirmed"), do not start implementation — run `/kickoff` and finish the spec first. No project is too simple for this; a simple project's spec can be just a few sentences.**
- When work reveals a conflict between the spec and reality (materials aren't what we expected, constraints are tighter than imagined, the original approach doesn't work): stop, record the conflict in the "Unknowns list" in `SPEC.md` first, confirm with me or decide by the conservative principle, and only continue changing deliverables after the spec is updated. The spec always changes before the deliverables do.
- When the conversation is approaching compaction, write any unsettled decisions and findings into `notes/implementation-notes.md` and `DECISIONS.md` first, then let compaction happen.

## Decision log (teaching mode)

I am learning alongside you, so the decision process matters more than the outcome:

- Any decision with two or more reasonable options goes into `DECISIONS.md`, following the format at the top of that file — especially the "How to judge this yourself next time" field. Content trade-offs, structural choices, presentation formats, and tool choices all count.
- Purely mechanical steps with no real choice don't get logged — don't dilute the signal.
- When something off-plan happens: pick the conservative option (reversible, small blast radius), log it in the "Deviation log" in `notes/implementation-notes.md`, and keep moving — don't stall waiting for me.
- Division of labor between the two: the deviation log records "what happened and the stopgap taken"; if the deviation involves a substantive trade-off (two or more reasonable options), the trade-off itself goes into `DECISIONS.md` and the deviation table references its D-number — don't write it up twice.

## Working notes

- Before starting work, derive "this round's plan" from SPEC.md and write it into `notes/implementation-notes.md`: step order and completion checkpoints, with the decisions most likely to be overturned placed first so I see them first (data structures, external-facing presentation, skeleton changes; mechanical steps last). For simple tasks the plan can be two or three lines; execute only after I confirm.
- For big rounds (many steps, or ones that need diagrams or code snippets to explain), upgrade the plan into an HTML implementation-plan page saved in `notes/` — same rule, most-likely-to-change decisions first. Once the plan is approved, you may open a new conversation and bring the plan page and the spec along, so a clean context does the implementation.
- Maintain `notes/implementation-notes.md` throughout each working session: this round's plan, current progress, deviation log, unknowns awaiting confirmation.
- This is the working-layer journal — messiness is allowed. Distilling it is `/reflect`'s job, not the job of the work itself.

## HTML output and interactive interfaces

- When you need me to "read long content, compare multiple options, or answer a string of questions," don't use long markdown or a barrage of messages — produce a **single self-contained HTML file** (saved in `notes/`) using visual structure, tables, and SVG diagrams. I will not finish reading markdown longer than a hundred lines.
- **The interaction loop must close**: you can't see what I do in the browser, so every interactive HTML page must end with a "Copy results" button that turns my choices/answers into structured text I can paste back into the conversation; once received, settle the conclusions into the corresponding files. An interactive interface with no exit might as well not exist.
- **Every HTML page must be able to collect my feedback — read-only reports included** (comparison pages, handouts, reports, checklists, all of them): put a collapsible comment box next to every section, card, and step, and a fixed "Copy all feedback" button in the footer. Output format: `## Feedback on "Title"` followed by one `### Section name` heading plus content per comment; comments persist in localStorage across refreshes. A drop-in implementation snippet lives in `notes/html-comment-layer.html` — embed it in every new page. My reactions while reading a report are the most valuable feedback there is; no comment box means throwing them away.
- **Write pages in ADHD format**: conclusion and next step in the first screen; number every multi-step sequence; when a list runs long, group and layer it (do now / do later, essential / bonus) rather than cutting items — never drop important information for the sake of brevity; details always collapsed by default. One question per page — if it doesn't fit, split the page.
- Format division of labor: markdown for the always-loaded layer and files that need version diffing (SPEC, WORKFLOW, DECISIONS); HTML for interfaces I read and operate (proposal comparisons, questionnaires, reports, quizzes, implementation plans, pitches, disposable editors).

## Communication

- Explain decisions mental-model-first, then details. Name trade-offs directly; don't paper over contradictions.
- When I ask "why," answer in a way that lets me judge it myself next time, not just the conclusion.

## Self-improvement rules

- This file only accepts rules where "the same kind of lesson has appeared two or more times," promoted here by the `/reflect` process with a one-line note on its origin.
- One-off lessons stay in `notes/` — never write them directly into this file.
