
A multi-model, multi-agent coding evaluation harness — compares AI coding models
(Claude, open-weight alternatives) on real engineering tasks under identical
conditions, scored on correctness, quality, cost, and latency.

This is a real, working build of the pilot design (see `docs/`), running entirely
on free-tier infrastructure:

- **Compute:** Oracle Cloud Always Free VM (Docker + Docker Compose)
- **Orchestration:** Harbor + harbor-rewardkit
- **Model routing:** LiteLLM, fronting free-tier providers (OpenRouter free models,
  Google Gemini free tier, Groq free tier) — swappable to Claude via one config
  change once budget allows
- **Observability:** self-hosted Grafana + Prometheus + Loki + Langfuse
- **CI/CD:** GitHub Actions (free tier)

## Status

🚧 Early setup — see `docs/decisions.md` for the running log.

## Structure

- `contracts/` — versioned interface schemas (agent, model, task, trace)
- `plugins/agents/` — pluggable agent implementations (opencode default)
- `router/` — LiteLLM config
- `tasks/internal/` — task definitions (repo + instruction + hidden tests)
- `tests/` — hidden tests, reward split (objective vs. judged quality)
- `observability/` — OTel collector, Grafana dashboards, Langfuse config
- `storage/` — local artifact storage config (pilot phase)
- `scripts/` — sweep and regrade scripts
- `docs/` — decisions log, pitfalls log, design docs
