---
name: scout
description: Competitor / product research — analyzes how others solve the same problem in order to make a decision, producing an HTML report with screenshots and a judgment framework. Trigger when the spec has several approaches still undecided, when building a new feature and wanting to know how the industry solves it, or when the user says "competitor research", "competitive analysis", "find competitors", "how do others do this", "check Mobbin for references", or "product research". Not for hunting visual inspiration, and not for looking up what a particular screen in a particular product looks like.
---

# Scout

Purpose: **Find the assumption behind a design, then test whether that assumption holds in our context.**

Not to look at what others look like. A descriptive feature-comparison table can't drive a decision, because it doesn't explain why. Only conclusions that carry assumptions, applicability conditions, and failure scenarios can be argued against — and tied back to our own spec for testing.

**Whether to use this skill**: You have a spec or requirement in hand, and several approaches are still undecided → use it. Hunting for layout or visual inspiration → don't; that's a different activity. Wanting to know what some screen in some product looks like → that's a lookup; just search.

## Steps

1. **Read the material, place the references**
   Read the spec (Notion / SPEC.md / ticket) and any screenshots or links the user provided. Identify — out loud, on the spot — which product a screenshot shows: the user often doesn't know what they pasted, and that image's role will steer the entire search direction.

2. **Ask before searching — searching without asking is the biggest waste**
   The cost of searching in the wrong direction far exceeds the cost of four questions. Ask them all in one AskUserQuestion call, and give every question a "this is exactly what I want to see how competitors solve" option, so the user can throw the question back to the research:
   - What role does the reference you provided play? (build it like this / just an example, find something better / I want to know whether this is any good) — these three lead to completely different searches.
   - Which undecided spot in the spec should this research answer? Research without a target turns into generalities.
   - Who is the user — and who is it **not**? One sentence of "who it's not" deletes an entire class of irrelevant competitors.
   - Platform scope and hard constraints? (desktop / mobile / both, count limits, whether the backend can play along)

   **When to switch to `/interview`**: if the answers reveal the fuzziness lives at a deeper level — the user themselves can't articulate whose problem they're solving, or the requirement is really several sub-projects that should be split, or three of the four questions come back "not sure" — stop, and run `/interview` first to settle the skeleton layer; don't go searching while fuzzy. A report searched under fuzziness looks rich but yields not a single usable conclusion.

