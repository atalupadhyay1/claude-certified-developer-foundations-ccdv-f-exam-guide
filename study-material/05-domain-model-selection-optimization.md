# Domain 5: Model Selection and Optimization (16.8%)

Second heaviest. Know LLM fundamentals, model tradeoffs, cost/token management.

## Sub-skills

| Sub-skill | Weight |
| --- | --- |
| LLM Fundamentals | 5.2% |
| Technical Fundamentals | 6.1% |
| Model Selection and Tradeoffs | 2.7% |
| Cost and Token Management | 2.8% |

## LLM Fundamentals (5.2%)

**How LLMs work**
- Tokens: subword units; input/output tokenized separately; pricing per token.
- Context window: max tokens (input+output) a model can handle; fixed.
- Next-token generation via sampling; non-deterministic (temperature/top_p/top_k).
- Sampling: greedy (temp 0) vs stochastic; temperature controls randomness.
- Extended thinking / adaptive thinking / effort levels: more reasoning for hard tasks.
- Fundamental prompting: zero-shot, single-shot (one example), multi-shot (few-shot).

**Model options**
- Fast mode: lower latency for some models.
- Extended thinking: budget_tokens for reasoning.
- Adaptive thinking: model decides reasoning depth.
- Effort levels: control compute.

## Technical Fundamentals (6.1%)

- Integrating with SDKs that wrap REST APIs (Python/TypeScript SDKs).
- Websockets for streaming.
- Basic engineering practices: env setup, dependency management, logging/observability/monitoring.
- JSON schemas, structured output validation.

## Model Selection and Tradeoffs (2.7%)

**Claude model tiers**
- **Opus**: highest capability, complex reasoning, agentic coding, long-horizon. Slowest/costliest. Use for hard problems, planning, evaluation.
- **Sonnet**: best speed/intelligence balance; default for most production. Use for general tasks, coding, agents.
- **Haiku**: fastest/cheapest; classification, extraction, routing, high-volume. Use for simple/high-throughput.

**Tradeoffs**: quality vs latency vs cost. Route: small model classifies → large model handles hard cases (cascade/routing).

**Breaking behavior changes across releases**: model updates can change behavior; pin versions; test before upgrading; read release notes.

**Adaptive thinking support varies by model.**

## Cost and Token Management (2.8%)

**Token budgeting**
- Track input + output tokens including conversation history (history grows cost).
- Cost modeling before scaling: estimate per-request and monthly.

**Cost optimization order (apply in this order before downgrading model):**
1. Prompt caching (cache stable prefixes).
2. Batch processing (50% off for latency-tolerant).
3. Shorter prompts / prune context.
4. Then consider smaller model / lower effort.

**Usage tracking**: log tokens per request; monitor spend; set budgets/alerts.

**Caching techniques**: prompt caching, cache check-pointing, pre-warming.

## Key exam points

- Routing pattern: small model classifies, larger handles hard cases.
- Cost optimization order: cache → batch → shorter prompts → downgrade model.
- Conversation history counts toward tokens/cost.
- Pin model versions; breaking changes across releases.
- Extended thinking costs output tokens; use for hard tasks.

## Common pitfalls

- Downgrading model before trying caching/batching.
- Forgetting history accumulates tokens.
- Using Opus for everything (cost).
- Using Haiku for complex reasoning (quality).
