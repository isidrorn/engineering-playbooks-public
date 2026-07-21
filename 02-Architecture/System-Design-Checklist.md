# System Design Checklist

## Purpose

Use this checklist when designing a new system or service from scratch, or when reviewing someone else's design before it gets built. It walks through requirements, scale, data, APIs, infrastructure, security, and observability so nothing load-bearing gets skipped in the excitement of drawing boxes and arrows.

---

## Level 1 Checklist

### 🔍 Requirements
□ Functional requirements written down and agreed with stakeholders
□ Non-functional requirements defined (latency, availability, durability targets)
□ In-scope vs out-of-scope explicitly stated
□ Read/write ratio and access patterns understood

### 💡 Scale
□ Expected traffic today and in 12-24 months estimated (QPS, data volume, concurrent users)
□ Peak vs average load considered, not just averages
□ Growth assumptions sanity-checked against business projections
□ Single point of scale bottleneck identified (DB, queue, gateway)

### ⚙️ Data
□ Consistency model chosen deliberately (strong vs eventual) and justified
□ Data ownership per entity is unambiguous
□ Schema/storage engine matches access pattern (read-heavy, write-heavy, analytical)
□ Retention, archival, and deletion policy defined
□ Backup and restore path exists and has been tested

### ⚙️ APIs
□ Contract defined (request/response shape, versioning strategy)
□ Idempotency handled for retried writes
□ Pagination, filtering, and rate limits designed in from the start
□ Backward compatibility strategy for future changes

### ⚙️ Infrastructure
□ Deployment topology matches availability requirements (multi-AZ, multi-region if needed)
□ Failure modes for each dependency identified (what happens when it's down/slow)
□ Timeouts, retries, and circuit breakers placed at every network boundary
□ Capacity headroom and autoscaling triggers defined

### 🔍 Security
□ AuthN/AuthZ model defined for every entry point
□ Sensitive data classified and encryption at rest/in transit confirmed
□ Least-privilege access enforced between components
□ Abuse/rate-limiting protections in place for public-facing endpoints

### ✅ Observability
□ Golden signals identified (latency, traffic, errors, saturation) with owners
□ Alerting thresholds tied to user-facing impact, not just resource usage
□ Distributed tracing covers the critical path end-to-end
□ Dashboards exist before launch, not after the first incident

### 📝 Trade-offs
□ Alternatives considered and rejection reasons documented
□ Known limitations and technical debt called out explicitly
□ Decision recorded somewhere durable (ADR, design doc) for future readers

---

## Notes

Treat this as a design review companion, not a gate to pass once. Revisit the Scale and Data sections whenever traffic assumptions change materially.
