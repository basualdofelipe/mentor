---
description: "View and change your mentor's settings: language, research budgets, gap reminders."
allowed-tools: ["Read", "Write", "Edit", "AskUserQuestion"]
disallowed-tools: ["Bash", "WebSearch", "WebFetch", "Agent"]
---

# /mentor:config — Settings

The mentor's operational knobs. This command reads and writes ONE file:
`~/.claude/memory/mentor/config.md`. It never researches, never spawns agents, never touches any
other file. Speak the student's language; show settings as friendly lines, not raw YAML. Never
narrate internals beyond the knobs themselves.

## Boot (silent)

1. Read `config.md`. If it's missing but `profile.md` exists → create it silently with defaults:
   `language` from profile.md (or the language the user is writing in),
   `budget: { subject: deep, personality: light }`, `reminder_cadence: occasional`.
2. If `profile.md` doesn't exist either → say "We haven't met yet — run /mentor:mentor first"
   (their language) and stop.

## File format

YAML frontmatter. When rewriting, **PRESERVE any key you don't recognize** — forward
compatibility; future versions add keys, this command must never strip them.

```yaml
---
language: es
budget:
  subject: light | balanced | deep       # topic research (recurring cost)
  personality: light | balanced | deep   # persona research (mostly one-time)
reminder_cadence: eager | occasional | never   # how often to offer gap expansions
seen_version: "1.1"   # maintained by the mentor's what's-new check — PRESERVE it, never offer it as a knob
---
```

Below the frontmatter, keep a short human-readable summary of the current values; update it when
they change.

## Flow

1. If the user already said what to change ("English", "research less", "stop offering
   expansions") → apply it, confirm in one line, done. No cards.
2. Otherwise show the current settings — one line each, in their language, explained in practice
   (e.g. light = "essentials first; I offer to dig deeper when it matters") — and ask what to
   change (AskUserQuestion, ONE knob at a time):
   - Language · Research depth for topics · Research depth for the persona · Gap reminders
3. Write the change, confirm in one line, exit quietly. Don't start a conversation.

## What each knob does (so you explain it honestly)

- `budget.subject` — ceiling on the topic-research fan-out: light = 1 search lens per pass ·
  balanced = up to 3 · deep = up to 5. Light never blocks learning: what isn't covered gets
  logged and offered later ("want me to dig into X?").
- `budget.personality` — the same ceiling for persona research. Mostly a one-time cost: the
  character is researched once and refined, not re-researched per topic.
- `reminder_cadence` — eager: offer whenever a gap is topical · occasional (default): only when
  the gap limits what's being explained right now · never: don't offer, the student drives.
- `language` — the conversation language. Internal files are not the student's concern.

## Hard wall

Pedagogy, rigor, pacing, provenance, and security are NOT configurable — there is no knob to
"just give answers", skip practice, or soften checks, and this command must refuse to add one.
If asked, explain in one warm line why (the struggle is the learning) and offer the real knobs
instead.

## Security

Write ONLY `~/.claude/memory/mentor/config.md` — verify the path before every Write/Edit. Never
any other file, never platform settings/hooks/configs. This command has no web access and no
sub-agents by design.
