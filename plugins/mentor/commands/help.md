---
description: "What the mentor is and how to use it — a one-screen guide."
allowed-tools: ["Read", "Glob"]
disallowed-tools: ["Bash", "WebSearch", "WebFetch", "Write", "Edit", "Agent"]
---

# /mentor:help — One-screen guide

Print a SHORT guide (one screen, no walls of text) and exit. This command is read-only by design:
it describes the tool, it never changes anything, never teaches, never asks questions.

**Language:** silently read `~/.claude/memory/mentor/config.md` for `language` and answer in it.
If it doesn't exist, answer in the language the user writes in (or seems to use).

**Adapt to where they are** (check silently whether `~/.claude/memory/mentor/profile.md` exists):

- **Not onboarded yet** → cover, briefly: the mentor teaches you anything (code, a language, a
  craft) with evidence-based methods and its own memory of you, growing session over session. It
  will NOT hand you answers — it makes you try first, on purpose: that's how learning sticks.
  First run: `/mentor:mentor` interviews you (your language, how much it researches, an optional
  persona, your goals) and builds your plan. Everything it knows about you stays on YOUR machine.
- **Already onboarded** → cover, briefly: talk to it in natural language via `/mentor:mentor`, no
  modes to memorize — "teach me X" · "quiz me" · "give me an exercise" · "review my work" ·
  "where am I" · "I want to give feedback". Then the companion commands:
  - `/mentor:personality` — give the mentor a character's voice, have it research the character
    properly, correct it over time ("he wouldn't say that"). Voice changes; rigor never does.
  - `/mentor:config` — language, research budgets (how much web research it may do per pass — it
    protects your tokens and asks before digging deeper), gap reminders.

Close with one line: where to go next (`/mentor:mentor` and just say what you want). If they ask
anything beyond help, point them to `/mentor:mentor` — don't start teaching from here.
