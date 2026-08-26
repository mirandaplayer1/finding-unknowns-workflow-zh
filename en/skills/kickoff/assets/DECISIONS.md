# Decision Log

> Purpose: don't just record "what was decided" — let the user learn "how to judge" by following along.
> Bar for logging: only decisions with two or more reasonable options; mechanical steps don't count.
> Filled in by the agent as work happens; new entries go on top.

## Format

```
## D-number | Date | One-sentence title

Situation: what problem came up, and why a decision was unavoidable
Options:
  A. ... — pros / cons
  B. ... — pros / cons
Decision: which one was chosen
Rationale: the key trade-off (under what condition this choice is the right one)
How to judge this yourself next time: one portable rule of thumb, so the reader can decide on their own next time this comes up
Status: active | superseded by D-XX
```

---

## D-000 | (Example) 2026-07-07 | Course material organized around "scenario tasks" rather than a "feature list"

Situation: the workshop material needed a narrative structure — most attendees are non-technical colleagues touching the tool for the first time.
Options:
  A. Walk through features one by one — complete and easy to look up later, but attendees won't remember "when to use which"
  B. Walk through tasks in three real work scenarios — engaging and immediately usable, but incomplete feature coverage
Decision: B, with a full feature overview as a linked appendix page
Rationale: the spec's acceptance criterion is "attendees can operate it on their own the next day" — memory runs on scenarios, not lists; the coverage requirement is handled by the appendix, so the main line doesn't have to be sacrificed.
How to judge this yourself next time: if the goal is "able to use it," choose scenario narrative; if the goal is "able to look it up," choose feature structure. When you need both, give the main line to the former and the appendix to the latter — never braid them into one thread.
Status: active
