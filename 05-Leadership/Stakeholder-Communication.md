# Stakeholder Communication Checklist

## Purpose

This playbook helps a senior engineer or tech lead communicate technical decisions, status, and trade-offs to non-technical or cross-functional stakeholders — because the decision is only as good as the buy-in behind it. It covers understanding your audience, framing the message, choosing the right format, following through, and common pitfalls to avoid.

---

## Level 1 Checklist

### 🔍 Understand Your Audience

- [ ] Who needs to know — decision-makers, affected teams, downstream consumers, leadership?
- [ ] What do they care about — cost, timeline, risk, user impact — not implementation details?
- [ ] What's their technical depth, and is the language and detail level adjusted accordingly?
- [ ] What's the actual decision-making process — advisory input, consensus, or a single decision-maker?
- [ ] Are there known concerns or objections that should be addressed proactively, before someone raises them?

### 💡 Frame the Message

- [ ] Lead with the problem and its business impact, not the solution
- [ ] Present options with trade-offs (cost, time, risk, quality) — not just your recommendation
- [ ] State your recommendation clearly and explain why
- [ ] Quantify where possible — latency in user-facing terms, cost in dollars, risk as probability x impact
- [ ] Be honest about uncertainty — "we don't know yet" is better than false confidence
- [ ] Separate facts from opinions — label assumptions explicitly as assumptions

### ⚙️ Choose the Right Format

- [ ] RFC/design doc for decisions that need broad input and a paper trail
- [ ] Short write-up + meeting for decisions that need discussion and quick alignment
- [ ] Slack/email for status updates and FYIs, not for decisions needing real input
- [ ] Diagrams over text for architecture and data flow discussions
- [ ] Demo/prototype for "show don't tell" situations where words undersell or oversell the change

### ✅ Follow Through

- [ ] Decision recorded and accessible — not buried in Slack history
- [ ] Dissenting opinions documented, not dismissed
- [ ] Action items and owners are clear
- [ ] Revisit date set for significant decisions
- [ ] Stakeholders updated when reality diverges from the plan — don't wait for them to ask

### 📝 Common Pitfalls

- [ ] Don't surprise leadership with bad news in a public forum — brief them first
- [ ] Don't present a decision as final when it's actually still open for input
- [ ] Don't use jargon with non-technical audiences — say "page load time," not "P99 latency"
- [ ] Don't hide trade-offs — they'll surface eventually, and trust is lost when they do
- [ ] Don't wait until you have 100% certainty to communicate — progress updates build trust

---

## Notes

Technical correctness doesn't guarantee adoption — a well-communicated good-enough decision often beats a brilliant one nobody understood or bought into.
