# Incident Response

## Purpose

This playbook helps a senior engineer act as or support an incident commander during a live production incident. It covers assessing severity, communicating clearly, mitigating impact, and driving recovery — prioritizing speed and coordination over root-cause depth, which belongs in a follow-up RCA.

---

## Level 1 Checklist

### 🔍 Assess
□ Confirm the incident is real and reproducible, not a false alarm
□ Determine severity/priority using the org's defined scale
□ Identify blast radius: users, regions, services, revenue affected
□ Assign or confirm incident commander and roles (comms, ops, scribe)
□ Open an incident channel/ticket and start a timeline log

### 📝 Communicate
□ Post initial status update within the expected SLA window
□ State what is known, what is being done, and next update time
□ Notify stakeholders proportional to severity (team, leadership, customers)
□ Keep updates factual and cadence-driven, even if "no change"
□ Avoid speculating on root cause in external-facing updates

### ⚙️ Mitigate
□ Prioritize actions that stop or reduce user impact over understanding cause
□ Consider rollback, feature-flag disable, traffic shift, or scaling as first options
□ Apply the smallest safe change that addresses the symptom
□ Log every action taken with timestamp and rationale
□ Avoid uncoordinated changes — one driver at a time

### ⚙️ Recover
□ Confirm the mitigation is fully rolled out (all instances, all regions)
□ Restore any degraded functionality that was intentionally disabled
□ Clear backlogs, queues, or caches left in an inconsistent state
□ Reconcile any data affected during the incident window

### ✅ Verify
□ Confirm key metrics have returned to baseline, not just alerts clearing
□ Hold a soak period appropriate to the failure mode before declaring resolved
□ Get explicit sign-off from incident commander before closing
□ Send final status update confirming resolution

### 📝 Follow-up
□ Schedule the postmortem/RCA within the expected timeframe
□ Capture the timeline and key decisions while memory is fresh
□ File tickets for any temporary mitigations that need permanent fixes
□ Thank responders and close out the incident channel per process

---

## Notes

Severity and communication cadence should follow your organization's defined incident levels — this checklist assumes such a framework exists. Use the Root Cause Analysis playbook for the postmortem itself.