3. **Work in parallel: bare derivation + multi-angle search + existing-code inventory**

   **Bare derivation (write it before the search starts — this is the anti-copying foundation)**: Pretend there are no competitors to look at, and write three to five lines of "how we would reason through this problem ourselves" from our spec, hard constraints, and the job the user is trying to get done. This first-principles baseline must never be deleted — competitor material may only **correct** it (which assumption was wrong, which constraint was missed), never replace it. Search first and derive later, and the cases will anchor you: the whole report ends up starting from "what others built" instead of "our problem".

   **Search**: Split the same requirement into at least four to six angles and search each separately; don't throw the whole requirement in as one query. Generic angle types —
   - Entry point (where this capability gets invoked from)
   - State presentation (how "enabled / in progress" is made visible)
   - Long-running or async behavior (how things that take a long time are handled)
   - Invocation and input methods (slash, mention, keyboard shortcut)
   - Progress and result display (how the system reports what it did)
   - Narrow-screen degradation (what mobile sacrifices first)
   - Permissions and settings source (who decides what users can use)

   Tool division (requires the [Mobbin](https://mobbin.com) MCP connector; when it isn't installed, fall back to web search plus screenshots from product sites and review articles — the rest of the steps stay the same): `search_screens` for single screens, `search_flows` for multi-step flows, `search_sections` for website sections. Search desktop and mobile separately; don't assume mobile is desktop shrunk down. **Explicitly ask for cases that contradict each other** — total agreement means you've only found the convention, and convention tells you what's common, not why.

   **Code inventory** (do it whenever there's a repo — this is the step most easily skipped): In parallel, dispatch an Explore agent to inventory the existing code, requiring an "already exists / net new" comparison table as output. This step often flips the conclusion from "build the whole thing" to "most of the parts already exist", directly changing the scope assessment. Without it, the report stops at "how others do it" and never reaches "how much we should build".

4. **Build the judgment framework — before writing the report**
   Once the material is collected, produce three things before writing any section:
   - **The one-sentence problem**: what are these products actually solving for the user? (e.g. "not a settings problem — an expectation-calibration problem")
   - **Mental models**: the two to four ways users might imagine this problem, and their axes of divergence (e.g. "who decides" and "scope of effect"). Draw it as one diagram.
   - **Journey moments**: slice the experience into moments; for each, mark the question in the user's head, and whether we can currently answer it.

   ⚠️ **Re-derive the mental models every time.** Last time's set grew out of last time's problem; new problem, new set. Reusing the old ones is where this skill breaks most easily.

5. **Place the cases into the framework**
   Every approach gets the same three-line annotation:
   - What it assumes is going on in the user's head
   - Where in the journey it speaks up
   - How it breaks when the assumption fails

   There is no absolute better or worse in design. An approach holds only when "the mental model it assumes" matches "the one our users actually hold". Every conclusion must come with "under what conditions to switch to the other approach".

   Cases are **evidence about assumptions**, not a menu of options: the report may not contain "do what X does"-style conclusions — only "X bets on assumption P; P holds / does not hold in our context, and the evidence is …". An approach becomes a direction only after its assumption survives the test; what can't be tested gets labeled "unverified".

6. **Counterexample pass (mandatory before delivery — don't wait to be asked)**
   Take your strongest, most settled-looking conclusion and actively hunt for counterevidence: does any product deliberately do the opposite? How do they handle the problems you listed? If no counterexample turns up, state which directions you searched — **failing to find one does not count as confirmation**. The most fragile part of the report is usually the "everyone does it this way, so it must be right" passage — and it reads as the most persuasive.

   Run two checks at the same time:
   - **Label observation vs. inference separately.** Mobbin provides static screenshots; inferring dynamic or temporal behavior from a single image ("the input box is locked while it's running") is actually speculation. Competitor research is where the rule "a single steady-state screenshot cannot support temporal inferences" gets violated most easily, because all the material is static.
   - **Falsifiability.** Pick a conclusion at random and ask "what fact would it take to overturn this?" If there's no answer, that passage has no content — rewrite it.

7. **Produce the report**
   A single HTML file saved in the project's `docs/`, skeleton from `assets/report-skeleton.html` (four block types: framework blocks, case cards, direction cards, edge-case checklist). The skeleton defines only styling; **the section structure is determined by the problem — don't copy the previous report's outline**.

   Every report embeds the **comment layer** + a footer "copy all feedback" exit: use the ready-made snippet `assets/html-comment-layer.html`, embedded per the three steps at the top of the snippet. The reader's per-section feedback is the most valuable thing this research brings back; no comment box means throwing it away.

   Screenshot rules:
   - Always download into a same-named `-assets/` folder. Source URLs are short-lived; hotlinking will rot.
   - Every image clicks through to its original source.
   - Images must be large enough to read the interface text; beyond two columns you start sacrificing detail — widen the layout instead.

   Required content: judgment framework first; every section leads with its conclusion; three directions from "embarrassingly small" to most complete, with pros/cons and a recommendation — **the first line of every direction card must be "the assumption it bets on + the result of testing that assumption in our context" (citing our spec or our users' evidence); competitor cases may appear only from the second line on, as supporting evidence — "product X does it this way" is not a reason**; an edge-case checklist (count limits / truncation / empty states / insufficient permissions / mid-flight cancellation / state conflicts); the existing-code comparison table; and a **search log** (which angles were used, how many screens were scanned, which directions were discarded).

8. **Pre-delivery self-check**
   - Are there cases that contradict each other? Total agreement means the search was too narrow.
   - How many "but", "unless", "not applicable when"? Zero means collection without judgment.
   - Does every approach have its three-line annotation?
   - Was the counterexample pass done?
   - The word scan is only a symptom check: if "copy", "replicate", "worth copying" show up, the reasoning chain in that passage is broken — swapping the word doesn't fix it. Every recommended direction must be able to answer three questions — what assumption does it bet on? Why do we believe that assumption holds in our context? What evidence would overturn it? Directions that can't answer get deleted, or explicitly downgraded to "unverified".
   - Is the bare-derivation baseline still in the report? Say exactly which of its lines the competitor material corrected — a baseline with zero corrections means the search brought back no information; a baseline discarded wholesale means the cases anchored you.
   - Are all screenshots local, all clickable back to their original source, all with legible text?
   - Was it actually opened in a browser? (When verifying via screenshot, first confirm the scroll position is at the top or use a full-page capture — otherwise you'll capture the blank area below the content and misjudge the page as broken)

9. **Hand off**
   After the report is delivered, the user picks a direction. Once picked:
   - Needs a spec → `/kickoff` (this report's direction comparison and edge-case checklist are exactly the material for kickoff step 4 and the unknowns list)
   - Edge-case items that need the user's call → `/interview`

## Principles

- **Ask before searching.** Four questions cost far less than a search in the wrong direction.
- **Hunt contradictions, not consensus.** Conflicting cases carry information; agreeing cases are just convention.
- **Re-derive the mental models every time.** The old set is the product of the old problem.
- **Static material cannot support inferences about dynamic behavior.** When you infer, label it as inference.
- **Conclusions must be falsifiable.** A sentence that can't be argued against says nothing.
- **Competitors are an evidence base for assumptions, not a menu of solutions.** Conclusions are derived from "our problem + assumptions that survived testing"; competitors are cited only as evidence, never as the reason.
- **Describing others is not the goal.** Every passage must be able to answer "so what should we build, and why".
