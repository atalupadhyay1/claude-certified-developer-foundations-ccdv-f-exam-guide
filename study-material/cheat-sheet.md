# Cheat Sheet — CCDV-F

## Exam facts
53 items · 120 min · scaled 720/1000 · $125 · 12 months validity.

## Domains & weights
1 Agents & Workflows 14.7%
2 Applications & Integration 33.1%
3 Claude Code 3.1%
4 Eval/Testing/Debugging 2.6%
5 Model Selection & Optimization 16.8%
6 Prompt & Context Engineering 11.0%
7 Security & Safety 8.1%
8 Tools & MCPs 10.6%

## Top 6 topics (>5%)
1 Claude Application Design 8.6%
2 Software Engineering Foundations 7.4%
3 Claude API Mechanics 6.8%
4 Technical Fundamentals 6.1%
5 Agent Construction with Claude 5.3%
6 LLM Fundamentals 5.2%

## API quick facts
- Endpoint POST /v1/messages; roles: system (top-level), user, assistant.
- stop_reason: end_turn | max_tokens | stop_sequence | tool_use | pause_turn | refusal.
- Streaming: stream:true (SSE). Batch: stream not supported.
- Batch: 50% cost, ≤100k req or 256MB, most <1h, results ≤24h (expire), results kept 29 days, no streaming/fast mode/max_tokens:0.
- Cache: default 5-min TTL (1h option); auto or explicit breakpoints; write ~1.25×, read ~0.1× input; stable content first.
- Errors: 400 bad req, 401 auth, 413 too large, 429 rate limit, 500, 529 overloaded. Backoff + jitter; idempotent writes.
- Vendors: Bedrock, Vertex, Foundry.

## Agent loop
Think → call tool → observe → repeat until end_turn/max turns/approval. Subagents isolate context. Hooks = deterministic guardrails.

## Workflow patterns
Prompt chaining, routing, parallelization (sectioning/voting), orchestrator-workers, evaluator-optimizer.

## Model tiers
Opus = hardest reasoning/coding; Sonnet = balance (default); Haiku = fast/cheap (classify/extract/route).
Cost order: cache → batch → shorter prompts → downgrade model.

## Prompt/context
System vs user; XML tags; few-shot; prefill. Context rot → prune tool output, compact, isolate via subagents. Attention budget: important at start/end.

## Security
Injection (direct/indirect): treat retrieved content as data; keep instructions in system; guardrails/hooks; least privilege; read-only default; confirm writes; no secrets in prompts; validate output.

## Tools/MCP
Client tools: you execute; server tools: Anthropic executes. tool_choice: auto/any/tool/none. MCP primitives: tools/resources/prompts. Transports: stdio/HTTP. MCP for reusable cross-app capabilities.

## Claude Code
CLAUDE.md = guidance (hierarchy home→project→subfolder, deeper overrides). settings.json = machine settings (perms, hooks, MCP). Modes: headless, streaming, auto/manual. /init.

## Debugging 4 steps
Identify error type → origin (plumbing vs model) → trace → recovery. Evals: golden sets, LLM-as-judge, regression tests, log for repro.
