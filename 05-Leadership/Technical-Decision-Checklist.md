# Technical Decision Checklist

## Purpose

This playbook is a reflective checklist for a senior engineer or tech lead to run through before proposing a technical solution. It is framed as questions rather than tasks — the goal is to pressure-test your own thinking on problem framing, trade-offs, risk, team readiness, and long-term consequences before committing the team to a direction.

---

## Level 1 Checklist

### 🔍 Problem Framing

- [ ] Am I solving the root cause, or just a visible symptom?
- [ ] Do I actually understand why this problem exists, or am I assuming?
- [ ] Have I quantified the cost of NOT solving this — is it actually urgent, or does it just feel urgent?
- [ ] Am I being influenced by recency bias (the last incident, a conference talk I just saw)?
- [ ] Is this the right time to solve this, or are there higher-priority problems competing for the same effort?
- [ ] Who is affected by this problem, and how badly?
- [ ] Is this problem worth solving now, or is it acceptable to defer?
- [ ] Have I talked to the people closest to the pain before proposing a fix?

### 💡 Solution Evaluation

- [ ] Is there a simpler solution I'm dismissing too quickly?
- [ ] What would "do nothing" cost us, honestly?
- [ ] What are the trade-offs of this approach vs. the alternatives?
- [ ] How will this affect developer experience and velocity — day to day, not just at launch?
- [ ] What's the migration cost for existing code/data, and have I actually estimated it?
- [ ] Can old and new run in parallel during the transition, or is this a hard cutover?
- [ ] Am I choosing this because it's right, or because it's familiar/interesting to me?
- [ ] Does this solution match the size of the problem, or is it overengineered?

### ⚙️ Risk Assessment

- [ ] What operational cost does this introduce (on-call, maintenance, complexity)?
- [ ] What new risks or failure modes appear that didn't exist before?
- [ ] What happens if the person who built this leaves the team?
- [ ] Does this decision create vendor lock-in, and is that an acceptable trade?
- [ ] What's the change in security surface area — new attack vectors, new secrets, new trust boundaries?
- [ ] How do we roll back if this doesn't work?
- [ ] What's the blast radius if this fails in production?
- [ ] What dependencies or teams does this put us at the mercy of?

### 💡 Team & Organizational

- [ ] Does the team have the skills to execute and maintain this? If not, what's the upskilling plan?
- [ ] Have I gotten input from the people who'll live with this decision daily, not just approvers?
- [ ] Am I factoring in actual team capacity and competing priorities, or planning against an idealized team?
- [ ] Is this decision reversible enough that we can course-correct without a full rewrite?

### ✅ Long-Term Thinking

- [ ] How do we measure success, and when do we check?
- [ ] Will this still be a good decision in one year? In three?
- [ ] What happens if the assumptions behind this decision change?
- [ ] Who owns this after I move on to something else?
- [ ] How will I communicate and socialize this decision (RFC, design review, tech talk)?
- [ ] What documentation will future engineers need to understand why we did this?
- [ ] Does this decision align with the team's stated technical direction?
- [ ] Am I creating a decision someone else will have to painfully unwind later?

---

## Notes

Not every decision warrants every question — use judgment on depth. Reserve the full pass for decisions that are expensive to reverse.
