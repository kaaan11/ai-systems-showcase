# MCP Guardian

**Security scanner and validation toolkit for Model Context Protocol servers.**

> Private, in development.

MCP servers expose tools and resources to model-authored calls. That creates security
boundaries around authorization, state handles, outbound requests, command execution,
file access, and other ordinary system operations.

MCP Guardian maps those boundaries and produces evidence for review rather than turning
every static match into a vulnerability claim.

## Current development line

The current private development line includes:

- static rules for Python and TypeScript/JavaScript
- MCP framework and entrypoint recognition
- risk normalization and ground-truth regression cases
- bounded Docker-based dynamic probing
- HTTP authentication and SSRF-oriented audit paths
- authorization-topology analysis
- state-handle / BOLA topology analysis
- OAuth control-plane topology analysis
- static-to-dynamic experiment manifests for narrow local validation recipes

The project fails closed where possible: unresolved analysis is recorded as unresolved,
not silently converted into a clean result.

## The important distinction

A static `missing` result is a **candidate for review**, not proof of a vulnerability.

For example, an ownership check that cannot be seen statically does not become a BOLA
finding by assertion. Confirmation requires an appropriate dynamic oracle, explicit
target authorization, and evidence that the boundary was actually crossed.

## Validation model

Ground-truth checks use known vulnerable and fixed revisions where available.
Dynamic validation is deliberately narrow and opt-in, with local/sandboxed targets and
explicit recipes.

The output can also be normalized for evidence-first research workflows such as ArgusSec,
without turning an unexecuted candidate into a confirmed finding.

## Boundaries

- The project is not distributed as a public scanner package.
- Static absence is not treated as exploit proof.
- Dynamic recipes are intentionally bounded; unsupported cases remain unresolved.
- No external target is presented here as vulnerable merely because a rule matched.

*Source status checked 2026-09-24.*
