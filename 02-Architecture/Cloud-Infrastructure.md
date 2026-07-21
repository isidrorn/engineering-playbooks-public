# Cloud Infrastructure

## Purpose

Use this checklist when making or reviewing infrastructure and cloud architecture decisions — provider topology, networking, identity, compute, IaC, cost, and resilience. It exists to pull back the non-obvious trade-offs that are easy to forget when it's been a while since you last had to reason about where and how workloads actually run.

---

## Level 1 Checklist

### 🔍 Provider & Topology

- [ ] Cloud vs on-prem vs hybrid decision made explicitly and justified, not inherited by default
- [ ] Single-cloud vs multi-cloud trade-off weighed deliberately (portability and negotiating leverage vs operational and skill-set complexity)
- [ ] Region/availability-zone strategy matched to latency, compliance, and disaster-recovery requirements — not just "wherever is cheapest"
- [ ] Vendor lock-in risk assessed per layer (compute, managed data stores, proprietary glue services) and consciously accepted or mitigated with an abstraction boundary
- [ ] Data residency and sovereignty requirements checked against where data actually gets replicated, backed up, and processed — not just where it's first written
- [ ] Exit cost estimated (data egress volume, re-platforming effort) before committing to a provider-specific managed service

### 💡 Networking

- [ ] Network segmentation follows least privilege — public/private subnet boundaries clear, nothing stateful reachable directly from the public path
- [ ] Firewall/security-group rules default-deny, least-privilege, and reviewed for stale broad rules left over from debugging
- [ ] DNS strategy defined (internal vs external resolution, TTLs sized for how fast you need failover to propagate)
- [ ] Egress cost and latency understood, especially cross-AZ and cross-region traffic that looks free in a diagram but isn't on the bill
- [ ] Private connectivity considered for sensitive internal or inter-service traffic instead of routing over the public internet
- [ ] Network topology diagrammed and kept current, not tribal knowledge in one person's head

### 🔍 Identity & Access

- [ ] IAM roles follow least privilege — no wildcard/blanket permissions granted for convenience
- [ ] Service-to-service auth uses short-lived, auto-rotated credentials, not long-lived static keys checked into config
- [ ] Break-glass/emergency access procedure exists, is documented, and has actually been tested — not just written down and forgotten
- [ ] Access reviewed and pruned on a cadence (stale roles, unused service accounts, orphaned permissions from people who've left or changed teams)
- [ ] Separation of duties enforced between environments — prod access is deliberate and audited, not a casual extension of dev access
- [ ] Cross-account/cross-project trust relationships enumerated — it's easy to lose track of who can assume what into where

### ⚙️ Compute & Orchestration

- [ ] Workload lifecycle matched to the right compute model (long-running vs bursty vs event-driven) rather than defaulting to one pattern for everything
- [ ] Autoscaling policies tested under real load, not just configured and assumed to work
- [ ] Resource requests/limits set deliberately to avoid noisy-neighbor effects on shared infrastructure
- [ ] Failure domains of the orchestration platform understood — what actually happens when a node dies, a zone goes dark, or the control plane itself degrades
- [ ] Stateful workloads' data locality and persistence handled deliberately (which volumes follow the workload, which don't, what happens on rescheduling)
- [ ] Cold-start and warm-up behavior understood for anything that scales from zero — the first request after idle is not the steady-state request

### ⚙️ Infrastructure as Code

- [ ] Infrastructure defined in code and version-controlled — no significant manual changes made directly against a live environment
- [ ] Infrastructure changes go through the same review process as application code, not a lighter-touch rubber stamp
- [ ] Drift between IaC and actual live state is detected on a cadence, not discovered during an incident
- [ ] Secrets are never committed to IaC repositories — referenced from a secrets manager instead
- [ ] State/backend access is controlled, encrypted, and itself backed up (losing state is losing the map to everything that exists)
- [ ] Modules/templates reused across environments instead of copy-pasted, so a fix in one place actually propagates
- [ ] Blast radius of a single IaC change understood before applying — does one `apply` touch one service or the whole account

### 💡 Cost Management

- [ ] Cost allocation tags/labels in place per team or service, enforced at creation time rather than backfilled later
- [ ] Budget alerts configured before overspend becomes a surprise on the monthly bill
- [ ] Unused/orphaned resources (idle volumes, unattached IPs, forgotten snapshots) cleaned up on a cadence
- [ ] Committed/reserved capacity considered for stable steady-state load instead of paying on-demand rates indefinitely
- [ ] Cost reviewed as part of the architecture decision itself, not bolted on after the bill arrives
- [ ] Cost of redundancy (multi-AZ, multi-region, cross-region replication) weighed explicitly against the availability it buys

### ✅ Resilience

- [ ] Redundancy across failure domains is the default for anything stateful, not an afterthought added post-incident
- [ ] Health checks reflect real readiness (dependencies checked), not just process liveness
- [ ] Single points of failure in the control plane or shared services (DNS, secrets manager, identity provider) explicitly identified
- [ ] Infra-layer failure injection tested — node loss, AZ loss, dependency degradation — cross-reference `Disaster-Recovery.md`
- [ ] Rollback path for infrastructure changes exists and has been exercised, not just for application deploys
- [ ] Backup restore path tested end to end, including for the infrastructure that restores infrastructure (not just application data)

---

## Notes

Treat this as a periodic review companion for anything long-lived, not a one-time gate. Revisit Cost Management and Provider & Topology whenever traffic or contract terms change materially — decisions that were right at one scale quietly stop being right at another. The most expensive infrastructure mistakes are rarely the ones that fail loudly; they're the ones that work fine until the one time a zone, a credential, or a state file goes missing.
