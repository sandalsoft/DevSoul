# DevSoul

A living developer preference profile that AI agents consume as passive context. Every new conversation starts with your decisions already made — tech stack, design taste, testing philosophy, workflow patterns — so the agent focuses on what's actually new.

## The Problem

Every AI coding session starts from scratch. The agent asks the same questions: what framework? what test runner? tabs or spaces? You repeat yourself across dozens of sessions, and the agent still gets it wrong when you forget to mention something.

## How It Works

DevSoul captures how you build software into a single structured markdown file (`~/.claude/devsoul.md`) that loads into every agent session via `@~/.claude/devsoul.md` in your global CLAUDE.md.

The profile covers:

- **Tech Stack** — languages, frameworks, runtimes, deployment targets
- **Design & Styling** — aesthetics, color systems, component patterns, motion
- **Verbiage** — writing voice, AI-isms to avoid, tone rules
- **Testing** — frameworks, coverage philosophy, verification requirements
- **Data Modeling** — database defaults, schema patterns, migration approach
- **Communication** — how you want the agent to interact with you
- **Architecture** — API design, project structure, security patterns

Every preference carries a citation — the interview answer, project history, or skill usage log that backs it up. No guessing.

## Seeding

The initial profile is built from two sources:

1. **Developer interview** — explicit preferences stated directly
2. **History mining** — scanning memory files, skill usage logs, settings, and past project patterns for demonstrated preferences

Cross-referencing both sources catches the gap between what you say you prefer and what you actually do.

## Updating

Three mechanisms keep the profile current, in priority order:

1. **Auto-detection** — a Stop hook scans sessions for preference signals (tech choices, corrections, patterns) and proposes updates with citations
2. **Periodic check-in** — a `/devsoul-checkin` skill triggers every 5 sessions or on new projects, reviewing recent activity and asking targeted questions
3. **Correction-driven** — when you explicitly override a preference, the profile updates with a new citation

## Key Principle

DevSoul is **passive context**, not active scaffolding. The agent knows your preferences and applies them when building, but doesn't auto-scaffold without being asked. When a project's needs conflict with a preference, the agent flags it, explains why the alternative is better for this case, and asks.

## Project Structure

```
devsoul.md              # The profile (output of Phase 1)
DESIGN.md               # Full architecture spec
INTERVIEW-2026-03-18.md # Initial developer interview
TODO.md                 # Phased implementation plan
CLAUDE.md               # Project-level agent instructions
sources/                # Snapshots from developer's local env
  CLAUDE.md             #   Global Claude Code instructions
  settings.json         #   Hooks, permissions, tool config
  skill-usage.jsonl     #   Skill invocation log
  memories/             #   Memory files from past projects
  skills/               #   Installed skill definitions
template-patches/       # Patches for Claude project templates
```

## Status

Phase 1 (seeding) is complete. The initial `devsoul.md` has been generated from interview + history mining and is installed at `~/.claude/devsoul.md`.

Phases 2-5 (auto-detection, check-in system, correction handling, refinement) are planned but not yet built. See `TODO.md` for details.
