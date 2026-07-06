# App & website design and build

Code that compiles is not a UI that works. The medium is the browser/device, so verification happens there — never declare a UI done from reading its source.

## Before building

- Acceptance criteria per screen or flow, written first: "user can X, sees Y within Z, error case shows W". These become your Verify list.
- Reuse before invention: existing tokens, components, spacing/type scale. New one-off styles are design debt; justify each.

## While building

- Build the real states, not just the happy path: empty, loading, error, long/overflow content, and (where relevant) unauthenticated. Most "bugs" users hit are unbuilt states.
- Responsive from the start: check the narrowest target width as you go, not as a final patch.
- Keyboard reachability and readable contrast are baseline, not polish.

## Verify before delivering (in the medium)

- Open it. Click the entire primary flow from a fresh load — every acceptance criterion, checked in the running artifact.
- Resize through breakpoints; feed a too-long string; trigger the error state deliberately.
- Console clean (no errors), obvious performance sanity (image sizes, bundle not absurd).
- If you cannot render it in this environment, say so explicitly and list exactly which criteria remain unverified — do not imply visual correctness you haven't seen.
- SESSION.md current: acceptance criteria checked off with how each was verified.
