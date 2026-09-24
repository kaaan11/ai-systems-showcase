# Why some things are not here

A showcase is where unproven claims creep in. These are the deliberate omissions,
and the rules used to keep them out.

## Undisclosed security findings

Some of these tools may produce candidates or findings in third-party software.
**Undisclosed material does not appear here** — no target names, private reproduction
steps, partial hints, or counts that would narrow a search.

Findings stay in separate private workspaces until the relevant disclosure process
allows publication.

If a project page here says a tool reproduced a vulnerability, it refers either to a
purpose-built validation target or to an **already-published, already-fixed** vulnerability
used as a ground-truth case.

## Sensitive exploit material

The showcase does not publish working exploit code, sensitive payload corpora, secrets,
or private target data.

Public defensive projects linked from this repository may contain detection rules,
lab-safe validation material, or response automation. That is different from publishing
undisclosed exploit material.

## A listed project is not automatically a proven result

A project can be listed because the **artifact itself is real and inspectable** while its
research result is still unknown. The status line on each page matters.

Two examples are intentionally explicit:

- **LLM Security–Usability Benchmark** is listed because its pre-registration,
  controlled stimuli, review workflow, and audit trail exist. Its page also states that
  no model evaluation has been run and no empirical result exists yet.
- **ArgusSec** is listed for its implemented research-workbench architecture and
  evidence model. Its presence is not a claim that it has discovered external
  vulnerabilities or that every planned workflow has been validated end to end.

This distinction lets the showcase document serious work without converting an
unfinished study into a result.

## Internal tooling

Raw session logs, private research corpora, undisclosed evidence, temporary orchestration
state, and internal notebooks are not published merely to make the portfolio look larger.

## Numbers in flux

Projects under active development change quickly. Numeric claims should therefore be
traceable to the source repository and, where useful, carry a date or validation context.

Test counts are intentionally not used as the primary proof of project quality here.
A dated capability claim — for example, reproducing a known patched CVE or completing a
frozen study-design milestone — is usually more meaningful than a large test number.
