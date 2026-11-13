---
name: feedback-confirm-shared-git-ops
description: "Ask before merging/pushing branches in this repo, and prefer the safest mechanical option (e.g. fast-forward without checkout) rather than picking silently."
metadata:
  type: feedback
---

When asked something like "ready to merge this branch to main?", treat it as a
readiness check, not an instruction to merge immediately — report status (clean
working tree, fast-forward possible or not, any divergence) and offer options via
AskUserQuestion rather than just doing it.

**Why:** confirmed this pattern 2026-09 — asked the user how to merge `slides-review`
into `main` (fast-forward without checkout vs. fast-forward + push vs. wait), user
picked the safe non-disruptive option ("fast-forward without checkout (recommended)")
without objecting to being asked. This matches the general rule of confirming before
actions that touch shared state, and the repo's working tree is sometimes shared with
another concurrent session — see [[project-shared-working-tree]].

**How to apply:**
- For "merge branch to main" type requests: check for divergence, prefer
  `git fetch . <branch>:main` (updates the ref without checkout) when a clean
  fast-forward is possible, and ask whether to also push before doing so.
- Once the user gives a direct follow-up instruction in the same vein (e.g. "Pusha,
  sen radera denna branch om allt mergat och ok"), execute it directly without
  re-asking — the earlier confirmation already covered the intent; only the safety
  checks (fully merged before deleting, fast-forward before pushing) still need to be
  verified each time.
- Deleting a branch: use `git branch -d` (not `-D`) so git itself refuses if it isn't
  fully merged — a good extra safety net, no need to double-check manually first.
