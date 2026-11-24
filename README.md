# tele33776-lab17-agentgateway
## Security controls

| Control | Purpose | Mechanism / Scope |
| --- | --- | --- |
| Scoped API Keys | Restrict access by client/endpoint | Separate keys for Claude Code, Pi, and MCP (`sha256` hashes in `config.yaml`) |
| PII Guardrails | Redact or mask sensitive data | Regex guardrails (`<CREDIT_CARD>`, `<SSN>`, `<EMAIL_ADDRESS>`, `<PHONE_NUMBER>`) |
| Token Budgets | Prevent runaway token usage | Per-key/daily token limits returning `HTTP 429` when exceeded |
| Fine-Grained GitHub PAT | Limit repository blast radius | Scoped to `tele33776-lab17-agentgateway` (`Contents`, `Issues`, `Pull requests` read/write; `Metadata` read-only) |
| Audit & Gateway Logs | Trace requests, guardrails, and MCP calls | Gateway UI and request logs recording status, guards, and protocol activity |
