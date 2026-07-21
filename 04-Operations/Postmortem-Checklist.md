# Postmortem Checklist

## Purpose

This playbook helps a senior engineer run a blameless postmortem that produces real learning and follow-through, not just a document. It covers assessing impact, reconstructing the timeline, finding root cause, extracting lessons, defining action items, and documenting the outcome.

---

## Level 1 Checklist

### 🔍 Assess Impact

- [ ] Quantify user/customer impact: duration, scope, severity
- [ ] Quantify business impact: revenue, SLA breaches, reputational cost
- [ ] Identify affected SLA/SLO metrics specifically, not just "it was down"
- [ ] Calculate the cost of the incident (lost revenue, engineering hours spent, customer trust/churn risk)
- [ ] Check for data loss or corruption, not just availability impact
- [ ] Identify all affected systems and downstream dependencies
- [ ] Note what was degraded vs. fully unavailable

### 📝 Build Timeline

- [ ] Reconstruct events minute-by-minute using automated sources first (deploy logs, alert history, chat transcripts), not memory
- [ ] Mark detection time, response time, mitigation time, resolution time
- [ ] Identify the "detection gap" — the time between incident start and first alert
- [ ] Note where manual intervention was required and why automation didn't handle it
- [ ] Note key decisions made and by whom, without assigning blame
- [ ] Flag gaps where the timeline is unclear or disputed

### 💡 Identify Root Cause

- [ ] Distinguish trigger (what set it off) from root cause (why it was possible)
- [ ] Ask "why" enough times to reach a systemic, not superficial, cause
- [ ] Check for contributing organizational factors: unclear ownership, team handoff gaps, understaffing
- [ ] Check whether a previously identified risk (known issue, flagged tech debt) materialized here
- [ ] Consider "what if" scenarios — what would have prevented or shortened this at each stage
- [ ] Consider contributing factors: process, tooling, and human factors together
- [ ] Avoid stopping at "human error" — ask what allowed the error to matter

### 💡 Extract Lessons

- [ ] Identify what worked well during detection and response
- [ ] Identify what slowed down detection, diagnosis, or mitigation
- [ ] Identify what surprised the responders — gaps in their mental model of the system
- [ ] Check whether documentation/runbooks matched what was actually needed in the moment
- [ ] Identify tooling gaps that slowed the response (missing dashboards, no easy rollback, etc.)
- [ ] Look for similar latent risks elsewhere in the system

### ⚙️ Define Actions

- [ ] Every action item has a single owner and a due date
- [ ] Tag each action as prevent (stop it happening again), detect (catch it faster next time), or respond (fix it faster next time)
- [ ] Actions address root cause, not just the immediate symptom
- [ ] Avoid vague action items ("improve monitoring") — specify exactly what, on what system, measured how
- [ ] Prioritize actions by risk reduction, not effort or convenience
- [ ] Distinguish must-fix from nice-to-have, and track both
- [ ] Set review checkpoints for action completion — a created ticket is not a completed action
- [ ] Confirm actions are tracked in the team's normal work system, not just the doc

### 📝 Document

- [ ] Write the postmortem in a blameless, factual tone
- [ ] Use a consistent template across the organization so postmortems are comparable
- [ ] Include the timeline, impact, root cause, and action items
- [ ] Distribute to a wider audience than just the team involved — other teams learn from this
- [ ] Archive it searchably so future incidents can be correlated against past ones
- [ ] Follow up on action item completion, don't let the doc be the end state

---

## Notes

A postmortem without tracked, completed action items is a wasted incident — treat follow-through as part of the process, not optional.
