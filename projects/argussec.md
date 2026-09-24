# ArgusSec

**Evidence-first LLM and AI-security research workbench.**

> Private, in development.

ArgusSec is the layer that asks a different question from a scanner:

> What would count as evidence that a security hypothesis was actually falsified?

It is designed to organise AI-security research around explicit hypotheses, reproducible
experiments, typed evidence, and human approval rather than around a flat list of scanner
matches.

## Current development line

The private development line includes:

- first-class research hypotheses and security invariants
- multi-principal experiment concepts for tenant/session/identity boundaries
- a directed evidence graph with provenance and cryptographic hashes
- normalized ingestion from tools such as BackFlowFuzz and MCP Guardian
- an exploitability ladder from pattern-level evidence to stronger boundary proof
- patch-differential and fix-validation workflows
- suggested cross-tool investigations that require human acceptance
- reproducibility statistics for deterministic and probabilistic experiments

## Why candidates stay separate

ArgusSec deliberately avoids silently merging scanner outputs into one "confirmed"
finding. Independent candidates remain independent evidence until a researcher accepts
the relationship between them.

The same rule applies to validation state: a static pattern, a reachable path, a triggered
behaviour, and a demonstrated cross-boundary impact are different evidence levels.

## What this does not prove

Listing ArgusSec here does **not** claim that:

- it has discovered a vulnerability in a named external target
- every planned workflow has been validated end to end
- a scanner candidate is equivalent to a validated finding
- a research-opportunity score is a vulnerability-severity score

The showcase documents the workbench architecture and implemented research machinery,
not a blanket claim about external security results.

*Source status checked 2026-09-24.*
