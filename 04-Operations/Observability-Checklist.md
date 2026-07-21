# Observability Checklist

## Purpose

This playbook helps a senior engineer verify that a service is genuinely observable — not just instrumented. It covers metrics, logs, traces, dashboards, alerting, and correlation, so that when something breaks, the system can answer "what, where, and why" without requiring a code change first.

---

## Level 1 Checklist

### 🔍 Metrics
□ Golden signals covered: latency, traffic, errors, saturation
□ Metrics are per-endpoint/operation, not just service-wide averages
□ Percentiles (p50/p95/p99) captured, not only averages
□ Cardinality is bounded — no unbounded labels (user ID, request ID, etc.)
□ Business-relevant metrics exist alongside technical ones

### 📝 Logs
□ Structured logging (key-value/JSON), not free-text strings
□ Log levels used consistently and mean the same thing everywhere
□ No sensitive data (PII, secrets, tokens) ever logged
□ Logs are queryable/searchable in the aggregation tool, not just local files
□ Sampling/retention policy won't silently drop the events that matter

### 🔍 Traces
□ Distributed tracing enabled across service boundaries
□ Spans cover external calls: DB, cache, queue, downstream APIs
□ Trace sampling rate is high enough to catch rare failures
□ Slow/error traces are easy to find, not buried in noise

### ⚙️ Dashboards
□ A default dashboard exists showing golden signals at a glance
□ Dashboard reflects the user's/on-caller's actual mental model of the system
□ Drill-down path exists from dashboard → logs/traces for the same window
□ Dashboard is kept current — no dead panels pointing at retired metrics

### ✅ Alerting
□ Alerts fire on symptoms (user impact), not just internal causes
□ Each alert has a clear, actionable runbook or next step
□ Thresholds are validated against real traffic, not guessed
□ Alert fatigue checked — noisy/flapping alerts are tuned or removed
□ Paging routes to the right owner, with escalation defined

### 🔍 Correlation
□ Correlation/trace ID propagated across every service hop
□ ID appears in logs, traces, and metrics tags consistently
□ ID is surfaced to the client/caller for support and debugging
□ A single ID can reconstruct the full request path end-to-end

---

## Notes

Treat this as a pre-launch and periodic audit, not a one-time setup task — observability gaps tend to surface only during the incident that needed them.
