# Domain 7: Security and Safety (8.1%)

## Sub-skills

| Sub-skill | Weight |
| --- | --- |
| AI Application Security | 3.2% |
| Guardrails and Safe Deployment | 2.3% |
| Claude Hooks | 1.0% |
| Identity, Secrets, and Key Management | 1.6% |

## AI Application Security (3.2%)

**Prompt injection**
- Direct: user input contains instructions to override system prompt.
- Indirect: untrusted content (web pages, docs, tool results) contains injected instructions.
- Mitigation: treat retrieved content as data; keep instructions in system prompt; separate trusted/untrusted; guardrails/hooks so injected text can't trigger sensitive actions.

**Jailbreak defense**: defense in depth; don't rely on single control.

**Trust boundaries**: mark content as trusted/untrusted; never let untrusted content become instructions.

**Data leakage prevention**: don't echo system prompt/secrets; minimize data in prompts; mask PII.

**PII handling**: minimize, mask, access control; comply with policies.

**AuthN/AuthZ/confidentiality/privacy/integrity**: standard security principles applied to AI apps.

## Guardrails and Safe Deployment (2.3%)

- Content policy enforcement; guardrail layering (input filters, model, output filters, tool-level).
- Secure-by-design: privacy, IAM, least privilege.
- Human-in-the-loop for high-risk actions.
- Safe deployment: staging, monitoring, rollback.

## Claude Hooks (1.0%)

- Hooks (pre/post tool) for guardrails and safety controls; prevent destructive actions.
- Deterministic enforcement outside model (e.g., block `rm -rf`, require approval for writes).
- Use for: command allowlists, path restrictions, secret scanning, approval gates.

## Identity, Secrets, and Key Management (1.6%)

- API key best practices: never commit keys; use env vars/secret managers; rotate; least privilege; separate dev/prod keys.
- Identity validation and authentication; access approval and level verification; authorized access monitoring.
- Logging/retention: don't log secrets/PII; retention policies.

## Key exam points

- Prompt injection via tool results/docs: treat as data; keep instructions in system prompt.
- Least privilege for tools: read-only by default; confirmation for writes; no secrets in prompts.
- Output validation before executing/sending/storing.
- Hooks = deterministic guardrails.
- Anthropic usage policies constrain what you build.

## Common pitfalls

- Relying on system prompt alone to prevent injection.
- Putting secrets in prompts.
- Over-permissive tools (write access by default).
- Skipping security because small weight (8.1% still ~4 questions).
