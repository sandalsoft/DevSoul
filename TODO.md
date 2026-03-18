# DevSoul — Implementation TODO

## Phase 1: Foundation
- [ ] Seed `~/.claude/devsoul.md` from interview + history mining
- [ ] Add `@~/.claude/devsoul.md` reference to `~/.claude/CLAUDE.md`

## Phase 2: Auto-Detection
- [ ] Build Stop hook (or extend existing) to scan sessions for preference signals
- [ ] Define what "preference signals" look like (tech choices, corrections, patterns)
- [ ] Write proposed updates with citations to a staging area before applying

## Phase 3: Check-In System
- [ ] Create `/devsoul-checkin` skill
- [ ] Implement session counter (`~/.claude/devsoul-sessions.json`)
- [ ] Detect new project directories and trigger check-in

## Phase 4: Correction Handling
- [ ] Detect when user overrides a stated preference
- [ ] Update soul file with new citation
- [ ] Preserve historical context for preference evolution

## Phase 5: Refinement
- [ ] Tune auto-detection sensitivity based on real usage
- [ ] Evaluate check-in cadence (5 sessions may be too frequent or too rare)
- [ ] Consider cross-agent portability if expanding beyond Claude Code
