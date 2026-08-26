# Claude Code Project Scaffold Template (General-Purpose)

Works for any project with a concrete deliverable: course material, documents, slide decks, marketing plans, data reports — and code, of course. Goal: give the agent (1) persistent memory of the spec, (2) the ability to reflect, and (3) a decision log people can learn from.

## Mental model

The spec is the **map**; the actual working materials and constraints are the **territory**; the gap between them is the "unknowns." The model itself is stateless — everything worth remembering must land in files and be read at the right moment. The whole architecture therefore answers three questions: what should be always-loaded (every conversation), what should be on-demand (loaded when used), and what should be periodically distilled (promoted from journal to rule).

```
project root/
├── CLAUDE.md                  ← loader shell: a single line, `@WORKFLOW.md` (existing projects just append this line)
├── WORKFLOW.md                ← always-loaded layer: behavior rules (how to work, how to record)
├── SPEC.md                    ← always-loaded layer: the spec (single source of truth)
├── DECISIONS.md               ← learning layer: decision log (teaching-oriented format)
├── notes/
│   ├── workflow-guide.md      ← this file: template usage guide
│   ├── implementation-notes.md ← working layer: this round's notes and deviation log
│   └── html-comment-layer.html ← comment-layer snippet: embed directly in every HTML output
└── .claude/skills/
    ├── kickoff/SKILL.md       ← kickoff: draft a first SPEC.md from a rough idea
    ├── interview/SKILL.md     ← before work: interview to clarify the "known unknowns"
    ├── blindspot/SKILL.md     ← before work: scan for "unknown unknowns" + crash-course teaching
    ├── quiz/SKILL.md          ← before delivery: change report + quiz (do you actually understand it)
    ├── pitch/SKILL.md         ← at delivery: pitch (explainer) — help others understand, get buy-in
    └── reflect/SKILL.md       ← after work: retrospective and memory promotion
```

Two user-level skills complement this flow: `kickoff` (a same-named user-level version that builds the skeleton first in an empty folder, then drafts the spec) and `scout` (competitive research — when kickoff is picking a direction and "how does the industry solve this" is still unknown, run it in between).

## How the three needs are met

**The spec stays remembered**: SPEC.md is the single source of truth, and WORKFLOW.md (auto-loaded every conversation via the `@WORKFLOW.md` import in CLAUDE.md) forces the agent to read it before starting work, and to update the spec first — then the deliverables — whenever spec and reality conflict. Before conversation compaction, unsettled decisions get written into files first (borrowing OpenClaw's memory-flush concept), so the spec doesn't evaporate into a summary.

**The ability to reflect**: reflection isn't done casually inside the working conversation — you open a new conversation and run `/reflect`, an independent round with fresh context, avoiding the confirmation bias of a producer grading their own work. Promotion has a gate: only lessons of the same kind that appear two or more times get written into WORKFLOW.md; one-offs stay in the notes layer (borrowing OpenClaw Dreaming's promotion system, to keep the rules file from bloating).

**A decision log people can learn from**: the DECISIONS.md format is teaching-oriented — each entry records not just "what was decided" but "what the options were, why this one, and how you'd judge it yourself next time." This comes from the implementation-notes pattern in Thariq's article (when something off-plan happens, pick the conservative option, log the deviation, keep moving), plus his quiz pattern: pass a quiz before delivering, to confirm you truly understand what was produced.

## HTML as output and interactive interface

Long content for humans to read, and interfaces for humans to operate, always go in a single self-contained HTML file (saved in `notes/`, archived along with the retrospective): kickoff's direction-comparison page, interview's questionnaire, blindspot's domain handout, the pre-implementation plan page, quiz's interactive test, pitch's explainer, reflect's promotion checklist page. Three disciplines: (1) **the interaction loop must close** — the agent can't see what happens in the browser, so every interactive page ends with a "Copy results" button; choices only count once they're turned back into text and pasted into the conversation; (2) **write pages in ADHD format** — conclusion and next step in the first screen, numbered steps, lists grouped and layered (without dropping important information), details collapsed; (3) **format division of labor** — markdown for the always-loaded layer and files that need version diffing (SPEC, WORKFLOW, DECISIONS), HTML for what humans read and operate. (Source: Thariq, "The Unreasonable Effectiveness of HTML," claude.com/blog)

## The user's view: what you actually do

Across the whole flow you only ever do five kinds of things: state ideas, ask questions, make choices, approve/reject, and answer questions.

1. Kickoff (pick one): with the user-level `kickoff` skill installed, open `claude` in an empty folder and say "I want to build X" — missing scaffold files get created automatically, then spec drafting begins; or copy this template folder by hand and then say "I want to build X." From there: answer the starting questions, pick a direction, confirm the spec section by section, approve.
2. Say "interview me" first (one question at a time; say "I don't know" when you don't), then "scan for blind spots" if the domain is new (read the crash course + learn how to give instructions). Skip the blind-spot scan in familiar domains.
3. Say "start" → look at the first few items of this round's plan, say OK, let go. During work it only comes to you for "unknowns awaiting confirmation."
4. Say "quiz me" → read the change report, answer, deliver only on a perfect score; if others need to see the result, say "pitch" and get a shareable explainer.
5. **Open a new conversation** and say "reflect" → review the promotion/deletion list, approve or reject. This is the only step where you must remember to switch conversations.
6. Browse DECISIONS.md whenever you want to learn; pay special attention to the decision entries behind any quiz questions you got wrong.

## Suggested working loop

1. **Kickoff**: bring a rough idea and run `/kickoff` — the agent explores the materials, brainstorms scope options, and drafts SPEC.md (unknowns list included); you only react and revise. When the approach is undecided and you want to see how the industry solves it, run `/scout` in between.
2. **Before work**: run `/interview` to clarify the fuzzy spots question by question, then `/blindspot` to surface the angles you hadn't considered; answers flow back into SPEC.md. The agent derives this round's plan from the spec (big rounds become an HTML implementation-plan page); work starts only after you approve.
3. **During work**: the agent maintains notes/implementation-notes.md and DECISIONS.md automatically.
4. **Before delivery**: run `/quiz` for a change report + quiz; deliver only on a perfect score. If others need to see it and you need buy-in, follow with `/pitch`.
5. **After delivery**: open a new conversation and run `/reflect` — retrospective, rule promotion, archiving the working notes. (The order can't be flipped: reflect archives the notes, and quiz needs to read them.)

Advanced option: the "settle before compaction" rule in WORKFLOW.md relies on the agent's own diligence; for a hard guarantee, configure a PreCompact hook in Claude Code to force it.

## Sources

Architecture synthesized from: Thariq, "A Field Guide to Claude Fable 5: Finding Your Unknowns" (claude.com/blog — this template's blindspot / interview / implementation plan / implementation-notes / pitch / quiz all map to that article's unknowns patterns); OpenClaw's memory flush and Dreaming promotion system; Hermes's skill consolidation and capacity discipline.
