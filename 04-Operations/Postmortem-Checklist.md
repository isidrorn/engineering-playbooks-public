# Postmortem Checklist

## Purpose

This playbook helps a senior engineer run a blameless postmortem that produces real learning and follow-through, not just a document. It covers assessing impact, reconstructing the timeline, finding root cause, extracting lessons, defining action items, and documenting the outcome.

---

## Level 1 Checklist

### 🔍 Assess Impact
□ Quantify user/customer impact: duration, scope, severity
□ Quantify business impact: revenue, SLA breaches, reputational cost
□ Identify all affected systems and downstream dependencies
□ Note what was degraded vs. fully unavailable

### 📝 Build Timeline
□ Reconstruct events minute-by-minute from logs, alerts, and chat history
□ Mark detection time, response time, mitigation time, resolution time
□ Note key decisions made and by whom, without assigning blame
□ Flag gaps where the timeline is unclear or disputed

### 💡 Identify Root Cause
□ Distinguish trigger (what set it off) from root cause (why it was possible)
□ Ask "why" enough times to reach a systemic, not superficial, cause
□ Consider contributing factors: process, tooling, and human factors together
□ Avoid stopping at "human error" — ask what allowed the error to matter

### 💡 Extract Lessons
□ Identify what worked well during detection and response
□ Identify what slowed down detection, diagnosis, or mitigation
□ Check whether existing runbooks/alerts matched what was actually needed
□ Look for similar latent risks elsewhere in the system

### ⚙️ Define Actions
□ Every action item has a single owner and a due date
□ Actions address root cause, not just the immediate symptom
□ Prioritize actions by risk reduction, not effort or convenience
□ Distinguish must-fix from nice-to-have, and track both
□ Confirm actions are tracked in the team's normal work system, not just the doc

### 📝 Document
□ Write the postmortem in a blameless, factual tone
□ Include the timeline, impact, root cause, and action items
□ Share broadly enough that other teams can learn from it
□ Follow up on action item completion, don't let the doc be the end state

---

## Notes

A postmortem without tracked, completed action items is a wasted incident — treat follow-through as part of the process, not optional.
