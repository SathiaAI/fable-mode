# Architecture & system design (incl. multi-agent systems)

Frame the deliverable as a decision record: context → decision → consequences. A design without named consequences is a wish.

## Any architecture decision

- Name the quality attributes that actually decide this (latency, throughput, failure isolation, cost, operability, time-to-ship) and rank them. A design that optimizes an attribute nobody ranked is scope creep.
- Ask the boring-tech question first: what would this look like with the simplest proven tool? Depart from that baseline only for reasons you can write down.
- Steelman the rejected option in two lines. If your choice can't survive the alternative's best case, the decision isn't done.
- Name the flip conditions: what scale, requirement, or failure would reverse this decision.
- Walk one failure scenario end-to-end (component X dies mid-operation: what do users see, what recovers it, what data is at risk) before accepting the design. Hand-waving detector: "robust error handling" without a mechanism is a blank.

## Multi-agent / agent-OS specifics

- Choose the coordination topology explicitly — central orchestrator, peer handoff, or shared blackboard — and record why. Each fails differently: orchestrator = bottleneck/single point of failure; peer = loops and lost accountability; blackboard = write conflicts and stale reads.
- Define the state contract between agents: what is shared, where it lives, who may write it, and the schema. Agents communicating through vibes duplicate work and poison each other's context.
- Loop and runaway prevention is a mechanism, not a hope: hop counters, invocation budgets, cycle detection, or dedup keys — name one.
- Dead-agent recovery: how is a stalled agent detected, who retries, and is the retry idempotent?
- Attribution: every artifact and decision traceable to the agent that produced it, or debugging becomes archaeology.

## Verify before delivering

- Each ranked quality attribute is addressed or explicitly traded away.
- The failure walkthrough exists in the doc, not just your head.
- Flip conditions named. SESSION.md decisions logged.
