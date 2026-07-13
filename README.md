<div align="center">

# SlowChrome

**SlowChrome is an AI-powered motorcycle customization platform that helps riders visualize future builds, discover relevant parts, and stay connected with motorcycle style trends and local events.**

<p>
  <img alt="Status" src="https://img.shields.io/badge/status-HTTPS%20MVP-blue">
  <img alt="Source" src="https://img.shields.io/badge/source-private-lightgrey">
  <img alt="Frontend" src="https://img.shields.io/badge/frontend-Next.js-black">
  <img alt="Backend" src="https://img.shields.io/badge/backend-FastAPI-009688">
  <img alt="Cloud" src="https://img.shields.io/badge/cloud-Azure%20VM-0078D4">
</p>

<p>
  <a href="#what-i-built">What I Built</a> |
  <a href="#project-highlights">Highlights</a> |
  <a href="#live-demo-and-media">Demo</a> |
  <a href="#observability-preview">Observability</a> |
  <a href="#tech-stack">Tech Stack</a> |
  <a href="docs/technical-case-study.md">Technical Case Study</a>
</p>

</div>

---

## What This Repository Is

This is a public portfolio showcase for SlowChrome, built for recruiters and interviewers. It summarizes the product, my role, and the strongest engineering signals without exposing the private production source code.

> Production source code is private. I can discuss architecture, implementation decisions, tradeoffs, and selected code during interviews.

## What I Built

I built the full-stack MVP end to end, from the Next.js product experience and FastAPI AI workflow to Docker/Azure deployment, CI/CD, authentication, cloud storage, and observability.

## Project Highlights

| Highlight | What it shows |
| --- | --- |
| **Full-stack customization platform** | Built a mobile-first Next.js product loop for style discovery, AI bike previews, parts direction, saved builds, and a culture feed. |
| **AI image workflow** | Added YOLOv8 photo validation before server-side OpenAI image generation. |
| **Cloud-backed garage** | Used Supabase Auth, Row Level Security, and private storage for account-owned saved builds. |
| **Production HTTPS deployment** | Deployed Dockerized frontend/backend services to an Azure VM behind a production domain and reverse proxy. |
| **CI/CD and recovery readiness** | Added GitHub Actions test/build gates, visual sanity checks, SHA-tag deployments, smoke tests, rollback workflow, runbooks, and Grafana observability. |

## Product Scope

SlowChrome is more than an AI image generator. The product direction includes:

- Future-build visualization from a rider's motorcycle photo.
- Personalized parts discovery based on the user's bike and build direction.
- A cloud garage for saved builds.
- A biweekly explore feed for motorcycle customization news, style updates, and local events.

## Live Demo and Media

**Live demo:** [https://theslowchrome.com](https://theslowchrome.com)

Product screenshots and a short walkthrough video are planned as public showcase assets after the next visual QA pass.

## Observability Preview

![SlowChrome Grafana observability preview](assets/grafana-observability-preview.png)

SlowChrome includes Grafana dashboards for backend golden signals, VM/container saturation, logs, traces, alerting, and deployment identity. More screenshots and architecture context are available in the [Technical Case Study](docs/technical-case-study.md#observability-evidence).

## Tech Stack

**Tech Stack:** Next.js, React, TypeScript, Tailwind CSS | FastAPI, YOLOv8, OpenAI Images | Supabase Auth/Storage | Docker, GitHub Actions, Azure VM, HTTPS reverse proxy | Playwright, Prometheus, Grafana, Loki, Tempo, OpenTelemetry, Alertmanager.

## Technical Deep Dive

For architecture diagrams, deployment flow, observability details, security boundaries, and engineering tradeoffs, see the [Technical Case Study](docs/technical-case-study.md).

## Repository Boundary

This public repository intentionally excludes application source code, environment files, API keys, private logs, user data, and unredacted provider screenshots. It includes only portfolio-safe project summary material.
