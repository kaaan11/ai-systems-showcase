# BackFlowFuzz

**A deterministic, offline fuzzer for the LLM model-output trust boundary.**

> Private, in development.

Most fuzzing points at input. This one points the other way. When an application
calls a language model, the model's *response* crosses back into the
application: it gets parsed, streamed, matched against tool-call schemas, and
dispatched. That return path is a trust boundary, and it is frequently treated
as if it were internal data.

BackFlowFuzz mutates valid model responses and watches what the application does
with them — response parsing, SSE streaming, and tool-dispatch layers.

## What it demonstrates

On a purpose-built simulation target the tool has shown, in one chain:

- An input that genuinely triggers the dangerous behaviour.
- The **observed effect** recorded rather than a bare crash.
- **Exact replay** of the same input reproducing it on the vulnerable revision.
- A **safe-twin differential**: the same input against the hardened equivalent
  function, where the effect does not appear.
- The full `source → transform → entrypoint → sink → effect` chain reported.

## What that does and does not prove

It proves the tool works. It does not prove field discovery.

The simulation target's tests call functions directly; there is no production
call chain from a real model provider in that setup. This is **tool validation**
on a development and regression corpus, and it is recorded as such rather than
presented as a field result.

## Measured state

- 748 tests; 658 run by default, 90 excluded as network-dependent.
- No network is required for the core suite: everything runs on locally built
  archives and directories.
- Offline and deterministic by design.

*Figures taken on 2026-09-08, with the working tree under active revision.*

## A provenance mismatch, recorded rather than hidden

The package reports version `0.2.0` while the project documentation describes
v0.6 and v0.7 work. Until the version string and the documented state agree, any
report this tool produces carries an ambiguous provenance line — and provenance
is the thing an evidence-producing tool cannot be loose about. It is listed here
because a showcase that omits it would be doing the thing this project exists to
catch.

## Boundaries

- No interaction with third-party services; the corpus is local.
- Findings from real targets are not published here. See
  [what is not here](../docs/what-is-not-here.md).
