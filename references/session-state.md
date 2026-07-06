# SESSION.md — template and maintenance rules

Keep it short. This file is working memory, not documentation — if it takes more than a minute to update, it will stop being updated. Target under ~60 lines; prune aggressively. Superseded entries get deleted, not accumulated (except Decisions — see rules).

## Template

```markdown
# SESSION — <short task name>
Updated: <date or step marker>

## Goal
<one sentence, outcome terms>

## Success criteria
- [ ] <checkable statement>
- [ ] <checkable statement>

## Not doing
- <explicit non-goal>

## Decisions
<!-- newest first; one line each -->
- <decision> — <why> — <rejected: alternative>

## Assumptions & open questions
- ASSUMED: <assumption> (flag to user if it becomes load-bearing)
- OPEN: <question awaiting user answer>

## State
Done: <compact list>
Next: <the single next action>
Blocked: <what and why, or "nothing">
```

## Rules

- **One file per task/project**, at the root of the working directory. If a SESSION.md already exists there, read it before writing anything — it may be earlier state of this same work.
- **Decisions are append-mostly.** Never silently reverse a logged decision. If a decision changes, log the reversal and the reason — that line is what prevents flip-flopping across a long session.
- **Criteria change only with the user.** They are the contract. If the goal shifts mid-session, update the criteria explicitly and record the change in Decisions.
- **"Next" is exactly one action.** A list of possible next steps is planning; one concrete next step is state.
- **On resume**: read this file before any other context, confirm with the user in one line, then proceed.

## No-filesystem fallback (pure chat)

End substantial responses with:

```
STATE: goal=<...> | done=<...> | next=<...> | decisions=<key ones> | open=<...>
```

Tell the user once: pasting the latest STATE line into a new conversation restores working context with any model.
