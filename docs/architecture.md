# Architecture

## System Overview

This qualifier uses a two-agent setup:

```
Human User → Hermes Agent → OpenClaw → Ollama Local Model
```

---

## Agents

### Hermes Agent — Brain

Hermes is used as the orchestration layer.

**Responsibilities:**
- Planning tasks
- Remembering project details
- Running reusable skills
- Coordinating development workflow

**Model:**
- Provider: Ollama (local)
- Model: `qwen2.5-coder-64k`

### OpenClaw — Hands

OpenClaw is used as the coding/execution agent.

**Responsibilities:**
- Code generation
- File creation planning
- Command/task execution workflow
- Reporting generated actions

**Model:**
- Provider: Ollama (local)
- Model: `qwen2.5-coder:7b`

---

## Model Routing

| Agent | Model |
|---|---|
| Hermes | `qwen2.5-coder-64k` |
| OpenClaw | `qwen2.5-coder:7b` |

**Reason:** Both are free local models running on Ollama. This avoids paid APIs and rate limits.

---

## Slack Channel Scheme

Planned Slack channels:

| Channel | Purpose |
|---|---|
| `#sprint-main` | Human-to-Hermes planning channel |
| `#agent-coder` | OpenClaw coding task channel |
| `#agent-log` | Raw logs and evidence |

**Status:** The Slack plugin installation was completed, but full live-loop verification was not completed before the submission deadline.

---

## Evidence

Evidence is stored in:
- `screenshots/openclaw_evidence/`
- `screenshots/hermes_evidence/`
- `recordings/`