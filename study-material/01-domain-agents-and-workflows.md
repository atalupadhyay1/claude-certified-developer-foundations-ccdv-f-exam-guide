# Domain 1: Agents and Workflows (14.7%)

## Sub-skills

| Sub-skill | Weight |
| --- | --- |
| Agent Architecture | 4.5% |
| Agent Construction with Claude | 5.3% |
| Agent Patterns and Frameworks | 4.9% |

## Agent Architecture (4.5%)

**Workflow vs Agent**
- **Workflow**: predetermined code paths; LLM and tools orchestrated through predefined logic. Use when steps are known and fixed, need predictability/cost control, deterministic behavior.
- **Agent**: LLM dynamically directs its own processes and tool usage, maintains control over how it accomplishes tasks. Use when open-ended, unpredictable steps, model judgment needed.
- Decision criteria: task complexity, need for autonomy, predictability requirements, cost/latency budget, safety.

**Manager/supervisor hierarchies**
- Manager (orchestrator) agent plans and delegates; worker/subagents execute subtasks.
- Improves task execution by decomposition, parallelism, specialization.

**Subagents**
- Specialized agents spawned for subtasks; isolate context, enable parallel work, reduce context bloat in main agent.
- Tradeoffs: coordination overhead, context passing, cost.

**Agent loop (core)**
1. Think (model reasons about next action)
2. Call tool (emit tool_use)
3. Observe result (tool_result appended)
4. Repeat until stop condition (end_turn, max turns, human approval)

**Request-execute gap**: model requests tool call; your code executes it. Model never runs code directly (client tools). Server tools (web_search etc.) run on Anthropic infra.

**Stopping problem**: define stop conditions — max turns, max tokens, human approval checkpoints, end_turn. Prevent runaway loops.

**Three loop shapes**: single tool loop; parallel tool calls; nested/subagent loops.

## Agent Construction with Claude (5.3%)

**Claude Agent SDK**
- Handles the loop, tools, permissions, hooks, subagents for you vs hand-rolled loop.
- Decide: SDK vs writing loop; where it runs (self-hosted vs Anthropic-hosted managed); safety via hooks.

**Custom agent loops and harnesses**
- Build loop manually: send messages → detect tool_use blocks → execute → append tool_result → repeat until end_turn.
- Stop conditions, max turns, human approval steps.

**Managed agent deployment models**
- Self-hosted: you run infra, full control.
- Anthropic-hosted: managed, less ops.

**Hooks for deterministic actions**
- Pre/post tool hooks; guardrails; prevent destructive actions; deterministic side effects outside model control.

**Claude Code as agent platform**: rules, skills, commands, agents, memory.

## Agent Patterns and Frameworks (4.9%)

**Anthropic workflow patterns** (from "Building effective agents"):
- **Prompt chaining**: sequential LLM calls, each output feeds next; good for decomposed tasks.
- **Routing**: classify input, route to specialized handler/prompt.
- **Parallelization**: sectioning (split task into independent subtasks) or voting (multiple attempts, aggregate).
- **Orchestrator-workers**: central LLM breaks task into subtasks, delegates to workers, synthesizes.
- **Evaluator-optimizer**: generate → evaluate → refine loop until quality threshold.

**Agentic frameworks**: Strands, LangGraph, PydanticAI, Claude Agent SDK. Tradeoffs: abstraction vs control, debugging, lock-in.

**Context-window management in agents**: tool output pruning, compaction/summarization, subagent isolation, just-in-time context.

## Key exam points

- Know when to choose workflow vs agent (predictability vs autonomy).
- Agent loop steps and stop_reason `tool_use` vs `end_turn`.
- Subagents improve execution via decomposition/context isolation.
- Hooks = deterministic guardrails; not model-dependent.
- Evaluator-optimizer vs orchestrator-workers distinction.
- Claude Agent SDK handles loop/tools/permissions/hooks/subagents.

## Common pitfalls

- Confusing agent (model-driven) with workflow (code-driven).
- Forgetting human-in-the-loop approval for destructive tools.
- Unbounded loops (no max turns).
- Letting tool outputs bloat context (no pruning).
