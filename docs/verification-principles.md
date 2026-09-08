# Verification principles

The claim these projects share, in one sentence:

> **A label is not evidence that the work beneath it was done. It is only the
> assertion that it was.**

None of the principles below is a preference. Each came from a mistake, and each
is recorded here with the measurement that produced it.

## 1. A label is not evidence

`DONE`, `PASS`, `RESOLVED`, `IN_PROGRESS` are assertions. Before repeating one,
verify that what sits beneath it earns it.

*The measurement:* three places on the same day. A task marked `DONE` had an
empty change list. Two design records marked `DONE` had no production caller.
A task marked `IN_PROGRESS` had a body that was still the template text. All
three were caught by measurement; none by the label.

## 2. A passing test is not proof that it measures the right thing

That a test catches a defect is proven by **putting the defect back and watching
the named test fail.**

*The measurement:* a determinism test called twice inside one process. The hash
seed is fixed per process, so the test passed against broken code too. In
another case a test caught not the defect it claimed, but the defect's *side
effect* — repairing an empty field left a different field unowned, and the test
was reading that.

## 3. A model's output cannot be evidence for its own claim

A model saying "done" is not proof that it is done. Evidence is a `file:line`,
a test identifier, or the log of a command that ran.

*In practice:* the audit schema in Partitür has no `worker_says` evidence type
and will not get one. A worker's summary is classed as `MODEL_ASSERTION` — that
records the fact that the claim was made, not that it is true.

## 4. Absence is not evidence

Zero findings is not proof of safety. A clean result obtained without exercising
the boundary shows only that the boundary was not exercised.

*In practice:* "I could not break it" is a claim whose evidence is the log of
what was attempted. A scanner that fails must produce a `could-not-scan` result
and a non-zero exit code, or its caller will read the failure as a clean scan.

## 5. Detection and confirmation are different numbers

`detection` is a candidate. `confirmed` is evidence. They do not collapse into
one figure.

*The measurement:* on its own development corpus a scanner reported
**15/15 detection and 0/15 confirmed.** Publishing both is less impressive and
more true than publishing the first and omitting the second.

## 6. A result on the set that produced a policy does not validate it

The data that produced a policy cannot confirm it. No generalisation without a
held-out set.

*The measurement:* a routing policy was consistent on its own derivation set.
Measured against a held-out target, the observation the policy rested on
**reversed** — the derivation set's task descriptions happened to make the
measured behaviour unnecessary.

## 7. A crash alone is not a security finding

A finding requires three things together: the forbidden effect is **named**, the
effect is **reproduced**, and a **control run** on the same path did not produce
it. Without all three there is an observation, not a finding.

## 8. A repair may not change the promise

When work fails, what gets repaired is *how it was done* — never *what was
promised*. Editing the claim after failing the exam is changing the question.

*In practice:* Partitür freezes the outcome list and records its digest. A
correction round may change the tasks; a proposal that touches the outcomes is
rejected whole rather than filtered.

## 9. The instrument is not repaired mid-measurement

A defect found during a campaign is recorded, not fixed. Repairing the
instrument while it runs changes what it is measuring.

## 10. Failures are published too

The most concrete example in this showcase: Partitür was run against its own
engine in its first real campaign and **did not finish the job.** All three
outcomes ended unproven, the merge was refused, and the premise the campaign
rested on was falsified by the campaign's own logs.

Details: [a campaign that failed](../examples/failed-campaign.md).
