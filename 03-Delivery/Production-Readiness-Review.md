# Production Readiness Review

## Purpose

Use this checklist before a new service or significant feature goes live. It confirms the system can be observed, will fail gracefully, can be deployed and rolled back safely, is secured against realistic threats, and that the team on call actually knows how to operate it.

---

## Level 1 Checklist

### ✅ Observability

- [ ] Metrics cover the golden signals (latency, traffic, errors, saturation)
- [ ] Logs are structured, correlated with a request/trace ID, and searchable
- [ ] Distributed tracing covers the critical path end-to-end
- [ ] Dashboards exist and are linked from the on-call runbook
- [ ] Alerts are tied to user-facing impact, with sane thresholds and no known false-positive noise
- [ ] SLOs/SLIs are defined for the service, not just informally understood
- [ ] Error budget is tracked and visible, so it can inform release pace decisions

### 🔒 Security

- [ ] AuthN/AuthZ verified for every endpoint, including internal/admin ones
- [ ] Secrets rotation policy exists and is documented (not "rotate manually if we remember")
- [ ] Vulnerability scanning (dependencies, containers, IaC) runs in the CI pipeline
- [ ] Penetration testing completed or explicitly scheduled before/shortly after launch
- [ ] CORS, CSP, and other security headers are configured, not left at framework defaults
- [ ] Input validation is enforced on all external-facing endpoints, not just the obvious ones

### ⚙️ Resilience

- [ ] Timeouts, retries, and circuit breakers are set on every external dependency
- [ ] Graceful degradation defined for each dependency being down or slow
- [ ] Graceful degradation actually tested (dependency killed/blocked in a test env), not just theorized
- [ ] Chaos or failure-injection testing performed on the critical path
- [ ] Load tested at expected peak, with headroom above it
- [ ] Connection pool sizing (DB, HTTP clients, thread pools) validated under realistic load, not left at library defaults
- [ ] Backpressure or rate-limiting in place so overload fails safely, not catastrophically
- [ ] Data backup/restore path exists and has been tested, not just configured

### ⚙️ Deployment

- [ ] Rollback path is fast, tested, and doesn't require a human to remember steps
- [ ] Feature flags or kill switches exist for the riskiest behavior
- [ ] Database migrations are backward-compatible with the previous code version
- [ ] Database migration tested against a production-like data volume, not just an empty/small dev DB
- [ ] Deployment is automated and repeatable, not a one-off manual sequence
- [ ] Blue-green or canary rollout strategy is documented, not assumed

### 📝 Documentation

- [ ] Runbook exists for known failure modes and common alerts
- [ ] Architecture and key decisions are written down somewhere durable
- [ ] On-call rotation knows this service exists and has access to its dashboards/logs
- [ ] Ownership (team, escalation path) is unambiguous

### 📝 Capacity

- [ ] Current and projected resource usage is known (compute, storage, throughput)
- [ ] Autoscaling limits and quotas are configured, not left at defaults
- [ ] Autoscaling actually tested under load, not just configured and assumed to work
- [ ] Cost projections at expected scale have been calculated, not just sanity-checked at current scale
- [ ] Growth runway is understood — when will this need revisiting

---

## Notes

Treat this as a gate for anything customer-facing or revenue-impacting. For low-risk internal tools, use judgment on which sections to skip rather than applying it wholesale.
