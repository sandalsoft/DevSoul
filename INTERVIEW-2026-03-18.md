# DevSoul Interview — 2026-03-18

> Initial interview to capture developer preferences and design the DevSoul system.

## Q1: What frustrates you today? What questions do you answer over and over?

**Answer:** The tech stack — Python or TypeScript, what framework for web apps. These are decisions I've already made and shouldn't have to re-state.

## Q2: Scope of preferences — what layers matter?

**Answer:**
- Tech defaults (SvelteKit, Tailwind v4, TypeScript, Vercel)
- Design taste (clean-web-design aesthetic, cornflower-blue palette, no emojis unless asked)
- Working style (communication preferences, autonomy level)
- **Testing philosophy**: Use the most popular test suite for the framework/language. Be comprehensive — create both unit tests and functional tests.
- **Data modeling**: Use PostgreSQL for everything, normalized according to best practices.

## Q3: Cross-agent scope?

**Answer:** Start with Claude Code. Expand to other agents later if needed.

## Q4: History mining vs. forward capture?

**Answer:** Both. Interview the user periodically, especially when patterns shift.

## Q5: How should the system stay current?

**Answer:** All three mechanisms, prioritized:
1. **Auto-detection** (preferred) — detect from behavior
2. **Periodic check-ins** — catch drift before it accumulates
3. **Correction-driven** — update when explicitly corrected

Bias toward aggressive auto-detection with frequent check-ins to catch issues early.

## Q6: Tech stack defaults — verification

**Confirmed preferences:**
- **Web apps**: SvelteKit + Tailwind v4 + TypeScript
- **Backend**: TypeScript preferred for all backend, except where Python is absolutely a better fit
- **Database**: PostgreSQL always, normalized. But if a clearly better database is suited for the project (e.g., iOS app where local Postgres isn't practical), ask the user — don't silently override.
- **Deployment**: Vercel
- **Styling**: clean-web-design skill aesthetic, shadcn/ui-inspired components
- **Testing**: Vitest for JS/TS, pytest for Python, comprehensive coverage (unit + functional)

## Q7: Storage format — the soul file

**Answer:** Structured markdown (`~/.claude/devsoul.md`) with citation-like references. Each preference should explain *why* the system believes it, with evidence. Example: "Adding X to devsoul.md because qmd skill was used 8 times in the JSONL logs."

## Q8: Auto-detection aggressiveness

**Answer:** Aggressive, with more frequent check-ins to catch issues before they add up.

## Q9: Interview cadence

**Answer:** Every 5 sessions, and when a new project is started.

## Q10: Ideal experience in 3 months

**Answer:** All non-project-feature related details are inferred and started. When saying "build me X," the agent already knows the stack, the patterns, the style — and only asks about what's unique to X.

## Q11: Database nuance

**Answer:** Default to Postgres. But if a better database is absolutely suited for the project, ask the user if they still prefer Postgres. Example: iOS app where local Postgres isn't the best option.

## Q12: Passive vs. active?

**Answer:** Passive context. The agent knows preferences and applies them when building, but doesn't auto-scaffold without being asked.

## Q13: Conflict resolution

**Answer:** Flag it and ask for clarification. Include why you think the non-default is the better option for the project.

## Q14: Scope boundaries

**Answer:** Exclude project-specific state, credentials/secrets. Those belong in CLAUDE.md and memory files.

## Q15: Architecture confirmation

**Answer:** Confirmed the five-component architecture:
1. `~/.claude/devsoul.md` — the soul file
2. Stop hook enhancement — detect preference signals
3. `/devsoul-checkin` skill — periodic interview
4. Session counter — track sessions since last check-in
5. CLAUDE.md integration — load soul into every session
