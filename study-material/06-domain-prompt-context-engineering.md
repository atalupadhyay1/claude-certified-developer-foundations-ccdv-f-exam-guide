# Domain 6: Prompt and Context Engineering (11.0%)

## Sub-skills

| Sub-skill | Weight |
| --- | --- |
| Context Engineering | 3.8% |
| Prompt Engineering | 4.6% |
| Output Handling | 2.6% |

## Context Engineering (3.8%)

**Context window management**
- Fixed token budget; allocate among system prompt, tools, examples, history, retrieved docs, output.
- Attention budget: model attention degrades with long context; put important info where model attends (beginning/end; avoid middle for critical).
- Context rot / drift: quality degrades as context grows/stales; mitigate by pruning, summarization, isolation.

**Preventing context bloat**
- Tool output pruning: truncate/summarize tool results; keep only relevant fields.
- Compaction: summarize older conversation turns.
- Context isolation via subagents: each subagent gets focused context; main agent gets summary.

**Memory management**
- Conversation history: truncation, summarization, keep verbatim what matters (decisions, user prefs).
- Just-in-time context: fetch/retrieve only when needed (RAG, tool calls) instead of stuffing everything.

**RAG basics**
- Retrieve relevant chunks; inject into context; cite sources; manage chunk size/overlap.

## Prompt Engineering (4.6%)

**Parts of a prompt**
- Instruction (what to do), Context (background), Examples (few-shot), Format (output shape).

**Writing clear instructions**
- Be specific, unambiguous, ordered; use XML tags to structure (`<instructions>`, `<context>`, `<examples>`).
- System prompt vs user turn: system for role/rules/persistent; user for task/input.

**Placement**
- Prompt/instruction placement across components (system, user, tool descriptions).
- Long-context ordering: instructions at start and end; data in middle; or repeat key instructions.

**Examples & templates**
- Few-shot examples set pattern; consistent formatting.
- Reusable templates with variables.

**Refinement loop**
- Write → test → measure → adjust → repeat; iterate on failures.

**Input sanitization**
- Sanitize user input; separate from instructions; prevent injection.

**Prefilling**
- Prefill assistant response to steer format (e.g., start with `{` for JSON). (Note: prefilling availability varies by model/API.)

## Output Handling (2.6%)

**Structured output patterns**
- JSON via tool definitions (tool_use with schema) or structured outputs; validate.
- Defensive parsing: handle missing fields, extra text, malformed JSON; retry/repair.

**Response validation**
- Schema validation (Pydantic/Zod); type checks; range checks.

**Handling refusals and errors**
- Detect refusals; adjust prompt or escalate; don't silently fail.

**Consistency techniques for non-determinism**
- Temperature 0 for deterministic; few-shot; constrained decoding; validation + retry; majority voting.

**Skepticism toward confident output**
- Models can be confidently wrong; verify critical outputs; use tools/grounding.

## Key exam points

- System vs user placement; XML structure; prefilling.
- Context rot, attention budget, pruning, compaction, isolation.
- Structured output via tools + validation.
- Few-shot examples for consistency.
- Just-in-time context / RAG.

## Common pitfalls

- Stuffing all context (rot).
- Critical instructions buried in middle of long context.
- Trusting model output without validation.
- No handling of refusals.
