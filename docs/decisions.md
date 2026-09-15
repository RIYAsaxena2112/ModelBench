# Decisions Log

Running record of real decisions made while building this, and why.

## 2026-09-12 — Scope: build the pilot, not the production doc
The production-scale doc (K8s, Terraform, multi-tenancy, SOC 2) describes a
sales-pitch architecture for selling this to external clients. This build
targets the pilot design only, on free-tier infrastructure. The production
doc is retained as a forward-looking "path to scale" reference, not something
implemented here.

## 2026-09-12 — Infra substitutions for zero budget
- Oracle Cloud Always Free VM instead of managed Kubernetes
- Docker Compose instead of Argo Workflows / KEDA
- LiteLLM routed to OpenRouter free models / Gemini free tier / Groq free tier
  instead of paid Anthropic API for the bulk of the sweep; Claude added later
  via config change for a small spot-validation run
- Self-hosted Grafana/Prometheus/Loki/Langfuse instead of managed services
- GitHub Actions instead of ArgoCD/GitOps (no cluster to reconcile at this scale)
