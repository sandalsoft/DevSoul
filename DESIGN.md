# DevSoul — Design Specification

> A living developer preference profile that agents consume as passive context, so every new conversation starts with 80% of decisions already made.

## Core Concept

DevSoul captures how a developer thinks about building software — tech stack defaults, design taste, testing philosophy, workflow preferences — and makes it available as passive context to any AI agent session. Instead of re-answering the same boilerplate questions every time, the agent already knows the developer and focuses only on project-specific decisions.

## Architecture

### The Soul File (`~/.claude/devsoul.md`)

Structured markdown, human-readable, consumable by any agent. Every preference carries a **citation** — why the system believes this preference exists.

```markdown
## Database
- Default to PostgreSQL, normalized schemas following best practices
  > Source: Stated in interview (2026-03-18), reinforced across 12 projects

- If a clearly better database exists for the project type (e.g., SQLite for iOS local storage), flag it and ask — don't silently override
  > Source: Stated in interview (2026-03-18)
```

**Sections:**
- Tech Stack (languages, frameworks, runtimes)
- Design & Styling (aesthetics, palette, component patterns)
- Testing Philosophy (frameworks, coverage expectations, unit + functional)
- Data Modeling (database choices, normalization, migration patterns)
- Communication & Workflow (how the developer likes to interact with agents)
- Architectural Patterns (API design, project structure, deployment)

### Behavior Model

DevSoul is **passive context**, not active scaffolding. The agent:
- Knows preferences and applies them when building
- Does NOT auto-scaffold projects without being asked
- Flags when a non-default choice would be better, with reasoning
- Asks for clarification on conflicts, never silently overrides

### Conflict Resolution

When a project's needs conflict with a stated preference:
1. Flag the conflict explicitly
2. Explain why the non-default is better for this specific case
3. Ask the developer for their preference
4. If the developer agrees to the non-default, note it as project-specific (don't update the soul)

## Three Update Mechanisms

Updates are prioritized in this order:

### 1. Auto-Detection (Primary)

A Stop hook scans each session for preference signals:
- Tech choices made (frameworks installed, languages used)
- Patterns followed (project structure, naming conventions)
- Corrections given ("no, use X instead of Y")
- Tools and skills used frequently

Bias toward aggressive detection with frequent check-ins to catch issues early.

**Proposed updates** are written with citations:
```markdown
- Prefer Vitest over Jest for TypeScript projects
  > Source: Auto-detected — chose Vitest in 5/5 recent TS projects (2026-03-01 through 2026-03-18)
```

### 2. Periodic Check-In (Secondary)

A `/devsoul-checkin` skill triggers:
- Every **5 sessions**
- When a **new project** is started (new working directory not seen before)

The check-in reviews recent activity and asks targeted questions about:
- Detected patterns that haven't been confirmed
- Preferences that may have shifted
- New domains or tools being explored

### 3. Correction-Driven (Tertiary)

When the developer explicitly overrides a preference:
- Update the soul file with the new preference
- Add citation referencing the correction
- Preserve the old preference as historical context if relevant

## Session Counter

A lightweight tracker (`~/.claude/devsoul-sessions.json`) counts sessions since last check-in:

```json
{
  "sessions_since_checkin": 3,
  "last_checkin": "2026-03-18T14:30:00Z",
  "known_projects": ["/Users/eric/Development/code/ProjectA", "..."]
}
```

## Integration

- `CLAUDE.md` references `@~/.claude/devsoul.md` so preferences load every session
- The soul file is agent-agnostic markdown — usable by any LLM-based tool
- Project-specific overrides live in project CLAUDE.md files, not in the soul

## What DevSoul Is NOT

- **Not project-specific state** — that belongs in CLAUDE.md and memory files
- **Not credentials/secrets** — never stored in the soul
- **Not active scaffolding** — it informs decisions, doesn't auto-execute them
- **Not a replacement for CLAUDE.md** — CLAUDE.md has project rules, DevSoul has developer identity

## Initial Seeding

The soul file is seeded from two sources:
1. **This interview** (2026-03-18) — explicit preferences stated by the developer
2. **History mining** — scanning past session transcripts, memory files, skill usage logs, and CLAUDE.md for demonstrated preferences
