# Technology Migration

## Purpose

Use this playbook when migrating from one technology, platform, or major dependency to another (database engine, language runtime, message broker, cloud provider, etc.). It keeps the migration justified, scoped, reversible, and fully closed out — instead of leaving two systems running in parallel forever.

---

## Level 1 Checklist

### 🔍 Justify
□ Concrete problem with the current technology stated (not just "it's old")
□ Cost of staying vs cost of migrating compared honestly
□ Target technology's trade-offs understood, not just its advertised benefits
□ Alternative of not migrating (mitigate in place) explicitly considered and rejected for a reason

### 💡 Scope
□ What is and isn't included in the migration is explicit
□ Dependent systems and integration points inventoried
□ Data/schema compatibility gaps identified upfront
□ Migration broken into independently shippable phases, not one giant cutover

### ⚙️ Plan
□ Rollout strategy chosen (dual-run, phased traffic shift, big-bang only if truly justified)
□ Rollback plan defined and tested before execution starts, not improvised mid-incident
□ Success criteria and go/no-go checkpoints defined per phase
□ Communication plan for affected teams and downstream consumers in place

### ⚙️ Execute
□ Migration executed in the planned phases with checkpoints honored
□ Feature flags or routing control the traffic split between old and new
□ Data consistency between old and new systems validated continuously during dual-run
□ Deviations from plan documented as they happen, not reconstructed afterward

### ✅ Verify
□ Performance, error rates, and cost compared against baseline from the old system
□ Edge cases and failure modes specific to the new technology tested, not assumed equivalent
□ On-call/runbooks updated to reflect the new technology's operational profile
□ Monitoring and alerting fully migrated, not still pointed at the old system

### 📝 Decommission
□ Old system traffic confirmed at zero before teardown
□ Old infrastructure, credentials, and access actually removed, not just left idle
□ Documentation, diagrams, and onboarding material updated to reflect the new reality
□ Migration retrospective captured: what worked, what to change next time

---

## Notes

A migration isn't done when the new system works — it's done when the old one is gone and nobody has to remember it existed.
