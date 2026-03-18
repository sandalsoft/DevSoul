---
name: flow-next-plan defaults
description: User's preferred defaults for flow-next-plan - deep depth, repo-scout research, codex review
type: feedback
---

When using flow-next:plan, always apply these defaults (set via flowctl config in each project):
- **Plan depth**: `deep` (comprehensive with phases, alternatives, rollout plan)
- **Research**: `grep` / repo-scout (faster)
- **Review**: `codex` CLI for Carmack-level review

**Why:** User wants to skip the setup questions every time and go straight to planning with these options.

**How to apply:** When setting up `.flow/` in a new project, run:
```bash
$FLOWCTL config set plan.depth deep
$FLOWCTL config set plan.research grep
$FLOWCTL config set review.backend codex
```
If a project already has `.flow/` but these aren't configured, proactively set them.
