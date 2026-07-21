# Senior Engineering Playbooks

A personal engineering handbook: thinking processes, decision frameworks, and checklists
for Senior Engineers, Tech Leads, Staff Engineers, and Software Architects.

This is **not** technology documentation. It captures how to *think* through a production
incident, a design decision, a review, or a migration — the questions to ask, the order to
ask them in, the traps to avoid. The technology changes every few years; the reasoning
process doesn't.

## Playbooks

### 01. Problem Solving

- [Troubleshooting](01-Problem-Solving/Troubleshooting.md) — structured diagnosis from symptom to validated fix
- [Incident Response](01-Problem-Solving/Incident-Response.md) — severity, communication, mitigation, recovery
- [Root Cause Analysis](01-Problem-Solving/Root-Cause-Analysis.md) — evidence, timeline, causal chain, preventive actions
- [Performance Investigation](01-Problem-Solving/Performance-Investigation.md) — systematic bottleneck diagnosis across infra and app layers

### 02. Architecture

- [System Design Checklist](02-Architecture/System-Design-Checklist.md) — requirements through trade-offs for new systems
- [Architecture Decision Checklist](02-Architecture/Architecture-Decision-Checklist.md) — problem, alternatives, trade-offs, risks, rollback
- [Scalability Decision Framework](02-Architecture/Scalability-Decision-Framework.md) — ordered escalation from optimize to split
- [Monolith to Microservices](02-Architecture/Monolith-to-Microservices.md) — bounded contexts, data ownership, strangler pattern
- [Technology Migration](02-Architecture/Technology-Migration.md) — justify, scope, execute, decommission

### 03. Delivery

- [Feature Design Checklist](03-Delivery/Feature-Design-Checklist.md) — problem, success metrics, edge cases, failure scenarios
- [Peer Review Checklist](03-Delivery/Peer-Review-Checklist.md) — correctness, performance, security, observability, maintainability
- [Production Readiness Review](03-Delivery/Production-Readiness-Review.md) — observability, resilience, deployment, capacity
- [Deployment Checklist](03-Delivery/Deployment-Checklist.md) — pre-deploy through post-deploy monitoring

### 04. Operations

- [Observability Checklist](04-Operations/Observability-Checklist.md) — metrics, logs, traces, dashboards, alerting, correlation
- [Postmortem Checklist](04-Operations/Postmortem-Checklist.md) — impact, timeline, root cause, lessons, action items

### 05. Leadership

- [Technical Decision Checklist](05-Leadership/Technical-Decision-Checklist.md) — reflective questions before proposing a solution

## How to Use

Every playbook starts as a **Level 1 Checklist** — a 30-60 second read. It's not meant to
teach you something new; it's meant to trigger knowledge you already have, at the moment
you need it.

- **Start with the checklist.** Read it top to bottom before reasoning from scratch.
- **Extract when it gets dense.** When a checklist item needs more than a bullet, pull
  the detail into its own document. The checklist stays scannable.
- **Cross-reference over time.** Add links between playbooks as overlap becomes obvious.

## Principles

- **Vendor-agnostic** — no tool-specific instructions or vendor lock-in.
- **Process-oriented** — decision trees and checklists, not reference material.
- **Production-focused** — for people accountable for live systems, not tutorials.
- **Lightweight** — every playbook survives a sub-minute read. Depth is optional.
