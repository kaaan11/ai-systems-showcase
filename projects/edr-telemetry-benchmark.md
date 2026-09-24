# EDR Telemetry Benchmark

**A Windows-focused benchmark for separating action success from endpoint visibility.**

> Private, in development.

The benchmark exercises controlled Windows behaviours and records three different
questions instead of collapsing them into one result:

1. **action_status** — did the attempted operation complete?
2. **behavioral_verification** — was the intended behaviour actually observed?
3. **telemetry_observation** — did the endpoint-security telemetry show it?

That separation exists because "the technique ran" and "the EDR saw it" are not the same
claim.

## Current scope

The development line covers process, memory, execution, network, file, and registry
behaviour. Runs produce structured artifacts with provenance, execution identifiers, and
report-generation logic that keeps parent/worker results separated.

Potentially dangerous modes require explicit lab opt-in. The benchmark also includes
cleanup and process-lifecycle safeguards intended to reduce the chance of leaving test
processes behind.

## What is deliberately manual

EDR telemetry observation is currently entered from the security product's logs rather
than automatically ingested.

That limitation is important: the project does not pretend that a locally completed action
was automatically visible to an EDR.

## What is not yet claimed

- Remote/injection technique correctness is not claimed as fully runtime-validated across
  EDR products.
- There is no automated EDR scoring or cross-product ranking.
- A private development benchmark is not presented as an independent product comparison.

The benchmark is useful primarily as a disciplined way to record **what happened**, **what
was verified**, and **what the endpoint product actually exposed**.

*Source status checked 2026-09-24.*
