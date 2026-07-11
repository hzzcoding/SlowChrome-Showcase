# Assets

This directory is reserved for public, non-sensitive showcase assets.

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

