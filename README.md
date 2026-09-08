# AI Systems — Showcase

A showcase for a set of security and orchestration systems built over 2026.
The code lives elsewhere. What lives here is **what was built, what was proven,
and — with equal prominence — what was not.**

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

## Projects

| Project | What it does | Status |
| --- | --- | --- |
| [SlopLab](projects/sloplab.md) | Adversarial testing framework for vulnerability-report triage evaluators | **Public**, MIT, CI + releases |
| [MCP Guardian](projects/mcp-guardian.md) | Security scanner and validation toolkit for Model Context Protocol servers | In development |
| [BackFlowFuzz](projects/backflowfuzz.md) | Deterministic, offline fuzzer for the LLM model-output trust boundary | In development |
| [Partitür](projects/partitur.md) | Multi-model orchestration with a frozen outcome contract and evidence-bound audit | In development |
| [AI-OS](projects/ai-os.md) | Layered governance and record engine for AI-assisted project work | Baseline released |

Also public, and older than this showcase:
[AiSOC](https://github.com/kaaan11/AiSOC) ·
[Wazuh-IRIS-SOC](https://github.com/kaaan11/Wazuh-IRIS-SOC)

## Examples

- [What a safe output looks like](examples/safe-output-example.md)
- [A campaign that failed](examples/failed-campaign.md)

## What is deliberately absent

**[Why some things are not here](docs/what-is-not-here.md)** — undisclosed
security findings, unverified projects, and internal tooling.
