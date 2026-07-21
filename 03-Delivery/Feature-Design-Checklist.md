# Feature Design Checklist

## Purpose

Use this checklist before writing a line of code for a new feature or significant change. It forces clarity on the problem, success criteria, edge cases, and failure scenarios up front, so design decisions are deliberate rather than discovered mid-implementation.

---

## Level 1 Checklist

### 🔍 Understand

- [ ] Problem stated in one sentence — who has it, and what does it cost them today
- [ ] Actual user/business need distinguished from the requested solution
- [ ] Constraints identified (deadline, team size, existing tech debt, compliance)
- [ ] Prior attempts or adjacent work checked before starting fresh
- [ ] Similar features already built elsewhere in the codebase checked, so you extend rather than reinvent
- [ ] Riskiest assumption identified — the thing most likely to invalidate the whole design if wrong

### 💡 Define

- [ ] Success metrics defined and measurable (not "improve UX")
- [ ] Explicit non-goals stated to prevent scope creep
- [ ] Acceptance criteria agreed with stakeholders before design starts
- [ ] Who owns the decision if trade-offs conflict is clear
- [ ] "Done" defined up front — tests, docs, observability, and a demo, not just "code merged"

### ⚙️ Design

- [ ] Two or more approaches considered, not just the first idea
- [ ] Data model changes sketched out, including the migration path to get there
- [ ] API/interface contract drafted, including error responses
- [ ] Edge cases enumerated (empty states, limits, concurrent access, partial failure)
- [ ] Failure scenarios walked through — what happens when each dependency is slow or down
- [ ] Backward compatibility considered for existing clients/consumers, not just the data layer
- [ ] Accessibility and internationalization considered if the feature is user-facing
- [ ] Riskiest assumption validated with a spike or prototype before committing to the full build

### 📝 Plan

- [ ] Work broken into independently shippable increments
- [ ] Feature flag or kill switch planned if risk warrants it
- [ ] A/B test or gradual rollout plan defined if uncertainty about impact is high
- [ ] Observability requirements defined alongside the feature, not after (metrics, logs, traces, alerts specific to this feature)
- [ ] Rollout plan sketched (who gets it first, how it expands)
- [ ] Testing strategy agreed (unit, integration, load, manual) for the risk level involved
- [ ] Existing tests that need updating identified, not just new tests to write
- [ ] Documentation needs identified (API docs, user guides, runbooks) before implementation starts

### ✅ Validate

- [ ] Design reviewed by at least one other senior engineer
- [ ] Security and privacy implications checked for new data or access paths
- [ ] Estimated effort sanity-checked against the plan's granularity
- [ ] Open questions and assumptions written down, not just resolved silently

---

## Notes

Keep this fast for small changes — a paragraph answering each phase is enough. Reserve a full design doc for anything touching shared infrastructure, external contracts, or data that's expensive to migrate later.
