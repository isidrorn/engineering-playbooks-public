# Observability

## Purpose

This playbook helps a senior engineer verify that a service is genuinely observable — not just instrumented. It covers metrics, logs, traces, dashboards, alerting, and correlation, so that when something breaks, the system can answer "what, where, and why" without requiring a code change first.

---

## Level 1 Checklist

### 🔍 Metrics

- [ ] SLOs/SLIs are defined per service and error budget is tracked, not just "uptime feels fine"
- [ ] RED (Rate, Errors, Duration) covered for every service
- [ ] USE (Utilization, Saturation, Errors) covered for underlying infrastructure (CPU, disk, queues, connection pools)
- [ ] Metrics are per-endpoint/operation, not just service-wide averages
- [ ] Percentiles (p50/p95/p99) captured, not only averages
- [ ] Cardinality is bounded — no unbounded labels (user ID, request ID, etc.) that could blow up the metrics backend
- [ ] Business-relevant metrics exist alongside technical ones (signups, orders placed, revenue at risk)
- [ ] DORA metrics tracked: deployment frequency and change failure rate

### 📝 Logs

- [ ] Structured logging (key-value/JSON), not free-text strings
- [ ] Log levels used consistently and mean the same thing everywhere
- [ ] No sensitive data (PII, secrets, tokens, auth headers) accidentally logged — checked, not assumed
- [ ] Structured fields that are actually searched are indexed for fast query, not just stored
- [ ] Request/response logging exists at system boundaries, with sampling to control volume
- [ ] Log rotation and retention policy won't silently drop events that matter before they're needed
- [ ] Log volume and its cost are known and reviewed, not an open-ended bill

### 🔍 Traces

- [ ] Distributed tracing enabled across service boundaries
- [ ] Spans cover external calls: DB, cache, queue, downstream APIs
- [ ] Trace context propagates through async boundaries (queue publish → consume, event bus, background jobs), not just synchronous calls
- [ ] No unexplained gaps in traces — missing spans are investigated, not shrugged off
- [ ] Sampling strategy captures error and slow traces at a higher rate than the happy path

### ⚙️ Dashboards

- [ ] A "service overview" dashboard exists that answers "is it healthy?" in 5 seconds
- [ ] Drill-down dashboards exist for each subsystem/dependency
- [ ] Each alert links to the dashboard and runbook relevant to it
- [ ] Drill-down path exists from dashboard → logs/traces for the same time window
- [ ] Dashboard is kept current — no dead panels pointing at retired metrics

### ✅ Alerting

- [ ] Alerts fire on symptoms (user impact), not just internal causes
- [ ] Every alert has a runbook attached — not tribal knowledge in someone's head
- [ ] Escalation path is defined: page → team lead → management, with clear timing
- [ ] Duplicate/flapping alerts are suppressed or deduplicated, not left to spam the channel
- [ ] Alerts trigger on SLO burn rate rather than raw static thresholds where possible
- [ ] Alert fatigue is reviewed quarterly — noisy/low-value alerts are tuned or removed

### 🔍 Correlation

- [ ] Correlation/trace ID propagated across every service hop
- [ ] Correlation ID survives async boundaries (queue publish → consume, event handlers, scheduled jobs)
- [ ] ID appears in logs, traces, and metrics tags consistently
- [ ] ID is surfaced in error responses so it can be handed to support for ticket correlation
- [ ] A single ID can reconstruct the full request path end-to-end

---

## Notes

Treat this as a pre-launch and periodic audit, not a one-time setup task — observability gaps tend to surface only during the incident that needed them.
