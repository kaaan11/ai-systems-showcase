# AI Systems — Showcase

A portfolio of cybersecurity, AI-security research, and orchestration systems built over 2026.
The code often lives in separate repositories. What lives here is **what was built,
what was verified, and — with equal prominence — what has not been verified yet.**

## What I work on

I build and study systems at the intersection of cybersecurity, AI security, and
evidence-driven software engineering.

Current focus:

- security testing for LLM and MCP systems
- reproducible AI-security research
- multi-model engineering and verification workflows
- defensive security automation

> **The one rule of this showcase:** no number appears here unless it was
> measured. Anything unmeasured is labelled as such. A project's failed attempt
> is as visible as its successful one.

## AI-assisted development

Claude Code is one of the tools I use in a broader **multi-model engineering workflow**.
I use different models for implementation, research, critique, and independent review,
while tests, explicit acceptance criteria, and human verification determine whether a
change is accepted.

The point of the workflow is not to attribute a project to a single model. It is to make
AI-assisted work inspectable: tasks are bounded, claims are checked at the source, and
important changes are verified before they become project truth.

**[How these systems were built](docs/ai-workflow.md)** documents the full method:
specification, delegation, independent verification, mutation proof, and record keeping.

## Read this first

**[Verification principles](docs/verification-principles.md)** — the claim these
projects share. Each principle is traced to the measurement that produced it,
not stated as a preference.

**[How these systems were built](docs/ai-workflow.md)** — the working method:
specification, delegation to models, independent verification, mutation proof.

## Featured research & systems

| Project | What it does | Status |
| --- | --- | --- |
| [LLM Security–Usability Benchmark](projects/llm-security-usability-benchmark.md) | Pre-registered pilot on how conversational context changes risk interpretation for the same final prompt | Human QC in progress; **no model results yet** |
| [MCP Guardian](projects/mcp-guardian.md) | Static + bounded dynamic security analysis for Model Context Protocol servers | Private, in development |
| [BackFlowFuzz](projects/backflowfuzz.md) | Deterministic offline fuzzer for the LLM model-output trust boundary | Private, in development; three already-patched CVEs reproduced |
| [ArgusSec](projects/argussec.md) | Evidence-first research workbench for AI and agent security | Private, in development |
| [SlopLab](projects/sloplab.md) | Adversarial testing framework for vulnerability-report triage evaluators | Private, release-oriented benchmark |
| [Partitür](projects/partitur.md) | Multi-model orchestration with a frozen outcome contract and evidence-bound audit | Private, in development |
| [AI-OS](projects/ai-os.md) | Layered governance and record engine for AI-assisted project work | Private, baseline released |

## Security engineering

| Project | What it does | Status |
| --- | --- | --- |
| [Wazuh–IRIS SOC](projects/wazuh-iris-soc.md) | SOC automation, alert/case routing, enrichment, detection rules, and response controls | **Public**; personal-lab flows validated |
| [EDR Telemetry Benchmark](projects/edr-telemetry-benchmark.md) | Windows benchmark separating action success, behavioural verification, and endpoint visibility | Private, in development |


## Examples

- [What a safe output looks like](examples/safe-output-example.md)
- [A campaign that failed](examples/failed-campaign.md)

## What is deliberately absent

**[Why some things are not here](docs/what-is-not-here.md)** — undisclosed
security findings, sensitive material, unsupported claims, and internal tooling.
