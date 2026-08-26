---
name: kickoff
description: Project kickoff — sets up the project skeleton (when files are missing) and distills a first draft of SPEC.md from a rough idea. Trigger when a project is just starting or work begins in an empty folder, when SPEC.md is still a blank template, or when the user says "kickoff", "init", "initialize the project", "draft a spec", or "I want to build... (a rough idea)". Install location: user level (~/.claude/skills/), so the skill is available even in empty projects.
---

# Kickoff

Purpose: A spec draft should not come from the user staring at a blank template and filling it in from thin air — it should be distilled from a brainstorming conversation. The user only needs to bring a rough idea; when the workflow skeleton (file templates) is missing, this skill sets it up along the way.

**Gate: No implementation begins before the user approves the SPEC.md draft. Every project goes through this flow, no matter how simple — a simple project's spec can be a few sentences short, but it cannot be skipped. Projects "too simple to need a spec" are exactly where unexamined assumptions cause the most rework.**

## Steps

0. **Skeleton check and setup**: List the project folder contents and confirm the skeleton (`WORKFLOW.md`, `SPEC.md`, `DECISIONS.md`, `notes/`, `.claude/skills/`) is in place. If complete, go straight to step 1; if anything is missing, copy everything under this skill's `assets/` into the project root (preserving relative paths), with these rules —
   - **Never overwrite existing files**: ask about each name collision one by one, defaulting to skip; the user's work matters more than the template.
   - Existing `CLAUDE.md` → do not overwrite it or merge content; only append a single line `@WORKFLOW.md` at the end of the file (leave it untouched if the line is already there), and tell the user before appending.
   - **Copy faithfully**: do not "improve" the templates in assets along the way; templates evolve through each project's `/reflect` feedback, which the user then applies to this skill's assets by hand.
   - After setup, list the file tree to verify (including the six project-level skills under `.claude/skills/` and `CLAUDE.md` containing `@WORKFLOW.md`), then continue straight into step 1 — this skill lives at the user level, so no new conversation is needed.
   - If the user only wants the skeleton and isn't ready to talk content yet, stop here, and note that they can say "I want to build X" later to continue.
1. **Hear the starting point**: Ask the user to say in a few sentences what they want to build, why now, and whether they have a vague picture or reference in mind. Don't press for details — get the raw material first.
2. **Explore**: Read existing material in the project folder (past work, data, notes); search the web when needed to learn domain conventions and comparable work.
3. **Scope assessment**: Before asking any questions, judge — is this idea one project, or several independent sub-projects (e.g. "course material + marketing site + signup system")? If the latter, help decompose first: what the independent parts are, how they relate, a suggested order — then proceed with only the first sub-project. Don't waste questions on the details of a project that should have been split in the first place.
4. **Brainstorm directions**: Propose three to five approaches, ordered from minimum-viable to most ambitious, each with one line on "under what conditions you'd pick this". **Put the recommended option first and explain why**, so the user can simply agree or push back. This step prevents scoping too narrow (missing a high-value approach) or too wide (never finishing). Label each direction with **the belief it bets on** (e.g. "this version assumes full coverage beats fast onboarding") — only when the belief is written down can the user argue with the belief instead of picking at the surface. When the user vetoes a direction, distill the veto into one line — "you rejected X, which means the real need is Y" — and, once confirmed, write it into the spec: reactions to options are themselves spec material. When the differences between approaches hinge on "how the industry solves this" and nobody knows yet, run `/scout` first to produce a comparison report, then come back to choose. When there are more than three directions, or the differences suit visual presentation, build a **single HTML comparison page** (saved to `notes/`): a side-by-side grid, each direction annotated with its trade-offs and when it applies, simple diagrams welcome, with a "copy my choice" button at the bottom that outputs the choice plus reasoning for the user to paste back into the conversation.
5. **Draft SPEC.md section by section**: Fill in each section following the chosen direction, **presenting each completed section and asking "does this look right so far?"** before writing the next (pace by complexity — simple sections can be batched) —
   - One-line goal, audience and context, in scope / out of scope: distilled from the conversation, in the user's own words.
   - Skeleton: propose proactively (directory structure, narrative arc, page flow), marked "first draft, pending confirmation".
   - Acceptance criteria: propose a verifiable definition of done.
   - Unknowns list: record every question that came up in conversation without a conclusion, in its corresponding quadrant.
   - Reference examples: any references mentioned in the conversation.
6. **Spec self-review**: After writing, scan the whole thing with fresh eyes and fix in place —
   - Placeholder scan: any "TBD", "to be filled in", or vague sentences left?
   - Consistency: do the sections contradict each other? Does the skeleton match the goal?
   - Scope check: is this spec still so big it should go back for decomposition?
   - Ambiguity check: can any sentence be read two ways? If so, pick one reading and pin it down.
7. **Approval and hand-off**: Ask the user to read the spec and approve it. Once approved, suggest running `/interview` next (to settle what's undecided) and then `/blindspot` (to scan for what hasn't been thought of); if the user requests changes, make them and rerun step 6.

## Principles

- The first draft optimizes for speed, not completeness: loosely right beats precisely wrong; details are for the next two skills to converge.
- Distill, don't invent: spec content must come from the conversation and the materials; anything the agent assumed on its own is labeled "assumption" and added to the unknowns list.
- Scope proposals must include one "embarrassingly small" option — the minimum-viable version is often the right starting point; ruthlessly cut non-essential features from every direction (YAGNI).
- All HTML output follows WORKFLOW.md "HTML output and interactive interfaces": embedded comment layer + "copy results" exit (ready-made snippet: `notes/html-comment-layer.html`).
