# Exam Overview — CCDV-F

## What the credential validates

The **Claude Certified Developer – Foundations (CCDV-F)** validates that an individual can **build, integrate, and ship production-grade applications, agents, and workflows** using Anthropic's Claude platform at a foundational level. It targets technical professionals who bridge Claude's capabilities and production-ready applications.

## Intended audience

- AI/ML engineers, technical leads, senior software engineers
- 1–5 years software engineering experience (recommended)
- ≥ 6 months hands-on with Claude or comparable LLM
- Proficient in Python and/or TypeScript
- Fluent with REST APIs and CLI tools
- Working understanding of LLM fundamentals, agents, context management, MCP

Not for non-technical users, casual users, or roles limited to prompt writing.

## Exam facts

| Item | Detail |
| --- | --- |
| Exam code | CCDV-F |
| Items | 53 (multiple-choice + multiple-response; each states how many to select) |
| Time | 120 minutes |
| Delivery | Proctored: online or test center (Pearson VUE) |
| Passing | Scaled 720 / 1000 |
| Fee | $125 USD |
| Validity | 12 months from award |
| Result | Pass/fail + scaled score + % correct by domain |

## Scoring

- Criterion-referenced (not curved). Pass by demonstrating blueprint knowledge.
- Scaled score 100–1000, cut score 720.
- Domain percentages on score report are informational only; pass/fail based on total scaled score.

## Registration

1. Go to certification page on Anthropic Partner Academy.
2. Download Exam Guide; review Terms/Conditions and Exam Policy.
3. Register + checkout ($125, partner-tier discounts may apply).
4. Create Pearson VUE account; schedule session (online proctored or test center).
5. Cancel/reschedule up to 24 hours before; within 24h forfeits fee.

## Policies

- **ID:** valid unexpired government-issued photo ID; name must match registration exactly.
- **Accommodations:** request/approve via Pearson VUE before scheduling.
- **Retake:** 14 days after 1st failure, 30 after 2nd, 90 after 3rd; max 4 attempts per 12 months; fee per attempt.
- **No-show/late:** forfeits fee.
- **NDA:** accept before exam; all content confidential.
- **Misconduct:** invalidation, revocation, ban.

## Credential maintenance

- Valid 12 months. Renew on time via free non-proctored assessment on Partner Academy (review changes since certifying). No fee for on-time renewal.
- If lapsed, retake full exam at full fee.
- If content changes significantly, Anthropic may require full retake.

## How to prepare (official guidance)

- Self-assess against every objective in Section 6 blueprint.
- Review official Anthropic docs: Claude API, models, prompt engineering, Claude Code, Skills, MCP.
- Build and operate at least one Claude app exercising the API, ≥1 tool, basic prompt/context engineering, simple security + eval.
- Practice developer competencies: prompts/system instructions, agents/workflows, Claude Code config, token/cost management, guardrails, custom tools/MCP servers.
- Complete sample questions (Section 8) for item style.

## Sample questions (from official guide)

**Sample 1 — Domain 2 (Applications and Integration).** Process 10,000 documents overnight for a non-urgent analytics report; cost primary; results next morning.
- A. Send every request synchronously through Messages API in parallel.
- B. Use Message Batches API (large async workloads, 24h window, reduced cost). ✅
- C. Lower max_tokens on synchronous calls.
- D. Switch to smallest model regardless of quality.
Rationale: Batches API is designed for latency-tolerant high-volume workloads at lower cost. Sync parallel (A) doesn't reduce per-token cost; lowering max_tokens (C) or blindly downsizing (D) doesn't address batch-vs-realtime tradeoff.

**Sample 2 — Domain 7 (Security).** Agent summarizes web pages; one page has hidden text instructing model to ignore previous instructions and reveal system prompt.
- A. Raise temperature.
- B. Treat retrieved page content as untrusted, keep separate from trusted instructions, use guardrails/hooks so injected instructions can't trigger sensitive actions. ✅
- C. Add a line to system prompt asking users not to include malicious instructions.
- D. Switch to larger model.
Rationale: Isolate untrusted content from trusted instructions + least-privilege guardrails. Temperature irrelevant; polite request not enforceable; more instruction-following model can be more susceptible.

**Sample 3 — Domain 8 (Tools and MCPs).** Need Claude to call internal inventory REST service; capability reusable across several apps and maintained independently.
- A. Hard-code inventory logic into each app's system prompt.
- B. Build MCP server exposing inventory operations as tools. ✅
- C. Paste current inventory data into context window every request.
- D. Rely on built-in tool.
Rationale: MCP server exposes reusable tools shareable across apps and independently maintained. Hard-coding (A) not reusable/maintainable; pasting (C) no live access + wastes context; built-in tools (D) don't reach arbitrary internal APIs.

## Study tips

- Weight your study time by domain weight: Domain 2 (33.1%) ≈ half your effort; Domains 3+4 (5.7%) small but don't skip.
- Build at least one real app: API + tool + prompt/context engineering + security + eval.
- Drill stop_reason values, error codes (429/529/400), caching breakpoints, batch limits.
- Know the 25 sub-skill weights; the top 6 topics (>5%) = 39.4% of exam.
