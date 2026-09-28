# Tabularium

*Renamed on 2026-09-28 from AI-OS. The code repository (`AI_OSv1`) and distribution package (`kaan-ai-os`) still use their old names.*

*Tabularium* was Rome’s state archive on the Capitolium, where laws, Senate decisions and official records were kept.

**A layered governance and record engine for AI-assisted project work.**

> Private, baseline released.

Tabularium defines what an agent working on a project may decide, what gets
written down, and how the human stays the authority.

It is a written constitution — immutable principles, protocols, policies — plus
the machinery that enforces the record-keeping those documents describe.

## What it actually provides

**A record taxonomy with teeth.** Seven frozen families — Task, Question,
Decision, Investigation, Evidence, Handoff, Report — each with a schema. The
Evidence contract is the sharpest of them: it has a closed vocabulary for what
*kind* of thing was obtained (`OBSERVATION`, `EXPERIMENT`, `MODEL_ASSERTION`,
and others), it requires the observation itself rather than only its source, and
it deliberately has **no conclusion field**. Interpretation is not evidence.

**A persistence gate.** A durable write requires a proposal, a passing
nine-condition evaluation, and a human authorisation bound to the exact content
— so approving a run is explicitly not approving whatever the run later
produces.

**Deterministic context loading with omission accounting.** Selecting what a
worker sees is done by selection and omission over existing material, never by
summarisation, and every omission is recorded with its reason.

**An approval checkpoint.** `AWAITING_APPROVAL` is a first-class state, but
continuation across process death is not yet implemented.

## Measured state

- 1,696 tests collected; with the `runtime` and `api` extras installed: 1,613
  passed, 83 skipped, 1 warning, and 3,102 subtests passed in 143.04s.
- GitHub CI succeeded on the same commit.
- Base install depends only on a YAML parser; the record layer imports and runs
  without the execution runtime, which is what makes it usable as a library.

*Figures taken on 2026-09-28 at commit 6d38514 (origin/main).*

## What is not wired

Two packages exist, are tested, and have **no production caller**: a governed
tool boundary and a code indexer. A payload section for code context is defined
and consumed but never populated by anything in production.

The consequence is worth stating plainly: Tabularium has a constitution, a
court and an archive, but no autonomous economy. It can run a worker against its
own records, while the human still selects tasks and authorizes durable changes.

That is also why it is listed here as what it is. Its record layer is genuinely
used — [Partitür](partitur.md) consumes it as a dependency, and every durable
write in that system goes through this gate. The repository now runs its own
worker pipeline; its charter still marks durable persistence through the
nine-condition gate and continuation across process death as
`PLANNED / NOT IMPLEMENTED`.

## The lesson it taught

Tabularium was not written in vain; it was wired to the wrong place. Its real
defect is ergonomic: it made the record a **precondition** of the work, and people want
the record as a **by-product** of it. The schemas, protocols and gate survive
intact in Partitür — what changed is who fills the record in. Not the human, but
the run.
