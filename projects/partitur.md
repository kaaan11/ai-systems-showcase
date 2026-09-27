# Partitür

**Multi-model orchestration with a frozen outcome contract and an
evidence-bound audit.**

> Private, in development.

A *partitur* is the full score of a piece: every part written under every other,
the thing the conductor reads and each player takes their line from — and the
document against which "was it played correctly" is answered.

Agent frameworks have a conductor. None of them has a score. That is the gap
this project addresses.

## The shape

```
directory → planner model → conversation → human approval
  → PLAN-*.json  (tasks + OUTCOMES written, then frozen)
  → dispatcher: parallel workers, isolated workspaces
  → reviewer + merge gate
  → AUDITOR: find evidence for each outcome → report
  → human → planner: correction round, bound to the same score
  → auditor clean → BREAKER: run it, try to break it
```

## The binding rule

The auditor cannot say `PASS`. It may only say:

- `PROVEN(evidence-ref)` — where evidence is a `file:line`, a test identifier,
  or a command log, and the reference must resolve in version control
- `UNPROVEN`

There is no third value, and no partial credit. An outcome too large to answer
as a binary must be split when the plan is written — deliberate pressure on the
planner rather than a gap.

## Two ideas worth naming

**The score does not move.** A correction round may change *how* the work is
done and never *what was promised*. The outcome list is hashed at freeze time;
a correction proposal that touches the outcomes is rejected whole rather than
filtered. Editing the claim after failing the exam is changing the question.

**The differential gate.** A passing audit test is not proof that it measures
anything. So every audit test runs twice: against the state *before* the change
and *after*. Fail-then-pass is `PROVEN`. Passing on both sides means the test
does not measure the outcome, and the verdict is `UNPROVEN`.

## Measured state

- 1,321 tests collected; default run: 1,311 passed, 10 skipped.
- Governance record layer consumed as a library from AI-OS; operational data
  kept in a separate namespace so that record schemas are never invented.
- The breaker executes only commands a human declared in a charter file, matched
  on an exact argument-vector prefix, with no shell.

*Figures taken on 2026-09-27 at commit 9362cb7 (origin/master).*

## Its first real campaign failed

Partitür was pointed at its own engine and asked to change a policy in it. The
result: **all three outcomes ended `UNPROVEN`**, the merge was refused, and the
measurement the campaign rested on was falsified by the campaign's own logs.

The full account, including the six defects it found in itself and the three
specification mistakes that shaped it, is
[here](../examples/failed-campaign.md).

## The audit-test proposer is now connected

`partitur audit` can load proposals from a file or ask a named model to propose
tests. Each proposal still has to pass the differential gate before it can
support a verdict.
