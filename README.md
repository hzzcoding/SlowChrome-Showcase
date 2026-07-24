<div align="center">

# SlowChrome — Cloud-Native Operations Case Study

**An AI web application evolved from a single Azure VM into a real, time-boxed AKS evidence environment with Terraform, OIDC delivery, Helm, observability, and measured recovery exercises.**

<p>
  <img alt="Scope" src="https://img.shields.io/badge/scope-AKS%20evidence%20captured-326CE5">
  <img alt="Delivery" src="https://img.shields.io/badge/delivery-GitHub%20Actions%20%2B%20OIDC-2088FF">
  <img alt="Runtime" src="https://img.shields.io/badge/runtime-VM%20baseline%20%2B%20AKS-0078D4">
  <img alt="Observability" src="https://img.shields.io/badge/observability-metrics%20%7C%20logs%20%7C%20traces-F46800">
</p>

<p>
  <a href="https://theslowchrome.com">Product Demo</a> ·
  <a href="#project-highlights">Project Highlights</a> ·
  <a href="docs/technical-case-study.md">Technical Case Study</a>
</p>

</div>

---

> **Repository boundary:** this is a public, documentation-only portfolio
> repository. It contains sanitized architecture and operational evidence, not
> application source code, credentials, Terraform state, kubeconfig, private
> logs, Azure resource names, or user data.

## Project Highlights

SlowChrome is an AI-assisted motorcycle customization app built with Next.js,
FastAPI, YOLOv8, OpenAI Images, and Supabase. The operational story is more
important here than a list of tools: I began with a debuggable Docker Compose
deployment on Azure, then built and exercised a short-lived AKS environment to
validate a cloud-native delivery and recovery path. This repository documents
that operational work; it is not a mirror of the private application source.

| What I built | Why it matters | Evidence to inspect |
| --- | --- | --- |
| Terraform-managed Azure foundation | Infrastructure changes are reviewable and repeatable rather than console-only. | [Infrastructure as code](docs/technical-case-study.md#infrastructure-as-code) |
| GitHub Actions → Azure OIDC → AKS delivery | CI can deploy immutable images without storing a long-lived Azure secret in GitHub. | [CI/CD identity and release path](docs/technical-case-study.md#cicd-identity-and-release-path) |
| Helm-managed frontend and private backend | The application is deployed as Kubernetes workloads with explicit rollout and rollback behavior. | [AKS topology](docs/technical-case-study.md#4-aks-runtime-topology) |
| Metrics, logs, traces, dashboards, and alerts | Diagnosis is based on correlated operational signals instead of SSH-only debugging. | [Observability](docs/technical-case-study.md#5-kubernetes-observability) |
| Recovery and resilience drills | A bad configuration, Pod loss, internal alert-pipeline flow, and planned node maintenance were tested with timestamps. | [Recovery evidence](docs/technical-case-study.md#6-measured-recovery-exercises) |

## From VM Baseline to an AKS Evidence Environment

The Azure VM remains the original application baseline. AKS ran beside it as a
real, time-boxed environment for building and validating cloud-native delivery,
observability, and recovery practices—not as an immediate public migration.

The current application's traffic and operational needs do not justify the
ongoing cost and complexity of a permanent AKS runtime. The VM is therefore the
more proportionate long-term operating model, while AKS is paused as the
evidence and lifecycle decision are closed. This Showcase does **not** claim a
DNS cutover, sustained public AKS traffic, or that the VM has been retired.

The [VM observability baseline](assets/grafana-observability-preview.png)
captures the original single-host operating model that motivated the parallel
AKS work.

```mermaid
flowchart LR
    user["Browser"] --> vm["Existing Azure VM baseline\nNext.js + private FastAPI\nDocker Compose"]

    subgraph delivery["Cloud-native evidence path"]
        gha["GitHub Actions"] --> oidc["Azure OIDC"]
        oidc --> tf["Terraform-managed Azure foundation"]
        gha --> images["Immutable container images"]
        images --> helm["Helm release"]
    end

    subgraph aks["Temporary AKS evidence environment"]
        helm --> web["Next.js Deployment"]
        web --> api["Private FastAPI Deployment"]
        obs["Prometheus · Loki · Tempo\nGrafana · Alertmanager"]
        web --> obs
        api --> obs
    end
```

The value of this work is a concrete operating chain: infrastructure definition,
delivery identity, workload health, telemetry, controlled failure, and measured
recovery.

## What Was Built and Verified

| Capability | What was verified |
| --- | --- |
| Infrastructure foundation | Terraform created the Azure foundation for the evidence environment; state and credentials remained private. |
| Delivery identity | GitHub Actions authenticated to Azure through OIDC without requiring a long-lived Azure delivery credential in CI. |
| Release safety | Immutable images were released with Helm, readiness checks, rollout checks, and rollback behavior. |
| Observability | Prometheus, Grafana, Loki, Tempo, Alloy, OpenTelemetry Collector, and Alertmanager ran inside AKS. |
| Availability controls | Frontend/backend replicas, readiness probes, and a PodDisruptionBudget were exercised. |

## Recovery and Resilience Drills

These were intentional, scoped exercises in the AKS evidence environment to
validate detection and recovery behavior. They are not user-facing production
incidents or SLO measurements.

| Exercise | Measurement | What it demonstrates |
| --- | --- | --- |
| Invalid backend readiness configuration | Detection: **370 s** · recovery: **383 s** | A rejected configuration is visible and the workload returns to Ready after rollback. |
| Frontend Pod loss | Detection: **8 s** · recovery: **9 s** | A Deployment replaces a lost frontend Pod. |
| Backend Pod loss | Detection: **7 s** · recovery: **14 s** | A Deployment replaces a lost backend Pod. |
| Alert pipeline | Detection: **41 s** · clear: **345 s** | Prometheus-to-Alertmanager flow was observed internally. |
| Workload-node drain | Drain completion: **15 s** · controlled recovery: **28 s** | A PDB-guarded planned-maintenance drain reschedules workloads. |

The final row is planned-maintenance timing, not incident MTTD/MTTR. The full
method, timestamps, and caveats are in the [technical case study](docs/technical-case-study.md#6-measured-recovery-exercises).

## Scope and Current State

| Verified | Not claimed or intentionally deferred |
| --- | --- |
| AKS foundation, OIDC delivery, Helm workloads, Kubernetes observability, and the recovery drills above | AKS DNS cutover, trusted public TLS on AKS, external Slack/email/PagerDuty paging, SLO compliance, multi-region HA, or a completed VM migration |
| The original Docker Compose VM baseline and its operational evidence | AKS remains paused; its teardown or any return to service requires a separate lifecycle and cost decision |

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
