# BackFlowFuzz

**A deterministic, offline fuzzer for the LLM model-output trust boundary.**

> Private, in development.

Most fuzzing points at input. This project points at the return path from a model
provider into an application: response parsing, SSE streaming, tool-call decoding,
argument conversion, and dispatch.

BackFlowFuzz mutates valid model responses and records what the target application
actually does with them. The core design treats a crash and a security impact as
different outcomes.

## What it demonstrates now

The current development line reproduces three **already-published and already-patched**
vulnerabilities in real open-source projects:

| CVE | Ground-truth case | Current result |
| --- | --- | --- |
| CVE-2026-61539 | Xinference Llama3 tool-call parsing | reproduced; derived from benign seeds |
| CVE-2025-9141 | vLLM qwen3coder parameter conversion | reproduced; derived from benign seeds |
| CVE-2025-48887 | vLLM pythonic parser ReDoS | reproduced and measured |

These are regression and ground-truth cases, **not original vulnerability discoveries**.

The project also preserves the earlier acceptance properties:

- observed effects are recorded instead of treating a bare crash as a finding
- exact input replay is available for reproduction
- vulnerable and patched/safe behaviour can be compared differentially
- findings preserve the path from source input to sink and observed effect
- the core control plane is offline and deterministic

## What that does and does not prove

Reproducing published CVEs is stronger validation than a synthetic-only target because
the tool must survive real parser and dispatch code. It still does not prove that the
tool will discover new vulnerabilities in arbitrary projects.

A finding is not created merely because a parser throws an exception. The tool separates
security effects, crash-only outcomes, and benign executions.

## Boundaries

- No model is required in the core fuzzing loop.
- Core scans are designed to run offline.
- Already-patched public CVEs are used as ground truth; they are not claimed as discoveries.
- Unpublished third-party findings, if any, are not exposed through this showcase.

*Source status checked 2026-09-24.*
