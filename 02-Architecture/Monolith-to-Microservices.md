# Monolith to Microservices

## Purpose

Use this playbook when considering or executing a decomposition of a monolith into microservices. It centers on business drivers, bounded contexts, and data ownership rather than technology for its own sake, and pushes toward an incremental strangler-pattern migration instead of a risky big-bang rewrite.

---

## Level 1 Checklist

### 🔍 Assess

- [ ] Business driver for splitting is explicit (independent deploys, team scaling, isolation of failure domains)
- [ ] Confirmed the problem is organizational/deployment coupling, not solvable within the monolith
- [ ] Current pain points mapped to specific modules, not "the whole thing is slow"
- [ ] Team's operational maturity (CI/CD, monitoring, on-call) assessed as ready for distributed systems
- [ ] Modular monolith considered first: would well-defined module boundaries within a single deployable solve the problem without the distributed systems tax?
- [ ] Conway's Law check: does current team structure actually support the proposed service boundaries, or would the split fight the org chart?

### 💡 Design Boundaries

- [ ] Bounded contexts identified using domain language, not database tables
- [ ] Each candidate service has a single clear owning team
- [ ] Data ownership per entity assigned to exactly one service
- [ ] Shared/ambiguous data flagged and resolved before splitting (no shared database across services)
- [ ] Synchronous vs asynchronous communication decided per boundary, with consistency implications understood
- [ ] Event-driven communication considered for boundaries that can tolerate eventual consistency
- [ ] API contracts defined before splitting, not reverse-engineered from the monolith's internal calls after
- [ ] SLOs defined for each new service boundary (a boundary without an SLO is just a distributed function call)

### ⚙️ Plan Migration

- [ ] Strangler pattern applied: new service intercepts traffic incrementally, monolith shrinks over time
- [ ] Extraction order prioritized by lowest coupling / highest pain first
- [ ] Dual-write or change-data-capture strategy defined for data migration
- [ ] Infrastructure tax calculated upfront: additional CI/CD pipelines, deployments, on-call surfaces, service mesh, distributed tracing cost
- [ ] Shared libraries / common concerns planned across services (auth, logging, tracing) so each team doesn't reinvent them inconsistently
- [ ] Rollback path exists at every extraction step

### ⚙️ Execute

- [ ] Feature flag or routing layer controls traffic shift between old and new paths
- [ ] Data migrated with a validated backfill and reconciliation process
- [ ] Old code path kept alive until new path is proven, then removed deliberately
- [ ] Cross-service transactions replaced with sagas or eventual consistency where needed

### ✅ Verify

- [ ] Latency and error rates compared old path vs new path before full cutover
- [ ] Distributed tracing confirms request flow across the new service boundary
- [ ] Services confirmed independently deployable — if they can't ship without coordinating with each other, this is a distributed monolith, not a real split
- [ ] On-call runbook updated for the new service's failure modes
- [ ] Monolith's removed code path fully decommissioned, not left as dead weight

---

## Notes

Resist extracting a service until its bounded context and data ownership are unambiguous — a premature split just moves the coupling into the network, where it's harder to see and slower to fix. If independent deployability isn't achieved, all the distributed-systems cost was paid for none of the benefit.
