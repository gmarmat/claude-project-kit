# Claude Code Cheat Sheet

One-page quick reference. Pin this.

---

## Session Workflow (Every Time)

```
/startnow           → Load project context
[build features]    → One at a time, from PRD
commit              → After each sub-task
/updatenow          → Update docs
```

## Core Skills

| Skill | When | What It Does |
|-------|------|-------------|
| `/startnow` | Start of session | Loads arch.md, CLAUDE.md, git status, memory |
| `/updatenow` | After any change | Updates arch.md, feature docs, version history |
| `/advise [topic]` | Before decisions | Researches options, presents comparison table |
| `/l3 [error]` | When broken | Systematic debugging with root cause analysis |
| `/audit [area]` | Before launch | Security, cost, performance, quality check |
| `/localcompact` | arch.md too long | Trims back under 300 lines |

## Document Hierarchy

```
CLAUDE.md           = Rules (read every session, keep short)
docs/arch.md        = Architecture index (<300 lines)
docs/PRD.md         = Requirements & vision (no limit)
docs/features/*.md  = Deep dives per feature (verbose OK)
docs/plans/*.md     = Research & decisions (dated)
```

## How to Give Good Instructions

| Bad | Good |
|-----|------|
| "Add a login page" | "Build login per docs/features/auth.md, use Supabase Auth magic links, follow design system in globals.css" |
| "Fix the bug" | "/l3 TypeError: Cannot read properties of undefined at api/generate line 45" |
| "Should we use Redis?" | "/advise Redis vs Supabase realtime for caching. Budget $25/mo, stack is Next.js + Supabase" |
| "Make it better" | "Refactor the video pipeline to follow Key Pattern #7 in arch.md. Don't change behavior." |

## The Build Loop

```
/startnow → Review feature index → /advise (if needed) → Build → Test → Commit → /updatenow → Repeat
```

## Golden Rules

1. **Docs before code** — PRD → arch.md → then build
2. **Tables over prose** — everywhere, always
3. **Commit frequently** — after each sub-task, not at the end
4. **Research before deciding** — `/advise` before architecture choices
5. **Keep arch.md under 300 lines** — link to feature docs for details
6. **Update docs after changes** — `/updatenow` is not optional
7. **One feature at a time** — don't batch unrelated changes
8. **Reference specific docs** — point Claude to the right file, section, pattern

## Token Budget Reference

| Document | Line Budget | When to Update |
|----------|------------|----------------|
| CLAUDE.md | ~75 lines | When rules change |
| docs/arch.md | <300 lines | After every feature |
| docs/PRD.md | No limit | During planning |
| docs/features/*.md | No limit | During feature dev |
| docs/plans/*.md | No limit | When research is done |
| Skills (SKILL.md) | ~100-200 lines | When workflow changes |
