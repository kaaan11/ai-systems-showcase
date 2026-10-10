# Probandum

*Renamed on 2026-09-28 from ArgusSec. The code repository (ArgusSec), distribution package (llmsec-workbench), and CLI names (argus, argussec, llmsec) still use their existing names.*

*Probandum* is legal Latin for “the thing that must be proved”: a claim that still needs evidence before it can be treated as established.

**A research workbench for hypotheses, experiments, candidate findings, and evidence records in AI and agent security.**

> Private, in development.

Probandum organizes research records around explicit hypotheses, experiment outcomes,
evidence artifacts, candidate findings, and investigations. A recorded status is a
record of what the tool accepted; by itself, it does not prove that the underlying
verification was performed.

## What the audited main snapshot supports

- Hypotheses can be declared, listed, and inspected with expected invariants and
  falsification conditions. An empty experiment without an observation receipt returns
  INCONCLUSIVE and does not falsify the hypothesis; persisted hypothesis status changes
  were not demonstrated by the audit.
- The experiment model represents multiple principals and boundary entities. A synthetic
  cross-user violation returned a PROVEN_CROSS_USER/L4 candidate; persisted hypothesis
  status changes and behavior on a live target were not demonstrated.
- A directed evidence graph and content-addressed store use SHA-256. A synthetic
  integrity probe detected a modified blob. Synthetic imports of [Hostis](hostis.md)
  and [Vestigium](vestigium.md) fixtures recovered raw reports byte-for-byte from the
  store, while normalized candidate metadata omitted unknown extension fields. Evidence
  target-version fields are optional, and exported bundle hashes are checksums rather
  than digital signatures.
- A synthetic investigation flow kept matching candidates separate until a researcher
  accepted their relationship. The accept and reject paths changed the investigation
  state without silently merging the candidate records.
- Wilson interval outputs for the sampled deterministic and probabilistic examples
  matched an independent calculation; zero attempts were rejected.
- Synthetic candidate records produced investigation suggestions and could be accepted
  or rejected. No independent third-party scanner was run in this audit.

## Limits in the audited main snapshot

- The candidates validate command records caller-supplied values; it does not run a
  reproducer or verify that referenced evidence bytes exist in the content-addressed
  store. In a synthetic probe, a non-hash evidence value and an impossible
  successes-to-attempts ratio were recorded as PASS / REPRODUCIBLE. Promotion writes
  PASS directly, does not verify CAS membership, and accepts an approver label without
  authenticating the person behind it.
- The hardening report prints tamper rejection as 100% and five hardening status fields
  as PASS, but those values are hard-coded. The mutation run was 16/22 (73%); the
  report's PASS fields and tamper percentage do not establish that the corresponding
  suites ran or passed. This does not negate the separate synthetic CAS integrity check.
- A calibration helper checks proof objects for some exploitability-level transitions,
  but candidate records also accept caller-supplied levels. An assigned level alone
  does not demonstrate a boundary impact.
- The sandbox-external full-suite run for main was 13 failed and 1,019 passed. The
  current main snapshot is not a clean full-suite result.
- The documented patch-verification CLI returned NOT_TESTED when run without a
  repository path. A service probe with an injected synthetic runner completed, but
  that does not establish that the documented CLI workflow performs fix verification.

A fix is in review but has not been merged into main. This page describes main at the
audited snapshot, not the unmerged fix.

## What this does not prove

Listing Probandum here does **not** claim that:

- it has discovered a vulnerability in a named external target
- every planned workflow has been validated end to end
- a scanner candidate is equivalent to a validated finding
- a research-opportunity score is a vulnerability-severity score

The showcase documents the implemented workbench and the limits measured in its main
snapshot, not a blanket claim about external security results.

*README claim audit: 2026-09-28 at main commit d529f92.*
