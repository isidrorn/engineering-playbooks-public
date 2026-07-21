# Deployment

## Purpose

Use this checklist when shipping a change to production, from final pre-deployment checks through post-deployment monitoring. It exists so that deploying stays a routine, low-drama event even for changes with real blast radius.

---

## Level 1 Checklist

### 🔍 Pre-deployment

- [ ] Change reviewed and approved per team policy
- [ ] CI green — build, tests, and any required scans passed
- [ ] Migrations, if any, are backward-compatible with the currently running version
- [ ] Feature flag defaults are safe if left untouched
- [ ] Rollback plan written down and understood by whoever is deploying
- [ ] Deployment window respects change-freeze or high-traffic period policies
- [ ] Stakeholders/on-call aware a deployment is happening, if impact warrants it
- [ ] Environment-specific config differences checked (env vars, endpoints, feature flags) between staging and target environment
- [ ] Secrets/env vars confirmed present and correct in the target environment before deploying, not discovered missing after

### ⚙️ Deploy

- [ ] Deploy to a staged or canary slice first if the blast radius justifies it
- [ ] Deployment automation used — no manual, undocumented steps
- [ ] Health checks pass before traffic is shifted or increased
- [ ] Health checks actually verify the service works (dependency connectivity, not just "process is up and returns 200")
- [ ] Deployment progress is visible (logs, pipeline status) to whoever is watching
- [ ] Deployment pipeline auto-rolls-back on health check failure, rather than requiring a human to notice and act

### ✅ Verify

- [ ] Golden signals checked immediately after rollout (latency, errors, traffic, saturation)
- [ ] Key user flows spot-checked, not just infrastructure health
- [ ] Logs checked for new error patterns or unexpected warnings
- [ ] Feature flag, if used, ramped gradually rather than flipped to 100% immediately
- [ ] Memory usage trend checked over the soak window, not just an instant snapshot (catch leaks, not just crashes)
- [ ] Async job/queue processing checked for health (queue depth, processing rate), not just request-response paths
- [ ] Error tracking checked for elevated exception rates, not just the metrics dashboard

### 🔍 Rollback Readiness

- [ ] Rollback path tested, not just theorized — know the exact command/pipeline step
- [ ] Previous version/artifact is still available and deployable
- [ ] Rollback doesn't strand data (migrations are reversible or forward-compatible)
- [ ] Clear trigger criteria defined for when to roll back vs. roll forward with a fix

### 📝 Post-deployment

- [ ] Monitoring continued for a reasonable soak period, not abandoned after the first green check
- [ ] Deployment recorded (changelog, deploy log) with what shipped and when
- [ ] Any deviations from plan or surprises documented while memory is fresh
- [ ] Flags/toggles cleaned up once the change is confirmed stable, so they don't linger indefinitely
- [ ] Downstream teams notified if API behavior changed, even if technically backward-compatible
- [ ] Feature flags left over from previous deployments cleaned up while in the area, not just this deployment's own flags

---

## Notes

For high-risk deployments (schema changes, payment paths, auth), pair the Verify step with a second engineer watching dashboards in real time rather than relying on a single set of eyes.
