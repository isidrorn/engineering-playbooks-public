# Troubleshooting

## Purpose

This playbook guides a senior engineer through diagnosing an unfamiliar or unclear production issue, from initial symptom to a validated fix. It emphasizes disciplined observation and hypothesis-driven investigation over guesswork, so the real cause is found before anything is changed.

---

## Level 1 Checklist

### 🔍 Understand
□ Restate the problem in one sentence — what is broken, for whom, since when
□ Confirm scope: all users or a subset, all regions/environments or one
□ Identify what changed recently (deploys, config, feature flags, infra, traffic pattern)
□ Check if this is a known issue or recurring pattern
□ Define what "fixed" looks like before investigating further

### 🔍 Observe
□ Pull the relevant dashboards: error rates, latency, throughput, saturation
□ Check alerts that fired and their exact timing
□ Correlate symptom onset with deploys, releases, or external events
□ Capture representative error messages, stack traces, or failing request samples

### 🔍 Investigate — Infrastructure
□ Check compute health (CPU, memory, disk, restarts, OOM kills)
□ Check network health (DNS, load balancer errors, timeouts, packet loss)
□ Check autoscaling behavior and instance/pod count over time
□ Check for resource limits or quotas being hit

### 🔍 Investigate — Application
□ Check application logs around the incident window for anomalies
□ Check for recent code, config, or feature-flag changes in the affected path
□ Check connection pool, thread pool, and queue saturation
□ Reproduce locally or in a lower environment if feasible

### 🔍 Investigate — Dependencies
□ Check upstream/downstream service health and status pages
□ Check database, cache, and message broker health and latency
□ Check third-party API status and rate-limit responses
□ Check for schema, contract, or version mismatches between services

### 💡 Hypothesize
□ List candidate root causes ranked by evidence strength
□ Identify what data would confirm or rule out each hypothesis
□ Avoid fixating on the first plausible theory — test, don't assume

### ⚙️ Mitigate
□ Apply the fastest safe action to reduce user impact (rollback, restart, scale, flag off)
□ Communicate mitigation status to stakeholders per incident process
□ Avoid changes that make root-cause evidence harder to gather, unless impact demands it

### ✅ Verify
□ Confirm the symptom is resolved using the same signal that first showed the problem
□ Watch for recurrence over a reasonable soak period
□ Check for side effects introduced by the mitigation itself

### 📝 Learn
□ Record the timeline, root cause, and fix for future reference
□ Identify follow-up hardening or monitoring gaps
□ Feed findings into RCA process if impact warrants it

---

## Notes

For incidents with customer impact or SLA implications, switch to the Incident Response playbook in parallel with technical investigation.
