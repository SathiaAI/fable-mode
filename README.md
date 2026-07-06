# fable-mode

**Frontier-grade reasoning discipline for any LLM agent — in one portable Markdown skill.**

Most agents don't fail long sessions because they aren't smart enough. They fail because they solve the wrong problem, resolve ambiguity silently, let scope creep past what anyone asked for, lose state when the context window rolls over, and deliver claims nobody verified. fable-mode is a protocol that removes those failure modes. It doesn't add capability — it stops capability from leaking away.

## The loop

**Frame → Work → Anchor → Verify**

1. **Frame** — restate the goal in outcome terms, write 2–5 checkable success criteria, surface every assumption (ask if being wrong is expensive, state it and proceed if not), and write down what you are *not* doing.
2. **Work** — plan at the smallest sufficient scale; label every claim *know / infer / guess*; log each decision with the alternative it beat; make the smallest change that meets the criteria; stop and say so when confused.
3. **Anchor** — keep state outside the conversation in a `SESSION.md` file (goal, criteria, decision log, open questions, done/next). Re-read it on resume and on a drift symptom — repeating work, contradicting a logged decision, scope quietly expanding. In file-less chat environments, a compact `STATE:` block at the end of each response does the same job: paste it into a fresh session with *any* model and the work continues.
4. **Verify** — check the deliverable against the *written* criteria (not your memory of them), verify by execution wherever possible, re-read the user's original words, and report honestly what is verified / assumed / untested.

A triage gate keeps all of this away from trivial requests — ceremony on a rename erodes trust, so the protocol only engages when a wrong interpretation would cost real time.

Domain checklists load on demand for the work you're actually doing: **architecture & multi-agent systems**, **code review**, **product planning & value analysis**, **app/site design & build**, plus generic code / writing / analysis verification.

## Does it work?

Developed with with/without-skill benchmarking on identical tasks (Claude Sonnet runner; single runs per configuration — directional, not statistical):

| Round | Tasks | With skill | Without |
|---|---|---|---|
| 1 | Generic (data script, tech recommendation, trivial-task triage) | 16/16 | 13/16 |
| 2 | Domain (code review w/ planted defects, multi-agent architecture, product teardown, session hand-off) | 24/25 | 20/25 |
| 3 | **A real merged production PR** (~1,000 lines, written by an AI build agent, merged green) | 7/7 | 4/7 |

The interesting deltas weren't the scores — they were behavioral. With the skill: judgment calls flagged to the user instead of decided silently; a dedicated "when this recommendation flips" section; file:line evidence throughout a review whose baseline counterpart had none; and on the real PR, a scratch harness that *executed* the code's claims — confirming its math, timing its clustering hot path, self-correcting one suspected bug before reporting it, and catching that the build log's test count was off by one. The skill-guided review of the real PR surfaced issues the CI gate had merged past: an audit ledger that was written but never consulted, a missing authorization layer, and schema assumptions asserted three times and checked zero.

Honest caveats, because the skill would demand them: some assertions (does `SESSION.md` exist?) structurally favor the skill; the session-resume test telegraphed the interruption, and the baseline improvised a decent hand-off when warned — the skill's edge is that state exists *by default*, unwarned; and cross-vendor validation (GPT, Gemini) hasn't been run yet, though the skill contains nothing vendor-specific.

## Install

**Claude (Cowork / claude.ai):** import the skill via Settings → Capabilities, or package the folder as a `.skill` zip and use *Save skill*.

**Claude Code:** drop the `fable-mode/` folder into `.claude/skills/` in your repo (or `~/.claude/skills/` globally).

**Cursor / Codex / Gemini CLI / anything with a rules file:** put the folder in your repo and point the agent at it — one line in `.cursorrules`, `AGENTS.md`, or `GEMINI.md`: *"Read and follow fable-mode/SKILL.md for any substantial task."*

**Plain chat, no filesystem:** paste `SKILL.md` into the system/first message. The skill's `STATE:` block fallback is designed exactly for this.

## Structure

```
fable-mode/
├── SKILL.md                     # the protocol (~80 lines — read this first)
├── references/
│   ├── session-state.md         # SESSION.md template + maintenance rules
│   ├── verification.md          # generic verification: code, writing, analysis, recommendations
│   └── checklists/
│       ├── architecture.md      # system design + multi-agent coordination
│       ├── code-review.md       # adversarial review discipline, no-fabrication rules
│       ├── product.md           # value teardowns, impact×effort×confidence, kill criteria
│       └── design-build.md      # UI acceptance criteria, verify-in-the-medium
└── evals/evals.json             # the benchmark prompts this skill was developed against
```

## When *not* to use it

Trivial, single-step, cheap-to-redo requests. The skill says so itself — its first instruction is a triage gate, because a protocol that turns "rename this function" into a ceremony is a protocol you'll turn off.

## License

MIT
