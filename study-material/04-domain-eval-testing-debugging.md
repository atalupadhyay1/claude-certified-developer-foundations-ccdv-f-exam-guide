# Domain 4: Eval, Testing, and Debugging (2.6%)

Smallest domain. Know debugging method + eval basics.

## Sub-skills

| Sub-skill | Weight |
| --- | --- |
| Debugging and Error Handling | 2.6% |

## Debugging and Error Handling (2.6%)

**Four-step debugging method**
1. Identify error type (429/529/400 etc.).
2. Identify origin: integration layer (plumbing) vs model output.
3. Trace (logs, request/response, tool calls).
4. Precise recovery (retry, fix schema, adjust prompt, escalate).

**Error types**
- 429 rate limit → backoff/retry, reduce concurrency, cache.
- 529 overloaded → retry with backoff, possibly switch region/model.
- 400 bad request → fix payload (schema, params, tokens).
- 413 too large → reduce input, chunk.
- 401/403 → auth/permissions.
- 500 → retry; report if persistent.

**Isolate integration-layer vs model-output problems**
- Plumbing: HTTP, auth, JSON parsing, tool execution, network.
- Model output: hallucination, format violations, refusals, wrong tool choice.
- Test with minimal repro; swap model; check stop_reason.

**Eval practices**
- Golden test sets (input → expected output).
- LLM-as-judge grading (rubrics, pairwise).
- Regression tests on prompt changes.
- Log enough to reproduce bad responses (request/response, tool calls, model version, prompt version).
- Structured output validation; defensive parsing.

## Key exam points

- Classify error before acting (don't guess).
- Distinguish plumbing vs model output.
- LLM-as-judge + golden sets + regression tests.
- Reproducibility via logging.

## Common pitfalls

- Treating all failures as model problems (often plumbing).
- No version pinning → can't reproduce.
- Skipping small domain entirely (still scored).
