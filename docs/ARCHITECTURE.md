# TELE33776 Lab 17 Architecture

## Overview

This setup routes AI coding harnesses and Model Context Protocol (MCP) tool requests through `agentgateway` so authentication, PII guardrails, token budgets, model routing, and logging stay centralized.

## Component Connections

- **Claude Code & Pi Harnesses:** Connect to `agentgateway` (`http://localhost:4000`) using scoped gateway keys (`AGW_CLAUDE_KEY`, `AGW_PI_KEY`) and model aliases (`fast` and `smart`).
- **agentgateway (v1.7.0):** Listens on port `4000` (with UI/admin endpoints), enforces key authentication, applies PII guardrails and token budgets, routes `fast` (`qwen3:1.7b`) and `smart` (`qwen3:4b`) to Ollama, and exposes the `/mcp` endpoint (`http://localhost:4000/mcp`).
- **Ollama (`localhost:11434`):** Runs local models (`qwen3:1.7b` and `qwen3:4b`) to serve chat/completion requests forwarded by `agentgateway`.
- **GitHub MCP & GitHub API:** `agentgateway` forwards authenticated MCP requests (`AGW_MCP_KEY`) using the fine-grained GitHub token (`GITHUB_MCP_PAT`) to interact with the `tele33776-lab17-agentgateway` repository (issues, branches, files, and pull requests).
