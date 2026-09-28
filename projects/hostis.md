# Hostis

*Renamed on 2026-09-27 from BackFlowFuzz. The code repository (`BackFlowFuzz`), package (`backflowfuzz`), and CLI (`backflowfuzz`) still use their old names.*

*Hostis* is Latin for “stranger” or “enemy”; it shares a root with *hospes* (“guest” or “host”), behind “hostile” and “hospitality.”

**A deterministic, offline fuzzer for the LLM model-output trust boundary.**

> Private, in development.

Most fuzzing points at input. This one points the other way. When an application
calls a language model, the model's *response* crosses back into the
application: it gets parsed, streamed, matched against tool-call schemas, and
dispatched. That return path is a trust boundary, and it is frequently treated
as if it were internal data.

Hostis mutates valid model responses and watches what the application does
with them — response parsing, SSE streaming, and tool-dispatch layers.

## What it demonstrates

On a purpose-built simulation target the tool has shown, in one chain:

- An input that genuinely triggers the dangerous behaviour.
- The **observed effect** recorded rather than a bare crash.
- **Exact replay** of the same input reproducing it on the vulnerable revision.
- A **safe-twin differential**: the same input against the hardened equivalent
  function, where the effect does not appear.
- The full `source → transform → entrypoint → sink → effect` chain reported.

*Simulation demonstration recorded on 2026-09-08; not re-run for this refresh.*

## What that does and does not prove

The results recorded here are tool validation, not field discovery.

The simulation target's tests call functions directly; there is no production
call chain from a real model provider in that setup. This is **tool validation**
on a development and regression corpus, not a field result.

## Measured state

- Default selection: 1,443 tests from 1,534 collected; 91 marked `slow` are
  excluded by default.
- Both self-hosted CI shards succeeded on the same commit.
- No network is required for the core suite: everything runs on locally built
  archives and directories.
- Offline and deterministic by design.

*Figures taken on 2026-09-28 at commit d17ecaf (origin/main).*

## A provenance mismatch, recorded rather than hidden

The package reports version `0.2.0` while the project documentation describes
v0.7 work. Until the version string and the documented state agree, any
report this tool produces carries an ambiguous provenance line — and provenance
is the thing an evidence-producing tool cannot be loose about. It is listed here
because a showcase that omits it would be doing the thing this project exists to
catch.

## Boundaries

- No interaction with third-party services; the corpus is local.
- This showcase carries no target-specific results. See
  [what is not here](../docs/what-is-not-here.md).
