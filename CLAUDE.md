# DevSoul Project

This project builds a living developer preference profile system for AI agent sessions.

## Context

- `DESIGN.md` — full architecture and design spec
- `INTERVIEW-2026-03-18.md` — initial interview with developer preferences
- `TODO.md` — phased implementation plan
- `sources/` — snapshot of the developer's local environment for history mining

## Sources Directory

All files in `sources/` are snapshots from the developer's local machine:

- `sources/CLAUDE.md` — global Claude Code instructions
- `sources/settings.json` — hooks, permissions, tool configuration
- `sources/skill-usage.jsonl` — skill invocation log with timestamps and projects
- `sources/memories/` — memory files from various projects (prefixed with project path)
- `sources/skills/` — SKILL.md files from all installed skills (named by skill)

## Current Task

**Phase 1**: Seed the initial `devsoul.md` file.

Read DESIGN.md and INTERVIEW-2026-03-18.md first to understand the system design and stated preferences.

Then mine `sources/` for demonstrated preferences:
- What tech stacks appear across projects?
- What patterns repeat in memory files?
- What skills are used most frequently (skill-usage.jsonl)?
- What hooks/tools are configured (settings.json)?
- What design/style preferences are evident?

Cross-reference mined data against interview answers. Every preference in the output needs a **citation** — what evidence supports it.

Output the seeded `devsoul.md` into this project root for review before the developer installs it to `~/.claude/devsoul.md`.
