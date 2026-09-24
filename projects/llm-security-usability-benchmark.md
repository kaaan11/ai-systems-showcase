# LLM Security–Usability Benchmark

**Does conversational context change how a model interprets the same final prompt?**

> Private research repository · pre-registered pilot · **no model results yet**.

This study sits between two failure modes: over-refusal of legitimate security work and
under-refusal of harmful requests. It asks whether conversational context changes the
risk interpretation of a byte-identical final user prompt.

## Study design

One research item contains one canonical final prompt evaluated under controlled
preceding contexts:

- **A — final prompt only**
- **B — legitimating context**
- **C — incriminating context**
- **D — neutral filler control**

The final prompt is kept byte-identical across conditions. The context is the manipulated
variable.

The current pilot contains **50 research items** represented across **171 condition
records**. The design also keeps benign and high-risk null controls separate rather than
collapsing them into the primary ambiguity group.

## Why the neutral control matters

Condition D exists to falsify a tempting explanation.

If B and C move the model but neutral conversational filler moves it just as much, the
effect may be generic priming or conversation length rather than meaningful context.
That possibility is part of the pre-registered interpretation rules rather than something
added after seeing results.

## Frozen before evaluation

The study's hypotheses, analysis rules, stopping conditions, and reporting rules were
frozen before model evaluation. Protocol files are hash-pinned, and the tooling checks
that the recorded documents remain byte-identical to the frozen versions.

The current phase is **blind human review / quality control (Phase 7G)**.
Model evaluation (Phase 8) has not started.

## What this does not prove

- No model has been evaluated in this study yet.
- There is no refusal rate, attack-success rate, latency result, or model comparison.
- The stimuli are research artifacts under human review, not expert-validated ground truth.
- A 50-item pilot can test feasibility and direction; it cannot justify broad prevalence claims.

The absence of a result is intentional and visible. The study is shown here as a research
design and reproducibility artifact, not as evidence that a particular model behaves a
particular way.

*Source status checked 2026-09-24.*
