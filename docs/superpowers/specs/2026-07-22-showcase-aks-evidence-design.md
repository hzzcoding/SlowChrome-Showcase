# SlowChrome Showcase AKS Evidence Design

## Goal

Update the public documentation-only Showcase so a recruiter can understand the
project's cloud-native operations evidence in under one minute, while a technical
interviewer can follow the Azure, Kubernetes, CI/CD, observability, and recovery
details without seeing private source, credentials, or infrastructure identifiers.

## Audience and document roles

| Document | Primary reader | Job |
| --- | --- | --- |
| `README.md` | recruiter, hiring manager, fast-scanning interviewer | Establish the product, the cloud-native outcome, selected proof, and an honest current-status boundary. |
| `docs/technical-case-study.md` | SRE/DevOps/Cloud interviewer | Explain decisions, delivery path, observability, measured drills, recovery limits, and tradeoffs. |
| private SlowChrome evidence records | project owner and technical audit | Retain detailed timestamps, workflows, implementation diagnosis, and full acceptance checks. |

## Public claim boundary

The public Showcase may claim the following because the private source repository
has merged acceptance evidence:

- Terraform-managed Azure foundation and GitHub-to-Azure OIDC delivery;
- immutable-image AKS delivery through Helm;
- Kubernetes-native metrics, logs, traces, dashboards, and Alertmanager;
- controlled invalid-readiness, frontend Pod-loss, backend Pod-loss, alert-pipeline,
  and workload-node-drain exercises with the recorded measurements; and
- a short-lived AKS evidence environment running in parallel with the existing VM.

It must not claim high-traffic production AKS, trusted public TLS on AKS,
external email/Slack/PagerDuty paging, a completed SLO observation window,
multi-region HA, a completed Regular VM migration, DNS cutover, or AKS teardown.

## README design

The README becomes a recruiter-facing landing page with this order:

1. Hero: project name, factual badges, concise cloud-native outcome, and links.
2. Repository boundary: documentation and sanitized evidence only; private source
   remains private.
3. Recruiter scan: product context, what was built, why the AKS work matters, and
   direct evidence links.
4. Before/after architecture: one Mermaid diagram showing the Spot-VM baseline
   beside the temporary AKS evidence path, without implying a DNS cutover.
5. Evidence gallery: the existing VM Grafana preview plus the two sanitized AKS
   dashboard screenshots.
6. Cloud-native proof: Terraform, OIDC, Helm, immutable delivery, observability,
   and recovery-drill table.
7. Honest status: implemented/evidenced, next operational step, and deliberately
   unclaimed capabilities.
8. Short interview prompts and a link to the technical case study.

The README will retain enough product context to show that the platform is a real
application, but prioritizes the DevOps/SRE story over installation instructions.

## Technical Case Study design

The case study keeps the current VM baseline and expands it into an evidence-led
"baseline to AKS" narrative:

1. Executive summary with a status table separating VM production baseline from
   the temporary AKS evidence environment.
2. VM baseline architecture and operational limitation.
3. AKS architecture and delivery flow: Terraform, remote state, GitHub OIDC, ACR,
   Key Vault/Workload Identity, Helm, Gateway, and application workloads.
4. Observability implementation: Prometheus, Grafana, Loki, Tempo, Alloy, OTel,
   Alertmanager, bounded PVCs, and private access.
5. Measured recovery evidence with exact scope:
   - invalid readiness: MTTD 370s, MTTR 383s;
   - frontend Pod loss: MTTD 8s, MTTR 9s;
   - backend Pod loss: MTTD 7s, MTTR 14s;
   - alert pipeline: MTTD 41s, MTTR 345s, internal Alertmanager only;
   - node drain: 15s drain completion and 28s controlled maintenance recovery,
     not incident MTTD.
6. Operational lessons: OTel/Prometheus/Loki integration contracts, non-root Alloy
   writable state, ConfigMap checksum rollout, and a PDB-guarded control-plane
   reschedule.
7. Cost/security boundaries and remaining work.

## Assets and redaction

Copy the two already-sanitized AKS dashboard screenshots from the private source
repository into `assets/` using descriptive names. Do not copy raw logs, cluster
identifiers, internal IPs, kubeconfig material, provider resource names, tokens,
or dashboard screenshots containing those values.

## Verification

- Validate Markdown headings, relative links, Mermaid fences, and image paths.
- Scan public Markdown for IP addresses, Azure resource IDs, tokens, kubeconfig,
  internal URLs, and credential-looking values.
- Confirm the README and case study distinguish implemented/evidenced from planned.
- Review the rendered top section and screenshot placement before publishing.
