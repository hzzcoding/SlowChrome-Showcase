<div align="center">

# SlowChrome — Cloud-Native Operations Case Study

**A working motorcycle-customization MVP operated on Azure, with a time-boxed AKS environment used to apply cloud-native delivery, observability, and recovery practices.**

<p>
  <a href="https://theslowchrome.com">Live Application</a> ·
  <a href="#project-highlights">Project Highlights</a> ·
  <a href="docs/technical-case-study.md">Technical Case Study</a>
</p>

</div>

---

> **Repository boundary:** Public, documentation-only portfolio repository with
> sanitized architecture and operational artifacts. Application source, secrets,
> and production access data are not included.

## Project Highlights

SlowChrome is a working web application for motorcycle riders to explore
AI-assisted customization ideas, discover motorcycle styles, and learn about
customization culture. It is built with Next.js, FastAPI, YOLOv8, OpenAI
Images, and Supabase. This repository focuses on its operational evolution: a
practical Docker Compose deployment on Azure, local Kubernetes practice in
Minikube, and a time-boxed AKS environment for applying cloud-native delivery,
observability, and recovery practices to the same application.

| What I built | Why it matters | Details |
| --- | --- | --- |
| Terraform-managed Azure foundation | Infrastructure changes are reviewable and repeatable rather than console-only. | [Terraform-managed foundation](docs/technical-case-study.md#terraform-managed-foundation) |
| GitHub Actions → Azure OIDC → AKS delivery | CI can deploy immutable images without storing a long-lived Azure secret in GitHub. | [Release workflow and workload identity](docs/technical-case-study.md#release-workflow-and-workload-identity) |
| Helm-managed frontend and private backend | The application is deployed as Kubernetes workloads with explicit rollout and rollback behavior. | [AKS topology](docs/technical-case-study.md#4-aks-runtime-topology) |
| Metrics, logs, traces, dashboards, and alerts | Diagnosis is based on correlated operational signals instead of SSH-only debugging. | [Observability](docs/technical-case-study.md#5-kubernetes-observability) |
| Recovery and resilience drills | A bad configuration, Pod loss, internal alert flow, and planned node maintenance were exercised in a managed cluster. | [Recovery evidence](docs/technical-case-study.md#6-recovery-and-resilience-drills) |

## Operating the MVP on a VM, Exercising AKS in Parallel

SlowChrome was built first as a working product MVP, not as an infrastructure
exercise. Its public application currently runs on an Azure Regular VM, which
fits the product's present traffic and operating needs.

Alongside the product work, I used the same application locally with Minikube
and then in a time-boxed AKS environment to apply cloud-native delivery,
observability, and recovery practices against a real workload. AKS was not a
public migration: the current product does not justify its ongoing cost and
operational complexity, so the cluster is paused. Any return to service or
teardown requires a separate lifecycle and cost decision.

The [VM observability baseline](assets/grafana-observability-preview.png)
captures the current single-host operating model that motivated the parallel
AKS work.

| Dimension | Current production: Azure Regular VM | AKS evidence environment: paused |
| --- | --- | --- |
| Public traffic | Serves the public application at `theslowchrome.com`. | Does not receive public DNS or sustained public traffic. |
| Infrastructure | The VM network security group is managed with Terraform; the application runs with Docker Compose. | Terraform manages the AKS foundation: network, AKS, ACR, Key Vault, workload identity, and the Gateway API profile. |
| Release path | A push to `main` runs quality gates, builds Docker Hub images, and deploys through a self-hosted runner with Docker Compose, smoke tests, and recovery behavior. | An explicitly confirmed manual workflow runs quality gates, uses Azure OIDC, builds or reuses immutable ACR images, and releases through Helm. |
| Runtime and operations | Next.js, private FastAPI, and the VM observability stack run on one host. | Frontend/backend Kubernetes workloads, Kubernetes observability, and controlled resilience drills were exercised. |
| Current decision | Proportionate long-term runtime for the product's present needs. | Time-boxed operations environment; paused pending a separate lifecycle and cost decision. |

## Recovery and Resilience Drills

Controlled AKS drills exercised invalid readiness configuration, Pod loss,
internal alert flow, and planned node maintenance. The [technical case
study](docs/technical-case-study.md#6-recovery-and-resilience-drills) records
what each drill validated.

## Scope and Current State

| Verified | Not claimed or intentionally deferred |
| --- | --- |
| Current production on the Azure Regular VM; AKS foundation, OIDC delivery, Helm workloads, Kubernetes observability, and the recovery drills above | AKS DNS cutover, trusted public TLS on AKS, external Slack/email/PagerDuty paging, SLO compliance, or multi-region HA |
| Docker Compose VM baseline and its operational evidence | AKS remains paused; its teardown or any return to service requires a separate lifecycle and cost decision |

For the architecture, implementation choices, exact drill scope, and remaining
work, read the [technical case study](docs/technical-case-study.md).

## Technology Snapshot

| Layer | Technologies |
| --- | --- |
| Application | Next.js, React, TypeScript, FastAPI, Python, YOLOv8 |
| Data and AI | Supabase Auth/Postgres/Storage, OpenAI Images |
| Baseline runtime | Docker Compose, Azure VM, HTTPS reverse proxy |
| Cloud-native evidence | AKS, Terraform, Helm, Azure Container Registry, Key Vault, Workload Identity, Gateway API |
| Delivery | GitHub Actions, Azure OIDC, immutable image tags, rollout checks |
| Observability | Prometheus, Grafana, Loki, Tempo, Alloy, OpenTelemetry, Alertmanager |
