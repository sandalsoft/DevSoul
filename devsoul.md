# DevSoul — Developer Preference Profile

> Last seeded: 2026-03-18
> Source: Interview + history mining of memory files, skill-usage.jsonl, settings.json, installed skills

---

## Tech Stack

### Languages & Runtimes
- Default to **TypeScript** for all web and backend work
  > Source: Stated in interview (2026-03-18) — "TypeScript preferred for all backend, except where Python is absolutely a better fit"
- Use **Python** when it's clearly the better fit (data generation, ML, scripting)
  > Source: Stated in interview (2026-03-18); reinforced by KYC datagen project using Python generators (memories/AMEX-POV)
- Use **Go** for CLI/TUI tools (Bubble Tea framework, Charmbracelet lipgloss)
  > Source: Demonstrated in promptql-tui and tui-animations projects (memory files)

### Frontend Framework
- **SvelteKit** as the primary web framework
  > Source: Stated in interview (2026-03-18) — "SvelteKit + Tailwind v4 + TypeScript"; reinforced across claudeitor, Interior AI, and hot-claude projects (memory files); dedicated skills for sveltekit-data-flow, sveltekit-remote-functions, svelte-runes
- **Svelte 5** with runes (`$state`, `$derived`, `$effect`, `$props`) — not Svelte 4 syntax
  > Source: svelte-runes skill; claudeitor and Interior AI memory files reference Svelte 5 rune patterns
- **React 19** as secondary framework when project requires it (Server Components, `useActionState`)
  > Source: react-dev skill covers React 19 patterns; design-taste-frontend skill references React Server Components

### Styling
- **Tailwind CSS v4** via `@tailwindcss/vite` plugin (NOT PostCSS)
  > Source: Stated in interview (2026-03-18); tailwind-v4-shadcn skill documents 8 breaking changes from v3→v4; claudeitor memory confirms Vite plugin usage
- **shadcn/ui-inspired** component architecture (shadcn-svelte for Svelte projects)
  > Source: Stated in interview (2026-03-18) — "shadcn/ui-inspired components"; Interior AI memory confirms shadcn-svelte usage
- **OKLCH color tokens** (not HSL) for precision color management
  > Source: tailwind-v4-shadcn skill; Interior AI memory explicitly states "OKLCH color tokens (not HSL)"
- **Dark mode** as first-class feature via custom Tailwind variants
  > Source: clean-web-design skill; Interior AI memory references `@custom-variant dark (&:is(.dark *))`

### Deployment
- **Vercel** as default deployment target
  > Source: Stated in interview (2026-03-18); vercel-deployment skill installed; Node.js 22.x adapter referenced in claudeitor memory

### Visualization
- **D3.js** for custom data visualizations (over higher-level chart libraries)
  > Source: d3js skill installed; skill-usage.jsonl shows d3js usage (2026-03-16); claudeitor memory references D3 for visualization

### Data Validation
- **Zod** or **Valibot** (StandardSchemaV1) for schema validation
  > Source: react-dev skill uses Zod; sveltekit-remote-functions skill uses Valibot/StandardSchemaV1

---

## Design & Styling

### Aesthetic
- **Clean, distinctive, context-specific design** — not generic AI aesthetics
  > Source: clean-web-design skill; design-taste-frontend skill explicitly bans Inter, Roboto, purple gradients, "Acme Corp" placeholder names
- **Cornflower-blue palette** as default accent; restrained color use (mostly neutrals, single accent)
  > Source: Stated in interview (2026-03-18) — "cornflower-blue palette"; clean-web-design skill reinforces restrained accent usage
- **No emojis** in interfaces or code unless explicitly asked
  > Source: Stated in interview (2026-03-18) — "no emojis unless asked"; design-taste-frontend skill confirms "high-quality icons instead"

### Motion & Interaction
- **Spring physics** for animations (Framer Motion), not linear easing
  > Source: design-taste-frontend skill — MOTION_INTENSITY: 6, spring physics required
- **Micro-interactions** as a sign of quality; perpetual animations must be memoized for performance
  > Source: design-taste-frontend skill — "bento grid paradigms with perpetual micro-interactions"

