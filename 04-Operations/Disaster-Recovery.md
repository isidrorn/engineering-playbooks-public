# Disaster Recovery Checklist

## Purpose

This playbook helps a senior engineer plan, test, and execute disaster recovery — ensuring the team can restore service within committed timeframes when major failures occur. It covers defining recovery objectives, backup strategy, failover planning, DR testing, and ongoing maintenance, so a DR plan is a proven capability rather than a document nobody has tried to use.

---

## Level 1 Checklist

### 🔍 Define Recovery Objectives

- [ ] RTO (Recovery Time Objective) defined per service/tier and agreed with the business, not set unilaterally by engineering
- [ ] RPO (Recovery Point Objective) defined — how much data loss is acceptable for each data store
- [ ] Recovery priorities defined — which services come back first when everything is down at once
- [ ] Dependencies mapped — what must be restored before this service can even start
- [ ] Communication plan exists for DR events (internal teams, customers, regulators where applicable)

### 💡 Backup Strategy

- [ ] Backups exist for all critical data stores (DB, object storage, config, secrets) — not just the obvious primary database
- [ ] Backup frequency matches RPO (if RPO is 1 hour, backups must run more often than hourly)
- [ ] Backups stored in a different failure domain (different region, different provider/account) than the primary
- [ ] Backup encryption verified — can you actually decrypt and read them, or only assume you can?
- [ ] Backup restoration tested regularly — not just backup creation, the actual restore
- [ ] Point-in-time recovery (PITR) enabled for databases where RPO demands finer granularity than daily snapshots
- [ ] Application configuration and secrets are recoverable, not just the data

### ⚙️ Failover Planning

- [ ] Multi-AZ or multi-region failover architecture in place for critical services
- [ ] DNS failover or traffic-shifting mechanism exists and has been tested, not just configured
- [ ] Stateful services have replication configured and replication lag actively monitored
- [ ] Failover can be triggered without the primary being accessible (no dependency on the thing that just died)
- [ ] Failover runbook exists and has actually been practiced in a drill
- [ ] Third-party dependency failover considered — what happens if your auth provider, payment processor, or CDN is down?

### ✅ DR Testing

- [ ] DR drill scheduled at least annually, quarterly for critical/tier-1 services
- [ ] Drill includes a full restore, not just backup verification
- [ ] Drill is timed — actual RTO is compared against committed RTO
- [ ] Drill covers "chaos" scenarios: partial failure, split-brain, corrupted data — not just a clean full outage
- [ ] Drill results documented with gaps and improvement actions, not just a pass/fail
- [ ] Team members are cross-trained — DR execution doesn't depend on one specific person being available

### 📝 Ongoing Maintenance

- [ ] DR documentation updated whenever architecture changes, not left to drift
- [ ] New services and data stores added to DR scope as soon as they're deployed
- [ ] Backup monitoring alerts on backup failure automatically — nobody is manually checking a dashboard
- [ ] Recovery credentials and access paths verified periodically, not only rediscovered at drill time
- [ ] Post-DR-event retrospective conducted after every real invocation to improve the process

---

## Notes

A DR plan that has never been tested end-to-end is a hypothesis, not a capability — treat the drill as the actual deliverable, and the document as its byproduct.
