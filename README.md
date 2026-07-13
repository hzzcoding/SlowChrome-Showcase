<div align="center">

# SlowChrome SRE / DevOps Showcase

**A production-style deployment, observability, and release-safety showcase for an AI motorcycle customization web app.**

<p>
  <img alt="Status" src="https://img.shields.io/badge/status-HTTPS%20MVP-blue">
  <img alt="Source" src="https://img.shields.io/badge/source-private-lightgrey">
  <img alt="CI/CD" src="https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF">
  <img alt="Observability" src="https://img.shields.io/badge/observability-Grafana%20%7C%20Prometheus-F46800">
  <img alt="Cloud" src="https://img.shields.io/badge/cloud-Azure%20VM-0078D4">
</p>

<p>
  <a href="https://theslowchrome.com">Live Site</a> |
  <a href="#what-this-demonstrates">What This Demonstrates</a> |
  <a href="#observability-preview">Observability</a> |
  <a href="#tech-stack">Tech Stack</a> |
  <a href="docs/technical-case-study.md">Technical Case Study</a>
</p>

</div>

---

## What This Repository Is

This is a public SRE/DevOps portfolio showcase for SlowChrome. The application is an AI motorcycle customization product, but this repository focuses on the operational layer around it: deployment, CI/CD, observability, rollback readiness, and production boundaries.

> Production source code, secrets, private logs, environment files, and user data are intentionally excluded.

## What This Demonstrates

| Capability | Evidence |
| --- | --- |
| **Production deployment** | Dockerized Next.js and FastAPI services running on an Azure VM behind an HTTPS reverse proxy. |
| **CI/CD safety** | GitHub Actions build/test gates, visual sanity checks, SHA-tagged Docker images, deploy workflow, and post-deploy smoke tests. |
| **Observability** | Grafana dashboards backed by Prometheus, Loki, Tempo, OpenTelemetry, node-exporter, cAdvisor, and Alertmanager. |
| **Release traceability** | Deployment identity metrics, recorded current/previous release state, and immutable image tags tied to commits. |
| **Recovery readiness** | Manual rollback workflow, runbooks, ops/release logs, and smoke-test verification after deploys or rollback. |
| **Security boundaries** | Private backend port, server-side AI credentials, Supabase RLS/private storage, and tunnel-only monitoring access. |

## Observability Preview

![SlowChrome Grafana observability preview](assets/grafana-observability-preview.png)

The SRE focus of this project is the operating layer around the app: backend golden signals, VM/container saturation, Loki log search, Tempo traces, alert visibility, smoke tests, and deployment identity. Grafana is intentionally private and accessed through SSH tunnels; the screenshots in this repo are static portfolio evidence.

More observability screenshots and architecture context are available in the [Technical Case Study](docs/technical-case-study.md#observability-evidence).

## Tech Stack

**Application:** Next.js, React, TypeScript, FastAPI, YOLOv8, OpenAI Images, Supabase Auth/Storage.

**Platform and operations:** Docker, GitHub Actions, Azure VM, HTTPS reverse proxy, Playwright, Prometheus, Grafana, Loki, Tempo, OpenTelemetry, Alertmanager, node-exporter, cAdvisor.

## Case Study

For architecture diagrams, deployment flow, observability evidence, security boundaries, production-readiness notes, and engineering tradeoffs, see the [Technical Case Study](docs/technical-case-study.md).

## Boundary Note

This public repository is a showcase, not the production source repo. It contains portfolio-safe documentation, diagrams, and screenshots only.
