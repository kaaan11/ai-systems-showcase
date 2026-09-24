# SlopLab

**An adversarial testing framework for vulnerability-report triage evaluators.**

> Private implementation · MIT-licensed codebase.

SlopLab measures one question:

> When a triage system receives a technically valid report that has been
> degraded with missing evidence, inflated impact, or fabricated detail, does it
> still classify the report consistently?

As vulnerability-report pipelines increasingly use automated triage, a useful failure
mode to test is not only whether a system can recognise a report, but whether controlled
degradation can move its verdict.

## What it does

- Loads Markdown vulnerability-report fixtures with structured manifests.
- Applies controlled, traceable mutations.
- Runs pluggable evaluators through a normalised contract.
- Measures how each mutation changes the evaluator's decision.
- Produces reproducible benchmark artifacts.

## What it deliberately does not do

- No scanning or interaction with real targets.
- No working exploit generation.
- No bug-bounty submissions.
- No claim that a specific triage product is weak unless that product is actually run
  and the run is published.

## Why it is still in the showcase

SlopLab is useful as a release-oriented benchmark project: the emphasis is on a committed
corpus, explicit mutation operators, a threat model, reproducible outputs, and a
deterministic baseline rather than on a demo-only prototype.

The implementation repository is currently private. Older showcase text that described
it as public was stale and has been corrected here.

*Repository visibility checked 2026-09-24.*
