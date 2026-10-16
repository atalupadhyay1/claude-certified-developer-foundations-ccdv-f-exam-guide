# Domain 3: Claude Code (3.1%)

Small domain — keep prep proportionate. Know operation, hierarchy, modes.

## Sub-skills

| Sub-skill | Weight |
| --- | --- |
| Claude Code Operation | 3.1% |

## Claude Code Operation (3.1%)

**Core components**
- **Rules**: CLAUDE.md instructions; permissions in settings.json.
- **Skills**: reusable slash-command skills (authoring Claude Skills).
- **Commands**: built-in and custom slash commands.
- **Agents**: subagents within Claude Code.
- **Agent Memory**: persistent memory across sessions.

**Features**
- Session management: resume, continue conversations.
- Built-in and custom slash commands.
- Headless mode: run non-interactively (CI/automation) via `claude -p` / SDK.
- Streaming mode: stream output.
- Auto-mode: auto-approve tool calls (with permissions).
- Manual mode: prompt for approval.

**CLAUDE.md hierarchy**
- Home (`~/.claude/CLAUDE.md`) → project root → subfolders.
- Deeper rules override root rules.
- `/init` generates tailored CLAUDE.md for project.
- Use for project conventions, build/test commands, style.

**Repository initialization**
- `/init` scans repo and creates CLAUDE.md.

**settings.json configuration**
- Permissions: allow/deny tool use (bash, file edits).
- Hooks: pre/post tool hooks.
- MCP server config.
- Model selection, env vars.

**Headless use**
- Programmatic invocation for automation, CI, scripting; structured output.

## Key exam points

- CLAUDE.md is guidance; settings.json is machine settings.
- Hierarchy: home → project → subfolder; deeper overrides.
- Modes: headless, streaming, auto-approve vs manual.
- Hooks for guardrails.
- Small weight (3.1%) — don't over-invest; know basics.

## Common pitfalls

- Confusing CLAUDE.md (markdown guidance) with settings.json (JSON config).
- Thinking Claude Code only interactive (has headless).
