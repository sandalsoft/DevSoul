# Interior AI - Project Memory

## Project
SvelteKit 2.x + Svelte 5 interior design app. Redesigning from "Room Maker" prototype to "Interior AI" — split-panel layout with Gemini-3 + pin-drop annotation refinement.

## Key Architecture
- Epic: fn-1-26u (12 tasks, plan reviewed SHIP by Codex GPT 5.2)
- shadcn-svelte for UI (OKLCH tokens, not HSL)
- Gemini-3 Flash/Pro only (removing OpenAI)
- Migrating `@google/generative-ai` → `@google/genai`
- SSE streaming for generation progress
- localStorage + S3 hybrid persistence
- Pin-drop annotation with Canvas API compositing

## Critical Implementation Notes
- **Svelte 5 stores**: Use `.svelte.ts` extension for files with `$state`/`$derived` runes. Plain `.ts` won't be transformed.
- **Tailwind v4**: Use `@custom-variant dark (&:is(.dark *))` for dark mode.
- **Canvas retina**: Always handle `devicePixelRatio` — 2x dimensions, scale context.
- **Pin coordinates**: Store in normalized space (0-1000), map to/from display pixels. Min-distance in normalized space, not CSS px.
- **SSRF protection**: `downloadImage()` in image.ts needs scheme allowlist + private IP blocking before adding more endpoints.
- **Import aliases**: `$components`, `$utils`, `$server` configured. Add `$stores` in Task 1.

## Conventions
- Prettier: tabs, single quotes, no trailing commas, 100 printWidth
- ESLint: flat config with svelte plugin
- Vercel adapter with Node.js 22.x
- Path aliases in svelte.config.js

## Files to Reference
- `.flow/specs/fn-1-26u.md` — full epic spec
- `.claude/napkin.md` — review findings + decisions
- `2026-02-07-audit.md` — tech debt audit (42 items)
