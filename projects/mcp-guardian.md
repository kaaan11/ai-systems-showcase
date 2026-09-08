# MCP Guardian

**Security scanner and validation toolkit for Model Context Protocol servers.**

> Private, in development.

MCP servers expose tools to a model. That makes them a trust boundary with an
unusual shape: the caller is a language model, the arguments are model-authored,
and the operations behind them are often ordinary system operations — file
reads, process spawns, outbound requests, authorisation decisions.

MCP Guardian statically maps that boundary: it finds entrypoints, follows call
relationships into the operations behind them, and produces a prioritised
**review queue** rather than a verdict list.

## What it does

- Discovers MCP entrypoints across several framework adapters.
- Resolves service boundaries by receiver, class, and import identity, so a
  name collision does not become a false link.
- Applies a rule set spanning Python and TypeScript/JavaScript sources.
- Clusters candidates for review and hands each cluster to a dynamic oracle
  where one applies.
- Fails closed: an engine failure is recorded as a failure, never as a clean
  scan.

## The number it publishes about itself

On its own development corpus:

> **detection 15/15 · confirmed 0/15**

Both numbers belong together. The first says the tool finds the places worth
looking at. The second says that, on that corpus, it has not yet carried a
single candidate across to a demonstrated boundary violation on its own.

That gap is the tool's current frontier: it is good at *where should someone
look*, and not yet an answer to *was the boundary actually crossed*. Publishing
only the first number would be the failure this showcase exists to refuse.

## Validation beyond its own corpus

The scanner has been exercised differentially against public MCP server
repositories at the commit before and after a published, already-fixed
vulnerability, checking that the finding appears on one side and not on the
other. That is a ground-truth check against public history, not a discovery
claim.

## Measured state

- 658 tests collected.
- Rule sets for Python and TypeScript/JavaScript; five framework adapters.
- A static-to-dynamic experiment bridge exists that emits preparation manifests
  and can execute a narrow authorisation oracle against an explicitly allowed
  local target. It never turns an unexecuted cluster into a confirmed finding.

*Figures taken on 2026-09-08, with the working tree under active revision.*

## Known limitations, stated

- Scanning a single wrapper file can miss sibling service implementations; the
  package or repository root is the correct scan target.
- Static-analysis engine resolution depends on the environment's `PATH`, so a
  campaign can silently run against a different analyser version unless it is
  pinned.
- A taint layer proving attacker-controlled data flow is not implemented.
