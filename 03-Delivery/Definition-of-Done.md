# Definition of Done

## Purpose

Use this checklist before marking any ticket, story, or work item as complete. It's a universal gate for "am I actually finished with this?" — covering the things that quietly get skipped when time pressure hits and "the code works" starts to feel like "the work is done."

---

## Level 1 Checklist

### ✅ Code Complete

- [ ] Feature works as specified in the acceptance criteria, not just as you interpreted them
- [ ] Edge cases handled (empty states, limits, error cases, concurrent access)
- [ ] No TODOs or FIXMEs left in the code, or each one is tracked as a ticket, not just a comment
- [ ] Code reviewed and approved
- [ ] No unresolved review comments left hanging as "will fix later"

### ✅ Tested

- [ ] Unit tests cover new logic and its edge cases
- [ ] Integration tests cover the critical path
- [ ] Existing tests still pass — no regressions introduced
- [ ] Manual testing done for UI/UX changes
- [ ] Performance tested if the change touches a hot path
- [ ] Security implications tested (input validation, access control), not just assumed safe

### ✅ Observable

- [ ] Metrics/logs/traces added for the new behavior
- [ ] Alerts configured for new failure modes this change introduces
- [ ] Dashboard updated if new metrics were added — a metric nobody looks at isn't observability
- [ ] Error messages are actionable — someone on-call can understand and act on them at 3am

### 📝 Documented

- [ ] API documentation updated if contracts changed
- [ ] Runbook updated if operational behavior changed
- [ ] README/architecture diagrams updated if system structure changed
- [ ] Migration guide provided if the change is breaking for consumers

### ⚙️ Deployable

- [ ] Feature flag in place if the change is risky or incomplete
- [ ] Database migration is backward-compatible with the previous version
- [ ] Rollback path tested or at least clearly understood
- [ ] No manual steps required for deployment, or the manual steps are documented

### 📣 Communicated

- [ ] Stakeholders notified of completion
- [ ] Downstream teams notified if their integration is affected
- [ ] Release notes written if this is a user-facing change

---

## Notes

This checklist is deliberately generic — it applies to a one-line bug fix and a multi-sprint feature alike, just with different weight per section. If a section genuinely doesn't apply (e.g., no observability changes for a copy fix), skip it explicitly rather than silently ignoring it.
