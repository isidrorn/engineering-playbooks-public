# Performance Investigation

## Purpose

This playbook helps a senior engineer systematically diagnose performance degradation — latency, throughput, or resource usage — by establishing a baseline, observing across infrastructure and application layers, and narrowing to a validated cause before acting. It applies to both live incidents and proactive performance work.

---

## Level 1 Checklist

### 🔍 Define Baseline

- [ ] Establish what "normal" looks like for the affected metric (latency, throughput, error rate)
- [ ] Confirm the current deviation is statistically meaningful, not noise
- [ ] Identify when the degradation started and whether it's sudden or gradual
- [ ] Note recent changes in traffic volume, data volume, or usage patterns
- [ ] Check whether client-side behavior changed — are clients sending pathological or unusually large requests

### 🔍 Observe — Infrastructure

- [ ] CPU: check utilization, throttling, and steal time per host/container
- [ ] Memory: check usage trend, swap activity, and OOM events
- [ ] Disk: check IOPS, latency, and free space/inode exhaustion
- [ ] Network: check bandwidth saturation, retransmits, connection resets, and cross-zone latency
- [ ] Check for MTU mismatches on affected network paths if seeing intermittent large-payload failures
- [ ] Check for resource contention from co-located workloads (noisy neighbor) on shared hosts

### 🔍 Observe — Application

- [ ] GC: check full GC pauses versus minor GC frequency, promotion rate, and humongous allocations
- [ ] Thread pools: check active/queued/rejected task counts, pool sizing, and thread leaks
- [ ] Connection pools: check checkout wait time, saturation, leak detection, and max-lifetime settings
- [ ] Database: check slow queries, lock wait timeouts, table/index bloat, and vacuum/analyze recency
- [ ] Cache: check hit/miss ratio, eviction rate, stale entries, and thundering-herd behavior on cache miss
- [ ] External services: check latency, error rate, and timeout/retry behavior

### 🔍 Investigate

- [ ] Correlate the affected layer's anomaly with the timing of degradation
- [ ] Profile the hot path (CPU profile, query plan, flame graph) if cause is unclear
- [ ] Check for N+1 queries, unbounded loops, or missing pagination
- [ ] Check for concurrency issues: lock contention, blocked threads (via thread dump), thread starvation, deadlocks
- [ ] Check for JVM safepoint pauses unrelated to GC (biased locking revocation, deoptimization)
- [ ] Check for classloading or JIT warm-up overhead if degradation is concentrated right after startup/deploy
- [ ] Check cache serialization/deserialization overhead, not just hit ratio
- [ ] Rule out noisy-neighbor or shared-resource contention as the actual driver

### ⚙️ Act

- [ ] Apply the least invasive fix that addresses the confirmed bottleneck
- [ ] Consider scaling, tuning pool/cache sizes, or query/index changes as appropriate
- [ ] Avoid speculative tuning of parameters without evidence they're the bottleneck
- [ ] Roll out changes incrementally with a rollback path

### ✅ Verify

- [ ] Confirm the target metric returns to baseline under real load
- [ ] Check for regressions introduced elsewhere (memory, other endpoints)
- [ ] Load-test or soak-test if the fix touches a critical path
- [ ] Document the finding and update capacity/alerting thresholds if warranted

---

## Notes

Prefer profiling and measurement over intuition — performance bottlenecks are frequently in a different layer than initial suspicion suggests.
