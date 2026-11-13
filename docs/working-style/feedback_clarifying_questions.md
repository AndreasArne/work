---
name: feedback-clarifying-questions
description: For design/policy decisions, open with a plain-text clarifying question instead of jumping straight to a structured AskUserQuestion with pre-baked options
metadata:
  type: feedback
---

When a decision is genuinely open-ended (how should a secret be distributed, how should an
infra blocker be handled), don't lead with the `AskUserQuestion` tool's structured
multiple-choice UI. Ask in plain text what the user wants to clarify, and wait for their
free-form reply before proposing options.

**Why:** Twice in one session (2026-09-15, during the [[api_key_server]] / issue 06-50
key-distribution discussion), the user rejected an `AskUserQuestion` call with the same
system-relayed message both times: they wanted to clarify first, and pre-baked options were
premature — they had their own framing in mind (e.g. "generate the key at repo-creation time
and drop it in `.env.example`") that a structured list of guesses would have missed or
constrained.

**How to apply:** Structured `AskUserQuestion` is fine for narrow implementation choices
where a short fixed list genuinely covers the space (e.g. "which of these three file layouts").
For anything shaped like a design or policy tradeoff — especially early in a discussion,
before the user has stated their own take — ask a short, open, plain-text question first and
let them set the frame. Only reach for the structured tool once the shape of the real options
is already established by the conversation, not guessed by me.
