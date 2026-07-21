# Diagramming

## Purpose

Use this checklist when creating or maintaining architectural diagrams — what to diagram, when, what level of detail to include, and how to keep the result useful instead of a stale picture nobody trusts. A diagram that lies is worse than no diagram, because people make decisions based on it.

---

## Level 1 Checklist

### 🔍 When to Diagram

- [ ] New system design being proposed or reviewed
- [ ] Significant change to an existing system's shape (new dependency, new data store, new boundary)
- [ ] Onboarding documentation for a system a new team member will need to understand
- [ ] Incident investigation where the actual request/data flow is unclear or contested
- [ ] Cross-team dependency discussion where each side has a different mental model of the boundary
- [ ] Before writing any ADR that changes structure — the diagram usually surfaces objections the prose doesn't

### 💡 What Level (C4 Model)

- [ ] Context diagram exists: the system as one box, its users, and external systems it talks to
- [ ] Container diagram exists: deployable units, data stores, and how they communicate
- [ ] Component diagram exists for any container complex enough that "what's inside" isn't obvious from the container diagram alone
- [ ] Code-level diagram (class/sequence) only added when complexity genuinely demands it — not by default
- [ ] Right level chosen for the audience: don't hand a component diagram to someone who asked "what does this system depend on?"

### ⚙️ What to Include

- [ ] System boundaries clearly marked (what's inside this system vs external)
- [ ] Trust boundaries marked separately from system boundaries (they don't always coincide)
- [ ] Data flows labeled with protocol (HTTP, gRPC, AMQP, etc.), not just an arrow
- [ ] Sync vs async communication visually distinguished (solid vs dashed line, or explicit label)
- [ ] External dependencies shown, including the ones considered "someone else's problem"
- [ ] Failure domains indicated (what goes down together)
- [ ] Data stores labeled with their type (relational, document, cache, object store) — "database" alone isn't enough
- [ ] Deployment environments shown where relevant (which boxes are per-region, per-environment)

### ⚙️ Diagram Types

- [ ] Context/landscape diagram for the 30,000-foot view
- [ ] Component/container diagram for internal structure
- [ ] Sequence diagram for any flow with more than two or three hops or with branching error handling
- [ ] Data flow diagram for pipelines/ETL where transformation order matters
- [ ] Deployment diagram for infrastructure topology (regions, AZs, network boundaries)
- [ ] Entity relationship diagram for data models with more than a couple of related entities

### ✅ Quality Checks

- [ ] Has a title and a date (or a "last updated" pointer, if diagrams-as-code)
- [ ] Has a legend/key if it uses any non-obvious shape, color, or line style
- [ ] Shows direction of data flow, not just that two boxes are connected
- [ ] Distinguishes sync vs async explicitly
- [ ] Shows what happens on failure, not just the happy path
- [ ] Kept in version control near the code it describes, not in a wiki page or slide deck that drifts from reality
- [ ] Reviewed by someone who didn't draw it — the author's blind spots are usually the diagram's blind spots

### 📝 Maintenance

- [ ] Updated when the system changes, not on a quarterly schedule that guarantees staleness in between
- [ ] Linked from the README, ADR, or runbook it's relevant to, so people actually find it
- [ ] Diagrams-as-code (Mermaid, PlantUML, Structurizr) preferred over static image files, so changes show up in diffs and reviews

---

## Notes

A diagram's value decays the moment the system changes underneath it. Treat an out-of-date diagram as actively misleading, not merely incomplete — either fix it or delete it.
