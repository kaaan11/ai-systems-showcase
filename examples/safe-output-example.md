# What a safe output looks like

Two shapes recur across these systems: an **audit verdict** and an **evidence
record**. Both are designed so that the interesting failure — a label surviving
while its justification disappears — cannot happen quietly.

## An audit verdict

```json
{
  "run_id": "RUN-20260908T114503Z",
  "plan_id": "PLAN-2026-0001",
  "score_digest": "42e639bbb4bfae0a…",
  "findings": [
    {
      "kazanim_id": "K1",
      "verdict": "PROVEN",
      "kanit_tipi": "test_id",
      "kanit_ref": "tests/engine/test_dispatcher.py::test_selection_round_is_skipped_when_round_zero_found_files",
      "note": "fails on the pre-change tree, passes on the post-change tree"
    },
    {
      "kazanim_id": "K2",
      "verdict": "UNPROVEN",
      "kanit_tipi": "test_id",
      "kanit_ref": "",
      "note": "fails on both states: the work is not there"
    }
  ]
}
```

Four properties are load-bearing:

1. **Two values only.** `PROVEN` or `UNPROVEN`. There is no `PARTIAL`, no
   `SKIPPED`, no `NEEDS_REVIEW`. "Partly done" is where label rot lives.
2. **A `PROVEN` finding cannot be constructed with an empty reference.** The
   type refuses it before serialisation.
3. **The reason travels with the verdict.** An earlier version of this type was
   a string subclass carrying its reason as an attribute — `json.dumps` kept the
   label and dropped the reason, silently. It was replaced by a plain record
   whose only route to disk carries both.
4. **The score digest is on the report.** A verdict is meaningless without
   knowing which frozen promise it answers.

## An evidence record

```yaml
---
schema_version: '1.4'
id: EVD-2026-0007
title: held-out run produced tool calls
source_type: EXPERIMENT
status: ACTIVE
observation: 'delegations.jsonl contained 10 tool: lines across four tasks'
collected_at: '2026-09-08T09:14:00Z'
collected_by: partitur
source: run artifact
source_locator: .partitur/evidence/EVD-2026-0007/delegations.jsonl
---
```

The rules doing the work here:

- **`source_type` is a closed vocabulary and it is not a trust score.** A model's
  claim is `MODEL_ASSERTION`: that records the fact that the claim was made, and
  nothing about whether it is true. A command that actually ran is `EXPERIMENT`.
  There is no evidence type that means "the worker said so and we believed it".
- **The observation states what happened, not what it means.** The schema has no
  conclusion field, on purpose. "Three tests failed" is an observation;
  "authentication is broken" is an interpretation and belongs elsewhere.
- **The record is immutable.** When evidence turns out to be wrong the original
  is marked superseded and a new record is written. History is not edited.
- **The locator points inside version control.** A citation that does not
  resolve is not evidence — "I had proof but it was deleted" is not proof.

## What is redacted, and when

Command output captured from a run passes through redaction **before** it is
truncated, never after. The order matters and it was found the hard way: output
is kept from the end, so a secret straddling the cut loses its `api_key=` prefix
— and the redaction pattern matches on exactly that prefix. Truncating first
leaks a fragment that redaction can no longer see.
