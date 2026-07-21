# Senior Engineering Playbooks

A personal engineering handbook: thinking processes, decision frameworks, and checklists
for Senior Engineers, Tech Leads, Staff Engineers, and Software Architects.

This is **not** technology documentation. It captures how to *think* through a production
incident, a design decision, a review, or a migration — the questions to ask, the order to
ask them in, the traps to avoid. The technology changes every few years; the reasoning
process doesn't.

Every playbook here is drafted collaboratively with AI assistance, then personally reviewed
and curated before it's trusted. The [Review Status](#review-status) table below is that
curation record, not a formality — an unchecked row means treat the content as a draft.

## Playbooks

### 01. Problem Solving

- [Troubleshooting](01-Problem-Solving/Troubleshooting.md) — structured diagnosis from symptom to validated fix
- [Incident Response](01-Problem-Solving/Incident-Response.md) — severity, communication, mitigation, recovery
- [Root Cause Analysis](01-Problem-Solving/Root-Cause-Analysis.md) — evidence, timeline, causal chain, preventive actions
- [Performance Investigation](01-Problem-Solving/Performance-Investigation.md) — systematic bottleneck diagnosis across infra and app layers
- [Security Review](01-Problem-Solving/Security-Review.md) — threat modeling, OWASP risks, AuthN/AuthZ, data protection, compliance

### 02. Architecture

- [System Design](02-Architecture/System-Design.md) — requirements through trade-offs for new systems
- [Architecture Decision](02-Architecture/Architecture-Decision.md) — problem, alternatives, trade-offs, risks, rollback
- [Scalability Decision Framework](02-Architecture/Scalability-Decision-Framework.md) — ordered escalation from optimize to split
- [Monolith to Microservices](02-Architecture/Monolith-to-Microservices.md) — bounded contexts, data ownership, strangler pattern
- [Technology Migration](02-Architecture/Technology-Migration.md) — justify, scope, execute, decommission
- [Diagramming](02-Architecture/Diagramming.md) — what to diagram, C4 levels, quality checks, maintenance
- [OOP Design](02-Architecture/OOP-Design.md) — SOLID, coupling, cohesion, common traps
- [Design Patterns](02-Architecture/Design-Patterns.md) — GoF catalog plus modern/architectural patterns, when to reach for each
- [Database Design](02-Architecture/Database-Design.md) — modeling, engine choice, indexing, transactions, migrations, scaling
- [Cloud Infrastructure](02-Architecture/Cloud-Infrastructure.md) — topology, networking, IAM, IaC, cost, resilience

### 03. Delivery

- [Feature Design](03-Delivery/Feature-Design.md) — problem, success metrics, edge cases, failure scenarios
- [Peer Review](03-Delivery/Peer-Review.md) — correctness, performance, security, observability, maintainability
- [Production Readiness Review](03-Delivery/Production-Readiness-Review.md) — observability, resilience, security, deployment, capacity
- [Deployment](03-Delivery/Deployment.md) — pre-deploy through post-deploy monitoring
- [Definition of Done](03-Delivery/Definition-of-Done.md) — the universal "am I actually finished" gate
- [Testing Strategy](03-Delivery/Testing-Strategy.md) — test pyramid, contract testing, test quality, infrastructure
- [Coding Best Practices](03-Delivery/Coding-Best-Practices.md) — naming, method design, error handling, defensive coding

### 04. Operations

- [Observability](04-Operations/Observability.md) — metrics, logs, traces, dashboards, alerting, correlation
- [Postmortem](04-Operations/Postmortem.md) — impact, timeline, root cause, lessons, action items
- [Disaster Recovery](04-Operations/Disaster-Recovery.md) — RTO/RPO, backups, failover, DR drills, maintenance

### 05. Leadership

- [Technical Decision](05-Leadership/Technical-Decision.md) — reflective questions before proposing a solution
- [Stakeholder Communication](05-Leadership/Stakeholder-Communication.md) — framing decisions, choosing formats, getting buy-in

## Philosophy

Every playbook is a **Level 1 Checklist** — it's not meant to teach you something new;
it's meant to trigger knowledge you already have, at the moment you need it. Read it top
to bottom before reasoning from scratch.

## Review Status

Every playbook below is AI-drafted and human-curated. Unchecked means it hasn't been
personally reviewed and approved yet — treat its content as a draft, not a trusted source,
until it's checked off.

| Playbook | Category | Approved |
|---|---|---|
| [Troubleshooting](01-Problem-Solving/Troubleshooting.md) | Problem Solving | [ ] |
| [Incident Response](01-Problem-Solving/Incident-Response.md) | Problem Solving | [ ] |
| [Root Cause Analysis](01-Problem-Solving/Root-Cause-Analysis.md) | Problem Solving | [ ] |
| [Performance Investigation](01-Problem-Solving/Performance-Investigation.md) | Problem Solving | [ ] |
| [Security Review](01-Problem-Solving/Security-Review.md) | Problem Solving | [ ] |
| [System Design](02-Architecture/System-Design.md) | Architecture | [ ] |
| [Architecture Decision](02-Architecture/Architecture-Decision.md) | Architecture | [ ] |
| [Scalability Decision Framework](02-Architecture/Scalability-Decision-Framework.md) | Architecture | [ ] |
| [Monolith to Microservices](02-Architecture/Monolith-to-Microservices.md) | Architecture | [ ] |
| [Technology Migration](02-Architecture/Technology-Migration.md) | Architecture | [ ] |
| [Diagramming](02-Architecture/Diagramming.md) | Architecture | [ ] |
| [OOP Design](02-Architecture/OOP-Design.md) | Architecture | [ ] |
| [Design Patterns](02-Architecture/Design-Patterns.md) | Architecture | [ ] |
| [Database Design](02-Architecture/Database-Design.md) | Architecture | [ ] |
| [Cloud Infrastructure](02-Architecture/Cloud-Infrastructure.md) | Architecture | [ ] |
| [Feature Design](03-Delivery/Feature-Design.md) | Delivery | [ ] |
| [Peer Review](03-Delivery/Peer-Review.md) | Delivery | [ ] |
| [Production Readiness Review](03-Delivery/Production-Readiness-Review.md) | Delivery | [ ] |
| [Deployment](03-Delivery/Deployment.md) | Delivery | [ ] |
| [Definition of Done](03-Delivery/Definition-of-Done.md) | Delivery | [ ] |
| [Testing Strategy](03-Delivery/Testing-Strategy.md) | Delivery | [ ] |
| [Coding Best Practices](03-Delivery/Coding-Best-Practices.md) | Delivery | [ ] |
| [Observability](04-Operations/Observability.md) | Operations | [ ] |
| [Postmortem](04-Operations/Postmortem.md) | Operations | [ ] |
| [Disaster Recovery](04-Operations/Disaster-Recovery.md) | Operations | [ ] |
| [Technical Decision](05-Leadership/Technical-Decision.md) | Leadership | [ ] |
| [Stakeholder Communication](05-Leadership/Stakeholder-Communication.md) | Leadership | [ ] |

## Principles

- **Vendor-agnostic** — no tool-specific instructions or vendor lock-in.
- **Process-oriented** — decision trees and checklists, not reference material.
- **Production-focused** — for people accountable for live systems, not tutorials.
- **Lightweight** — depth is optional and one link away; the checklist is not.
