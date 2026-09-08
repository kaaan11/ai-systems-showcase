# Why some things are not here

A showcase is where unproven claims creep in. These are the deliberate
omissions, and the reasons.

## Undisclosed security findings

Some of these tools have produced findings in third-party software. **None of
that material appears here** — no target names, no reproduction steps, no
partial hints, and no counts that would narrow a search.

Findings live in separate private repositories and stay there until a
coordinated disclosure process concludes. A disclosure timeline is not shortened
because a showcase would look better with a finding in it.

This also means: if a project page here says a tool found something, it says so
about a **simulation target** built for that purpose, or about an
**already-published, already-fixed** vulnerability used as a ground-truth case.

## Exploit material

No working exploit code, no payload corpora, and no attack tooling is published
here or in the public repositories linked from here. SlopLab, the one public
project in this showcase, states the same boundary in its own README: it is a
benchmark, not a scanner and not an exploit framework.

## Projects that are real but unverified

Several other repositories exist and are not listed. The reason is uniform:
**this showcase only lists work whose claims have been checked.** A project can
be substantial, actively developed, and still absent, because nobody has yet
measured whether its numbers hold.

Two specific cases worth naming as a matter of honesty:

- A research pilot on contextual risk in language models exists and is
  deliberately excluded. Its own README states that no model has ever been
  evaluated in it and that no result of any kind exists. Showcasing it would be
  showcasing an intention.
- A workbench that sits above the other security tools is excluded because its
  documentation has previously carried figures that did not survive inspection —
  in one case a score whose denominator was hard-coded. It returns to this list
  when its claims have been re-measured, not before.

## Internal tooling

Measurement harnesses, task corpora, session logs and the private notebook used
to run this work are not published. They are not interesting on their own and
some of them carry raw model output that has not been reviewed for sensitive
content.

## Numbers in flux

Three of the listed projects were under active revision while these pages were
written. Every project page therefore carries the date its figures were taken
and the state of the tree at that moment. A number without that line is a number
you should not trust — including here.
