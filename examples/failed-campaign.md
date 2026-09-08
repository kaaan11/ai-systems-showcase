# A campaign that failed

On 2026-09-08, [Partitür](../projects/partitur.md) was pointed at its own engine
and asked to change a policy in it. This is the account, because
[principle 10](../docs/verification-principles.md) says failures are published
too.

## The job

The worker's tool discovery ran in two rounds. Round 0 was deterministic: paths
named in the task instructions were read directly, no model call. Round 1 asked
a model which tools it wanted with whatever call budget was left.

A prior measurement on a held-out target had found round 1 to be **43–44% of
total cost and to execute no tool at all.** The campaign's job was to act on
that: remove round 1, or gate it.

## The result: the work did not land

- The planner produced a three-outcome score; a human approved it unedited.
- Round 0 produced one fragile diff. The correction round's patch did not apply
  — context mismatch — and its two dependent tasks could not run.
- **All three outcomes ended `UNPROVEN`.** The breaker correctly refused to run,
  because its ordering gate requires a clean audit first.
- The merge was refused.

## The result that mattered: the premise was falsified

Reading the campaign's own delegation log, per task:

```
t1: deterministic first read → read_file(ok) → search_code(ok)
t2: deterministic first read → read_file(ok) → search_code(denied)
t3: deterministic first read → read_file(ok) → git_history(ok)
```

Round 0 can only issue `read_file`. `search_code` and `git_history` can only
come from round 1. **Round 1 requested tools in all three tasks and executed
them in two.** The measurement the whole campaign rested on did not hold on this
task distribution.

Why: on the held-out set that produced the original figure, the task
instructions happened to name the files. Round 0 satisfied the need, so round 1
had nothing left to do. Here they did not, and round 1 did real work.

This is [principle 6](../docs/verification-principles.md) landing on the people
who wrote it: a result on the set that produced a policy does not validate it.

## The gate that saved something

Before the campaign, a rule was written into it: **nothing merges until the
campaign closes.** The stated reason was that a merged diff would change the
code the next round runs and make rounds incomparable.

It caught something else entirely. The worker's diff proposed **deleting the
run's own delegation log** — the target repository contains the run directory,
and the workspace copy was taken before that log grew, so the diff read the
growth as a deletion. Right rule, right place, wrong reason.

## Six defects, none fixed

Recorded and deliberately left alone, because
[principle 9](../docs/verification-principles.md) forbids repairing the
instrument mid-measurement:

1. Run artefacts entering the worker's diff (above).
2. The auditor's token cap too small for its own work, and not settable from the
   command line — which is why the auditor returned nothing, twice.
3. A tester role reporting changes with no workspace: `DONE` at 0.82 confidence,
   naming a file that does not exist.
4. The action gate rejecting `a|b|c` in a regular-expression search parameter as
   a shell metacharacter, on a path that never reaches a shell.
5. The worker inspecting `locals()` to guess a variable name when the variable
   was in scope. The generated code is **accidentally correct** and breaks
   silently on a rename — and the merge gate scored it `DONE` at 0.72.
6. The falsified premise itself.

## Three of the mistakes were in the specification

Not in the code, and not in the models:

- The brief listed three candidate policy shapes and recommended one. Afterwards
  it was impossible to tell whether the planner **reasoned** or **echoed**.
- The brief required an evidence-type preference in the prompt, so the resulting
  3/3 distribution measured **obedience, not habit**.
- The brief declared a six-step flow "not to be skipped" — and two of those
  steps had no command-line path at all. A flow the product cannot perform was
  made mandatory by someone who never checked that it could.

## What was decided

The merge was refused on three independent grounds, any one sufficient: the
premise had reversed, the code was accidentally correct, and no outcome was
proven.

The next campaign's brief will contain **no recommendation of any kind** — no
policy shape, no evidence-type preference. Only the target and the rules.
