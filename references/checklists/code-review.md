# Code review

Read the diff twice: once for intent (does it do what it claims), once adversarially (how does it break). One pass does neither well.

## Hunt list (adversarial pass)

- Security: injection (SQL/command/path), authz on every new endpoint, secrets in code, unvalidated redirects/inputs at trust boundaries.
- Correctness: edge cases (empty, one, max, duplicate), off-by-one at boundaries and pagination, error paths (what happens when the call fails — swallowed exceptions are defects, not style), concurrency around shared state.
- Performance: N+1 queries, unbounded loops/fetches, work inside loops that belongs outside.
- Tests: do they exercise the changed behavior, or only pass around it? A green suite that never enters the new branch verifies nothing.

## Report discipline

- Every finding: severity (blocker / should-fix / nit) + file:line evidence + a concrete fix. Never mix unlabeled nits with blockers — the author can't tell what gates the merge.
- Do not fabricate findings to appear thorough. A short review with evidence beats a padded one; "this section is clean, checked for X and Y" is a legitimate finding.
- Verify claims by execution where possible: run the tests, run the linter, actually trigger the suspicious path. A suspected bug you confirmed is a report; one you didn't is a guess — label it.
- Say what you did NOT review (files skipped, behavior untestable here) so silence isn't mistaken for approval.

## Verify before delivering

- No runnable test suite is NOT "no execution": extract the pure functions you are judging into a scratch harness (node/python) and execute the claims you are about to assert. A proven merge-risk beats a "very plausibly" — and a disproven one saves the author a false alarm.
- Each blocker reproduced or reasoned to a concrete failure input.
- No finding contradicts another. Severity labels present. Un-reviewed areas listed.
- SESSION.md exists and is current — a review that gates a merge is substantial work; its criteria and decisions belong in state like any other. (Field note: this is the step most often skipped on review tasks.)
