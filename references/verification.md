# Verification checklists by domain

Pick the section matching the deliverable. Universal rule: verify by *doing*, not by *rereading* — execution finds what inspection misses.

## Code

- Run it. If you cannot run it in this environment, say so explicitly in the delivery.
- Test the boundaries the task implies (empty input, duplicates, case differences, malformed rows, unicode). Generate small fixture data if none was provided.
- Check the failure path: what happens on bad input? Silent wrong output is worse than a loud crash.
- Diff review: every changed line traceable to a success criterion. Lines that aren't → revert (minimum intervention).
- If it will run unattended (cron, CI, handed to a team): verify the operator experience — clear error messages, non-zero exit on failure, no interactive prompts.

## Writing & research

- Every factual claim gets a label: know / infer / guess. Upgrade by checking, or keep the label in the delivery.
- Numbers, dates, names, quotes: check each against its source. Never fabricate a citation — an honest "from general knowledge, uncited" beats a fake source.
- Contradiction sweep: does any paragraph contradict another? Common after long sessions.
- Constraint check: length, format, audience, tone — reread the user's stated constraints and measure; don't estimate.

## Analysis & data

- Recompute at least one headline number a second, independent way.
- Sanity-check magnitudes: does the result survive a "does this number even make sense" pass?
- State the data's limits: sample size, timeframe, what it cannot show.
- Separate observation from interpretation in the delivery.

## Plans & recommendations

- The recommendation must trace to the stated criteria — if cost-sensitivity was the constraint, cost must be quantified, not vibed.
- Steelman the rejected option in a line or two. A recommendation that can't survive the alternative's best case isn't done.
- Name the conditions under which the recommendation flips.

## Universal final gate

1. Each criterion in SESSION.md checked, with evidence.
2. The user's original request reread, in their words. Answered?
3. Delivery states: verified / assumed / untested.
