# Performance Investigation

## Purpose

This playbook helps a senior engineer systematically diagnose performance degradation — latency, throughput, or resource usage — by establishing a baseline, observing across infrastructure and application layers, and narrowing to a validated cause before acting. It applies to both live incidents and proactive performance work.

---

## Level 1 Checklist

### 🔍 Define Baseline
□ Establish what "normal" looks like for the affected metric (latency, throughput, error rate)
□ Confirm the current deviation is statistically meaningful, not noise
□ Identify when the degradation started and whether it's sudden or gradual
□ Note recent changes in traffic volume, data volume, or usage patterns

### 🔍 Observe — Infrastructure
□ CPU: check utilization, throttling, and steal time per host/container
□ Memory: check usage trend, swap activity, and OOM events
□ Disk: check IOPS, latency, and free space/inode exhaustion
□ Network: check bandwidth saturation, retransmits, and cross-zone latency

### 🔍 Observe — Application
□ GC: check pause frequency/duration and heap growth trend
□ Thread pools: check active/queued/rejected task counts and pool sizing
□ Connection pools: check checkout wait time, saturation, and leaks
□ Database: check slow queries, lock contention, and index usage
□ Cache: check hit/miss ratio, eviction rate, and stale entries
□ External services: check latency, error rate, and timeout/retry behavior

### 🔍 Investigate
□ Correlate the affected layer's anomaly with the timing of degradation
□ Profile the hot path (CPU profile, query plan, flame graph) if cause is unclear
□ Check for N+1 queries, unbounded loops, or missing pagination
□ Check for concurrency issues: lock contention, thread starvation, deadlocks
□ Rule out noisy-neighbor or shared-resource contention

### ⚙️ Act
□ Apply the least invasive fix that addresses the confirmed bottleneck
□ Consider scaling, tuning pool/cache sizes, or query/index changes as appropriate
□ Avoid speculative tuning of parameters without evidence they're the bottleneck
□ Roll out changes incrementally with a rollback path

### ✅ Verify
□ Confirm the target metric returns to baseline under real load
□ Check for regressions introduced elsewhere (memory, other endpoints)
□ Load-test or soak-test if the fix touches a critical path
□ Document the finding and update capacity/alerting thresholds if warranted

---

## Notes

Prefer profiling and measurement over intuition — performance bottlenecks are frequently in a different layer than initial suspicion suggests.
