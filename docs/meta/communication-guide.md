# Communication Guide: How to Talk to Claude Code

The quality of Claude's output is directly proportional to the quality of your instructions. This guide covers what works and what doesn't.

---

## The Mental Model

```
You (Human)                          Claude (AI)
─────────────                        ──────────
Vision & Goals          ──────>      Understands context via docs
Architecture Decisions  ──────>      Executes within constraints
Review & Course-Correct ──────>      Generates code, docs, plans
Domain Expertise        ──────>      Handles boilerplate + research
Quality Bar             ──────>      Follows your patterns consistently
```

**You are the architect. Claude is the builder.** This isn't a limitation — it's the model that produces the best results.

---

## Instruction Patterns

### For Features
```
"Build [feature] per [doc reference]. Follow [pattern] from arch.md. Use [design system/component library]."
```

### For Debugging
```
"/l3 [paste the exact error message or describe the symptom with specifics]"
```

### For Research
```
"/advise should we use X or Y for [use case]? Consider cost, complexity, and our current stack."
```

### For Refactoring
```
"Refactor [specific thing] to follow pattern #N from arch.md. Don't change behavior, just structure."
```

---

## Bad vs Good Instructions

| Bad | Why It Fails | Good |
|-----|-------------|------|
| "Add a settings page" | No spec, no constraints, no design reference | "Build settings per docs/features/settings.md. Use design tokens from globals.css. API routes follow Key Pattern #3 in arch.md." |
| "Fix the bug" | No error, no context, no reproduction steps | "/l3 TypeError: Cannot read 'name' of undefined — happens when clicking Save on /profile after clearing the form" |
| "Make it faster" | No measurement, no target, no scope | "The /api/dashboard route takes 3s. Profile it, identify the bottleneck, propose a fix. Target: under 500ms." |
| "Should we use Redis?" | No context, no constraints, no criteria | "/advise Redis vs Supabase realtime for session caching. Budget $25/mo, 2 users, Next.js + Supabase stack." |
| "Make it look better" | Subjective, no design system reference | "Apply the card pattern from design-system.md to the job list. Use --ext-bg-secondary for the card background." |
| "Add error handling" | Vague scope, over-engineering risk | "Add try/catch to the /api/generate route. On failure, return 500 with {error: message}. Log to console." |

---

## Style Rules to Set in CLAUDE.md

Tell Claude how you want responses formatted:

| Rule | Why |
|------|-----|
| Short responses — lead with the answer | You don't need a preamble before every answer |
| Tables over prose | Scannable, token-efficient, easier to compare |
| File references as `file_path:line_number` | Clickable navigation in most editors |
| No emojis unless requested | Professional, clean output |
| No trailing summaries | You can read the diff — don't recap what just happened |
| Diagrams for architecture | Visual flows > text descriptions |

---

## What to Never Do

- **Give vague instructions** ("make it better", "clean this up")
- **Let Claude decide architecture** without `/advise`
- **Skip reading arch.md** before a session
- **Batch many unrelated changes** in one request
- **Let Claude add features you didn't ask for**
- **Accept code you don't understand** — if you can't explain it, don't ship it

---

## The Progression

Most people start at Level 1 and should aim for Level 3:

| Level | How You Work | Quality |
|-------|-------------|---------|
| 1. Vibe coding | "Build me an app" → accept whatever comes out | Low — works for demos, breaks in production |
| 2. Directed coding | Feature-by-feature instructions with some references | Medium — functional but inconsistent |
| 3. Structured system | PRD → arch.md → skill-driven workflow → doc references in every instruction | High — production-grade, maintainable |

This kit is designed to get you to Level 3.
