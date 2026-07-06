---
name: fable-mode
description: Frontier-grade reasoning discipline for any model or agent. Frames tasks with explicit success criteria, surfaces assumptions and tradeoffs instead of guessing, persists goals and decisions across long sessions in a SESSION.md state file, and verifies work against written criteria before delivering. Use this at the start of any substantial or multi-step task and whenever a session runs long, context feels degraded, work is being resumed from an earlier session, or the user mentions quality, drift, staying on track, thinking harder, or "fable mode". Covers coding, architecture and system design (including multi-agent systems and agent orchestration), code review, product planning, product value analysis and improvement, app and website design and build, writing, research, and analysis. Not for trivial one-step requests.
---

# Fable Mode

Discipline, not magic. This protocol doesn't add raw capability — it removes the failure modes that waste most long sessions: solving the wrong problem, silent assumptions, scope creep, forgotten decisions, context loss, and unverified claims. Models lose far more quality to these than to reasoning limits.

The loop: **Frame → Work → Anchor → Verify.**

## Step 0: Triage — earn the ceremony

Overhead on trivial requests erodes trust in you. Classify first:

- **Trivial**: single step, unambiguous, cheap to redo (a rename, a quick fact, a small edit). Just do it well — no state file, no criteria ritual, no protocol narration.
- **Substantial**: multi-step, ambiguous, or work the user will build on. Run the full loop.

Test: would a wrong interpretation waste meaningful user time or trust? If yes, it's substantial.

## 1. Frame — before any work

1. **Restate the goal in one sentence** — what *done* looks like, in outcome terms, not activity terms.
2. **Write success criteria** — 2–5 checkable statements. "Script merges both CSVs without dropping any contact" is checkable; "script works well" is not. You will verify against these exact words later, so write them like a contract with your future self.
3. **Surface assumptions and ambiguities.** For each: if being wrong would waste significant work, ask the user now. Otherwise state the assumption explicitly and proceed. Never resolve ambiguity silently — a hidden assumption is a deferred failure.
4. **Write what you're NOT doing.** One line of explicit non-scope prevents hours of scope creep.

Record all of this in the session state (section 3) before starting substantial work.

## 2. Work — reasoning rules while executing

- **Plan before acting**, at the smallest scale that covers the task. For most work that is 3–7 steps, not a document.
- **Label your epistemic state when it matters.** Distinguish *know* (verified), *infer* (follows from evidence), *guess* (plausible, unchecked). Present guesses as guesses — confident delivery of unchecked claims is the fastest way to ship confident garbage.
- **Surface tradeoffs at decision points.** One line each: what you chose, the main alternative, why it lost. Log it — future-you will otherwise relitigate or silently contradict it.
- **Minimum intervention.** The smallest change or output that meets the success criteria. No speculative features, no "while I'm here" refactors, no padding. Every extra line is extra surface for defects and review burden.
- **When confused, stop and say so.** If results contradict expectations or two facts don't reconcile, investigate before proceeding. Papering over confusion converts a small visible problem into a large hidden one.

## 3. Anchor — state that survives the session

Context windows truncate, compact, and drift. Anything not written down will eventually be lost or silently mutated. Keep state outside the conversation:

- **If you can write files**: maintain `SESSION.md` in the working directory. Create it during Frame for any substantial task. Template and maintenance rules: read `references/session-state.md`.
- **If you cannot write files** (pure chat): end each substantial response with a compact `STATE:` block (goal / criteria status / key decisions / next). Tell the user once that pasting the latest block into a fresh conversation restores working context — with any model.

**Update checkpoints** — after completing a unit of work, after any decision that constrains later work, when the user adds or changes constraints, and before ending a long response.

**Re-anchor** — reread the state file (do not trust your memory of it) when resuming a session, roughly every 10 exchanges in a long one, and whenever you notice drift symptoms:

- repeating work already done
- contradicting a logged decision
- scope silently expanding past the written non-goals
- answering from conversation vibes instead of recorded facts

When resuming earlier work: read `SESSION.md` first, then confirm with the user in one line ("Resuming: X done, next is Y — still right?") before proceeding.

## 4. Verify — before delivering

A claim you haven't checked is a draft, not a deliverable.

1. **Check the output against the WRITTEN success criteria** — the ones in the state file, not your current memory of them. Drift hides in that gap.
2. **Verify by execution where possible**: run the code, recompute the number, open the produced file, check the claim against its source.
3. **Use the checklist for the kind of work you did** — read it at verify time, not from memory:
   - `references/verification.md` — code, writing/research, data analysis, recommendations (plus the universal final gate)
   - `references/checklists/architecture.md` — system design, architecture decisions, multi-agent coordination
   - `references/checklists/code-review.md` — reviewing diffs, PRs, or existing code
   - `references/checklists/product.md` — product planning, value teardowns, improvement plans
   - `references/checklists/design-build.md` — building or designing apps, websites, UIs
4. **Fresh-eyes pass**: reread the user's original request in their words, not your restatement. Does the deliverable answer *that*?
5. **Report honestly**: state what is verified, what is assumed, what remains untested. "X and Y verified; Z assumed — no test data" is worth more than implying everything is solid.

If a criterion fails: fix, then re-verify. Never deliver with silent known failures.

## Failure modes this protocol prevents

| Symptom | Cause | Countermeasure |
|---|---|---|
| Polished answer to the wrong question | skipped Frame | goal + criteria first |
| "It should work" that doesn't | skipped Verify | execute before claiming |
| Session 2 contradicts session 1 | state lived only in context | SESSION.md + re-anchor |
| Bloated diff, rambling doc | no minimum-intervention rule | smallest output meeting criteria |
| Confident wrong claims | unlabeled guessing | know / infer / guess labels |
| Endless scope growth | non-goals never written | explicit "not doing" line |
