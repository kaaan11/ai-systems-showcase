# Partitür

**Multi-model orchestration with frozen outcomes and evidence-bound verification.**

> Private, in development.

A *partitür* is a score: the thing every player works from and the thing the final
performance is judged against.

The project applies that idea to AI-assisted engineering. The planner writes the intended
outcomes before implementation starts, those outcomes are frozen, workers execute against
them, and later stages must produce evidence against the same frozen score.

## The binding rule

The auditor does not issue a vague `PASS`.

For each outcome it can report only:

- `PROVEN(evidence-ref)`
- `UNPROVEN`

Evidence references must resolve to concrete material such as version-controlled
file/line references, test identifiers, or command logs.

## Current workflow

The current development line includes:

1. planning and frozen outcome contracts
2. parallel workers in isolated workspaces
3. merge gating
4. evidence-bound audit
5. differential verification against before/after states
6. correction rounds bound to the original frozen score
7. a test-engineer / breaker stage for searching for regressions beyond the promised outcomes
8. workflow and authority preflight surfaces

The repository currently records F7 and campaigns 02→05 as completed.

## The score does not move

A correction round may change the implementation plan, but it may not rewrite the promised
outcomes or their score digest.

Only work that remains unproven is eligible for correction. Correction loops are bounded;
running out of attempts leaves the remaining outcomes `UNPROVEN`.

## Differential evidence

A test passing after a change is not enough by itself.

For an audit test to count as evidence of the change, the project can require it to fail on
the pre-change state and pass on the post-change state. Passing on both sides means the test
did not demonstrate the claimed outcome.

## Breaker / test-engineer boundary

The breaker asks a different question from the auditor: **what else did this change break?**

It does not produce `PROVEN` / `UNPROVEN` verdicts and cannot rewrite the frozen score.
Executable commands come from a human-declared charter and are run without a general shell.

## What it does not claim

- the frozen score guarantees that the original specification was good
- a green implementation test automatically proves an outcome
- zero breaker findings means the system is secure
- correction rounds may redefine success after the work begins
- the tool has unrestricted shell or write authority

The project is designed to make specification, implementation, verification, and
regression search separate stages rather than one model grading its own work.

*Source status checked 2026-09-24.*
