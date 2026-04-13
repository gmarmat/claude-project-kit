# Token Budget Reference

Claude reads your project docs at the start of every session. Bloated docs waste context tokens — making Claude slower, less focused, and more expensive. This guide sets line budgets for every document type.

---

## The Principle

Every token Claude spends reading bloated docs is a token it can't use for reasoning about your code. **Optimize docs for Claude's reading, not human reading.**

| Strategy | How |
|----------|-----|
| Tables over prose | A 5-row table replaces 15 lines of paragraphs |
| Links over inline | `See [docs/features/auth.md]` beats 50 lines of auth details in arch.md |
| Grep-friendly headings | `## API Routes` not `## A Note About Our API Route Structure` |
| Self-contained sections | Each section stands alone — no forward references |
| Names only for env vars | List `DATABASE_URL=` — never include values |

---

## Document Line Budgets

| Document | Target | Hard Max | When to Update |
|----------|--------|----------|----------------|
| `CLAUDE.md` | ~50 lines | 100 lines | When rules change (rarely) |
| `docs/arch.md` | ~200 lines | 300 lines | After every feature completion |
| `docs/PRD.md` | No limit | — | During planning phase |
| `docs/features/*.md` | No limit | — | During feature development |
| `docs/plans/*.md` | No limit | — | When research is done |
| Skills (`SKILL.md`) | ~100 lines | 200 lines | When workflow changes |

---

## What to Do When arch.md Gets Too Long

Run `/localcompact`. It will:
1. Identify sections that grew beyond their budget
2. Extract verbose content into feature docs
3. Replace inline content with links
4. Preserve all information — nothing is lost, just reorganized

**Rule of thumb:** If a section in arch.md is longer than 20 lines, it should be a link to a feature doc.

---

## Read Frequency

Claude reads these files in this order at session start:

```
1. CLAUDE.md           ← Every session (rules + constraints)
2. docs/arch.md        ← Every session (architecture context)
3. Memory files        ← Every session (cross-session context)
4. git log             ← Every session (recent changes)
5. Config files        ← Every session (dependencies, env vars)
6. docs/features/*.md  ← Only when working on that feature
7. docs/plans/*.md     ← Only when referenced
```

Files 1-5 are read **every time**. Keep them lean. Files 6-7 are read on demand — they can be verbose.
