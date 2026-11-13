---
name: feedback-memory-vs-code-conflicts
description: "When a memory file and the actual code/docs disagree, ask the user before assuming the code is right and rewriting the memory"
metadata:
  type: feedback
---

Don't resolve a conflict between an existing memory and the current code/docs by unilaterally trusting the code and "correcting" the memory to match it.

**Why:** On 2026-09-14, [[project_student_submission]] said kmom03 requires a PR, but `kmom03.mdx` and `scripts/create-student-repo.sh`'s `SUBMIT_BRANCHES` didn't implement that. I assumed the memory was stale copy-paste and rewrote it to say "kmom06/kmom10 only," treating the code as the source of truth. The user then pointed out the opposite was true: kmom03 was always meant to require a PR, the code just never implemented it. See [[project_check_submission]] for the full incident.

**How to apply:** A missing feature and a stale memory look identical from the outside — both present as "the memory claims X, the code doesn't do X." When you hit that shape of conflict, surface it to the user (or at minimum flag the discrepancy explicitly when reporting your work) instead of silently picking a side. This applies generally, not just to submission/PR requirements.
