---
name: repo-philosophy-and-workflow
description: Why this repo exists, what it excludes, how playbooks evolve, and the human-approval trust workflow
metadata:
  type: project
---

This repo documents senior-engineer **thinking processes, decision frameworks, and
checklists** — not technology tutorials (no "Kafka guide," no vendor-specific
instructions). Every playbook starts as a Level 1 Checklist: a terse GitHub task list
(`- [ ] item`) meant to trigger knowledge the reader already has, not teach from scratch.
Structure is fixed: Title → Purpose (1 paragraph) → `---` → Level 1 Checklist (icon-tagged
phases: 🔍 Investigate, 💡 Think, ⚙️ Act, ✅ Verify, 📝 Document) → `---` → Notes (optional,
brief).

**Evolution model**: Level 1 checklist → used in practice → gaps identified → deep-dive
doc extracted into its own file when a checklist item needs more explanation or a section
would exceed ~15 items → cross-referenced from the checklist via relative markdown links.
No Level 2/3 docs exist yet as of 2026-07 — this is a trigger condition, not a schedule.

**Filename convention**: Title-Case-With-Dashes, no `-Checklist` suffix (dropped 2026-07
for consistency — e.g. `System-Design.md`, not `System-Design-Checklist.md`).

**Trust workflow — important safety rule**: all content is AI-drafted. The README's
"Review Status" table is the human-curation record: every row starts unchecked (`[ ]`)
and only the repo owner checks a box after personally reviewing that file. **Never check
a Review Status box on the user's behalf** — doing so would misrepresent review that
hasn't happened, undermining the entire point of the table.