### Typography & Layout
- Custom fonts preferred (never default to Inter/Roboto)
  > Source: design-taste-frontend skill bans generic font choices
- **Visual density: 4** (balanced, not cramped or sparse)
  > Source: design-taste-frontend skill baseline metrics — VISUAL_DENSITY: 4
- **Design variance: 8** (distinctive, high-quality, not template-feeling)
  > Source: design-taste-frontend skill baseline metrics — DESIGN_VARIANCE: 8

### Code Formatting
- Tabs for indentation, single quotes, no trailing commas, 100 char printWidth
  > Source: claudeitor memory — Prettier config with tabs, single quotes, no trailing commas, 100 printWidth

---

## Testing Philosophy

- Use the **most popular test framework** for the language/framework
  > Source: Stated in interview (2026-03-18) — "Use the most popular test suite for the framework/language"
- **Vitest** for JavaScript/TypeScript projects
  > Source: Stated in interview (2026-03-18) — "Vitest for JS/TS"
- **pytest** for Python projects
  > Source: Stated in interview (2026-03-18) — "pytest for Python"
- Write **both unit tests and functional tests** — be comprehensive
  > Source: Stated in interview (2026-03-18) — "comprehensive coverage (unit + functional)"; qa-test-planner skill treats QA as systematic discipline
- **Regression tests for API contracts** — detect field removal, schema drift
  > Source: promptql-tui memory — TestLookup queries catch removed fields; fixture-based testing in temp directories
- **Verify before committing** — tests and linting must pass
  > Source: commit-work skill requires verification before commit; qa-test-planner skill integrates automated + manual testing
- **Visual verification** for UI changes (screenshots compared before/after)
  > Source: claudeitor memory; CLAUDE.md best practices section

---

## Data Modeling

- **PostgreSQL** as the default database for everything
  > Source: Stated in interview (2026-03-18) — "PostgreSQL always, normalized"; reinforced across KYC datagen project (3-database architecture with pgcrypto, pg_trgm extensions)
- **Normalized schemas** following best practices (3NF baseline)
  > Source: Stated in interview (2026-03-18); database-schema-designer skill covers normalization, denormalization tradeoffs
- If a clearly better database exists for the project type, **flag it and ask** — don't silently override
  > Source: Stated in interview (2026-03-18) — "if a clearly better database is suited for the project, ask the user"
- **Schema-first design** — define the schema, then generate code from it
  > Source: KYC datagen memory — kyc_schema.json v2.0 drives DDL and Python generators
- **Cross-database references** documented as SQL comments, not enforced foreign keys
  > Source: KYC datagen memory — split database architecture with documented cross-DB references
- **Migration patterns** with zero-downtime deployment in mind
  > Source: database-schema-designer skill covers migration patterns and zero-downtime deployments

---

## Communication & Workflow

### Agent Interaction Style
- **Passive context** — the agent knows preferences and applies them, but doesn't auto-scaffold without being asked
  > Source: Stated in interview (2026-03-18) — "Passive context. The agent knows preferences and applies them when building, but doesn't auto-scaffold"
- **Flag conflicts and ask** — when a non-default choice is better, explain why and ask for confirmation
  > Source: Stated in interview (2026-03-18) — "Flag it and ask for clarification. Include why you think the non-default is the better option"
- **Aggressive auto-detection** with frequent check-ins to catch drift early
  > Source: Stated in interview (2026-03-18) — "Bias toward aggressive auto-detection with frequent check-ins"

### Planning & Execution
- **Plan-Research-Review-Code cadence** — deliberate phases, not ad-hoc coding
  > Source: flow-next workflow skills used in sequence (interview→plan→review→work) in skill-usage.jsonl (2026-03-16); CLAUDE.md emphasizes "Think Different → Plan Like Da Vinci → Craft → Iterate"
- **Visual thinking** — prefer diagrams and visual explanations for communicating architecture
  > Source: visual-explainer is the most-used skill (4 invocations in skill-usage.jsonl); mermaid-diagrams, excalidraw, draw-io, c4-architecture, napkin skills all installed

### Git Discipline
- **Conventional Commits** (`type(scope): message`) — split by concern, not by file
  > Source: commit-work skill requires Conventional Commits format; patch staging for mixed changes
