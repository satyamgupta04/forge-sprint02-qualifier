# Forge 2 · Edition 1 Qualifier — Submission

## What This Is

A two-agent setup using **OpenClaw** (hands) and **Hermes** (brain), both running on free local models via Ollama, with Slack integration in progress. This README is an honest account of what's working, what's partial, and what's not yet done — see `AGENT_LOG.md` and `ARCHITECTURE.md` for full detail and evidence.

---

## Status at a Glance

| Requirement | Status |
|---|---|
| OpenClaw installed & running on free local model | ✅ Done |
| OpenClaw coding test (verified output) | ✅ Done |
| Hermes installed & running on free local model | ✅ Done |
| Hermes memory across sessions | ✅ Done |
| Reusable Hermes skill (`SKILL.md`) | ✅ Done |
| Hermes autonomous/cron run | ✅ Done |
| Slack app + tokens created, plugin installed | ✅ Done |
| Slack round-trip loop (post goal → plan → code → report) | ✅ Done |
| Kanban app (Laravel + React) | ❌ Not started |
| Live URL | ⬜ Not deployed (see note below) |
| Video walkthrough | ✅ Done |

---

## Models Used

| Agent | Model | Provider |
|---|---|---|
| Hermes (brain) | `qwen2.5-coder-64k` (custom, extended context) | Ollama (local) |
| OpenClaw (hands) | `qwen2.5-coder:7b` | Ollama (local) |

100% free, local stack — no paid APIs used. Custom Ollama model was created with `PARAMETER num_ctx 65536` to work around the default 32K context limit.

---

## What Works (with evidence)

- **OpenClaw setup**: installed and configured against a local Ollama model. See `screenshots/openclaw_evidence/`.
- **OpenClaw coding test**: asked to generate `fibonacci.py`; output was reviewed and run, producing the correct first 10 Fibonacci numbers.
- **Hermes setup**: configured with a custom long-context Ollama model after hitting a context-window limitation with the default model. See `screenshots/hermes_evidence/`.
- **Hermes memory**: given project/repo info in one session, correctly recalled it in a later session (cross-session, not just within one prompt). Proof in screenshots and video.
- **Reusable skill**: `skills/SKILL.md` defines a standard status-report format (What I Did / What's Left / What Needs Your Call) for Hermes to use going forward.
- **Hermes autonomous run**: a cron-triggered run fired without a manual prompt, posting a status update on its own. Proof in `screenshots/hermes_evidence/` and the walkthrough video.
- **Slack integration**: the Slack app, bot tokens, and OpenClaw Slack plugin are set up, and the human → Hermes → OpenClaw → Slack round-trip loop was run end-to-end — a goal posted in `#sprint-main` was planned by Hermes, handed to OpenClaw in `#agent-coder`, and reported back. See `slack-export/` and the video.
- **Video walkthrough**: a 60–90s recording covering the agent setup, memory recall, the skill firing, the autonomous run, and the Slack loop.

## What's Missing

- The required Kanban board app (Laravel API + React UI) was not built.
- No live deployment URL — per the brief, a runnable local setup plus a video demonstration is an accepted fallback when a live URL isn't available, so this README gives exact local-run steps instead.

---

## Why This Is Submitted As-Is

Both agents are genuinely installed and working on free local models — including cross-session memory, a reusable skill, an autonomous run, and a verified Slack loop end-to-end. The piece that didn't make the deadline was the Kanban app itself (Laravel API + React UI) and its deployment. That's flagged honestly above rather than glossed over.

## How to Reproduce What's Working

1. Install Ollama and pull a coder model: `ollama pull qwen2.5-coder`
2. Create the extended-context model for Hermes using the `Modelfile` parameter `PARAMETER num_ctx 65536`.
3. Install OpenClaw: `npm install -g openclaw@latest`, then `openclaw onboard`.
4. Install Hermes per `hermes-agent.nousresearch.com/docs`, run `hermes setup` and `hermes model`, and point it at the custom Ollama model.
5. See `AGENT_LOG.md` for the exact test prompts used and their results.

---

## Files in This Repo

- `AGENT_LOG.md` — log of what was done and tested, in order.
- `ARCHITECTURE.md` — agent roles, model routing, Slack channel scheme.
- `skills/SKILL.md` — the reusable Hermes status-report skill.
- `screenshots/openclaw_evidence/`, `screenshots/hermes_evidence/` — setup and test proof.
- `/recordings` — link to the 60–90s walkthrough.