# AI-OS

**A model-agnostic governance and execution layer for AI-assisted project work.**

> Private · released baseline; current development tree continues beyond the baseline.

AI-OS defines what an AI-assisted project may treat as durable truth, what requires
human authority, and how model-backed execution is allowed to interact with project
state.

Its core idea is simple: execution approval and persistence approval are different
decisions.

## Current system

The current development line includes:

- seven structured record families: Task, Question, Decision, Investigation,
  Evidence, Handoff, and Report
- a nine-condition persistence gate
- content-bound persistence authorization
- deterministic project/context loading
- Task creation, inspection, validation, and explicit lifecycle handling
- read-only preflight through `aios explain` and `aios run --dry-run`
- governed execution through `run` / `continue`
- an opt-in multi-agent DAG workflow
- model/API and native CLI worker paths
- strict ruleset-version matching that fails closed on incompatible project state

The base governance and record layer is intentionally separable from heavier execution
dependencies.

## The authority boundary

A run being authorized does **not** mean its output may become durable project truth.

Durable writes require a separate authorization bound to the exact content. Task state
changes and other governance transitions remain explicit operator actions rather than
being inferred from model output.

## Why this matters

AI-assisted development can fail in subtle ways when temporary model output quietly
becomes accepted project fact. AI-OS makes that transition visible and auditable.

It also tries to keep model choice replaceable: governance rules live in vendor-neutral
documents and adapters, not in one provider's prompt format.

## What it does not claim

- no fully autonomous project governance
- no implicit permission to persist whatever a worker produces
- no automatic provider fallback or hidden routing
- no claim that every future package in the architecture is already wired

The project is best understood as a governed execution and record system with explicit
human authority, not as a general autonomous-agent operating system.

*Source status checked 2026-09-24.*
