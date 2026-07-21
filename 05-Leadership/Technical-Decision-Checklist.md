# Technical Decision Checklist

## Purpose

This playbook is a reflective checklist for a senior engineer or tech lead to run through before proposing a technical solution. It is framed as questions rather than tasks — the goal is to pressure-test your own thinking on problem framing, trade-offs, risk, and long-term consequences before committing the team to a direction.

---

## Level 1 Checklist

### 🔍 Problem Framing
□ Am I solving the root cause, or just a visible symptom?
□ Do I actually understand why this problem exists, or am I assuming?
□ Who is affected by this problem, and how badly?
□ Is this problem worth solving now, or is it acceptable to defer?
□ Have I talked to the people closest to the pain before proposing a fix?

### 💡 Solution Evaluation
□ Is there a simpler solution I'm dismissing too quickly?
□ What would "do nothing" cost us, honestly?
□ What are the trade-offs of this approach vs. the alternatives?
□ Am I choosing this because it's right, or because it's familiar/interesting?
□ Does this solution match the size of the problem, or is it overengineered?

### ⚙️ Risk Assessment
□ What operational cost does this introduce (on-call, maintenance, complexity)?
□ What new risks or failure modes appear that didn't exist before?
□ How do we roll back if this doesn't work?
□ What's the blast radius if this fails in production?
□ What dependencies or teams does this put us at the mercy of?

### ✅ Long-Term Thinking
□ How do we measure success, and when do we check?
□ Will this still be a good decision in one year? In three?
□ What happens if the assumptions behind this decision change?
□ Who owns this after I move on to something else?
□ Am I creating a decision someone else will have to painfully unwind later?

---

## Notes

Not every decision warrants every question — use judgment on depth. Reserve the full pass for decisions that are expensive to reverse.
