# How these systems were built

These systems were built by one person delegating work to several models. The
method below was not designed; it was **distilled from mistakes**, and each rule
carries the measurement that produced it.

In one sentence: **getting a model to do work is cheap; verifying what it did is
expensive — and the whole method is about domesticating the expensive half.**

---

## The loop

```
specification → delegation → independent verification → mutation proof → record
```

Every stage treats the previous stage's output as **untrusted data**. At no
point is "the model said so" a reason.

### 1. Specification

Each unit of work starts from a self-contained brief: context built from
nothing, no reference to another conversation. It contains:

- **Binding rules** — not preferences, but the constraints the project exists to
  enforce.
- **Tasks with explicit signatures.** *Return types are stated exactly; anything
  described in prose but absent from the signature was not asked for.*
- **Named acceptance gates** — not "works well", but "a corrupt JSON file raises
  instead of quietly returning an empty dict".
- **A not-to-be-done list.**
- **A definition of done**, in measurable items.

### 2. Delegation

One criterion:

> **If you can write an objective acceptance gate for it, delegate it.
> If deciding the gate is the work, do it yourself.**

The criterion sometimes says *delegate nothing*, and then nothing is delegated.
Applied to a 3,172-line code port, the answer was that having a model retype
code whose correctness is already established adds **transcription risk to
working code** and nothing else.

### 3. Dual delegation

Pure, single-file tasks with explicit signatures go to **two independent models
from the same specification**, and the outputs are read against each other
before either is read on its own merits.

> **Where two independent implementations agree, the specification was silent.**

*The measurement:* one module went to two models. Both silently resolved an
input carrying two contradictory records for one identifier — one kept the
first, the other kept the last. Both had passing tests. Both were wrong. Given
one output this reads as a *choice*; placed side by side it is visibly a *gap*.
The merged module now refuses that input: it will not invent a verdict the audit
never reached.

The same pattern recurred in a later phase. The method is not a coincidence.

### 4. Independent verification

Sub-model output is **not accepted on a green run.** Every factual and numeric
claim in its report is verified at the source: open the code, run the test,
count the targets.

*The measurement:* a report listed three defects as fixed. The documentation
said "the three most common" where the code chose at random; a test named
"determinism" measured something else; a claim of "only `.ts` files" was made
about a target that also contained `.js`. All three surfaced only under
independent measurement.

### 5. Mutation proof

That a test catches a defect is proven by **putting the defect back and watching
the named test fail.** At least one mutation per acceptance gate, listed in the
commit message.

The most valuable moment in this discipline is when a mutation **refuses to go
red**:

> A mutation applied to an output-redaction layer — "redact first, then
> truncate" — left the test passing. The reason was that the mutation was the
> correct order and the code was wrong. Output is kept from the end, so a secret
> straddling the cut loses its `api_key=` prefix, and the redaction pattern
> matches on exactly that prefix. Measured: `truncate-then-redact leaks`,
> `redact-then-truncate does not`.

So the discipline also runs backwards: instead of exposing a weak test, it
exposes wrong code.

---

## The specification is the weakest link

After four phases of work, the measured pattern was this: **defects came from
the specification more often than from the code.** Three examples, all by the
same author:

| Mistake | Consequence |
| --- | --- |
| An inventory derived from an incomplete search, presented as *"measured, not guessed"* | Four statements did not hold; the implementing side measured against the source and corrected them |
| A signature said `-> str` while the prose asked for a verdict *and* a reason | The result was a `str` subclass whose `json.dumps` kept the label and **silently dropped** the reason |
| A brief declared a flow "not to be skipped" that the product **could not perform** | Two of its steps had no command-line path; the flow had to be wired by hand |

The rule drawn from this: the party writing the specification is verified too,
and the specification itself is subject to an acceptance gate.

### And a specification can contaminate its own measurement

In one campaign, three candidate policy shapes were written into the brief and
one was recommended. Afterwards it became impossible to separate whether the
planning model **reasoned** or **echoed the recommendation**. The same happened
to an evidence-type preference: because the rule was in the prompt, what got
measured was obedience rather than habit.

> Write the thing you want to measure into the specification, and you can no
> longer measure it.

---

## Measurement hygiene

A result is only as valid as the environment it was taken in.

- **Clean shell.** Tests are not run with `PYTHONPATH` set. After a package
  move, a single leftover import left a suite looking green; in a clean shell it
  failed.
- **The console command is exercised separately.** "pytest is green" and "the
  installed command runs" are different claims. A phase was believed complete
  while the package had never been installed into the virtualenv; the tests
  passed only because the root directory was on the path.
- **The verifier can contaminate the environment too.** A directory left under
  `/tmp` during one verification misled an upward-walking project-root finder
  and failed three tests. The defect was in the measurer, not the code.

---

## Records

**A brief is the record of what was asked, and it is never retrofitted to what
was done.** When an implementation deviates, the deviation is reported; the
brief is not edited backwards. Fitting the record to the outcome falsifies the
record.

Every meaningful piece of work leaves a trace: a decision record, an evidence
record, or an updated state file. Decisions freeze with their reasoning, so that
six weeks later the question "why is this like this" still has an answer.

---

## What this method costs

Honestly: **it does not make anything faster.**

Verification cost is human time and does not disappear until it is automated.
Two real defects were found in one delegated module, and what caught both was
review rather than tests. "Delegate and verify" produced working code; it did
not produce it cheaply.

The gain is elsewhere: **less time spent on the wrong work.** When an outcome is
not proven, you learn it the same day rather than six weeks later.
