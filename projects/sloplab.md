# SlopLab

**An adversarial testing framework for vulnerability-report triage evaluators.**

> Public · MIT (corpus CC0-1.0) · CI + tagged releases ·
> [github.com/kaaan11/sloplab](https://github.com/kaaan11/sloplab)

SlopLab measures one question:

> When a triage system receives a technically valid report that has been
> degraded with missing evidence, inflated impact, or fabricated detail, does it
> still classify the report correctly?

As bug-bounty and vulnerability-report pipelines start leaning on automated
triage, the failure mode that matters is not "does it find bugs" but "can it be
talked out of a correct verdict". SlopLab degrades good reports on purpose and
measures how far a verdict moves.

## What it does

- Loads Markdown vulnerability-report fixtures with structured manifests.
- Applies controlled, traceable mutations — 12 deterministic operators in V1.
- Runs pluggable evaluators through a normalised contract.
- Measures how much each mutation degrades the triage decision.
- Produces reproducible JSONL / CSV / Markdown benchmark reports.

## What it deliberately does not do

- No scanning, attacking, or interaction with real targets.
- No working exploit generation and no bug-bounty submissions.
- No "is this report true" verdicts — only **evaluator consistency**.
- No network access, API key, or model required to run the tests or the
  benchmark.

## Why it is the most finished thing here

It is the only project in this showcase that has left development discipline
behind and taken on release discipline: a committed corpus with a dataset card,
a documented threat model and safety boundary, continuous integration, tagged
releases, and a deterministic rules baseline so that a benchmark run does not
require a model at all.

## Measured state

- 62 test files; deterministic benchmark suite runs offline.
- Committed corpus of 60 fixture files covering 52 logical reports.
- V1 benchmark suite: roughly 297 cases against the rules baseline.

*Figures read from the repository on 2026-09-08.*

## What is not claimed

SlopLab does not claim that any particular triage product is weak. It provides
a harness and a baseline; a claim about a specific evaluator would require
running that evaluator and publishing the run, which has not been done here.
