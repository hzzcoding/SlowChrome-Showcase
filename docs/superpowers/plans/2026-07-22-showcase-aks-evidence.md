# SlowChrome Showcase AKS Evidence Implementation Plan

> **For the project owner:** This plan is executed on the isolated
> `codex/showcase-aks-evidence` branch. It updates public documentation and
> sanitized screenshot assets only; it does not change Azure, AKS, DNS, or the
> application runtime.

**Goal:** Turn the documentation-only Showcase into a recruiter-readable and
technically defensible account of the completed AKS evidence work, without
overstating the temporary environment as a full production cutover.

**Architecture:** Keep the README as a concise landing page and make the
technical case study the evidence-led technical deep dive. Reuse only
sanitized dashboard screenshots from the private project evidence directory.

**Tech Stack:** GitHub-flavored Markdown, Mermaid, PNG evidence assets, GitHub.

---

### Task 1: Add safe AKS evidence assets

**Files:**
- Create: `assets/aks-observability-dashboard.png`
- Create: `assets/aks-observability-signals.png`
- Modify: `assets/README.md`

**Steps:**
1. Copy the two pre-sanitized AKS dashboard screenshots from the private source
   evidence directory with descriptive public names.
2. Confirm both are PNG files and inspect their dimensions.
3. Update the public asset inventory with purpose and redaction boundary.
4. Verify that no raw logs, identifiers, kubeconfig files, or source code were
   added.

### Task 2: Rewrite the recruiter-facing README

**Files:**
- Modify: `README.md`

**Steps:**
1. Replace the previous VM-baseline/AKS-planned framing with a factual hero,
   repository boundary, quick links, and recruiter scan.
2. Add a parallel-environment Mermaid diagram so the AKS evidence environment
   is not confused with a DNS or production cutover.
3. Surface the sanitized evidence gallery, cloud-native implementation table,
   and measured-drill summary near the top.
4. Add a concise current-status boundary and interview prompts.
5. Verify every relative link, image reference, heading, and Mermaid fence.

### Task 3: Rewrite the technical case study

**Files:**
- Modify: `docs/technical-case-study.md`

**Steps:**
1. Preserve the single-VM baseline as context and distinguish it from the
   temporary AKS evidence environment.
2. Document Terraform, GitHub OIDC, image delivery, Helm, identity, and the
   ingress/workload topology at a level safe for a public repository.
3. Describe the observability architecture and its private-access, bounded
   storage boundaries.
4. Publish the exact recovery exercise measurements and label maintenance drain
   timing correctly rather than calling it incident MTTD/MTTR.
5. Record operational lessons, limitations, remaining work, and interview
   talking points.

### Task 4: Public-safety and publication verification

**Files:**
- Verify: `README.md`
- Verify: `docs/technical-case-study.md`
- Verify: `assets/`

**Steps:**
1. Run `git diff --check` and ensure expected Markdown/image files are the only
   changes.
2. Scan for IP addresses, Azure resource IDs, credential keywords, kubeconfig
   content, and private hostnames.
3. Programmatically check local Markdown links and image paths.
4. Review the public claims against the design document’s implemented versus
   unclaimed boundary.
5. Commit, push, open a ready-for-review PR, verify any checks, then merge under
   the standing authorization.
