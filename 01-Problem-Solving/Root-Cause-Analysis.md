# Root Cause Analysis

## Purpose

This playbook guides a senior engineer through conducting a thorough, blameless root cause analysis after an incident is resolved. It focuses on gathering solid evidence, reconstructing an accurate timeline, tracing the causal chain, and turning findings into preventive action rather than assigning blame.

---

## Level 1 Checklist

### 🔍 Gather Evidence
□ Collect logs, metrics, traces, and alerts covering the full incident window
□ Collect the incident channel/ticket history and all actions taken
□ Collect relevant deploy history, config changes, and feature-flag states
□ Identify gaps in available evidence and note them explicitly

### 📝 Build Timeline
□ Establish first-detectable signal of the problem, not just alert time
□ Sequence every relevant event: changes, alerts, actions, escalations
□ Timestamp each entry precisely and note the source
□ Cross-check timeline against multiple independent sources

### 💡 Analyze
□ Trace the causal chain from trigger to observed impact
□ Distinguish the root cause from symptoms and coincidental factors
□ Apply a structured technique (e.g. five whys) to avoid stopping too early
□ Identify why existing safeguards did not prevent or catch this sooner

### 🔍 Identify Contributing Factors
□ Note process gaps (review, testing, deployment safeguards)
□ Note system design factors (coupling, missing redundancy, unclear ownership)
□ Note detection/alerting gaps that delayed awareness or response
□ Note human factors without assigning blame (unclear runbooks, ambiguous ownership)

### ⚙️ Define Preventive Actions
□ Propose actions that address root cause, not just the symptom
□ Assign an owner and realistic timeline to each action
□ Prioritize actions by risk reduction versus effort
□ Distinguish must-do fixes from nice-to-have improvements

### 📝 Document
□ Write a clear, blameless summary suitable for wide distribution
□ Include timeline, impact, root cause, contributing factors, and action items
□ Review draft with incident participants before publishing
□ Track action items to completion, not just to ticket creation

---

## Notes

Keep the RCA blameless in both language and intent — the goal is a more resilient system, not accountability for individuals.