- **Code review before ship** — Codex review required, SHIP status gates merge
  > Source: claudeitor memory — codex exec for "Carmack-level" reviews; flow-next workflow includes review phase

### Tool Preferences
- **CLI tools** for external service interaction (gh, flowctl, codex)
  > Source: settings.json shows dcg bash hook, skill-usage tracking hooks; memories reference flowctl, codex CLI usage
- **Skills and hooks** for repeatable workflows (not ad-hoc prompting)
  > Source: settings.json configures PreToolUse, PostToolUse, Stop, UserPromptSubmit hooks; 60+ skills installed
- **Local-first tools** when possible (qmd for search, not cloud-only dependencies)
  > Source: qmd skill for local markdown search; skill-usage.jsonl shows qmd usage

### Status Line & Observability
- Custom **status line** script for session context
  > Source: settings.json — `statusLine.command: "~/.claude/scripts/context-bar.sh"`
- **Skill usage tracking** via hooks on PostToolUse, Stop, and UserPromptSubmit
  > Source: settings.json — track-skill-usage.sh, track-skill-usage-stop.sh, track-skill-usage-prompt.sh hooks

---

## Architectural Patterns

### Project Structure
- **Modular file splitting** — avoid monolithic files; split by concern
  > Source: KYC datagen memory — explicit instruction to avoid monolithic files that Claude can't manage across steps
- **Path aliases** in tsconfig/svelte.config (`$components`, `$utils`, `$server`, `$stores`)
  > Source: claudeitor memory — path aliases configured for clean imports
- **Flat architecture** over deeply nested folders
  > Source: Inferred from project structures in memory files; SvelteKit route-based organization

### API Design
- **GraphQL** as primary API protocol (Hasura/PromptQL stack)
  > Source: promptql-tui and KYC datagen memories — GraphQL queries, DDN integration
- **Server-Side Events (SSE)** for streaming/real-time data
  > Source: claudeitor memory — sveltekit-sse for streaming pages; polling as fallback
- **Server-only data readers** — prevent client import of sensitive server code
  > Source: claudeitor memory — server-only patterns to protect API keys

### Security
- **API keys server-only** — never exposed to client
  > Source: claudeitor memory — "Bearer token authentication in headers (no API keys in client)"
- **SSRF protection** — scheme allowlist + private IP blocking
  > Source: claudeitor memory — SSRF protection in image.ts
- **Localhost-only binding** for dev tools (127.0.0.1, not 0.0.0.0)
  > Source: claudeitor memory — security enforcement for development servers

### Configuration
- **Experimental features enabled** — agent teams, LSP tool
  > Source: settings.json — CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1, ENABLE_LSP_TOOL=1
- **Plugins active**: git-workflow, flow-next, gopls-lsp, claude-mem, worktrunk, swift-lsp
  > Source: settings.json — enabledPlugins section
- **Model default**: Sonnet for general work; Opus for complex code/review tasks
  > Source: settings.json — `"model": "sonnet"`; memories reference model pinning by task type (Sonnet for assets, Opus for code)

---

## Installed Skills Inventory

> 60+ skills installed. Most frequently used (from skill-usage.jsonl, 2026-03-16 through 2026-03-17):

| Skill | Uses | Category |
|-------|------|----------|
| visual-explainer | 4 | Communication |
| flow-next-* (interview, plan, review, work) | 4 | Workflow |
| skill-creator | 2 | Meta/tooling |
| find-skills | 2 | Meta/tooling |
| d3js | 1 | Visualization |
| database-schema-designer | 1 | Data modeling |
| clean-web-design | 1 | Design |
| qmd | 1 | Knowledge search |
| napkin | 1 | Diagramming |

> Source: skill-usage.jsonl — 23 total invocations across 2 projects

---

## What This Profile Is NOT

- **Not project-specific state** — that belongs in project CLAUDE.md and memory files
- **Not credentials/secrets** — never stored here
- **Not active scaffolding** — informs decisions, doesn't auto-execute them
- **Not a replacement for CLAUDE.md** — CLAUDE.md has project rules, DevSoul has developer identity
