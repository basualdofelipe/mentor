# Mentor — a learning mentor for Claude Code

A Claude Code **plugin** that helps you get better at whatever you want to learn — code, a
language, a craft, a subject — with its own memory that evolves over time. It interviews you, builds
a personalized learning plan, and teaches you toward it with evidence-based methods.

Built on evidence-based learning (retrieval practice, spaced repetition, deliberate practice,
desirable difficulties) and an **anti-slop** discipline: it anchors teaching to canonical sources
and tags provenance, instead of laundering the model's median back at you.

## Install

```
/plugin marketplace add basualdofelipe/mentor
/plugin install mentor@mentor-marketplace
```

Then restart the session and run:

```
/mentor:mentor
```

The first run interviews you (in your language) and builds your profile. Everything is local to
your machine.

> No payment, no registration, no account — a "marketplace" is just this public git repo, installed
> straight from GitHub.

## What it does

Just tell it what you want — "teach me X", "quiz me", "where am I", "review my work", "feedback" —
and it routes to the right mode (chat · lesson · drill · review · recall · progress · roadmap ·
reflect · feedback). The teaching philosophy is hardcoded; the *voice* is customizable
(`personality.md`).

## Privacy & data

- The plugin ships **no personal data**. Your profile, goals, progress and notes are created and
  stored only under `~/.claude/memory/mentor/` on your machine — never sent to the plugin author or
  any third party (your data is only ever part of your own Claude conversation).
- Updating the plugin never touches your memory.

## Security model

The main command's tool grant excludes Bash and the web entirely, and it is instructed to write
only inside its own memory folder. All web research is delegated to **isolated sub-agents**:
`mentor:researcher` (web read-only, no local-file access) and `mentor:synthesizer` (no tools). They
can't write or execute — they only return text, which is treated as data, never obeyed as
instructions. See `plugins/mentor/commands/mentor.md` → `## Security`.

## Updating

This repo omits an explicit plugin `version`, so every push is a new version. Users get it with:

```
/plugin update mentor@mentor-marketplace
```

## Layout

```
.claude-plugin/marketplace.json     # the marketplace (this repo)
plugins/mentor/
  .claude-plugin/plugin.json        # the plugin manifest
  commands/mentor.md                # the /mentor:mentor command
  agents/researcher.md              # isolated web fetcher (return-only)
  agents/synthesizer.md             # synthesizer (read-only, return-only)
```
