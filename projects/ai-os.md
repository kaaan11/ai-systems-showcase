# AI-OS

**A layered governance and record engine for AI-assisted project work.**

> Private, baseline released.

AI-OS answers a narrower question than its name suggests: *when an agent works
on a project, what may it decide, what gets written down, and how does the human
stay the authority?*

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

**An approval checkpoint that survives process death.** `AWAITING_APPROVAL` is a
first-class state and work resumes from it.

## Measured state

- 1,833 tests collected.
- Base install depends only on a YAML parser; the record layer imports and runs
  without the execution runtime, which is what makes it usable as a library.

*Figures taken on 2026-09-08.*

## What is not wired

Two packages exist, are tested, and have **no production caller**: a governed
tool boundary and a code indexer. A payload section for code context is defined
and consumed but never populated by anything in production.

The consequence is worth stating plainly: AI-OS has a constitution, a court and
an archive, and no economy. It reasons about records, and it cannot read the
project it governs.

That is also why it is listed here as what it is. Its record layer is genuinely
used — [Partitür](partitur.md) consumes it as a dependency, and every durable
write in that system goes through this gate. Its execution ambitions are not
met, and the repository's own charter marks them `PLANNED / NOT IMPLEMENTED`.

## The lesson it taught

AI-OS was not written in vain; it was wired to the wrong place. Its real defect
is ergonomic: it made the record a **precondition** of the work, and people want
the record as a **by-product** of it. The schemas, protocols and gate survive
intact in Partitür — what changed is who fills the record in. Not the human, but
the run.
