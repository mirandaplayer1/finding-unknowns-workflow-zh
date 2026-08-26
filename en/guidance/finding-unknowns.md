# Finding Unknowns — Single-File Lite Version

Don't want to install skills? Paste the whole block below into your project's `CLAUDE.md` for a passive version of this workflow. For the full version (interactive questionnaires, quizzes, file templates), install the [skills](../skills/).

---

## Find the unknowns first, then start work

The bottleneck on work quality is "the gap between instructions (the map) and reality (the territory)." Before starting, lay the unknowns out:

- **Known knowns**: write them into the spec.
- **Known unknowns**: what I know I haven't thought through — interview me one question at a time. Ask first about answers that would change the skeleton (structure, audience, scope), details later. When the remaining unknowns become cheaper to discover during implementation, stop the interview and say so.
- **Unknown knowns**: what I took for granted and never wrote down, but would recognize if done wrong (taste, conventions) — use disposable prototypes or multi-direction comparisons to draw my reaction; label each direction with the belief it's betting on.
- **Unknown unknowns**: what I never considered at all — proactively scan domain conventions, common pitfalls, and audience expectations, each with an actionable fix attached. "No major blind spots here" is also a valid result — don't force it.

## Working rules

1. The spec is the single source of truth: no work starts until I have approved the spec; when spec and reality conflict, update the spec first, then the deliverables.
2. Every decision with two or more reasonable options gets recorded: the options, the trade-offs, and "how to judge this yourself next time."
3. Off-plan situations: pick the conservative (reversible) option, log the deviation, keep moving — don't stall waiting for me.
4. Before delivery, quiz me with five to eight questions (why A over B, edge cases, if this changes what else must move); deliver only when I get them all right. On a wrong answer, diagnose first: is it a gap in my understanding, or is the thing built too convoluted and due for simplification?
5. After delivery, run a retrospective in a new conversation: only lessons of the same kind that appear two or more times get promoted into standing rules; proactively propose deleting stale ones.

---

Method source: Thariq Shihipar, "A Field Guide to Claude Fable 5: Finding Your Unknowns" (claude.com/blog).
