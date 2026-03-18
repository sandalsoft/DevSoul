# Claudeitor Project Memory

## Project Overview
- Coding activity dashboard reading from ~/.claude/ and git repos
- SvelteKit + Svelte 5 (runes), Tailwind v4 (@tailwindcss/vite), D3.js, TypeScript strict
- Localhost only, bound to 127.0.0.1, single-user, no auth
- Epic: fn-1-claudeitor-coding-activity-dashboard (15 tasks)

## Key Technical Decisions
- Tailwind v4: @tailwindcss/vite plugin (NOT PostCSS), CSS directives: @import, @source, @theme
- SSE via sveltekit-sse on Readout page ONLY; Live page uses polling
- Chokidar singleton watcher on globalThis (prevents HMR duplicates)
- Model ID mapping: multi-strategy (exact → regex → normalization → fallback)
- Split git caching: commit log by HEAD hash, working-tree status always fresh
- API key server-only: never exposed to client, returns hasApiKey boolean
- claudeitor.config.json in .gitignore, .example committed
- Bits UI Command for Cmd+K (cmdk-sv deprecated)
- Session replay MVP: messages+timestamps core, file diffs best-effort

## Data Sources
- ~/.claude/stats-cache.json: dailyActivity, modelUsage, hourCounts, totalSessions
- ~/.claude/readout-cost-cache.json: per-day per-model token usage
- ~/.claude/readout-pricing.json: model pricing (short names like "opus-4-5")
- ~/.claude/history.jsonl: session history (JSONL, ~235KB)
- ~/.claude/settings.json, skills/, agents/, plugins/, projects/

## Code Architecture
- Server-only readers in src/lib/server/claude/ (SvelteKit prevents client import)
- Shared types in src/lib/data/types.ts (safe for client)
- All readers accept optional claudeDir param for testability
- Tests use temp fixture directories (not real ~/.claude/)

## Codex Review Lessons (Pitfalls)
- NEVER return module-level mutable objects as defaults — use factory functions
- Model mapping cache must invalidate when pricing data changes
- Token-overlap matching can silently mismatch versions (use strict family+version)
- Derive model family names from pricing keys, don't hard-code
- Log warnings for malformed data (don't silently skip)

## Codex Review Fixes Applied
- Localhost enforcement (127.0.0.1 binding)
- Tailwind v4 integration specifics (@tailwindcss/vite)
- Split git caching (HEAD for logs, always-fresh for working tree)
- Robust model ID mapping (multi-strategy)
- API key security (.gitignore, server-only)
- SSE watcher singleton (globalThis)
- Live page scope (polling not SSE)
- Session replay MVP definition

## flowctl Usage
```bash
FLOWCTL="/Users/eric/.claude/plugins/cache/gmickel-claude-marketplace/flow-next/0.20.21/scripts/flowctl"
```
- Must use bash -c with proper quoting (zsh parse issues with parentheses in heredocs)
- Use Write tool for temp files, then pass to flowctl for complex content
