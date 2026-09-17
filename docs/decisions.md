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

## 2026-09-16 — Deferred cloud VM, building local-first
Oracle Cloud Always Free signup blocked: Oracle rejects PIN-based debit cards
(most Indian debit cards), only accepts credit cards or debit cards that
function like one. Rather than block Phase 0 on resolving a card, the plan is
to build and validate everything locally via Docker Compose first — this was
already the pilot doc's own Week 1-3 approach anyway. Cloud hosting (Oracle,
or an alternative) is revisited later, only once a public/always-on
deployment is actually needed (e.g. for a live dashboard demo), at which
point it's a hosting decision made with working software behind it rather
than a blocker on day one.