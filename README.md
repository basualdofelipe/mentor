# Mentor — a learning mentor for Claude Code

A Claude Code **plugin** that helps you get better at whatever you want to learn — code, a
language, a craft, a subject — with its own memory that evolves over time. It interviews you, builds
a personalized learning plan, and teaches you toward it with evidence-based methods.

Built on evidence-based learning (retrieval practice, spaced repetition, deliberate practice,
desirable difficulties) and an **anti-slop** discipline: it anchors teaching to canonical sources
and tags provenance, instead of laundering the model's median back at you.

## Install

```
/plugin marketplace add <your-github-user>/<this-repo>
/plugin install mentor@mentor-marketplace
```

Then restart the session and run:

```
/mentor:mentor
```

The first run interviews you (in your language) and builds your profile. Everything is local to
your machine.

> **Private repo?** Each person needs git access to it (add them as collaborators on GitHub), or
> make the repo public. No payment, no registration — a "marketplace" is just this git repo.

## What it does

Just tell it what you want — "teach me X", "quiz me", "where am I" — and it routes to the right
mode (lesson · drill · recall · progress · roadmap · reflect · chat). The teaching philosophy is
hardcoded; the *voice* is customizable (`personality.md`).

## Privacy & data

- The plugin ships **no personal data**. Your profile, goals, progress and notes are created
  locally under `~/.claude/memory/mentor/` and never leave your machine.
- Updating the plugin (a new push here) never touches your memory.

## Security model

The only component with write access is the main command (and only to its own memory folder).
All web research happens in **isolated sub-agents** (`mentor:researcher`, `mentor:synthesizer`)
that can't write or execute — they only return text, treated as data. Web content is never
obeyed as instructions. See `plugins/mentor/commands/mentor.md` → `## Security`.

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
