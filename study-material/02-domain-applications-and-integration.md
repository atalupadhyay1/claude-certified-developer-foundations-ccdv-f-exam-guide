# Domain 2: Applications and Integration (33.1%)

The heaviest domain — a third of the exam. Master API mechanics, app design, SE foundations, config.

## Sub-skills

| Sub-skill | Weight |
| --- | --- |
| Understanding Requirements | 3.4% |
| Systems Life Cycle | 2.8% |
| Claude API Mechanics | 6.8% |
| Software Engineering Foundations | 7.4% |
| Claude Application Design | 8.6% |
| Configuration Management | 4.1% |

## Understanding Requirements (3.4%)

- Translate business/functional requirements into Claude-powered application designs.
- Identify functional vs infrastructure requirements.
- Solution architecture: components, data flow, integration points, constraints (latency, cost, privacy).
- Non-functional: scalability, reliability, security, observability.

## Systems Life Cycle (2.8%)

- SDLC phases: plan → design → build → test → deploy → operate → maintain.
- Waterfall vs Agile; Claude models change with updates (model versioning matters).
- "Operate and maintain trap": shipping is not the end; monitoring, drift, model updates, cost.
- Version control, code review, refactoring as part of lifecycle.

## Claude API Mechanics (6.8%)

### Messages API

- Endpoint: `POST /v1/messages`.
- Roles: `system` (top-level param, not a message), `user`, `assistant`.
- Content blocks: `text`, `image`, `document` (PDF), `tool_use`, `tool_result`, `thinking`.
- Key params: `model`, `max_tokens` (required), `messages`, `system`, `tools`, `tool_choice`, `temperature`, `top_p`, `top_k`, `stop_sequences`, `stream`, `metadata`.
- `stop_reason`: `end_turn`, `max_tokens`, `stop_sequence`, `tool_use`, `pause_turn`, `refusal`.
- `max_tokens` must be ≥ 1 (0 not allowed, except cache pre-warming not in batch).

### Streaming

- Set `stream: true`; server-sent events (SSE).
- Events: `message_start`, `content_block_start`, `content_block_delta`, `content_block_stop`, `message_delta`, `message_stop`.
- Delta types: `text_delta`, `input_json_delta` (tool args), `thinking_delta`, `signature_delta`.
- Use for UX (perceived latency), long outputs, tool-use streaming.
- Handle partial content and tool-use blocks as they arrive.

### Vision / Multimodal

- Images as content blocks: `{"type":"image","source":{"type":"base64","media_type":"image/png","data":...}}` or `{"type":"url",...}`.
- PDFs via `document` blocks or Files API.
- Files API: upload once, reference by file_id across requests (reuse uploads).

### Extended thinking

- `thinking: {"type":"enabled","budget_tokens":N}` (or adaptive). Model produces reasoning in `thinking` blocks (not counted as output? billed as output tokens). Improves complex reasoning. Reduces? Use for hard tasks; costs tokens.

### Prompt caching

- Cache prompt prefixes to reduce cost/latency.
- Two modes: **automatic** (top-level `cache_control: {"type":"ephemeral"}`) and **explicit breakpoints** (place `cache_control` on content blocks).
- Default TTL 5 minutes; refreshed at no cost on hit. 1-hour TTL option (write cost higher).
- Minimum cacheable length: 1024 tokens (Sonnet/Opus) / 2048 (Haiku) for a breakpoint (varies by model). Cache breakpoint must align to block boundaries.
- Order stable content first (system, tools, examples, large context) then variable.
- Pricing: cache write ~1.25× base input; cache read ~0.1× base input (varies). Big savings on repeated prefixes.
- Lifetime measured from start of request that writes/reads; generation time counts against TTL.

### Third-party vendors

- Invoke Claude via AWS Bedrock, Google Vertex AI, Microsoft Foundry (Azure). Same models, different endpoints/SDKs/auth. Region availability, pricing may differ.

### Batch vs realtime

- **Message Batches API**: async, up to 100,000 requests or 256 MB per batch; most finish <1h; results within 24h or expire; results available 29 days. 50% cost reduction. No streaming, no fast mode, no max_tokens:0. Use for latency-tolerant high-volume work (evals, moderation, bulk generation).
- **Realtime Messages API**: synchronous, low latency, streaming, full feature set. Use for interactive.
- Tradeoff: cost vs latency; batch for overnight/bulk.

### Error handling & retries

- Status codes: 400 (bad request/validation), 401 (auth), 403, 404, 413 (request too large), 429 (rate limit), 500, 529 (overloaded).
- Exponential backoff with jitter; respect `Retry-After` header.
- Idempotent design for writes (idempotency keys) to safely retry.
- Distinguish integration-layer (plumbing) vs model-output problems.

## Software Engineering Foundations (7.4%)

- **REST APIs**: HTTP methods, status codes, headers, JSON bodies, statelessness.
- **JSON**: schemas, structured output validation, parsing.
- **Async programming**: Python (asyncio) / TypeScript (promises/await); concurrency, non-blocking I/O.
- **Version control**: git as unlimited undo for code, prompts, configs; branches, PRs.
- **SDLC integration**: plan→operate; Claude models change with updates → pin versions.
- **Code review**: second pair of eyes; review prompts/configs too.
- **Refactoring**: small (rename/extract) and large (restructure); keep tests.

## Claude Application Design (8.6%)

- **Interfaces**: Claude Code, Desktop, claude.ai, API, SDKs — each handles instructions differently (system prompt placement, tool availability, context). Design for the interface.
- **Content boundaries**: safeguard against untrusted data; separate trusted instructions from untrusted content; treat retrieved docs/tool results as data.
- **Schema design**: JSON schemas for structured outputs; validate responses; defensive parsing.
- **Session hygiene**: manage conversation history; truncation/summarization; keep system prompt stable; don't leak secrets into logs.
- **Plugin management**: versioned plugins, dependencies.
- **Multi-modal input handling**: text, images, code.
- **State management & context window budgeting**.

## Configuration Management (4.1%)

- **CLAUDE.md**: guidance (markdown instructions) for Claude Code; hierarchy from home → project → subfolders; deeper overrides root.
- **settings.json**: machine settings (permissions, hooks, MCP servers).
- **Model version pinning**: pin model IDs (e.g., claude-sonnet-4-5) for predictable behavior; plan upgrades.
- **Prompt versioning**: track prompts in git; versioned model/prompt/plugin configs.
- **Plugin dependencies**: declare and pin.
- Principle: guidance (CLAUDE.md) vs machine settings (settings.json) vs versioned artifacts (models/prompts/plugins), all tracked in git.

## Key exam points

- stop_reason values and meanings.
- Cache TTL 5 min default; min cacheable tokens; order stable first.
- Batch: 50% cost, 24h, 100k req/256MB, 29-day results, no streaming.
- Error codes 429/529/400 and recovery.
- Content boundaries = security (untrusted as data).
- CLAUDE.md (guidance) vs settings.json (machine settings).

## Common pitfalls

- Confusing system prompt placement (top-level `system`, not a message).
- Thinking batch supports streaming (it doesn't).
- Caching variable content first (breaks cache hits).
- Treating tool results as trusted instructions.
