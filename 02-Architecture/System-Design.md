# System Design

## Purpose

Use this checklist when designing a new system or service from scratch, or when reviewing someone else's design before it gets built. It walks through requirements, scale, data, APIs, infrastructure, security, and observability so nothing load-bearing gets skipped in the excitement of drawing boxes and arrows.

---

## Level 1 Checklist

### 🔍 Requirements

- [ ] Functional requirements written down and agreed with stakeholders
- [ ] Non-functional requirements defined (latency, availability, durability targets)
- [ ] In-scope vs out-of-scope explicitly stated
- [ ] Read/write ratio and access patterns understood
- [ ] SLOs/SLIs defined per critical user journey, with an error budget attached
- [ ] Ownership boundaries between teams defined (who owns what, who gets paged)
- [ ] Multi-tenancy implications considered (data isolation, noisy-neighbor, per-tenant limits)
- [ ] Single hardest technical risk identified and flagged to spike first

### 💡 Diagram & Scale

- [ ] System diagrammed before building it (context diagram, component diagram, data flow) — see `Diagramming-Checklist.md`
- [ ] Expected traffic today and in 12-24 months estimated (QPS, data volume, concurrent users)
- [ ] Peak vs average load considered, not just averages
- [ ] Growth assumptions sanity-checked against business projections
- [ ] Single point of scale bottleneck identified (DB, queue, gateway)
- [ ] Read replicas / CQRS considered for read-heavy workloads
- [ ] Geo-distribution / data residency requirements identified (where data must live, where it must not)

### ⚙️ Data

- [ ] Consistency model chosen deliberately (strong vs eventual) and justified
- [ ] Data ownership per entity is unambiguous
- [ ] Schema/storage engine matches access pattern (read-heavy, write-heavy, analytical)
- [ ] Data lifecycle defined end to end (creation → access → archival → deletion)
- [ ] Schema evolution plan exists (how the model changes without breaking readers/writers)
- [ ] Retention, archival, and deletion policy defined
- [ ] Backup and restore path exists and has been tested

### ⚙️ APIs

- [ ] Contract defined (request/response shape, versioning strategy)
- [ ] Idempotency keys required on all write operations, not just the obviously risky ones
- [ ] Pagination, filtering, and rate limits designed in from the start
- [ ] Rate limiting strategy defined for both inbound traffic (protect this system) and outbound traffic (protect dependencies)
- [ ] Backward compatibility strategy for future changes

### ⚙️ Infrastructure

- [ ] Deployment topology matches availability requirements (multi-AZ, multi-region if needed)
- [ ] Failure modes for each dependency identified (what happens when it's down/slow)
- [ ] Graceful degradation plan exists per dependency (degrade a feature vs fail the whole request)
- [ ] Timeouts, retries, and circuit breakers placed at every network boundary
- [ ] Dead letter queue strategy defined for failed async operations (retry policy, alerting, replay path)
- [ ] Capacity headroom and autoscaling triggers defined

### 🔍 Security

- [ ] AuthN/AuthZ model defined for every entry point
- [ ] Sensitive data classified and encryption at rest/in transit confirmed
- [ ] Least-privilege access enforced between components
- [ ] Abuse/rate-limiting protections in place for public-facing endpoints

### ✅ Observability

- [ ] Golden signals identified (latency, traffic, errors, saturation) with owners
- [ ] Alerting thresholds tied to user-facing impact (SLO burn rate), not just resource usage
- [ ] Distributed tracing covers the critical path end-to-end
- [ ] Dashboards exist before launch, not after the first incident

### 📝 Trade-offs

- [ ] Alternatives considered and rejection reasons documented
- [ ] Known limitations and technical debt called out explicitly
- [ ] Decision recorded somewhere durable (ADR, design doc) for future readers

---

## Notes

Treat this as a design review companion, not a gate to pass once. Revisit the Scale and Data sections whenever traffic assumptions change materially. Spike the single hardest technical risk early — a design that looks complete on paper can still fail because the one uncertain part turned out to be the load-bearing one.
