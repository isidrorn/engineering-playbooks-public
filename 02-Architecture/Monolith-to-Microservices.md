# Monolith to Microservices

## Purpose

Use this playbook when considering or executing a decomposition of a monolith into microservices. It centers on business drivers, bounded contexts, and data ownership rather than technology for its own sake, and pushes toward an incremental strangler-pattern migration instead of a risky big-bang rewrite.

---

## Level 1 Checklist

### 🔍 Assess
□ Business driver for splitting is explicit (independent deploys, team scaling, isolation of failure domains)
□ Confirmed the problem is organizational/deployment coupling, not solvable within the monolith
□ Current pain points mapped to specific modules, not "the whole thing is slow"
□ Team's operational maturity (CI/CD, monitoring, on-call) assessed as ready for distributed systems

### 💡 Design Boundaries
□ Bounded contexts identified using domain language, not database tables
□ Each candidate service has a single clear owning team
□ Data ownership per entity assigned to exactly one service
□ Shared/ambiguous data flagged and resolved before splitting (no shared database across services)
□ Synchronous vs asynchronous communication decided per boundary, with consistency implications understood

### ⚙️ Plan Migration
□ Strangler pattern applied: new service intercepts traffic incrementally, monolith shrinks over time
□ Extraction order prioritized by lowest coupling / highest pain first
□ Dual-write or change-data-capture strategy defined for data migration
□ Contract between monolith and new service defined and versioned
□ Rollback path exists at every extraction step

### ⚙️ Execute
□ Feature flag or routing layer controls traffic shift between old and new paths
□ Data migrated with a validated backfill and reconciliation process
□ Old code path kept alive until new path is proven, then removed deliberately
□ Cross-service transactions replaced with sagas or eventual consistency where needed

### ✅ Verify
□ Latency and error rates compared old path vs new path before full cutover
□ Distributed tracing confirms request flow across the new service boundary
□ On-call runbook updated for the new service's failure modes
□ Monolith's removed code path fully decommissioned, not left as dead weight

---

## Notes

Resist extracting a service until its bounded context and data ownership are unambiguous — a premature split just moves the coupling into the network, where it's harder to see and slower to fix.
