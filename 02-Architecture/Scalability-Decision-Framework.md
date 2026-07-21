# Scalability Decision Framework

## Purpose

Use this framework when a system is hitting a performance or scale ceiling and the instinct is to reach for a big architectural rewrite. The key insight: complexity is expensive and mostly irreversible, so evaluate solutions in ascending order of complexity and only escalate to the next rung when the current one is proven insufficient. Jumping straight to microservices or sharding without exhausting simpler options is the most common scalability mistake.

---

## Level 1 Checklist

Work top to bottom. Do not skip a rung — prove it's insufficient before moving to the next one.

### 🔍 Step 0 — Measure First

- [ ] Bottleneck identified with data (profiling, tracing, query plans), not guesswork
- [ ] Confirmed the bottleneck is actually server-side, not the client or the network (DNS, TLS handshake, client rendering, CDN misses)
- [ ] Confirmed it's a real user-facing problem, not a vanity metric
- [ ] Baseline numbers captured so improvement can be measured

### ⚙️ Step 1 — Optimize

- [ ] Slow queries, N+1 calls, and missing indexes checked
- [ ] Algorithmic complexity of hot paths reviewed
- [ ] Unnecessary work removed (redundant calls, over-fetching, serialization overhead)
- [ ] Serialization/deserialization overhead checked on hot paths (payload size, format choice, unnecessary re-parsing)
- [ ] Logging overhead checked on hot paths (log level, synchronous I/O, excessive structured-log payloads)
- [ ] Unnecessary middleware/interceptors checked (each one adds latency on every request, even when it does nothing)
- [ ] Config tuning tried (connection pools, batch sizes, timeouts)

### ⚙️ Step 2 — Scale Vertically

- [ ] Bigger instance/box evaluated as a stopgap
- [ ] Cost of vertical scaling compared against engineering time for alternatives
- [ ] Ceiling of vertical scaling for this workload understood (when does this stop working?)

### ⚙️ Step 3 — Scale Horizontally (Stateless)

- [ ] Service confirmed stateless or made stateless before adding instances
- [ ] Load balancing and health checks in place
- [ ] Autoscaling triggers defined and tested

### ⚙️ Step 4 — Cache

- [ ] Cacheable data identified (read-heavy, tolerant of some staleness)
- [ ] Cache invalidation strategy chosen deliberately, not bolted on later
- [ ] Local vs distributed cache trade-off considered (local is faster but inconsistent across nodes; distributed adds a network hop and its own failure mode)
- [ ] Cache stampede protection in place (request coalescing, jittered TTLs, stale-while-revalidate) for hot keys
- [ ] Cache hit ratio monitored, not just assumed to help

### ⚙️ Step 5 — Read Replicas / CQRS

- [ ] Read-heavy workload confirmed as the actual bottleneck (not writes)
- [ ] Read replicas or a CQRS split evaluated before reaching for async, partitioning, or sharding
- [ ] Replication lag and staleness tolerance defined for consumers of the read path

### ⚙️ Step 6 — Go Async

- [ ] Work that doesn't need a synchronous response identified
- [ ] Queue/event-driven path introduced for that work
- [ ] Backpressure and retry/dead-letter handling designed in
- [ ] Observability of async flows in place (correlation IDs propagated through queues so a request can be traced end to end)

### ⚙️ Step 7 — Partition Data

- [ ] Hot tables/collections identified for splitting (by feature, by access pattern)
- [ ] Cross-partition queries minimized before committing
- [ ] Partitioning key chosen for even distribution

### ⚙️ Step 8 — Shard

- [ ] Confirmed a single data store, even partitioned, cannot handle the load
- [ ] Shard key chosen to avoid hotspots and support common queries
- [ ] Rebalancing and cross-shard transaction strategy defined

### ⚙️ Step 9 — Geo-Distribution / Multi-Region

- [ ] Confirmed the bottleneck is latency-to-user or regulatory (data residency), not raw capacity
- [ ] Multi-region replication/consistency model chosen deliberately (active-active vs active-passive)
- [ ] Data residency and cross-region legal requirements checked before this rung, not after

### ⚙️ Step 10 — Split Into Services

- [ ] Confirmed the bottleneck is organizational or deployment coupling, not just data or compute
- [ ] Bounded contexts identified before drawing service boundaries
- [ ] Team ownership, on-call, and operational cost of the split accepted upfront

### ✅ Verify

- [ ] Chosen rung actually resolved the measured bottleneck from Step 0
- [ ] New failure modes introduced by the change are understood and monitored
- [ ] Simpler rungs re-confirmed as insufficient, not skipped out of preference

---

## Notes

Every rung down this ladder trades simplicity for capability. Each one also adds new failure modes and on-call burden — don't pay that price before you've earned it.
