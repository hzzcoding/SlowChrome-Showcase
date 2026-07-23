# Assets

This directory is reserved for public, non-sensitive showcase assets.

Current evidence assets include:

- `aks-observability-dashboard.png` - sanitized Grafana overview from the AKS
  evidence environment.
- `aks-observability-signals.png` - sanitized application/Kubernetes signal
  view used by the recovery evidence.
- `grafana-*.png` - sanitized observability evidence from the original VM
  baseline.

All dashboard images are static portfolio artifacts. They must remain free of
credentials, user data, cloud resource identifiers, IP addresses, tokens, and
raw logs.

Recommended files:

- `architecture.png` - polished architecture diagram exported from the README Mermaid diagram.
- `dashboard.png` - Grafana dashboard screenshot with hosts, IPs, emails, and secrets redacted.
- `alerts.png` - Alertmanager or Grafana alerting overview screenshot with private values redacted.
- `ci-cd.png` - GitHub Actions pipeline screenshot with secret names only, never secret values.

Do not add:

- `.env` files
- API keys
- Supabase service-role keys
- raw logs containing user data
- screenshots with access tokens, private emails, or unredacted IPs
- application source code
