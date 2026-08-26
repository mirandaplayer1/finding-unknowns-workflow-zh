---
name: interview
description: Interviews the user to clarify ambiguities in the spec. Trigger when known unknowns remain after drafting the spec, when the spec has fuzzy areas, as a final confirmation before starting work, or when the user says "interview me", "ask me questions", or "help me clarify".
---

# Interview

Purpose: Turn "known unknowns" — the things the user knows they haven't thought through — into spec, one question and answer at a time. Division of labor with /blindspot: the blindspot pass finds problems the user isn't aware of; the interview handles ambiguity that has already surfaced.

## Steps

1. Read `SPEC.md` (especially the unknowns list) and the "unknowns to confirm" section of `notes/implementation-notes.md`, and list every ambiguity.
2. Order by impact: **ask first the questions whose answers would change the skeleton** (structure, audience, scope, definition of success); ask later the ones that only affect the flesh (wording, details, styling).
3. **Choose the interview format**:
   - **Three questions or fewer, needing follow-up probing** → conversation mode: ask one question at a time, and wait for the answer before asking the next.
   - **Four or more questions, or questions that compare options** → produce an "HTML interview questionnaire" (a single self-contained file, saved to `notes/`): each question comes with a note on "why this question matters and what the answer will affect", two to four option buttons plus a free-text field plus a "haven't thought this through yet" checkbox; at the bottom, a "copy answers" button that outputs the responses as structured text for the user to paste back into the conversation. When the answers come back, fill them into the spec question by question; questions marked "haven't thought this through yet" drop into conversation mode for stepped-down follow-up.
   - Shared principle for both formats: explain the reasoning behind each question (the user is learning how to decompose problems by following along); when the user can't answer, don't skip — step down a level, or mark it "pending prototype confirmation" and hand it to a throwaway prototype.
4. If new ambiguities surface during the interview, add them to the question queue, but cap the total at eight; more than that means it's time to go back and revise the spec first.
5. As each question reaches a conclusion, immediately fill it back into the corresponding section of `SPEC.md`; when the interview ends, update the status of the unknowns list and summarize for the user: what got clarified, what remains; then suggest running `/blindspot` to scan for aspects not yet noticed.

## Principles

- The interview exists to change the spec, not to chat; don't ask a question that can't yield an answer worth filling back in.
- Prioritize the questions where "a wrong answer is expensive": skeleton-level misunderstandings cost the most to fix late.
- If the user's answer contradicts what's already in the spec, point it out on the spot and decide together which one wins.
- Stop-loss: when discovering the remaining unknowns during implementation is cheaper than asking now, stop the interview and say so — mark them "pending implementation verification" in the unknowns list; don't ask every question just because you can.
- All HTML output follows WORKFLOW.md "HTML output and interactive interfaces": embedded comment layer + "copy results" exit (ready-made snippet: `notes/html-comment-layer.html`).
- This skill ends at "fill back the spec, summarize, wrap up": no implementation without the user's request.
