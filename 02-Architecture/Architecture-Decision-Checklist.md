# Architecture Decision Checklist

## Purpose

Use this checklist when making a significant architectural decision — choosing a technology, a pattern, or a structural approach that will be expensive to reverse. It forces a clear problem statement, honest exploration of alternatives, and explicit trade-off analysis before anyone commits to a direction.

---

## Level 1 Checklist

### 🔍 Define Problem

- [ ] Problem statement is written in one or two sentences, no solution baked in
- [ ] Constraints identified (budget, timeline, team skills, existing platform)
- [ ] Who is affected and who needs to sign off is known
- [ ] "Do nothing" considered as a baseline option
- [ ] "Do nothing + mitigate" considered as a first-class option, not just a strawman on the way to the real answer

### 💡 Explore Alternatives

- [ ] At least two viable alternatives considered, not just the first idea
- [ ] Checked whether someone already solved this (internal wikis, ADR archives, Slack search) before designing from scratch
- [ ] Prior art checked (has this problem been solved elsewhere in the org?)
- [ ] Build vs buy vs extend evaluated honestly
- [ ] Each alternative's assumptions and dependencies made explicit

### ⚙️ Evaluate Trade-offs

- [ ] Cost, complexity, and time-to-value compared side by side
- [ ] Migration/adoption cost estimated separately from implementation cost (rollout, retraining, data movement)
- [ ] Impact on team's ability to operate and debug the system considered
- [ ] Vendor/technology lock-in implications understood
- [ ] Effect on existing systems and teams assessed (blast radius)
- [ ] Conway's Law check: does the solution align with current team structure, or does it require a reorg to work well?
- [ ] Learning curve and hiring implications considered (can we hire for this, can we ramp the current team)

### 🔍 Assess Risk

- [ ] Worst-case failure scenario for each option identified
- [ ] Reversibility of the decision evaluated (one-way vs two-way door)
- [ ] Operational cost after launch estimated (on-call burden, maintenance)
- [ ] Security and compliance implications reviewed

### ✅ Decide

- [ ] Decision criteria stated before picking a winner, not rationalized after
- [ ] Chosen option maps back to the original problem statement
- [ ] Dissenting opinions heard and addressed, not just overruled
- [ ] Success metrics defined for evaluating the decision later
- [ ] Decision's dependencies documented (what must remain true — a vendor SLA, a team's headcount, a traffic assumption — for this decision to still hold)

### 📝 Document

- [ ] Decision recorded in an ADR or equivalent durable format
- [ ] Rejected alternatives and reasons captured, not just the winner
- [ ] Rollback plan written down in case the decision needs reversing
- [ ] Communication plan set for socializing the decision (RFC, design review, tech talk) so it doesn't just live in a doc nobody reads
- [ ] Review date set to revisit the decision against reality

---

## Notes

A decision without a documented "why not" for the alternatives is a decision nobody can safely challenge or revisit later. An expiry date turns a decision into a hypothesis you'll actually re-check, instead of tribal knowledge that outlives its reasoning.
