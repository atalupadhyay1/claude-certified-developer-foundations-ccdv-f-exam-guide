# Domain 8: Tools and MCPs (10.6%)

## Sub-skills

| Sub-skill | Weight |
| --- | --- |
| Tool Implementation | 4.4% |
| MCP Server Development | 2.1% |
| Agentic Customization | 4.1% |

## Tool Implementation (4.4%)

**Tool definitions**
- JSON Schema for `input_schema`: name, description, properties, required, types.
- Descriptions written for the model: clear, when to use, parameter semantics; model relies on description to decide.

**Tool use loop (client tools)**
1. Define tools in request.
2. Model returns `stop_reason: "tool_use"` + `tool_use` block(s) with id/name/input.
3. Your code executes.
4. Send `tool_result` block(s) with matching `tool_use_id`; content = result or error.
5. Repeat until `end_turn`.

**tool_choice**
- `{"type":"auto"}` (default): model decides.
- `{"type":"any"}`: must call a tool.
- `{"type":"tool","name":"..."}`: force specific tool.
- `{"type":"none"}`: no tools.
- `disable_parallel_tool_use`: true to force at most one tool call per turn.

**Parallel tool use**: model may call multiple tools in one turn; handle all, return all results.

**Built-in vs custom tools**
- Built-in/server tools: web_search, web_fetch, code_execution, tool_search, MCP connector — run on Anthropic infra; results returned directly.
- Custom/client tools: you define schema + execute.

**Tool description best practices** (Anthropic "Writing tools for agents"): clear purpose, parameters, when (not) to use, examples, error behavior; keep sets focused; avoid overlapping tools.

**Error handling in tools**: return `is_error: true` in tool_result with explanation; model can recover/retry.

**Approval patterns**: human approval for destructive/write actions; read-only by default.

**Agentic harness dispatch**: how tools are dispatched in agent loops; client-side vs server-side.

## MCP Server Development (2.1%)

**MCP (Model Context Protocol)**
- Standard (USB-C-like) connecting AI apps to tools/data; turns M×N integrations into M+N.

**Primitives**
- **Tools**: executable functions.
- **Resources**: data/context (files, DB rows) the client can read.
- **Prompts**: reusable prompt templates.

**Transports**
- stdio (local process), HTTP/SSE or streamable HTTP (remote), sockets.
- Client vs server roles.

**Server authoring & deployment**
- Build server exposing tools/resources/prompts; deploy; connect from Claude apps.
- MCP connector: connect Claude API to MCP servers directly.

**When to use MCP**: reusable capability across multiple apps, independent maintenance, standardization.

## Agentic Customization (4.1%)

**Tradeoffs among built-in Tools, custom Tools, Skills, and MCPs**
- Built-in/server tools: zero infra, limited to provided capabilities.
- Custom tools: app-specific, in-process, tight control.
- Skills: reusable prompt+tool bundles within Claude Code.
- MCPs: reusable across apps, independently maintained, standard protocol, extra infra/latency.
- Choose based on reuse scope, maintenance ownership, latency, security boundaries.

## Key exam points

- Client vs server tools; request-execute gap.
- stop_reason `tool_use`; tool_result with tool_use_id; is_error.
- tool_choice options.
- MCP primitives: tools/resources/prompts; transports stdio/HTTP.
- MCP for reusable cross-app capabilities (Sample 3).
- Tradeoff matrix for tool type selection.

## Common pitfalls

- Forgetting to return tool_result for every tool_use.
- Mismatched tool_use_id.
- Using built-in tools for arbitrary internal APIs (they can't).
- Over-engineering with MCP for single-app use.
